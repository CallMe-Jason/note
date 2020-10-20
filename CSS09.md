转换transform

移动translate （x,y) 1.不会影响其他元素的位置2.xy为百分比时是相对于自身3.对于行内元素是无效的

旋转rotate 1.默认围绕盒子的中心点2.transform-origin x y设置中心点

xy可以是left top bottom right

缩放scale (x,y) 1.xy表示坐标即宽度和高度，只写一个值时一样2.大于1是放大，小于1是缩小

综合写法：transform 先移动 后旋转 再缩小放大

动画animation

steps（）分几步来完成

1.先定义2.再调用

from to 相当于0%和100%

@keyframes move {from{}to{}}

简写：名称 持续时间 运动曲线 何时开始 播放次数 是否反方向 动画起始或结束的状态 （暂停一般写在hover里）



单标签不能用伪元素