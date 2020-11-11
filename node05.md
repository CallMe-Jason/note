## 什么是数据库

数据库是用来组织，存储和管理数据的仓库

可以对数据进行增删改查等操作

---

## 常见的分类

MySQL数据库

Oracle数据库

SQL Server 数据库

Mongodb数据库

前三种是传统数据库，设计理念相同（关系型数据库）

### 关系型数据库

用来处理数据性强的

---

## Excel的数据组织结构

分别为工作簿=>工作表=>数据行=>列这四大部分组成

## 传统数据库的数据组织结构

在传统型数据库中组织结构分为 数据库=>数据表=>数据行=>字段

---

## 创建数据库

点击create a new schema创建数据库 

tables里创建表格

### DataType的数据

1.int 整数

2.varhcar(len)字符串

3.tinyint(1)布尔值

### 字段的特殊表示

1.PK主键，唯一的标识

2.NN值不允许为空

3.UQ值唯一

4.AI值自动增长	

---

## SQL三个关键点

1.SQL是一门数据库编程语言

2.使用SQL语言编程写出来的代码，叫做SQL语句

3.SQL语言只能在关系型数据库中使用

---

## SQL能做什么

增删改查

---

## SELECT语句

```js
SELECT * FROM 表名称
SELECT 列名称 FROM 表名称

//获取名为username和password的列的内容（从名为users的数据库表）
SELECT username,password FROM users
#查询
```

## INSERT INTO语句

```js
//用于向数据表中插入新的数据行
INSERT INTO users(username,password) values ('tony','233')
#添加
```

##  UPDATE语句

```js
UPDATE 表名称 SET 列名称 = '新值' WHERE 列名称 = 某值
//修改多个值时用逗号分开
#改
```

## DELETE语句

```js
DELETE FROM 表名称 WHERE 列名称 = 某值
#删
```

## WHERE子句

```js
//用于限定选择的标准，在SELECT，UPDATE，DELETE语句中皆可使用WHERE子句来限定标准
例 ： SELECT 列名称 FROM 表名称 WHERE 列 运算符 值
```

## AND和OR运算符

AND和OR可在WHERE子语句中把两个或多个条件结合起来

AND表示必须同时满足多个条件

OR表示只要满足一个条件即可

```js
SELECT * FROM users where status=0 and <3
SELECT * FROM users where status=1 or name='zs'
```

## ORDER BY 子句

用于根据指定的列对结果集进行排序

```js
//ASC表示升序，默认升序，DESC表示降序 
SELECT * FROM users ORDER BY status

//多重排序
SELECT * FROM users ORDER BY status DESC,username ASC
//对表中的数据先按照status降序排序，再按照username升序排序
```

## COUNT(*)

用于返回查询结果的总数据条数

```js
SELECT COUNT(*) FROM 表名称 WHERE status=0
```

##  用AS为列设置别名

```js
SELECT username as uname,password as upwd from users
//给username和password起了别名 
```

---

## 在项目中操作MySQL

1.导入

```js
const mysql = require('mysql')
```

2.建立与数据库的连接

```js
const db = mysql.createPool({
	host : '127.0.0.1',
  user : 'root',
  password : 'admin123',
  database : 'my_db_01'
})
```

3.测试mysql模块能否正常工作

```js
db.query('sleect 1',(err,results)=>{
	if(err) return console(err.message)
  console.log(results)
})
```

## 1.查询数据

```js
db.query('select * from users',(err,results) =>{
if(err) return console.log(err.message)
  console.log(results)
})
#如果执行的是select查询语句，返回的是个数组
```

## 2.插入数据

```js
//要插入到users表中的数据对象
const user = { username : 'Spider-Man',password : 'pcc321'}
//待执行的SQL语句，其中的？表示占位符
const sqlStr = 'INSERT INTO users (username,password) VALUES(?,?)'
//使用数组的形式，依次为？占位符指定具体的值
db.query(sqlStr,[user.username,user.password],(err,results) =>{
if(err) return console.log(err.message)//失败
  if(results.affectedRows === 1) {console.log('插入数据成功')}//成功
})


//便捷方式，向表中新增数据时，如果数据对象的每个属性和数据表的字段一一对应，则可以通过如下方式快速插入数据

//要插入到users表中的数据对象
const user = { username : 'Spider-Man',password : 'pcc321'}
//待执行的SQL语句，其中的？表示占位符
const sqlStr = 'INSERT INTO users SET ?'
//直接将数据对象当作占位符的值
db.query(sqlStr,user,(err,results) =>{
if(err) return console.log(err.message)//失败
  if(results.affectedRows === 1) {console.log('插入数据成功')}//成功
})
```

## 3.更新数据

```js
const user = {id : 7,username : 'aaa',password : '000'}
//要执行的SQL语句
const sqlStr = 'UPDATE users SET username=?,password=? WHERE id=?'
//调用db.query()执行SQL语句的同时，使用数组依次为占位符指定具体的位置
db.query(sqlStr,[user.username,user.password,user.id],(err,results)=>{
	if(err) return console.log(err.message)//失败
  if(results.affectedRows === 1) {console.log('更新数据成功')}//成功
})


//更新数据的便捷方式
const user = {id : 7,username : 'aaaa',password : '0000'}
//要执行的SQL语句
const sqlStr = 'UPDATE users SET ？ WHERE id=?'
//调用db.query()执行SQL语句的同时，使用数组依次为占位符指定具体的位置
db.query(sqlStr,[user,user.id],(err,results)=>{
	if(err) return console.log(err.message)//失败
  if(results.affectedRows === 1) {console.log('更新数据成功')}//成功
})
```

## 4.删除数据

```js
//通过id删除数据
const sqlStr = 'DELETE FROM users WHERE id=?'
//调用db.query()执行SQL语句的同时，为占位符指定具体的值
//注意：如果语句中有多个占位符，则必须使用数组为每个占位符指定具体的值。
//如果只有一个占位符，则可以省略数组
db.query(sqlStr,1,(err,results) => {
if(err) return console.log(err.message)	//失败
  if(results.affectedRows === 1) {console.log('删除数据成功')}//成功
})
```

## 5.标记删除

```js
//使用delete语句会真正的把数据删除，推荐使用标记删除的形式来模拟删除的动作，就是设置类似于status这样的状态字段来标记这条语句是否被删除。
//当用户执行了删除的动作时，我们并没有执行DELETE语句把数据删除掉，而是执行了UPDATE语句，标记为删除
const sqlStr = 'update users set status=? where id=?'
db.query(sqlStr,[1,6],(err,results)=>{
if(err) return console.log(err.message)
  if(results.affectedRows===1)
    console.log('标记删除成功')
})
```



---

