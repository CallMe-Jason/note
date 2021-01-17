## 受控组件

```jsx
// React将state与表单元素值value绑定到一起，由state的值来控制
// 1.在state中添加一个状态，作为表单的Value的值
state = { txt: '' }
<input type="text" value={this.state.txt} />

// 2.给表单元素绑定change事件，将表单元素的值设置为state的值
<input type="text" value={this.state.txt}	onChange={ e=> this.setState({ txt: e.target.value })}/>
```

---

## 多表单元素变化

```js
// 给表单元素添加name属性
#名称与state相同
<input type="text" name="txt" onChange={this.handlerForm} />
  
// 根据表单元素类型获取对应值
  // 获取当前DOM对象
const target = e.target
	// 根据类型获取值
const value = target.type === 'checkbox' ? target.checked : target.value
	// 获取name
const name = target.name
  
// 在change事件处理程序中通过[name]来修改对应的state
handlerForm = e => {
  	const target = e.target
		const value = target.type === 'checkbox' ? target.checked : target.value
		const name = target.name
    // 改值
	  this.setState({
  	[name]: value
	})
}

#使用此方法时，可以不加value
```

---

## 非受控组件

```jsx
// 1.调用React.createRef()方法创建一个ref对象
constructor () {
  super()
  this.txtRef = React.createRef()
}

// 2.将创建好的ref对象添加到文本框中
<input type="text" ref={this.txtRef} />
<button onClick={this.getTxt}>获取文本框的值</button>

// 3.获取文本框的值
getTxt = () => {
  console.log(this.txtRef.current.value)
}
```

---

## 父组件向子组件传值

```jsx
// 接收传递给组件的数据
// 1.给组件传递数组
<Hello name='jack' age={19} />

// 2.接收数据--函数组件
function Hello(props) {
  console.log(props)
  return (<div>接收到的数据:{props.name}</div>)
}

// 2.接收数据--类组件
class Hello extends React.Component{
  render () {
    return (<div>接收到的数据: {this.props.age}</div>)
  }
}
#props是个对象，里面有所有传过来的值

// 特点1.可以给组件村阿迪任意类型的数据，包括函数
// 特点2.props是只读的对象，不能修改
// 特点3.使用类组件时，如果写了构造函数，应该将props传递给super()，否则无法在构造函数中使用props
constructor (props) {
  // 推荐
  super(props)
  console.log(this.props) 
}

```

---

## 子组件向父组件传值

```jsx
// 1.父组件提供一个回调函数（用于接收数据）
getChildMsg = (msg) => {
  console.log('接收到子组件的数据', msg)
}

// 2.将该函数作为属性的值，传递给子组件
render () {
  return (
    <div>
      子组件:<Child getMsg={this.getChildMsg} />
    </div>
    )
}

// 3.子组件通过props调用回调函数
state = { childMsg: 'React'}
handleClick = () => {
  this.props.getMsg(this.state.childMsg)
}
return (<button onClick={this.handleClick}>给父组件传递数据</button>)
```

---

## 兄弟传值

将共享状态/数据提升到最近的公共父组件中，由公共父组件管理这个状态，成为状态提升
公共父组件的职责：1.提升共享状态 2.提供操作共享状态的方法
要通讯的子组件只需要通过props接收状态或操作状态的方法

---

## 祖孙传值Context

```jsx
// 1.调用React.createContext()创建Provider（提供数据）和Consumer（消费数据）
const { provider, Consumer } = React.createContext()

// 2.使用Provider组件作为父节点,设置value属性，表示要传递的数据
<Provider value="pink">
      <div className="App">
        <Child1 />
      </div>
</Provider>

// 3.哪一层想要接收数据，就用Consumer进行包裹，在里面回调函中的参数就是传递过来的值
  <Consumer>
    <!--data为形参，可以变，但是箭头函数的主体为jsx语法，要有标签包起来或者return!-->
    {data => <span>data参数表示接收到的数据--{data}</span>}
  </Consumer>

#如果是两个抽离出来的文件要互相传值最好把React.createContext()方法也抽离为一个单独的组件再使用Provider和Consumer方法
// 导入react
import React from 'react'
// 创建变量接收React.createContext()方法
const myContext = React.createContext()
// 导出
export default myContext

// 使用
// 导入祖组件和孙组件
import contextApp from './context.js'

// 祖组件使用
 <contextApp.Provider value="red"></contextApp.Provider>
   
// 孙组件使用
 <contextApp.Consumer>
     {data => <span>{data}</span>}
 </contextApp.Consumer>
```

---

## props的深入

### Children属性

```jsx
// 可以是文本也可以是组件，还可以是函数

// ...省略组件的语法
return (
  <div>
  	{this.props.children}    <!--文本或者组件!-->
    {props.chidlren()}		<!--函数!-->
  </div>
)
ReactDOM.render(
	<App>
  	<Test />
  </App>
)
```

---

### props校验

```jsx
// 允许在创建组件的时候，就指定props的类型，格式等
// 1.安装包 prop-types
npm i prop-types

// 2.导入包
import propTypes from 'prop-types'

// 3.使用组件名.PropTypes = {}给组件添加校验规则
App.propTypes = {
  // 指定为数组
  colors: propTypes.Array
  // 必选的函数
 	colors: propTypes.func.isRequired
  // React元素
  colors: propTypes.element
  // 特定结构的对象：对象({area: '上海', price: 1999})
  colors: propTypes.shape({
	  area: propTypes.srting,
  	price: propTypes.number
})
}

#可以写在渲染ReactDOM.render()的上面
```

---

### props的默认值

```js
// 场景： 分页组件=> 每页显示条数
// 设置默认值
App.defaultProps = {
 pageSize: 10 
}
```

---

