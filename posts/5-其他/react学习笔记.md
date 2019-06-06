# 前言
react 是数据驱动的框架，也是目前前端最火的框架之一，学习react，我们照旧从应用维度跟设计维度进行学习。

<br/>

# 应用维度

<br/>

## 问题

> 从技术的应用维度看，首先考虑的是要解决什么问题，这是技术产生的原因。问题这层，用来回答“干什么用”。

<br/>

## 技术规范

> 技术被研发出来，人们怎么用它才能解决问题呢？这就要看技术规范，可以理解为技术使用说明书。技术规范，回答“怎么用”的问题，反映你对该技术使用方法的理解深度。

<br/>

### 生命周期函数

生命周期函数指的是在某一个时刻组件会自动调用执行的函数

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/86.jpg' width='800'>
<br/>

注意下update阶段，触发组件update有两种情况，props或者state的修改。

可以看到，这两种情况 生命周期函数是有重合的。唯一的不同就是props改变时，会先调用 componentWillReceiveProps .

componentWillReceiveProps 的执行：

1. 一个组件要从父组件接受参数
2. 如果这个组件第一次存在于父组件中，不会执行
3. 如果这个组件之前已经存在于父组件中，才会执行

<br/>

### redux
redux资料：
1. [Redux 中文文档](http://cn.redux.js.org/)

redux 注意点：
1. store是唯一的
2. 只有store能够改变自己的内容
3. Reducer必须是纯函数

reducer其实并没有直接修改store，他只是通过旧的state，返回新的state，然后将newstate传给store，store将newstate替换掉旧的state。

<br/>

### redux-thunk 发送异步请求获取数据
首先，安装redux。可以使用`yarn add redux-thunk` 

然后，引入redux-thunk。（按官方文档配置）

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/87.png' width='800'>
<br/>

配置了redux-thunk后，他允许我们在action中写异步代码。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/88.png' width='500'>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/89.png' width='500'>
<br/>

没引入redux-thunk之前，action只能是一个js对象。现在，action可以是一个函数。如果没引入redux-thunk，那么action为函数时会报错。

执行dispatch(action)时，默认会运行 action 返回的函数。

action对应的其实是红框中的函数

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/90.png' width='500'>
<br/>

在这里，是可以拿到dispatch方法，等拿到异步请求回来的数据后，可以封装成最终的action对象，传给store。


<br/>

### 到底什么是redux中间件


<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/91.png' width='600'>
<br/>


view会派发一个action，通过dispatch方法发送给store。

store接收到action，然后会将action连同之前的state一起传给给reducer。

reducer会返回一个新的数据给store，store拿到数据后，改变state。

而redux中间件的“中间”，指的是action跟store中间。

没引入redux-thunk之前，action只能是对象， 使用了redux-thunk后，action可以是函数。

action跟store是靠dispatch方法连接，事实上中间件就是对dispatch方法的封装或者说升级。

没有中间件的情况，dispatch方法接受一个对象，并把对象传递给store

引入redux-thunk后，如果dispatch方法接受的是对象，则将对象传递给store。如果接收的是函数，则会执行函数，等函数执行完再调用store。也就是说dispatch方法会根据参数不同，执行不同操作。

综上，中间件指的是action跟store的中间， 是对store的dispatch方法做了封装，或者说升级。

类似的中间件还有redux-logger、redux-saga。

redux-thunk 跟 redux-saga 非常类似，

redux-thunk 采用的是把异步操作放到action中操作。而 redux-saga 的思想是单独把异步逻辑拆分到另一个文件中管理。


为什么中间件会添加在action这个环节？我们可以站在框架作者的角度考虑：

1. Reducer：纯函数，只承担计算 State 的功能，不合适承担其他功能，也承担不了，因为理论上，纯函数不能进行读写操作。
2. View：与 State 一一对应，可以看作 State 的视觉层，也不合适承担其他功能。
3. Action：存放数据的对象，即消息的载体，只能被别人操作，自己不能进行任何操作。

想来想去，只有发送 Action 的这个步骤，即store.dispatch()方法，可以添加功能。


<br/>

### redux-saga 中间件的使用

首先，安装saga。`yarn add redux-saga`

然后，引入saga。（根据官方文档）

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/92.png' width='500'>
<br/>

saga跟thunk的区别在于，saga把异步逻辑拆分到独立的文章执行，所以我们要新建saga 文件。

saga文件内容如下：

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/93.png' width='500'>
<br/>


当组件dispatch的action是 GET_INIT_LIST 时，就会被 saga捕获，并去执行。

执行完异步操作，生成最终的action，通过put方法传给reducer。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/94.png' width='500'>
<br/>

有了中间件，就可以处理异步操作。

同步操作只要发出一种 Action 即可，异步操作的差别是它要发出三种 Action。

1. 操作发起时的 Action
2. 操作成功时的 Action
3. 操作失败时的 Action

<br/>

### react-redux 的使用

Redux 的作者封装了一个 React 专用的库 React-Redux，这个库是可以选用的。实际项目中，你应该权衡一下，是直接使用 Redux，还是使用 React-Redux。后者虽然提供了便利，但是需要掌握额外的 API，并且要遵守它的组件拆分规范。

一、React-Redux 将所有组件分成两大类：UI 组件和容器组件

UI 组件有以下几个特征：

1. 只负责 UI 的呈现，不带有任何业务逻辑
2. 没有状态（即不使用this.state这个变量）
3. 所有数据都由参数（this.props）提供
4. 不使用任何 Redux 的 API

容器组件的特征恰恰相反：

1. 负责管理数据和业务逻辑，不负责 UI 的呈现
2. 带有内部状态
3. 使用 Redux 的 API

总之，只要记住一句话就可以了：UI 组件负责 UI 的呈现，容器组件负责管理数据和逻辑。

二、connect()

三、<Provider> 组件

参考资料：[Redux 入门教程（三）：React-Redux 的用法](http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_three_react-redux.html)


<br/>

### 组件测试
jest
enzyme： https://airbnb.io/enzyme/

<br/>

## 最佳实践
> 最佳实践回答“怎么能用好”的问题，反映你实践经验的丰富程度。

<br/>

### 无状态组件

一个组件只有render函数时，可以定义为无状态组件，无状态组件就是一个函数，相比普通组件性能更高，因为他没有其他声明周期的方法。UI组件一般都可以定义为无状态组件。

### 高阶组件

<br/>

### redux性能优化
reselect库

<br/>

### react性能优化
**如何检测react性能**
在Chrome中监测react性能：在URL后加?react_perf，比如：
localhost:3000/?react_perf

<br/>

**函数传递优化**
render中使用到的函数，最好都在constructor中使用bind进行绑定，这样可以提高性能。

<br/>

### 不可变数据

reducer是纯函数，我们在操作reducer时，要切记不能修改传入的state，但新手很可能就会误操作，这就需要immutable库。

使用 immutable，我们可以生成immutable对象，

当然，它的优势不只在于此，他还有其他优点：
1. 减少内存使用
2. 并发安全（不用担心状态被他人修改）
3. 降低项目复杂度
4. 便于比较复杂数据，定制 shouldComponentUpdate 方便
5. 时间旅行方便

immutable也有缺点：
1. 学习成本
2. 库的大小
3. 对现有项目入侵太严重

针对immutable库比较大的缺点，可以使用seamless-immutable作为替换方案。


immutable学习资料：
1. [IMMUTABLE 详解](https://www.cnblogs.com/3body/p/6224010.html)
2. [结合 Immutable.JS 使用 Redux](http://cn.redux.js.org/docs/recipes/UsingImmutableJS.html)

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

### render函数何时执行
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


### VDOM

如果没有VDOM，state改变，如何渲染页面？

最原始的做法：

1. state 数据
2. JSX 模板
3. 数据 + 模板 结合，生成真实DOM，来显示
4. state发生改变
5. 数据 + 模板 结合，生成真实DOM，替换原来的DOM

缺陷：
第一次生成了完整的DOM片段
第二次生成了完整的DOM片段
第二次的DOM替换第一次的DOM，非常耗性能

改进的做法：

1. state 数据
2. JSX 模板
3. 数据 + 模板 结合，生成真实DOM，来显示
4. state发生改变
5. 数据 + 模板 结合，生成真实DOM，不直接替换原来的DOM
6. 新的DOM（DocumentFragment） 和 原始的DOM 做对比，找差异
7. 只替换有变动的DOM元素

缺陷：性能提升不明显，因为对比DOM也消耗了性能

react的做法

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
2. 跨端应用得以实现

<br/>

## 优劣局限

> 每种技术实现，都有其局限性，在某些条件下能最大化的发挥效能，缺少了某些条件则暴露出其缺陷。优劣局限层回答“做得怎么样”的问题。对技术优劣局限的把握，更有利于应用时总结最佳实践，是分析各种“坑”的基础。

<br/>


## 演进趋势

> 技术是在迭代改进和不断淘汰的。了解技术的前生后世，分清技术不变的本质，和变化的脉络，以及与其他技术的共生关系，能体现你对技术发展趋势的关注和思考。这层体现“未来如何”。

<br/>

react16新特性
1. 新的核心算法Fiber
2. Render 可以返回数据、字符串
3. 错误处理机制

新版本带来的优化和新功能
1. Portals 组件
2. 更好更快的服务端渲染
3. 体积更小，MIT协议