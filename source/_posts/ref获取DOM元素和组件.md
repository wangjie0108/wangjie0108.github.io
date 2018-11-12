---
title: ref获取DOM元素和组件
date: 2018-11-07 00:43:00
categories:
    - 前端
    - Vue
tags:
    - Vue
---
# ref获取DOM元素和组件
```javascript
<body>
    <div id='app'>
        <input type="button" value="获取dom节点" @click="getElement" ref="mybtn">
        <h3 id="myh3" ref="myh3">哈哈哈，哈哈哈</h3>
        <hr>
        <login ref="mylogin"></login>
    </div>
    <script>
        var login = {
            template: '<h1>登录组件</h1>',
            data() {
                return {
                    msg: 'son msg'
                }
            },
            methods: {
                show() {
                    console.log('调用了子组件的方法');
                }
            }
        }
        var vm = new Vue({
            el: '#app',
            data: {},
            methods: {
                getElement() {
                    // 获取DOM元素
                    console.log(this.$refs.myh3.innerText)
                    // 获取子组件的信息
                    console.log(this.$refs.mylogin.msg)
                    // 获取子组件的方法
                    this.$refs.mylogin.show()
                }
            },
            components: {
                login
            }
        })
    </script>
```
![ref](/img/ref.png)
