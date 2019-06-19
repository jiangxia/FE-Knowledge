# 学习CSS的线索

CSS相关的标准一共98份，暂且去掉Working Draft状态的标准，还有22份候选标准和6份推荐标准。面对这22+6份标准，我们需要一条线索，才能把这些离散的标准组织成易于理解和记忆的形式。

而这条线索就是CSS语法，任何CSS的特性都必须通过一定的语法结构表达出来，所以语法可以帮助我们发现大多数CSS特性。

CSS的顶层样式表由两种规则组成的规则列表构成，一种被称为 at-rule，也就是at 规则，另一种是 qualified rule，也就是普通规则。

at-rule由一个 @ 关键字和后续的一个区块组成，如果没有区块，则以分号结束。at-rule不常用，但却是掌握CSS的一些高级特性所必须的内容。

qualified rule则是指普通的CSS规则，也就是我们所熟识的，由选择器和属性指定构成的规则。

<br/>

# at 规则

<br/>

## @charset

@charset用于提示CSS文件使用的字符编码方式，它如果被使用，必须出现在最前面。这个规则只在给出语法解析阶段前使用，并不影响页面上的展示效果。

```css
@charset "utf-8";
```

<br/>

## @import

@import用于引入一个CSS文件，除了@charset规则不会被引入，@import可以引入另一个文件的全部内容。

```css
@import "mystyle.css";
@import url("mystyle.css");
```

```css
@import [ <url> | <string> ]
[ supports( [ <supports-condition> | <declaration> ] ) ]?
<media-query-list>? ;
```

通过代码，我们可以看出，import还支持 supports 和media query形式。

<br/>

## @media

media就是大名鼎鼎的media query使用的规则了，它能够对设备的类型进行一些判断。在media的区块内，是普通规则列表。

```css
@media print {
  body { font-size: 10pt }
}
```

<br/>

## @page

page用于分页媒体访问网页时的表现设置，页面是一种特殊的盒模型结构，除了页面本身，还可以设置它周围的盒。

```css
@page {
  size: 8.5in 11in;
  margin: 10%;
  @top-left {
  	content: "Hamlet";
	}
  @top-right {
  	content: "Page " counter(page);
  }
}
```

<br/>

## @counter-style

counter-style产生一种数据，用于定义列表项的表现。

```css
@counter-style triangle {
  system: cyclic;
  symbols: ‣;
  suffix: " ";
}
```

<br/>

## @key-frames

keyframes产生一种数据，用于定义动画关键帧。

```css
@keyframes diagonal-slide {
  from {
    left: 0;
    top: 0;
  }
  to {
    left: 100px;
    top: 100px;
  }
}
```

<br/>

## @fontface

fontface用于定义一种字体，icon font技术就是利用这个特性来实现的。

```css
@font-face {
  font-family: Gentium;
  src: url(http://example.com/fonts/Gentium.woff);
}
p { font-family: Gentium, serif; }
```

<br/>

## @support

support检查环境的特性，它与media比较类似。

<br/>

## @namespace

用于跟XML命名空间配合的一个规则，表示内部的CSS选择器全都带上特定命名空间。

<br/>

## @viewport

用于设置视口的一些特性，不过兼容性目前不是很好，多数时候被html的meta代替。

<br/>

# 普通规则

qualified rule主要是由选择器和声明区块构成。声明区块又由属性和值构成。

- 普通规则
    + 选择器
    + 声明列表
        - 属性
        - 值
            + 值的类型
            + 函数

## 选择器

我们从语法结构可以看出，任何选择器，都是由几个符号结构连接的：空格、大于号、加号、波浪线、双竖线，这里需要注意一下，空格，即为后代选择器的优先级较低。

然后对每一个选择器来说，如果它不是伪元素的话，由几个可选的部分组成，标签类型选择器，id、class、属性和伪类，它们中只要出现一个，就构成了选择器。

如果它是伪元素，则在这个结构之后追加伪元素。只有伪类可以出现在伪元素之后。下面用一个列表（不太严谨地）整理了选择器的语法结构：


<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/26.png' width='800'>
<br/>

我们在这里可以参考一个示例图：


<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/27.png' width='700'>
<br/>

看完了选择器，我们继续来看看声明部分的语法。

<br/>

## 声明：属性和值

声明部分是一个由“属性:值”组成的序列。

属性是由中划线、下划线、字母等组成的标识符，CSS还支持使用反斜杠转义。我们需要注意的是：属性不允许使用连续的两个中划线开头，这样的属性会被认为是CSS变量。

在CSS Variables标准中，以双中划线开头的属性被当作变量，与之配合的则是 var 函数：

```css
:root {
  --main-color: #06c;
  --accent-color: #006;
}
/* The rest of the CSS file */
#foo h1 {
  color: var(--main-color);
}
```

值的部分，主要在标准 CSS Values and Unit，根据每个CSS属性可以取到不同的值，这里的值可能是字符串、标识符。

CSS属性值可能是以下类型。

1. CSS范围的关键字：initial，unset，inherit，任何属性都可以的关键字。
2. 字符串：比如content属性。
3. URL：使用url() 函数的URL值。
4. 整数/实数：比如flex属性。
5. 维度：单位的整数/实数，比如width属性。
6. 百分比：大部分维度都支持。
7. 颜色：比如background-color属性。
8. 图片：比如background-image属性。
9. 2D位置：比如background-position属性。
10. 函数：来自函数的值，比如transform属性。

这里我们要重点介绍一下函数。一些属性会要求产生函数类型的值，比如easing-function会要求cubic-bezier()函数的值：

CSS支持一批特定的计算型函数：

1. calc()
2. max()
3. min()
4. clamp()
5. toggle()
6. attr()

calc()函数是基本的表达式计算，它支持加减乘除四则运算。在针对维度进行计算时，calc()函数允许不同单位混合运算，这非常的有用。

例如：

```css
section {
  float: left;
  margin: 1em; border: solid 1px;
  width: calc(100%/3 - 2*1em - 2*1px);
}
```

max()、min()和clamp()则是一些比较大小的函数，max()表示取两数中较大的一个，min()表示取两数之中较小的一个，clamp()则是给一个值限定一个范围，超出范围外则使用范围的最大或者最小值。

toggle()函数在规则选中多于一个元素时生效，它会在几个值之间来回切换，比如我们要让一个列表项的样式圆点和方点间隔出现，可以使用下面代码：

```css
ul { list-style-type: toggle(circle, square); }
```

attr()函数允许CSS接受属性值的控制。

<br/>

# 总结

在这篇文章中，我们了解了CSS语法的总体结构，CSS的语法总体结构是由两种规则列表构成，一种是at 规则，另一种是普通规则。

我们来了解了选择器语法结构、声明区块以及函数。

从整体上去掌握内容，再去定位到单个细节，这对于我们学习CSS有非常重要的提示作用。