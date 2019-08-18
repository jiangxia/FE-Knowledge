# 前言
react 是数据驱动的框架，也是目前前端最火的框架之一，学习react，我们照旧从应用维度跟设计维度进行学习。

<br/>

# 应用维度

<br/>

## 问题

> 从技术的应用维度看，首先考虑的是要解决什么问题，这是技术产生的原因。问题这层，用来回答“干什么用”。

<br/>

react 的诞生其实是要解决两个问题。UI细节问题问题 和 数据模型的问题。

**UI细节问题问题**

传统UI操作关注太多细节，jQuery虽然可以给我们提供了便捷的API，以及良好的浏览器兼容，但开发人员还是要手动去操作DOM，关注太多细节，不仅降低了开发效率，还容易引入BUG。

react以数据为中心，数据驱动视图，而不直接操作dom，也就是只负责描述界面应该显示成什么样子，而不关心实现细节。

> 之所以使用框架，不是因为社区，不是因为工具，不是因为生态，不是因为第三方库......
> 目前为止，框架最大的改进是为我们提供了应用内部状态与 UI 同步的可靠保证。
> 我们只需要定义一次 UI 界面，不再需要为每个操作编写特定的 UI 代码，同时，每个相同的状态下UI 总是一致，当状态改变后，框架自动更新视图。
> 更加详细的介绍，请看[现代 js 框架存在的根本原因](https://zcfy.cc/article/the-deepest-reason-why-modern-javascript-frameworks-exist?from=groupmessage&isappinstalled=0)

**数据模型的问题**

在react之前，前端管理数据的模型是MVC架构。传统的MVC架构难以扩展和维护，当应用程序出现问题，很难知道是model还是view出现问题。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/96.jpg' width='600'>
<br/>

react采用的是单向数据流，可以很好的避免类似的问题。

<br/>

## 技术规范

> 技术被研发出来，人们怎么用它才能解决问题呢？这就要看技术规范，可以理解为技术使用说明书。技术规范，回答“怎么用”的问题，反映你对该技术使用方法的理解深度。

<br/>

### React 的基本原则

要真正理解 React，开发者必须要明白这几点：

- React 界面完全由数据驱动；
- React 中一切都是组件；
- props 是 React 组件之间通讯的基本方式。

下面逐一分析。

<br/>

> 笔者认为：学习框架，关键是要关注框架本身解决了什么问题，以及如何解决，这些才是框架最核心的部分，如果胡子眉毛一把抓，很容易就迷失在知识的海洋中。
>
> 细心的你肯定会发现，react的三个基本原则，正是解决上文提到的两大传统的良方。
>
> 针对UI细节问题，react的解决方案就是：数据驱动与组件化；
>
> 针对数据模型，react的解决方案是单向数据流，而props为单向数据流提供了支持。
>
> 学习react的过程中，牢记两大传统问题以及react开出的解决方案，有利于你形成系统思维，强化你的react的理解。

<br/>

### 界面完全由数据驱动

React 的哲学，简单说来可以用下面这条公式来表示：

```js
UI = f(data)
```

等号左边的 UI 代表最终画出来的界面；等号右边的 f 是一个函数，也就是我们写的 React 相关代码；data 就是数据，在 React 中，data 可以是 state 或者 props。

UI 就是把 data 作为参数传递给 f 运算出来的结果。这个公式的含义就是，**如果要渲染界面，不要直接去操纵 DOM 元素，而是修改数据，由数据去驱动 React 来修改界面**。

我们开发者要做的，就是设计出合理的数据模型，让我们的代码完全根据数据来描述界面应该画成什么样子，而不必纠结如何去操作浏览器中的 DOM 树结构。

这样一种程序结构，是[声明式编程](#命令式编程VS声明式编程)（Declarative Programming）的方式，代码结构会更加容易理解和维护。

<br/>

### 组件：React 世界的一等公民

在 React 中一切皆为组件。这是因为：

- 用户界面就是组件；
- 组件可以嵌套包装组成复杂功能；
- 组件可以用来实现副作用。

第一点用户界面就是组件，很好理解，我们需要一个按钮，就可以实现一个Button组件，在 React 中，一个组件可以是一个类，也可以是一个函数，这取决于这个组件是否有自己的状态。

第二点，组件可以嵌套包装组成复杂功能。现实中的应用是很复杂的，React 中的组件可以重复嵌套，就是为了支持现实中的用户界面需要。

第三点，组件可以用来实现副作用。并不是说组件必须要在界面画一些东西，一个组件可以什么都不画，或者把画界面的事情交给其他组件去做，自己做一些和界面无关的事情，比如获取数据。

<br/>

### 组件之间的语言：props

父组件想要传递数据给子组件，可以通过 props。

同样，子组件想要传递数据给父组件，可以让父组件传递一个函数类型的 props 进来，当子组件要传递数据给父组件时，调用这个函数类型 props，就把信息传递给了父组件。

如果两个完全没有关系的组件之间有话说，情况就复杂了一点，比如下图中，两个橙色组件之间如果有话说，就没法直接通过 props 来传递信息。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/168.png' width='600'>
<br/>

一个比较土的方法，就是通过 props 之间的逐步传递，来把这两个组件关联起来。如果之间跨越两三层的关系，这种方法还凑合，但是，如果这两个组件隔了十几层，或者说所处位置多变，那让 props 跨越千山万水来相会，实在是得不偿失。

另一个简单的方式，就是建立一个全局的对象，两个组件把想要说的话都挂在这个全局对象上。这种方法当然简单可行，但是，我们都知道全局变量的危害罄竹难书，如果不想将来被难以维护的代码折磨，我们最好对这种方法敬而远之。

一般，业界对于这种场景，往往会采用第三方数据管理工具来解决，比如 Redux 和 Mobx 。

其实，不依赖于第三方工具，React 也提供了自己的跨组件通讯方式，这种方式叫 Context，后面会介绍。

小结：

- 父组件向子组件通信：props
- 子组件向父组件通信
    + 利用回调函数
    + 利用自定义事件机制
- 跨级组件通信：context
- 没有嵌套关系的组件通信：自定义事件机制

<br/>

### 组件设计

我们日常创建组件的一般步骤，是这样的：

1. 创建静态 UI
2. 考虑组件的状态组成：状态（state） 及 状态的改变（effect、reducer）
3. 考虑组件的交互方式：状态的触发（dispatch）

如果要设计出更优雅的组件，我们还要了解组件设计原则。

React 组件设计原则，简单说来，就是高内聚、低耦合。

#### 低耦合

就是要减少组件之间的耦合性，让系统易于理解、易于维护。

所以，创建组件的原则，归纳起来有两点：

1. 何时创建组件：单一职责原则
    - 每个组件只做一件事
    - 如果组件变得复杂，那么应该拆分成小组件
2. 数据状态管理：DRY原则
    - 能计算得到的状态就不要单独存储
    - 组件尽量无状态，所需数据通过 props 获取

更具体一点，在设计 React 组件时，要注意以下事项：

- 保持接口小，props 数量要少；
- 根据数据边界来划分组件，充分利用组合；
- 把 state 往上层组件提取，让下层组件只需要实现为纯函数。

#### 高内聚

传统的网页应用分为三层，分别是用 HTML 实现的“内容”，用 CSS 实现的“样式”，还有用 JS 实现的“动态行为”。

HTML、CSS 和 JS 被分开管理，导致的问题是要修改一个功能，需要至少修改三个文件，这就违背了高内聚的原则。

在 React 中，当你要修改一个功能的内容和行为时，在一个文件中就能完成，这样就满足了高内聚的要求。

在react中处理CSS，官方没有一个统一的标准，请看后面[样式处理](#样式处理)的章节。

组件设计的内容远不止这些。社区有非常多的最佳实践，请看[组件设计模式](组件设计模式)

<br/>

### 状态管理·组件状态

在前面的章节中，我们反复声明过 React 其实就是这样一个公式：

```js
UI = f(data)
```

f 的参数 data，除了 props，就是 state。props 是组件外传递进来的数据，state 代表的就是 React 组件的内部状态。

#### 为什么要了解 React 组件自身状态管理

虽然有 Redux 和 Mobx 这样的状态管理工具，不过，我们首先不要管这些第三方工具，先从了解 React 组件自身的管理开始。

为什么呢？

第一个原因，因为 React 组件自身的状态管理是基础，其他第三方工具都是在这个基础上构筑的，连基础都不了解，无法真正理解第三方工具。

另一个重要原因，对于很多应用场景，React 组件自身的状态管理就足够解决问题，犯不上动用 Redux 和 MobX 这样的大杀器，简单问题简单处理，可以让代码更容易维护。

#### 组件自身状态 state

##### 什么数据放在 state 中

判断一个数据应该放在哪里，用下面的原则：

- 如果数据由外部传入，放在 props 中；
- 如果是组件内部状态，是否这个状态更改应该立刻引发一次组件重新渲染？如果是，放在 state 中；不是，放在成员变量中。

##### 修改 state 的正确方式

不能直接修改 state 对象，必须使用 this.setState。

因为使用 setState 函数，那不光修改 state，还能引发组件的重新渲染。

##### state 改变引发重新渲染的时机

React 为了性能考虑，不会每次 setState 都引发重新渲染。

```js
this.setState({count: 1});
this.setState({caption: 'foo'});
this.setState({count: 2});
```

连续的同步调用 setState，第三次还覆盖了第一次调用的效果，但是效果只相当于调用了下面这样一次：

```js
this.setState({count: 2, caption: 'foo'});
```

每个 setState 都引发一次重新渲染，实在太浪费了。

React 非常巧妙地用任务队列解决了这个问题，可以理解为每次 setState 函数调用都会往 React 的任务队列里放一个任务，多次 setState 调用自然会往队列里放多个任务。React 会选择时机去批量处理队列里执行任务，当批量处理开始时，React 会合并多个 setState 的操作，比如上面的三个 setState 就被合并为只更新 state 一次，也只引发一次重新渲染。

因为这个任务队列的存在，React 并不会同步更新 state，所以，在 React 中，setState 也不保证同步更新 state 中的数据。

##### state 不会被同步修改

简单说来，调用 setState 之后的下一行代码，读取 this.state 并不是修改之后的结果。

```js
console.log(this.state.count);// 修改之前this.state.count为0
this.setState({count: 1})
console.log(this.state.count);// 在这里this.state.count依然为0
```

这是因为React 的任务队列机制。setState 只是给任务队列里增加了一个修改 this.state 的任务，这个任务并没有立即执行，所以 this.state 并不会立刻改变。

但也有例外。**由 React 的生命周期函数或者事件处理函数之外引起的 setState ，就可以同步更新 state**。

看下面的代码，结果可能会出乎你的所料：

```js
setTimeout(() => {
  this.setState({count: 2}); //这会立刻引发重新渲染
  console.log(this.state.count); //这里读取的count就是2
}, 0);
```

为什么 setTimeout 能够强迫 setState 同步更新 state 呢？

可以这么理解，当 React 调用某个组件的生命周期函数或者事件处理函数时，React 会想：“嗯，这一次函数可能调用多次 setState，我会先打开一个标记，只要这个标记是打开的，所有的 setState 调用都是往任务队列里放任务，当这一次函数调用结束的时候，我再去批量处理任务队列，然后把这个标记关闭。”

因为 setTimeout 是一个 JS 函数，和 React 无关，对于 setTimeout 的第一个函数参数，这个函数参数的执行时机，已经不是 React 能够控制的了，换句话说，React 不知道什么时候这个函数参数会被执行，所以那个“标记”也没有打开。

当那个“标记”没有打开时，setState 就不会给任务列表里增加任务，而是强行立刻更新 state 和引发重新渲染。这种情况下，React 认为：“这个 setState 发生在自己控制能力之外，也许开发者就是想要强行同步更新呢，宁滥勿缺，那就同步更新了吧。”

虽然有办法同步更新state，但要谨慎使用。

React 选择不同步更新 state，是一种性能优化。

而且，每当你觉得需要同步更新 state 的时候，往往说明你的代码设计存在问题，绝大部分情况下，你所需要的，并不是“state 立刻更新”，而是，“确定 state 更新之后我要做什么”，这就引出了 setState 另一个功能。

##### setState 的第二个参数

setState 的第二个参数可以是一个回调函数，当 state 真的被修改时，这个回调函数会被调用。

```js
console.log(this.state.count); // 0
this.setState({count: 1}, () => {
  console.log(this.state.count); // 这里就是1了
})
console.log(this.state.count); // 依然为0
```

当 setState 的第二个参数被调用时，React 已经处理完了任务列表，所以 this.state 就是更新后的数据。

如果需要在 state 更新之后做点什么，请利用第二个参数。

##### 函数式 setState

setState 的第一个参数除了可以是对象，其实也可以传入一个函数。

当 setState 的第一个参数为函数时，任务列表上增加的就是一个可执行的任务函数了，React 每处理完一个任务，都会更新 this.state，然后把新的 state 传递给这个任务函数。

setState 第一个参数的形式如下：

```js
function increment(state, props) {
  return {count: state.count + 1};
}
```

可以看到，这是一个纯函数，不光接受当前的 state，还接受组件的 props，在这个函数中可以根据 state 和 props 任意计算，返回的结果会用于修改 this.state。

如此一来，我们就可以这样连续调用 setState：

```js
this.setState(increment);
this.setState(increment);
this.setState(increment);
```

用这种函数式方式连续调用 setState，就真的能够让 this.state.count 增加 3，而不只是增加 1。

<br/>

## 最佳实践

> 最佳实践回答“怎么能用好”的问题，反映你实践经验的丰富程度。

<br/>

### 组件设计模式

#### 聪明组件和傻瓜组件

> 聪明组件和傻瓜组件：让我们更好的组织代码

<br/>

在 React 应用中，最简单也是最常用的一种组件模式，就是“聪明组件和傻瓜组件”。

软件设计中有一个原则，叫做“责任分离”，简单说就是让一个模块的责任尽量少，如果发现一个模块功能过多，就应该拆分为多个模块，让一个模块都专注于一个功能，这样更利于代码的维护。

使用 React 来做界面，无外乎就是获得驱动界面的数据，然后利用这些数据来渲染界面。

把获取和管理数据的逻辑放在父组件，也就是聪明组件；把渲染界面的逻辑放在子组件，也就是傻瓜组件。

这么做的好处，是可以灵活地修改数据状态管理方式，比如，最初你可能用 Redux 来管理数据，然后你想要修改为用 Mobx，如果按照这种模式分割组件，那么，你需要改的只有聪明组件，傻瓜组件可以保持原状。

因为傻瓜组件一般没有自己的状态，我们可以利用 PureComponent 来提高傻瓜组件的性能。

PureComponent 帮我们处理了shouldComponentUpdate。

值得一提的是，PureComponent 中 shouldComponentUpdate 对 props 做得只是浅层比较，不是深层比较，如果 props 是一个深层对象，就容易产生问题。

比如，两次渲染传入的某个 props 都是同一个对象，但是对象中某个属性的值不同，这在 PureComponent 眼里，props 没有变化，不会重新渲染，但是这明显不是我们想要的结果。

虽然 PureComponent 可以提高组件渲染性能，但是它也不是没有代价的，它逼迫我们必须把组件实现为 class，不能用纯函数来实现组件。

如果你使用 React v16.6.0 之后的版本，可以使用一个新功能 React.memo 来完美实现 React 组件，比如：

```js
const Joke = React.memo(() => (
    <div>
        <img src={SmileFace} />
        {this.props.value || 'loading...' }
    </div>
));
```

<br/>

#### 高阶组件

> 高阶组件：让我们更好的抽象公共逻辑

<br/>

在开发 React 组件过程中，很容易发现这样一种现象，某些功能是多个组件通用的，如果每个组件都重复实现这样的逻辑，肯定十分浪费，而且违反了“不要重复自己”（DRY，Don't Repeat Yourself)的编码原则，我们肯定想要把这部分共用逻辑提取出来重用。

我们说过，在 React 的世界里，组件是第一公民，首先想到的是当然是把共用逻辑提取为一个 React 组件。不过，有些情况下，这些共用逻辑还没法成为一个独立组件，换句话说，这些共用逻辑单独无法使用，它们只是对其他组件的功能加强。

举个例子，对于很多网站应用，有些模块都需要在用户已经登录的情况下才显示。比如，对于一个电商类网站，“退出登录”按钮、“购物车”这些模块，就只有用户登录之后才显示，对应这些模块的 React 组件如果连“只有在登录时才显示”的功能都重复实现，那就浪费了。

这时候，我们就可以利用“高阶组件（HoC）”这种模式来解决问题。

##### 高阶组件的基本形式

高阶组件，本质是一个函数，它接受至少一个 React 组件为参数，并且能够返回一个全新的 React 组件作为结果，当然，这个新产生的 React 组件是对作为参数的组件的包装，所以，有机会赋予新组件一些增强的“神力”。

一个最简单的高阶组件是这样的形式：

```js
const withDoNothing = (Component) => {
  const NewComponent = (props) => {
    return <Component {...props} />;
  };
  return NewComponent;
};
```

有了高阶组件，我们就可以用它来抽取共同逻辑。

##### 高阶组件的高级用法

高阶组件只需要返回一个 React 组件即可，没人规定高阶组件只能接受一个 React 组件作为参数，完全可以传入多个 React 组件给高阶组件。

我们可以用高阶组件封装登录与登出的逻辑，如下：

```js
const withLoginAndLogout = (ComponentForLogin, ComponentForLogout) => {
  const NewComponent = (props) => {
    if (getUserId()) {
      return <ComponentForLogin {...props} />;
    } else {
      return <ComponentForLogout{...props} />;
    }
  }
  return NewComponent;
};
```

##### 链式调用高阶组件

高阶组件最巧妙的一点，是可以链式调用。

假设，你有三个高阶组件分别是 withOne、withTwo 和 withThree，那么，如果要赋予一个组件 X 三个高阶组件的超能力，可以连续调用高阶组件，如下：

```js
const SuperX = withThree(withTwo(withOne(X)));
```

高阶组件本身就是一个纯函数，纯函数是可以组合使用的，所以，我们其实可以把多个高阶组件组合为一个高阶组件，然后用这一个高阶组件去包装X，代码如下：

```js
const hoc = compose(withThree, withTwo, withOne);
const SuperX = hoc(X);
```

在上面代码中使用的 compose，是函数式编程中很基础的一种方法，作用就是把多个函数组合为一个函数。

React 组件可以当做积木一样组合使用，现在有了 compose，我们就可以把高阶组件也当做积木一样组合，进一步重用代码。

假如一个应用中多个组件都需要同样的多个高阶组件包装，那就可以用 compose 组合这些高阶组件为一个高阶组件，这样在使用多个高阶组件的地方实际上就只需要使用一个高阶组件了。

##### 不要滥用高阶组件

高阶组件虽然可以用一种可重用的方式扩充现有 React 组件的功能，但高阶组件并不是绝对完美的。

首先，高阶组件不得不处理 displayName，不然 debug 会很痛苦。当 React 渲染出错的时候，靠组件的 displayName 静态属性来判断出错的组件类，而高阶组件总是创造一个新的 React 组件类，所以，每个高阶组件都需要处理一下 displayName。

如果要做一个最简单的什么增强功能都没有的高阶组件，也必须要写下面这样的代码：

```js
const withExample = (Component) => {
  const NewComponent = (props) => {
    return <Component {...props} />;
  }
  
  NewComponent.displayName = `withExample(${Component.displayName || Component.name || 'Component'})`;
  
  return NewCompoennt;
};
```

对于 React 生命周期函数，高阶组件不用怎么特殊处理，但是，如果内层组件包含定制的静态函数，这些静态函数的调用在 React 生命周期之外，那么高阶组件就必须要在新产生的组件中增加这些静态函数的支持，这更加麻烦。关于这点，请参考[这里](https://zhuanlan.zhihu.com/p/36178509)

其次，高阶组件支持嵌套调用，这是它的优势。但是如果真的一大长串高阶组件被应用的话，当组件出错，你看到的会是一个超深的 stack trace，十分痛苦。

关于高阶组件的进阶内容，请参考[高阶组件实现方法](#高阶组件实现方法)

<br/>

#### render props 模式

> render props 模式：让我们更好的抽象公共逻辑，同时又避免了高阶组件的一些问题

<br/>

高阶组件并不是 React 中唯一的重用组件逻辑的方式，且高阶组件存在一些弊端，所以又诞生了render props 模式，也称为“以函数为子组件”的模式。

所谓 render props，指的是让 React 组件的 props 支持函数这种模式。因为作为 props 传入的函数往往被用来渲染一部分界面，所以这种模式被称为 render props。

一个最简单的 render props 组件 RenderAll，代码如下：

```js
const RenderAll = (props) => {
  return(
     <React.Fragment>
     	{props.children(props)}
     </React.Fragment>
  );
};
```

这个 RenderAll 预期子组件是一个函数，它所做的事情就是把子组件当做函数调用，调用参数就是传入的 props，然后把返回结果渲染出来，除此之外什么事情都没有做。

使用 RenderAll 的代码如下：

```js
<RenderAll>
  {() => <h1>hello world</h1>}
</RenderAll>
```

可以看到，RenderAll 的子组件，也就是夹在 RenderAll 标签之间的部分，其实是一个函数。这个函数渲染出 `<h1>hello world</h1>`，这就是上面使用 RenderAll 渲染出来的结果。

当然，这个 RenderAll 没做任何实际工作，接下来我们看 render props 真正强悍的使用方法。

##### 传递 props

下面是实现 render props 的 Login 组件，可以看到，render props 和高阶组件的第一个区别，就是 render props 是真正的 React 组件，而不是一个返回 React 组件的函数。

```js
const Login = (props) => {
  const userName = getUserName();

  if (userName) {
    const allProps = {userName, ...props};
    return (
      <React.Fragment>
        {props.children(allProps)}
      </React.Fragment>
    );
  } else {
    return null;
  }
};
```

当用户处于登录状态，getUserName 返回当前用户名，否则返回空，然后我们根据这个结果决定是否渲染 props.children 返回的结果。

当然，render props 完全可以决定哪些 props 可以传递给 props.children，在 Login 中，我们把 userName 作为增加的 props 传递给下去，这样就是 Login 的增强功能。

一个使用上面 Login 的 JSX 代码示例如下：

```js
<Login>
  {({userName}) => <h1>Hello {userName}</h1>}
</Login>
```

##### 不局限于 children

render props 这个模式不必局限于 children 这一个 props，任何一个 props 都可以作为函数，也可以利用多个 props 来作为函数。

我们来扩展 Login，不光在用户登录时显示一些东西，也可以定制用户没有登录时显示的东西，我们把这个组件叫做 Auth，对应代码如下：

```js
const Auth= (props) => {
  const userName = getUserName();

  if (userName) {
    const allProps = {userName, ...props};
    return (
      <React.Fragment>
        {props.login(allProps)}
      </React.Fragment>
    );
  } else {
    <React.Fragment>
      {props.nologin(props)}
    </React.Fragment>
  }
};
```

用法如下：

```js
<Auth
  login={({userName}) => <h1>Hello {userName}</h1>}
  nologin={() => <h1>Please login</h1>}
/>
```

##### 依赖注入

render props 其实就是 React 世界中的“依赖注入”。

所谓依赖注入，指的是解决这样一个问题：逻辑 A 依赖于逻辑 B，如果让 A 直接依赖于 B，当然可行，但是 A 就没法做得通用了。依赖注入就是把 B 的逻辑以函数形式传递给 A，A 和 B 之间只需要对这个函数接口达成一致就行，如此一来，再来一个逻辑 C，也可以用一样的方法重用逻辑 A。

在上面的代码示例中，Login 和 Auth 组件就是上面所说的逻辑 A，而传递给组件的函数类型 props，就是逻辑 B 和 C。

##### render props 和高阶组件的比较

首先，render props 模式的应用，就是做一个 React 组件，而高阶组件，虽然名为“组件”，其实只是一个产生 React 组件的函数。

render props 不像高阶组件有那么多毛病，如果说 render props 有什么缺点，那就是 render props 不能像高阶组件那样链式调用，当然，这并不是一个致命缺点。

render props 相对于高阶组件还有一个显著优势，就是 props 传递更加灵活。

总结：**当需要重用 React 组件的逻辑时，建议首先看这个功能是否可以抽象为一个简单的组件；如果行不通的话，考虑是否可以应用 render props 模式；再不行的话，才考虑应用高阶组件模式**。

<br/>

#### mixin

> mixin：一样可以抽象公共逻辑，但现在已经不提倡使用。这里只做简单介绍。

<br/>

React 在使用 createClass 构建组件时提供了 mixin 属性。mixin有两个作用：

- 共享工具方法。
- 生命周期继承，props 与 state 合并。

ES6 Classes 不支持 mixin。

mixin 的问题:

- 破坏了原有组件的封装：mixin 方法会混入方法，给原有组件带来新的特性，但它也可能带来了新的 state 和 props，这意味着组件有一 些“不可见”的状态需要我们去维护，但我们在使用的时候并不清楚。另外，mixin 也有可能去依赖其他的 mixin，这样会建立一个 mixin 的依赖链，当我们改动其 中一个 mixin 的状态时，很可能会直接影响其他的 mixin。
- 命名冲突：尽管我们可以通过更改名字来解决，但遇到第三方引用，或已经引用了几个 mixin 的情况下， 总是要花一定的成本去解决冲突。
- 增加复杂性

##### 高阶组件与mixin的比较

高阶组件与 mixin 的不同之处

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/163.png' width='600'>
<br/>

高阶组件符合函数式编程思想。对于原组件来说，并不会感知到高阶组件的存在，只需要把功能套在它之上就可以了，从而避免了使用 mixin 时产生的副作用。

<br/>

#### 提供者模式

> 提供者模式：让我们更好的跨层级传递数据

<br/>

在 React 中，props 是组件之间通讯的主要手段，但是，有一种场景单纯靠 props 来通讯是不恰当的，那就是两个组件之间间隔着多层其他组件，下面是一个简单的组件树示例图图：

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/169.png' width='600'>
<br/>

在上图中，组件 A 需要传递信息给组件 X，如果通过 props 的话，那么从顶部的组件 A 开始，要把 props 传递给组件 B，然后组件 B 传递给组件 D，最后组件 D 再传递给组件 X。

其实组件 B 和组件 D 完全用不上这些 props，但是又被迫传递这些 props，这明显不合理，要知道组件树的结构会变化的，将来如果组件 B 和组件 D 之间再插入一层新的组件，这个组件也需要传递这个 props，这就麻烦无比。

可见，对于跨级的信息传递，我们需要一个更好的方法。

在 React 中，解决这个问题应用的就是“提供者模式”。

##### 提供者模式

提供者模式有两个角色，一个叫“提供者”（Provider），另一个叫“消费者”（Consumer）。在上面的组件树中，组件 A 可以作为提供者，组件 X 就是消费者。

既然名为“提供者”，它可以提供一些信息，而且这些信息在它之下的所有组件，无论隔了多少层，都可以直接访问到，而不需要通过 props 层层传递。

避免 props 逐级传递，即是提供者的用途。

##### 如何实现提供者模式

实现提供者模式，需要 React 的 Context 功能，可以说，提供者模式只不过是让 Context 功能更好用一些而已。

所谓 Context 功能，就是能够创造一个“上下文”，在这个上下文笼罩之下的所有组件都可以访问同样的数据。

提供者模式的一个典型用例就是实现“样式主题”（Theme），由顶层的提供者确定一个主题，下面的样式就可以直接使用对应主题里的样式。这样，当需要切换样式时，只需要修改提供者就行，其他组件不用修改。

##### React v16.3.0 之前的提供者模式

在 React v16.3.0 之前，要实现提供者，就要实现一个 React 组件，不过这个组件要做两个特殊处理。

- 需要实现 getChildContext 方法，用于返回“上下文”的数据；
- 需要定义 childContextTypes 属性，声明“上下文”的结构。

下面就是一个实现“提供者”的例子，组件名为 ThemeProvider：

```js
class ThemeProvider extends React.Component {
  getChildContext() {
    return {
      theme: this.props.value
    };
  }

  render() {
    return (
      <React.Fragment>
        {this.props.children}
      </React.Fragment>
    );
  }
}

ThemeProvider.childContextTypes = {
  theme: PropTypes.object
};
```

对于 ThemeProvider，我们创造了一个上下文，这个上下文就是一个对象，结构是这样：

```
{
  theme: {
    //一个对象
  }
}
```

接下来，就是使用这个“上下文”的组件。这里有两种方式：

使用类的方式：

```js
class Subject extends React.Component {
  render() {
    const {mainColor} = this.context.theme;
    return (
      <h1 style={{color: mainColor}}>
        {this.props.children}
      </h1>
    );
  }
}

Subject.contextTypes = {
  theme: PropTypes.object
}
```

使用纯函数组件：

```js
const Paragraph = (props, context) => {
  const {textColor} = context.theme;
  return (
    <p style={{color: textColor}}>
      {props.children}
    </p>
  );
};

Paragraph.contextTypes = {
  theme: PropTypes.object
};
```

这两种方式访问“上下文”的方式有些不同，都必须增加 contextTypes 属性，必须和 ThemeProvider 的 childContextTypes 属性一致，不然，this.context 就不会得到任何值。

最后，我们看如何结合”提供者“和”消费者“。

我们做一个组件来使用 Subject 和 Paragraph，这个组件不需要帮助传递任何 props，代码如下：

```js
const Page = () => (
  <div>
    <Subject>这是标题</Subject>
    <Paragraph>
      这是正文
    </Paragraph>
  </div>
);
```

上面的组件 Page 使用了 Subject 和 Paragraph，现在我们想要定制样式主题，只需要在 Page 或者任何需要应用这个主题的组件外面包上 ThemeProvider，对应的 JSX 代码如下：

```js
<ThemeProvider value={{mainColor: 'green', textColor: 'red'}} >
  <Page />
</ThemeProvider>
```

当我们需要改变一个样式主题的时候，改变传给 ThemeProvider的 value 值就搞定了。

##### React v16.3.0 之后的提供者模式

首先，要用新提供的 `createContext` 函数创造一个“上下文”对象。

```js
const ThemeContext = React.createContext();
```

这个“上下文”对象 `ThemeContext` 有两个属性，分别就是——对，你没猜错——Provider 和 Consumer。

```js
const ThemeProvider = ThemeContext.Provider;
const ThemeConsumer = ThemeContext.Consumer;
```

使用“消费者”如下：

```js
const Paragraph = (props, context) => {
  return (
    <ThemeConsumer>
      {
        (theme) => (
          <p style={{color: theme.textColor}}>
            {props.children}
          </p>
          )
      }
    </ThemeConsumer>
  );
};
```

实现 Page 的方式并没有变化:
```js
<ThemeProvider value={{mainColor: 'green', textColor: 'red'}} >
  <Page />
</ThemeProvider>
```

##### 两种提供者模式实现方式的比较

在老版 Context API 中，“上下文”只是一个概念，并不对应一个代码，两个组件之间达成一个协议，就诞生了“上下文”。

在新版 Context API 中，需要一个“上下文”对象（上面的例子中就是 ThemeContext)，使用“提供者”的代码和“消费者”的代码往往分布在不同的代码文件中，那么，这个 ThemeContext 对象放在哪个代码文件中呢？

最好是放在一个独立的文件中，这么一来，就多出一个代码文件，而且所有和这个“上下文”相关的代码，都要依赖于这个“上下文”代码文件，虽然这没什么大不了的，但是的确多了一层依赖关系。

为了避免依赖关系复杂，每个应用都不要滥用“上下文”，应该限制“上下文”的使用个数。

<br/>

#### 组合组件

> 组合组件：简化父组件向子组件传递props的方式

<br/>

组合组件模式要解决的是这样一类问题：父组件想要传递一些信息给子组件，但是，如果用 props 传递又显得十分麻烦。

利用 Context 可以解决问题，但非常繁琐，组合组件让我们可以用更简洁的方式去实现。

##### 问题描述

很多界面都有 Tab 这样的元件，我们需要一个 Tabs 组件和 TabItem 组件，Tabs 是容器，TabItem 是一个一个单独的 Tab，因为一个时刻只有一个 TabItem 被选中，很自然希望被选中的 TabItem 样式会和其他 TabItem 不同。

这并不是一个很难的功能，首先我们想到的就是，用 Tabs 中一个 state 记录当前被选中的 Tabitem 序号，然后根据这个 state 传递 props 给 TabItem，当然，还要传递一个 onClick 事件进去，捕获点击选择事件。

按照这样的设计，Tabs 中如果要显示 One、Two、Three 三个 TabItem，JSX 代码大致这么写：

```js
<TabItem active={true} onClick={this.onClick}>One</TabItem>
<TabItem active={false} onClick={this.onClick}>Two</TabItem>
<TabItem active={false} onClick={this.onClick}>Three</TabItem> 
```

这样写可以实现功能，但未免过于繁琐，且不利于维护。我们希望可以简单点，最好代码就这样：

```js
<Tabs>
  <TabItem>One</TabItem>
  <TabItem>Two</TabItem>
  <TabItem>Three</TabItem>
</Tabs>
```

类似这种场景，父子组件不通过 props 传递，二者之间有某种神秘的“组合”，就是我们所说的“组合组件”。

##### 实现方式

我们先写出 TabItem 的代码，如下：

```js
const TabItem = (props) => {
  const {active, onClick} = props;
  const tabStyle = {
    'max-width': '150px',
    color: active ? 'red' : 'green',
    border: active ? '1px red solid' : '0px',
  };
  return (
    <h1 style={tabStyle} onClick={onClick}>
      {props.children}
    </h1>
  );
};
```

有了 TabItem ，我们再看下 TabItem 的调用方式。

```js
<Tabs>
  <TabItem>One</TabItem>
  <TabItem>Two</TabItem>
  <TabItem>Three</TabItem>
</Tabs>
```

没有 props 传递，怎么悄无声息地把 active 和 onClick 传递给 TabItem ？

我们可以把 props.children 拷贝一份，这样就有机会去篡改这份拷贝，最后渲染这份拷贝就好了。

我们来看 Tabs 的实现代码：

```js
class Tabs extends React.Component {
  state = {
    activeIndex:  0
  }

  render() {
    const newChildren = React.Children.map(this.props.children, (child, index) => {
      if (child.type) {
        return React.cloneElement(child, {
          active: this.state.activeIndex === index,
          onClick: () => this.setState({activeIndex: index})
        });
      } else {
        return child;
      }
    });

    return (
      <Fragment>
        {newChildren}
      </Fragment>
    );
  }
}
```

在 render 函数中，我们用了 React 中不常用的两个 API：

- React.Children.map
- React.cloneElement

使用 React.Children.map，可以遍历 children 中所有的元素，因为 children 可能是一个数组嘛。

使用 React.cloneElement 可以复制某个元素。这个函数第一个参数就是被复制的元素，第二个参数可以增加新产生元素的 props，我们就是利用这个机会，把 active 和 onClick 添加了进去。

这两个 API 双剑合璧，就能实现不通过表面的 props 传递，完成两个组件的“组合”。

##### 实际应用

应用组合组件的往往是共享组件库，把一些常用的功能封装在组件里，让应用层直接用就行。在 antd 和 bootstrap 这样的共享库中，都使用了组合组件这种模式。

<br/>

#### 模式总结

所谓模式，就是特定于一种问题场景的解决办法。

> 模式(Pattern) = 问题场景(Context) + 解决办法(Solution)

<br/>

如果不搞清楚场景，单纯知道有这么一个办法，就好比拿到了一杆枪却不知道这杆枪用于打什么目标，是没有任何意义的。并不是所有的枪都是一样的，有的枪擅长狙击，有的枪适合近战，有的枪只是发个信号。

模式就是我们的武器，我们一定要搞清楚一件武器应用的场合，才能真正发挥这件武器的威力。

<br/>

### 高阶组件实现方法

实现高阶组件的方法有：

#### 属性代理

定义：高阶组件通过被包裹的 React 组件来操作 props。

```js
import React from 'react';

const MyContainer = WrapComponent =>
  class extends React.Component {
    render () {
      return <WrapComponent {...this.props} />;
    }
  };

```

高阶组件的作用有：控制 props、通过 refs 使用引用、抽象 state 和使用其他元素包裹。

##### 控制 props

我们可以读取、增加、编辑或是移除从 WrappedComponent 传进来的 props，但需要小心删除与编辑重要的 props。我们应该尽可能对高阶组件的 props 作新的命名以防止混淆。

##### 通过 refs 使用引用

在高阶组件中，我们可以接受 refs 使用WrappedComponent 的引用。

```js
import React, {Component} from 'React';
const MyContainer = WrappedComponent =>
  class extends Component {
    proc (wrappedComponentInstance) {
      wrappedComponentInstance.method ();
    }
    render () {
      const props = Object.assign ({}, this.props, {
        ref: this.proc.bind (this),
      });
      return <WrappedComponent {...props} />;
    }
  };
```

当 WrappedComponent 被渲染时，refs 回调函数就会被执行，这样就会拿到一份Wrapped-Component 实例的引用。这就可以方便地用于读取或增加实例的 props，并调用实例的方法。

##### 抽象 state

我们可以通过 WrappedComponent 提供的 props 和回调函数抽象 state，高阶组件可以将原组件抽象为展示型组件，分离内部状态。

```js
import React, {Component} from 'React';
const MyContainer = WrappedComponent =>
  class extends Component {
    constructor (props) {
      super (props);
      this.state = {
        name: '',
      };
      this.onNameChange = this.onNameChange.bind (this);
    }
    onNameChange (event) {
      this.setState ({
        name: event.target.value,
      });
    }
    render () {
      const newProps = {
        name: {
          value: this.state.name,
          onChange: this.onNameChange,
        },
      };
      return <WrappedComponent {...this.props} {...newProps} />;
    }
  };

```

我们把 input 组件中对 name prop 的 onChange 方法提取到高阶组件中，这样就有效地抽象了同样的 state 操作。可以这么来使用它

```js
import React, {Component} from 'React';

@MyContainer 
class MyComponent extends Component {
  render () {
    return <input name="name" {...this.props.name} />;
  }
}
```

通过这样的封装，我们就得到了一个被控制的 input 组件。

##### 使用其他元素包裹 WrappedComponent

我们还可以使用其他元素来包裹 WrappedComponent，这既可以是为了加样式，也可 以是为了布局。

```js
import React, {Component} from 'React';
const MyContainer = WrappedComponent =>
  class extends Component {
    render () {
      return (
        <div style={{display: 'block'}}>
          {' '}<WrappedComponent {...this.props} />
        </div>
      );
    }
  };
```

<br/>


#### 反向继承

定义：高阶组件继承于被包裹的 React 组件（从字面意思上看，它一定与继承特性相关）


简单例子：高阶组件返回的组件继承于 WrappedComponent。因为被动地继承了 WrappedComponent，所有的调用都会反向，这也是这种方法的由来。

```js
const MyContainer = WrappedComponent =>
  class extends WrappedComponent {
    render () {
      return super.render ();
    }
  };
```

在反向继承方法中，高阶组件可以使用 WrappedComponent 引用，这意味着它可以使用WrappedComponent 的 state、props 、生命周期和 render 方法。但它不能保证完整的子组件树被解析。

反向继承两大特点:

##### 渲染劫持

渲染劫持指的就是高阶组件可以控制 WrappedComponent 的渲染过程，并渲染各种各样的结 果。我们可以在这个过程中在任何 React 元素输出的结果中读取、增加、修改、删除 props，或 读取或修改 React 元素树，或条件显示元素树，又或是用样式控制包裹元素树。

正如之前说到的，反向继承不能保证完整的子组件树被解析，这意味着将限制渲染劫持功能。 渲染劫持的经验法则是我们可以操控 WrappedComponent 的元素树，并输出正确的结果。但如果 元素树中包括了函数类型的 React 组件，就不能操作组件的子组件。

```js
const MyContainer = WrappedComponent =>
  class extends WrappedComponent {
    render () {
      if (this.props.loggedIn) {
        return super.render ();
      } else {
        return null;
      }
    }
  };
```


##### 控制 state

高阶组件可以读取、修改或删除WrappedComponent 实例中的 state，如果需要的话，也可以 增加 state。但这样做，可能会让WrappedComponent 组件内部状态变得一团糟。大部分的高阶组 件都应该限制读取或增加 state，尤其是后者，可以通过重新命名 state，以防止混淆。

```js
const MyContainer = WrappedComponent =>
  class extends WrappedComponent {
    render () {
      return (
        <div>
          <h2>HOC Debugger Component</h2>
          <p>Props</p>
          {' '}
          <pre>{JSON.stringify (this.props, null, 2)}</pre>
          {' '}
          <p>State</p>
          <pre>{JSON.stringify (this.state, null, 2)}</pre>
          {' '}
          {super.render ()}
        </div>
      );
    }
  };
```

<br/>

### 状态管理·第三方工具

上文提到了[状态管理·组件状态](#状态管理·组件状态)，接下来我们来看看社区主流的状态管理工具。

<br/>

#### Redux

##### 理解 Redux

要理解 Redux，首先要明白我们为什么需要 Redux，或者说，Redux 适用于什么样的场景。

在真实应用中，React 组件树会很庞大很复杂，两个没有父子关系的 React 组件之间要共享信息，怎么办呢？

最直观的做法，就是将状态保存在一个全局对象中，这个对象，叫 store。

如果 store 是一个普通对象，谁都可以修改，那状态就乱套了。所以我们要做一些限制，让 store 只接受特定事件，如果要修改 store 的数据，就往 store 发送这些事件， store 对事件进行响应，从而修改状态。

这里说的事件，就是 action ，而对应修改状态的函数，就是reducer。

Redux 的主要贡献，**就是限制了对状态的修改方式，让所有改变都可以被追踪**。

##### 适合 Redux 的场景

对于某个状态，到底是放在 Redux 的 Store 中呢，还是放在 React 组件自身的状态中呢？

针对这个问题，有以下原则：

第一步，看这个状态是否会被多个 React 组件共享。

第二步，看这个组件被 unmount 之后重新被 mount，之前的状态是否需要保留。

第三步，到这一步，基本上可以确定，这个状态可以放在 React 组件中了。

##### Redux 和 React 结合的最佳实践

一、Store 上的数据应该范式化。

所谓范式化，就是尽量减少冗余信息，像设计 MySQL 这样的关系型数据库一样设计数据结构。

二、使用 selector。

对于 React 组件，需要的是『反范式化』的数据，当从 Store 上读取数据得到的是范式化的数据时，需要通过计算来得到反范式化的数据。你可能会因此担心出现问题，这种担心不是没有道理，毕竟，如果每次渲染都要重复计算，这种浪费积少成多可能真会产生性能影响，所以，我们需要使用 seletor。业界应用最广的 selector 就是 reslector 。

reselector 的好处，是把反范式化分为两个步骤，第一个步骤是简单映射，第二个步骤是真正的重量级运算，如果第一个步骤发现产生的结果和上一次调用一样，那么第二个步骤也不用计算了，可以直接复用缓存的上次计算结果。

绝大部分实际场景中，总是只有少部分数据会频繁发生变化，所以 reselector 可以避免大量重复计算。

三、只 connect 关键点的 React 组件

当 Store 上状态发生改变的时候，所有 connect 上这个 Store 的 React 组件会被通知：『状态改变了！』

然后，这些组件会进行计算。connect 的实现方式包含 shouldComponentUpdate 的实现，可以阻挡住大部分不必要的重新渲染，但是，毕竟处理通知也需要消耗 CPU，所以，尽量让关键的 React 组件 connect 到 store 就行。

一个实际的例子就是，一个列表种可能包含几百个项，让每一个项都去 connect 到 Store 上不是一个明智的设计，最好是只让列表去 connect，然后把数据通过 props 传递给各个项。

##### 如何实现异步操作

使用 Redux 对于同步状态更新非常顺手，但是，遇到需要异步更新状态的场景，例如调用 AJAX 从服务器获得数据，这时候单用 Redux 就不够了，需要其他方式来辅助。

至今为止，还无法推荐一个杀手级的方法，各种方法都在吹嘘自己多厉害，但是任何一种方法都是易用性和复杂性的平衡。

最简单的 redux-thunk，代码量少，只有几行，用起来也很直观，但是开发者要写很多代码；而比较复杂的 redux-observable 相当强大，可以只用少量代码就实现复杂功能，但是前提是你要学会 RxJS，RxJS 本身学习曲线很陡，内容需要 一本书 的篇幅来介绍，这就是代价。

读者在自己的项目中，无论选择什么方式，一定要考虑这个方式的复杂度和学习成本。

在这里我不想过多介绍任何一种 Redux 扩展，因为任何一种都比不上 React 将要支持的 Suspense，Suspense 才是 React 中做异步操作的未来，在第 19 小节会详细介绍 Suspense。

<br/>

#### Mobx

##### 理解 Mobx

我们用 Mobx 来实现一个很简单的计数工具，首先，需要有一个对象来记录计数值，代码如下：

```js
import {observable} from 'mobx';

const counter = observable ({
  count: 0,
});
```

在上面的代码中，counter 是一个对象，其实就是用 observable 函数包住一个普通 JS 对象，但是 observable 的介入，让 counter 对象拥有了神力。

我们用最简单的代码来展示这种“神力”，代码如下：

```js
import {autorun} from 'mobx';

window.counter = counter;

autorun (() => {
  console.log ('#count', counter.count);
});
```

把 counter 赋值给 window.counter，是为了让我们在 Chrome 的开发者界面可以访问。用 autorun 包住了一个函数，这个函数输出 counter.count 的值，这段代码的作用，我们很快就能看到。

在 Chrome 的开发者界面，我们可以直接访问 window.counter.count，神奇之处是，如果我们直接修改 window.counter.count 的值，可以直接触发 autorun 的函数参数！


<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/170.png' width='400'>

这个现象说明，mobx 的 observable 拥有某种“神力”，任何对这个对象的修改，都会立刻引发某些函数被调用。和 observable 这个名字一样，被包装的对象变成了“被观察者”，而被调用的函数就是“观察者”，在上面的例子中，autorun 的函数参数就是“观察者”。

Mobx 这样的功能，等于实现了设计模式中的“观察者模式”（Observer Pattern），通过建立 observer 和 observable 之间的关联，达到数据联动。不过，传统的“观察者模式”要求我们写代码建立两者的关联，也就是写类似下面的代码：

```js
observable.register(observer);
```

Mobx 最了不起之处，在于不需要开发者写上面的关联代码，Mobx自己通过解析代码就能够自动发现 observer 和 observable 之间的关系。

我们很自然想到，如果让我们的数据拥有这样的“神力”，那我们就不用在修改完数据之后，再费心去调用某些函数使用这些数据了，数据管理会变得十分轻松。

##### 用 decorator 来使用 Mobx

Mobx 和 React 并无直接关系，为了建立二者的关系，需要安装 mobx-react

还是以 Counter 为例，看如何用 decorator 使用 Mobx，我们先看代码：

```js
import {observable} from 'mobx';
import {observer} from 'mobx-react';

@observer 
class Counter extends React.Component {
  @observable count = 0;

  onIncrement = () => {
    this.count++;
  };

  onDecrement = () => {
    this.count--;
  };

  componentWillUpdate () {
    console.log ('#enter componentWillUpdate');
  }

  render () {
    return (
      <CounterView
        caption="With decorator"
        count={this.count}
        onIncrement={this.onIncrement}
        onDecrement={this.onDecrement}
      />
    );
  }
}
```

在上面的代码中，Counter 这个 React 组件自身是一个 observer，而 observable 是 Counter 的一个成员变量 count。

注意 observer 这 个decorator 来自于 mobx-react，它是 Mobx 世界和 React 的桥梁，被它“装饰”的组件，就是一个“观察者”。

本例中，成员变量 count 是被观察者，只要被观察者一变化，作为观察者的 Counter 组件就会重新渲染。

##### 独立的 Store

真实的业务场景是一个状态需要多个组件共享，所以 observable 一般是在 React 组件之外。

我们重写一遍 Counter 组件，代码如下：

```js
const store = observable ({
  count: 0,
});
store.increment = function () {
  this.count++;
};
store.decrement = function () {
  this.count--;
}; // this decorator is must

@observer 
class Counter extends React.Component {
  onIncrement = () => {
    store.increment ();
  };

  onDecrement = () => {
    store.decrement ();
  };

  render () {
    return (
      <CounterView
        caption="With external state"
        count={store.count}
        onIncrement={this.onIncrement}
        onDecrement={this.onDecrement}
      />
    );
  }
}
```

<br/>

#### Mobx 和 Redux 的比较

Mobx 和 Redux 的目标都是管理好应用状态，但是最根本的区别在于对数据的处理方式不同。

Redux 认为，数据的一致性很重要，为了保持数据的一致性，要求Store 中的数据尽量范式化，也就是减少一切不必要的冗余，为了限制对数据的修改，要求 Store 中数据是不可改的（Immutable），只能通过 action 触发 reducer 来更新 Store。

Mobx 也认为数据的一致性很重要，但是它认为解决问题的根本方法不是让数据范式化，而是不要给机会让数据变得不一致。所以，Mobx 鼓励数据干脆就“反范式化”，有冗余没问题，只要所有数据之间保持联动，改了一处，对应依赖这处的数据自动更新，那就不会发生数据不一致的问题。

值得一提的是，虽然 Mobx 最初的一个卖点就是直接修改数据，但是实践中大家还是发现这样无组织无纪律不好，所以后来 Mobx 还是提供了 action 的概念。和 Redux 的 action 有点不同，Mobx 中的 action 其实就是一个函数，不需要做 dispatch，调用就修改对应数据

如果想强制要求使用 action，禁止直接修改 observable 数据，使用 Mobx 的 configure，如下：

```js
import {configure} from 'mobx';

configure({enforceActions: true});
```

总结一下 Redux 和 Mobx 的区别，包括这些方面：

- Redux 鼓励一个应用只用一个 Store，Mobx 鼓励使用多个 Store；
- Redux 使用“拉”的方式使用数据，这一点和 React是一致的，但 Mobx 使用“推”的方式使用数据，和 RxJS 这样的工具走得更近；
- Redux 鼓励数据范式化，减少冗余，Mobx 容许数据冗余，但同样能保持数据一致。

<br/>

### 样式处理

#### 基本样式设置

我们可以使用 classnames 库来操作类。

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
// 使用了 classnames 库代码后，就可以变得很简单: 
import React, { Component } from 'react';
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

#### CSS模块

CSS 模块化要解决两个问题：CSS 样式的导入与导出。灵活按需导入以便复用代码，导出时要能够隐藏内部作用域，以免造成全局污染。

CSS 模块化解决方案有两种：Inline Style、CSS Modules。

Inline Style

这种方案彻底抛弃 CSS，使用 JS 或 JSON 来写样式，能给 CSS 提供 JS 同样强大的模块化能力。但缺点同样明显，Inline Style 几乎不能利用 CSS 本身 的特性，比如级联、媒体查询(media query)等，:hover 和 :active 等伪类处理起来比较 复杂。另外，这种方案需要依赖框架实现，其中与 React 相关的有 Radium、jsxstyle 和 react-style。

CSS Modules

依旧使用 CSS，但使用 JS 来管理样式依赖。CSS Modules 能最大化地结合现有 CSS 生态和 JS 模块化能力，其 API 非常简洁，学习成本几乎为零。 发布时依旧编译出单独的 JS 和 CSS 文件。webpack css-loader 内置 CSS Modules 功能。

<br/>

#### CSS Modules 注意事项

##### 样式默认局部

使用了 CSS Modules 后，就相当于给每个 class 名外加了 :local，以此来实现样式的局部化。如果我们想切换到全局模式，可以使用 :global 包裹

##### 使用 composes 来组合样式

```css
/* components/Button.css */ 
.base { /* 所有通用的样式 */ }
.normal { 
  composes: base; 
  /* normal其他样式 */
}

.disabled {
  composes:base; 
  /* disabled 其他样式 */
}
```

生成的 HTML 变为:

```html
<button class="button--base-abc53 button--normal-abc53"> Processing... </button>
```

由于在 .normal 中组合了 .base，所以编译后的 normal 会变成两个 class。 此外，使用 composes 还可以组合外部文件中的样式:

```css
/* settings.css */
.primary-color {
  color: #f40; 
}
/* components/Button.css */ 
.base { /* 所有通用的样式 */ }
.primary {
  composes: base;
  composes: $primary-color from './settings.css'; /* primary 其他样式 */
}
```

##### 实现 CSS 与 JS 变量共享

:export 关键字可以把 CSS 中的变量输出到 JS 中

```css
/* config.scss */ 
$primary-color: '#f40';
:export {
  primaryColor: $primary-color;
}
```

```js
/* app.js */
import style from 'config.scss';
// 会输出 #F40 console.log(style.primaryColor);
```

<br/>


### React Router

随着 AJAX 技术的成熟，现在单页应用（Single Page Application）已经是前端网页界的标配，名为“单页”，其实在设计概念上依然是多页的界面，只不过从技术层面上页之间的切换是没有整体网页刷新的，只需要做局部更新。

要实现“单页应用”，一个最要紧的问题就是做好“路由”（Routing)，也就是处理好下面两件事：

- 把 URL 映射到对应的页面来处理；
- 页面之间切换做到只需局部更新。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/127.jpg' width='600'>
<br/>

#### react router v4 的动态路由

react-router 的 v3 和 v4 版完完全全是不同的两个工具，最大的区别是 v3 为静态路由， v4 做到了动态路由。

所谓“静态路由”，就是说路由规则是固定的。

所谓动态路由，指的是路由规则不是预先确定的，而是在渲染过程中确定的。

#### 使用

react-router 的工作方式，是在组件树顶层放一个 Router 组件，然后在组件树中散落着很多 Route 组件（注意比 Router 少一个“r”），顶层的 Router 组件负责分析监听 URL 的变化，在它保护伞之下的 Route 组件可以直接读取这些信息。

很明显，Router 和 Route 的配合，就是之前我们介绍过的“提供者模式”，Router 是“提供者”，Route是“消费者”。

更进一步，Router 其实也是一层抽象，让下面的 Route 无需各种不同 URL 设计的细节，不要以为 URL 就一种设计方法，至少可以分为两种。

第一种很自然，比如 / 对应 Home 页，/about 对应 About 页，但是这样的设计需要服务器端渲染，因为用户可能直接访问任何一个 URL，服务器端必须能对 /的访问返回 HTML，也要对 /about 的访问返回 HTML。

第二种看起来不自然，但是实现更简单。只有一个路径 /，通过 URL 后面的 # 部分来决定路由，/#/ 对应 Home 页，/#/about 对应 About 页。因为 URL 中#之后的部分是不会发送给服务器的，所以，无论哪个 URL，最后都是访问服务器的 / 路径，服务器也只需要返回同样一份 HTML 就可以，然后由浏览器端解析 # 后的部分，完成浏览器端渲染。

在 react-router，有 BrowserRouter 支持第一种 URL，有 HashRouter 支持第二种 URL。

#### 动态路由

假设，我们增加一个新的页面叫 Product，对应路径为 /product，但是只有用户登录了之后才显示。如果用静态路由，我们在渲染之前就确定这条路由规则，这样即使用户没有登录，也可以访问 product，我们还不得不在 Product 组件中做用户是否登录的检查。

如果用动态路由，则只需要在代码中的一处涉及这个逻辑：

```js
<Switch>
  <Route exact path='/' component={Home}/>
  {
    isUserLogin() &&
    <Route exact path='/product' component={Product}/>,
  }  
  <Route path='/about' component={About}/>
</Switch>
```

#### 常见API

1. `<Link>` ：普通链接，不会触发浏览器刷新
2. `<NavLink>`：类似`<Link>`但是会添加当前选中状态
3. `<Prompt>`：满足条件时提示用户是否离开当前页面
4. `<Redirect>`：重定向当前页面，例如登录判断
5. `<Route>`：路由配置的核心标记，路径匹配时显示对应组件
6. `<Switch>`：只现实第一个匹配路由

#### React Router技巧

1. 如何通过URL传递参数：<Route path='/topic/:id'/>
2. 如何获取参数：this.props.match.params
3. 路由匹配进阶[资料](https://github.com/pillarjs/path-to-regexp)

<br/>

### 服务器端渲染

最近几年浏览器端框架很繁荣，以至于很多新入行的开发者只知道浏览器端渲染框架，都不知道存在服务器端渲染这回事，其实，网站应用最初全都是服务器端渲染，由服务器端用 PHP、Java 或者 Python 等其他语言产生 HTML 来给浏览器端解析。

相比于浏览器端渲染，服务器端渲染的好处是：

1. 缩短首屏渲染时间
2. 更好的搜索引擎优化

#### 大体流程

React v16 之前的版本，代码是这样：

```js
import React from 'react';
import ReactDOMServer from 'react-dom/server';

// 把产生html返回给浏览器端
const html = ReactDOMServer.renderToString(<Hello />);
```

从 React v16 开始，上面的服务器端代码依然可以使用，但是也可以把 renderToString 替换为 renderToNodeStream，代码如下：

```js
import React from 'react';
import ReactDOMServer from 'react-dom/server';

// 把渲染内容以流的形式塞给response
ReactDOMServer.renderToNodeStream(<Hello />).pipe(response);
```

此外，浏览器端代码也有一点变化，ReactDOM.render 依然可以使用，但是官方建议替换为 ReactDOM.hydrate，原来的 ReactDOM.render 将来会被废弃掉。

renderToString 的功能是一口气同步产生最终 HTML，如果 React 组件树很庞大，这样一个同步过程可能比较耗时。

renderToNodeStream 把渲染结果以“流”的形式塞给 response 对象，这意味着不用等到所有 HTML 都渲染出来了才给浏览器端返回结果，“流”的作用就是有多少内容给多少内容，这样可以改进首屏渲染时间。

#### “脱水”和“注水”

React 有一个特点，就是把内容展示和动态功能集中在一个组件中。比如，一个 Counter 组件既负责怎么画出内容，也要负责怎么响应按键点击，这当然符合软件高内聚性的原则，但是也给服务器端渲染带来更多的工作。

设想一下，如果只使用服务器端渲染，那么产生的只有 HTML，虽然能够让浏览器端画出内容，但是，没有 JS 的辅助是无法响应用户交互事件的。

如何让页面响应用户事件？其实我们已经做过这件事了，Counter 组件里面已经有对按钮事件的处理，我们所要做的只是让 Counter 组件在浏览器端重新执行一遍，也就是 mount 一遍就可以了。

也就是说，**如果想要动态交互效果，使用 React 服务器端渲染，必须也配合使用浏览器端渲染**。

现在问题变得更加有趣了，在服务器端我们给 Counter 一个初始值（这个值可以不是缺省的 0），让 Counter 渲染产生 HTML，这些 HTML 要传递给浏览器端，为了让 Counter 的 HTML“活”起来点击相应事件，必须要在浏览器端重新渲染一遍 Counter 组件。在浏览器端渲染 Counter 之前，用户就可以看见 Counter 组件的内容，但是无法点击交互，要想点击交互，就必须要等到浏览器端也渲染一次 Counter 之后。

接下来的一个问题，如果服务器端塞给 Counter 的数据和浏览器端塞给 Counter 的数据不一样呢？

在 React v16 之前，React 在浏览器端渲染之后，会把内容和服务器端给的 HTML 做一个比对。如果完全一样，那最好，接着用服务器端 HTML 就好了；如果有一丁点不一样，就会立刻丢掉服务器端的 HTML，重新渲染浏览器端产生的内容，结果就是用户可以看到界面闪烁。因为 React 抛弃的是整个服务器端渲染内容，组件树越大，这个闪烁效果越明显。

React 在 v16 之后，做了一些改进，不再要求整个组件树两端渲染结果分毫不差，但是如果发生不一致，依然会抛弃局部服务器端渲染结果。

总之，**如果用服务器端渲染，一定要让服务器端塞给 React 组件的数据和浏览器端一致**。

为了达到这一目的，必须把传给 React 组件的数据给保留住，随着 HTML 一起传递给浏览器网页，这个过程，叫做“脱水”（Dehydrate）；在浏览器端，就直接拿这个“脱水”数据来初始化 React 组件，这个过程叫“注水”（Hydrate）。

前面提到过 React v16 之后用 React.hydrate 替换 React.render，这个 hydrate 就是“注水”。


<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/171.png' width='600'>

总之，为了实现React的服务器端渲染，必须要处理好这两个问题：

- 脱水
- 注水

<br/>

#### 同构应用

有很多文章都提到同构应用，其实就是首屏使用服务端渲染，后面使用浏览器端渲染的应用。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/130.jpg' width='600'>
<br/>


### 使用 Next.js 实现服务端渲染

上文提到[服务器端渲染](#服务器端渲染)，不过，服务器端渲染的问题并不这么简单，一个最直接的问题，就是怎么处理多个页面的『单页应用』?

所谓单页应用，就是虽然用户感觉有多个页面，但是实现上只有一个页面，用户感觉到页面可以来回切换，但其实只是一个页面并没有完全刷新，只是局部界面更新而已。

假设一个单页应用有三个页面 Home、Prodcut 和 About，分别对应的的路径是 /home、/product 和 /about，而且三个页面都依赖于 API 调用来获取外部数据。

现在我们要做服务器端渲染，如果只考虑用户直接在地址栏输入 /home、/product 和 /about 的场景，很容易满足，按照上面说的套路做就是了。但是，这是一个单页应用，用户可以在 Home 页面点击链接无缝切换到 Product，这时候 Product 要做完全的浏览器端渲染。换句话说，每个页面都需要既支持服务器端渲染，又支持完全的浏览器端渲染，更重要的是，对于开发者来说，肯定不希望为了这个页面实现两套程序，所以必须有同时满足服务器端渲染和浏览器端渲染的代码表示方式。

#### getInitialProps

我们通过一个简单的例子来讲解Next.js中最重要的概念getInitialProps。

```js
import React from 'react';

const timeout = (ms, result) => {
  return new Promise (resolve => setTimeout (() => resolve (result), ms));
};

const Home = props => (
  <h1>
    Hello {props.userName}
  </h1>
);

Home.getInitialProps = async () => {
  return await timeout (200, {userName: 'Morgan'});
};

export default Home;
```

这里模拟了一个延时操作用以获取userName，并将其展示在页面上。

这段代码的关键在于getInitialProps。

这个 getiInitialProps 是 Next.js 最伟大的发明，它确定了一个规范，一个页面组件只要把访问 API 外部资源的代码放在 getInitialProps 中就足够，其余的不用管，Next.js 自然会在服务器端或者浏览器端调用 getInitialProps 来获取外部资源，并把外部资源以 props 的方式传递给页面组件。

注意 getInitialProps 是页面组件的静态成员函数，也可以在组件类中加上 static 关键字定义。

```js
class Home extends React.Component {
  static async getInitialProps () {}
}
```

我们可以这样来看待 getInitialProps，它就是 Next.js 对代表页面的 React 组件生命周期的扩充。React 组件的生命周期函数缺乏对异步操作的支持，所以 Next.js 干脆定义出一个新的生命周期函数 getInitialProps，在调用 React 原生的所有生命周期函数之前，**Next.js 会调用 getInitialProps 来获取数据，然后把获得数据作为 props 来启动 React 组件的原生生命周期过程**。

这个生命周期函数的扩充十分巧妙，因为：

- 没有侵入 React 原生生命周期函数，以前的 React 组件该怎么写还是怎么写；
- getInitialProps 只负责获取数据的过程，开发者不用操心什么时候调用 getInitialProps，依然是 React 哲学的声明式编程方式；
- getInitialProps 是 async 函数，可以利用 JS 语言的新特性，用同步的方式实现异步功能。

#### Next.js 的“脱水”和“注水”

我们打开Next应用的网页源代码，可以看到类似下面的内容：

```html
<script>
  __NEXT_DATA__ = {
    "props":{
      "pageProps": {"userName":"Morgan"}},
      "page":"/","pathname":"/","query":{},"buildId":"-","assetPrefix":"","nextExport":false,"err":null,"chunks":[]}
</script>
```

Next.js 在做服务器端渲染的时候，页面对应的 React 组件的 getInitialProps 函数被调用，异步结果就是“脱水”数据的重要部分，除了传给页面 React 组件完成渲染，还放在内嵌 script 的 __NEXT_DATA__ 中，这样，在浏览器端渲染的时候，是不会去调用 getInitialProps 的，直接通过 __NEXT_DATA__ 中的“脱水”数据来启动页面 React 组件的渲染。

这样一来，如果 getInitialProps 中有调用 API 的异步操作，只在服务器端做一次，浏览器端就不用做了。

那么，getInitialProps 什么时候会在浏览器端调用呢？

当在单页应用中做页面切换的时候，比如从 Home 页切换到 Product 页，这时候完全和服务器端没关系，只能靠浏览器端自己了，Product页面的 getInitialProps 函数就会在浏览器端被调用，得到的数据用来开启页面的 React 原生生命周期过程。

关键点是，浏览器可能会直接访问 /home 或者 /product，也可能通过网页切换访问这两个页面，也就是说 Home 或者 Product 都可能被服务器端渲染，也可能完全只有浏览器端渲染，不过，这对应用开发者来说无所谓，应用开发者只要写好 getInitialProps，至于调用 getInitialProps 的时机，交给 Next.js 处理就好了。

<br/>

### 服务端渲染小结

react 提供了renderToString、renderToNodeStream、hydrate等API支持服务端渲染，但Facebook官方并没有使用react的服务端渲染，导致react服务端渲染没有一个官方标准。

服务端渲染的思路并不难，就是在服务端渲染出HTML传给浏览器去解析。

难就难在，服务端渲染的数据从何而来。如果服务端渲染的数据和浏览器端渲染的数据不一致，浏览器端会重新执行渲染，页面会出现闪烁。

为什么有了服务端渲染，还需要关注浏览器端渲染呢？

这是因为服务端渲染只是返回了HTML，页面能绘制出来，却没办法响应用户操作，所以必须重新进行浏览器端渲染，让页面可以正常响应用户操作。当浏览器端渲染出的HTML跟服务端返回的HTML不一致时，就会出现上面说的闪烁。

要解决这个问题，就引入了“注水”跟“脱水”的概念。

服务端渲染时，获取的数据，一方面用于生成最终的HTML，另一方面，也会包含在HTML中返回给浏览器端，这个过程称为“脱水”。

浏览器端拿到脱水的数据进行渲染，就保证了渲染出的HTML跟服务端返回的一致，这个过程就是“注水”，涉及的API就是hydrate。

原理搞明白了，如何实施呢？如果我们做的是单页应用，那问题更加麻烦。因为用户可以通过不同的URL返回页面，这意味着我们每个页面都要既支持服务端渲染，也支持浏览器端渲染，但我们肯定不希望为每个页面写两份代码！

这就轮到 Next.js 登场了。

Next.js 是目前解决服务端渲染最好的框架。他通过增加 getInitialProps 这个API优雅的解决了上述的问题。

Next.js 将服务端渲染脱水后的数据，通过 __NEXT_DATA__ 返回给浏览器端，首屏加载可以使用该数据进行渲染，就保证前后数据一致，页面不会闪烁。

浏览器可能会直接访问 /home 或者 /product，也可能通过网页切换访问这两个页面，也就是说 Home 或者 Product 都可能被服务器端渲染，也可能完全只有浏览器端渲染，不过，这对应用开发者来说无所谓，应用开发者只要写好 getInitialProps，至于调用 getInitialProps 的时机，交给 Next.js 处理就好了。

### 常用开发调试工具

开发react应用最常用的调试工具有：ESLint，Prettier，React DevTool，Redux DevTool

ESLint
- 使用.eslintrc进行规则的配置
- 使用airbnb的JS代码风格

Prettier
- 代码格式化的神器
- 保证更容易写出风格一致的代码

> 小技巧：在Chrome中监测react性能：在URL后加?react_perf，比如：localhost:3000/?react_perf

<br/>


### 组件测试

React 让前端单元测试变得容易:
- React 应用很少需要访问浏览器API
- 虚拟DOM可以在nodejs环境运行和测试
- Redux隔离了状态管理，纯数据层单元测试

React 组件的单元测试，只有三个要点：

- 用 Jest；
- 用 Enzyme；
- 保持 100% 的代码覆盖率。

#### Jest

“测试驱动”难以开展，主要有几个原因：

- 单元测试用例庞大，执行时间过长。
- 单元测试用例之间相互影响。

Jest 较好地解决了上面说的问题，因为 Jest 最重要的一个特性，就是支持并行执行。

Jest 为每一个单元测试文件创造一个独立的运行环境，换句话说，Jest 会启动一个进程执行一个单元测试文件，运行结束之后，就把这个执行进程废弃了，这个单元测试文件即使写得比较差，把全局变量污染得一团糟，也不会影响其他单元测试文件，因为其他单元测试文件是用另一个进程来执行。

更妙的是，因为每个单元测试文件之间再无纠葛，Jest 可以启动多个进程同时运行不同的文件，这样就充分利用了电脑的多 CPU 多核，单进程 100 秒才完成的测试执行过程，8 核只需要 12.5 秒，速度快了很多。

使用 create-react-app 产生的项目自带 Jest 作为测试框架，不奇怪，因为 Jest 和 React 一样都是出自 Facebook。

jest中文[教程](https://jestjs.io/docs/zh-Hans/getting-started)

#### Enzyme

Enzyme 是最受欢迎的 React 测试工具库。

Enzyme 的官网[地址](https://airbnb.io/enzyme/)

#### 代码覆盖率

一个应用不光所有的单元测试都要通过，而且所有单元测试都必须覆盖到代码 100% 的角落。

如果对覆盖率的要求低于 100%，时间一长，质量必定会越来越下滑

在 create-react-app 创造的应用中，已经自带了代码覆盖率的支持，运行下面的命令，不光会运行所有单元测试，也会得到覆盖率汇报。

npm test -- --coverage
代码覆盖率包含四个方面：

- 语句覆盖率
- 逻辑分支覆盖率
- 函数覆盖率
- 代码行覆盖率

只有四个方面都是 100%，才算真的 100%。


<br/>

## 市场应用趋势

> 随着技术生态的发展，和应用问题的变迁，技术的应用场景和流行趋势会受到影响。这层回答“谁用，用在哪”的问题，反映你对技术应用领域的认识宽度。

<br/>

# 设计维度

<br/>

## 目标

> 为了解决用户的问题，技术本身要达成什么目标。这层定义“做到什么”。

<br/>

### 命令式编程VS声明式编程

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

react的核心理念之一就是函数式编程。

<br/>

### JSX

在JS中写HTML标记，这体现了高内聚。要达到这种效果，就必须依赖JSX。 

JSX 的本质不是模板引擎，而是动态创建组件的语法糖，它允许我们在JS代码中直接写HTML标记。最终生成的代码就是React.CreateElement。

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


## 实现原理

> 为了达到设计目标，该技术采用了什么原理和机制。实现原理层回答“怎么做到”的问题。把实现原理弄懂，并且讲清楚，是技术人员的基本功。

<br/>

### 生命周期函数

> 关于生命周期，可以参考这篇[文章](https://juejin.im/post/5b6f1800f265da282d45a79a)

生命周期函数指的是在某一个时刻组件会自动调用执行的函数。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/86.jpg' width='800'>
<br/>

也可以参考网上的[这张图](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)。

一些注意点：

不管是挂载阶段还是更新阶段，都要到render时才能获取到更新后的this.state。在componentWillMount、 componentWillReceiveProps、 shouldComponentUpdate 和 componentWillUpdate 中也还是无法获取到更新后的 this.state。

mountComponent 本质上是通过递归渲染内容的，由于递归的特性，父组件的 componentWillMount 在其子组件的 componentWillMount 之前调用，而父组件的 componentDidMount 在其子组件的 componentDidMount 之后调用。updateComponent同理。

updateComponent 负责管理生命周期中的 componentWillReceiveProps、shouldComponentUpdate、componentWillUpdate、render 和 componentDidUpdate。在 componentWillReceiveProps 中调用 setState，是不会触发 re-render 的，而是会进行 state 合并。禁止在 shouldComponentUpdate 和 componentWillUpdate 中调用 setState，这会造成循环调用，直至耗光浏览器内存后崩溃。

在 componentWillUnmount 中调用 setState，是不会触发 re-render 的。

无状态组件只是一个 render 方法，并没有组件类的实例化过程，也没有实例返回。无状态组件没有状态，没有生命周期，只是简单地接受 props 渲染生成 DOM 结构，是一个纯粹为渲染而生的组件。

<br/>

这里简单介绍下各个生命周期函数：

#### constructor

1. 用于初始化内部状态，很少使用
2. 唯一可以直接修改 state 的地方

#### getDerivedStateFromProps

1. 当 state 需要从 props 初始化时使用
2. 尽量不要使用：维护两者状态一致性会增加复杂度
3. 每次 render 都会调用
4. 典型场景：表单控件获取默认值

#### componentDidMount

1. UI 渲染完成后调用
2. 只执行一次
3. 典型场景：获取外部资源

#### componentWillUnmount

1. 组件移除时被调用
2. 典型场景：资源释放

#### getSnapshotBeforeUpdate

1. 在元素被渲染并写入 DOM 之前调用，这样，你在 DOM 更新前捕获 DOM 信息（例如：滚动位置）。
2. 在页面 render t前调用，state 已更新
3. 典型场景：获取 render 之前的 DOM 状态

#### componentDididUpdate

1. 每次 UI 更新时被调用
2. 典型场景：页面需要根据 props 变化重新获取数据

#### shouldComponentUpdate

1. 决定 VDOM 是否要重绘
2. 一般可以由 PureComponent 自动实现
3. 典型场景：性能优化

#### componentWillReceiveProps
注意下update阶段，触发组件update有两种情况，props或者state的修改。

可以看到，这两种情况生命周期函数是有重合的。唯一的不同就是props改变时，会先调用 componentWillReceiveProps

1. 一个组件要从父组件接受参数
2. 如果这个组件第一次存在于父组件中，不会执行
3. 如果这个组件之前已经存在于父组件中，才会执行

<br/>


### MV* 与 Flux

#### MVC/MVVM

MVC/MVVM 简称 MC* 模式，其中 MVVM 是从 MVC 演进而来的。

MVC 是一种架构设计模式，它通过关注数据界面分离，来鼓励改进应用程序结构。具体地 说，MVC 强制将业务数据(Model)与用户界面(View)隔离，用控制器(Controller)管理逻 辑和用户输入。

Model 负责保存应用数据，和后端交互同步应用数据，或校验数据。

View 是 Model 的可视化表示，表示当前状态的视图。

Controller负责连接 View 和 Model，Model 的任何改变会应用到 View 中，View 的操作会通过 Controller应用到 Model 中。

Controller 管理了应用程序中 Model 和 View 之间的逻辑和协调。

MVC 的致命缺点：混乱的数据流动方式，此外，前端 MVC 模式的实现各有各的理解，千奇百怪。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/165.jpg' width='600'>
<br/>

MVVM 出现于 2005 年，最大变化在于 VM(ViewModel)代替了 C(Controller)。其关键“改 进”是数据绑定(DataBinding)，也就是说，View 的数据状态发生变化可以直接影响 VM，反之 亦然。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/164.jpg' width='800'>
<br/>

#### Flux 的解决方案

Flux 的核心思想就是数据和逻辑永远单向流动

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/166.jpg' width='600'>
<br/>

Flux 核心思想，也就是中心化控制。中心化控制让所有的请求与改变都只能通过 action 发出，统一 由 dispatcher 来分配。这样View就可以保持高度简洁，发生问题时也便于定位。比起 MVC 架构下数据或逻 辑的改动可能来自多个完全不同的源头，Flux 架构追查问题的复杂度和困难度显然要小得多。

Flux 的不足：冗余代码过多，每个应用中都需要手动创建一个 dispatcher 的示例，这还是让很多开发者觉得烦恼

如果非要把Flux 和MVC 做一个结构对比，那么， Flux 的Dispatcher 相当于MVC 的Controller, Flux 的Store 相当于MVC 的Model, Flux 的View 当然就对应MVC 的View了，至于多出来的这个Action ，可以理解为对应给MVC 框架的用户请求

#### Redux

Redux 是一个可预测的状态容器。简单地说，在摒弃了传统 MVC 的发布/订阅模式并通过 Redux 三大原则强化对状态 的修改后，使用 Redux 可以让你的应用状态管理变得可预测、可追溯。


redux的相关知识繁多，还包含了Mobx、dva，为此我将他抽离出来，请看[这里](https://github.com/jiangxia/FE-Knowledge/blob/master/posts/4-前端工程化/数据管理学习笔记.md)。

<br/>


### render的执行

1. 当组件的state和props发生改变时，render函数就会重新执行
2. 父组件render函数被执行时，它的子组件的render函数都将被重新运行一次

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

### 事件系统

VDOM 在内存中是以对象的形式存在的，如果想要在这些对象上添加事件，就会非常简单。

React 基于 VDOM 实现了一个 SyntheticEvent (合成事件)层，我们所定义的事件处理器会接收到一个 SyntheticEvent 对象的实例，它完全符合 W3C 标准，不会存在任何 IE 标准的兼容性问题。并且与原生的浏览器事件一样拥有同样的接口，同样支持事件的冒泡机制，我们可以使用 stopPropagation() 和 preventDefault() 来中断它。所有事件都自动绑定到最外层上。如果需要访问原生事件对象，可以使用 nativeEvent 属性。

#### 合成事件的实现机制

在 React 底层，主要对合成事件做了两件事:事件委派和自动绑定

##### 事件委派

react 并不会把事件处理函数直接绑定到真实的节点上，而是把所有事件绑定到结构的最外层，使用一个统一的事件监听器。

事件监听器上维持了一个映射来保存所有组件内部的事件监听和处理函数。

当组件挂载或卸载时，只是在这个统一的事件监听器上插入或删除一些对象

当事件发生时，首先被这个统一的事件监听器处理，然后在映射里找到真正的事件处理函数并调用。

这样做简化了事件处理和回收机制，效率也有很大提升。 

##### 自动绑定

在 React 组件中，每个方法的上下文都会指向该组件的实例，即自动绑定 this 为当前组件。 而且 React 还会对这种引用进行缓存，以达到 CPU 和内存的最优化。在使用 ES6 classes 或者纯函数时，这种自动绑定就不复存在了，我们需要手动实现 this 的绑定。

常见的绑定方法有：

- 双冒号语法：`<button onClick={::this.handleClick}>Test</button>`
- 构造器内使用bind绑定
- 箭头函数

<br/>

#### 合成事件与原生事件对比

##### 事件对象

原生 DOM 事件对象在 W3C 标准和 IE 标准下存在着差异。在低版本的 IE 浏览器中，只能使用 window.event 来获取事件对象。

而在 React 合成事件系统中，不存在这种兼容性问题，在事件处理函数中可以得到一个合成事件对象。

##### 事件类型

React 合成事件的事件类型是 JS 原生事件类型的一个子集

##### 事件传播与阻止事件传播

事件传播分为捕获阶段、目标阶段、冒泡阶段。

事件捕获在程序开发中的意义不大，还有兼容性问题。所以，React 的合成事件则并没有实现事件捕获，仅仅支持了事件冒泡机制。

阻止事件传播：阻止原生事件传播需要使用 e.preventDefault()，不过对于不支持该方法的浏览器(IE9 以 下)，只能使用 e.cancelBubble = true 来阻止。而在 React 合成事件中，只需要使用 e.preventDefault() 即可。

##### 事件绑定方式

原生事件有三种方式:

- 直接在DOM元素中绑定: `<button onclick="alert(1)">Test</button>`
- 在JS中，通过为元素的事件属性赋值的方式实现绑定：`el.onclick = e => {console.log(e)} `
- 通过事件监听函数来实现绑定：`el.addEventListener("click", ()=>{},false); el.attachEvent("onclick", ()=>{})`

React 合成事件的绑定方式则简单得多:`<button onClick={this.handleClick}>Test</button>`

<br/>

#### 获取真实DOM的方式

要获取真实的DOM节点有两种方式，一种是通过e.target，一种是ref。

但能不使用ref尽量不用

<br/>

#### 注意事项

一、原生事件

componentDidMount 会在组件已经完成安装并且在浏览器中存在真实的 DOM 后调用，此时我们就可以完成原生事件的绑定。

在 React 中使用 DOM 原生事件时，一定要在组件卸载时手动移除，否则很 可能出现内存泄漏的问题。而使用合成事件系统时则不需要，因为 React 内部已经帮你妥善地处理了。

二、合成事件与原生事件混用

尽量避免在 React 中混用合成事件和原生 DOM 事件。

阻止 React 事件冒泡的行为只能用于 React 合成事件系统 中，且没办法阻止原生事件的冒泡。反之，在原生事件中的阻止冒泡行为，却可以阻止 React 合成事件的传播。

React 的合成事件系统只是原生 DOM 事件系统的一个子集。它仅仅实现了 DOM Level 3 的事件接口，并且统一了浏览器间的兼容问题。有些事件 React 并没有实现，或者受某些限制没办法去实现，比如 window 的 resize 事件。

<br/>


## 优劣局限

> 每种技术实现，都有其局限性，在某些条件下能最大化的发挥效能，缺少了某些条件则暴露出其缺陷。优劣局限层回答“做得怎么样”的问题。对技术优劣局限的把握，更有利于应用时总结最佳实践，是分析各种“坑”的基础。

<br/>


## 演进趋势

> 技术是在迭代改进和不断淘汰的。了解技术的前生后世，分清技术不变的本质，和变化的脉络，以及与其他技术的共生关系，能体现你对技术发展趋势的关注和思考。这层体现“未来如何”。

<br/>


### 拥抱异步渲染

react v16.0.0 引入了叫 Fiber 这个全新的架构。这个架构使得 React 用异步渲染成为可能，但要注意，这个改变只是让异步渲染（async rendering）成为“可能”，React 却并没有在 v16 发布的时候立刻开启这种“可能”，也就是说，React 在 v16 发布之后依然使用的是同步渲染。

不过，虽然异步渲染没有立刻采用，Fiber 架构还是打开了通向新世界的大门，React v16 一系列新功能几乎都是基于 Fiber 架构。

要面向 React 未来，我们首先要理解这个异步渲染的概念。

#### 同步渲染的问题

长期以来，React 一直用的是同步渲染，这样对 React 实现非常直观方便，但是会带来性能问题。

当要渲染的组件树非常庞大，JS的单线程遇到react的同步渲染，结果就是同步渲染霸占 JS 唯一的线程，其他的操作什么都做不了，在这 1 秒钟内，如果用户要点击什么按钮，或者在某个输入框里面按键，都不会看到立即的界面反应，这也就是俗话说的“卡顿”。

在同步渲染下，要解决“卡顿”的问题，只能是尽量缩小组件树的大小，以此缩短渲染时间，但是，应用的规模总是在增大的，不是说缩小就能缩小的，虽然我们利用定义 shouldComponentUpdate 的方法可以减少不必要的渲染，但是这也无法从根本上解决大量同步渲染带来的“卡顿”问题。

#### 异步渲染：两阶段渲染

React Fiber 引入了异步渲染，有了异步渲染之后，React 组件的渲染过程是分时间片的，不是一口气从头到尾把子组件全部渲染完，而是每个时间片渲染一点，然后每个时间片的间隔都可去看看有没有更紧急的任务（比如用户按键），如果有，就去处理紧急任务，如果没有那就继续照常渲染。

根据 React Fiber 的设计，一个组件的渲染被分为两个阶段：

第一个阶段（也叫做 render 阶段）是可以被 React 打断的，一旦被打断，这阶段所做的所有事情都被废弃，当 React 处理完紧急的事情回来，依然会重新渲染这个组件，这时候第一阶段的工作会重做一遍；

第二个阶段叫做 commit 阶段，一旦开始就不能中断，也就是说第二个阶段的工作会稳稳当当地做到这个组件的渲染结束。

两个阶段的分界点，就是 render 函数。render 函数之前的所有生命周期函数（包括 render)都属于第一阶段，之后的都属于第二阶段。

开启异步渲染，虽然我们获得了更好的感知性能，但是考虑到第一阶段的的生命周期函数可能会被重复调用，不得不对历史代码做一些调整。

在 React v16.3 之前，render 之前的生命周期函数（也就是第一阶段生命周期函数）包括这些：

- componentWillReceiveProps
- shouldComponentUpdate
- componentWillUpdate
- componentWillMount
- render

React 官方告诫开发者，虽然目前所有的代码都可以照常使用，但是未来版本中会废弃掉，为了将来，使用 React 的程序应该快点去掉这些在第一阶段生命函数中有副作用的功能。

一个典型的错误用例，也是我被问到做多的问题之一：为什么不在 componentWillMount 里去做AJAX？componentWillMount 可是比 componentDidMount 更早调用啊，更早调用意味着更早返回结果，那样性能不是更高吗？

首先，一个组件的 componentWillMount 比 componentDidMount 也早调用不了几微秒，性能没啥提高；而且，等到异步渲染开启的时候，componentWillMount 就可能被中途打断，中断之后渲染又要重做一遍，想一想，在 componentWillMount 中做 AJAX 调用，代码里看到只有调用一次，但是实际上可能调用 N 多次，这明显不合适。相反，若把 AJAX 放在 componentDidMount，因为 componentDidMount 在第二阶段，所以绝对不会多次重复调用，这才是 AJAX 合适的位置

#### getDerivedStateFromProps

到了 React v16.3，React 干脆引入了一个新的生命周期函数 getDerivedStateFromProps，这个生命周期函数是一个 static 函数，在里面根本不能通过 this 访问到当前组件，输入只能通过参数，对组件渲染的影响只能通过返回值。没错，getDerivedStateFromProps 应该是一个纯函数，React 就是通过要求这种纯函数，强制开发者们必须适应异步渲染。

```js
static getDerivedStateFromProps(nextProps, prevState) {
  //根据nextProps和prevState计算出预期的状态改变，返回结果会被送给setState
}
```

React v16发布时，还增加了异常处理的生命周期函数。

如果异常发生在第一阶段（render阶段），React就会调用`getDerivedStateFromError`，如果异常发生在第二阶段（commit阶段），React会调用`componentDidCatch`。这个区别也体现出两个阶段的区分对待。

#### 适应异步渲染的组件原则

当 React 开启异步渲染的时候，你的代码应该做到在 render 之前最多只能这些函数被调用：

- 构造函数
- getDerivedStateFromProps
- shouldComponentUpdate

幸存的这些第一阶段函数，除了构造函数，其余两个全都必须是纯函数，也就是不应该做任何有副作用的操作。

<br/>

### Suspense带来的异步操作革命

Suspense 应用的场合就是异步数据处理，最常见的例子，就是通过 AJAX 从服务器获取数据，每一个 React 开发者都曾为这个问题纠结。

如果用一句话概括 Suspense 的功用，那就是：用同步的代码来实现异步操作。

#### React 同步操作的不足

React 最初的设计，整个渲染过程都是同步的。同步的意思是，当一个组件开始渲染之后，就必须一口气渲染完，不能中断，对于特别庞大的组件树，这个渲染过程会很耗时，而且，这种同步处理，也会导致我们的代码比较麻烦。

当我们开始渲染某个组件的时候，假设这个组件需要从服务器获取数据，那么，要么由这个组件的父组件想办法拿到服务器的数据，然后通过 props 传递进来，要么就要靠这个组件自力更生来获取数据，但是，没有办法通过一次渲染完成这个过程，因为渲染过程是同步的，不可能让 React 等待这个组件调用 AJAX 获取数据之后再继续渲染。

常用的做法，需要组件的 render 和 componentDidMount 函数配合。

1. 在 componentDidMount 中使用 AJAX，在 AJAX 成功之后，通过 setState 修改自身状态，这会引发一次新的渲染过程。
2. 在 render 函数中，如果 state 中没有需要的数据，就什么都不渲染或者渲染一个“正在装载”之类提示；如果 state 中已经有需要的数据，就可以正常渲染了，但这也必定是在 componentDidMount 修改了 state 之后，也就是只有在第二次渲染过程中才可以。

下面是代码实例：

```js
class Foo extends React.Component {
  state = {
    data: null,
  };

  render () {
    if (!this.state.data) {
      return null;
    } else {
      return <div>this.state.data</div>;
    }
  }

  componentDidMount () {
    callAPI ().then (result => {
      this.setState ({data: result});
    });
  }
}
```

这种方式虽然可行，我们也照这种套路写过不少代码，但它的缺点也是很明显的。

- 组件必须要有自己的 state 和 componentDidMount 函数实现，也就不可能做成纯函数形式的组件。
- 需要两次渲染过程，第一次是 mount 引发的渲染，由 componentDidMount 触发 AJAX 然后修改 state，然后第二次渲染才真的渲染出内容。
- 代码啰嗦，十分啰嗦。

#### 理想中的代码形式

而 Suspense 就是为了克服上述 React 的缺点。

在了解 Suspense 怎么解决这些问题之前，我们不妨自己想象一下，如果要利用 AJAX 获取数据，代码怎样写最简洁高效？

我先来说一说自己设想的最佳代码形式。首先，我不想写一个有状态的组件，因为通过 AJAX 获取的数据往往也就在渲染用一次，没必要存在 state 里；其次，想要使数据拿来就用，不需要经过 componentDidMount 走一圈。所以，代码最好是下面这样：

```js
const Foo = () => {
  const data = callAPI ();
  return <div>{data}</div>;
};
```

够简洁吧，可是目前的 React 版本做不到啊！

因为 callAPI 肯定是一个异步操作，不可能获得同步数据，无法在同步的 React 渲染过程中立足。

不过，现在做不到，不代表将来做不到，将来 React 会支持这样的代码形式，这也就是 Suspense。

有了Suspense，我们可以这样写代码：

```js
const Foo = () => {
  const data = createFetcher (callAJAX).read ();
  return <div>{data}</div>;
};
```

接下来，我们就介绍一下 Suspense 的原理。

在 React 推出 v16 的时候，就增加了一个新生命周期函数 componentDidCatch。如果某个组件定义了 componentDidCatch，那么这个组件中所有的子组件在渲染过程中抛出异常时，这个 componentDidCatch 函数就会被调用。

可以这么设想，componentDidCatch 就是 JS 语法中的 catch，而对应的 try 覆盖所有的子组件，就像下面这样:

```js
try {
  //渲染子组件
} catch (error) {
  // componentDidCatch被调用
}
```

Suspense 就是巧妙利用 componentDidCatch 来实现同步形式的异步处理。

Suspense 提供的 createFetcher 函数会封装异步操作，当尝试从 createFetcher 返回的结果读取数据时，有两种可能：一种是数据已经就绪，那就直接返回结果；还有一种可能是异步操作还没有结束，数据没有就绪，这时候 createFetcher 会抛出一个“异常”。

你可能会说，抛出异常，渲染过程不就中断了吗？

的确会中断，不过，createFetcher 抛出的这个“异常”比较特殊，这个“异常”实际上是一个 Promise 对象，这个 Promise 对象代表的就是异步操作，操作结束时，也是数据准备好的时候。当 componentDidCatch 捕获这个 Promise 类型的“异常”时，就可以根据这个 Promise 对象的状态改变来重新渲染对应组件，第二次渲染，肯定就能够成功。

下面是 createFetcher 的一个简单实现方式：

```js
var NO_RESULT = {};

export const createFetcher = task => {
  let result = NO_RESULT;

  return () => {
    const p = task ();

    p.then (res => {
      result = res;
    });

    if (result === NO_RESULT) {
      throw p;
    }

    return result;
  };
};
```

在上面的代码中，createFetcher 的参数 task 被调用应该返回一个 Promise 对象，这个对象在第一次调用时会被 throw 出去，但是，只要这个对象完结，那么 result 就有实际的值，不会再被 throw。

还需要一个和 createFetcher 配合的 Suspense，代码如下：

```js
class Suspense extends React.Component {
  state = {
    pending: false,
  };

  componentDidCatch (error) {
    // easy way to detect Promise type
    if (typeof error.then === 'function') {
      this.setState ({pending: true});

      error.then (() =>
        this.setState ({
          pending: false,
        })
      );
    }
  }

  render () {
    return this.state.pending ? null : this.props.children;
  }
}
```

上面的 Suspense 组件实现了 componentDidCatch，如果捕获的 error 是 Promise 类型，那就说明子组件用 createFetcher 获取异步数据了，就会等到它完结之后重设 state，引发一次新的渲染过程，因为 createFetcher 中会记录异步返回的结果，新的渲染就不会抛出异常了。

使用 createFetcher 和 Suspense 的示例代码如下:

```js
const getName = () =>
  new Promise (resolve => {
    setTimeout (() => {
      resolve ('Morgan');
    }, 1000);
  });

const fetcher = createFetcher (getName);

const Greeting = () => {
  return <div>Hello {fetcher ()}</div>;
};

const SuspenseDemo = () => {
  return (
    <Suspense>
      <Greeting />
    </Suspense>
  );
};
```

上面的 getName 利用 setTimeout 模拟了异步 AJAX 获取数据，第一次渲染 Greeting 组件时，会有 Promise 类型的异常抛出，被 Suspense 捕获。1 秒钟之后，当 getName 返回实际结果的时候，Suspense 会引发重新渲染，这一次 Greeting 会显示出 hello Morgan。

上面的 createFetcher 和 Suspense 是一个非常简陋的实现，主要用来让读者了解 Suspense 的工作原理，正式发布的 Suspense 肯定会具备更强大的功能。

#### Suspense 带来的 React 使用模式改变

Suspense 被推出之后，可以极大地减少异步操作代码的复杂度。

之前，只要有 AJAX 这样的异步操作，就必须要用两次渲染来显示 AJAX 结果，这就需要用组件的 state 来存储 AJAX 的结果，用 state 又意味着要把组件实现为一个 class。总之，我们需要做这些：

- 实现一个 class；
- class 中需要有 state；
- 需要实现 componentDidMount 函数；
- render 必须要根据 this.state 来渲染不同内容。

有了 Suspense 之后，不需要做上面这些杂事，只要一个函数形式组件就足够了。

在介绍 Redux 时，我们提到过在 Suspense 面前，Redux 的一切异步操作方案都显得繁琐，读者现在应该能够通过代码理解这一点了。

很可惜，目前 Suspense 还不支持服务器端渲染，当 Suspense 支持服务器端渲染的时候，那就真的会对 React 社区带来革命性影响。

<br/>

### 函数化的 Hooks

Hooks 的目的，简而言之就是让开发者不需要再用 class 来实现组件。

#### useState

Hooks 会提供一个叫 useState 的方法，它开启了一扇新的定义 state 的门，对应 Counter 的代码可以这么写：

```js
import {useState} from 'react';

const Counter = () => {
  const [count, setCount] = useState (0);

  return (
    <div>
      <div>{count}</div>
      <button onClick={() => setCount (count + 1)}>+</button>
      <button onClick={() => setCount (count - 1)}>-</button>
    </div>
  );
};
```

注意看，Counter 拥有自己的“状态”，但它只是一个函数，不是 class。

useState 只接受一个参数，也就是 state 的初始值，它返回一个只有两个元素的数组，第一个元素就是 state 的值，第二个元素是更新 state 的函数。

这个例子中，我们可以利用 count 可以读取到这个 state，利用 setCount 可以更新这个 state。

因为 useState 在 Counter 这个函数体中，每次 Counter 被渲染的时候，这个 useState 调用都会被执行，useState 自己肯定不是一个纯函数，因为它要区分第一次调用（组件被 mount 时）和后续调用（重复渲染时），只有第一次才用得上参数的初始值，而后续的调用就返回“记住”的 state 值。

读者看到这里，心里可能会有这样的疑问：如果组件中多次使用 useState 怎么办？React 如何“记住”哪个状态对应哪个变量？

React 是完全根据 useState 的调用顺序来“记住”状态归属的，假设组件代码如下：

```js
const Counter = () => {
  const [count, setCount] = useState (0);
  const [foo, updateFoo] = useState ('foo');

  // ...
};
```

每一次 Counter 被渲染，都是第一次 useState 调用获得 count 和 setCount，第二次 useState 调用获得 foo 和 updateFoo。

React 不知道你把 useState 等 Hooks API 返回的结果赋值给什么变量，但是它也不需要知道，它只需要按照 useState 调用顺序记录就好了。

正因为这个原因，Hooks，千万不要在 if 语句或者 for 循环语句中使用！

像下面的代码，肯定会出乱子的：

```js
const Counter = () => {
  const [count, setCount] = useState (0);
  if (count % 2 === 0) {
    const [foo, updateFoo] = useState ('foo');
  }
  const [bar, updateBar] = useState ('bar');
};
```

因为条件判断，让每次渲染中 useState 的调用次序不一致了，于是 React 就错乱了。

#### useEffect

除了 useState，React 还提供 useEffect，用于支持组件中增加副作用的支持。

在 React 组件生命周期中如果要做有副作用的操作，代码放在哪里？

当然是放在 componentDidMount 或者 componentDidUpdate 里，但是这意味着组件必须是一个 class。

在 Counter 组件，如果我们想要在用户点击“+”或者“-”按钮之后把计数值体现在网页标题上，这就是一个修改 DOM 的副作用操作，所以必须把 Counter 写成 class，而且添加下面的代码：

```js
componentDidMount () {
    document.title = `Count: ${this.state.count}`;
  }

  componentDidUpdate () {
    document.title = `Count: ${this.state.count}`;
  }
```

而有了 useEffect，我们就不用写一个 class 了，对应代码如下：

```js
import {useState, useEffect} from 'react';

const Counter = () => {
  const [count, setCount] = useState (0);

  useEffect (() => {
    document.title = `Count: ${count}`;
  });

  return (
    <div>
      <div>{count}</div>
      <button onClick={() => setCount (count + 1)}>+</button>
      <button onClick={() => setCount (count - 1)}>-</button>
    </div>
  );
};
```

useEffect 的参数是一个函数，组件每次渲染之后，都会调用这个函数参数，这样就达到了 componentDidMount 和 componentDidUpdate 一样的效果。

虽然本质上，依然是 componentDidMount 和 componentDidUpdate 两个生命周期被调用，但是现在我们关心的不是 mount 或者 update 过程，而是“after render”事件，useEffect 就是告诉组件在“渲染完”之后做点什么事。

读者可能会问，现在把 componentDidMount 和 componentDidUpdate 混在了一起，那假如某个场景下我只在 mount 时做事但 update 不做事，用 useEffect 不就不行了吗？

其实，用一点小技巧就可以解决。useEffect 还支持第二个可选参数，只有同一 useEffect 的两次调用第二个参数不同时，第一个函数参数才会被调用，所以，如果想模拟 componentDidMount，只需要这样写：

```js
useEffect(() => {
  // 这里只有mount时才被调用，相当于componentDidMount
}, [123]);
```

在上面的代码中，useEffect 的第二个参数是 [123]，其实也可以是任何一个常数，因为它永远不变，所以 useEffect 只在 mount 时调用第一个函数参数一次，达到了 componentDidMount 一样的效果。

#### useContext

Context API的设计不完美，在多个 Context 嵌套的时候尤其麻烦。

比如，一段 JSX 如果既依赖于 ThemeContext 又依赖于 LanguageContext，那么按照 React Context API 应该这么写：

```js
<ThemeContext.Consumer>
  {theme => (
    <LanguageContext.Cosumer>
      language => {
        //可以使用theme和lanugage了
      }
    </LanguageContext.Cosumer>
  )}
</ThemeContext.Consumer>;

```

因为 Context API 要用 render props，所以用两个 Context 就要用两次 render props，也就用了两个函数嵌套，这样的缩格看起来也的确过分了一点点。

使用 Hooks 的 useContext，上面的代码可以缩略为下面这样：

```js
const theme = useContext(ThemeContext);
const language = useContext(LanguageContext);
// 这里就可以用theme和language了
```

这个useContext把一个需要很费劲才能理解的 Context API 使用大大简化，不需要理解render props，直接一个函数调用就搞定。

但是，useContext也并不是完美的，它会造成意想不到的重新渲染，我们看一个完整的使用useContext的组件。

```js
const ThemedPage = () => {
  const theme = useContext (ThemeContext);

  return (
    <div>
      <Header color={theme.color} />
      <Content color={theme.color} />
      <Footer color={theme.color} />
    </div>
  );
};
```

因为这个组件ThemedPage使用了useContext，它很自然成为了Context的一个消费者，所以，只要Context的值发生了变化，ThemedPage就会被重新渲染，这很自然，因为不重新渲染也就没办法重新获得theme值，但现在有一个大问题，对于ThemedPage来说，实际上只依赖于theme中的color属性，如果只是theme中的size发生了变化但是color属性没有变化，ThemedPage依然会被重新渲染，当然，我们通过给Header、Content和Footer这些组件添加shouldComponentUpdate实现可以减少没有必要的重新渲染，但是上一层的ThemedPage中的JSX重新渲染是躲不过去了。

说到底，useContext需要一种表达方式告诉React：“我没有改变，重用上次内容好了。”

希望Hooks正式发布的时候能够弥补这一缺陷。

#### Hooks 带来的代码模式改变

Hooks 将大大简化使用 React 的代码。

我们可能不再需要 class了,只用函数形式来编写组件。

对于 useContext，它并没有为消除 class 做贡献，却为消除 render props 模式做了贡献

对了，所有的 Hooks API 都只能在函数类型组件中调用，class 类型的组件不能用，从这点看，很显然，class 类型组件将会走向消亡。

# 相关资料

- [React.js 小书](http://huziketang.mangojuice.top/books/react/)
- [Ant Design 实战教程](https://www.yuque.com/ant-design/course)
- [对React children 的深入理解](https://www.jianshu.com/p/d1975493b5ea)