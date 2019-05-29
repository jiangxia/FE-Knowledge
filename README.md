# 前言

你觉得，前端工程师的痛点是什么？

一方面，大学并没有开设前端这一门专业课，前端工程师更像是野路子，基本都是靠自学，没有接受系统的学习训练。

另一方面，前端知识点既多且杂，学过便忘，感觉自己懂了很多，却又说不出自己到底懂了什么。

如果你也有类似的感受，那么，是时候系统学习前端了。

本项目专为前端工程师而设，希望用最简洁的语言，构建尽可能完善的前端知识体系。

关于该前端知识体系，并非作者自创，是借鉴了winter大神的《重学前端》，并且对《重学前端》的内容进行提炼。感谢winter大神！

本项目不会止于《重学前端》，作者会在此体系的基础上，持续更新，敬请关注！

# 体系

1. [javascript][0]
    - 文法
        * 词法
            + [词法介绍][1]
        * 语法
            + [基本规则][2]
            + [语法特性][3]
            + [语句][4]
            + [表达式][5]
    - 运行时
        * 数据结构
            + 类型
                * [类型 及 类型转换][6]
            + 实例
                * [对象][7]
                * [面向对象][8]
                * [对象的分类][9]
                * [常见数据结构][10]
        * 执行过程（算法）
            + [事件循环][11]
            + [闭包和执行上下文][12]
            + [函数的执行][13]
            + [语句级的执行][14]
2. [css][15]
    - 语言
        + [css语法][16]
        + [选择器][17]
    - 功能
        + 排版
            - [正常流][18]
            - [flex][19]
3. [html][20]
    - 标签（功能）
        + [语义类标签][21]
        + [元信息类标签][22]
        + [链接][23]
        + [替换型元素][24]
    - 补充标准
4. [浏览器原理和API][25]
    - 原理
        + [浏览器实现原理][26]
            - [网络通讯][27]
            - [构建DOM树][28]
            - [计算CSS][29]
            - [排版][30]
            - [渲染、合成、绘制][31]
            - [补充知识点][32]
        + [浏览器缓存机制][33]
        + [浏览器安全机制][34]
        + [网络协议][35]
    - API
        + [DOM][36]
        + [CSSOM][37]
        + [事件][38]
        + [跨域][39]
        + [存储][40]
5. 前端工程化
    - [性能优化][41]
    - [监控][42]
    - [设计模式][43]





[0]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/JS%E6%A6%82%E8%BF%B0.md
[1]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E8%AF%8D%E6%B3%95.md
[2]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E5%9F%BA%E6%9C%AC%E8%A7%84%E5%88%99.md
[3]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E8%AF%AD%E6%B3%95%E7%89%B9%E6%80%A7.md
[4]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E8%AF%AD%E5%8F%A5.md
[5]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E8%A1%A8%E8%BE%BE%E5%BC%8F.md
[6]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E7%B1%BB%E5%9E%8B%E5%8F%8A%E7%B1%BB%E5%9E%8B%E8%BD%AC%E6%8D%A2.md
[7]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E5%AF%B9%E8%B1%A1.md
[8]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.md
[9]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%88%86%E7%B1%BB.md
[10]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E5%B8%B8%E8%A7%81%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84.md
[11]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E4%BA%8B%E4%BB%B6%E5%BE%AA%E7%8E%AF.md
[12]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E9%97%AD%E5%8C%85%E5%92%8C%E6%89%A7%E8%A1%8C%E4%B8%8A%E4%B8%8B%E6%96%87.md
[13]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E5%87%BD%E6%95%B0%E7%9A%84%E6%89%A7%E8%A1%8C.md
[14]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/0-JavaScript/%E8%AF%AD%E5%8F%A5%E7%BA%A7%E7%9A%84%E6%89%A7%E8%A1%8C.md
[15]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/1-css/CSS概述.md
[16]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/1-css/css语法.md
[17]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/1-css/选择器.md
[18]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/1-css/正常流.md
[19]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/1-css/flex.md
[20]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/2-html/html概述.md
[21]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/2-html/语义类标签.md
[22]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/2-html/元信息类标签.md
[23]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/2-html/链接.md
[24]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/2-html/替换型元素.md
[25]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/浏览器原理和API概述.md
[26]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/浏览器实现原理概述.md
[27]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/网络通讯.md
[28]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/构建DOM树.md
[29]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/计算CSS.md
[30]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/排版.md
[31]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/渲染、合成、绘制.md
[32]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/补充知识点.md
[33]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/浏览器缓存机制.md
[34]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/浏览器安全机制.md
[35]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/网络协议.md
[36]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/DOM.md
[37]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/CSSOM.md
[38]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/事件.md
[39]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/跨域.md
[40]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/3-浏览器原理和api/存储.md
[41]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/4-前端工程化/性能优化.md
[42]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/4-前端工程化/监控.md
[43]: https://github.com/jiangxia/FE-Knowledge/blob/master/posts/4-前端工程化/设计模式.md
