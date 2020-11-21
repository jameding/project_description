<!-- 页面大标题 -->
# 听力备考计划，真题小练页面

<!-- 页面说明 -->
真题小练页面比以前多了三种题型


<!--页面路径说明-->
## 页面路径说明
- 测试地址：https://jztest.jinghangapps.com/live/h5/listen/examination/zhenPractice
- 生产地址：https://live.jinghangapps.com/live/h5/listen/examination/zhenPractice
### 参数说明
| 参数 | 有效值 | 传参说明 |
|--------|---------|---------|
|webview | 1 | 1的时候，说明是webview内嵌网页 | 
|token | xxxxx | webview=1的时候，需要传入token | 

<!-- 页面bridge交互说明 -->
## 页面和客户端(app)数据交互

#### web→app，告知客户端页面已经加载完成
告知客户端，客户端将做题的数据传给web端
```
方法：onPageFinish
参数：'true'
```

#### app→web，客户端将接口数据传给web端
onPageFinish后；
客户端从接口/v1/discover/listenPlan/getPracQuesItem获取的数据，传给web端
```
方法：listenZenPageInit
参数：''
-----------------
userAnswer= "xx" or ""(如果没有请传"")
```

#### web→app，告知客户端测试已经完成，可以继续其他逻辑了
在测试完成后，在测试结果页面，用户点击屏幕继续其他逻辑
```
方法：clickGoOnOtherLogic
参数：''
```