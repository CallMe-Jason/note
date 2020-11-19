## 表单操作

input和单选，复选框用v-model获取

下拉多选时多加一个multiple="true"

```js
#html
<select v-model='occupation' multiple='true'>
  <option></option>
	<option></option>
	<option></option>
</select>
<textarea v-model='desc'></textarea>
#Vue
data : {
  occupation : ['2','3'],
   desc : 'nihao'
}
```

---

## 表单域修饰符

number:转换为数值

trim：去掉开始和结尾的空格

lazy：将input事件切换为change事件（即失去焦点）

---

## 自定义指令

```js
//定义
Vue.directive('focus',{
              inserted : function(el) {
  //获取元素的焦点,把这个指令写到哪里，el就是哪个元素
	el.focus()
}
              })

//使用
<input type='text' v-focus>
```

---

## 带参数的自定义指令

```js
Vue.directive('color',{
  bind : function(el,binding) {
	el.style.backgroundColor = binding.value.color
  }
})
```

操作样式相关的可以使用bind和inserted都行，操作行为相关的不要使用bind

---

## 局部生效指令

```js
 var vm = new Vue({
            el: '#app',
            data: {
                color : 'orange'
            },
            methods: {

            },
            directives : {
            //局部指令
						}
        })
 #只能在本组间中使用，有更多组件的话这个指令就不能使用了
```

---

## 计算属性

```js
//表达式的计算逻辑比较复杂的时候要使用此属性，使模版的内容更加简洁
var vm = new Vue({
            el: '#app',
            data: {
                color : 'orange'
            },
            methods: {

            },
  					computed : {
              reverseString : function(){
	//注意return
                return this.msg.split('').reverse().join()
              }
            }
   					
        })
```

面试：

计算属性是基于依赖的data中的数据进行缓存的，而方法不缓存，每次都要调用

即在计算属性中的结果会被缓存再此调用时直接打印出结果，而方法中则会每次都执行里面的代码

---

## 侦听器

```js
//处理异步或者开销较大的操作，如ajax和定时器可以使用侦听器
#html
 <div id="app">
        <input type="text" v-model="firstName">
        <input type="text" v-model="lastName">
        <div>{{fullName}}</div>
    </div>
#Vue
 var vm = new Vue({
            el : '#app',
            data : {
                firstName : 'CallMe',
                lastName : 'Jason',
                fullName : 'CallMe Jason'
            },
            methods : {

            },
            watch : {
                firstName : function(val){
                    this.fullName = val + ' ' + this.lastName
                },
                lastName : function(val){
                    this.fullName = this.firstName + ' ' + val
                },
            }
        })
```

---

## 过滤器

```js
//格式化数据，比如将字符串格式化为首字母大写，将日期格式化为指定格式等
Vue.filter('过滤器名称',function(value){
//过滤器业务
})

<div>{{msg | 过滤器名称}}</div>
```

## 带参数的过滤器

```js
//带参数的过滤器
Vue.filter('format',function(value,arg1){
  //value就是过滤器传递过来的参数
})

<div>{{date | format('abc')}}</div>
```

---

## 生命周期

### 主要阶段：

#### 挂载

```js
beforeCreate//实例初始化之后，但是这个阶段实例的data和methods是读不到的

created//可以访问data和methods,但是无法渲染

beforeMount//渲染之前被调用，但是不能获取渲染之后的内容

mounted//数据已经渲染到页面上了，可以通过this.$el.innerHTML获取到数据
#想尽早的使用data和methods可以把代码写到created里，可以做一些接口调用。想操作DOM并且操作渲染之后的数据，把代码写到mounted里面
```

#### 更新

```js
beforeUpdate//数据更新之前被调用

updated//数据更新之后被调用
```

#### 销毁

```js
beforeDestroy//数据销毁之前被调用

destroyed//数据销毁之后被调用
```

---

## 变异数组

```js
push()
pop()
shift()
unshift()
splice()
sort()
reverse()
//会影响到原数组，更改即产生视图的修改
```

## 替换数组

```js
filter()
concat()
slice()
//不会影响到原数组，会返回一个新的数组，想要更改到视图的需要赋值
```

---

## 修改响应式数据

```js
//通过下标
Vue.set(vm.list,2,'lemon')
vm.$set(vm.list,1,'lemon')

//通过键名
vm.$set(vm.info,'gender','male')
```

---

