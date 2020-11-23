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
参数：'{commitItemCount:xx、lastCommitQuesItemId:xx、lastCommitQuesType:xx、totalItemCount:xx、realQuesInfo:xx、realQuesInfoFix:xx}'
```

#### web→app，告知客户端测试已经完成，可以继续其他逻辑了
新题型，后台设置了倒计时时间后，倒计时结束客户端强制web自动提交题目
一步选择题：直接强制提交
二部选择题：强制题目翻页
```
方法：countDownSubmitTheAnswer
参数：''
```
##### web→app，真题小练页面，告知客户端播放音乐或者倒计时
这里存在两种情况，
一种是新的题型（一步/两步）选择题，可能会给一个倒计时
二中是原先的提醒，会播放英文录音，也会告知客户端
```
方法：examinationZhenTellQuestionInfo
参数："{type:'audio',audioUrl:''}" or "{type:'countDown',timeout:213}"
```
##### web→app，真题小练页面，最后做完题后，用户点击完成按钮
用户点击完成按钮，告知客户端完成h5做题了，剩下的交给客户端处理了
参数为：最后一次提交答案后，后端返回的数据结果：res.data中的数据
接口：/v1/discover/listenPlan/uploadPracQuesItemAnswer
```
方法：examinationZhenTestIsOver
参数："res.data"
```