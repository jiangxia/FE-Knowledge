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

**数据模型的问题**

在react之前，前端管理数据的模型是MVC架构。传统的MVC架构难以扩展和维护，当应用程序出现问题，很难知道是model还是view出现问题。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/96.jpg' width='600'>
<br/>

react采用的是单向数据流，可以很好的避免类似的问题。

<br/>

> 笔者认为：学习框架，关键是要关注框架本身解决了什么问题，以及如何解决，这些才是框架最核心的部分，如果胡子眉毛一把抓，很容易就迷失在知识的海洋中。
> 
> react解决的问题就两个，其中UI细节问题，react的解决方案是数据驱动、JSX、事件系统、组件化等等，而数据模型问题，react的解决方案是单向数据流。
>
> 学习react的过程中，要时刻把这两个问题放在心中，善于联系，这样知识才能学得扎实。

<!-- facebook 推出react的同时，也推出了flux架构。flux架构的最大特点就是单向数据流，前端应用状态管理变得可预测、可追溯。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/97.jpg' width='600'>
<br/> -->

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

> 笔者注：
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

React 组件基本上由 3 个部分组成——属性(props)、状态(state)以及生命周期方法。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/160.png' width='600'>
<br/>

官方在 React 组件构建上提供了 3 种不同的方法：React.createClass、ES6 classes 和无状态函数。

**创建组件的一般步骤：**

1. 创建静态 UI
2. 考虑组件的状态组成：状态（state） 及 状态的改变（effect、reducer）
3. 考虑组件的交互方式：状态的触发（dispatch）

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

按照这样“内容”->“样式”->“动态功能”的方式渐进增强，是非常正确的思想。但是，长期以来，实现方式存在问题，问题就是 HTML、CSS 和 JS 被分开管理了。

如果你在 React 诞生之前从事过网页开发，肯定有这样的体会。为了修改一个功能，需要牵扯到 HTML、CSS 和 JS 的修改，但是这三部分分别属于不同的文件，明明是一个功能，你却要去修改至少三个文件。

在软件开发中，同一个功能相关的代码最好放在一个地方，这就是高内聚性。把网页功能分在 HTML、CSS 和 JS 中，明显背离了高内聚性的原则，但是我们也忍受了这个做法这么多年，直到 React 出现。

在 React 中，当你要修改一个功能的内容和行为时，在一个文件中就能完成，这样就达到了高内聚的要求。

我们在JS中写类似HTML标记的语法，就符合高内聚的要求。

要做到彻底的高内聚，react还要考虑如何处理CSS。

主要有这几种方式：

**style 属性**

```js
const clockStyle = {
  'font-family': 'monospace'
};

const MajorClock = ({milliseconds=0}) => {
  return <h1 style={clockStyle}>{ms2Time(milliseconds)}</h1>
}
```

**导入 CSS 文件**

类似：

```js
import "./ControlButtons.css";
```

**组件式的样式**

对比使用 style 属性和导入 CSS 两种方法，可以看出各有优缺点。

使用 style 属性，好处是可以将样式应用到每个元素，互相不干扰；缺点就是非常不简洁，如果你想要定制一个元素的样式，必须给这个元素加 style 属性。

相反，用 CSS 表达复杂的样式规则很容易，但CSS 定义的样式是全局的，这样很容易失控。

为了解决不同模块之间 CSS 互相干扰的问题，我们需要组件化的样式。

上面说过，在 React 的世界中，一切都是组件。那么，组件化的样式，也是非常符合react的思想。

我们可以使用styled-jsx来达到这样的效果。关于更多的样式处理细节，请看[这里](#样式处理)

组件设计的内容远不止这些。社区有非常多的最佳实践，请看[组件设计模式](组件设计模式)

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


## 最佳实践
> 最佳实践回答“怎么能用好”的问题，反映你实践经验的丰富程度。

<br/>

### 组件设计模式

#### 聪明组件和傻瓜组件

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

#### 提供者模式

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

路由的基本原理：保证 View 和 URL 同步。

在 React 中，组件就是一个方法。 props 作为方法的参数，当它们发生变化时会触发方法执行，进而帮助我们重新绘制 View。在 React Router 中，我们同样可以把 Router 组件看成一个方法，location 作为参数，返回的结果同 样是 View。

路由切换方式：hashChange （hashHistory） 或是history.pushState（browserHistory）

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/167.jpg' width='600'>
<br/>


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

### 无状态组件

一个组件只有render函数时，可以定义为无状态组件，无状态组件就是一个函数，相比普通组件性能更高，因为他没有其他声明周期的方法。UI组件一般都可以定义为无状态组件。

<br/>


### mixin

React 在使用 createClass 构建组件时提供了 mixin 属性。mixin有两个作用：

- 共享工具方法。
- 生命周期继承，props 与 state 合并。

ES6 Classes 不支持 mixin。

mixin 的问题:

- 破坏了原有组件的封装：mixin 方法会混入方法，给原有组件带来新的特性，但它也可能带来了新的 state 和 props，这意味着组件有一 些“不可见”的状态需要我们去维护，但我们在使用的时候并不清楚。另外，mixin 也有可能去依赖其他的 mixin，这样会建立一个 mixin 的依赖链，当我们改动其 中一个 mixin 的状态时，很可能会直接影响其他的 mixin。
- 命名冲突：尽管我们可以通过更改名字来解决，但遇到第三方引用，或已经引用了几个 mixin 的情况下， 总是要花一定的成本去解决冲突。
- 增加复杂性

<br/>

### 高阶组件与mixin的比较

高阶组件与 mixin 的不同之处

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/163.png' width='600'>
<br/>

高阶组件符合函数式编程思想。对于原组件来说，并不会感知到高阶组件的存在，只需要把功能套在它之上就可 以了，从而避免了使用 mixin 时产生的副作用。

<br/>

### react性能优化

问题：浏览器重绘，重排是影响性能的第一要素

解决：React render 会更新虚拟DOM，虚拟DOM会去渲染真实DOM，尽可能减少render的次数是关键所在

优化原则：减少渲染

纯函数
- 相同的输入总是有相同的输出
- 过程没有副作用，不改变外部状态
- 没有额外的状态依赖，方法内部的状态只在方法生命周期内存活

React组件与纯函数的关系
- React组件本身就是纯函数，传入相同的props和state总是得到相同的virtualDom
- 从而引申出PureRender

shouldComponentUpdate
- PureRender
    - 重新实现shouldComponentUpdate方法，对props和state作浅比较
    - 少为组件绑定箭头函数
    - 不直接设置props为数组或者对象
- 使用redux connect函数优化
    - 实现了shouldComponentUpdate函数的实现,会进行浅层比较​
    - 父组件尽量不传无意义的参数,特别是箭头函数,不然会导致子组件无意义render，浪费性能

**如何检测react性能**

在Chrome中监测react性能：在URL后加?react_perf，比如：localhost:3000/?react_perf

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
- 使用airbnb的JS代码风格

Prettier
- 代码格式化的神器
- 保证更容易写出风格一致的代码

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

## 实现原理

> 为了达到设计目标，该技术采用了什么原理和机制。实现原理层回答“怎么做到”的问题。把实现原理弄懂，并且讲清楚，是技术人员的基本功。

<br/>

### 生命周期函数

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


### setState

setState 通过一个队列机制实现 state 更新。

当执行 setState 时，会将需要更新的 state 合并 后放入状态队列，而不会立刻更新 this.state。

队列机制可以高效地批量更新 state。

如果不通过 setState 而直接修改 this.state 的值，那么该 state 将不会被放入状态队列中，当下次调用 setState 并对状态队列进行合并时，将会忽略之前直接被修改的 state，而造成无法预知的错误。

因此，应该使用 setState 方法来更新 state，同时 React 也正是利用状态队列机制实现了setState 的异步更新，避免频繁地重复更新 state。

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

### React数据流
在 React 中，数据是自顶向下单向流动的，即从父组件到子组件。这条原则让组件之间的关系变得简单且可预测。

把组件看成一个函数，那么它接受了 props 作为参数，内部由 state 作为函数的内部参数，返回一个 VDOM 的实现。

#### state

setState 是一个异步方法，一个生命周期内所有的 setState 方法会合并操 作。 

#### props

- React 的单向数据流，主要的流动管 道就是 props。props 本身是不可变的。当我们试图改变 props 的原始值时，React 会报出类型错 误的警告 
- props 可以配置默认值，使用defaultProps设置。
- 子组件 prop ： children （ React.Children 是 React 官方提供的一系列操作children 的方法。它提供诸如 map、 forEach、count 等实用函数 ）
- 组件 props ： 对于子组件而言，我们不仅可以直接使用 this.props.children 定义，也可以将子组件以 props 的形式传递。 
- propTypes  ： 规范 props 的类型与必需的状态 

<br/>


## 优劣局限

> 每种技术实现，都有其局限性，在某些条件下能最大化的发挥效能，缺少了某些条件则暴露出其缺陷。优劣局限层回答“做得怎么样”的问题。对技术优劣局限的把握，更有利于应用时总结最佳实践，是分析各种“坑”的基础。

<br/>


## 演进趋势

> 技术是在迭代改进和不断淘汰的。了解技术的前生后世，分清技术不变的本质，和变化的脉络，以及与其他技术的共生关系，能体现你对技术发展趋势的关注和思考。这层体现“未来如何”。

<br/>


### react16新特性

1. 新的核心算法Fiber
2. Render 可以返回数据、字符串
3. 错误处理机制

新版本带来的优化和新功能：

1. Portals 组件
2. 更好更快的服务端渲染
3. 体积更小，MIT协议

异步渲染

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




