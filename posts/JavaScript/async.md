
# 新特性：async/await

Promise是JavaScript中的一个定义，但是实际编写代码时，我们可以发现，它似乎并不比回调的方式书写更简单，但是从ES6开始，我们有了async/await，这个语法改进跟Promise配合，能够有效地改善代码结构。

async/await是ES2016新加入的特性，它提供了用for、if等代码结构来编写异步的方式。它的运行时基础是Promise，面对这种比较新的特性，我们先来看一下基本用法。

async函数必定返回Promise，我们把所有返回Promise的函数都可以认为是异步函数。

async函数是一种特殊语法，特征是在function关键字之前加上async关键字，这样，就定义了一个async函数，我们可以在其中使用await来等待一个Promise。

```js
function sleep (duration) {
  return new Promise (function (resolve, reject) {
    setTimeout (resolve, duration);
  });
}
async function foo () {
  console.log ('a');
  await sleep (2000);
  console.log ('b');
}
```

这段代码利用了我们之前定义的sleep函数。在异步函数foo中，我们调用sleep。

async函数强大之处在于，它是可以嵌套的。我们在定义了一批原子操作的情况下，可以利用async函数组合出新的async函数。

```js
function sleep (duration) {
  return new Promise (function (resolve, reject) {
    setTimeout (resolve, duration);
  });
}
async function foo (name) {
  await sleep (2000);
  console.log (name);
}
async function foo2 () {
  await foo ('a');
  await foo ('b');
}
```

这里foo2用await调用了两次异步函数foo，可以看到，如果我们把sleep这样的异步操作放入某一个框架或者库中，使用者几乎不需要了解Promise的概念即可进行异步编程了。

此外，generator/iterator也常常被跟异步一起来讲，我们必须说明 generator/iterator 并非异步代码，只是在缺少async/await的时候，一些框架（最著名的要数co）使用这样的特性来模拟async/await。

但是generator并非被设计成实现异步，所以有了async/await之后，generator/iterator来模拟异步的方法应该被废弃。

最后，来看个例子：

```js
let a = 0
let b = async () => {
  a = a + await 10
  console.log('2', a) 
}
b()
a++
console.log('1', a) 

// -> '1' 1
// -> '2' 10
```

对于以上代码你可能会有疑惑，让我来解释下原因：

1. 首先函数 b 先执行，在执行到 await 10 之前变量 a 还是 0，因为 await 内部实现了 generator ，generator 会保留堆栈中东西，所以这时候 a = 0 被保存了下来
2. 因为 await 是异步操作，后面的表达式不返回 Promise 的话，就会包装成 Promise.reslove(返回值)，然后会去执行函数外的同步代码，也就是执行了 console.log('1', a) ，输出 '1' 1 
3. 同步代码执行完毕后开始执行异步代码，将保存下来的值拿出来使用，这时候 a = 0 + 10

上述解释中提到了 await 内部实现了 generator，其实 await 就是 generator 加上 Promise的语法糖，且内部实现了自动执行 generator。

<br/>
