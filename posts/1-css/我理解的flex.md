# 前言

在 Flex 布局出来之前，浏览器布局被正常流统治着，那是个非常黑暗的年代。

在设计的眼中，排版的操作是一件很简单的事情，靠左、置中、靠右，我只要点一下，所有元素，就会乖乖的到指定的位置。

但到了前端在排版的实现上，就不是这样了。

我们常常得用一堆其实本来不是这样用的属性来做 hack。

比如说用 line-height 来做垂直置中，这样做的确能达到效果，但是在语意上就有点不顺，拿刚刚提到的 line-height 来说，这本来是用来当作段落中的行距，但却因为这个属性能扩展文字的上下空间，结果也被拿来做垂直置中。

那有没有一个方法能用来更好地实现 Web 布局呢？

<br/>

# 正常流布局的困境

虽然上文说那是个黑暗的时代，但不代表正常流错了。

我们需要先思考一个问题：**正常流适用什么场景**？

正常流下面，文字排版的思路是**改变文字和盒的相对位置，把它放进特定的版面中**。

这种设计来源于数百年来出版行业的排版经验，而HTML诞生之初，也确实是作为一种“超文本”存在的。所以，HTML诞生之初，正常流布局是可以满足需求的！

但我们知道，自上世纪90年代以来，Web标准和各种Web应用蓬勃发展，网页的功能逐渐从“文本信息”向着“软件功能”过渡，这个思路的变化导致了：CSS的正常流逐渐不满足人民群众的需求了。

到这里，我们终于明确一个问题：不是正常流错了，而是时代变了。

时代让我们对排版的要求越来越高，已经不满足于“改变文字和盒的相对位置，把它放进特定的版面中”，而是要做到“**改变盒的大小，使得它们的结构保持固定**”！

正常流在这里的时代大背景下，步履艰难。所以也就出现了很多诟病正常流的地方，比如CSS三大经典问题：垂直居中问题，两列等高问题，自适应宽问题。这是在其它UI系统中最为基本的问题，而到了CSS中，却变成了困扰工程师的三座大山。

机智的前端开发者们，曾经创造了各种黑科技来解决问题，包括著名的table布局、负margin、float与clear等等。

在早几年前，这些hack还被业界追捧，那真是个黑暗的年代，实现个非常简单的垂直居中都还要费大力气！

好在，Flex 布局出现了！它随着CSS3一起提出（最初叫box布局），可以说是解决了大问题。

<br/>

# Flex 布局的特点

首先，Flex 布局跟正常流布局是两套完全不同的布局系统，并且是不完全相容的。

所以，Flex 布局以后，子元素的float、clear和vertical-align属性将失效。因为这些属性是正常流布局时使用的。

其次，Flex在英文中是可伸缩的意思，所以Flex 布局也叫弹性布局。

Flex布局的主要思想是，子元素能够以最好的方式去填充可用空间。

这也就满足上文提到的“改变盒的大小，使得它们的结构保持固定”这一要求。所以，曾经的CSS三座大山，在 Flex布局 这不复存在。

最后， Flex布局 已经非常成熟，未来完全可以代替正常流布局。 

在这方面做得最为大胆的，是React Native ，它使用了纯粹的Flex排版，不再支持正常流，最终也很好地支持了大量的应用界面布局，这一点也证明了Flex排版的潜力。

# Flex 布局的使用

关于 Flex 布局的使用，可以直接参考阮一峰的[文章](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)。

这里我想说说我对flex布局属性的理解。

我们都知道，flex布局一共有12个属性，6个容器属性，6个项目属性。但之前我一直记不住（可能也因为用得少吧）。

今天我就想着一定要把它们理顺。

## 容器的属性

先看容器属性：

```
flex-direction    // 项目的排列方向

flex-wrap         // 换行

flex-flow         // flex-direction和flex-wrap的简写形式,默认值为row nowrap。

justify-content   // 主轴上的对齐方式

align-items       // 交叉轴上如何对齐

align-content     // 交叉轴上如何对齐（多根轴线下才生效）
```

从这六个属性不难看出，容器属性设置了子元素的**排列方式与对齐方式**。

**先说排列方式**

由于 flex-flow 是 flex-direction 跟 flex-wrap 的简写形式，我们只需要记住 flex-flow即可。

flex-flow 其实跟正常流的思路是很像的：**规定了子元素朝一个方向排列，排不下就换行**。

只不过 Flex 布局更加强大，可以向上下左右四个方向排列，而且换行时，还能规定换行的方向。

**再说对齐方式**

flex 布局一共为我们提供了三个属性：justify-content、align-items、align-content。

假设我们的主轴默认是X轴，那么 justify-content 可以很容易地实现水平向左、居中、向右的对齐；而align-items、align-content 可以很容易实现垂直居中。

以前很难实现的垂直居中布局，在 Flex 布局下，就是三个属性的事，是不是很简单？

## 项目的属性

```
order         // 排列顺序，默认为0，可以为负数

flex-grow     // 项目的放大比例，默认为0

flex-shrink   // 项目的缩小比例，默认为1

flex-basis    // 项目占据主轴的基准空间

flex          // flex-grow, flex-shrink 和 flex-basis的简写

align-self    // 对齐方式
```

项目的属性更加简单，其中，order 是排列属性，数值越小，排列越靠前；align-self 为项目的对齐方式注入了灵活性，它可以覆盖容器的align-items属性，这对我们实现复杂布局提供了支持。

项目属性中，最值得我们关注的，是另外四个属性，说到底，是一个属性，那就是**flex**。

单看 flex 这个属性名，就知道它的地位非常之高了，它是最能体现flex布局的精华。

**Flex排版的核心是display:flex和flex属性**。

**flex项如果有flex属性，会根据flex方向代替宽/高属性，形成“填补剩余尺寸”的特性，这是一种典型的“根据外部容器决定内部尺寸”的思路**。

flex属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。

不难理解，auto 表示可以根据剩余空间自由伸缩，而none表示，不会随着剩余空间自由伸缩。

建议优先使用这个属性，而不是单独写三个分离的属性。

## 简单记忆

讲了这么多，可能你还是记不住，让我们记住一个简单的套路吧：

```css
.parent {
  display:flex;
  flex-flow:row nowrap;
}
.child {
  flex: 0 1 auto;
}
```

如需调整对齐方式，就在parent下增加justify-content、align-items、align-content 即可。

<br/>

# flex 布局实例

这里整理了一些示例，请看：

- [示例1](https://github.com/jiangxia/FE-Knowledge/blob/master/code/flex/index.html)
- [示例2](https://github.com/jiangxia/FE-Knowledge/blob/master/code/flex/demo1.html)
- [示例3](https://github.com/jiangxia/FE-Knowledge/blob/master/code/flex/demo2.html)
- [示例4](https://github.com/jiangxia/FE-Knowledge/blob/master/code/flex/demo3.html)

