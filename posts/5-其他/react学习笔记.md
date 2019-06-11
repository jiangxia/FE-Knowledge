# 前言
react 是数据驱动的框架，也是目前前端最火的框架之一，学习react，我们照旧从应用维度跟设计维度进行学习。

<br/>

# 应用维度

<br/>

## 问题

> 从技术的应用维度看，首先考虑的是要解决什么问题，这是技术产生的原因。问题这层，用来回答“干什么用”。

<br/>

react 的诞生其实是要解决两个问题。UI细节问题问题 和 数据模型的问题。

传统UI操作关注太多细节，jQuery虽然可以给我们提供了便捷的API，以及良好的浏览器兼容，但开发人员还是要手动去操作DOM，关注太多细节，不仅降低了开发效率，还容易引入BUG。

react以数据为中心，数据驱动视图，而不直接操作dom，也就是只负责描述界面应该显示成什么样子，而不关心实现细节。

在react之前，前端管理数据的模型是MVC架构。传统的MVC架构难以扩展和维护，当应用程序出现问题，很难知道是model还是view出现问题。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/96.jpg' width='600'>
<br/>

facebook 推出react的同时，也推出了flux架构。flux架构的最大特点就是单向数据流，前端应用状态管理变得可预测、可追溯。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/97.jpg' width='600'>
<br/>

## 技术规范

> 技术被研发出来，人们怎么用它才能解决问题呢？这就要看技术规范，可以理解为技术使用说明书。技术规范，回答“怎么用”的问题，反映你对该技术使用方法的理解深度。

<br/>


### react组件

React 组件基本上由 3 个部分组成——属性(props)、状态(state)以及生命周期方法。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/160.png' width='600'>
<br/>

官方在 React 组件构建上提供了 3 种不同的方法：React.createClass、ES6 classes 和无状态函数(stateless function)。

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

1. 决定 Virtual DOM 是否要重绘
2. 一般可以由 PureComponent 自动实现
3. 典型场景：性能优化

#### componentWillReceiveProps
注意下update阶段，触发组件update有两种情况，props或者state的修改。

可以看到，这两种情况生命周期函数是有重合的。唯一的不同就是props改变时，会先调用 componentWillReceiveProps

1. 一个组件要从父组件接受参数
2. 如果这个组件第一次存在于父组件中，不会执行
3. 如果这个组件之前已经存在于父组件中，才会执行

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

JSX 的本质  不是模板引擎，而是动态创建组件的语法糖，它允许我们在JavaScript代码中直接写HTML标记。最终生成的代码就是React.CreateElement

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

在 React 0.13 版本之前，React 官方提供 React.addons.classSet 插件来给组件动态设置 className，这在后续版本中被移除(为了精简 API )。我们可以使用 classnames 库来操作类。

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

#### CSS问题及CSS模块
react开发中的CSS问题：全局污染、命名混乱、依赖管理不彻底、无法共享变量、代码压缩不彻底。这些问题只凭CSS自身是无法解决的，必须用JS来管理CSS。

- 全局污染:CSS 使用全局选择器机制来设置样式，优点是方便重写样式。缺点是所有的 样式都是全局生效，样式可能被错误覆盖，因此产生了非常丑陋的 !important，甚至 inline !important 和复杂的选择器权重计数表1 ，提高犯错概率和使用成本。Web Components 标准中的 Shadow DOM 能彻底解决这个问题，但它把样式彻底局部化，造成 外部无法重写样式，损失了灵活性。
- 命名混乱:由于全局污染的问题，多人协同开发时为了避免样式冲突，选择器越来越复杂，容易形成不同的命名风格，很难统一。样式变多后，命名将更加混乱。
- 依赖管理不彻底:组件应该相互独立，引入一个组件时，应该只引入它所需要的 CSS 样 式。现在的做法是除了要引入 JavaScript，还要再引入它的 CSS，而且 Saas/Less 很难实现 对每个组件都编译出单独的 CSS，引入所有模块的 CSS 又造成浪费。JavaScript 的模块化 已经非常成熟，如果能让 JavaScript 来管理 CSS 依赖是很好的解决办法，而 webpack 的 css-loader 提供了这种能力。
- 无法共享变量:复杂组件要使用 JavaScript 和 CSS 来共同处理样式，就会造成有些变量 在 JavaScript 和 CSS 中冗余，而预编译语言不能提供跨 JavaScript 和 CSS 共享变量的这种 能力。
- 代码压缩不彻底:由于移动端网络的不确定性，现代工程项目对 CSS 压缩的要求已经到 了变态的程度。很多压缩工具为了节省一个字节,会把 16px 转成 1pc，但是这对非常长的 类名却无能为力。

<br/>

CSS 模块化要解决两个问题：CSS 样式的导入与导出。灵活按需导入以便复用 代码，导出时要能够隐藏内部作用域，以免造成全局污染。

CSS 模块化解决方案有两种：Inline Style、CSS Modules。

- Inline Style。这种方案彻底抛弃 CSS，使用 JavaScript 或 JSON 来写样式，能给 CSS 提供 JavaScript 同样强大的模块化能力。但缺点同样明显，Inline Style 几乎不能利用 CSS 本身 的特性，比如级联、媒体查询(media query)等，:hover 和 :active 等伪类处理起来比较 复杂。另外，这种方案需要依赖框架实现，其中与 React 相关的有 Radium、jsxstyle 和 react-style。
- CSS Modules。依旧使用 CSS，但使用 JavaScript 来管理样式依赖。CSS Modules 能最大 化地结合现有 CSS 生态和 JavaScript 模块化能力，其 API 非常简洁，学习成本几乎为零。 发布时依旧编译出单独的 JavaScript 和 CSS 文件。现在，webpack css-loader 内置 CSS Modules 功能。

<br/>

#### CSS Modules的优点

- 所有样式都是局部化的，解决了命名冲突和全局污染问题;
- class 名的生成规则配置灵活，可以以此来压缩 class 名;
- 只需引用组件的 JavaScript，就能搞定组件所有的 JavaScript 和 CSS;
- 依然是 CSS，学习成本几乎为零。

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

##### 实现 CSS 与 JavaScript 变量共享

:export 关键字可以把 CSS 中的变量输出到 JavaScript 中

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

### 组件间通信

通信种类：父组件向子组件通信、子组件向父组件通信和没有嵌套关系的组件之间通信。

- 父组件向子组件通信：props
- 子组件向父组件通信
    + 利用回调函数
    + 利用自定义事件机制
- 跨级组件通信：context
- 没有嵌套关系的组件通信：自定义事件机制


<br/>

## 最佳实践
> 最佳实践回答“怎么能用好”的问题，反映你实践经验的丰富程度。

<br/>

### 无状态组件

一个组件只有render函数时，可以定义为无状态组件，无状态组件就是一个函数，相比普通组件性能更高，因为他没有其他声明周期的方法。UI组件一般都可以定义为无状态组件。


### 高阶组件（HOC）

高阶组件、mixin和函数子组件都是设计模式。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/100.jpg' width='800'>
<br/>

高阶函数：这种函数接受函数作为输入，或是输出一个函数。

高阶组件：类似于高阶函数，它接受 React 组件作为输入，输出一 个新的 React 组件。

实现高阶组件的方法有：

#### 属性代理

定义：高阶组件通过被包裹的 React 组件来操作 props。

<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/162.jpg' width='500'>

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
const MyContainer = WrappedComponent => {
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
}
```
我们把 input 组件中对 name prop 的 onChange 方法提取到高阶组件中，这样就有效地抽象了同样的 state 操作。可以这么来使用它

```js
import React, {Component} from 'React';

@MyContainer class MyComponent extends Component {
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

在这个例子中，WrappedComponent 的渲染结果中，顶层的 input 组件的 value 被改写为 may the force be with you。因此，我们可以做各种各样的事，甚至可以反转元素树，或是改变元素 树中的 props。

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

### 函数子组件

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/101.jpg' width='800'>
<br/>


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

### react性能优化

问题：浏览器重绘，重排是影响性能的第一要素

解决：React render 会更新虚拟DOM，虚拟DOM会去渲染真实DOM，尽可能减少render的次数是关键所在

优化原则：减少渲染
- 纯函数
    - 相同的输入总是有相同的输出
    - 过程没有副作用，不改变外部状态
    - 没有额外的状态依赖，方法内部的状态只在方法生命周期内存活
- React组件与纯函数的关系
    - React组件本身就是纯函数，传入相同的props和state总是得到相同的virtualDom
    - 从而引申出PureRender
- shouldComponentUpdate
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


redux的相关知识繁多，还包含了Mobx、dva，为此我将他抽离出来，请看[这里](https://github.com/jiangxia/FE-Knowledge/blob/master/posts/5-其他/数据管理学习笔记.md)。

<br/>


### render的执行

1. 当组件的state和props发生改变时，render函数就会重新执行
2. 父组件render函数被执行时，它的子组件的render函数都将被重新运行一次

<br/>


### setState

setState 通过一个队列机制实现 state 更新。当执行 setState 时，会将需要更新的 state 合并 后放入状态队列，而不会立刻更新 this.state，队列机制可以高效地批量更新 state。如果不通过 setState 而直接修改 this.state 的值，那么该 state 将不会被放入状态队列中，当下次调用 setState 并对状态队列进行合并时，将会忽略之前直接被修改的 state，而造成无法预知的错误。因此，应该使用 setState 方法来更新 state，同时 React 也正是利用状态队列机制实现了setState 的异步更新，避免频繁地重复更新 state。

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

### React数据流
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