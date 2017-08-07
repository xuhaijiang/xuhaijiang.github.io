##### [node](https://nodejs.org/zh-cn/)

Node.js 是一个基于Chrome V8 引擎的 JavaScript 运行时。 Node.js 使用高效、轻量级的事件驱动、非阻塞 I/O 模型。Node.js 之生态系统是目前最大的开源包管理系统。

##### [webpack](https://webpack.js.org/)
webpack是一个现代javascript应用程序的模块打包器(module bundler)。当webpack处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成少量的bundle-通常只有一个，由游览器加载。
它是高度可配置的，四个核心概念：
- 入口(entry)
- 输出(output)
- loader
- 插件(plugins)

##### [vue](https://cn.vuejs.org/)
vue.js是一套构建用户界面的渐进式javascript框架

#### [express](http://www.expressjs.com.cn/)
基于node.js平台，快速、开放、极简的web开发框架

##### [koa](http://koajs.com/)
Koa是有express团队设计的新的web开发框架。它的目标提供一个更小，更具表现力和更强大的基础的Web应用程序和API

#### [thinkjs](https://thinkjs.org/)
web开发框架

##### [PostCSS ](http://postcss.org/)
用JavaScript转换CSS的工具

##### [autoprefixer](https://github.com/postcss/autoprefixer)
Google推荐的PostCSS plugin，用来解析CSS，设置CSS前缀规则

##### [babel](https://babeljs.io/)
一个JavaScript编译器，可以作为 ES6 转码器，可以将 ES6 代码转为 ES5 代码。
**示例：**
```
    // 转码前
    input.map(item => item + 1);

    // 转码后
    input.map(function (item) {
      return item + 1;
    });
```

##### [Traceur](https://github.com/google/traceur-compiler)
和babel类似，Google公司的转码器，也可以将 ES6 代码转为 ES5 代码

##### [chalk](https://github.com/chalk/chalk)
终端字符串输出样式设置

##### [semver](http://semver.org/lang/zh-CN/)
语义化的版本控制

##### [node-open](https://github.com/pwnall/node-open)
打开文件或网址，可跨平台
**示例：**
```
    var open = require("open");
    open("http://www.google.com");
```

##### [opn](https://github.com/sindresorhus/opn)
 类似 node-open 的功能

##### [npm](https://www.npmjs.com/)
npm是javascript包管理器，软件注册表。通过它让javascript开发者可以简单的分享和复用代码

##### [rimraf]()
node模块(插件)，可以递归删除文件

##### [cordova](http://cordova.apache.org/)
- 代码跨平台可重用
- 对离线场景的支持
- 访问本地设备API

##### [nodemon](http://nodemon.io/)
nodemon将监视nodemon启动目录中的文件，如果任何文件更改，nodemon将自动重新启动节点应用程序

##### [ESLint](https://eslint.org/)
静态检查代码的语法和风格，类似的还有[JSLint](http://jslint.com/)和[JSHint](http://jshint.com/)

##### [Mocha](http://mochajs.org/)
JavaScript 测试框架

















