---
title: div居中方式
date: 2018-3-04 21:41:46
categories: 
    - '前端'
    - js
tags: 
    - js
---
##### div居中方式
###### 第一种方式：
+ flex方式实现居中
    - 这些属性要放在居中元素的父元素上。
    - display:flex;
    - align-items: center;
    - justify-content: center;
    - align-items: center;
    - justify-content设置主轴(x轴)对齐方式
    - align-items设置侧轴(y轴)对齐方式
 ```javascript
<body>
    <div class="wrapper">
        <div class="demo"></div>
    </div>
</body>

// <!-- style样式 -->

<style>
    .wrapper {
        width: 400px;
        height: 400px;
        border: 1px solid #ccc;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .demo {
        width: 200px;
        height: 200px;
        background-color: pink;
    }
</style>
 ```
---
###### 第二种方式：
+ 这两个属性要放在居中元素的父级上，块级元素设置两个参数：
    - height
    - line-height会使块元素内部的含有行级元素特点的元素(这个元素身上有vertical-algin: middle;属性)垂直水平居中
    - height = line-height;
    - text-align: center;
 ```javascript
<body>
    <div class="wrapper">
        <div class="demo"></div>
    </div>
</body>

// <!-- style样式 -->

<style>
    .wrapper {
        width: 400px;
        height: 400px;
        border: 1px solid #ccc;
        line-height: 400px;
        text-align: center;
    }
    .demo {
        width: 200px;
        height: 200px;
        background-color: pink;
        display: inline-block;
        vertical-align: middle;
    }
</style>
 ```
---
###### 第三种方式：
+ 此方法适用于固定宽高的元素
    - 这些属性要作用在居中的元素本身
    - 绝对定位要注意父级的定位
    - position: absolute;
    - top: 50%;
    - left: 50%;
    - margin-top: -(高度的一半);
    - margin-left: -(宽度的一半);
```javascript
<body>
    <div class="wrapper">
        <div class="demo"></div>
    </div>
</body>

// <!-- style样式 -->

<style>
    .wrapper {
        width: 400px;
        height: 400px;
        border: 1px solid #ccc;
        position: relative;
    }
    .demo {
        width: 200px;
        height: 200px;
        background-color: pink;
        position: absolute;
        top: 50%;
        left: 50%;
        margin-top: -100px;
        mix-blend-mode: -100px;
    }
</style>
```
---
###### 第四种方式：
+ 非固定宽高
    - 这些属性要作用在居中的元素本身
    - 绝对定位要注意父级的定位
    - position: absolute;
    - top: 50%;
    - left: 50%;
    - transform: translate(-50%, -50%);
 ```javascript
<body>
    <div class="wrapper">
        <div class="demo"></div>
    </div>
</body>

// <!-- style样式 -->

<style>
    .wrapper {
        width: 400px;
        height: 400px;
        border: 1px solid #ccc;
        position: relative;
    }
    .demo {
        width: 200px;
        height: 200px;
        background-color: pink;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }
</style>
 ```
---
###### 第五种方式：
+ 不确定宽高的情况
    - 这些属性要作用在居中的元素本身
    - 绝对定位要注意父级的定位
    - position: ansolute;
    - top: 0;
    - left: 0;
    - right: 0;
    - margin: auto;
 ```javascript
<body>
    <div class="wrapper">
        <div class="demo"></div>
    </div>
</body>

// <!-- style样式 -->

<style>
    .wrapper {
        width: 400px;
        height: 400px;
        border: 1px solid #ccc;
        position: relative;
    }
    .demo {
        width: 200px;
        height: 200px;
        background-color: pink;
        position: absolute;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        margin: 0;
    }
</style>
 ```
---

