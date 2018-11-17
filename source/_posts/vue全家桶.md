---
title: vue全家桶
date: 2018-11-14 23:03:40
categories:
    - 前端
    - Vue
tags:
    - Vue
---
# vue全家桶
# vue-router
+ vue的路由
+ 安装： `npm i vue-router`
+ 引用方式： 
    - 标签引用
    - 模块化引用
        - Vue.use(router)
        - 在根组件注册路由
        - render： 
            - 组件的渲染方式；
            - 缺点：会替换div#app

# vue-resource
+ 作用：`vue`中发送`http`的，但是官方已经不再维护了，建议使用`axios`
+ 安装： `npm i vue-resource`
+ 如何获取服务器返回的数据： 
    - `then(function(res){ res.body.message })`

# axios 
+ 作用： 发送`http`请求的工具（官方建议使用的）
+ 注意: `axios``then`中`this`指向不是当前的`vue`组件对象，所以建议使用箭头函数

# Vue-cli
+ 作用：`vue`项目的搭建工具
    - 可以帮助我们快速的生成一个基于`webpack`构建的模块化的`vue`项目，里面整合了常见的一些工具，比如`babel`和一些文件的`loader`还有`vue`的全家桶
+ 全局安装： `npm i vue-cli -g`
+ 定位到项目目录: `vue init webpack "项目名称"` 

# vueX
vue项目的状态管理（可以理解为vue的共享数据库）
+ 作用：存储一些共享的数据，所有的组件都可以访问vuex中的共享数据，解决了组件之间传值的问题
+ 引入：`Vue.use(Vuex)`
+ `var store = new Vuex.store({ })`
+ `vuex`的四个核心：
    - `state`状态（数据）：可以理解为组件对象中的`data`
        - `state`中数据如何变化？ `this.$store.state.**`
        - 可以通过`store.state`获取状态对象，`store.commit`触发状态变更
    - `getter`：对外提供数据，与组件中的过滤器比较像；可以认为是store的计算属性（和computed比较像），只有当它的依赖值发生了变化，才会重新计算；
    - `mutation`变化：可以理解为组件对象中的`methods`
        - 注意：`mutations`中不支持异步的操作
        - 里面的方法专门用来操作`state`中的数据
        - 更改`store`中的状态的唯一的方法，当`store`发生变化，需要提交的时候，会用到`mutations`
        - 在组件中通过`this.$store.commit('函数名')`调用mutations中的方法
    - `action`: 类似于mutations，但不完全相同
        - `action`提交的是`mutation`，而不是直接变更状态；
        - `action`可以包含任意异步操作
    - `module`
+ 注意点：不要再组件中直接修改vuex中state，而是要使用commit调用mutations中的函数。去修改state的值，
    - 好处： 避免数据紊乱，更好的追踪每个状态的变化
+ 什么时候对组件进行拆分？
    - 高复用，分治的情况下对组件进行拆分
    - 拆分组件有时是为了代码的简洁性和可阅读性
+ 什么时候使用路由？
    - 适用于构建单页面应用。vue的单页面应用基于路由和组件的，路由由于设定访问路径，并将路径和组件映射起来；
    - 传统的单页面应用是用一些超链接实现页面切换和跳转的；
    - 在`vue-router`单页面应用中，则是路径之间的切换，也就是组件之间的切换
- vue的一些插件：
    - vue-resource
    - http-server
    - v-tap
    - min-ui
    - vue-clipboard2
        - 网页端、H5操作剪切板

# data、props、vueX的区别？
- vueX相当于数据库，保存vue状态--就是保存vue的数据
- vueX是一个全局的共享数据存储区域，只有共享的数据才能放到vueX中；
- data：组件内部私有的数据才可以放到组件的data中去，数据是可读可写的；
- props：父子组件之间传递的数据才可以放到props中，且数据是只读的；
    