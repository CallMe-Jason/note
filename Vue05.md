# 路由

路由的本质就是对应关系

### 前端路由

概念：根据不同的用户事件，显示不同的页面内容

本质：用户事件与事件处理函数之间的对应关系

#### 前端路由负责事件监听，触发事件后，通过事件函数渲染不同内容

---

## 模拟路由

```html
<!--component可以当作是组件占位符-->
<component :is="comName"></component>

<!--监听window.onhashchang可以获取到最新的hash值-->
window.onhashchange = function() {
 switch(location.hash.slice(1)){
          case '/zhuye':
            vm.comName = 'zhuye'
            break
          case '/keji' :
            vm.comName = 'keji'
            break
          case '/caijing' : 
          vm.comName = 'caijing'
            break
          case '/yule' : 
          vm.comName = 'yule'
            break
        }
}
<!--可以通过hash来记住状态-->
```

---

## Vue Router

官方的路由模拟器 ( https://router.vue.js.org/zh/ )

包含的功能有：

1.支持HTML5历史模式或hash模式

2.支持嵌套路由

3.支持路由参数

4.编程式路由

5.支持命名路由

---

## vue-router的基本使用步骤

1.引入相关的库文件

先引入vue再引入router

2.添加路由链接

```js
//router-link会被渲染成a标签，to则是href
<router-link to='/user'>User</router-link>
```

3.路由占位符

```js
//路由进行匹配的时候，对应的组件放到这里
<router-view></router-view>
```

4.定义路由组件

```js
const User = {
  template : '<h1>User</h1>'
}
```

5.配置路由规则并创建路由实例

```js
const router = new VueRouter({
  //routers是路由规则数组
  routes : [
    //每个路由规则都是一个配置对象，其中至少包含path和component两个属性
    //path表示当前路由规则匹配的hash地址
    //component表示当前路由规则对应要展示的组件
    {path : '/user',component : User}
  ]
})
```

6.把路由挂载到Vue根实例中

```js
const vm = new Vue({
  el : '#app'
  data : {
  },
  	router//名字一样可以简写
})
```

---

## 路由重定向

用户在访问地址A的时候，强制用户跳转到地址C，从而展示特定的组件页面

通过redirect属性，制定一个新的路由地址

```js
//当访问/路径时，就会跳转到/user这个页面
{path : '/',redirect:'/user'}
```

---

## 嵌套路由

### 定义组件

```js
const Tab1 = {
            template : '<h2>tab1</h2>'
        }
const Tab2 = {
            template : '<h2>tab2</h2>'
        }
```

### 子级路由模版

```js
const regUser = {
template: `<div>
<h1>Register 组件</h1>
<hr/>
<router-link to="/regUser/tab1">Tab1</router-link>
<router-link to="/regUser/tab2">Tab2</router-link>
<!-- 子路由填充位置 --> 
<router-view/>
</div>`
}
```

### 嵌套路由配置

```js
const router = new VueRouter({
routes: [
{ path: '/user', component: User },
{
path: '/regUser',
component: Register,
// 通过 children 属性，为 /regUser 添加子路由规则
children: [
{ path: '/regUser/tab1', component: Tab1 },
{ path: '/regUser/tab2', component: Tab2 }
] } ]
})
```

---

## 动态路由匹配

通过动态路由参数的模式进行路由匹配

```js
const User = {
// 路由组件中通过$route.params获取路由参数
template: '<div>User {{ $route.params.id }}</div>'
}

var router = new VueRouter({
routes: [
// 动态路径参数 以冒号开头
{ path: '/user/:id', component: User }
]
})
```

---

## 路由组件传递参数

$router与对应路由形成高度耦合，不够灵活，所以可以使用props将组件和路由解耦

```js
#传递静态
const router = new VueRouter({
routes: [
// 如果 props 被设置为 true，route.params 将会被设置为组件属性
{ path: '/user/:id', component: User, props: true } ]
})
const User = {
props: ['id'], // 使用 props 接收路由参数
template: '<div>用户ID：{{ id }}</div>' // 使用路由参数
}

#传递对象
const router = new VueRouter({
routes: [
// 如果 props 是一个对象，它会被按原样设置为组件属性
{ path: '/user/:id', component: User, props: { uname: 'lisi', age: 12 }} ]
})
const User = {
props: ['uname', 'age'],//此时里面只能收到props中对象里包含的参数
template: ‘<div>用户信息：{{ uname + '---' + age}}</div>'
}

#传递函数
const router = new VueRouter({
routes: [
// 如果 props 是一个函数，则这个函数接收 route 对象为自己的形参
{ path: '/user/:id', 
component: User, 
props: route => ({ uname: 'zs', age: 20, id: route.params.id })} ]
})
const User = {
props: ['uname', 'age', 'id'],
template: ‘<div>用户信息：{{ uname + '---' + age + '---' + id}}</div>'
}
```

---

## 命名路由

为了更加方便的表示路由的路径，可以给路由规则起一个别名，即为命名路由

```js
const router = new VueRouter({
routes: [
{
path: '/user/:id',
name: 'user',
component: User
} ]
})

//组件 to前加冒号动态接收可以解析里面的对象
<router-link :to="{ name: 'user', params: { id: 123 }}">User</router-link>
```

---

## 编程式导航

声明式导航：通过点击链接实现导航的方式，叫做声明式导航

例如：通过标签跳转

编程式导航：通过调用js的api实现导航的方式

例如：普通网页中的location.href

```js
//常用的编程式导航api
this.$router.push('hash地址')
this.$router.go(n)

const User = {
template: '<div><button @click="goRegister">跳转到注册页面</button></div>',
methods: {
goRegister: function(){
// 用编程的方式控制路由跳转
this.$router.push('/register');
} } }

// 字符串(路径名称)
router.push('/home')
// 对象
router.push({ path: '/home' })
// 命名的路由(传递参数)
router.push({ name: '/user', params: { userId: 123 }})
// 带查询参数，变成 /register?uname=lisi
router.push({ path: '/register', query: { uname: 'lisi' }})

#注意 this.$route当路由规则匹配的时候，可以获取信息，this.$router是用来跳转的
```

