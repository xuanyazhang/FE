# JS(ES5)基础

#### ES5常用知识
* call,apply和bind的区别
   我们知道call,apply,bind都可以改变**函数调用this的指向,调用者是方法(函数)**

   call语法
    >**fun**.call(thisArg, arg1, arg2, ...)

    >thisArg: 在fun函数运行时指定的this值。需要注意的是，指定的this值并不一定是该函数执行时真正的this值，如果这个函数处于非严格模式下，则指定为null和undefined的this值会自动指向全局对象(浏览器中就是window对象)，同时值为原始值(数字，字符串，布尔值)的this会指向该原始值的自动包装对象。
    
    >arg1, arg2, ... 指定的参数列表

   apply语法
    >**fun**.apply(thisArg, [argsArray])

    >thisArg 在 fun 函数运行时指定的 this 值。需要注意的是，指定的 this 值并不一定是该函数执行时真正的 this 值，如果这个函数处于非严格模式下，则指定为 null 或 undefined 时会自动指向全局对象（浏览器中就是window对象），同时值为原始值（数字，字符串，布尔值）的 this 会指向该原始值的自动包装对象。
    
    >argsArray 一个数组或者类数组对象，其中的数组元素将作为单独的参数传给 fun 函数。如果该参数的值为null 或 undefined，则表示不需要传入任何参数。从ECMAScript 5 开始可以使用类数组对象。

   bind语法
    >**fun**.bind(thisArg[, arg1[, arg2[, ...]]])
    
    >thisArg 当绑定函数被调用时，该参数会作为原函数运行时的 this 指向。当使用new 操作符调用绑定函数时，该参数无效。
    
    >arg1, arg2, ... 当绑定函数被调用时，这些参数将置于实参之前传递给被绑定的方法。

    总结
    > 当我们使用一个函数需要改变this指向的时候才会用到call apply bind; fun.call/apply/bind()一次时，fun会立即执行一次然后返回

    > 如果你要传递的参数不多，则可以使用fn.call(thisObj, arg1, arg2 ...)
    
    > 如果你要传递的参数很多，则可以用数组将参数整理好调用fn.apply(thisObj, [arg1, arg2 ...])
    
    > 如果你想生成一个新的函数长期绑定某个函数给某个对象使用，则可以使用const newFn = fn.bind(thisObj); newFn(arg1, arg2...)

* 异步编程

   异步编程共有以下方法

   * 回调函数

   * 事件监听

   * 观察者

   * Promise

   * Generator
   
   * async/await
  
   **传统解决方案**

   回调函数和事件

   **Promise、Generator和async...await方案**

   Promise是一个容器，里面保存着某个未来才会结束的事件的结果，从语法上说，Promise是一个对象，从它可以获取异步操作的消息

