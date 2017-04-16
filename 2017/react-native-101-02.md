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

（2）JSX 语法中可以插入 JavaScript 代码，使用大括号。

```jsx
let myTitle = <p>{'Hello ' + 'World'}</p>
```
