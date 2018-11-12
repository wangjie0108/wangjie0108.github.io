---
title: vue-cli的基本使用
date: 2018-10-27 19:29:13
categories:
    - 前端
    - vue
tags:
---
# VUE-CLi的基本使用
+ Vue-cli是快速构建这个单页应用的脚手架。
1. 使用`npm`安装全局`vue-cli`(前提你已经安装了node.js,[`node -v `: 可以查看`node`是否安装以及版本号])，在`cmd`中输入一下命令`npm install -g vue-cli`
2. 定位到项目目录运行 `vue init webpack "项目名称"`
3. 相关初始化信息提示：
1) `Runtime + Compiler: recommended for most users` 
运行加编译
2) `Runtime-only: about 6KB lighter min+gzip, but templates (or any Vue-specificHTML) are ONLY allowed in .vue files - render functions are required elsewhere`
仅运行时，已经有推荐了就选择第一个了
3) `Install vue-router? (Y/n)`
是否安装`vue-router`，这是官方的路由，大多数情况下都使用
4) `Use ESLint to lint your code? (Y/n)`
是否使用`ESLint`管理代码，`ESLint`是个代码风格管理工  具，是用来统一代码风格的，并不会影响整体的运行  
5) `Pick an ESLint preset (Use arrow keys)`   
选择一个`ESLint`预设，编写  `vue`项目时的代码风格
6) `Standard (https://github.com/feross/standard)  `
js的标准风格
7)` none (configure it yourself) `  
自己定义风格
8) Setup unit tests with Karma + Mocha? (Y/n)  
是否安装单元测试
9) `Setup e2e tests with Nightwatch(Y/n)?  `   
是否安装`e2e`测试
10) 自己用什么就在什么的后面回车就OK了
![Image text](/img/vue-cli1.png)
4. 安装完毕之后会生成项目目录 如图:
![Image text](/img/vue-cli.png)