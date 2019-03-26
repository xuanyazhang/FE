# Webpack基础

### 使用指南

   1 安装

   ```
   npm install --save-dev webpack
   npm install --save-dev webpack-cli //webpack 4+版本必须安装此依赖

   ``` 

   2 运行

   package.json的 script脚本中通过webpack/webpack-dev-server运行

   ```
   "script": {
       "dev": "webpack --config webpack.config.js"
   }

   ```

   3 webpack.config.js 配置（大多数情况下输出配置对象）

   1）webpack.config.js 运行在node环境中，所以遵循的是CommonJS规范，通过require和module.exports 进行模块的引入和输出

   2） 入口JS文件,可以使用ES6, 通过import和export 进行模块的引入和输出

   ```
    // 注意区分module.exports = {} 和 export default {}
   module.exports = {
      mode: "production" || "development", //
      entry: String|Array<String>|Object|Function,  // 切记路径相对于根路径
      output: {
          path: path.resolve(__dirname, "../dist"), // __dirname是当前文档目录
          filename: "[name].[hash].js",             // 版本控制
          publicPath: "https://gray.umetrip.com/assets/"  //打包完成后，html文件中资源路径为 https://gray.umetrip.com/assets/**.**.js
      },
      devtool: ""  //
      resolve: {

      },
      module: {
          rules: [
              配置各种loader
          ]
      },
      externals: string|array|object|function|regex, // 不打包外部依赖，详情见下方具体介绍
      target: "node" || "web" || "webworker"// 常用的选项,
      devServer: {
          配置开发server
      },
      // 一定注意这是个数组
      plugins:[
         配置各种插件
      ]
   }

   ```
   3）externals配置详解

     externals 配置选项提供了「从输出的 bundle 中排除依赖」的方法

     3.1）externals 配置本地工程，仅仅为了打包速度加快，减少包的大小，通过CDN方式<script>引入, 首次加载比较慢，后面加载都是缓存不影响性能

     ```
   externals: {
     jquery: "jQuery",   // key 代表本地代码使用时需要的名称 import * from jquery|lodash
     lodash: "_"         // value 代表 <script> 引入的js暴露的全局变量(可以通过源码看)
   },

     ```

     3.2）externals 与 library,libraryTarget配合开发开源库配置

     ```
   externals: {
     "lodash": {
        commonjs: "lodash",//如果我们的库运行在Node.js环境中，import _ from 'lodash'等价于const _ = require('lodash')
        commonjs2: "lodash",//同上
        amd: "lodash",//如果我们的库使用require.js等加载,等价于 define(["lodash"], factory);
        root: "_"//如果我们的库在浏览器中使用，需要提供一个全局的变量‘_’，等价于 var _ = (window._) or (_);
     }
   }
     ```
   
   **注意：** libraryTarget决定了你的library运行在哪个环境，哪个环境也就决定了你哪种模式去加载所引入的额外的包。也就是说，externals应该和libraryTarget保持一致。library运行在浏览器中的，你设置externals的模式为commonjs，那代码肯定就运行不了了。

   4 tree shaking 和 shimming
     
     1）JS tree shaking

   * webpack 2-3
   
   **tress-shaking只针对于ES6模块方式**
   在.babelrc设置babel-preset-es2015的modules为fasle，表示不对ES6模块进行处理成commonjs模块。

   * webpack 4

     2）CSS tree shaking

   * webpack 2-3

   * webpack 4


   5 懒加载


   6 创建library

   
   7 构建性能

