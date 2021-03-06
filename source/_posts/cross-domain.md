---
title: 跨域解决方案
date: 2016-04-16 13:22:36
tags: 跨域
---

## • 前期准备

用WAMP搭建两个站点分别：`http://www.example.com` 、 `http://api.example.com`，很显然第一个站点是主站点，第二个站点是提供服务的站点（当然我们在实际的架构上也是这种方式，我们还可以为提供静态资源专门配置一个站点诸如：`http://assets.example.com` ）。

## • JSONP解决GET跨域

关于跨域问题出现的，是因为浏览器 `同源策略` ，本文就不一一概述了这里主要讲干货，JSON和JSONP其实就像Java和JavaScript的区别，你可以理解为雷锋和雷锋塔的区别，JSONP是我们程序猿想出的跨域的解决方案，跟JSON没有办毛线的关系，我们先举一个通俗易懂的栗子：

首先在 `http://api.example.com` 域下新建一个文件：get_user_info.php，其内容

```php
$user_info = '{ "name": "张三", "age": "18" }';
echo "get_user_info($user_info)";
```

<!--more-->

然后在 `http://www.example.com` 域下创建一个文件：index.html，其内容

```html
<script>
    function get_user_info(data) {
        console.log(data);
    }
</script>
<script src="http://api.example.com/get_user_info.php"></script>
```

最后我们可以看到控制台输出的结果。其实这就是一个最基础的JSONP跨域，很显然我们利用了script标签发送GET请求，其实jQuery的实现也是采用这种方式，需要注意的是**JSONP只支持GET请求**。

```javascript
$.ajax({
    url: 'http://api.example.com/get_user_info.php',
    dataType: 'jsonp',
    jsonpCallback: 'get_user_info'
}).done(function (data) {
    console.log(data);
});
```

## • 设置Access-Control-Allow-Origin响应头

显然JSONP只支持GET请求，那么对于POST请求它就无能为力了，这个时候我们需要在服务端配置响应头Access-Control-Allow-Origin，并且添加允许跨域的域名

```php
header('Access-Control-Allow-Origin: http://www.example.com');
$user_info = '{ "name": "张三", "age": "18" }';
echo $user_info;
```

需要注意的是响应头允许跨域的域名结尾不要加‘/’，诸如 `header('Access-Control-Allow-Origin: http://www.example.com/');` ，假如需要允许跨多个域名需如下配置

```php
$origin = isset($_SERVER['HTTP_ORIGIN'])? $_SERVER['HTTP_ORIGIN'] : '';  

$allow_origin = array('http://www.example.com', 'http://www.example2.com'); 

if(in_array($origin, $allow_origin)){  
    header('Access-Control-Allow-Origin:'.$origin);       
} 
```

通过设置Access-Control-Allow-Origin响应头实现跨域，GET/POST请求方式都能够实现。

## • Apache反向代理

### 步骤一

配置Apache的httpd.conf文件，取消如下注释

```
LoadModule proxy_module modules/mod_proxy.so
LoadModule proxy_connect_module modules/mod_proxy_connect.so
LoadModule proxy_ftp_module modules/mod_proxy_ftp.so
LoadModule proxy_http_module modules/mod_proxy_http.so
```

### 步骤二

配置httpd-vhosts.conf文件

```
<VirtualHost *:80>
    DocumentRoot "D:/workspace/tech/www.example.com"
    ServerName www.example.com
        
    ##反向代理设置
    ProxyPass /action http://api.example.com/action
    ProxyPassReverse /action http://api.example.com/action
</VirtualHost>
```

### 步骤三

修改主站index.html文件，注意此时不要添加 `http://api.example.com` 这个域名前缀，因为我们做了反向代理，当我们访问 `http://www.example.com/action/get_user_info.php`，其实就是访问 `http://api.example.com/action/get_user_info.php`

```javascript
$.ajax({
    url: 'action/get_user_info.php',
    dataType: 'jsonp',
    jsonpCallback: 'get_user_info'
}).done(function (data) {
    console.log(data);
});
```

## 总结

本文介绍了三种最基础的跨域解决方案，无非就是JSONP、设置Access-Control-Allow-Origin响应头和反向代理代理这几种方式，个人觉得反向代理方式最简洁省事儿，只需要在服务器端配置即可。而其余两种都需要通过程序方式，相对来说开发成本较大。当然跨域的解决方法还有很多，诸如postMessage、iframe、PHP中curl和flash等等，这里面也有较多的坑，比如异步跨域请求在低版本的IE下需要用XDomainRequest对象来实现。