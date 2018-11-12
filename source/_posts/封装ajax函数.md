---
title: 封装ajax函数
date: 2018-8-06 10:14:44
categories: 
    - "前端"
    - ajax
tags:
    - ajax
---
# 封装ajax函数的目的
1. 了解ajax函数的原理
2. 理解success函数参数的含义
3. 掌握jq中$.ajax各属性的含义
- 测试数据如下（随意手写的data.json文件）：
```javascript
{
    "name": "这鬼天气强迫我穿上了秋裤"
}
```
- 因为有时候我们的接口数据的获取需要传入参数，比如?id=1指定到底获取哪条数据，我们这里假设数据需要传入参数a=1&b=2
1. 我们先用get方式实现
```javascript
<script>
    var xhr = new XMLHttpRequest();
    xhr.open('get', './data.json?a=1&b=2');
    xhr.send(null);
    xhr.onreadystatechange = function () {
        if (xhr.status == 200 && xhr.readyState == 4) {
            console.log(JSON.parse(xhr.responseText))
        }
    }
</script>
```
2. 接下来用post实现
```javascript
<script>
    var xhr = new XMLHttpRequest();
    xhr.open('post', './data.json')
    xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
    xhr.send('a=1&b=2');
    xhr.onreadystatechange = function() {
        if(xhr.status == 200 && xhr.readyState == 4) {
            console.log(JSON.parse(xhr.responseText));
        }
    }
</script>
```
3. 封装
```javascript
<script>
    function ajax(type, url, data, dataType){
        var xhr = new XMLHttpRequest();
        if(type == 'get') {
            xhr.open('get', './data.json?' + data);
            xhr.send(null);
        } else {
            xhr.open('post', url)
            xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
            xhr.send(data);
        }
        xhr.onreadystatechange = function() {
            if(xhr.status == 200 && xhr.readyState == 4) {
                if(dataType == 'json') {
                    console.log(JSON.parse(xhr.responseText));
                } else {
                    console.log(xhr.responseText);
                }
            }
        }
    }
    ajax('get', './data.json', 'a=1&b=2', 'json');
</script>
```
4. 进一步改造上面的代码
```javascript
<script>
    function ajax(type, url, data, dataType) {
        var xhr = new XMLHttpRequest();
        if (type == 'get') {
            xhr.open('get', './data.json? + data');
            xhr.send(null);
        } else {
            xhr.open('post', url)
            xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencode')
            xhr.send(data);
        }
        xhr.onreadystatechange = function() {
            if (xhr.status == 200 && xhr.readyState == 4) {
                var success = function(data) {
                    console.log(data);
                }
                if (dataType == 'json') {
                    success(JSON.parse(xhr.responseText))
                } else {
                    success(xhr.responseText)
                }
            }
        }
    }
    ajax('get', './data.json', 'a=1&b=2', 'json');
</script>
```
5. 提取success函数作为参数
```javascript
<script>
    function ajax(type, url, data, dataType, success) {
        var xhr = new XMLHttpRequest();
        if(type == 'get') {
            xhr.open('get', './data.json?' + data);
            xhr.send(null)
        } else {
            xhr.open('post', url);
            xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
            xhr.send(data);
        }
        xhr.onreadystatechange = function() {
            if(xhr.status == 200 && xhr.readyState == 4) {
                success(JSON.parse(xhr.responseText))
            } else {
                success(xhr.responseText)
            }
        }
    }
    ajax('get', './data.json', 'a=1&b=2', 'json', function(data) {
        console.log(data);
    });
</script>
```
6. 这样的代码在传参的时候很麻烦，考虑用对象的形式来传递
```javascript
<script>
    function ajax(type, url, data, dataType, success) {
        if (typeof data == 'object') {
            var str = "";
            for (var i in data) {
                str = i + '=' + data[i] + '&';
            }
            str = str.slice(0, str.length - 1)
            data = str;
        }
        var xhr = new XMLHttpRequest();
        if(type == 'get') {
            xhr.open('get', './data.json?' + data);
            xhr.send(null)
        } else {
            xhr.open('post', url);
            xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
            xhr.send(data);
        }
        xhr.onreadystatechange = function() {
            if(xhr.status == 200 && xhr.readyState == 4) {
                success(JSON.parse(xhr.responseText))
            } else {
                success(xhr.responseText)
            }
        }
    }
</script>
```
7. 把参数换成对象
```javascript
<script>
    function ajax(obj) {
        type = obj.type;
        url = obj.url;
        data = obj.data;
        dataType = obj.dataType;
        success = obj.success;
        if (typeof data == 'object') {
            var str = "";
            for (var i in data) {
                str = i + '=' + data[i] + '&';
            }
            str = str.slice(0, str.length-1)
            data = str;
        }
        var xhr = new XMLHttpRequest();
        if (type == 'get') {
            xhr.open('get', './data.json?' + data);
            xhr.send(null);
        } else {
            xhr.open('post', url);
            xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
            xhr.send(data);
        }
        xhr.onreadystatechange = function () {
            if (xhr.status == 200 && xhr.readyState == 4) {
                if(dataType == 'json') {
                    success(JSON.parse(xhr.responseText))
                } else {
                    success(xhr.responseText)
                }
            }
        }
    }
    ajax({
        type: 'get',
        url: './data.json',
        data: { a: 1, b: 2 },
        dataType: 'json',
        success: function (data) {
            console.log(data);
        }
    })
</script>
```
8. 全局变量容易造成变量污染，把它挂在一个对象上
```javascript
<script>
    var itcast = {
        ajax: function (obj) {
            type = obj.type;
            url = obj.url;
            data = obj.data;
            dataType = obj.dataType;
            success = obj.success;
            if (typeof data == 'object') {
                var str = "";
                for (var i in data) {
                    str = i + '=' + data[i] + '&';
                }
                str = str.slice(0, str.length - 1)
                data = str;
            }
            var xhr = new XMLHttpRequest();
            if (type == 'get') {
                xhr.open('get', './data.json?' + data);
                xhr.send(null);
            } else {
                xhr.open('post', url);
                xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
                xhr.send(data);
            }
            xhr.onreadystatechange = function () {
                if (xhr.status == 200 && xhr.readyState == 4) {
                    if (dataType == 'json') {
                        success(JSON.parse(xhr.responseText))
                    } else {
                        success(xhr.responseText)
                    }
                }
            }
        }
    }

    itcast.ajax({
        type: 'get',
        url: './data.json',
        data: {
            a: 1,
            b: 2
        },
        dataType: 'json',
        success: function (data) {
            console.log(data);
        }
    })
</script>
```
+ 如上封装，需要了解：
1. success 我们这里写的是data，其实写什么都无所谓
2. jq中的 data可以是对象，也可以 a=1&b=2这种形式都支持的
3. jq中除了$.ajax 除了这5个参数外，还有一些其他的参数属性名，如：
    - timeout
    - error
    - beforeSend(比如：提交表单数据之前，可以先对数据进行格式验证)
    - complete
