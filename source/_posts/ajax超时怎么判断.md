---
layout: posts
title: ajax超时怎么判断
date: 2018-8-02 23:38:53
categories: 
    - '前端'
    - ajax
tags: 
    - ajax
---

+ ajax超时判断

```javascript
var ajaxTimeoutTest = $.ajax({
    url: '',
    timeout: 1000, //超时时间设置，单位毫秒
    type: 'get', // get post
    data: {},
    dataType: 'json', //返回数据格式
    success：function（data）{
    	alert（'成功'）;
    },
    complete: function(XMLHttpRequest, status) { //请求完成后最终执行参数
        if (status == 'timeout') { //超时，status还有success，error等值的情况
            ajaxTimeoutTest.abort();
            alert('超时');
        }
    }
})；
设置timeout的时间，通过检测complete时status的值判断请求是否超时，如果超时执行响应的操作。
```

