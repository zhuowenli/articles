# React Native 101 (02)

React Native 看起来很像 React，只不过其基础组件是原生组件而非 web 组件。要理解 React Native 应用的基本结构，你可能需要了解一些基本的 React 的概念，比如 JSX 语法、组件、state 状态以及 props 属性等等。

如果你已经了解了 React ，可以跳过这章教程。

## JSX 语法

JSX 是一个看起来很像 XML 的 JavaScript 语法扩展。React 可以用来做简单的 JSX 句法转换。

### HTML 标签对比 React 组件

React 可以渲染 HTML 标签 (strings) 或 React 组件 (classes)。

要渲染 HTML 标签，只需在 JSX 里使用小写字母的标签名。

```jsx
const myDivElement = <div className="foo" />;

ReactDOM.render(myDivElement, document.getElementById('example'));
```

要渲染 React 组件，只需创建一个大写字母开头的本地变量。

```jsx
const MyComponent = React.createClass({/*...*/});
const myElement = <MyComponent someProperty={true} />;

ReactDOM.render(myElement, document.getElementById('example'));
```

React 的 JSX 使用大、小写的约定来区分本地组件的类和 HTML 标签。

> 注意：在 React Native 中只有原生组件，不要使用 HTML 标签。
>
> 由于 JSX 就是 JavaScript，一些标识符像 class 和 for 不建议作为 XML 属性名。作为替代，React DOM 使用 className 和 htmlFor 来做对应的属性。

### 转换（Transform）

JSX 把类 XML 的语法转成原生 JavaScript，XML 元素、属性和子节点被转换成 React.createElement 的参数。

输入JSX：

```jsx
const Nav = React.createClass({className: 'Nav'});
const app = <Nav color="blue" />;
```

输出 JavaScript：
```js
var Nav = React.createClass({
    displayName: "Nav",
    className: 'Nav'
});
var app = React.createElement(Nav, { color: "blue" });
```

注意，要想使用 `<Nav />`，`Nav` 变量一定要在作用区间内。

JSX 也支持使用 XML 语法定义子结点：

```jsx
const Nav = React.createClass({className: 'Nav'});
const Profile = React.createClass({className: 'Profile'});

const app = (
    <Nav color="blue">
        <Profile>click</Profile>
    </Nav>
);
```

输出 JavaScript：

```js
var Nav = React.createClass({
    displayName: 'Nav',
    className: 'Nav'
});
var Profile = React.createClass({
    displayName: 'Profile',
    className: 'Profile'
});

var app = React.createElement(
    Nav,
    { color: 'blue' },
    React.createElement(Profile, null, 'click')
);
```

### 注意事项

（1）JSX 语法的最外层，只能有一个节点。

```jsx
// 错误
let myTitle = <p>Hello</p><p>World</p>;
```

（2）JSX 语法中可以插入 JavaScript 代码，使用大括号包裹。

```jsx
let myTitle = <p>{'Hello ' + 'World'}</p>
```

更多 JSX 知识点可以阅读官方文档: [https://facebook.github.io/react/docs/jsx-in-depth.html](https://facebook.github.io/react/docs/jsx-in-depth.html)

> 以上内容你都可以在 [https://babeljs.io/repl/](https://babeljs.io/repl/) 中输入，并查看转换效果，快去尝试看看吧！

## React 组件

React 允许用户定义自己的组件：

```jsx
class MyComponent extends React.Component {
    render() {
        return (
            <h1>Hello, World!</h1>
        );
    }
}

ReactDOM.render(<MyComponent/>, document.getElementById('example'));
```

### 组件的参数

组件可以从外部传入参数，内部使用 `this.props` 获取参数。

```jsx
class MyComponent extends React.Component {
    render() {
        return (
            <h1
                className="title"
                style={{ color: this.props.color }}
            >Hello, World!</h1>
        );
    }
}

<MyComponent color="red" />,
```

### 组件的状态

组件往往会有内部状态，使用 `this.state` 表示。

```jsx
class Clock extends React.Component {
    constructor(props) {
        super(props);
        this.state = { date: new Date() };
    }

    render() {
        return (
            <div>
                <h1>Hello, world!</h1>
                <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
            </div>
        );
    }
}
```

### 组件的生命周期

React 为组件的不同生命阶段，提供了近十个钩子方法。

* `componentWillMount()`：组件加载前调用
* `componentDidMount()`：组件加载后调用
* `componentWillUpdate():` 组件更新前调用
* `componentDidUpdate():` 组件更新后调用
* `componentWillUnmount()`：组件卸载前调用
* `componentWillReceiveProps()`：组件接受新的参数时调用

我们可以利用这些钩子，自动完成一些操作。

> 更多 React 组件的知识点可以阅读官方文档:
> - [https://facebook.github.io/react/docs/components-and-props.html](https://facebook.github.io/react/docs/components-and-props.html)
> - [https://facebook.github.io/react/docs/state-and-lifecycle.html](https://facebook.github.io/react/docs/state-and-lifecycle.html)

## React 的核心思想

View 是 State 的输出。

```js
view = f(state)
```

上式中，`f`表示函数关系。只要 State 发生变化，View 也要随之变化。

React 的本质是将图形界面（GUI）函数化。

```jsx
const person = {
  name: "michel",
  age: 31
};

const App = ({ person }) => <h1>{ person.name }</h1>

ReactDOM.render(<App person={person} />, document.body);
```

## React 没有解决的问题

React 本身只是一个 DOM 的抽象层，使用组件构建虚拟 DOM。

如果开发大应用，还需要解决两个问题。

- 架构：大型应用程序应该如何组织代码？
- 通信：组件之间如何通信？

### 架构问题

React 只是视图层的解决方案，可以用于任何一种架构。

* MVC
* MVVM
* Observer
* Reactive
* ...

那么到底哪一种架构最合适 React ？

### 通信问题

组件会发生三种通信。

* 向子组件发消息
* 向父组件发消息
* 向其他组件发消息

React 只提供了一种通信手段：传参。对于大应用，很不方便。

### 状态的同步

通信的本质是状态的同步。

React 同步状态的基本方法：找到通信双方最近的共同父组件，通过它的 `state` ，使得子组件的状态保持同步。


