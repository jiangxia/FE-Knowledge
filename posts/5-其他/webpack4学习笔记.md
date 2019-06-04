
# webpack

## 应用维度

<br/>

### 问题
随着前端越来越复杂，网页其实可以看做是功能丰富的应用，它们拥有着复杂的JavaScript代码和一大堆依赖包。

由于浏览器对ES module的支持还不完善，所以就诞生了webpack，webpack官方定义就是一个模块打包工具。webpack不仅支持 ES module 的语法，也支持 CommonJS 的语法。

webpack 不仅可以打包JS，也可以打包其他格式的文件， 比如css、image等。
<br/>

### 技术规范


<br/>

### 最佳实践
webpack 不建议全局安装，因为每个项目依赖的webpack版本可能不同，全局安装可能导致项目依赖的webpack版本不对而无法运行，建议局部安装，也就是 `npm i webpack webpack-cli -D`。

局部安装完webpack后，如果要查看webpack的版本，执行 `webpack -v`是得不到预期的结果，因为webpack并没全局安装，此时要执行 `npx webpack -v`，npx是npm提供的命令，它会在我们当前目录下的node_modules文件下寻找安装过的依赖。

如果我们是在package.json文件中配置 npm scripts，则不需要npx这个指令，因为 npm scripts 默认会在当前目录下的 node_modules 寻找依赖。

安装webpack时，可以指定webpack的版本号，如果不清楚webpack有什么版本，可以使用`npm info webpack`查看

> webpack-cli 允许我们在命令里使用webpack这个命令。
<br/>

### 市场应用趋势


<br/>

## 设计维度

### 目标
webpack 打包时，不同类型的文件，打包策略是不同的。如果打包的是图片，只需要拿到图片的路径即可。

webpack没那么智能，无法自动识别文件的类型，所以就需要我们告诉它怎么打包。

所以我们需要对webpack进行配置。

webpack 默认会读取 webpack.config.js文件，我们也可以更改默认的文件名`npx webpack --config webpack.xxx.js`

注：webpack开发团队为了提高开发体验，一直在丰富webpack的默认配置，所以我们虽然没有指定JS的打包策略，但一样可以打包成功。

<br/>

### 实现原理
这里要重点讲解webpack的配置。


<br/>

**模式**
<br/>
webpack 配置文件需要指定 mode，默认是production，打包后的文件会被压缩。可以指定成 development。不设置mode，会有警告


<br/>

**Loader**
<br/>


<br/>


### 优劣局限

<br/>


### 演进趋势