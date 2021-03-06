
# 前言
webpack 是当下最好用的前端模块打包工具，前端开发人员日常都要跟脚手架打交道，而手脚架就是基于webpack构建的，深入理解webpack，对我们日常工作意义重大。

本文将系统讲解webpack，老规矩，从应用维度跟设计维度展开，由于作者能力有限，有些部分暂时整理不出来，如果你有所补充，欢迎push~

<br/>

# 应用维度
<br/>

## 问题

> 从技术的应用维度看，首先考虑的是要解决什么问题，这是技术产生的原因。问题这层，用来回答“干什么用”。

<br/>

随着前端的演变，网页已经相当于一个功能丰富的应用，前端面临诸多挑战：

1. 首先，前端代码越来越复杂，就需要模块化开发，模块化开发带来的问题就是代码如何组织，如何处理依赖关系？
2. 前端社区日益繁荣，日常开发已经离不开第三方依赖，如何管理好第三方依赖，也成为一个问题。
3. 浏览器对ES6的兼容还不够友好，这也是前端需要解决的问题
4. 上线时我们需要对代码进行打包，这样可以有效减少http请求，从而提高性能
5. 我们要打包的文件，不仅包含JS，还可能包含CSS、image等。

由于前端界存在种种问题，webpack应运而生。

webpack官方定义就是一个模块打包工具。webpack不仅支持 ES module 的语法，也支持 CommonJS 的语法。

webpack 不仅可以打包JS，也可以打包其他格式的文件， 比如css、image等。

<br/>

## 技术规范
> 技术被研发出来，人们怎么用它才能解决问题呢？这就要看技术规范，可以理解为技术使用说明书。技术规范，回答“怎么用”的问题，反映你对该技术使用方法的理解深度。

<br/>

这里要重点讲解webpack的配置。

### 模式
webpack 配置文件需要指定 mode，默认是production，打包后的文件会被压缩。可以指定成 development。不设置mode，会有警告

```js
module.exports = {
  // ……
  mode: 'production',
}
```

<br/>

### Entry 与 Output
entry 支持配置多项，每一项的key是文件名，当entry配置多个入口文件时，output的filename不能写死，不然会报错，可以写成 `filename: [name].js`。

output 还可以配置publicPath，从而设置导出JS文件的前缀，通过这个配置，可以设置CDN地址。

```js
module.exports = {
  entry: {
    main: './src/index.js',
    sub: './src/index.js'
  },
  output: {
    filename: '[name].js', // 设置成 index.js 会报错
    chunkFilename: '[name].chunk.js',
    publicPath: 'http://cdn.com',
    path: path.resolve(__dirname, '../dist')
  }
}
```

<br/>

### Loader
loader就是打包方案。

比如，打包jpg图片时，可以使用 file-loader 进行打包，也可以使用url-loader，url-loader包含了 file-loader 所有的功能，而且，他默认会将图片转成base64格式。如果不希望转成base64位，可以设置 limit，这样的话，当图片大于设置值的时候，就不会转成base64。

```js
// webpack.config.js
module.exports = {
  module: {
    rules: [{
      test: /\.(jpg|png|gif)$/,
      use: {
        loader: 'url-loader',
        options: {
          name: '[name]_[hash].[ext]',
          outputPath: 'images/',
          limit: 10240
        }
      }
    }]
  }
}
```

又比如，打包css文件时，需要同时引入两个loader：css-loader跟style-loader。css-loader会分析css文件的引用关系，最后把css文件合并成一段css。而style-loader的作用是把这段css放到head下的style标签下。

如果是scss文件，还需要引入 scss-loader。如果需要css自动添加浏览器产商前缀，则需要引入postcss-loader。

由于css中还可以引用其他的css，为了避免出错，需要在css-loader 中设置importLoaders。

为了防止css全局污染，我们需要引入css modules的概念，也就是css模块化。同样需要在css-loader 中设置 modules 为true。引入时可以使用类似的方式： `import style from './index.css'`

如果css中引用了字体文件，还需要对 字体文件的格式设置loader，使用 file-loader 即可。

```js
module.exports = {
  module: {
    rules: [{
      test: /\.scss$/,
      use: [
        'style-loader',
        {
          loader: 'css-loader',
          options: {
            importLoaders: 2
          }
        },
        'sass-loader',
        'postcss-loader'
      ]
    }, {
      test: /\.css$/,
      use: [
        'style-loader',
        {
          loader: 'css-loader',
          options: {
            modules: true
          }
        },
        'postcss-loader'
      ]
    }, {
      test: /\.(eot|ttf|svg)$/,
      use: {
        loader: 'file-loader'
      }
    }]
  },
}
```

```js
// postcss.config.js
module.exports = {
  plugins: [
    require('autoprefixer')
  ]
}
```

> 如果有多个loader时，会从后往前执行。

<br/>

### plugins
使用plugins让打包更便捷。

plugin 很像生命周期函数，可以在webpack 运行到某一个时刻，帮你处理一些事情。

htmlWebpackPlugin 会在打包结束后，自动生成一个HTML文件，并把打包生成的JS自动引入到HTML中。

cleanWebpackPlugin 会在打包之前，删除某一个文件夹（比如dist文件夹）

```js
module.exports = {
  // ……
  plugins: [
    new HtmlWebpackPlugin({
      template: 'src/index.html'
    }),
    new CleanWebpackPlugin(['dist'], {
      root: path.resolve(__dirname, '../')
    })
  ]
}
```

<br/>

### sourceMap
sourceMap 是一个映射关系，当我们打包的文件报错时，它能提示我们是源文件的出错位置，而不是打包后文件的出错位置，这样就利于调试。

使用方式，就是在 webpack 中配置 `devtool: 'source-map'`

development 环境，推荐使用 `devtool: 'cheap-module-eval-source-map'`
production 环境，推荐使用 `devtool: 'cheap-module-source-map'`

```js
module.exports = {
  // ……
  mode: 'development',
  devtool: 'cheap-module-eval-source-map',
}
```

<br/>

### webpackDevServer

每次修改代码都要重新打包，这是非常繁琐的，我们可以修改npm scripts成`webpack --watch`。

但如果我们想实现更酷炫的效果，比如自动打开浏览器、自动刷新浏览器等，这个操作就做不到。此时，可以借助webpackDevServer 来实现。

webpack支持 devServer , 可以帮我们启动了一个服务器。我们在日常开发中，经常需要发ajax请求，这大大提高了我们的开发效率。此外，devServer打包后的文件，其实保存在内存中，这样打包的速度更快。

之前 devServer 还不够完善，所以很多脚手架工具会自己实现一个devServer，现在webpack的devServer已经非常完善了。

更多请参考[官网](https://www.webpackjs.com/configuration/dev-server/#devserver-proxy)

```js
module.exports = {
  devServer: {
    contentBase: './dist', // 服务器的根目录
    open: true, // 自动打开浏览器
    port: 8080,
    hot: true,
    proxy: { // 设置代理，访问/api，直接转发到3000端口
      "/api": "http://localhost:3000"
    }
  },
}
```

我们也可以手写一个 devServer，新建server.js，增加 npm scripts : `node server.js`。

```js
const express = require('express);
const webpack = require('webpack');
const webpackDevMiddleware = require('webpack-dev-middleware');
const config = require('./webpack.config.js');
const complier = webpack(config)

const app = express(); // 启动一个http服务器
app.use(webpackDevMiddleware(complier, {}))

app.listen(3000, ()=>{
  console.log("server is running");  
})
```

通过这个例子，也可以看到webpack有两种使用方式，一种是在命令行中使用，一种是在node中直接使用webpack。

在命令行使用webpack，可以参考官网[资料](https://www.webpackjs.com/api/cli/)

在node中使用webpack，可以参考官网[资料](https://www.webpackjs.com/api/node/)

<br/>



### hot mudule replacement 热更新
我们每一次修改代码，devServer都会帮我们刷新页面，但我们只希望显示修改的内容，而不刷新页面，此时就要用到热更新。

更多请参考官网[资料1](https://www.webpackjs.com/guides/hot-module-replacement/)、[资料2](https://www.webpackjs.com/api/hot-module-replacement/)

```js
const webpack = require('webpack');

module.exports = {
  devServer: {
    contentBase: './dist',
    open: true,
    port: 8080,
    hot: true,
    hotOnly: true, // 可选，即便hot功能不生效，浏览器也不刷新
  },
  plugins: [
    new webpack.HotModuleReplacementPlugin()
  ],
}
```

<br/>

### Babel
有些浏览器还不支持ES6的语法，此时就需要用babel转义，将ES6语法转成ES5。

babel提供了详细的使用指南，在[官网setup页面](https://babeljs.io/setup#installation)选择webpack选项就可以看到。

----

babel的使用分为三步：

1. Installation
```
npm install --save-dev babel-loader @babel/core
```

> babel-loader @babel/core 是 babel 跟 webpack 之间的桥梁

2. Usage
```js
module: {
  rules: [
    { test: /\.js$/, exclude: /node_modules/, loader: "babel-loader" }
  ]
}
```

3. Create .babelrc configuration file
新建 .babelrc 并按照 env preset

```
npm install @babel/preset-env --save-dev
```

```js
// .babelrc
{
  "presets": ["@babel/preset-env"]
}
```

> @babel/preset-env 将ES6的语法转义成ES5语法，比如let转成var
>
> @babel/polyfill 为低级浏览器注入了ES6的对象或方法，比如promise
> 
> 引入 @babel/polyfill 会让我们的文件变得非常大，可以配置 useBuiltIns 做到按需加载

babel 内容非常多，建议直接看官网。

----

```js
module.exports = {
  // ……
  module: {
    rules: [{
      test: /\.js$/,
      exclude: /node_modules/,
      loader: 'babel-loader',
      options: {
        presets: [["@babel/preset-env", {
          targets: {
            chrome: '67',  // 告诉 babel 目标浏览器，babel可以根据目标浏览器决定是否做转化，这样就可以减少最终输出文件的大小
          },
          useBuiltIns: 'usage  // 提高性能：用到的才引用
        }]]
      }
      // use: [{
      //   loader: 'babel-loader'
      // }, {
      //   loader: 'imports-loader?this=>window'
      // }]
    }]
  },
}
```

babel-loader 中 options 的内容会非常多，可以把 options 的内容放到 .babelrc 中




<br/>

### tree shaking
我们引入一个模块，只会引入该模块中的部分方法，tree shaking会帮我们把不需要的方法过滤掉，这样打包后的文件将显著变小。

tree shaking 只支持 ES Module 的引用方式。

development 模式下，默认是不支持 tree shaking，我们需要配置 optimization 的 usedExports 为true。

我们还需要给 package.json 增加一项配置 `"sideEffects": ["@babel/polyfill", "*.css"]`,这样打包时 tree shaking 对 @babel/polyfill就不会有作用。这是因为我们引用@babel/polyfill时，是`import @babel/polyfill`，tree shaking 会认为 @babel/polyfill 不需要引用任何东西，从而把它忽略掉。同理，我们可以使用 `import "index.css"`，我们同样不希望tree shaking生效，我们可以在sideEffects中增加 *.css 的配置。

如果设置`"sideEffects": false`，表示对所有模块都做 tree shaking。

development 模式下，为了调试方便，虽然设置了 tree shaking，但打包出来的文件一样包含没有引用的模块。当我们上线时，会设置 mode 为 production，此时 tree shaking 就会把不需要模块的代码过滤掉。


```js
module.exports = {
  // ……
  mode: 'development',
  optimization: {
    usedExports: true,
  },
}
```

<br/>

### development 和 production 模式的区分打包
由于 development 和 production 模式下的配置是不一样的，我们可以抽离出公共的 webpack.common.js，以及Dev下的 webpack.dev.js 和 production下的webpack.prod.js。最后使用 webpack.merge 合并。

```js
const merge = require('webpack-merge');
const commonConfig = require('./webpack.common.js');

const devConfig = {
  // ……
}

module.exports = merge(commonConfig, devConfig);
```

<br/>

### splitChunksPlugin
webpack代码分割底层使用了 splitChunksPlugin 插件。官网资料[地址](https://www.webpackjs.com/plugins/split-chunks-plugin/)。

```js
module.exports = {
  splitChunks: {
    chunks: "async", // 可选：all。async 只代码分割异步代码，all同时支持同步跟异步的方式
    minSize: 30000, // 小于 30KB 不做代码分割，大于 30KB，还要根据cacheGroups的规则决定是否做代码分割
    maxSize: 20000, // 大于 20KB 尝试做代码分割，但由于基础库是不允许分割的，所以一般不生效
    minChunks: 1,  // 引用超过1次，会做代码分割。
    maxAsyncRequests: 5, // 遇到的前5个库，会做代码分割，超过5个的不做代码分割
    maxInitialRequests: 3, // 入口文件最多只能做三次代码分割
    automaticNameDelimiter: '~', // 文件连接符
    name: true, // 为true时，cacheGroups的filename才会生效
    cacheGroups: { // 缓存组，满足以上要求的文件，会根据缓存组中的要求，加入缓存组，最终打包成文件。这样的好处是可以把多个库，输出成一个文件。此外，如果配置了上面的参数却没有代码分割，很可能就是缓存组的配置不满足
      vendors: {
        test: /[\\/]node_modules[\\/]/, // node_modules目录下的文件会被匹配
        priority: -10, // 优先级，值越大优先级越大
        // filename: 'vendors.js'
      },
      default: {
        minChunks: 2,
        priority: -20,
        reuseExistingChunk: true  // 如果一个模块已经被打包了，则再打包时会忽略该模块
      }
    }
  },
}
```

小技巧：splitChunks 如果不配置，默认值就是上面的这些选项。简便写法是：


```js
module.exports = {
  // …… 
  splitChunks: {
    chunks: "all", // 我们要对同步跟异步代码都做代码分割，所以改成all
  },
}
```

我们也可以为css进行代码分割，使用到的插件是[MiniCssExtractPlugin](https://webpack.js.org/plugins/mini-css-extract-plugin)，只需要用MiniCssExtractPlugin提供的loader 代替 style-loader 即可，具体内容看官网。

<br/>

## 最佳实践

> 最佳实践回答“怎么能用好”的问题，反映你实践经验的丰富程度。

<br/>

### webpack的安装
webpack 不建议全局安装，因为每个项目依赖的webpack版本可能不同，全局安装可能导致项目依赖的webpack版本不对而无法运行，建议局部安装，也就是 `npm i webpack webpack-cli -D`。

局部安装完webpack后，如果要查看webpack的版本，执行 `webpack -v`是得不到预期的结果，因为webpack并没全局安装，此时要执行 `npx webpack -v`，npx是npm提供的命令，它会在我们当前目录下的node_modules文件下寻找安装过的依赖。

如果我们是在package.json文件中配置 npm scripts，则不需要npx这个指令，因为 npm scripts 默认会在当前目录下的 node_modules 寻找依赖。

安装webpack时，可以指定webpack的版本号，如果不清楚webpack有什么版本，可以使用`npm info webpack`查看

> webpack-cli 允许我们在命令里使用webpack这个命令。
<br/>

### webpack与 code splitting
如果把所有的代码都打包到一个文件里，会带来两个问题：

1. 文件过于庞大
2. 基础库基本上不会改变，而业务代码却经常改变，一旦业务代码更改了，整个文件要重新加载，会极大的损耗性能。

code splitting 是代码分割，没有webpack我们也可以手动做代码分割，从而提升性能。webpack能帮我们自动完成代码分割。
 
webpack 中实现代码分割有两种方式：
1. 同步代码，我们可以在 optimization 中设置splitChunks。
2. 异步代码（import），无需任何配置，会自动进行代码分割。

```js
module.exports = {
  // ……
  optimization: {
    splitChunks: {
      chunks: 'all',
    }
  },
}
```


<br/>

### 打包分析
我们可以使用webpack提供的[analyse工具](https://github.com/webpack/analyse)进行打包分析.

我们在打包时，需要增加命令`webpack --profile --json > stats.json`，也就是 `webpack --profile --json > stats.json --config ./build/webpack.dev.js`

打包完的文件中，就会出现stats.json的文件。

我们打开[链接](http://webpack.github.com/analyse)，上次stats.json，就会出现打包的分析报告。

webpack官方提供的分析工具，除了analyse，还有[这些](https://www.webpackjs.com/guides/code-splitting/#bundle-%E5%88%86%E6%9E%90-bundle-analysis-)：

1. [webpack-chart](https://alexkuz.github.io/webpack-chart/): webpack 数据交互饼图。
2. [webpack-visualizer](https://chrisbateman.github.io/webpack-visualizer/): 可视化并分析你的 bundle，检查哪些模块占用空间，哪些可能是重复使用的。
3. [webpack-bundle-analyzer](https://github.com/webpack-contrib/webpack-bundle-analyzer): 一款分析 bundle 内容的插件及 CLI 工具，以便捷的、交互式、可缩放的树状图形式展现给用户。

<br/>

### Prefetching/Preloading 
webpack 建议我们写异步加载代码，也就是异步import。当代码执行时，才会去加载相应的代码，这样首屏的代码利用率就可以提高。类似：

```js
document.addEventListener('click', () => {
  import('./click.js').then(({ default: func }) => {
    func()
  })
})
```

我们可以用Chrome的coverage工具看代码的利用率。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/82.gif' width='800'>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/83.gif' width='800'>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/84.gif' width='800'>
<br/>

但我们不一定要等到用户操作时，才去加载相应的代码，而是在网络空闲时就去加载。我们可以在webpack中进行配置。具体做法如下：

```js
// 关注下魔法注释，js的新特性
document.addEventListener('click', () => {
  import(/* webpackPrefetch: true */ './click.js').then(({ default: func }) => {
    func()
  })
})
```
Prefetching/Preloading 是有区别的：

1. Prefetching会等待核心代码加载完，网络空闲时才去加载
2. Preloading是跟主要的代码一块加载的

所以Prefetching会更合适。


<br/>

### webpack 与 浏览器缓存
我们打包的文件，浏览器是会缓存的，当我们修改了内容，用户刷新页面，此时加载的还是缓存中的文件。为了解决这个问题，我们需要修改production模式下的配置文件。

```js
const commonConfig = require('./webpack.common.js');

const prodConfig = {
  mode: 'production',
  devtool: 'cheap-module-source-map',
  output: {
    filename: '[name].[contenthash].js',
    chunkFilename: '[name].[contenthash].js'
  },
  optimization: {
    runtimeChunk: {
      name: 'runtime'  // 旧版本必须配置此项，否则即便文件内容没有发生改变，hash值也会改变
    },
  }
}

module.exports = merge(commonConfig, prodConfig);
```

contenthash 会根据文件内容生成hash值，当我们文件内容改变时，contenthash就会改变，从而通知浏览器重新向服务器请求文件。

之所以在旧版webpack下，文件代码没变，生成文件的hash值也会改变的原因是：

我们业务逻辑的代码打包到main.js里，依赖库的代码打包到vendors.js里，但main.js跟vendors.js是有依赖关系的，这些依赖关系的代码会保存在manifest文件里。manifest文件既存在于main.js，也存在vendors.js里。而在旧版webpack每次打包manifest可能会有差异，这个差异导致vendors.js的hash值也会改变。设置runtimeChunk后，manifest相关的代码会被抽离出来，放到runtime文件里去，这样就能解决这个问题。

<br/>

### Shimming 垫片
jQuery时代，我们需要先引入jQuery，再引入其他依赖jQuery的类库，比如jQuery.ui.js。这在webpack中就有问题。比如这样：

```js
// a.js
import $ from 'jquery'
import 'jquery.ui'
```

这样引用，jquery.ui.js会报错：找不到$。之所以这样，是因为webpack是模块化，$只能在a.js里引用，jquery.ui.js是引用不到$的，而jquery.ui.js是第三方库，我们又不能去修改jquery.ui.js的代码，怎么办呢？

我们可以添加ProvidePlugin插件。在ProvidePlugin里我们设置了$，当JS文件中用到$，在当前又没引用$时，这个配置就会生效，告诉JS文件$指向jquery。

关于ProvidePlugin，可以到官网看[资料](https://webpack.js.org/plugins/provide-plugin)

```js
const webpack = require('webpack');
module.exports = {
  plugins: [
    new webpack.ProvidePlugin({
      $: 'jquery',
      _join: ['lodash', 'join']
    }),
  ],
  performance: false, // 额外补充：设置为false，打包时不会警告性能方面的问题
}
```

关于垫片机制，还有其他用法。比如我们在一个模块中全局打印this，发现this指向的是模块本身，而不是window对象，如果想要让this指向window，可以这样：

```js
module.exports = {
  module: {
    rules: [{
      test: /\.js$/,
      exclude: /node_modules/,
      use: [{
        loader: 'babel-loader'
      }, {
        loader: 'imports-loader?this=>window'
      }]
    }]
  },
}
```

我们需要安装imports-loader，设置this指向window。

关于shimming，可以看官网[资料](https://webpack.js.org/guides/shimming)

<br/>

### library 的打包
我们写的库，要支持多种方式的引用，诸如：

```js
// library.js
export function math (){
  console.log(1);
}
```

```js
import library from './library' // ES module
const library = require('library'); // commonjs
require(['library'], function(){}) // AMD
```

我们可以配置libraryTarget：

```js
module.exports = {
  mode: 'production',
  entry: {
    main: './src/index.js'
  },
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].js',
    libraryTarget: 'umd' // umd 是通用的意思。配置了umd，就可以支持不同的引用方式
  }
}
```

如果你还想通过script标签引用，比如`<script src="./library.js"></script>`，那还需要配置

```js
module.exports = {
  mode: 'production',
  entry: {
    main: './src/index.js'
  },
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].js',
    library: 'library', // 打包好的代码，挂载到页面library这个全局变量上
    libraryTarget: 'umd' // umd 是通用的意思。配置了umd，就可以支持不同的引用方式
  }
}
```

打包后到浏览器控制台输入library，就会打印出全局变量


<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/85.jpg' width='800'>
<br/>

这里要重点讲下 library 跟 libraryTarget 的关系。library的含义是要生成一个全局变量， libraryTarget 的含义是这个全局变量挂载到哪里。如果libraryTarget设置为umd，则两者关系不大。如果我们把libraryTarget 设置成this，则打包出来的文件不支持ES module、commonjs等的引用，他表示全局变量挂载到全局的this上。此时我们在浏览器控制台，输入`this.library`，就可以找到该全局变量。libraryTarget 还设置成 window、global。

此外，我们在打包时，还会出现一种情况：

```js
// library.js
import _ from lodash;
// 其他代码
```

```js
// a.js
import _ from lodash;
import library from './library';
```

这就造成lodash被打包了两次，我们希望library.js打包时，不要把lodash打包进去，可以这样配置：

```js
module.exports = {
  externals: ['lodash] // 打包时，遇到lodash，自动忽略
}
```

<br/>

### PWA
我们把生成的文件放到线上，用户就可以访问，如果服务器挂了，页面就会显示异常。这种时候，我们希望即便服务器挂了，用户还是可以看到之前访问的页面，而这就是PWA。

要做到PWA很简单，首先配置webpack。

```js
const WorkboxWebpackPlugin = require('workbox-webpack-plugin');
module.exports = {
  plugins: [
    new WorkboxWebpackPlugin.GenerateSW({
      clientsClaim: true,
      skipWaiting: true
    }),
  ]
}
```

然后在业务代码中，使用 serviceWorker。

```js
if('serviceWorker' in navigator) {
  window.addEventListener('load', () => {
    navigator.serviceWorker.register('/service-worker.js')
      .then(registration => {
        console.log('service-worker register')
      }).catch(error => {
        console.log('service-worker register error')
      })
  })
}
```


<br/>

### 请求转发
我们在开发时，经常会遇到跨域的问题，devServer 可以帮助我们实现请求转发，具体看官网[资料](https://www.webpackjs.com/configuration/dev-server/#devserver-proxy)

我们只需要在webpack进行如下配置：

```js
module.exports = {
  devServer: {
    proxy: {
      '/react/api': {
        target: 'https://baidu.com/',
        secure: false, // false 时才可以对https请求的转发
        pathRewrite: {
          'header.json': 'demo.json'
        }
      }
    }
  },
}
```

devServer 中的proxy允许我们做请求转发。当我们请求'/react/api'就会被转发到`http://baidu.com/`的域名下。此外，我们在日常开发中，可能需要用到header.json这个API时，该API还没开发完，我们需要先访问demo.json进行开发，此时就可以设置pathRewrite达到效果。

webpack的proxy内容非常多，底层使用的是http-proxy-middleware，可以上GitHub看相应的[资料](https://github.com/chimurai/http-proxy-middleware#options)

<br/>

### 单页面路由问题
我们在写react应用时，需要用到react-router-dom实现路由，但是我们会发现，当我们访问/list时，预期是要访问到/list路由，但浏览器会发送请求到/list，从而页面显示出错。

要解决这个问题，就要用到devServer的historyApiFallback这个API了。

当我们在devServer里配置`historyApiFallback:true`后，我们不管访问什么url，都会执行根目录（也就是/）下的代码，从而解决了单页路由的问题。

更多内容，看[官网](https://www.webpackjs.com/configuration/dev-server/#devserver-historyapifallback)

<br/>

### eslint
eslint 跟 webpack关系不大，很多编辑器是可以支持eslint插件，但可能我们为了调试方便，希望eslint的错误显示在浏览器上，这样即便我们编辑器没有eslint插件，也可以看到问题。

操作起来也很简单，我们先在自己的工程里安装eslint跟eslint-loader.

```js
module.exports = {
  devServer: {
    overlay: true  // 必须配置
  },
  rules: [
    {
      test: /\.js$/,
      exclude: /node_modules/,
      use: ["babel-loader", "eslint-loader"],  // 使用 eslint-loader 
    },
  ]
}
```

关于eslint-loader，可以看官网[资料](https://webpack.js.org/loaders/eslint-loader)

<br/>

### webpack性能优化
1. 跟上技术迭代（Node yarn npm ）
2. 在尽可能少的模块上应用loader
3. plugin 尽可能精简并确保可靠
4. 合理配置resolve。
5. 使用 DllPlugin 提高打包速度（5.10、5.11）
6. 控制包文件大小
7. 合理使用sourceMap
8. 结合 stats 分析打包结果
9. 开发环境内存编译（devServer打包文件存于内存，能提高速度）

<br/>

**跟上技术迭代**

webpack运行于node，node版本更新，自然会提高webpack的打包效率，npm跟yarn等包管理工具也是同理。

<br/>

**在尽可能少的模块上应用loader**：

为loader配置exclude，例如： `exclude: /node_moudles/`
为loader配置include，例如：`include: path.resolve(__dirname, '../src')`

<br/>

**plugin 尽可能精简并确保可靠**

比如开发环境下，不需要对代码进行压缩，这样就不需要在webpack.dev.js里引入相关的plugin

<br/>

**合理配置resolve**

当我们没有写js后缀时，webpack默认会帮我们补上，如果我们的jsx文件也不希望写上后缀，希望webpack会帮我们默认补上，可以设置resolve。

<br/>

```js
module.exports = {
  resolve: {
    extensions: ['.js', '.jsx'],
    mainFiles: ['index', 'child'] // 当我们引用的是某个路径，webpack默认会帮我们读取index文件，如果我们设置了['index', 'child']，webpack会逐一帮我们查找index.js index.jsx child.js child.jsx
  }
}
```
<br/>

## 市场应用趋势
> 随着技术生态的发展，和应用问题的变迁，技术的应用场景和流行趋势会受到影响。这层回答“谁用，用在哪”的问题，反映你对技术应用领域的认识宽度。

<br/>

# 设计维度

<br/>

## 目标
> 为了解决用户的问题，技术本身要达成什么目标。这层定义“做到什么”。

<br/>

webpack就是个模块打包工具，我们需要使用webpack打包不限于JS、CSS、image等文件。

不同的文件，打包策略是不同的，所以我们需要配置loader。

打包过程中，我们可能还需要做一些额外的操作，所以我们需要配置 plugin。

所以学习webpack的重点，就是理解与掌握loader跟plugin。

webpack 默认会读取 webpack.config.js文件，我们也可以更改默认的文件名`npx webpack --config webpack.xxx.js`

注：webpack开发团队为了提高开发体验，一直在丰富webpack的默认配置，所以我们虽然没有指定JS的打包策略，但一样可以打包成功。

<br/>

## 实现原理
> 为了达到设计目标，该技术采用了什么原理和机制。实现原理层回答“怎么做到”的问题。把实现原理弄懂，并且讲清楚，是技术人员的基本功。

<br/>

## 优劣局限
> 每种技术实现，都有其局限性，在某些条件下能最大化的发挥效能，缺少了某些条件则暴露出其缺陷。优劣局限层回答“做得怎么样”的问题。对技术优劣局限的把握，更有利于应用时总结最佳实践，是分析各种“坑”的基础。
<br/>


## 演进趋势
> 技术是在迭代改进和不断淘汰的。了解技术的前生后世，分清技术不变的本质，和变化的脉络，以及与其他技术的共生关系，能体现你对技术发展趋势的关注和思考。这层体现“未来如何”。