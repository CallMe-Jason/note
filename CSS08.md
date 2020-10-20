 HTML5新增的特性

新增的标签

头部<header>导航栏 <nav>内容 <article>定义文档某个区域 <section>侧边栏标签<aside>尾部标签<footer>

新增的多媒体标签

音频<audio src>autoplay自动播放 controls显示播放控件 loop重复播放

视频<video src>autoplay自动播放 muted 静音播放 controls向用户显示播放控件 loop循环播放 poster加载等待时显示的图片

使用mp4

新增表单元素

nubmer tel search

新增表单属性：

required 必须有字段才能提交

placeholder 提示信息默认值将不显示（写属性时前面写两个冒号）

autofocu 页面加载完毕自动聚焦到表单

autocomplete off/on 记录打开关闭（默认为打开）

multiple 选择文件时可多选

CSS新增的特性:

新增属性选择器 input[type=text]根据不同的属性值

权重为10

class^=icon 选出以icon开头的元素

class$=icon选出以icon结尾的元素

class*=icon选出有icon的元素

结构伪类选择器 nth-child {

2n 2n+1 5n n+5 -n+5

}

nth-child会把所有的同级盒子都排序号

nth-of-type会把指定元素的盒子排列序号

伪元素选择器：(权重为1)

::after在元素内部的前面插入内容

::before在元素内部的后面插入内容



CSS3盒子模型：box-sizing:content-box(默认)无变化border-box盒子大小不会因为padding和border变化而变化

图片变模糊：filter:blur（5px)



子盒子永远比父盒子少80px  width:calc(100% - 80px);可以用+-*/计算

过渡：transition 1.过渡的属性2.花费时间3.运动曲线4.延迟变化

写多个属性时中间加逗号 或者属性变成all

display没有动画性 所以不能使用transition



