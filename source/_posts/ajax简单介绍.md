---
layout: posts
title: ajax简单介绍
date: 2018-7-14 23:38:53
categories: 
    - '前端'
    - ajax
tags: 
    - ajax
---

- 为什么需要ajax
    + 本质：在不刷新页面的情况下，使用XMLHttpRequest对象进行异步的向服务器发送http请求，把请求回来的数据用来局部更新页面
    sync同步、async异步
- 异步的概念
    + 从代码执行角度解释异步: 代码从上往下执行, 某些代码非常耗时, 导致后续代码迟迟不能执行, 这就是同步; 而如果某行代码比较特殊, 虽然耗时, 但不会阻塞, 这种代码运行方式就称为异步
    + 同步会造成什么后果？
        - 同步如果阻塞了会造成假死的状态
    + 异步代码典型案例
        - 定时器setTimeout
            1. 特点：程序的执行顺序不依赖于程序的书写顺序，有可能比下面的代码晚完成
    + 从生活中的例子来理解同步异步
        1. 同步：一直守在娃身边, 等娃醒来, 这个期间什么事情都不能做 ---> 页面假死状态
        2. 异步：在客厅玩一把王者荣耀, 娃醒来后会哭, 哭的话再去喂奶
    + 理解为什么ajax中的XMLHttpRequest要设计成异步
        1. 因为网速可能比较慢，ajax请求数据不确定啥时候请求回来，在这个阶段如果是同步的等待则当前页面就会假死状态
- 使用异步对象发送get请求
    + 先不考虑ajax,直接在地址栏访问validate.php来理解整个流程（/03-XMLHttpRequest-get/validate.php?username=jack） --> 打开fiddler
        + 参数在请求行当中
        + 没有请求体
    + 书写ajax代码
        1. 获取用户数据
        2. 让异步对象发送请求
        2.1 创建异步对象
        2.2 设置请求行 open(请求方式，请求url)
            + get请求如果有参数就需要在url后面拼接参数
            + post如果有参数，就在请求体中传递
        2.3 设置请求头 setRequestHeader('key','value')
            + get方式不需要设置请求头content-type
            + post需要设置content-type:application/x-www-form-urlencoded（这个是get请求与post请求的区别）
        2.4 设置请求体：发送请求 send(参数：key=value&key=value)
            + 如果有参数，post应该在这个位置传递参数
            + 对于get请求不需要在这个位置传递参数
    + 打开network
        - 发现请求已经发送了，接下来我们要考虑的问题是通过什么办法来接收到请求回来的数据
- 使用异步对象发送接收响应
    + 响应报文
        1. 报文行：响应状态码 响应状态信息 200 ok
        2. 报文头：服务器返回给客户端的一些额外信息
        3. 报文体：服务器返回给客户端的数据：responseText:普通字符串,responseXML:符合xml格式的字符串
    + 要判断两个东西　readyState+status
        - 在网上买东西 --> 东西有货（status == 200）+快递到了可以去拿（readyState == 4）
        - 一个真正成功的响应应该有两个方面：1.服务器成功响应 2.数据已经成功回到客户端并且可以使用了
        - status的值
            + 0 什么都没发生
            + 1 载入，已调用 send(),正在发送请求
            + 2 载入完成，send()方法完成，已收到全部相应内容
            + 3 解析，正在解析响应内容
            + 4 完成，响应内容完成解析，可以在客户端调用了
    + 从淘宝上买东西的角度把这整个的代码理解一下

```js
var xhr = new XMLHttpRequest();
xhr.open('get','./validate.php');//开始下单 我想去validate.php这个网店买东西，发货方式我选的是顺丰
xhr.send(null);//没有额外的信息需要和老板沟通
//下单完成之后，我继续上班，然后等快递
xhr.onreadystatechange = function(){
    //淘宝店有这个货          快递员打电话让我去拿
    if(xhr.status == 200 && xhr.readyState == 4){
        document.querySelector('.msg').innerHTML = xhr.responseText;//买到的东西
    }
}
```

- 使用异步对象发送post请求并接收响应
    + 可以先在写ajax代码之前，写一个普通的post表单，然后打开fiddler看一下请求报文中的content-type和请求体的数据
    + 与get的区别
        1. xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')
        2. xhr.send(请求体)
- 通过异步对象读取json文件生成动态页面结构
    + JSON.parse
    + JSON.stringify
- XML语法介绍和XML文件的创建示例
    + xml 是一种数据格式，类似 json 一样，用来表示某一组数据(用数组)、一个对象(用对象)
    + https://www.bejson.com/xml2json/（推荐用xml转json格式比较靠谱，用json转xml有点小问题）


- 通过异步对象读取XML文件并生成动态页面结构
    + querySelector
    + querySelectorAll
    + innerHTML
   
- jquery中的ajax介绍
    + 介绍一个插件:jquery code snippet
    + 常用属性
        1. type
        2. url
        3. data
        4. dataType
        5. success
    + 不常用的属性
        1. timeout 超时时间
        2. beforeSend 在发送之前如果使用return false则阻止ajax的发送（需要记住）
        3. error 报错的时候会触发
        4. complete ajax结束的时候会触发（不管是成功还是失败都会触发）
- jq中其他ajax方法的介绍
    + 推荐还是用$.ajax（用起来最灵活，因为我们可以设置beforeSend之类的属性）
    + 简单的场景可以使用$.get,$.post