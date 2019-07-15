# 搭建本地开发环境和工作空间

本指南讲解了如何使用 [Angular CLI 工具](https://www.angular.cn/cli)搭建你的 Angular 开发环境。包括：前提条件、安装 CLI、创建初始工作空间和入门应用，以及在本地运行这个应用来验证你的搭建成果。

学习 ANGULAR

如果你不熟悉 Angular，请参阅[快速上手](https://www.angular.cn/start)。在构建基本版在线商店应用的过程中，快速上手可以帮助你快速学习 Angular 的基本知识。它充分利用了 [StackBlitz](https://stackblitz.com/) 在线开发环境，因此在你准备就绪之前，都不需要建立本地环境。









## 前提条件

在开始之前，请确保你的开发环境中包括 `Node.js®` 和 npm 包管理器。





### Node.js

Angular 需要 `Node.js` 版本 10.9.0 或更高版本。

- 要检查你的版本，请在终端/控制台窗口中运行 `node -v` 。
- 要获取 `Node.js`，请转到 [nodejs.org](https://nodejs.org/)。





### npm 包管理器

Angular、Angular CLI 和 Angular 应用都依赖于 [npm 包](https://docs.npmjs.com/getting-started/what-is-npm)中提供的特性和功能。要想下载并安装 npm 包，你必须拥有一个 npm 包管理器。

本搭建指南使用 [npm 客户端](https://docs.npmjs.com/cli/install)命令行界面，`Node.js` 已经默认安装了它。

要检查你是否安装了 npm 客户端，请在终端/控制台窗口中运行 `npm -v` 。





## 第 1 步：安装 Angular CLI

你可以使用 Angular CLI 来创建项目、生成应用和库代码，以及执行各种持续开发任务，比如测试、打包和部署。

全局安装 Angular CLI。

要使用 `npm` 命令安装 CLI，请打开终端/控制台窗口，输入如下命令：

```
content_copynpm install -g @angular/cli
```





## 第 2 步：创建工作空间和初始应用

你要在 Angular [**工作区**](https://www.angular.cn/guide/glossary#workspace)的上下文中开发应用。

要创建一个新的工作空间和初始入门应用：

1. 运行 CLI 命令 `ng new` 并提供 `my-app` 名称作为参数，如下所示：

   `content_copyng new my-app`

2. `ng new` 命令会提示你提供要把哪些特性包含在初始应用中。按 Enter 或 Return 键可以接受默认值。

Angular CLI 会安装必要的 Angular npm 包和其他依赖包。这可能要花几分钟的时间。

CLI 会创建一个新的工作区和一个简单的欢迎应用，随时可以运行它。





## 第 3 步：运行应用

Angular CLI 中包含一个服务器，方便你在本地构建和提供应用。

1. 转到 workspace 文件夹（`my-app`）。
2. 使用 CLI 命令 `ng serve` 和 `--open` 选项来启动服务器。

```
content_copycd my-app ng serve --open
```

`ng serve` 命令会启动开发服务器、监视文件，并在这些文件发生更改时重建应用。

`--open`（或者只用 `-o` 缩写）选项会自动打开你的浏览器，并访问 `http://localhost:4200/`。

你的应用会跟你打招呼：

![Welcome to my-app!](https://www.angular.cn/generated/images/guide/setup-local/app-works.png)



## 下一步

- 如果你不熟悉 Angular，请参阅[快速起步](https://www.angular.cn/start)教程。在构建基本的在线商店应用的过程中，快速起步可以帮助你快速学习 Angular 的基本知识。

“快速起步”假设以 [StackBlitz](https://stackblitz.com/) 作为在线开发环境 。要了解如何将应用从 StackBlitz 导出到本地环境，请跳到[部署](https://www.angular.cn/start/deployment)部分。