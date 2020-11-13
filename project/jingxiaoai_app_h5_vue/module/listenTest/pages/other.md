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
## 雅思听力测评结果页面

#### 页面路径说明
- 测试地址：https://jztest.jinghangapps.com/live/h5/listen/examination/report?customplan=1&webview=1
- 生产地址：https://live.jinghangapps.com/live/h5/listen/examination/freeGet?customplan=1&webview=1

### 参数说明
| 参数 | 有效值 | 传参说明 |
|--------|---------|---------|
|customplan | 1 | 0：不展示定制计划按钮，1：展示 | 

<!-- 页面bridge交互说明 -->
#### 页面和客户端(app)数据交互

##### web→app，告知客户端点击了“定制专属备考计划”按钮
```
方法：customizePreparationPlan
参数：""
```