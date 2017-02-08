# 标准
#### 标签风格
```
<script src="module1.js"></script>
<script src="module2.js"></script>
```
###### 非模块化
###### 全局对象冲突
###### 加载顺序很重要
###### 需要解决模块/库的依赖问题
###### 大型项目中这个列表会很长且难以维护

#### CommonJs: 同步require
```
require("module");
require("../file.js");
exports.doStuff = function() {};
module.exports = someValue;
```
###### 服务端js中使用(nodejs)
###### 模块可重用
###### npm中已有大量此风格模块可供使用
###### 使用简单
###### 无法满足网络异步请求的需
###### 无法平行加载多个模块

#### AMD: 异步 require
```
require(["module", "../file"], function(module, file) { /* ... */ });
define("mymodule", ["dep1", "dep2"], function(d1, d2) {
  return someExportedValue;
});
```
###### 满足网络异步请求风格
###### 平行加载多个模块
###### 过渡编码，难以阅读和编写
###### 更像是一种变通方案

#### ES6 Modules
```
import "jquery";
export function doStuff() {}
module "localModule" {}
```
###### 易于静态分析
###### 基于ES，不会过时
###### 本地浏览器支持费时
###### 

# webpack
###### 模块分块传输，按需加载
###### 可加载stylesheets、images、webfonts、html模板、coffeescript、less 等其他类型脚本及样式文件

#### 常用命令

##### 编译
```
$ webpack ./entry.js bundle.js
```
###### entry.js作为入口js文件，将依赖的其他js模块写在其中，然后编译为bundle.js

##### css模块依赖
```
require("./style.css");
```
##### 配置文件

```
module.exports = {
    entry: "./entry.js",
    output: {
        path: __dirname,
        filename: "bundle.js"
    },
    module: {
        loaders: [
            { test: /\.css$/, loader: "style!css" }
        ]
    }
};
```
###### loaders 申明需要使用的加载器，用于识别js以外的文件
###### 使用配置文件之后，可直接使用webpack命令编译

##### 美化编译输出

```
webpack --progress --colors
```
###### 添加进度和颜色

##### WATCH MODE

```
webpack --watch
```
###### 对所有文件进行观察，如有改动，立刻编译

#### DEVELOPMENT SERVER

```
webpack-dev-server --progress --colors
```
###### 类似于watch mode，编译后会刷新网页
