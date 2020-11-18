 

# Vue（国产框架）

渐进式：
声明式渲染 => 组件系统 => 客户端路由 => 集中式状态管理 => 项目构建

---

## 基本使用

步骤 ：

1.需要体统标签用于填充数据

2.引入vue.js文件

3.使用vue语法

4.把vue提供的数据填充到标签里

```js
#html部分
<div id="app">{{msg}}</div>
#js部分
var vm = new Vue({
            el : '#app',//表明容器
            data : {//提供数据
                msg : 'Hello Vue'
            }
        })
//el:元素挂载的位置（值可以是css选择器或者DOM元素）
//data:模型数据（值是一个对象）
//差值表达式里支持进行简单的运算
```

原理：概述编译过程的概念（vue语法=>原生语法）

---

## 模版语法概述

### 1.差值表达式

```js
//双花括号
{{msg}}
```

### 2.指令

```js
//v-cloak防止闪动 先隐藏，再替换
//先在样式里设置
[v-cloak]{display:none}
//再添加到div里
<div v-cloak></div>

//v-text填充纯文本
<div v-text=msg></div>

//v-html填充html片段,可以解析html标签
<div v-html=msg></div>
#容易导致XSS跨站脚本攻击，使用需慎重，原则是本网站内部的数据可用

//v-pre填充原始信息 跳过编译过程
<div v-pre>{{msg}}</div>

```

#### 数据响应式

通过vm.msg可以更改信息

```js
//指令v-once只编译一次，即显示内容后不再具有响应式的功能，vm.msg不会再更改值
```

### 3.事件绑定		

#### 双向数据绑定

数据的变化会导致视图的变化，视图的变化同样会导致数据的变化

```js
//v-model指令可以绑定数据和视图
<input type="text" v-model="msg">
```

```js
//v-on指令
<input tupe='button' v-on:click='num++'>
  //简写
  <input tupe='button' @click='num++'>
```

#### 事件函数的调用方式

```js
//直接绑定函数名称
<button v-on:click='say'>Hello</button>
//调用函数
<button v-on:click='say()'>Hello</button>
```

#### 事件函数参数传递

```js
//$event是固定写法
<button v-on:click='say(参数1，参数2，$event)'>Hello</button>
//1.如果事件直接绑定函数名称那么默认会传递事件对象作为事件函数的第一个参数
//2.如果事件绑定函数调用，那么事件对象必须作为最后一个参数进行传递，并且事件对象的名称必须是固定的$event
```

#### 事件修饰符

```js
//.stop阻止冒泡
<a v-on:click.stop = 'handle1'></a>

//.prevent阻止默认事件
<a href='http://www.baidu.com' v-on:click.prevent='handle2'></a>

//.self只有自己被点击的时候才会触发
<a v-on:click.self = 'handle1'></a>

//.prevent.self会阻止默认行为（无论是自己点击还是子元素被点击冒泡上来的都会被阻止
<a v-on:click.prevent.self = 'handle1'></a>

//.self.prevent会阻止默认行为（阻止的只是自己点击的默认行为）
<a v-on:click.self.prevent = 'handle1'></a>
```

#### 按键修饰符

```js
//.enter回车键
<input type='text' v-on:keyup.enter='handleSubmit'></input>

//.delete删除键
<input type='text' v-on:keyup.delete='handleDelete'></input>
```

#### 自定义按键修饰符

```js
//自定义按键修饰符名字是自定义的，但对应的值必须是按键对应的kecode值
<input type='text' v-on:keyup.a='handle' v-model = 'info'>
  
Vue.config.keyCodes.aaa = 65
//不支持驼峰写法	
```

### 4.属性绑定

```js
//v-bind指令用法
<a v-bind:herf='url'>跳转</a>
//简写
<a href='url'>跳转</a>

<img v-bind:src='imagesSrc'>
//简写
<img :src = 'imagesSrc'
```

##### 绑定对象

```js
<ul v-bind:class = '{textColor : isColor,textSize : isSize}'
data : {
isColor : true
}
```

##### 绑定数组

```js
<style>
  .textColor{
    color : #000,
    background-color:#eef
  }
</style>
<ul class="box" :class="[classA, classB]">
 data : {
classA : 'textColor'
```



### 5.样式绑定

```js
<div v-bind:style='{color : activeColor,fontSize : fontSize}'>heelo</style>
```



### 6.分支循环结构

v-if多个元素通过条件判断展示或者隐藏某个元素，或者多个元素进行两个视图之间的切换

```html
<div id="app">
    <!-- 判断是否加载，如果为真，就加载，否则不加载 -->
    <span v-if="flag">
        如果flag为true则显示,false不显示!
    </span>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    const vm = new Vue({
        el: '#app',
        data: {
            flag: true
        }
    });
</script>
```

```html
<div id="app">
    <div v-if="type === 'A'">
        A
    </div>
    <!-- v-else-if 紧跟在 v-if 或 v-else-if 之后，表示 v-if 条件不成立时执行 -->
    <div v-else-if="type === 'B'">
        B
    </div>
    <div v-else-if="type === 'C'">
        C
    </div>
    <!-- v-else 紧跟在 v-if或 v-else-if 之后 -->
    <div v-else>
        Not A/B/C
    </div>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    const vm = new Vue({
        el: '#app',
        data: {
            type: 'C'
        }
    });
</script>
```

v-show和v-if的区别：

v-show本质就是标签display设置为none,控制隐藏，v-show只编译一次

v-if是动态的向DOM树内添加或者删除DOM元素，v-if切换有一个局部编译/卸载的过程

###### 循环结构v-for

```js
<div id="app">
    <ul>
        <li v-for="item in items">
            {{ item.message }}
        </li>

    </ul>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    const vm = new Vue({
        el: '#app',
        data: {
            items: [
                { message: 'Foo' },
                { message: 'Bar' }
            ]
        }
    });
</script>
#不推荐同时使用v-if和v-for
```

key的作用，每个节点做一个唯一的标识，为了高效的更新虚拟DOM

