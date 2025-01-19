html2canvas
===========

[主页](https://html2canvas.hertzen.com) | [下载](https://github.com/niklasvh/html2canvas/releases) | [问题](https://github.com/niklasvh/html2canvas/discussions/categories/q-a)

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/niklasvh/html2canvas?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge) 
![CI](https://github.com/niklasvh/html2canvas/workflows/CI/badge.svg?branch=master)
[![NPM Downloads](https://img.shields.io/npm/dm/html2canvas.svg)](https://www.npmjs.org/package/html2canvas)
[![NPM Version](https://img.shields.io/npm/v/html2canvas.svg)](https://www.npmjs.org/package/html2canvas)

#### JavaScript HTML 渲染器 

该脚本允许您直接在用户浏览器上将网页或部分网页生成为可编辑可打印的pdf。由于截图是基于 DOM 的，因此可能与实际表现不会 100% 一致，因为它不是进行实际的截图，而是基于页面上可用的信息构建截图。

### 它是如何工作的
该脚本通过读取 DOM 和应用于元素的不同样式，将当前页面渲染为画布图像。

它**不需要服务器端的任何渲染**，因为整个图像是在**客户端浏览器**上创建的。但是，由于它严重依赖于浏览器，因此该库*不适合*在 nodejs 中使用。
它也不会神奇地绕过任何浏览器内容策略限制，因此渲染跨域内容将需要[代理](https://github.com/niklasvh/html2canvas/wiki/Proxies)来将内容转换为[同源](http://en.wikipedia.org/wiki/Same_origin_policy)。

该脚本仍处于**非常实验性的状态**，因此我不建议在生产环境中使用它，也不建议开始用它构建应用程序，因为还会有重大更改。

### 浏览器兼容性

该库应该可以在以下浏览器上正常工作（需要 `Promise` polyfill）：

* Firefox 3.5+
* Google Chrome
* Opera 12+
* IE9+
* Safari 6+

由于每个 CSS 属性都需要手动构建才能支持，因此目前还有许多属性尚未得到支持。

### 使用方法

html2canvas 库使用 `Promise` 并期望它们在全局上下文中可用。如果您希望支持不原生支持 `Promise` 的[较旧浏览器](http://caniuse.com/#search=promise)，请在引入 `html2canvas` 之前包含一个 polyfill，比如 [es6-promise](https://github.com/jakearchibald/es6-promise)。

要使用 html2canvas 渲染一个 `element`，只需调用：
`html2canvas(element[, options]);`

该函数返回一个包含 `<canvas>` 元素的 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)。只需使用 `then` 向 promise 添加一个 promise 完成处理程序：

    html2canvas(document.body).then(function(canvas) {
        document.body.appendChild(canvas);
    });

### 构建

您可以在[这里](https://github.com/niklasvh/html2canvas/releases)下载已构建好的版本。

克隆 git 仓库：

    $ git clone git://github.com/niklasvh/html2canvas.git

安装依赖：

    $ npm install

构建浏览器包：

    $ npm run build

### 示例

有关更多信息和示例，请访问[主页](https://html2canvas.hertzen.com)或尝试[测试控制台](https://html2canvas.hertzen.com/tests/)。

### 贡献

如果您希望为项目做出贡献，请将拉取请求发送到 develop 分支。在提交任何更改之前，请尝试测试这些更改是否适用于所有支持的浏览器。如果某些 CSS 属性不受支持或不完整，请在提交任何代码更改之前也为其创建适当的测试。
