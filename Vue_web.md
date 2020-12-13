## el-form组件上有三大重要的属性

```js
1.v-bind:model 用来双向数据绑定的

2.ref,用来获取el-form组件实例的

3.v-bind:rules,用来做表单的数据校验的
```

---

## 路由导航守卫

```js
router.beforeEach((to,from,next)=>{
  //to将要访问的路径
  //from代表从哪个路径跳转而来
  //next是一个函数，表示放行
	//next()表示放行，next('/login')强制跳转
})
```

---

## 高亮流程

```js
1.在data中定义activePath
2.把actiivePath给el-menu组件的default-active属性值
3.点击列表项的时候调用方法并传递当前的index
	3.1 激活高亮`this.activePath = 传递过来的index`
  3.2 保持高亮状态，把传递过来的index传递到本地		      `sessionStorgae.setItem('activePath',activePaht)`
4.在组件实例化之后应用本地存储的activePath,在created方法里面，this.activePath = sessionStorage.getItem('activePath')
```

---

## 渲染表格的注意点

```js
//data指定表格的数据源，要求是一个数组，数组里面是一个一个对象
//如果说后端返回给你的数据格式不是数组，你要想法办转换成需要的数据格式
<el-table :data="userlist">
  //label指定列头的文本
  //prop指定这一列需要展示的数据
  <el-table-column label="姓名" prop="username"></el-table-column>
</el-table>
```

---

## Scoped Css

问题：有的时候操作组件内部的样式斌不能生效

1.不使用scoped，但建议在当前组件的外部加一个自己的class,这样也不会对其他组件产生影响

```js
<style lang="less">
  .user-container .el-table {
    th{
      text-align: center
    }
  }
</style>
```

2.深度选择器

```js
<style lang="less" scoped>
  .el-table {
    /deep/ th {
      text-align: center
    }
  }
</style>
```

---

