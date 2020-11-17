 

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

### 4.属性绑定

### 5.样式绑定

### 6.分支循环结构