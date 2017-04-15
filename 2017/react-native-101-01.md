# React Native 101 (一)

这篇文章会帮助你搭建基本的 React Native 开发环境，根据你所使用的操作系统、针对的目标平台不同，具体可能步骤有所不同。

笔者所用的操作系统一直都是 MacOS，并且同时开发安卓和 iOS 应用。所以该系列的教程都是基于 MacOS 下的，使用 Windows 系统的朋友们可以跟据文章内容做一些微小的调整。

> 当然作为一个程序员，我还是非常的希望你能使用 MacOS 进行程序开发，具体的好处这里就不进行赘述了，大家可以搜索到诸多相关帖子及社区讨论。

## Mac下环境搭建

### NodeJS

使用 Homebrew 来安装 Node.js

```bash
brew install node
```

> React Native 目前需要 NodeJS 5.0 或更高版本，笔者当前使用的版本号是：v6.9.3。

### Yarn 以及 React Native CLI

Yarn 是 Facebook 提供的替代 npm 的工具，可以加速 node 模块的下载，并缓存已下载的依赖文件。

React Native 提供的命令行工具可以用于执行创建、初始化、更新项目、运行打包服务（packager）等任务。

```bash
npm install -g yarn react-native-cli
```

国内下载失败的话，可以通过阿里提供的镜像来加速下载：

```bash
npm install -g yarn react-native-cli --registry https://registry.npm.taobao.org
```

安装完 yarn 后也可以设置镜像源：

```bash
yarn config set registry https://registry.npm.taobao.org --global
yarn config set disturl https://npm.taobao.org/dist --global
```

### Xcode

React Native 目前需要 Xcode 8.0 或更高版本。你可以通过 App Store 或是到Apple开发者官网上下载。这一步骤会同时安装 Xcode IDE 和 Xcode 的命令行工具。

### Android Studio

如果你需要开发安卓应用的话，可能还需要去下载 Android Studio 这个 IDE。假如你手上没有安卓设备，并且想在手机上预览效果的话，Android Studio 内置的 AVD(Android Virtual Devices) 就能提供很大的帮助了。

可以直接去 [Android开发者主页](https://developer.android.com/studio/index.html) 点击下载。

### 开发工具

Facebook 提供了一个基于 atom 的集成开发环境 [Nuclide](https://nuclide.io/)，可用于编写、运行和 调试React Native应用。

> 笔者有尝试了一下，这玩意并不是好用，所以还是更推荐大家来使用我现在正在使用的 [VS Code](https://code.visualstudio.com/)，来开发 React Native 应用。

以上，你开发所需要的各种环境就搭建完成了！

## 测试安装

```bash
react-native init MyApp
cd MyApp
react-native run-ios
```

> 提示：你可以使用--version参数创建指定版本的项目。例如react-native init MyApp --version 0.39.2。注意版本号必须精确到两个小数点。

你也可以双击目录下的 `ios/AwesomeProject.xcodeproj` 文件然后可以在 Xcode 中打开该工程，点击 Run 按钮进行调试。

如需查看安卓下的效果，可以执行：

```bash
react-native run-android
```

> 该命令需要连接安卓设备（调试模式）、或者事先打开安卓模拟器才能成功执行！
> 笔者在进行安卓开发、调试的过程中，踩了不少的坑，后面会给大家一一道来。

同样可以在 Android Studio 引入目录下的 `android` 工程，然后执行 Run App 进行调试。

现在你已经成功运行了项目，我们可以开始尝试动手改一改代码看看效果了：

- 使用你喜欢的编辑器打开 `index.ios.js` 并随便改上几行。
- 在 iOS Emulator 中按下 `⌘-R` 就可以刷新 APP 并看到你的最新修改！
