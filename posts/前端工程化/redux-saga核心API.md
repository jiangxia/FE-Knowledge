# 前言

redux-saga是管理redux异步操作的中间件，redux-saga通过创建sagas将所有异步操作逻辑收集在一个地方集中处理。

sagas采用Generator函数来yield Effects。Generator函数可以暂停执行，再次执行的时候，从上次暂停的地方继续执行。常见的effect有：fork，call，take，put，cancel

由于使用了generator函数，redux-saga让你可以用同步的方式来写异步代码。

redux-saga启动的任务可以在任何时候通过手动来取消，也可以把任务和其他的Effects放到race方法里以自动取消。

<br/>

# sagas的分类

sagas 有3种类型，分别是：

## root saga

立即启动的所有sagas的唯一入口

```js
const sagaMiddleware = createSagaMiddleware();
const middlewares = [sagaMiddleware];

const store = createStore(appReducer, applyMiddleware(...middlewares));
sagaMiddleware.run(rootSaga);
```

## watcher saga

监听被dispatch的actions，当接收到action或者知道其被触发时，调用worker saga执行任务

## worker saga

执行具体的逻辑处理，如进行异步请求，处理返回结果等

<br/>

# redux-saga的执行流程

整个流程：

- ui组件触发action创建函数
- action创建函数返回一个action
- action被传入redux中间件(被 saga等中间件处理) ，产生新的action，传入reducer
- reducer把数据传给ui组件显示
- mapStateToProps
- ui组件显示

<br/>

# 常见effect的用法

1. call 异步阻塞调用
2. fork 异步非阻塞调用，无阻塞的执行fn，执行fn时，不会暂停Generator
3. put 相当于dispatch，分发一个action
4. select 相当于getState，用于获取store中相应部分的state
5. take 监听action，暂停Generator，匹配的action被发起时，恢复执行。take结合fork，可以实现takeEvery和takeLatest的效果
6. takeEvery 监听action，每监听到一个action，就执行一次操作。可以被 take 跟 fork这个组合替换
7. takeLatest 监听action，监听到多个action，只执行最近的一次
8. cancel 指示 middleware 取消之前的 fork 任务，cancel 是一个无阻塞 Effect。也就是说，Generator 将在取消异常被抛出后立即恢复
9. race 竞速执行多个任务
10. throttle 节流

