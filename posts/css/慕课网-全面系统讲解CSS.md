# HTML基础知识

## H5的理解

H4之前，开发者非常随意，标签名、属性名使用大写，标签没有闭合等，W3C认为这样过于随意不行，所以推出了XML。

XML 的要求非常严格，标签名、属性名不允许大写，标签必须闭合等。

后面开发者又发现，太严格也不好，所以就有了HTML5，HTML5的要求又降下来。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/180.png' width='800'>
<br/>

H5新增内容，主要包括语义化标签、表单增强、供JS调用的新特性，比如定位、存储等。

<br/>

## HTML元素分类

按默认样式分：
- 块级 block
- 行内 inline
- inline-block

按内容分：

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/181.png' width='600'>
<br/>

<br/>

## HTML元素的嵌套关系
- 块级元素可以包含行内元素
- 块级元素不一定能包含块级元素，比如p不能包含div
- 行内元素一般不能包含块级元素

关于第三点，我们可以联想到a包含div的场景。

a包含div是否合法？不一定，取决于外面包裹的元素，a是一个transparent content model，也就是计算时，会把a当成透明的，所以取决于外层包裹的元素。

以下就是不合法的。

```html
<p><a><div>测试</div></a></p>
```

因为a被当成透明，所以结果是

```html
<p><div>测试</div></p>
```

<br/>

## HTML面试题

### doctype 的意义是什么？

- 让浏览器以标准模式渲染
- 让浏览器知道元素的合法性

### HTML、XHTML、HTML5的关系

- HTML属于 SGML
- XHTML 属于 XML，是HTML进行XML严格化的结果
- HTML5不属于SGML或XML，比XHTML宽松

### HTML5有什么变化？

- 新的语义化元素
- 表单增强
- 新的API，如离线、音视频、图形、实时通信、本地存储、设备能力
- 分类与嵌套变更

### em与i有什么区别？

- em是语义化标签，表强调
- i是纯样式的标签，表斜体
- HTML5中i不推荐使用，一般用作图标

### 语义化的意义？

- 开发者容易理解
- 机器容易理解结构（搜索、读屏软件）
- 有助于SEO

### HTML跟DOM的关系

- HTML是“死”的
- DOM由HTML解析出来，是活的
- JS可以维护DOM

### property和attribute的区别

- attribute是“死”的，也就是写在HTML中的属性
- property是“活”的，是解析出来的特性

例子：
```html
<input type='number' value='1'/>
```

value是HTML上的一个attribute，是死的。

浏览器拿到这段代码，会解析成DOM元素，property是DOM上的特性，是活的。

我们可以在浏览器控制台执行以下代码

```js
$0.value // $0指向input元素，value是input元素上的property
"1"
$0.value=2 // 改变input元素上的property，页面上输入框的值会改变，但浏览器Element面板上，input代码上的value还是1
2
$0.getAttribute('value') // 要想拿到attribute值，可以使用getAttribute。注意，此时页面输入框的值已经是3，但attribute值仍为1
"1"
$0.setAttribute('value',5) // 要想改变attribute值，可以使用setAttribute，此时将attribute值设置为5，但页面输入框的值仍为3
```

可见，attribute是HTML的属性，而property是DOM上的特性，HTML是“死”的，所以attribute也是“死”的，渲染出DOM元素后，就跟DOM元素没有关联。

而DOM元素是活的，property也是活的，当我们改变property的值时，页面输入框的值也会跟着改变。
