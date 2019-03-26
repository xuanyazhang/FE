# VUE-Router

### 使用指南

   1）Vue要全局引用VueRouter插件
   
   2）实例中要同时挂载 new VueRouter({})实例

   ```
   import Vue from 'vue'
   import VueRouter from 'vue-router'

   Vue.use(VueRouter)

   const router = new VueRouter({
       routes: [
           {path:'', component: 组件},{}...
       ]
   })

   new Vue({
       el: '',
       router,
       component: '根组件'
       template: "</跟组件>"
   })

   ```

   3）单页应用只有一个VueRouter实例，实例初始化全局的路由定义

   4）router-view 是 routes中定义的path对应的component的代词，实际渲染中会被component组件的渲染视图替换掉

   5) router-link 最后会被渲染为```<a>```标签中 存在与模版组件中， **切记router-link和router-view没有直接关系，router-view是组件的具体渲染结果，router-link只是组件中定义的链接元素**

### 常用知识

   1）动态路由匹配和编程式导航

   * 动态路由匹配： 
     path设置动态路由：{path:'/order/:orid/detail?name=jd', component:*}   
     component组件获取参数 **$route.**params获取参数对象{orid:*}  或者 $route.query获取查询对象{name:jd}

   * 编程式导航：除了使用 ```<router-link>``` 创建 a 标签来定义导航链接，我们还可以借助 router 的实例方法，通过编写代码来实现。 
    ```$this.**router**.push({ path: `/user/${userId}?name=${username}` })``` 

   * 一定注意：**$route**.params 和 $this.**router** 还有VueRouter实例配置中的 **routes** 千万别写错


   2）嵌套路由

   通过routes配置children属性实现, **是否需要在二级父页面添加```<router-view></router-view>```展示不同子组件视图，根据业务需求来**

    ```
    routes:[
        {path: '/order', component: resolve => require(['../../component/order.vue'], resolve),children: [
            { path: 'ordetail',  component: resolve => require(['../../component/ordetail.vue'], resolve) },
            { path: 'orcount',  component: resolve => require(['../../component/orcount.vue'], resolve) }
        ]},
    ]
    ```

   3）命名路由和视图

   * routes中命名路由：方便router-link引用

   * 命名视图是方便，不同router-view展示不同组件

   * routes中配置prop属性，可以给组件传参，解藕 $route.params方式获取参数

   * router-view 外层使用```<transition>```实现组件视图过渡

  
   4）导航守卫

   * beforeRouteEnter(to, from, next)
  
    to 和 from参数展示如下
   
    ![参数实例](../images/router.jpg)

   * beforeRouteUpdate

   * beforeRouteLeave