# 前言
react 是数据驱动的框架，也是目前前端最火的框架之一，学习react，我们照旧从应用维度跟设计维度进行学习。

<br/>

# 应用维度

<br/>

## 问题

> 从技术的应用维度看，首先考虑的是要解决什么问题，这是技术产生的原因。问题这层，用来回答“干什么用”。

<br/>

react 的诞生其实是要解决两个问题。UI细节问题问题 和 数据模型的问题。

### UI细节问题问题 

传统UI操作关注太多细节，jQuery虽然可以给我们提供了便捷的API，以及良好的浏览器兼容，但开发人员还是要手动去操作DOM，关注太多细节，不仅降低了开发效率，还可能引入BUG。

react 将开发人员从细节中解放出来，它始终整体“刷新”页面，无需关心细节。

举个例子：假设开发一个聊天的应用，​当有一条新消息到的时候，需要把新消息显示在页面上。

如果是局部刷新，首先我们要知道哪条是新消息，并为这条新消息创建一个节点，并把节点更新到页面的特定位置上

如果是整体刷新，只需要关心前后的状态，一个是两条消息，一个是三条消息，不需要关心哪条消息是新的，只需要把消息展示在UI上，不需要关心细节。

<br/>

### 数据模型的问题

前端开发，不可避免要面临数据管理的问题。

在react之前，前端管理数据的模型是MVC架构。

传统的MVC架构难以扩展和维护，当应用程序出现问题，很难知道是model还是view出现问题。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/96.jpg' width='600'>
<br/>

facebook 推出react的同时，也推出了flux架构。flux架构的最大特点就是单向数据流，Flux建立在react始终以状态驱动视图的基础上，不需要关心细节。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/97.jpg' width='600'>
<br/>

flux只是一个架构，开发者也发现flux并不好用，所以就诞生了redux，当然还有Mobx、dva，这块内容太多了，为此我将他抽离出来，请看[这里](https://github.com/jiangxia/FE-Knowledge/blob/master/posts/5-其他/数据管理学习笔记.md)。

<br/>


## 技术规范

> 技术被研发出来，人们怎么用它才能解决问题呢？这就要看技术规范，可以理解为技术使用说明书。技术规范，回答“怎么用”的问题，反映你对该技术使用方法的理解深度。

<br/>

### react组件

React 组件基本上由 3 个部分组成——属性(props)、状态(state)以及生命周期方法。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/160.jpg' width='600'>
<br/>

官方在 React 组件构建上提供了 3 种不同的方法:React.createClass、ES6 classes 和无状态函数(stateless function)。

**react组件有四个特点**

1. 由属性和状态得到一个view （ props + state = view ）
2. React 组件一般不提供方法，而是某种状态机
3. React组件可以理解为一个纯函数
4. 单向数据绑定

<br/>

**创建组件的步骤：**

1. 创建静态 UI
2. 考虑组件的状态组成：状态（state） 及 状态的改变（effect、reducer）
3. 考虑组件的交互方式：状态的触发（dispatch）

<br/>

**创建组件的原则**

1. 何时创建组件：单一职责原则
    - 每个组件只做一件事
    - 如果组件变得复杂，那么应该拆分成小组件
2. 数据状态管理：DRY原则
    - 能计算得到的状态就不要单独存储
    - 组件尽量无状态，所需数据通过 props 获取

<br/>

### 受控组件 VS 非受控组件

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/98.jpg' width='800'>
<br/>

### 生命周期函数

生命周期函数指的是在某一个时刻组件会自动调用执行的函数。

React 生命周期分成两类 ：

- 当组件在挂载或卸载时 
- 当组件接收新的数据时，即组件更新时 

react生命周期图如下：

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/161.jpg' width='800'>
<br/>

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/86.jpg' width='800'>
<br/>

也可以参考网上的[这张图](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)。

这里简单介绍下：

<br/>

#### constructor

1. 用于初始化内部状态，很少使用
2. 唯一可以直接修改 state 的地方

<br/>

#### getDerivedStateFromProps

1. 当 state 需要从 props 初始化时使用
2. 尽量不要使用：维护两者状态一致性会增加复杂度
3. 每次 render 都会调用
4. 典型场景：表单控件获取默认值

<br/>

#### componentDidMount

1. UI 渲染完成后调用
2. 只执行一次
3. 典型场景：获取外部资源

<br/>

#### componentWillUnmount

1. 组件移除时被调用
2. 典型场景：资源释放

<br/>

#### getSnapshotBeforeUpdate

1. 在元素被渲染并写入 DOM 之前调用，这样，你在 DOM 更新前捕获 DOM 信息（例如：滚动位置）。
2. 在页面 render t前调用，state 已更新
3. 典型场景：获取 render 之前的 DOM 状态

<br/>

#### componentDididUpdate

1. 每次 UI 更新时被调用
2. 典型场景：页面需要根据 props 变化重新获取数据

<br/>

#### shouldComponentUpdate

1. 决定 Virtual DOM 是否要重绘
2. 一般可以由 PureComponent 自动实现
3. 典型场景：性能优化

<br/>

#### componentWillReceiveProps
注意下update阶段，触发组件update有两种情况，props或者state的修改。

可以看到，这两种情况生命周期函数是有重合的。唯一的不同就是props改变时，会先调用 componentWillReceiveProps

1. 一个组件要从父组件接受参数
2. 如果这个组件第一次存在于父组件中，不会执行
3. 如果这个组件之前已经存在于父组件中，才会执行

<br/>



<br/>

### 组件测试

React 让前端单元测试变得容易:
- React 应用很少需要访问浏览器API
- 虚拟DOM可以在nodejs环境运行和测试
- Redux隔离了状态管理，纯数据层单元测试

单元测试涉及的工具：
- Jest：Facebook 开源的JS单元测试框架
- JS DOM：浏览器环境的nodejs模拟
- Enzyme：React组件渲染和测试
- nock：模拟HTTP请求
- sinon：函数模拟和调用跟踪
- istanbul：单元测试覆盖率

jest中文[教程](https://jestjs.io/docs/zh-Hans/getting-started)

enzyme： https://airbnb.io/enzyme/

<br/>

### JSX

JSX 的本质  不是模板引擎，而是动态创建组件的语法糖，它允许我们在JavaScript代码中直接写HTML标记。

如果在 JSX 中往 DOM 元素中传入自定义属性，React 是不会渲染的。如果要使用 HTML 自定义属性，要使用 data- 前缀，这与 HTML 标准也是一致的。然而，在自定义标签中任意的属性都是被支持的，以 aria- 开头的网络无障碍属性同样可以正常使用。

**JSX的优点**

1. 直观：声明式创建界面
2. 灵活：代码动态创建界面
3. 易上手：无需学习新的模板语言

**约定**

1. 自定义组件以大写字母开头
2. react 认为小写的 tag 是原生 DOM 节点，如 div
3. JSX标记可以直接使用属性语法，例如`<menu.Item />`

<br/>

### React Router

先说结论：路由不只是页面切换，更是代码组织方式

**为什么需要路由?**

1. 单页应用需要进行页面切换
2. 通过URL可以定位到页面
3. 更有语义的组织资源

**路由实现的基本架构**

原理：React Router 在一个组件容器中，根据URL来显示路由配置中的组件。


<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/127.jpg' width='600'>
<br/>

**React Router的使用**

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/128.jpg' width='600'>
<br/>

**React Router的特性**

1. 声明式路由定义：像使用react标记一样，可以在任何地方使用路由，而不需要特殊的路由表
2. 动态路由：对比的是静态路由，传统的服务器端路由一旦配置了，就是一个静态的配置文件，而React Router只有在组件render时，才会实时去解析。

**三种路由实现方式**

1. URL路由
2. hash路由
3. 内存路由

**React Router API**

1. `<Link>` ：普通链接，不会触发浏览器刷新
2. `<NavLink>`：类似`<Link>`但是会添加当前选中状态
3. `<Prompt>`：满足条件时提示用户是否离开当前页面
4. `<Redirect>`：重定向当前页面，例如登录判断
5. `<Route>`：路由配置的核心标记，路径匹配时显示对应组件
6. `<Switch>`：只现实第一个匹配路由

**React Router可以通过URL传递参数**

1. 如何通过URL传递参数：<Route path='/topic/:id'/>
2. 如何获取参数：this.props.match.params
3. 路由匹配进阶[资料](https://github.com/pillarjs/path-to-regexp)

**何时需要URL参数**
页面状态尽量通过URL参数定义


<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/129.jpg' width='600'>
<br/>

### 前端项目的理想架构

前端项目的理想架构：可维护，可扩展，可测试，易开发，易构建

**易于开发**

1. 开发工具是否完善
2. 生态圈是否繁荣
3. 社区是否活跃

**易于扩展**

1. 增加新功能是否容易
2. 新功能是否会显著增加系统的复杂度

**易于维护**

1. 代码是否容易理解
2. 文档是否健全

**易于测试**
1. 功能的分层是否清晰
2. 副作用少
3. 尽量使用纯函数

**易于构建**

1. 使用通用技术和架构
2. 构建工具的选择

<br/>

### ref

要获取真实的DOM节点有两种方式，一种是通过e.target，一种是ref。

但能不使用ref尽量不用

<br/>

### 样式处理

#### 基本样式设置

在 React 0.13 版本之前，React 官方提供 React.addons.classSet 插件来给组件动态设置 className，
这在后续版本中被移除(为了精简 API )。我们可以使用 classnames 库来操作类。

```js
// 如果不使用 classnames 库，就需要这样处理动态类名:
import React, {Component} from 'react';
class Button extends Component {
  render () {
    let btnClass = 'btn';
    if (this.state.isPressed) {
      btnClass += ' btn-pressed';
    } else if (this.state.isHovered) {
      btnClass += ' btn-over';
    }
    return <button className={btnClass}>{this.props.label}</button>;
  }
}
// 使用了 classnames 库代码后，就可以变得很简单: import React, { Component } from 'react';
import classNames from 'classnames'; 
class Button1 extends Component {
  // ...
  render () {
    const btnClass = classNames ({
      btn: true,
      'btn-pressed': this.state.isPressed,
      'btn-over': !this.state.isPressed && this.state.isHovered,
    });
    return <button className={btnClass}>{this.props.label}</button>;
  }
}

```
<br/>

## 最佳实践
> 最佳实践回答“怎么能用好”的问题，反映你实践经验的丰富程度。

<br/>

### 无状态组件

一个组件只有render函数时，可以定义为无状态组件，无状态组件就是一个函数，相比普通组件性能更高，因为他没有其他声明周期的方法。UI组件一般都可以定义为无状态组件。

### 组件设计模式

高阶组件和函数子组件都是设计模式。

#### 高阶组件（HOC）

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/100.jpg' width='800'>
<br/>

#### 函数子组件

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/101.jpg' width='800'>
<br/>


<br/>



### react性能优化

**如何检测react性能**

在Chrome中监测react性能：在URL后加?react_perf，比如：localhost:3000/?react_perf

<br/>

**函数传递优化**

render中使用到的函数，最好都在constructor中使用bind进行绑定，这样可以提高性能。

<br/>


### UI组件库对比
目前热门的react UI框架有：Ant.Design、Material UI、Semantic UI

选择UI库的考虑因素:

1. 组件库是否齐全
2. 样式风格是否符合业务需求
3. API设计是否便捷和灵活
4. 技术支持是否完善
5. 开发是否活跃

<br/>

### 同构应用

**什么是同构应用**

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/130.jpg' width='600'>
<br/>


<br/>

### 常用开发调试工具

开发react应用最常用的调试工具有：ESLint，Prettier，React DevTool，Redux DevTool

ESLint
- 使用.eslintrc进行规则的配置
- 使用airbnb的JavaScript代码风格

Prettier
- 代码格式化的神器
- 保证更容易写出风格一致的代码

<br/>

### 命令式编程 VS 声明式编程

#### 命令式编程

命令“机器”如何去做事情(how)，这样不管你想要的是什么(what)，它都会按照你的命令实现。

#### 声明式编程

告诉“机器”你想要的是什么(what)，让机器想出如何去做(how)。

在React中，每个组件通过render函数返回“这个组件应该长得什么样”，而不去描述“怎么样去让这个组件长成这个样子”。

#### 声明式编程的好处

- 让开发者的工作简化了
- 减少了重复工作
- 留下了改进的空间：比如React Fiber，虽然算法改头换面，但是组件却几乎不用改，因为组件只操心“显示什么”而不操心“如何显示”啊，当然不受影响了。
- 提供了全局协调能力：在React的未来，每个组件还是只声明“想要画成什么样子”，但React却可以改进协调算法，让React组件根据不同优先级来渲染，提高用户感知性能，但是React组件的代码不需要改变

<br/>

## 市场应用趋势

> 随着技术生态的发展，和应用问题的变迁，技术的应用场景和流行趋势会受到影响。这层回答“谁用，用在哪”的问题，反映你对技术应用领域的认识宽度。

<br/>

# 设计维度

<br/>

## 目标

> 为了解决用户的问题，技术本身要达成什么目标。这层定义“做到什么”。

<br/>

## 实现原理

> 为了达到设计目标，该技术采用了什么原理和机制。实现原理层回答“怎么做到”的问题。把实现原理弄懂，并且讲清楚，是技术人员的基本功。

<br/>



### render的执行

1. 当组件的state和props发生改变时，render函数就会重新执行
2. 父组件render函数被执行时，它的子组件的render函数都将被重新运行一次

<br/>


### this.setState

this.setState 背后有一个队列的机制，每次调用 setState ，都会塞到队列里面，通过队列可以高效更新 state ，setState 对状态的更新是异步的

<br/>

### applyMiddleWare

applyMiddleWare 的实现：
1. 拿到原生的store跟dispatch
2. 对dispatch做了一层扩展
3. 将原生store中的dispatch覆盖掉

<br/>


### 为什么需要VDOM？

**如果没有VDOM，state改变，如何渲染页面？**

最原始的做法：

1. state 数据
2. JSX 模板
3. 数据 + 模板 结合，生成真实DOM，来显示
4. state发生改变
5. 数据 + 模板 结合，生成真实DOM，替换原来的DOM

这样做的缺陷：

1. 第一次生成了完整的DOM片段
2. 第二次生成了完整的DOM片段
3. 第二次的DOM替换第一次的DOM，非常耗性能

**改进的做法：**

1. state 数据
2. JSX 模板
3. 数据 + 模板 结合，生成真实DOM，来显示
4. state发生改变
5. 数据 + 模板 结合，生成真实DOM，不直接替换原来的DOM
6. 新的DOM（DocumentFragment） 和 原始的DOM 做对比，找差异
7. 只替换有变动的DOM元素

这样做的缺陷：性能提升不明显，因为对比DOM也消耗了性能

**react的做法**

1. state 数据
2. JSX 模板
3. 数据 + 模板结合，生成VDOM（VDOM就是一个JS对象，用他来描述真实DOM）
4. 用VDOM，生成真实DOM，来显示
5. state发生改变
6. 生成新的VDOM （极大提升性能）
7. 比较原始VDOM和新的VDOM的区别 （极大提升性能）
8. 只替换有变动的DOM元素

优点：

1. 性能提升了
2. 方便与其他平台集成，跨端应用得以实现

<br/>

### VDOM原理

JSX的运行基础就是VDOM。

VDOM的运行机制是广度优先分层比较。

VDOM 的两个假设：

1. 组件的DOM结构是相对稳定的（很少发生跨层移动的场景）
2. 类型相同的兄弟节点可以被唯一标识

<br/>

### React 数据流
在 React 中，数据是自顶向下单向流动的，即从父组件到子组件。这条原则让组件之间的关系变得简单且可预测。

把组件看成一个函数，那么它接受了 props 作为参数，内部由 state 作为函数的内部参数，返回一个 Virtual DOM 的实现。

#### state

setState 是一个异步方法，一个生命周期内所有的 setState 方法会合并操 作。 

#### props

- React 的单向数据流，主要的流动管 道就是 props。props 本身是不可变的。当我们试图改变 props 的原始值时，React 会报出类型错 误的警告 
- props 可以配置默认值，使用defaultProps设置。
- 子组件 prop ： children （ React.Children 是 React 官方提供的一系列操作children 的方法。它提供诸如 map、 forEach、count 等实用函数 ）
- 组件 props ： 对于子组件而言，我们不仅可以直接使用 this.props.children 定义，也可以将子组件以 props 的形式传递。 
- propTypes  ： 规范 props 的类型与必需的状态 

<br/>

### 事件系统

VDOM 在内存中是以对象的形式存在的，如果想要在这些对象上添加事件，就会非常简单。React 基于 VDOM 实现了一个SyntheticEvent (合成事件)层，我们所定义的事件处理器会接收到一个 SyntheticEvent 对象的实例，它完全符合 W3C 标准，不会存在任何 IE 标 准的兼容性问题。并且与原生的浏览器事件一样拥有同样的接口，同样支持事件的冒泡机制，我们可以使用 stopPropagation() 和preventDefault() 来中断它。所有事件都自动绑定到最外层上。如果需要访问原生事件对象，可以使用 nativeEvent 属性。

#### 合成事件的实现机制

在 React 底层，主要对合成事件做了两件事:事件委派和自动绑定

##### 事件委派

- react并不会把事件处理函数直接绑定到 真实的节点上，而是把所有事件绑定到结构的最外层，使用一个统一的事件监听器，
- 事件监听器上维持了一个映射来保存所有组件内部的事件监听和处理函数。
- 当组件挂载或卸载时，只是在这个统一的事件监听器上插入或删除一些对象
- 当事件发生时，首先被这个统一的事件监听器 处理，然后在映射里找到真正的事件处理函数并调用。
- 这样做简化了事件处理和回收机制，效率 也有很大提升。 

##### 自动绑定

在 React 组件中，每个方法的上下文都会指向该组件的实例，即自动绑定 this 为当前组件。 而且 React 还会对这种引用进行缓存，以达到 CPU 和内存的最优化。在使用 ES6 classes 或者纯函数时，这种自动绑定就不复存在了，我们需要手动实现 this 的绑定。

常见的绑定方法有：

- 双冒号语法：`<button onClick={::this.handleClick}>Test</button>`
- 构造器内使用bind绑定
- 箭头函数

##### 原生事件

componentDidMount 会在组件已经完成安装并且在浏览器中存在真实的 DOM 后调用，此时我们就可以完成原生事件的绑定。

在 React 中使用 DOM 原生事件时，一定要在组件卸载时手动移除，否则很 可能出现内存泄漏的问题。而使用合成事件系统时则不需要，因为 React 内部已经帮你妥善地处理了。

<br/>

#### 合成事件与原生事件混用

尽量避免在 React 中混用合成事件和原生 DOM 事件。

阻止 React 事件冒泡的行为只能用于 React 合成事件系统 中，且没办法阻止原生事件的冒泡。反之，在原生事件中的阻止冒泡行为，却可以阻止 React 合成事件的传播。

React 的合成事件系统只是原生 DOM 事件系统的一个子集。它仅仅实现了 DOM Level 3 的事件接口，并且统一了浏览器间的兼容问题。有些事件 React 并没有实现，或者受某些限制没办法去实现，比如 window 的 resize 事件。

<br/>

#### 对比React合成事件与JavaScript原生事件

##### 事件对象
原生 DOM 事件对象在 W3C 标准和 IE 标准下存在着差异。在低版本的 IE 浏览器中，只能使用 window.event 来获取事件对象。而在 React 合成事件系统中，不存在这种兼容性问题，在事件处理函数中可以得到一个合成事件对象。

##### 事件类型
React 合成事件的事件类型是 JavaScript 原生事件类型的一个子集

##### 事件传播与阻止事件传播
事件传播分为捕获阶段、目标阶段、冒泡阶段。事件捕获在程序开发中的意义不大，还有兼容性问题。所以，React 的合成事件则并没有实现事件捕获，仅仅支持了事件冒泡机制。
阻止事件传播：阻止原生事件传播需要使用 e.preventDefault()，不过对于不支持该方法的浏览器(IE9 以 下)，只能使用 e.cancelBubble = true 来阻止。而在 React 合成事件中，只需要使用 e.prevent- Default() 即可。

##### 事件绑定方式

原生事件有三种方式:
- 直接在DOM元素中绑定: `<button onclick="alert(1)">Test</button>`
- 在JS中，通过为元素的事件属性赋值的方式实现绑定：`el.onclick = e => {console.log(e)} `
- 通过事件监听函数来实现绑定：`el.addEventListener("click", ()=>{},false); el.attachEvent("onclick", ()=>{})`

React 合成事件的绑定方式则简单得多:`<button onClick={this.handleClick}>Test</button>`


<br/>

## 优劣局限

> 每种技术实现，都有其局限性，在某些条件下能最大化的发挥效能，缺少了某些条件则暴露出其缺陷。优劣局限层回答“做得怎么样”的问题。对技术优劣局限的把握，更有利于应用时总结最佳实践，是分析各种“坑”的基础。

<br/>


## 演进趋势

> 技术是在迭代改进和不断淘汰的。了解技术的前生后世，分清技术不变的本质，和变化的脉络，以及与其他技术的共生关系，能体现你对技术发展趋势的关注和思考。这层体现“未来如何”。

<br/>

### react16

#### react16新特性

1. 新的核心算法Fiber
2. Render 可以返回数据、字符串
3. 错误处理机制

新版本带来的优化和新功能：

1. Portals 组件
2. 更好更快的服务端渲染
3. 体积更小，MIT协议

#### 下一代 React：异步渲染

异步渲染的两个部分

1. 时间分片：DOM操作的优先级低于浏览器原生行为，例如键盘和鼠标的输入，从而保证操作的流畅
2. 渲染挂起：虚拟DOM节点可以等待某个异步操作的完成，并指定timeout，之后才完成真正的渲染。

时间分片

1. 虚拟DOM的diff操作可以分片进行
2. React 新API：unstable_deferredUpdates
3. Chome 新API：requestIdleCallback

渲染挂起

1. 新内置组件：Timeout
2. unstable_deferUpdate