层叠性：（覆盖）

就近原则，离哪个标签近就作用于哪个标签

继承性：

子元素可以继承父元素的样式（部分）

继承的特例：
a h标签有自己的属性，继承时无法继承已有属性。

继承的权重是0

优先级：

选择器相同，则执行层叠性

选择器不同，则根据权重执行

通配符<元素<类<ID<行内<!important（最重要）

权重虽然会叠加，但是永远不会进位

盒子模型：

外边距：margin 

上右下左

相邻块元素垂直外边距的合并bottom和top取最大值，不会叠加

嵌套块元素垂直外边距的塌陷 父子关系的块元素给子元素定义时父元素也会塌陷 解决：1设置一个边框2指定一个内边距3为父元素添加overflow:hidden 推荐第三种

边框：border

粗细width，样式style：solid（实线）dotted（点线）dashed(虚线）颜色color 可以简写 

border-collapse：collapse表示相邻的边框会合并到一起

内边距：padding

边框与内容之间的距离 

只跟一个值表示4个方向一样

跟两个值表示上下是第一个，左右时第二个

跟三个值表示上是第一个，左右时第二个 下是第三个

跟四个值表示上右下左

一般盒子不设置宽度由padding撑开

如果没有指定宽度或者高度，则padding不会撑开盒子

内容

行内元素和行内块元素居中时需要在父级元素中添加text-align=center

块元素则是设置margin

清除内外边距：（也是css的第一句代码）

*{

margin:0;

padding:0;

}