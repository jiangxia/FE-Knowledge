浏览器部分我们会先介绍下浏览器的实现原理，这是我们深入理解API的基础。

我们会从一般的浏览器设计出发，按照解析、构建DOM树、计算CSS、渲染、合成和绘制的流程来讲解浏览器的工作原理。

在API部分，我们会从W3C零散的标准中挑选几个大块的API来详细讲解，主要有：事件、DOM、CSSOM几个部分，它们分别覆盖了交互、语义和可见效果，这是我们工作中用到的主要内容。

其他的API，我会给出一份Chrome已经实现的API跟W3C标准的对应关系和它的生成过程，来覆盖其它部分。

以下，是浏览器及API的知识体系图。

- [原理][301]
    - [网络通讯][302]
    - [构建DOM树][303]
    - [计算CSS][304]
    - [排版][305]
    - [渲染、合成、绘制][306]
- API
    + [DOM][311]
    + [CSSOM][312]
    + [事件][313]
    + [跨域][314]
    + [存储][315]
- 延展阅读
    + [浏览器缓存机制][308]
    + [浏览器安全机制][309]
    + [网络协议][310]
    - [补充知识点][307]

[301]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/浏览器原理和api/浏览器实现原理概述.md
[302]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/浏览器原理和api/网络通讯.md
[303]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/浏览器原理和api/构建DOM树.md
[304]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/浏览器原理和api/计算CSS.md
[305]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/浏览器原理和api/排版.md
[306]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/浏览器原理和api/渲染、合成、绘制.md
[307]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/浏览器原理和api/补充知识点.md
[308]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/浏览器原理和api/浏览器缓存机制.md
[309]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/浏览器原理和api/浏览器安全机制.md
[310]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/浏览器原理和api/网络协议.md
[311]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/浏览器原理和api/DOM.md
[312]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/浏览器原理和api/CSSOM.md
[313]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/浏览器原理和api/事件.md
[314]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/浏览器原理和api/跨域.md
[315]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/浏览器原理和api/存储.md

