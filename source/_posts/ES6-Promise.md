---
title: ES6-Promise
date: 2018-9-25 11:09:11
categories:
    - '前端'
    - ES6
tags:
    - ES6
    - [Promise]
---
# Promise概念:
1. Promise 是一个构造函数，既然是构造函数，那么我们就可以new Promise()得到一个 Promise 的实例；
2. 在 Promise 上，有两个函数，分别叫做 resolve（成功之后的回调函数）和reject（失败之后的回调函数）
3. 在 Promise 构造函数的 Prototype 属性上，有一个 .then() 方法，也就是说，只要是 Promise构造函数创建的实例，都可以访问到 .then()方法；
4. Promise 表示一个异步操作；每当我们new一个 Promise 实例，这个实例，就表示一个具体的异步操作；
5. 既然 Promise 创建的实例，是一个异步操作，那么，这个异步操作的结果，只能有两种转态：
   - 5.1 转态1：异步执行成功了，需要在内部调用，成功的回调函数 resolve 把结果返回给调用者；
   - 5.2 状态2：异步执行失败了，需要在内部调用，失败的回调函数 reject 把结果返回给调用者
   - 5.3 由于Promise 的实例，是一个异步操作，所以内部拿到操作结果后，无法使用return 把操作的结果返回给调用者
6. 我可以在 new 出来的 Promise 实例上，调用.then() 方法，【预先】为这个 Promise 异步操作，指定 成功(resolve) 和 失败(reject) 回调函数
+ 注意： 这里 new 出来的 promise， 只是代表 【形式上】的一个异步操作；
+ 什么是形式上的异步操作：就是说，我们只知道它是一个异步操作，但是做什么具体的异步事情，目前还不清楚
    - var promise = new Promise()
+ 这是一个具体的异步操作，其中，使用 function 指定一个具体的异步操作
    - `var promise = new Promise(function() {`
        ​    `'这个 function 内部写的就是具体的异步操作'`
        `})`
```javascript
const fs = require('fs')
/**
 * 每当new一个 Promise 实例的时候，就会立即执行这个异步操作中的代码
 * 也就是说，new的时候，除了能够得到一个 Promise 实例之外， 还会立即代用 我们为 Promise 构造函数传递的那个function，执行这个function 中的异步操作代码：
*/
var promise = new Promise(function() {
    fs.readFile('./files/2.txt', 'utf-8', (err, dataStr) => {
        if(err) throw err
        console.log(dataStr)
    })
})
```
# Promise 的本质
+ Promise 的本质：就是单纯的为了解决回调地狱的问题，并不能帮我们减少代码量;
+ 使用ES6中的 Promise，来解决回调地域问题
+ new Promise的时候，会立即执行它的参数
+ then()方法默认返回的就是一个promise对象 
+ 在then中做异步操作，如果想维持这个then的函数链，那么必须要return new Promise
+ then 代表执行的顺序
# Promise 捕获异常的两种方式：
1.  如果前面的 Promise 执行失败，我们不想让后续的Promise操作被终止；
    - 当 我们有这样的需求： 哪怕前面的 Promise 执行失败了，但是，不要影响后续 promise 的正常执行，此时，我们可以单独为 每个 promise通过 .then()指定一下失败的回调；
```javascript
const fs = require('fs')

function getFileByPath(fpath) {
    return new Promise(function (resolve, reject) {
        fs.readFile(fpath, 'utf-8', (err, dataStr) => {
            if (err) return reject(err)
            resolve(dataStr)

        })
    })
}

getFileByPath('./files/11.txt')
    .then(function (data) {
        console.log(data)
        // 读取文件2
        return getFileByPath('./file/2.txt')
    }, function (err) {
        console.log('这是失败的结果:' + err.message);
        // return 一个新的 Promise
        return getFileByPath('./files2.txt')
    })
    .then(function (data) {
        console.log(data)
        return getFileByPath('./files/3.txt')
    }, function(err){
        console.log('这是失败的结果:' + err.message);
        return getFileByPath('./files/3.txt')
    })
    .then(function (data) {
        console.log(data)
    })
console.log('ok ok ok')
```
---
2. 有时候，我们有这样的需求，和上面的需求刚好相反：如果 后续的Promise 执行，依赖于 前面 Promise执行的结果，如果前面的失败了，则后面的就没有继续执行下去的意义了，此时，我们想要实现，一旦有报错，则立即终止所 Promise的执行；
    + catch 的作用： 如果前面有任何的 Promise 执行失败，则立即终止所有 promise 的执行，并 马上进入 catch 去处理 Promise中 抛出的异常
```javascript
const fs = require('fs)

function getFileByPath(fpath) {
    return new Promise(function (resolve, reject) {
        fs.readFile(fpath, 'utf-8', (err, dataStr) => {
            if (err) return reject(err)
            resolve(dataStr)

        })
    })
}
getFileByPath('./files/1.txt')
    .then(function (data) {
        console.log(data)

        // 读取文件2
        return getFileByPath('./files/22.txt')
    })
    .then(function (data) {
        console.log(data)

        return getFileByPath('./files/3.txt')
    })
    .then(function (data) {
        console.log(data)
    })  // catch处理 Promise异常
    .catch(function (err) {
        console.log('这是自己的处理方式：' + err.message)
    })
console.log('ok ok ok')
```
+ 在读取文件的案例中为什么封装Promise函数？
Promise表示一个异步操作，每当我们new Promise的时候 会立刻执行它的参数，而封装函数，就会阻止Promise的立即执行，在调用函数的时候，才会执行，Promise执行变得可控。。
---
# jquery中的 Promise
+ 初始化配置文件，安装jQuery
    - `npm i -y`
    - `npm i jquery`
+ 随便写了一个data.json的文件(注意：json文件里面不能有注释，且必须双引号("")包裹)
```javascript
{
    "name": "你的笑像一条恶狗",
    "gender":"撞乱了我心弦"
}
```
---
```javascript
<body>
    <input type="button" value="获取数据" id="btn">
    <script src="./node_modules/jquery/dist/jquery.min.js"></script>
    <script>
        $(function () {
            $('#btn').on('click', function () {
                $.ajax({
                    type: 'get', //get或post
                    url: './files/data.json', //请求的地址
                    // data: {}, //请求的参数，a=1&b=2或{a:1,b:2}
                    dataType: 'json', //text,json,xml
                    success: function (data) { //成功的回调函数
                        console.log(data);
                    }
                })
            })
        })
    </script>
</body>
```
