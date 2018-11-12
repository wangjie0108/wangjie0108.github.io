---
title: rem与em的使用
date: 2018-1-14 09:48:59
categories:
    - 前端
    - 移动端
tags:
    - 移动端
---
```javascript
    <style>
        html {
            font-size: 20px;
        }

        .box {
            /*
            width: 100px;
            height: 100px;*/
            width: 10em;
            height: 10em;
            background-color: red;
            font-size: 18px;
            /*1em=16  18/16 em*/
        }
        .parent {
            width: 10rem;
            height: 10rem;
            background-color: blue;
            font-size: 12px;
        }
    </style>
</head>

<body>
    <div class="box">
        写一些字
    </div>
    <div class="parent">
        也写一些字
    </div>
</body>
```
1. `em`:就是一种长度单位，它是参照当前元素的字号，如果没有设置，就参照父容器或者当前浏览器的默认字号
2. `rem`是`css3`新增的一种长度单位，它是参照根元素(`html`)的字号
![rem与em](/img/rem.png)