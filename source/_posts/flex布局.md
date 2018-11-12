---
title: flex布局
date: 2018-8-22 19:01:42
categories:
    - "前端"
    - Flex布局
tags:
    - Flex布局
---
# 伸缩布局
布局的传统解决方案，基于盒装模型，依赖于`display`属性 + `position`属性 + `float`属性。它对于那些特殊布局非常不方便。CSS3在布局页面方面做了非常强大的改进，使的我们对块级元素的布局排列变得十分灵活，强大的伸缩性，在响应式中可以发挥极大的作用。
# 重要属性
+ `display: flex;` 如果一个容器设置了这个属性，那么这个盒子里面的所有直接子元素都会自动变成伸缩项（`flex item`）
    + `justify-content`:定义了项目在主轴上的对齐方式
        + 语法： 
        `justify-content: flex-start | flex-end | center | space-between | space-around`
        - `flex-start(默认值)`: 左对齐
        - `flex-end`: 右对齐
        - `center`: 居中
        - `space-between`: 两端对齐，项目之间的间隔相等
        - `space-around`: 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍；
    - `flex-flow`: 是 `flex-direction` 属性和 `flex-wrap` 属性的简写；默认值是`row nowrap`;
        - `flex-flow:flex-direction | flex-wrap`
        - `flex-direction`：决定主轴的方向（项目排列方向：）
            - `flex-direction: row | row-reverse | column | column-reserve；`
            - `row(默认值)`：主轴为水平方向，起点在左端；
            - `row-reverse`：主轴为水平方向，起点在右端；
            - `column`：主轴为垂直方向，起点在上沿；
            - `column`：主轴为垂直方向，起点在下沿；
    - `flex-wrap`：控制flex容器是单行或者多行
        - `flex-wrap：nowrap | wrap | wrap-reverse；`
            - `nowrap(默认)`：不换行
            - `wrap`：换行，第一行在上方
            - `wrap-reverse`：换行，第一行在下方
    - `flex属性`：是`flex-grow`，`flex-shrink` 和 `flex-basis`的简写，默认值： `0 1 auto`，后两个属性可选;
        - `flex-grow`：定义项目的放大比例，默认：`0`，即如果存在剩余空间，也不放大
            - 如果所有项目的`flex-grow`属性都是`1`，则将它们等分剩余空间；如果一个项目的`flex-grow`属性为`2`，其他项目为`1`，前者占据的剩余空间将比其他项目多一倍；
        - `flex-shrink`：定义了项目缩小的比例，默认为`1`，即，如果空间不足，该项目将缩小；
            - 如果所有项目的`flex-shrink`属性都为`1`，当空间不足时，都将等比例缩小；如果一个项目的`flex-shrink`属性为`0`，其他项目都为`1`，则空间不足时，前者不会缩小；
            - 负值对该属性无效
        - `flex-basis`：属性值被设为`auto`的伸缩项，会根据主轴自动伸缩以占用所有剩余空间
            - 它可以设为跟`width`跟`height`属性一样的值(比如：350px)，则项目将占据固定的空间；


#### (^○^) 还有很多。。。。(^○^) 在百度上。。。。。 (^○^)..
# 一些案例：
1. 宽高自适应
```javascript
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        .layout {
            width: 500px;
            height: 600px;
            background-color: #CCCCCC;
            margin: 10px auto;
            /*设置父容器为伸缩盒子*/
            display: flex;
            /*默认的主轴是row,这里需要以列的方式进行排列*/
            flex-direction: column;
        }

        header {
            width: 100%;
            height: 60px;
            background-color: red;
        }

        main {
            width: 100%;
            background-color: green;
            /*让当前伸缩项占据父容器的剩余空间*/
            flex: 1;
            /*让main成为伸缩盒子*/
            display: flex;
        }

        main>article {
            height: 100%;
            flex: 1;
            background-color: pink;
        }

        main>aside {
            height: 100%;
            flex: 3;
            background-color: darkblue;
        }

        footer {
            width: 100%;
            height: 80px;
            background-color: purple;
        }
    </style>
</head>

<body>
    <div class="layout">
        <header></header>
        <main>
            <article></article>
            <aside></aside>
        </main>
        <footer></footer>
    </div>
</body>
```
2. 伸缩布局常用属性：align-items
```javascript
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        .box {
            width: 900px;
            height: 600px;
            border: 1px solid red;
            margin: 0 auto;
            /*设置父容器为盒子：会使每一个子元素自动变成伸缩项
             当子元素的宽度和大于父容器宽度的时候，子元素会自动平均收缩*/
            display: flex;
            /*设置子元素的主轴方向上的排列方式*/
            justify-content: space-around;
            /*align-items:设置子元素(伸缩项)在侧轴方向上的对齐方式
            center:设置在侧轴方向上居中对齐
            flex-start:设置在侧轴方向上顶对齐
            flex:end:设置在侧轴方向上底对齐
            stretch:拉伸：让子元素在侧轴方向上进行拉伸，填充满整个侧轴方向>> 默认值
            baseline:文本基线*/
            align-items: center;
        }

        .first {
            width: 200px;
            height: 200px;
            background-color: red;
            align-self: flex-start;
        }

        .second {
            width: 200px;
            height: 200px;
            background-color: green;
            /*设置单个元素在侧轴方向上的对齐方式*/
            align-self: flex-end;
        }

        .third {
            width: 200px;
            height: 200px;
            background-color: blue;
        }
    </style>
</head>

<body>
    <div class="box">
        <div class="first">bb</div>
        <div class="second" style="font-size: 100px">gg</div>
        <div class="third">klkaslg</div>
    </div>
</body>
```
3. 伸缩菜单
```javascript
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        div {
            width: 500px;
            height: 400px;
            border: 1px solid #ccc;
            margin: 100px auto;
        }

        div>ul {
            list-style: none;
            width: 100%;
            /*将父容器设置了伸缩盒子，子元素默认成为伸缩项  float margin*/
            display: flex;
        }

        div>ul>li {
            /*宽度
            1.我们并不知道li的具体的数量
            2.也不直接设置%*/
            height: 36px;
            line-height: 36px;
            text-align: center;
            background-color: #9fff9d;
            border-right: 1px solid #ccc;
            flex: 1;
        }
    </style>
</head>

<body>
    <div>
        <ul>
            <li>首页</li>
            <li>商品分类</li>
            <li>我的订单</li>
            <li>最新商品</li>
            <li>联系我们</li>
        </ul>
    </div>
</body>
```
4. flex 属性
```javascript
    <style>
        *{
            padding: 0;
            margin: 0;
        }
        .box{
            width: 800px;
            height: 500px;
            background-color: #ccc;
            margin:0 auto;
            /*设置父容器的为伸缩盒子*/
            display: flex;
            /*设置子元素在主轴方向上的排列方式*/
            /*justify-content: flex-start;*/
        }
        .left{
            /*flex是用来设置当前伸缩子项占据剩余空间的比例值*/
            flex: 2 2 auto;
            width:1000px;
            height: 500px;
            background-color: red;
        }
        .right{
            /* flex: 4; */
            flex: 2 5 auto;
            width:2800px;
            height: 500px;
            background-color: blue;
        }
    </style>
</head>
<body>
<div class="box">
    <div class="left"></div>
    <div class="right"></div>
</div>
</body>
```
