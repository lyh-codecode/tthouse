# 热更新

npm run start之后项目发生了什么？

为什么修改本地代码之后，页面也会马上改变？





# 打包过程

可以依赖webpack来进行项目的打包



## 1.初始化webpack配置

1.初始化项目，生成配置文件

```
npm init -y
```

2.安装webpack

```
npm install  webpack webpack-cli html-webpack-plugin -D
```

3.目录下创建webpack.config.js文件添加配置

```js
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname, "./dist"),
  },
  mode: "production",
  plugins: [
    new HtmlWebpackPlugin({
      template: "./index.html",
    }),
  ],
};

```



4.在package.json中的script添加,执行打包命令的

```
"build": "webpack"
```







## 2.创建入口文件

在index.js中构建好项目的结构和模块

在终端执行npm run build



根目录下会生成一个dist文件夹

* bundle.js
* index.html





基础打包的话不能监听代码的变更，增加watch

```
"build": "webpack --watch"
```

watch会监听文件变化，但是文件太多的时候会延迟项目的构建时间



如果配合webpack-dev-server可以解决这个问题





# webpack-dev-server是什么

`webpack-dev-server` 是一个用于开发环境的工具，它是 **Webpack** 的一个附加工具，主要用于提供快速的本地开发服务器和自动化刷新功能，极大地提升开发效率。它是前端开发流程中的一部分，通常与 **Webpack** 一起使用，来提供更方便的实时预览、自动重新加载等功能



## 1.本地服务器开发

会在本地启动一个http服务器，将项目托管到上面

我们可以通过浏览器访问项目



## 2.热更新

在项目中修改代码并保存，wds会监视文件的变化

自动重新编译相关的模块

通过热模块替换（HMR）功能，将新的代码推送到浏览器

无需刷整个页面，可以立即看到代码变动



## 3.自动刷新页面

修改的代码无法使用HMR更新，比如说HTML或者某些配置文件

wds会自动刷新浏览器，加载新的内容



## 4.支持代理

wds可以将特定的请求代理到其他服务器

使用wds可以将前端请求代理到后端服务



## 5.内存中的文件系统

开发模式下，wds会将编译后的文件保存在内存中，因此页面加载速度通常更快







## 6.使用流程

1.安装wds

```
npm install --save-dev webpack webpack-dev-server
```



2.package.json中添加

```
 "start": "webpack serve --open"
```



3.终端中执行

```
npm start
```



4.WDS会自动打开默认浏览器，默认端口为8080启动一个使用express的HTTP服务

这个服务器额和客户端采用WebSocket通信协议，当原始文件发生改变，WDS会实时编译，但是会index.html的修改不处理



当我们运行 `npm start` 的时候

也就是相当于运行 `node_modules/.bin/webpack-dev-server.cmd serve` 命令

并最终以 `webpack-dev-server/bin/webpack-dev-server.js` 就是整个命令行的入口

通过这里,它会自动给你开启 `webpack-cli`



































