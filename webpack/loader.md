# loader

   loader加载器就是对各种非JS资源的解析，转化成浏览器可以识别的js/css文件，loader就是一个小型的编译器

   loader是webpack的核心概念之一，它的基本工作流是将一个文件以字符串的形式读入，对其进行语法分析及转换（或者直接在loader中引入现成的编译工具，例如sass-loader中就引入了node-sass将SCSS代码转换为CSS代码，再交由css-loader处理），然后交由下一环节进行处理，所有载入的模块最终都会经过moduleFactory处理，转成javascript可以识别和运行的代码，从而完成模块的集成。

### 常用loader

   1. css-loader|style-loader|less-loader|sass-loader|postcss-loader

   2. vue-loader

   3. babel-loader

   4. url-loader和 file-loader

   5. mocha-loader

### Loader开发

    loader是导出为一个函数的node模块，该函数在loader转换资源的时候调用，给定的函数将调用loader API，并通过this访问上下文
    
    
