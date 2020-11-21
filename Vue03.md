## 组件

1.组件是Vue最强大的功能之一

2.组件可以拓展HTML元素，封装可重用的代码

---

## 全局组件注册语法

```js
//注册一个名为button-counter的新组件
Vue.component('button-counter',{
  data : function(){//必须是个函数
		return {//返回的必须是个对象
			count : 0//需要的数据
    }
  },
  template : '<button> v-on:click="count++">点击了{{count}}次.</button>',
  methods : {
    handle : function(){}
  }
})
```

## 组件的用法

```html
<div id='#app'>
  <button-counter></button-counter>
  <button-counter></button-counter>
  <button-counter></button-counter>
<!--  组件之间是相互独立的-->
</div>
```

## 注意事项：

1.data是个函数

2.组件模版的内容必须是单个的根元素

3.组件模版内容可以是模版字符串

## 组件的命名方式

```js
//短横线方式
Vue.component('my-component',{})

//驼峰方式
Vue.component('MyComponent',{})
<div id="app">
	<my-component></my-component>
</div>
#驼峰方式可以在命名时使用，但是在普通的标签模版中，必须使用短横线的方式使用组件
```

---

## 局部组件注册

```js
var ComponentA = {}
var ComponentB = {}
var ComponentC = {}
new Vue({
  el : '#app',
  components : {
		'component-a' : ComponentA,
    'component-b' : ComponentB,
    'component-c' : ComponentC,
  }
})
#局部组件只能在注册他的父组件中使用
```

---

## 组件间数据交互

---

### 父组件向子组件传值

```js
Vue.component('menu-item',{
	props : [title],
  template : '<div>{{title}}</div>'
})
#通过props接收传递过来的值

//父组件通过属性的方式将值传递给子组件
<menu-item title='来自父组件的数据'></menu-item>
<menu-item :title='title'></menu-item>
```

#### props属性名规则

1.在props中使用驼峰形式，模版中需要使用短横线的形式

2.字符串形式的模版中没有这个限制

#### props属性的值

1.字符串

2.数值

3.布尔

4.数组

5.对象

---

### 子组件向父组件传值

可以通过子组件改变父组件的数值，但是不推荐，因为props传递数据原则是单向数据流

1.通过自定义事件向父组件传递消息

```js
<button v-on:click='$emit("enlarge-text")'>扩大字体</button>
//通过给子组件一个$emit("自定义事件")
```

2.父组件监听子组件的事件

```js
<menu-item v-on:enlarge-text='fontSize += 0.1'></menu-item>
//同名的自定义事件在父组件并触发和执行相应的动作
```

3.通过自定义事件向父组件传递消息

```js
<button v-on:click='$emit("enlarge-text"，0.1)'>扩大字体</button>
//在$emit()中第二个参数为携带的参数
```

4.父组件监听子组件的事件

```js
<menu-item v-on:enlarge-text='fontSize += $event'></menu-item>
//传递给$event
```

---

### 非父子组件间传值

```js
//单独的实践中心管理组件间的通信
var eventHub = new Vue()

//监听事件与销毁事件
eventHub.$on('add-todo',addTodo)
eventHub.$off('add-todo')

//触发事件
eventHub.$emit('add-todo',id)
```

---

## 组件插槽

 父组件向子组件传递内容

1.插槽位置

```js
Vue.component('alert-box',{
  template : `<div>
	<strong>Error</strong>
	<slot></slot>
</div>`
})
```

2.插槽内容

```js
<alert-box>Something bad happened.</alert-box>
#如果传递内容了则会覆盖slot里的内容
```

## 具名插槽的用法

1.插槽定义

```js
<div class='container'>
  <header>
  <slot name='header'></slot>
</header>
<main>
    <slot></slot>
</main>
<footer>
    <slot name='footer'></slot>
</footer>
</div>
```

2.插槽内容

```js
<base-layout>
  <h1 slot='header'>标题内容</h1>
	<p>主要内容1</p>
	<p>主要内容2</p>
<p slot='footer'>底部内容</p>
</base-layout>

//同时把多条文本匹配到插槽中 template
<base-layout>
            <template slot="header">
                <p>标题信息1</p>
                <p>标题信息2</p>
            </template>
            <p>主要内容1</p>
            <p>主要内容2</p>
            <template slot="footer">
                <p>底部信息1</p>
                <p>底部信息2</p>
            </template>
        </base-layout>
```

## 作用域插槽

父组件对子组件的内容进行加工处理

1.插槽定义

```js
<ul>
	<li v-for='e in list' v-bind:key='e.id'>
    <slot v-bind:e='e'>
      {{e.name}}
    </slot>
	</li>
</ul>
```

2.插槽内容

```js
<fruit-list v-bind:list='list'>
  <template slot-scope='slotProps'>//slot-scope可以得到子组件中绑定的属性
    <strong v-if='slotProps.item.current'>
      {{slotProps.item.text}}
    </strong>
	</template>
</fruit-list>
```



---

