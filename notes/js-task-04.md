[4. 基础JavaScript练习（一）](http://ife.baidu.com/course/detail/id/103)

[代码](https://github.com/icyfish/IFE2017/blob/master/js-task-04.html)

[Demo](https://icyfish.github.io/IFE2017/js-task-04.html)

**学习笔记:**

# 几种DOM方法

## appendChild

`node.appendChild(newnode);`

在父节点node下添加一个子节点newnode, 添加位置在原有子节点的末尾, 返回新添加的节点;

## insertBefore

`node.insertBefore(newnode, existingchild);`

在父节点node下, 已存在的子节点existingchild前添加一个子节点newnode, 返回插入的节点;

**将新建子节点置于父节点下首位:**
(父节点下需至少含有一个子节点)

`parent.insertBefore(new, parent.firstChild);`

**将新建子节点置于父节点下末尾:**
(相当于appendChild)

`parent.insertBefore(new, null);`


## nodeType

`var type = node.nodeType`;

节点类型, 用数字标识, 共有12种节点类型, 其中Element(元素)的nodeType为1, Attr(属性) = 2, Text(文本) = 3.

## childNodes

`var kids = node.childNodes;`

获取父节点node的第一层所有类型的子节点集合, 返回的是NodeList, 并非数组, 如果要转化成数组需要用`Array.from()`或者`...`(spread operator).

## children

`var children = node.children;`

获取父节点node下的所有第一层元素子节点.

## firstChild

`var child = node.firstChild;`

获取父节点node的第一层第一个子节点, 若不存在则返回null.

## firstElementChild

`var element = node.firstElementChild;`

获取父节点node的第一层第一个元素子节点.

## lastElementChild

`var element = node.lastElementChild;`

获取父节点node的第一层最后一个元素子节点.

## childElementCount

`var count = node.childElementCount;`

获取父节点node的第一层元素子节点个数, 相当于 `node.children.length`

## removeChild

`node.removeChild(oldnode);`

从父节点node中移除某个子节点oldnode, 返回被移除的节点.

## replaceChild

`node.replaceChild(newchild, existingchild);`

在父节点node下用newchild替换已存在子节点existingchild, 返回被移除的节点;

## createElement

`document.createElement([tagname]);`

在document下创建元素;

## createTextNode

`document.createTextNode('some text');`

在document下创建一个内容为'some text'的文字节点;

**用法:**

```js
var element = document.createElement('h1');

element.appendChild(document.createTextNode('some text'));

// 结果: <h1>some text</h1>
```
##参考:

[DOM Core](http://reference.sitepoint.com/javascript/domcore)
