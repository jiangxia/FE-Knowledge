# 前言

你觉得，前端工程师的痛点是什么？

一方面，大学并没有开设前端这一门专业课，前端工程师更像是野路子，基本都是靠自学，没有接受系统的学习训练。

另一方面，前端知识点既多且杂，学过便忘，感觉自己懂了很多，却又说不清自己到底懂了什么。

最后，大家学知识都奔着实用性去的，这样学出来的知识体系又怎么可能完备呢？

如果你也有类似的感受，那么，是时候系统学习前端了。

本项目专为前端工程师而设，希望用最简洁的语言，构建尽可能完善的前端知识体系。

关于该前端知识体系，并非作者自创，而是借鉴了winter大神的《重学前端》，并且对《重学前端》的内容进行提炼。感谢winter大神！本项目不会止于《重学前端》，作者会在此体系的基础上，持续更新。

可能你会有疑问，学这些偏门的知识有什么用，工作中又用不到！

winter大神说得好：

> 我希望的是，通过这个有点偏的问题，引起你对这部分知识领域的关注，知道这部分知识的边界在哪里，从而形成一个完备的知识网络。让你在遇见不会的问题时候，可以快速定位到知识点，达成有效学习。并且，你也可以通过自己之前没有关注过的不同视角，来重新学习一遍这部分的知识。
> ……
> 比如，对JavaScript问题，先搞清楚看不懂的是词法问题、语法问题、还是运行时问题？定位清楚了问题，你已经距离解决问题前进了一大步。

好了，让我们一起努力，构建属于自己的前端知识体系吧！


# 体系

1. [javascript][000]
    - 文法
        * 词法
            + [词法介绍][001]
        * 语法
            + [基本规则][002]
            + [语法特性][003]
            + [语句][004]
            + [表达式][005]
    - 运行时
        * 数据结构
            + 类型
                * [类型 及 类型转换][006]
            + 实例
                * [对象][007]
                * [面向对象][008]
                * [对象的分类][009]
                * [常见数据结构][010]
        * 执行过程（算法）
            + [事件循环][011]
            + [闭包和执行上下文][012]
            + [函数的执行][013]
            + [语句级的执行][014]
2. [css][100]
    - 语言
        + [css语法][101]
        + [选择器][102]
    - 功能
        + 排版
            - [正常流][103]
            - [flex][104]
        + 交互
            - [CSS动画与交互][105]
        + 绘制
            - [渲染:绘制颜色][106]
3. [html][200]
    - 标签（功能）
        + [语义类标签][201]
        + [元信息类标签][202]
        + [链接][203]
        + [替换型元素][204]
    - 语言
        + [DTD][205]
    - 补充标准
        + [ARIA][206]
4. [浏览器原理和API][300]
    - 原理
        + [浏览器实现原理][301]
            - [网络通讯][302]
            - [构建DOM树][303]
            - [计算CSS][304]
            - [排版][305]
            - [渲染、合成、绘制][306]
            - [补充知识点][307]
        + [浏览器缓存机制][308]
        + [浏览器安全机制][309]
        + [网络协议][310]
    - API
        + [DOM][311]
        + [CSSOM][312]
        + [事件][313]
        + [跨域][314]
        + [存储][315]
5. 前端工程化
    - [性能][401]
    - [性能优化][402]
    - [工具链][403]
    - [持续集成][404]
    - [搭建系统][405]
    - [前端架构][406]
    - [监控][407]
    - [设计模式][408]





[000]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/JS%E6%A6%82%E8%BF%B0.md
[001]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E8%AF%8D%E6%B3%95.md
[002]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E5%9F%BA%E6%9C%AC%E8%A7%84%E5%88%99.md
[003]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E8%AF%AD%E6%B3%95%E7%89%B9%E6%80%A7.md
[004]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E8%AF%AD%E5%8F%A5.md
[005]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E8%A1%A8%E8%BE%BE%E5%BC%8F.md
[006]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E7%B1%BB%E5%9E%8B%E5%8F%8A%E7%B1%BB%E5%9E%8B%E8%BD%AC%E6%8D%A2.md
[007]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E5%AF%B9%E8%B1%A1.md
[008]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.md
[009]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%88%86%E7%B1%BB.md
[010]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E5%B8%B8%E8%A7%81%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84.md
[011]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E4%BA%8B%E4%BB%B6%E5%BE%AA%E7%8E%AF.md
[012]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E9%97%AD%E5%8C%85%E5%92%8C%E6%89%A7%E8%A1%8C%E4%B8%8A%E4%B8%8B%E6%96%87.md
[013]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E5%87%BD%E6%95%B0%E7%9A%84%E6%89%A7%E8%A1%8C.md
[014]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E8%AF%AD%E5%8F%A5%E7%BA%A7%E7%9A%84%E6%89%A7%E8%A1%8C.md



[100]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/1-css/CSS概述.md
[101]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/1-css/css语法.md
[102]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/1-css/选择器.md
[103]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/1-css/正常流.md
[104]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/1-css/flex.md
[105]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/1-css/CSS动画与交互.md
[106]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/1-css/绘制颜色.md




[200]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/2-html/html概述.md
[201]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/2-html/语义类标签.md
[202]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/2-html/元信息类标签.md
[203]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/2-html/链接.md
[204]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/2-html/替换型元素.md
[205]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/2-html/DTD.md
[206]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/2-html/ARIA.md




[300]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/浏览器原理和API概述.md
[301]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/浏览器实现原理概述.md
[302]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/网络通讯.md
[303]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/构建DOM树.md
[304]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/计算CSS.md
[305]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/排版.md
[306]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/渲染、合成、绘制.md
[307]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/补充知识点.md
[308]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/浏览器缓存机制.md
[309]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/浏览器安全机制.md
[310]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/网络协议.md
[311]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/DOM.md
[312]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/CSSOM.md
[313]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/事件.md
[314]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/跨域.md
[315]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/存储.md



[402]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/4-前端工程化/性能优化.md
[401]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/4-前端工程化/性能.md
[403]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/4-前端工程化/工具链.md
[404]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/4-前端工程化/持续集成.md
[405]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/4-前端工程化/搭建系统.md
[406]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/4-前端工程化/前端架构.md
[407]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/4-前端工程化/监控.md
[408]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/4-前端工程化/设计模式.md
