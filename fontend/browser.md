# 浏览器

### 浏览器基本工作原理

 **浏览器内核**由渲染引擎和JS引擎组成

 浏览器是由多个进程组成，每个进程都有自己核心的职责，它们互相配合完成浏览器的整体功能，进程就像是一个有边界的生产厂间，而线程就像是厂间内的一个个员工，可以自己做自己的事情，也可以相互配合做同一件事情。

 浏览器进程：

 Browser Process: 浏览器主进程 控制tab
 Network Process: 网络进程 处理网络请求，从网上获取数据
 UI Process: UI进程 控制浏览器上的按钮，输入框
 Renderer Process: 渲染进程
 GPU Process: GPU进程
 Plugin Process: 插件进程
 Storage Process: 存储进程 控制文件等的访问
 Device Process: 设备进程


### 渲染进程是如何工作的

渲染进程的核心目的在于转换HTML CSS JS为用户可交互的web页面，渲染进程包括以下线程：

1. 主线程 Main Tread
2. 工作线程 Worker Thread
3. 排版线程 Compositor Thread
4. 光栅线程 Raster Thread

![DOM树](https://sylvanassun.github.io/2017/10/03/2017-10-03-BrowserCriticalRenderingPath/)
 