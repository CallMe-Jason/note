内部样式：

写在style里 

选择器是用来选中标签的

标签选择器：

标签+空格+{属性；

​					属性；}

类选择器：

.命名

标签+空格+class="命名"

适用class属性的值选中标签，class相当于标签的名字，可自己命名

一个class可以放多个 中间用空格隔开

类选择器是用的最频繁的选择器

id选择器：

格式 #id值{键值对}，id值不允许重复

id选择器使用较少，主要在js中使用

当应用多个选择器时有优先级：id选择器>class类∫选择器>标签选择器>通配符选择器

通配符选择器：

主要用于样式重制

*表示通配符选择器，可以选中任意标签



样式：

字体系列：

字体相关样式用font开头

font-family字体

font-sizi大小

font-weight粗细 bold/normal

font-style倾斜 italic/normal

可用font简写 style->weight->size->family

font:italic normal 100px 字体 其中大小和字体必须写

font:字体像素px/行高像素px

文本系列：

color颜色 text-align水平对齐 text-indent设置首行缩进 数字+em   text-decoration设置文本修饰线underline（下划线）line-through(删除线)   none取消链接里的下划线                                                                                                    line-height设置行高 40px;若不带单位，表示为font-size的倍数，font中有默认的line-height,当同时设置font和line-height需写在后面 高度包含上下两部分以及文字，且上下间隙相等，故可利用实现当行文字垂直居中

颜色表示法 16进制 rgb表示法 英文 



样式引入的其他方式：

行内样式表：<p style="color: pink; font-size: 12px;"></p>用于修改较少的情况

外部样式：

link rel="stylesheet" href="css页面地址"

css页面不用写style标签直接写选择器

