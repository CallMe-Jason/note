## 排它思想

```js
var btns = document.querySelectorAll('button')
for (var i = 0; i < btns.length; i++) {
	btns[i].onclick = function () {
		for (var j = 0; j < btns.length; j++) {
			btns[j].style.backgroundColor = ''
           }
     this.style.backgroundColor = 'pink'
            }
        }
//使用两个for循环，执行点击的时候先让其他的背景颜色变为空，再设置点击的那个为想要的颜色
#案例 排它思想
```

---

## 全选反选

```js
:checked
//可以获取选中的个数
#案例 全选反选
```

---

## 操作标签自定义的属性

```js
标签对象.getAttribute('属性名')
//获取属性
标签对象.setAttribute('属性名','属性值')
//设置属性
标签对象.removeAttribute('属性名')
//删除属性
#案例 tab栏切换
```

---

## H5新增的自定义属性的方法(只支持ie11以上)

```html
<div date-index = '1'></div>
<!--H5规定自定义属性前面要加date- --!>
```

---

## 节点操作（更方便）

网页中所有的内容都是节点

### 利用节点层级关系获得元素

元素节点 nodeType 为1

属性节点 nodeType 为2

文本节点 nodeType 为3

在实际开发中，主要操作元素节点

#### 获取父元素

```js
子节点.parentNode
//得到的是离该节点最近的父元素/节点，如果找不到则返回为空，但是可叠加获得祖元素
```

#### 获取子节点

```js
父节点.childNodes//标准，可以获得空格等无用的节点
父节点.children//非标准
#常用，不会获得无用的节点

父节点.firstChild//获取第一个孩子 标准
父节点.lastChild//获取最后一个孩子 标准

父节点.firstElementChild//获取第一个孩子 
#只支持ie9以上
父节点.children[0]
#常用 
父节点.lastElementChild//获取最后一个孩子 
#只支持ie9以上
父节点.children[父节点.chilidren.length - 1]
#常用 
```

#### 下一个兄弟节点

```js
兄弟节点.nextSibling
```

#### 创建节点

```js
var liNode = document.createElement('节点名')
//创建节点名
liNode.innerHTML = '字符'
//字符
父对象.appendChild(要追加的子元素)
//追加节点,表示追加到某个父元素的最后面，有剪切的功能
父对象.insertBefore(要追加的元素，追加到谁的前面)
//追加到元素的前面，有剪切的功能
#案例 剪切功能
```

