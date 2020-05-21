<!-- 项目大标题 -->
<h1 align="center">鲸小爱h5项目</h1>
<!-- 项目说明 -->
鲸小爱App内嵌h5以及分享出去的h5以及活动网站

<!--项目功能模块说明-->
## 项目功能模块说明
| 模块名称 | 模块说明 |
|--------|-----------
|登录模块 [login](./module/login)|项目登录模块，所有需要登录的页面都会自动跳转到此模块下进行登录，登录成功后再返回功能页面
|直播模块 [live](./module/live)|项目直播模块，主要围绕直播详情页面展开，支持webview和第三方浏览器打开
|支付模块 [pay](./module/pay)|项目支付模块，app内支付功能都走此模块，当然浏览器内涉及的支付功能也走此模块
|听力模块 [listen](./module/listen)|项目听力模块，鲸小爱内部的听力模块页面，包含听力做题、听力原文、核对答案功能
|英语故事 [story](./module/story)|用英语讲故事模块，和新航道合作的一个活动项目，应该到六七月份活动才会结束
|九分达人 [jiufen](./module/jiufen)|九分达人模块，包含九分达人活动详情页面，以及九分达人支付功能等
|AI口语课 [aiClass](./module/aiClass)|AI口语外教课模块，包含外教课活动详情页面，以及外教课支付、听力部分修改功能等


## 接口说明

### 测试接口
测试接口：大部分接口都走这个测试环境
```
https://test.jinghangapps.com/jingxiaoai
```
测试接口：说是还没步数到测试，先让用这个路径
```
http://jztest.jinghangapps.com:5432
```
支付接口：测试环境涉及到支付的走这一个接口
```
https://jztest.jinghangapps.com/live
```
### 生产接口
生产接口：生产环境下的接口地址
```
https://www.jinghangapps.com/jingxiaoai
```
