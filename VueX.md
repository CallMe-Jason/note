##  Vuex是实现组件之间数据共享的一种方案

1.能够在vuex中集中管理共享的数据，易于开发和后期维护

2.能高效的实现组件之间数据的共享

3.存在vuex中的数据都是响应式的，能够实时的保持数据与页面的同步

---

## 什么样的数据适合存储在vuex中？

一般情况下，只有组件之间共享的数据，才有必要存储到vuex中，对于组件中的私有数据，依旧存储在组件自身的data中即可

---

## vuex的基本使用

```js
//安装
npm i vuex --save

//导入
import Vuex from 'vuex'
Vue.use(Vuex)

//创建store对象
const store = new Vuex.store({
  //定义全局共享的实例	
  state:{
    count: 0
  }
})
  
//挂载
  new Vue({
  el:'#app',
  render:h=>h(app),
  router,
  store
})
```

---

## Vuex的核心概念

### 1.State

提供唯一的公共数据源，所有共享的数据都要统一放到store的state中进行存储

#### 第一种方式：

```js
this.$store.state.要共享的数据
#差值表达式中不用使用this
```

#### 第二种方式：

```js
1.从 vuex中按需导入mapState函数
import { mapState } from 'vuex'

2.将全局数据映射为当前组件的计算属性
computed: {
  ...mapState(['count'])
}
```

### 2.Mutation

用于变更store中的数据

#### 第一种方式：

```js
1.只能通过Mutation来变更store中的数据，不可以直接操作store中的数据
2.方便集中管理和后期维护
mutations: {
  add(state){
    //变更状态
    state.count++
  }
}
#----------------
//触发mutation
methods: {
  handel(){
    //触发mutations的一种方式	
    this.$store.commit('add')
  }
}
```

##### 触发mutations时传递参数：

```js
const store = new Vuex.store({
  state: {
    count: 0
  },
  mutations: {
    addN(state,step){
      //变更状态
      state.count += step
    }
  }
})

//触发mutation
methods: {
  handle(){
     this.$store.commit('addN',3)
  }
}
```

#### 第二种方式：

```js
import { mapMutations } from 'vuex'

//将指定的函数映射为当前组件的methods函数
methods: {
  ...mapMutation(['add',])
}
```

```js
#如何选择两种方式
在组件中需要用到的store中的state比较多的情况下，建议使用map的形式

#流程：

组件当中绑定事件=>

调用自己的方法=> 

方法里面进行commit 触发store中的mutations修改数据 => 

数据改变触发视图改变 
#注意：不要在mutations函数中执行异步操作
```

### 3.Action

用于处理异步任务，但是在action中还是要通过出发mutation的方式间接变更数据

#### 第一种方式：

```js
//定义action
const store = new Vuex.Store({
  //省略其他代码
  mutations: {
    add(state) {
      state.count++
    }
  },
  actions: {
    addAsync(context) {
      setTimeout(()=> {
        context.commit('add')
      },1000)
    }
  }
})
//dispatch触发action
 this.$store.dispatch('addAsync')

#actions不能修改数据，只有mutations中的函数才有修改store中数据的权利
```

携带参数

```js
//定义action
const store = new Vuex.Store({
  //省略其他代码
  mutations: {
    addN(state,step) {
      state.count += step
    }
  },
  actions: {
    addAsync(context,step) {
      setTimeout(()=> {
        context.commit('addN',step)
      },1000)
    }
  }
})
//dispatch触发action
 this.$store.dispatch('addAsync',5)

```

#### 第二种方式：

```js
import { mapActions } from 'vuex'
//通过刚才导入的mapActions函数，将需要的actions函数，映射为当前组件的methods方法
methods: {
   ...mapActions(['subAsync'])
}
```

### 4.Getter

用于对store中的数据进行加工处理形成新的数据

1.getter可以对store中已有的数据加工处理之后形成新的数据，类似于vue的计算属性

2.store中数据发生变化，getter的数据也会发生变化

#### 第一种方式：

```js
//定义getter
const store = new Vuex.Store({
  state: {
    count: 0
  },
  getters: {
    showNum: state=> {
      return '当前最新的数量是['+ state.count +']'
    }
  }
})

//第一种方式
this.$store.getters.名称
```

#### 第二种方式：

```js
import { mapGetters } from 'vuex'
computed: {
  ...mapGetters(['showNum'])
}
```

