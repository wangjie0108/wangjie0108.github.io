---
title: vue传参、取值两种方式
date: 2018-10-17 22:52:24
categories:
    - "前端"
    - "Vue"
tags:
    - [query、params]
---
# query 传值、取值
+ 传值
```javascript
<div id='app'>
    <router-link to="/login?id=10&name=zs">登录</router-link>
    <router-link to="/register">注册</router-link>
    <!-- 占位 -->
    <router-view></router-view>
</div>
<script>
    var login = {
        // this就是指向当前创建的实例，因此不需要在这里加入this了
        template: '<h1>登录 --{{ $route.query.id }}--{{ $route.query.name }}</h1>',
        data() {
            return {
                msg: 'hhshsh'
            }
        },
        created() {
            // console.log(this.$route);
            // 查询参数可以直接通过 this.$route.query.id
            console.log(this.$route.query.id);
            console.log(this.$route.query.name);
        }
    }
    var register = {
        template: '<h1>注册</h1>'
    }
    var router = new VueRouter({
        routes: [
            {
                path: '/login',
                component: login
            },
            {
                path: '/register',
                component: register
            }
        ]
    })
</script>
```
+ 接收参数(注意：$route)
`this.$route.query.id`

# params 传值、取值
```javascript
<div id='app'>
    <router-link to="/login/12/zs">登录组件</router-link>
    <router-link to="/register">注册组件</router-link>
        <!-- 占位 -->
    <router-view></router-view>
</div>
<script>
var login = {
    template: '<h1>登录--{{ $route.params.id }}--{{ $route.params.name }}</h1>',
    created() {
        // 获取$route
        console.log(this.$route);
        // params方式获取值
        console.log(this.$route.params.id);
        console.log(this.$route.params.name);
    }
}
// 注册路由
var router = new VueRouter({
    routes: [
        {
            path: '/login/:id/:name',
            component: login
        },
        {
            path: '/register',
            component: register
        }
    ]
})
</script>
```
+ 接收参数
`this.$route.params`
+ query 是path引入;  params 是name引入
+ query 相当于get请求，页面跳转的时候，可以在地址栏看到请求参数
+ params 相当于 post请求，参数不会在地址栏中显示

