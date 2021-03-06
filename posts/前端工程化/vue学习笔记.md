# 前言
学习vue，我们照旧从应用维度跟设计维度进行学习。

<br/>

# 应用维度

<br/>

## 问题

> 从技术的应用维度看，首先考虑的是要解决什么问题，这是技术产生的原因。问题这层，用来回答“干什么用”。

<br/>

vue 的诞生其实是要解决两个问题。**UI细节问题问题** 和 **数据模型的问题**。

<br/>

## 技术规范

> 技术被研发出来，人们怎么用它才能解决问题呢？这就要看技术规范，可以理解为技术使用说明书。技术规范，回答“怎么用”的问题，反映你对该技术使用方法的理解深度。

<br/>

### vue属性

- 自定义属性 props ：组件props中声明的属性
- 原生属性 ： 没有声明的属性，默认自动挂载到组件根元素上，设置inheritAttrs 为false可以关闭自动挂载
- 特殊属性 class、style ：挂载到组件根元素上，支持字符串、对象、数组等多种语法

### 事件

- 普通事件：@click、@import、@change、@xxx等事件，通过 this.$emit('xxx', ...) 触发
- 修饰符事件：@input.trim、@click.stop、@submit.prevent等，一般用于原生HTML元素，自定义组件需要自行开发支持

### 插槽

- 普通插槽
- 作用域插槽

### 计算属性 与 监听器

计算属性：可以写计算逻辑的属性，通常用于数据缓存，数据没有变化，不会重复计算。计算属性依赖的数据，必须是响应式数据

监听器 watch ： 更加灵活通用，可以执行任何逻辑，如函数节流、ajax异步获取数据，甚至操作DOM

两者的区别：computed 能做的，watch都能做，反之则不行。能用computed的尽量使用computed。

<br/>


### 函数式组件

特点：无状态、无实例、没有this上下文、无生命周期
设置 `functional: true` 就可以声明函数式组件


### 生命周期

一、创建阶段
beforeCreate => created => beforeMount => render => mounted

二、更新阶段
beforeUpdate => render => updated

三、销毁阶段
beforeDestroy => destroyed

### 指令

#### 内置指令
```
v-text
v-html
v-show
v-if
v-else
v-else-if
v-for
v-on
v-bind
v-model
v-slot
v-pre
v-cloak
v-once
```

#### 自定义指令

```
bind  
inserted  
update  
componentuUpdate  
unbind
```

### 组件实例

```html
<!-- vm.$refs.p可以获取组件实例 -->
<p ref="p">hello</p>
<!-- vm.$refs.child可以获取组件实例 -->
<child-component ref="child"></child-component>
```

### 数组对响应式更新的支持情况

支持：push pop shift unshift splice sort reverse

不支持：filter concat slice

原理是使用 Object.definedProperty 对数组方法进行改写

-----------------

### 单向数据流

vue是单向数据流，不是双向绑定。
vue的双向绑定不过是语法糖
Object.definedProperty 是用来做响应式更新的，和双向绑定没关系。


### 组件通信

provide / inject

## 最佳实践

> 最佳实践回答“怎么能用好”的问题，反映你实践经验的丰富程度。

### vuex

State —— `this.$store.state.xxx` 取值 —— 提供一个响应式数据

Getter —— `this.$store.getters.xxx` 取值 —— 借助vue的计算属性computed来实现缓存

Mutation —— `this.$store.commit("xxx")` 赋值 —— 更新state的方法

Action —— `this.$store.dispatch("xxx")` 赋值 —— 触发 mutation的方法

Module —— `Vue.set` 动态添加state 到响应式数据中

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

### 响应式更新

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/182.png' width='800'>
<br/>

vue 实例化时，会对数据进行代理，不管是取数据，还是设置数据，都会对数据进行代理。

对于render需要的数据，才会把数据加入 watcher，下次数据有更新时，才会通知 watcher，并且通知组件的更新。


## 优劣局限

> 每种技术实现，都有其局限性，在某些条件下能最大化的发挥效能，缺少了某些条件则暴露出其缺陷。优劣局限层回答“做得怎么样”的问题。对技术优劣局限的把握，更有利于应用时总结最佳实践，是分析各种“坑”的基础。

<br/>


## 演进趋势

> 技术是在迭代改进和不断淘汰的。了解技术的前生后世，分清技术不变的本质，和变化的脉络，以及与其他技术的共生关系，能体现你对技术发展趋势的关注和思考。这层体现“未来如何”。

<br/>

# 相关资料
