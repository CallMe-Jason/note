# React

用来写HTML页面，或构建WEB应用

---

## 特点

声明式

基于组件

学习一次，随处可用

---

## 使用

```js
// 1.安装react和react-dom这两个包
npm i react react-dom

// 2.引入js文件

// 3.创建React元素
<div id='root'></div>

// 参数1: 元素名称
// 参数2: 元素属性
// 参数3: 元素的子节点（内容）
const title = React.createElement('h1', null, 'Hello React')

#可以用此方法嵌套节点，但是结构复杂，一般不推荐

// 4.渲染React元素到页面中
// 参数1: 要渲染的React元素
// 参数2: 挂载点
ReactDOM.render(title, document.getElementById('root'))
```

---

## React脚手架

```js
// 初始化项目
npx create-react-app my-app

// 进入项目根目录

// 启动项目
npm start

#npx可以不先下载脚手架就用脚手架创建项目，提升命令行工具的使用体验
```

---

## 在脚手架中使用

```js
// 1.在index.js文件中引入
import React from 'react';
import ReactDOM from 'react-dom';

// 2.创建react元素
const title = React.createElement('h1', null, 'Hello React!!!')

// 3.渲染react元素
ReactDOM.render(title, document.getElementById('root'))
```

---

## JSX

在js中使用html，语法和html一样,它不是标准的ECMAScript语法，它是ECMAScript的语法拓展

```js
// 使用JSX创建react元素
const title = <h1>Hello JSX</h1>
```

---

## JSX使用的注意点

1.React元素的属性名使用驼峰命名法

2.特殊属性名

```js
// 如：
class => className
```

3.没有子节点的React元素可以使用单标签

4.推荐使用小括号包裹JSX,避免js自动插入分号的情况

```js
const dv = (
  <div>Hello World</div>
)
```

---

## 嵌入JS表达式

数据存储在JS中

```js
// 使用单花括号{}把数据嵌入到JSX中
const name = 'Jack'
const dv = (
	<div>你好，我叫：{name}</div>
)

// 支持嵌入各类数据类型
// 支持计算
// 支持三元表达式
// 支持嵌入JSX
// 支持嵌入函数

const say = () => 'Hi~'
const dd = (
	{say()}
)

#不能直接嵌入语句，如if,for,但是可以放在函数中，再嵌入函数，使用时要注意html语法，如不能在h1标签里嵌入h2标签
```

---

## JSX的条件渲染

```js 
// 可以通过语句、三元、逻辑与运算符实现条件渲染
const isLoading = true
const loadData = () => {
  if (isLoading) {
    return <div>loading...</div>
  }
  return <div>数据加载完成，此处显示加载后的数据</div>
}

// 逻辑与运算符
const loadData = () => {
  return isLoading && (<div>loading...</div>)
}
```

---

## JSX的列表渲染

```js
// 如果要渲染一组数据，应该使用数组的map()方法
const songs = [
  {id: 1, name: '痴心绝对'},
  {id: 2, name: '像我这样的人'},
  {id: 3, name: '南山南'}
]
const list = (
	<ul>
  // 在花括号中，把数组中的普通对象转换成JSX的react对象
  	{songs.map(item => <li key={item.id}>{item.name}</li>))}
  </ul>
)

#遍历谁给谁添加key属性,这里是吧数组的数据遍历给了li,所以把key给了li
```

---

## JSX的样式处理

### 行内样式--style

```js
<h1 style={{color: 'red', backgroundColor: 'skyblue'}}
	JSX的样式处理
</h1>

// 样式使用驼峰命名法
// 第一个花括号是对象，第二个是嵌入
```

### 类名--className（推荐）

```js
<h1 className="title">
  JSX的样式处理
</h1>
// 样式写到css文件中并引入就可以生效了
```

---

## 组件

使用React就是在使用组件

特点：可复用，独立，可组合

---

## 创建组件的方式

### 使用函数创建组件

```js
// 函数名称必须大写开头
// 函数组件必须有返回值，表示该组件的结构
// 如果返回null,则不会渲染任何内容
function Hello () {
  return (<div>这是我的第一个函数组件</div>)
}

// 使用箭头函数创建组件
const Hello = () => (<div>这是我的第一个函数组件</div>)
                     
// 把函数名作为标签名即可使用组件
ReactDOM.render(<Hello />, document.getElementById('root'))
```

### 使用类创建组件

```js
// 类名称必须大写开头
// 类组件应该继承React.Component父类，从而可以使用父类提供的方法
class Hello extends React.Component{
  // 类组件必须提供render()方法
  render() {
    // 如果返回值为null, 不渲染任何内容
    return (<div>这是我的第一个类组件</div>)
  }
}

// 渲染组件
ReactDOM.render(<Hello />, document.getElementById('root'))
```

---

## 抽离为独立的JS文件

```js
// 1.创建Hello.js

// 2.在Hello.js中导入React
import React from 'react'

// 3.创建组件（函数或者类）
class FirstComponent extends React.Component{
  render () {
    return (<div>这是我的第一个抽离的组件</div>)
  }
}

// 4.在Hello.js中导出该组件
export default FirstComponent

// 5.在index.js中导入Hello组件
import FirstComponent from './FirstComponent'

// 6.渲染组件
ReactDOM.render(<FirstComponent />, document.getElementById('root'))

```

---

## React事件处理

### 事件绑定

```js
// 和原生DOM相似,采用驼峰命名法
// 在类组件
class App extends React.Component {
  handleClick () {
    console.log('单击事件触发了')
  }
  render () {
    return (<button onClick={this.handleClick}>触发单击事件</button>)
  }
}

// 函数组件
function App () {
	function  handleClick () {
    console.log('单击事件触发了')
  }
  return <button onClick={handleClick}>触发了点击事件</button>
}
```

### 事件对象

```js
// 可以通过事件处理函数程序的参数获取到事件对象（合成事件/合成对象，兼容所有浏览器）
function hanleClick(e) {
  // 阻止浏览器的默认行为
  e.preventDefault()
  console.log('事件对象', e)
}

<a onClick={handleClick}>点我不会跳转</a>
```

---

## 有状态组件和无状态组件

函数组件又叫做无状态组件，类组件又叫做有状态组件

状态即数据(state)

函数组件没有自己的状态，只负责数据展示（静态效果）

类组件有自己的状态，负责更新UI，让页面动起来

---

## 组件中的state和setState()

### state

```js
// state状态就是数据，只能在组件内容实用，state的值是对象，表示一个组件中可以有多个数据
// 简写
...省略类
state = {
  count: 0
}

// 正常
...省略类
constructor () {
  super ()
  // 初始化state
  this.state = {
    count: 0
  }
}

// 使用
<h1>计算器： {this.state.count}</h1>
```

### setState()

```js
// 状态是可以改变的
// 在事件处理函数中使用
this.setState({
  count: this.state.count + 1
})
#setState()的作用：1.修改state 2.更新UI，思想：数据驱动视图
```

---

## 从JSX中抽离事件处理程序

### 要抽离需要先解决this指向问题

#### 1.箭头函数

利用箭头函数自身不绑定this的特点

```js
render () {
  return <button onClick={() => this.事件名()}></button>
}
```

#### 2.Function.prototype.bind()

```js
constructor () {
  this.事件名 = this.事件名.bind(this)
}
render () {
  return <button onClick={this.事件名}></button>
}
```

### 3.class的实例方法

```js
 clickDouble = () => {
    this.setState({
      count: this.state.count + 2
    })
  }

```



