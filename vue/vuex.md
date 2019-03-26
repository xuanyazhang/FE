# VUEX

#### VUEX是什么？

   Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式，通俗来讲就是一个前端数据库，共享数据为私有属性，提供存取API供外部读写共享数据

#### VUEX基本语法
   
   store: new Vuex.Store({})   创建一个vuex数据仓库

   state: {}                   存储共享数据的对象

   getters: {}                 获取数据的函数的集合 通过this.$store.getters.方法名获取参数

   mutations: {}               设置数据的同步函数集合，通过this.$store.commit('方法命',{数据对象})修改数据

   actions: {}                 异步操作，调用context.commit()设置数据的函数集合，通过通过this.$store.dispatch('方法名')调用

   ```
   import {mapGetters,mapMutations,mapActions} from 'vuex'

   // mapGetters,mapMutations,mapActions 辅助函数应用在组件可以简化调用方式

   computed: {
     // 使用对象展开运算符将 getter 混入 computed 对象中
     ...mapGetters([
      'doneTodosCount',       // 用 `this.doneTodosCount` 代替为 `this.$store.getters.doneTodosCount`
      // ...
     ])
   },

    methods: {
        ...mapMutations([
           'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.commit('incrementBy', amount)`
        ]),

        ...mapActions([
        // `mapActions` 也支持载荷：
           'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.dispatch('incrementBy', amount)`
        ])
    }

   ```