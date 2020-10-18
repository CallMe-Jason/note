# 内容

1.为什么要创建对象 2.对象的创建方式 3.对象的访问方式 4.遍历对象

5.内置对象

## 1.为什么要创建对象

对象的作用也是用来保存数据的

### 变量，属性，函数，方法的区别

#### 变量和属性相同，都是用来储存数据的

但变量单独声明并赋值，使用的时候直接写变量名（单独存在）

属性在对象里面，不需要声明，使用的时候必须对象.属性（在对象里面的变量叫属性）

#### 函数和方法都是实现某种功能，做某件事

函数是单独声明并且调用的，是单独存在的

方法在对象里面，调用的时候对象.方法（在对象里的函数就叫方法）

## 2.对象的创建方式

### 字面量定义方式(常用)

```js
var obj = {
  uname:'张三',
  age:18,
  sex:'男'
}
//属性名 + 冒号
```

### new Object创建对象

```js
var obj = new Object() 
obj.uname = '张三丰'
obj.age = 18
obj.sayHello = function() {
console.log('打招呼')
}
```

### 构造函数创建对象(了解)

```js
function Star(uname,age,sex) {
	this.uname = uname;
  this.age = age;
  this.sex = sex;
  this.sing = function(song) {
  console.log(song)
  }
}
var ldh = new Star('刘德华',18,'男')
console.log(ldh.uname)
console.log(ldh.sex)
console.log(ldh['age'])
ldh.sing('冰雨')
```

## 3.对象的访问方式

### 字面量定义方式

```js
console.log(对象名.属性名)
console.log(对象名['属性名'])
//第二种方式当里面的属性名为变量时，即对象里没有这个属性名，赋值给了一个对象的时候，不用加引号
```

### new Object创建对象

```js
console(对象名.属性名)
console(对象名.方法名())
```

## 遍历对象

```js
//for...in循环遍历
for (var k in 对象名) {
  console.log(对象名[k])
}
//一般用k或者key 不能直接用k 否则它会输出属性而不是值
```

## 5.内置对象

不用new关键字，直接用

#### a.数学对象math

```js
//返回一组数字中的最大值
console.log(Math.max(v1,v2,v3))
//返回一组数字中的小值
console.log(Math.min(v1,v2,v3))
//向上取整
console.log(Math.ceil(8.1))
//向下取整
console.log(Math.floor(8.9))
//四舍五入
//写负数时需要注意，零点五的时候会往大了取，如-1.5时会取1
console.log(Math.round(4.6))
//绝对值
console.log(Math.abs(-10))
//返回0-1之间的一个随机数，包含零不包含1
console.log(Math.random())
```

#### b.时间对象

```js
//创建日期对象
var myDate = new Date()
//年
var y = myDate.getFullYear()
//月
var m = (myDate.getMonth()+1)
//日
var d = myDate.getDate()
//小时
var h = myDate.getHours()
//分钟
var f = myDate.getMinutes()
//秒
var s = myDate.getSeconds()
```

#### c.padStart

```js
//字符串对象，看看字符串的长度是否等于我们规定的长度，如果小于则在这个字符串最前面加这个方法的第二个参数。只能使用在字符中,在个位数字前加零要把数字转换为字符串
var res = num.toString().padStart(规定的长度 如： 2 + 逗号 + 在字符串前面加的东西)
```

#### d.时间戳

```js
//返回的是1970年到现在的总的毫秒数
var now = new Date()
var nowTime = now.getTime()
//案例  倒计时
```

#### e.检测是否为数组的方法instanceof

```js
console.log(arr instanceof Array)
//或者
console.log(Array.isArray(arr))
//返回为true或者fales
```

#### f.往数组里添加和删除元素的方法

```js
var arr = [1,2,3]
arr.push(4)
//在数组后面添加，长度加一，返回的结果是新数组的长度
#————————————————————————————————————————————————————
arr.unshift(0)
//在数组前面添加，长度加一，返回的结果是新数组的长度
#————————————————————————————————————————————————————
arr.pop()
//删除数组的最后一个元素，返回的是删除的元素
#————————————————————————————————————————————————————
arr.shift()
//删除数组的第一个元素，返回的是删除的元素
#————————————————————————————————————————————————————
.splice(参数1，参数2，参数3)
//第一个参数是下标，第二个参数是添加几个元素，第三个参数是添加的元素是什么
```

#### g.返回数组索引号的方法

```js
数组名.indexOf(元素)
//从前往后查找，如果有该元素则返回该元素的索引号，没有则返回-1
lastindexOf(元素)//从后往前查找
//案例 数组去重
```

#### h.根据字符返回位置

```js
var str = '字符串'
str.indexOf('要查找的字符',[起始位置])
```

#### i.根据位置返回字符

```js
var str = '字符串'
str.charAt(i) 		
//案例 遍历字符串
```

#### j.hasOwnProperty

```js
//用来检测对象里有没有该属性
对象名.hasOwnProperty('属性名')
//案例 统计出现最多字符和次数
```

#### k.截取字符串

```js
var str = 'javascript'
var index = str.indexOf('script')
//获取下标
var res = str.substr(index)
//.substr(第一个参数，第二个参数) 第一个参数表示开始下标，第二个参数表示截取的长度 要加[],可以不写，不写则表示截取到结尾
```

#### l.替换字符串

```js
replace(参数1，参数2)
//第一个参数为需要替换的字符，第二个参数为替换为什么
var str = 'hello美女'
var res = str.replace('hello','你好')
//遇到多个时只能替换第一个，想都替换可以用
#正则表达式
var reg = /hello/gi
//g表示global 译为全局
//i表示ignore 译为忽略大小写
var res = str.replace(reg,'你好')
```

#### m.分隔字符串

```js
spilt('分隔符号')
var str = '字符串1|字符串2|字符串3'
var arr = str.split('|')
//这样做可以把一个字符串分隔为数组
```

#### n.大小写

```js
需要转换的字母.toUpperCase()//小写变大写
需要转换的字母.toLowerCase()//大写变小写
```



