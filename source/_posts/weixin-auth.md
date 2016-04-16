---
title: 微信页面授权登陆
date: 2016-04-08 15:50:14
tags: 微信授权登陆
---

### 第一步：微信公众平台配置

首先登陆[微信公众平台](https://mp.weixin.qq.com/)，点击左侧菜单 开发 -> 接口权限，找到‘网页授权获取用户基本信息’，如下图：

![](1.png)

<!--more-->

我们点击修改，然后填上需要授权的域名，如下图：

![](2.png)



### 第二步：根据微信公众平台提供的开发文档授权并获取用户名和头像

#### 1.获取code	
只需要访问：[https://open.weixin.qq.com/connect/oauth2/authorize?appid=**您的appid**&redirect_uri=**授权地址成功后跳转URL**&response_type=code&scope=snsapi_userinfo&state=1&connect_redirect=1#wechat_redirect](javascript:;)

#### 2.通过code获取access_token，再根据access_token获取userinfo
```php
//通过code获取access_token
$code = $_GET['code'];
$appid = "您的appid";
$appsecret = "您的appsecret";
$url = "https://api.weixin.qq.com/sns/oauth2/access_token?appid=$appid&secret=$appsecret&code=$code&grant_type=authorization_code";
$result = https_request($url);
$jsoninfo = json_decode($result, true);

//根据access_token获取userinfo
$openid = $jsoninfo["openid"];
$access_token = $jsoninfo["access_token"];
$url1 = "https://api.weixin.qq.com/sns/userinfo?access_token=$access_token&openid=$openid&lang=zh_CN";
$result1 = https_request($url1);
$jsoninfo1 = json_decode($result1, true);

function https_request($url, $data = null)
{
    $curl = curl_init();
    curl_setopt($curl, CURLOPT_URL, $url);
    curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, FALSE);
    curl_setopt($curl, CURLOPT_SSL_VERIFYHOST, FALSE);
    if (!empty($data)) {
        curl_setopt($curl, CURLOPT_POST, 1);
        curl_setopt($curl, CURLOPT_POSTFIELDS, $data);
    }
    curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
    $output = curl_exec($curl);
    curl_close($curl);
    return $output;
}

//结果返回userinfo
echo json_encode($jsoninfo1);
```


