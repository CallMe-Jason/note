## 模块化开发

把单独的一个功能封装到一个模块中，模块之中相互隔离，但是可以通过特定的接口公开内部成员

AMD和CMD适用于浏览器端的js模块化

CommonJS适用于服务器端的js模块化

---

## 通过配置babel体验ES6模块化

```js
1.npm install --save-dev @babel/core @babel/cli @babel/preset-env @babel/node
2.npm install --save @babel/polyfill
3.项目跟目录创建文件 babel.config.js
4.babel.config.js 文件内容如下方代码
5.通过 npx babel-node index.js 执行代码

const presets = [
["@babel/env", {
targets: {
edge: "17",
firefox: "60",
chrome: "67",
safari: "11.1"
}
}]
];
module.exports = { presets };
```

---

## ES6模块化的基本语法

### 默认导出与默认导入

```js
//默认导出语法export default默认导出的成员
let a = 10
let c = 20
let d = 30

function show(){
    console.log('1111111');
}
export default{//默认导出
    a,
    c,
    show
}

//默认导入语法import接收名称from'模块标识符'
import m1 from './m1'

#注意：在每个模块中只允许使用唯一的一次export,否则会报错
```

### 按需导出与按需导入

```js
// 向外按需导出变量 s1
export let s1 = 'aaa' 
// 向外按需导出变量 s2
export let s2 = 'ccc'
// 向外按需导出方法 say
export function say = function() {}

// 导入模块成员
import m1 { s1, s2 as ss2, say } from './m1.js'//as表示别名，在默认导入后接{}即可按需导入，可以一块写
console.log(s1) // 打印输出 aaa
console.log(ss2) // 打印输出 ccc
console.log(say) // 打印输出 [Function: say]
#在每个模块中，可以使用多次按需导出
```

---

## 直接导入并执行模块代码

```js
//导入
improt './m2.js'

//m2
for(let i = 0; i < 3; i++){
  console.log(i)
}
#可以直接执行引入的文件而不暴露里面的成员
```

---

## webpack配置

前端项目构建工具（打包工具）

在项目中安装和配置webpack

1.运行 npm install webpack webpack-cli –D 命令，安装 webpack 相关的包

2.在项目根目录中，创建名为 webpack.config.js 的 webpack 配置文件

3.在 webpack 的配置文件中，初始化如下基本配置：

```js
module.exports = {
  //编译模式 development开始模式
mode: 'development' // mode 用来指定构建模式
}
```

4.在 package.json 配置文件中的 scripts 节点下，新增 dev 脚本如下：

```js
"scripts": {
"dev": "webpack" // script 节点下的脚本，可以通过 npm run 执行
}
```

5.在终端中运行 npm run dev 命令，启动 webpack 进行项目打包。

---

## 配置打包的入口与出口

默认打包的入口文件为src=>index.js

默认打包的输出文件为dist=>main.js

```js
//修改打包的入口与出口，可以在webpack.config.js中新增以下信息
const path = require('path')
module.exports = {
  entry:path.join(__dirname,'./src/index.js'),//打包入口文件的路径
  output:{
    path:path.join(__dirname,'./dist'),//输出文件的存放路径
    filename:'bundle.js'//输出文件的名称
  }
}
```

---

## 配置webpack的自动打包功能

```js
1.运行 npm install webpack-dev-server –D 命令，安装支持项目自动打包的工具
2.修改 package.json -> scripts 中的 dev 命令如下：
"scripts": {
"dev": "webpack-dev-server" // script 节点下的脚本，可以通过 npm run 执行
}
3.将 src -> index.html 中，script 脚本的引用路径，修改为 "/buldle.js“
4.运行 npm run dev 命令，重新进行打包
5.在浏览器中访问 http://localhost:8080 地址，查看自动打包效果
```

---

## 配置html-webpack-plugin生成预览页面

```js
1.运行npm install html-webpack-plugin - D 命令，安装生成预览页面的插件

2.修改web pack.config.js文件头部区域

```

---

## 配置自动打包相关的参数

```js
// package.json中的配置
// --open 打包完成后自动打开浏览器页面
// --host 配置 IP 地址
// --port 配置端口
"scripts": {
"dev": "webpack-dev-server --open --host 127.0.0.1 --port 8888"
},
```

---

## webpack中的加载器

协助webpack打包处理特定的文件模块

### 基本使用

```js
//打包处理css文件
1.运行 npm i style-loader css-loader -D 命令，安装处理 css 文件的 loader
2.在 webpack.config.js 的 module -> rules 数组中，添加 loader 规则如下：
// 所有第三方文件模块的匹配规则
module: {
rules: [
{ test: /\.css$/, use: ['style-loader', 'css-loader'] }
] }
#其中，test 表示匹配的文件类型， use 表示对应要调用的 loader,use 数组中指定的 loader 顺序是固定的,多个 loader 的调用顺序是：从后往前调用


//打包处理less文件
1.运行npm i less-loader less -D命令
2.在webpack.config.js的module -> rules数组中，添加loader规则如下
//所有第三方文件模块的匹配规则
module: {
  rules: [
    {test: /\.less$/,use: ['style-loader','css-loader','less-loader']}
  ]
}
#要依赖于{ test: /\.css$/, use: ['style-loader', 'css-loader'] }


//打包处理scss文件
1.运行 npm i sass-loader node-sass -D 命令//node-sass是sass-loader的依赖项
2.在 webpack.config.js 的 module -> rules 数组中，添加 loader 规则如下：
// 所有第三方文件模块的匹配规则
module: {
rules: [
{ test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] }
] }
#安装 node-sass 失败时，大部分情况是因为网络原因，解决：项目根目录新建 .npmrc然后输入以下代码
phantomjs_cdnurl=http://cnpmjs.org/downloads
sass_binary_site=https://npm.taobao.org/mirrors/node-sass/
registry=https://registry.npm.taobao.org
```

---

## 配置postCSS自动添加css的兼容前缀

```js
1.运行npm i postcss-loader autoprefixer -D命令
2.在项目根目录中创建postcss的配置文件postcss.config.js，并初始化如下配置
const autoprefixer = require('autoprefixer')//导入自动添加前缀的插件
module.exports = {
  plugins: [autoprefixer]//挂载插件
}
3.在webpack.config.js的module -> rulus数组中，修改css的loader规则如下:
module: {
  rules: [
    {test:/\.css$/,use: ['style-loader','css-loader','postcss-loader']}
  ]
}
```

---

## 打包样式表中的图片和字体文件

```js
1.运行npm i url-loader file-loader -D命令
2.在webpack.config.js的module->rules数组中，添加loader规则如下：
module: {
  rules: [
    {test:/\.jpg|png|gif|bmp\ttf|eot|svg|woff|woff2$,use: 'url-loader?limit=16940'}
  ]
}
#?后面的limit为判断小于该大小则转化为base64
```

---

## 打包处理js文件中的高级语法

```js
1.安装babel转换器相关的包：npm i babel-loader @babel/core @babel/runtime -D
2.安装babel语法插件相关的包：npm i @babel/preset-env @babel/plugin-transform-runtime @babel/plugin-propsal-class-properties -D
3.在项目根目录中，创建babel配置文件babel.config.js并初始化基本配置如下：
module.exports = {
  presets: ['@babel/preset-env'],
  plugins: ['@babel/plugin-transform-runtime','@babel/plugin-proposal-class-properties']
}
4.在webpack.config.js的module->rules数组中，添加loader规则如下：
//exclude为排除项，表示babel-loader不需要处理node_modules中的js文件
{test:/\.js$/,use: 'babel-loader',exclude: /node_modules/}
```

---

## Vue单文件组件

### 传统组件的问题和解决方案

#### 问题：

1.全局定义的组件必须保证组件的名称不重复

2.字符串模版缺乏语法高亮，在HTML有很多行的时候，需要用到丑陋的\

3.不支持CSS意味着当HTML和JS组件化时，CSS明显被遗漏

4.没有构建步骤限制，只能使用HTML和ES5 JS，而不能使用与处理器（如babel）

#### 解决方案：

针对传统组件的问题，Vue提供了一个解决方案，使用单文件组件

---

## 单文件组成结构

```js
//template 组件的模版区域
//script 业务逻辑区
//style 样式区域

<template>
  //这里用于定义Vue组件的模版内容
</template>
<script>//这里用来定义Vue组件的业务逻辑
  export default {
data:(){return{}},//私有数据
methods:{}//处理函数
//其他业务逻辑
}
</script>
<style scoped>
  //这里用于定义组件的样式
</style>
```

---

## webpack中配置vue组件的加载器

```js
1.运行npm i vue-loader vue-template-compiler -D命令
2.在webpack.config.js配置文件中,添加vue-loader的配置项如下：
const VueLoaderPlugin = require('vue-loader/lib/plugin')
module.exports = {
  module: {
    rules: [
      //其他规则
      {test:/\.vue$/,loader:'vue-loader'}
    ]
  },
  plugins: [
    //其他插件
    new VueLoaderPlugin()//请确保引入这个插件
  ]
}
```

---

## 在webpack项目中使用vue

```js
1.运行npm i vue -S 安装vue
2.在src->index.js入口文件中，通过import Vue from 'vue'来导入vue构造函数
3.创建vue的实例对象，并制定要控制的el区域
4.通过render函数渲染App根组件
//1.导入Vue构造函数
import Vue from 'vue'
//2.导入App根组件
import App from './components/App.vue'
const vm = new Vue({
  //3.指定vm实例要控制的页面区域
  el:'#app',
  //4.通过render函数，把指定的组件渲染到el区域中
  render:h=>h{App}
})
```

---

## webpack打包发布

上线之前需要通过webpack将应用进行整体打包，可以通过package.json文件配置打包命令：

```js
//在packahe.age文件中配置webpack打包命令
//该命令默认加载项目根目录中的webpack.config.js配置文件
"script":{
  //用于打包的命令
  "build":"webpack -p",
   //用于开发调试的命令
   "dev":"webpack-dev-server --open --host 127.0.0.1 --port 3000"
}
```



