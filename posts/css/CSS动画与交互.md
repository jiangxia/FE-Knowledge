# 前言

在CSS属性中，有这么一类属性，它负责的不是静态的展现，而是根据用户行为产生交互。

首先我们先从属性来讲起。CSS中跟动画相关的属性有两个：animation和transition。


<br/>

# animation属性和transition属性

我们先来看下animation的示例，通过示例来了解一下animation属性的基本用法:

```css
@keyframes mykf
{
  from {background: red;}
  to {background: yellow;}
}

div
{
    animation:mykf 5s infinite;
}
```

这里展示了animation的基本用法，实际上animation分成六个部分：

1. animation-name 动画的名称，这是一个keyframes类型的值（keyframes产生一种数据，用于定义动画关键帧）；
2. animation-duration 动画的时长；
3. animation-timing-function	动画的时间曲线；
4. animation-delay	动画开始前的延迟；
5. animation-iteration-count	动画的播放次数；
6. animation-direction	动画的方向。

我们先来看 animation-name，这个是一个keyframes类型，需要配合@规则来使用。

比如，我们前面的示例中，就必须配合定义 mykf 这个 keyframes。keyframes的主体结构是一个名称和花括号中的定义，它按照百分比来规定数值，例如：

```css
@keyframes mykf {
  0% { top: 0; }
  50% { top: 30px; }
  75% { top: 10px; }
  100% { top: 0; }
}
```

这里我们可以规定在开始时把top值设为0，在50%是设为30px，在75%时设为10px，到100%时重新设为0，这样，动画执行时就会按照我们指定的关键帧来变换数值。

这里，0%和100%可以写成from和to，不过一般不会混用，画风会变得很奇怪，比如：

```css
@keyframes mykf {
  from { top: 0; }
  50% { top: 30px; }
  75% { top: 10px; }
  to { top: 0; }
}
```

这里关键帧之间，是使用 animation-timing-function 作为时间曲线的，稍后我会详细介绍时间曲线。

<br/>

接下来我们来介绍一下transition。transition与animation相比来说，是简单得多的一个属性。

它有四个部分：

1. transition-property 要变换的属性；
2. transition-duration 变换的时长；
3. transition-timing-function 时间曲线；
4. transition-delay 延迟。

这里的四个部分，可以重复多次，指定多个属性的变换规则。

实际上，有时候我们会把transition和animation组合，抛弃animation的timing-function，以编排不同段用不同的曲线。

```css
@keyframes mykf {
  from { top: 0; transition:top ease}
  50% { top: 30px;transition:top ease-in }
  75% { top: 10px;transition:top ease-out }
  to { top: 0; transition:top linear}
}
```

在这个例子中，在keyframes中定义了transition属性，以达到各段曲线都不同的效果。

接下来，我们就来详细讲讲刚才提到的timing-function，动画的时间曲线。

<br/>

# 贝塞尔曲线

我想，你能从很多CSS的资料中都找到了贝塞尔曲线，

我们在这里首先要了解一下贝塞尔曲线，贝塞尔曲线是一种插值曲线，它描述了两个点之间差值来形成连续的曲线形状的规则。

一个量（可以是任何矢量或者标量）从一个值到变化到另一个值，如果我们希望它按照一定时间平滑地过渡，就必须要对它进行插值。

最基本的情况，我们认为这个变化是按照时间均匀进行的，这个时候，我们称其为线性插值。而实际上，线性插值不大能满足我们的需要，因此数学上出现了很多其它的插值算法，其中贝塞尔插值法是非常典型的一种。它根据一些变换中的控制点来决定值与时间的关系。

贝塞尔曲线是一种被工业生产验证了很多年的曲线，它最大的特点就是“平滑”。时间曲线平滑，意味着较少突兀的变化，这是一般动画设计所追求的。

贝塞尔曲线用于建筑设计和工业设计都有很多年历史了，它最初的应用是汽车工业用贝塞尔曲线来设计车型。

关于贝塞尔曲线，不过多介绍。

<br/>

# 总结

我们今天的课程，重点介绍了动画和它背后的一些机制。

CSS用transition和animation两个属性来实现动画，这两个属性的基本用法很简单，我们今天还介绍了它们背后的原理：贝塞尔曲线。