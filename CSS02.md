复合选择器：

后代选择器：

ul li {}

元素1 元素2 {}

元素1和元素2中间用空格隔开，最终选择的是元素2作用于元素2

可一直往后增加

元素1和元素2可以是任意基础选择器

子元素选择器：

元素1>元素2 {}

元素1是父级，元素2是子级，最终选择元素2

必须是子元素

并集选择器：
元素1，

元素2 {}

可以用任何形式的选择器，包括后代选择器 中间加逗号，最后一个选择器不需要加逗号

伪类选择器：

a:link 选择所有未被访问的链接

a:visited 选择所有已访问过的链接

a:hover 选择鼠标指针位于其上的链接

a:active 选择活动链接

一定按上面按顺序写 一般只用hover

focus伪类选择器：

用于选取获得焦点的选择器 

input:focus {}

input得到光标时被选中

交集选择器：

同时利用多个条件选出标签

元素1元素2元素3

通常是类和类交集或类和标签交集



块元素：

独占一行；可以设置宽度，高度，内外边距；宽度默认时父级宽度的百分之百；可以放块元素或者行内元素（文字类的标签不能放块元素：p h1-h6

常见：div h1-6 p ul ol li dl dt dd table form 

行内元素：（内联元素）

不会独占一行，一行占满之后自动换行；相邻行内元素在一行上，一行可以显示多个；高宽设置无效；默认宽度就是他本身内容的宽度；行内元素只能容纳文本或者其他行内元素（链接里不能放链接，a里面可以放块级元素，此时通常会给a转换显示模式）

常见：span strong b em i del s u ins a label

行内块元素：

常见：img input td 

和相邻行内元素在一行上，但是他们之间会有空格，一行可以显示多个；本身宽度就是默认宽度；可以设置宽度和高度。

显示模式的转换：

行内元素转换为块级元素：display:block 

块级元素转换为行内元素：display:inline

转换为行内块：display:inline-block

 



背景颜色：background-color:transparent(透明的)

背景图片：background-image url/none

背景图片可以写字

img不可以

背景平铺：background-repeat

背景不平铺：background-repeat: no-repeat;

沿着x轴平铺：background-repeat:repeat-x

沿着y轴平铺：background-repeat:repeat-y

页面元素既可以放图片也可以放背景颜色，但图片会压住颜色

背景图片的位置：

background-position:x y;

xy为坐标，可以为方位名词（top center……）或者精确单位

方位名词时只写一个第二个默认居中

 也可以混合使用 混合使用时第一个值默认为x



固定背景：

background-attachment:scroll/fixed

fixed(不滚动) scroll默认（滚动）

不滚动时background-position会受影响

简写background：颜色 地址 平铺 滚动 位置

背景透明：

background: rgba(0,0,0,0);最后一个数为透明度，取值范围为0-1

