<!-- 页面大标题 -->
# 听力备考计划，7天免费领取 和 入学测试报告页面

<!-- 页面说明 -->
由于页面交互接口少，所以多个页面写到一起了


<!--页面路径说明-->
## 7天免费领取

#### 页面路径说明
- 测试地址：https://jztest.jinghangapps.com/live/h5/listen/examination/freeGet?webview=1
- 生产地址：https://live.jinghangapps.com/live/h5/listen/examination/freeGet?webview=1

<!-- 页面bridge交互说明 -->
#### 页面和客户端(app)数据交互

##### web→app，告知客户端弹出联系老师的弹窗
```
方法：freeGetContactTeacher
参数："{'qrImg:'',wechat: '微信号：IELTS688'}"
```

##### app→web，客户端告知h5立即报名
```
方法：signUpImmediately
参数：''
```

<!--页面路径说明-->
## 雅思听力测评

#### 页面路径说明
- 测试地址：https://jztest.jinghangapps.com/live/h5/listen/examination/report?customplan=1&testId=123&pagetype=test&webview=1
- 生产地址：https://live.jinghangapps.com/live/h5/listen/examination/report?customplan=1&testId=123&pagetype=test&webview=1

### 参数说明
| 参数 | 有效值 | 传参说明 |
|--------|---------|---------|
|customplan | 0/1 | 0：不展示定制计划按钮<br/>1：展示 | 
|testId | 123 | 一个testId | 
|pagetype | test/stage | 默认 = test<br/>test：雅思测评的结果页面<br/>stage：阶段测试结果页面,此情况customplan无效 | 

<!-- 页面bridge交互说明 -->
#### 页面和客户端(app)数据交互

##### web→app，告知客户端点击了“定制专属备考计划”按钮
```
方法：customizePreparationPlan
参数：""
```

## 阶段测评结果

#### 页面路径说明
- 测试地址：https://jztest.jinghangapps.com/live/h5/listen/examination/report?pagetype=stage&webview=1
- 生产地址：https://live.jinghangapps.com/live/h5/listen/examination/report?pagetype=stage&webview=1

### 参数说明
| 参数 | 有效值 | 传参说明 |
|--------|---------|---------|
|pagetype | test/stage | 默认 = test<br/>test：雅思测评的结果页面<br/>stage：阶段测试结果页面,此情况customplan无效 | 

<!-- 页面bridge交互说明 -->
#### 页面和客户端(app)数据交互

#### web→app，告知客户端页面已经加载完成
告知客户端，客户端将做题的数据传给web端
```
方法：onPageFinish
参数：'true'
```

#### app→web，阶段测试，客户端将数据传递给web端
做题结束后，web端会给客户端传递测试结果，通过这个接口客户端再传回来
```
方法：stageReportPageInit
参数：'{testHasFinished/testHasPass/testReportInfo/nextCardType/nextCardId}'
```

##### web→app，告知客户端是“重新测试”or“继续学习”
阶段测试完毕到测试结果页面后，页面的按钮
```
方法：customizeStagePageAction
参数："retest" or "continueLearn"
```

<!--页面路径说明-->
## Lectrue测试报告页面

#### 页面路径说明
- 测试地址：https://jztest.jinghangapps.com/live/h5/listen/examination/lecturePort?cardId=1&webview=1
- 生产地址：https://live.jinghangapps.com/live/h5/listen/examination/lecturePort?cardId=1&webview=1

### 参数说明
| 参数 | 有效值 | 传参说明 |
|--------|---------|---------|
|cardId | 123 | 测评报告的cardId | 

<!-- 页面bridge交互说明 -->
#### 页面和客户端(app)数据交互

##### web→app，告知客户端点击了“重新测试”按钮
```
方法：customizeAgainLectureTest
参数：""
```

##### web→app，告知客户端点击了“分享成绩”按钮
这是一个全栈公共方法，点击去[查看](../../utils/bridge.md)