<!-- 模块大标题 -->
# SpeakUp模块说明
<!-- 模块说明 -->
SpeakUp，是一个app端的常规模块，是嵌入到鲸小爱广告模块的一个ai，主要给机考产品引导商品购买的用的，主要包含通过SpeakUp详情页面直接让用户购买；还包括机考用户通过扫描机考那边设置的二维码，跳转到这边的购买页面产生购买行为

<!--项目功能模块说明-->
## 模块页面链接说明
| 页面名称 | 页面路径 | 传参说明 | 支持平台 |
|--------|---------|---------|---------|
|SpeakUp详情页 | https://jztest.jinghangapps.com/live/h5/speakup/adDetail?webview=1 | webview=1 | webview、h5 | 
| SpeakUp支付页 | https://jztest.jinghangapps.com/live/h5/paysubmit?payId=29&payCate=speakup&webview=1&phoneNumber=17288277311 | webview=1<br/>payId=1<br/>payCate=speakup<br/>phoneNumber=189.. | webview、h5 | 


## 支付模块说明

支付支持直接从机考项目通过扫码跳转到支付页面，跳转的路径如下：<br/>

```
https://jztest.jinghangapps.com/live/h5/paysubmit?payId=38&payCate=speakup&webview=1&phoneNumber=17877837773&transValue=123
```
transValue字段，是机考那边传过来的附加字段，支付成功后，会原封不动的通过支付回调传给机考服务端
