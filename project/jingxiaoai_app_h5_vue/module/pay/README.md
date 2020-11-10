<!-- 模块大标题 -->
# h5支付页面说明
<!-- 模块说明 -->
承载了所有的app端的支付，以及h5浏览器支付

<!--项目功能模块说明-->
## 不同项目下触发支付路径以及参数
<table>
    <tr>
        <th>产品名称</th>
        <th>页面路径</th>
        <th>传参说明</th>
    </tr>
    <tr>
        <td rowspan='2'>九分达人支付</td>
        <td rowspan='2'>https://jztest.jinghangapps.com/live/h5/paysubmit?payId=26&payCate=jiufen&webview=1</td>
        <td>payId：可以不准，但是必须有</td>
    </tr>
    <tr>
        <td>payCate：jiufen</td>
    </tr>
    <tr>
        <td rowspan='2'>直播课支付</td>
        <td rowspan='2'>https://jztest.jinghangapps.com/live/h5/paysubmit?payId=113&payCate=live&webview=1</td>
        <td>payId：直播课ID</td>
    </tr>
    <tr>
        <td>payCate：live</td>
    </tr>
    <tr>
        <td rowspan='2'>英语讲故事支付</td>
        <td rowspan='2'>https://jztest.jinghangapps.com/live/h5/paysubmit?5e79d055ccaa4d5995139537&payCate=story&webview=1</td>
        <td>payId：故事课程ID</td>
    </tr>
    <tr>
        <td>payCate：story</td>
    </tr>
    <tr>
        <td rowspan='2'>听力备考计划</td>
        <td rowspan='2'>https://jztest.jinghangapps.com/live/h5/paysubmit?payId=listentest&payCate=listentest&webview=1</td>
        <td>payId：listentest(写死)</td>
    </tr>
    <tr>
        <td>payCate：listentest</td>
    </tr>
</table>

<!-- 页面bridge交互说明 -->
## 页面和客户端(app)数据交互
#### 点击免费试用按钮，h5→app
```
接口：judgePayAppInstall
参数："wiexin"/"alipay"
结果：{"app":"weixin","data":"1"}
    安卓：通过调用window.judgePayAppInstallBack方法来告诉h5
    IOS：直接可以return给h5结果
```
#### 客户端调用方法，来检测是否支付成功，app→h5
```
接口：judgePayStatusByApp
参数：""
结果：客户端去调用后端接口，来判断是否支付成功
```
<!-- 页面bridge交互说明 -->
#### 支付成功页面，点击"开始课程"按钮，h5→app
```
接口：goToNinePointListen
参数：buy
说明：点击去九分达人学习原生页面
```
```
接口：goToAISpokenLearning
参数：无
说明：点击去ai口语课原生页面
```
```
接口：goToListenExaminationLearning
参数：无
说明：听力备考计划，预定成功页面点击去学习
```


<!-- 逻辑结构 -->
## 页面逻辑结构
<!-- 单个页面说明 -->
#### 支付提交页面（PaySubmit页面）
##### 1）页面运行逻辑
- [支付逻辑]()：客户端点击支付的时候，会调用客户端判断是否安装微信/支付宝，客户端返回检测结果，成功走剩余支付逻辑；失败直接提示安装相应的软件
- [支付检测]()：支付发起后会在本地保存当前商品的订单号，支付回来后首先根据localstorage中的订单号，向后台询问是否支付成功；支付成功去成功页，失败直接忽略
- [支付成功弹窗]()：自动查询的时候，如果没有支付成功就弹出弹出提示；如果手动查询，支付失败就弹出toast提示
##### 2）页面结构说秘银
- 商品详情：LivePay、StoryPay、JiufenPay
- 优惠券兑换：CouponSet
- 支付选择以及支付提交在当前页面，没有抽离

<!-- 单个页面说明 -->
#### 支付成功页面
##### 1）页面运行逻辑
- 根据payCate选择展示不同的成功结果，结果内容通过支付详情接口返回，存在了store里
- 页面组件：JiufenSuccess、LiveSuccess、StorySuccess

#### 修改地址组件逻辑
- 在PaySubmit页面直接引入组件，点击修改地址的时候，打开组件，并且在路径上添加  link+'#cover'来控制路由栈里增加一层路由
- 添加成功，或者回退页面，页面监听route的变化，来控制显隐修改地址组件
- 这样做的好处是避免页面硬性跳转带来的数据传递问题，减少页面维护成本

#### 兑换码组件逻辑
- 点击页面弹出兑换码列表，如果没有兑换码，点击兑换直接跳转兑换[页面]
- 兑换页面的展示和修改地址组件一个逻辑，都是通过路径里添加#来完成
