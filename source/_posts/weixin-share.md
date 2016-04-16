---
title: 微信页面分享实现
date: 2015-09-08 16:45:46
tags: 微信公众平台 微信分享
---

## 第一步：微信公众平台配置

首先登陆[微信公众平台](https://mp.weixin.qq.com/)，点击左侧菜单 设置 -> 公众号设置，找到‘网页授权获取用户基本信息’：

![](1.png)

<!--more-->

我们点击第四项‘JS接口安全域名’，填上安全域名：

![注意：安全域名一个月内只能修改三次](2.png)

## 第二步：获取微信分享所需的四个参数

```php
//*载入微信工具类（微信SDK提供）
require 'extension/wxpay/WxPayPubHelper/SDKRuntimeException.php';
require 'extension/wxpay/WxPayPubHelper/WxPay.pub.config.php';
require 'extension/wxpay/WxPayPubHelper/WxPayPubHelper.php';

$jsApi = new JsApi_pub();
$jsApiParameters = $jsApi->getParameters();
$jsApiArr = json_decode($jsApiParameters, 1);
$ticket = get_ticket(get_token());

//给URL授权分享权限
$url = isset($_POST['url']) ? $_POST['url'] : '';
$signature = 'jsapi_ticket=' . $ticket . '&noncestr=' . $jsApiArr['nonceStr'] . '&timestamp=' . $jsApiArr['timeStamp'] . '&url=' . $url;
$signature = sha1($signature);
$result = array(
    'appid' => $jsApiArr['appId'],
    'timeStamp' => $jsApiArr['timeStamp'],
    'nonceStr' => $jsApiArr['nonceStr'],
    'signature' => $signature
);
echo json_encode($result);
```

根据后端返回的appid、timeStamp、nonceStr和signature四个字段实现分享：

```javascript
//*需引用微信jssdk

wx.config({
    debug: false,
    appId: '必填，公众号的唯一标识',
    timestamp: '必填，生成签名的时间戳', 
    nonceStr: '必填，生成签名的随机串', 
    signature: '必填，签名',
    jsApiList: ['onMenuShareTimeline', 'onMenuShareAppMessage', 'onMenuShareQQ', 'onMenuShareWeibo', 'onMenuShareQZone']
});
wx.ready(function () {
    var shareObj = {
        title: '分享的标题',
        desc: '分享的描述',
        link: '分享的URL',
        imgUrl: '分享的图片URL',
        trigger: function (res) {
        },
        success: function (res) {
        },
        cancel: function (res) {
        },
        fail: function (res) {
        }
    };

    //分享给朋友
    wx.onMenuShareAppMessage(shareObj);

    //分享到朋友圈
    wx.onMenuShareTimeline(shareObj);

    //分享到QQ
    wx.onMenuShareQQ(shareObj);

    //分享到微博
    wx.onMenuShareWeibo(shareObj);

    //分享到QZone
    wx.onMenuShareQZone(shareObj);

});

wx.error(function (res) {
    alert(res.errMsg);
});
```


