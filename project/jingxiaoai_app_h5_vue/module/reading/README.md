<!-- 模块大标题 -->
# 阅读做题模块
<!-- 模块说明 -->
阅读模块相关的做题、查看答案等逻辑

<!--项目功能模块说明-->
## 模块页面链接说明
| 页面名称 | 页面路径 | 传参说明 | 支持平台 |
|--------|---------|---------|---------|
| 做题页面（题目/原文/答题记录） | https://jztest.jinghangapps.com/live/h5/reading/readIndex?cardType=question&classcificationType=0&textId=127&groupIds=128,129&isStart=0 | cardType=question<br/>classcificationType=0<br/>textId=127<br/>groupIds=128,129<br/>isStart=0 | webview | 
| 答案页面（题目/原文） | https://jztest.jinghangapps.com/live/h5/reading/readIndex?cardType=answer&recordId=8 | cardType=answer<br/>recordId=8 | webview | 


## 阅读做题页面与客户端的交互

#### web调app，告诉客户端网页已经加载完毕
告知客户端页面加载完成了，并且拿到的数据也传递给客户端
```
方法：onPageFinish
参数：'xxx'
```

#### web调app，告诉客户端切换tab菜单了
用户通过左右滑动页面，来触发切换不同的页面
```
方法：changeListenTab
参数：'0' or '1' or '2'
```

#### app调web，客户端告知网页应该切换页面了
用户可以点击顶部的原生页面来打到切换网站页面的需求
```
方法：changeListenPage
参数：0 or 1 or 2
```

#### app调web，客户端告知网页用户收起键盘了
这样可以控制输入框在屏幕的位置，ios貌似不用
```
方法：loseKeyboard
参数：''
```

#### app调web，客户端告知网页用户选择了某个选项，并将数据传递回来
和以前的传递的数据格式是一样的，openSelectOptionByApp传给客户端什么，客户端再传递回来
```
方法：setSelectOptionForWeb
参数：'xxxx'
```

#### web调app，配对选择题点击的时候，告知客户端弹出选择列表
```
方法：openSelectOptionByApp
参数：'xxxx'
```

#### app调web，告知网页端保存数据了
返回上一页的时候，直接
```
方法：savePracQuesProgress
参数：'{"useTime":1231212}'
```

#### app调web，告知网页端要交卷了
提交做题完毕，会到结果页面
```
方法：commitPracQues
参数：'{"useTime":1231212}'
```

#### app调web，提交答案的时候询问网页是否有为作答的题目
网页端会通过tellUserAnswerIsOver方法告知客户端，是否已经做完
```
方法：askUserAnswerIsOver
参数：''
```

#### web调app，网页告知客户端，当前做题是否已经全部做完
配合askUserAnswerIsOver使用，客户端的逻辑分两种情况
- 已经做完：直接调用强制交卷方法，让网页端交卷commitPracQues
- 没有做完：弹窗原生的交卷确认弹窗，点击了交卷按钮后，再调用commitPracQues
```
方法：tellUserAnswerIsOver
参数：'false' or 'true'   （参数是字符串形式的，不是布尔类型）
```

#### web调app，网页告知客户端，已经交卷，该去结果页面了
客户端要打开一个新的webview了
```
方法：answerOverAndToRes
参数：'{recordId:123}'
```

#### ！！！！！！web调app，网页告知客户端，打开一个新的webview
这个算作一个全局方法吧，后期再用的话就不用重新写了
客户端需要自己在后边填上  webview、token、version等公共字段（是加？开头还是&要判断一下）
```
方法：openNewWebview
参数：'https://jztest.jinghangapps.com/live/h5/reading/readIndex?cardType=question&classcificationType=0&textId=127&groupIds=128,129&isStart=0'
```

#### web调app，网页告知客户端，可以正常返回了
只有客户端让保存数据，这时候才会走这个方法
```
方法：tellAppGoBackPage
参数：''
```
#### web调app，用户点击网页上的，“再次练习”按钮
点击再次练习返回到作答页面且清空用户所有输入内容
```
方法：againAnswerQuestion
参数：''
```
