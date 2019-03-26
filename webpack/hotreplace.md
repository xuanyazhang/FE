# 模块热替换

模块热替换(HMR - Hot Module Replacement)功能会在应用程序运行过程中替换、添加或删除模块，而无需重新加载整个页面。

主要是通过以下几种方式，来显著加快开发速度：

   * 保留在完全重新加载页面时丢失的应用程序状态。
   * 只更新变更内容，以节省宝贵的开发时间。
   * 调整样式更加快速 - 几乎相当于在浏览器调试器中更改样式。
   * 通过webpack-save-server和hot实现热替换

### CLI(命令行)方式： 

**命令行通过 webpack/webpack-dev-server --指令1 指令1值 --指令2 指令2值 进行指令赋值和**

   例如：

   ```
webpack-dev-server --colors --inline --hot --host 0.0.0.0 --port 3000 --open 'Chrome' --compress --content-base dist --config ./build/webpack.dev.js

   ```

### Option配置方式

通过在webpack.dev.js中的devServer配置项设置。对应上面的命令行配置如下

```
devServer: {
    // color和process只是CLI only
    contentBase: './dist', // 告诉浏览器内容从哪里来
    inline: true,
    host: "0.0.0.0", // 默认localhost,如果你希望服务器外部可访问，指定如下0.0.0.0
    port: 3000,  // 设置端口
    compress: true,  // 一切服务都启动gzip压缩
    open: 'Google Chrome', // 自动打开chrome浏览器
    hot: true // 启动webpack的模块热替换特性
    overlay: true // 编译源码错误时显示在IDE的命令控制台和页面中(输入url页面会是错误代码段)
}

```
> Note that **webpack.HotModuleReplacementPlugin** is required to fully enable HMR. If webpack or webpack-dev-server are launched with the --hot option, this plugin will be added automatically, so you may not need to add this to your webpack.config.js