<!-- 页面大标题 -->
# 九分达人活动落地页

<!-- 页面说明 -->
九分达人活动落地页，也就是活动展示页面
> 免费试用：webview端点击，去固定的听力做题页面、h5点击弹出下载提示<br>
> 立即购买：webview和h5都去购买此活动

<!--页面路径说明-->
## 页面路径说明
- 测试地址：https://jztest.jinghangapps.com/live/h5/jiufen/index?webview=1&token=123
- 生产地址：https://live.jinghangapps.com/live/h5/jiufen/index?webview=1&token=123
### 参数说明
| 参数 | 有效值 | 传参说明 |
|--------|---------|---------|
|webview | 1 | 1的时候，说明是webview内嵌网页 | 
|token | xxxxx | webview=1的时候，需要传入token | 

<!-- 页面bridge交互说明 -->
## 页面和客户端(app)数据交互
#### 点击免费试用按钮，h5→app
```
接口：goToNinePointListen
参数：free
```
