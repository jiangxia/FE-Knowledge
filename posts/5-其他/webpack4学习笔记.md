
# 前言

# 应用维度

<br/>

## 问题
随着前端越来越复杂，网页其实可以看做是功能丰富的应用，它们拥有着复杂的JavaScript代码和一大堆依赖包。

由于浏览器对ES module的支持还不完善，所以就诞生了webpack，webpack官方定义就是一个模块打包工具。webpack不仅支持 ES module 的语法，也支持 CommonJS 的语法。

webpack 不仅可以打包JS，也可以打包其他格式的文件， 比如css、image等。
<br/>

## 技术规范


<br/>

## 最佳实践
webpack 不建议全局安装，因为每个项目依赖的webpack版本可能不同，全局安装可能导致项目依赖的webpack版本不对而无法运行，建议局部安装，也就是 `npm i webpack webpack-cli -D`。

局部安装完webpack后，如果要查看webpack的版本，执行 `webpack -v`是得不到预期的结果，因为webpack并没全局安装，此时要执行 `npx webpack -v`，npx是npm提供的命令，它会在我们当前目录下的node_modules文件下寻找安装过的依赖。

如果我们是在package.json文件中配置 npm scripts，则不需要npx这个指令，因为 npm scripts 默认会在当前目录下的 node_modules 寻找依赖。

安装webpack时，可以指定webpack的版本号，如果不清楚webpack有什么版本，可以使用`npm info webpack`查看

> webpack-cli 允许我们在命令里使用webpack这个命令。
<br/>

## 市场应用趋势


<br/>

# 设计维度

## 目标
webpack 打包时，不同类型的文件，打包策略是不同的。如果打包的是图片，只需要拿到图片的路径即可。

webpack没那么智能，无法自动识别文件的类型，所以就需要我们告诉它怎么打包。

所以我们需要对webpack进行配置。

webpack 默认会读取 webpack.config.js文件，我们也可以更改默认的文件名`npx webpack --config webpack.xxx.js`

注：webpack开发团队为了提高开发体验，一直在丰富webpack的默认配置，所以我们虽然没有指定JS的打包策略，但一样可以打包成功。

<br/>

## 实现原理
这里要重点讲解webpack的配置。


### 模式
webpack 配置文件需要指定 mode，默认是production，打包后的文件会被压缩。可以指定成 development。不设置mode，会有警告

<br/>

### Entry 与 Output
entry 支持数组，数组的key是文件名，当entry配置多个入口文件时，output的filename不能写死，不然会报错，可以写成 `filename: [name].js`。

output 还可以配置导出JS文件的前缀，通过 publicPath，通过这个配置，可以设置CDN地址。

<br/>

### Loader
loader就是打包方案。

比如，打包jpg图片时，可以使用 file-loader 进行打包，也可以使用url-loader，url-loader包含了 file-loader 所有的功能，而且，他默认会将图片转成base64格式。如果不希望转成base64位，可以设置 limit，这样的话，当图片大于设置值的时候，就不会转成base64。

又比如，打包css文件时，需要同时引入两个loader：css-loader跟style-loader。css-loader会分析css文件的引用关系，最后把css文件合并成一段css。而style-loader的作用是把这段css放到head下的style标签下。

如果是scss文件，还需要引入 scss-loader。如果需要css自动添加浏览器产商前缀，则需要引入postcss-loader。

由于css中还可以引用其他的css，为了避免出错，需要在css-loader 中设置importLoaders。

为了防止css全局污染，我们需要引入css modules的概念，也就是css模块化。同样需要在css-loader 中设置 modules 为true。引入时可以使用类似的方式： `import style from './index.css'`

如果css中引用了字体文件，还需要对 字体文件的格式设置loader，使用 file-loader 即可。

> 如果有多个loader时，会从后往前执行。

<br/>

### plugins
使用plugins让打包更便捷。

plugin 很像生命周期函数，可以在webpack 运行到某一个时刻，帮你处理一些事情。

htmlWebpackPlugin 会在打包结束后，自动生成一个HTML文件，并把打包生成的JS自动引入到HTML中。

cleanWebpackPlugin 会在打包之前，删除某一个文件夹（比如dist文件夹）

<br/>

### sourceMap
sourceMap 是一个映射关系，当我们打包的文件报错时，它能提示我们是源文件的出错位置，而不是打包后文件的出错位置，这样就利于调试。

使用方式，就是在 webpack 中配置 `devtool: 'source-map'`

development 环境，推荐使用 `devtool: 'cheap-module-eval-source-map'`
production 环境，推荐使用 `devtool: 'cheap-module-source-map'`




<br/>


## 优劣局限

<br/>


## 演进趋势