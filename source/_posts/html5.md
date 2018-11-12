---
title: html5
date: 2018-5-28 19:29:03
categories:
tags:
---

# HTML5中的一些新特性
- 用于绘画的canvas元素
- 用于媒介回放的video和audio元素
- 对本地离线存储的更好的支持
- 语义化标签
- 新的表单控件  如：data  time  email  search
- 类样式操作

# 新增标签的兼容情况
1. IE9-IE10：浏览器不支持元素宽高，可以转化：display：block；
2. IE8以下不认识H5新增标签，可以引入js文件，解决兼容问题（还可以动态创建H5新增标签，但是会比较的麻烦）

# 样式
```javascript
添加样式： add()
移除类样式：remove()
切换样式：toggle()
判断是否包含某种类样式： constains()
```

# 自定义属性

```javascript
规范：
1.data-开头
2.data-后必须至少有一个字符，多个单词使用-连接
建议：
1.名称该使用小写
2.名称中不要任何的特殊字符
3.名称不要使用纯数字
```

# 获取自定义属性

```javascript
将data-后面的单词使用camel命名链接：必须使用camel合法取值，否则有可能无法获取
```



# DOM扩展，获取元素的方式

1. `document.querySelector('传入选择器名称')`

```javascript
参数要求：传入id传感器，需要加入#；传入类选择器，需要加入点（.）
只能获取单个元素，如果获取的元素不止一个，name只会返回第一个元素
可传入后代选择器
```

2. `document.querySelectorAll('传入选择器名称'`)

```javascript
获取满足条件的所有元素，返回伪数组
改变子元素color，需要遍历数组
```

# 表单新增type属性

`email`  `data`  `range`  `datatime`  `...`

`oninput`:  

```javascript
监听当前指定元素的内容改变，只要内容改变（内容增加，内容删除）就会触发这个事件  ------针对内容
```

`onvalid`:    

```javascript
当前验证不通过，就会触发
```
# SessionStorage:
1. 存储在本地，容量： 5MB左右
2. 这个数据本质是存储在当前页面的内存中---意味着：在其他页面和浏览器无法获取数据
3. 它的生命周期为当前页面关闭，关闭页面，数据会自动清除
    - setItem(key, value) 存储数据，以键值对的方式存储
    - getItem(key)      获取数据，通过指定名称获取对应的value值
    - removeItem(key)  删除数据，指定名称删除对应的数据
+ 特别注意：
    - 删除数据：在删除的时候，如果key错误，不会报错，但也不会删除数据

# localStorage：
1. 容量：20MB
2. 不同浏览器不能共享数据，但是在同一浏览器的不同窗口中可以共享数据
3. 生命周期：
    - 永久有效：它的数据是存储在硬盘上的，并不会随着页面或者浏览器的关闭而清除，如果想要删除，必须手动清除
    - setItem()
    - getItem()
    - removeItem()
    - clear() 清除所有内容

# cookie、 sessionStorage 和 localStorage区别：
    - 相同点：都存储在客户端
    - 不同点：
    1. 存储大小
    cookie数据大小不能超过4K；
    sessionStorage 和 localStorage虽然也有存储大小的限制，但比cookie大很多，可以达到5M或更大；
    2. 有效时间
    localStorage 存储持久数据，浏览器关闭后数据不丢失除非主动删除数据；
    sessionStorage 数据在当前浏览器窗口关闭后自动删除；
    cookie 设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭；
    3. 数据与服务器之间的交互方式
    cookie 的数据会自动的传递到服务器，服务器端也可以写cookie到客户端
    sessionStorage 和 localStorage 不会自动把数据发送给服务器，仅在本地保存；