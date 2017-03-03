[零基础JavaScript编码（一）](http://ife.baidu.com/course/detail/id/93)

**学习笔记:**

# innerText与重排

## innerText, textContent, innerHTML:

1. `textContent`可以获取所有元素节点的文本内容, 包括`<script>`和`<style>`中的, 而IE专属属性`innerText`不会获取.
2. `innerText`受样式影响, 不返回隐藏元素的文本, 而`textContent`会.
3. 因为`innerText`受样式影响, 所以改变后会触发重排(reflow), 而`textContent`不会触发.
4. `innerHTML`获取的是元素节点, 但很多人用`innerHTML`来获取或改变某个DOM元素的文本内容, 但实际上应该使用`textContent`, 这样就不会被解析为HTML, 对性能的影响较小, 还能避免XSS恶意程序的攻击.


## 重排

重排会重新安排页面的布局, 在一个元素节点中的重排指重新计算该元素的尺寸和位置, 并且会触发该元素子节点, 祖先元素的重排, 以及在出现在该元素之后的DOM元素的重排(下面有示例), 最后进行一次重绘(repaint). 重排是个很容易引起的现象, 但是对性能的影响很大, 在很多情况下相当于对整个页面的布局进行重新安排, 因此要尽量避免重排.

<**重绘:** 元素在页面中显示出来的样式发生改变, 就会引起重绘, 但此时元素的布局并未发生改变. 样式的改变的一些例子: 轮廓线(outline), 可见性(visibility), 背景颜色(background color).>

下列情况会引起重排:

- 插入, 移除, 更新DOM中的元素
- 改变页面内容, 如改变输入框中的文本
- 移动DOM元素
- 给DOM元素加动画效果
- 计算元素的样式值, 如offsetHeight或getComputedStyle
- 改变CSS样式
- 改变元素的className
- 添加或移除样式表
- 改变视窗大小
- 滚屏

```html
<body>
<div class=”error”>
	<h4>My Module</h4>
	<p><strong>Error:</strong>Description of the error…</p>
	<h5>Corrective action required:</h5>
	<ol>
		<li>Step one</li>
		<li>Step two</li>
	</ol>
</div>
</body>
```
在以上部分代码中, `<p></p>`的重排会引起子节点`<strong></strong>`, 祖先元素`<div class=”error”></div>`(和`<body></body>`[取决于浏览器]), 紧接其后的元素`<h5></h5>`和`<ol></ol>`的重排, 在Opera浏览器中, 大部分重排会引起页面的重新渲染.


## 参考

[innerText和textContent的区别](http://stackoverflow.com/questions/24427621/innertext-vs-innerhtml-vs-label-vs-text-vs-textcontent-vs-outertext)

[MDN - textContent](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent#Differences_from_innerText)

[reflow是什么](http://stackoverflow.com/questions/27637184/what-is-dom-reflow)

[reflow和repaint的区别](http://stackoverflow.com/questions/2549296/whats-the-difference-between-reflow-and-repaint)

[reflow, repaint与性能](http://www.stubbornella.org/content/2009/03/27/reflows-repaints-css-performance-making-your-JavaScript-slow/)
