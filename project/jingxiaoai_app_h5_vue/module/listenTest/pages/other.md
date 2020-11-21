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
- 测试地址：https://jztest.jinghangapps.com/live/h5/listen/examination/report?customplan=1&webview=1
- 生产地址：https://live.jinghangapps.com/live/h5/listen/examination/freeGet?customplan=1&webview=1

### 参数说明
| 参数 | 有效值 | 传参说明 |
|--------|---------|---------|
|customplan | 0/1 | 0：不展示定制计划按钮<br/>1：展示 | 
<!-- |pagetype | test/stage | 默认 = test<br/>test：雅思测评的结果页面<br/>stage：阶段测试结果页面,此情况customplan无效 |  -->

<!-- 页面bridge交互说明 -->
#### 页面和客户端(app)数据交互

##### web→app，告知客户端点击了“定制专属备考计划”按钮
```
方法：customizePreparationPlan
参数：""
```

<!--页面路径说明-->
## Lectrue测试报告页面

#### 页面路径说明
- 测试地址：https://jztest.jinghangapps.com/live/h5/listen/examination/lecturePort?id=1&webview=1
- 生产地址：https://live.jinghangapps.com/live/h5/listen/examination/lecturePort?id=1&webview=1

### 参数说明
| 参数 | 有效值 | 传参说明 |
|--------|---------|---------|
|id | 123 | 测评报告的id | 

<!-- 页面bridge交互说明 -->
#### 页面和客户端(app)数据交互

##### web→app，告知客户端点击了“重新测试”按钮
```
方法：customizeAgainLectureTest
参数：""
```

##### web→app，告知客户端点击了“分享成绩”按钮
这是一个全栈公共方法，点击去[查看](../../utils/bridge.md)