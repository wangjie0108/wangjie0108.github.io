---
title: CSS3动画
date: 2018-5-06 16:49:42
categories:
    - "前端"
    - "CSS3"
tags:
    - "CSS3"
---
# 什么是CSS3中的动画？
1. 动画使元素从一种样式逐渐变化成为另外一种样式的效果
2. 用表比分来规定变化发生的时间，或用关键词"from"和"to"，等同于0% 和 100%
3. 0% 是动画的开始  100%是动画的完成
4. 如果在CSS3中创建动画，需要用 @keyframes 规则创建动画
5. @keyframes 规定至少以下两项CSS3动画属性，即可将动画绑定到选择器：
    - 规定动画的名称
    - 规定动画的时长

# 写过的动画的小栗子：
+ 动画的添加

```javascript
<style>
    *{
        padding: 0;
        margin: 0;
    }
    div{
        width: 100px;
        height: 100px;
        background-color: red;
        transform: translate(0,0) rotate(80deg);
        /*添加动画效果*/
        /*1.animation-name:指定动画名称*/
        animation-name: moveTest;
        /*2.设置动画的总耗时*/
        animation-duration: 2s;
        /*3.设置动画的播放次数，默认为1次  可以指定具体的数值，也可以指定infinite(无限次)*/
        animation-iteration-count: 1;
        /*4.设置交替动画  alternate:来回交替*/
        animation-direction: alternate;
        /*5.设置动画的延迟*/
        animation-delay: 0s;
        /*5.设置动画结束时的状态：默认情况下，动画执行完毕之后，会回到原始状态
        forwards:会保留动画结束时的状态，在有延迟的情况下，并不会立刻进行到动画的初始状态
        backwards:不会保留动画结束时的状态，在添加了动画延迟的前提下，如果动画有初始状态，那么会立刻进行到初始状态
        both:会保留动画的结束时状态，在有延迟的情况下也会立刻进入到动画的初始状态*/
        animation-fill-mode: both;
        /*6.动画的时间函数*/
        animation-timing-function: linear;
        /*设置动画的播放状态  paused:暂停   running:播放*/
        animation-play-state: running;
        /* animation: moveTest 2s linear 0s infinite alternate both; */
    }

    /*创建动画*/
    @keyframes moveTest {
        /*百分比是指整个动画耗时的百分比  10s*/
        /*0%{
            transform: translate(0,0);
        }*/
        /*from:0%*/
        from{
            transform: translate(0,0) rotate(45deg);
        }
        /*0~1*/
        50%{
            transform: translate(0,500px);
        }
        /*1~2*/
        /*100%{
            transform: translate(500px,600px);
        }*/
        /*to:100%*/
        to{
            transform: translate(500px,600px);
        }
    }
</style>
```
```javascript
<body>
<div></div>
<input type="button" value="播放" id="play">
<input type="button" value="暂停" id="pause">
<script>
    var div=document.querySelector("div");
    document.querySelector("#play").onclick=function(){
        div.style.animationPlayState="running";
    }
    document.querySelector("#pause").onclick=function(){
        div.style.animationPlayState="paused";
    }
</script>
</body>
```
+ 动画实现无缝连接

```javascript
<style>
    *{
        padding: 0;
        margin: 0;
    }
    div{
        width: 882px;
        height: 86px;
        margin:100px auto;
        background-color: #ddd;
        overflow: hidden;
    }
    div >ul{
        width: 200%;
        list-style: none;
        /*1.设置的名称*/
        animation-name: move;
        /*2.设置动画的耗时*/
        animation-duration: 7s;
        /*3.市场无限循环*/
        animation-iteration-count: infinite;
        /*4.设置时间函数*/
        animation-timing-function: linear;
    }

    div > ul > li{
        width:126px;
        float: left;
    }
    div > ul > li　> img{
        width:100%;
    }
    /*鼠标上移，停止动画*/
    div:hover > ul{
        cursor: pointer;
        animation-play-state: paused;
    }

    /*创建动画*/
    @keyframes move {
        from{
            transform:translateX(0);
        }
        to{
            transform:translateX(-882px);
        }
    }
    //  这里如果换成 translateY(0) - translateY(..) 动画就是上下滚动
</style>
```
```javascript
<body>

<div>
    <ul>
        <li><img src="../images/1.jpg" alt=""></li>
        <li><img src="../images/2.jpg" alt=""></li>
        <li><img src="../images/3.jpg" alt=""></li>
        <li><img src="../images/4.jpg" alt=""></li>
        <li><img src="../images/5.jpg" alt=""></li>
        <li><img src="../images/6.jpg" alt=""></li>
        <li><img src="../images/7.jpg" alt=""></li>
        <li><img src="../images/1.jpg" alt=""></li>
        <li><img src="../images/2.jpg" alt=""></li>
        <li><img src="../images/3.jpg" alt=""></li>
        <li><img src="../images/4.jpg" alt=""></li>
        <li><img src="../images/5.jpg" alt=""></li>
        <li><img src="../images/6.jpg" alt=""></li>
        <li><img src="../images/7.jpg" alt=""></li>
    </ul>
</div>

</body>
```