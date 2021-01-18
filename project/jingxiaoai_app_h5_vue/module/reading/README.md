<!-- 模块大标题 -->
# 阅读做题模块
<!-- 模块说明 -->
阅读模块相关的做题、查看答案等逻辑

<!--项目功能模块说明-->
## 模块页面链接说明
| 页面名称 | 页面路径 | 传参说明 | 支持平台 |
|--------|---------|---------|---------|
| 做题页面（题目/原文/答题记录） | https://jztest.jinghangapps.com/live/h5/reading/readIndex?cardType=question&classcificationType=0&textId=127&groupIds=128,129&isStart=0 | cardType=question<br/>classcificationType=0<br/>textId=127<br/>groupIds=128,129<br/>isStart=0 | webview | 
| 答案页面（题目/原文） | https://jztest.jinghangapps.com/live/h5/reading/readIndex?cardType=answer&recordId=8&showAgain=1 | cardType=answer<br/>recordId=8<br/>showAgain=1 | webview | 


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
说明：如果是单选的时候，返回的userAnswer=1
     如果是多选的时候，返回的userAnswer=[1,3]
```

#### web调app，配对选择题点击的时候，告知客户端弹出选择列表
```
方法：openSelectOptionByApp
参数：'xxxx'
说明：客户端通过数据中的answer字段，判断当前数组的长度，
    1、如果是1就是单选，按照以前的逻辑
    2、如果大于1是多选，就走多选的UI和逻辑
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

#### app调web，“提交答案”或者“返回”的时候询问网页是否有为作答的题目
网页端会通过tellUserAnswerIsOver方法告知客户端，是否已经做完
```
方法：askUserAnswerIsOver
参数：交卷的时候'isOver'        返回的时候'isDown'
```
#### web调app，网页告知客户端，当前做题“是否已经全部做完”，“当前是否做过”
配合askUserAnswerIsOver使用，客户端的逻辑分两种情况
- 点击返回的时候,给客户端的数据为：{"isDown":"false"}
    - 有做过题目：弹出是否保存的确认弹窗
    - 没做过题目：直接返回上一页了
- 提交试题的时候，给客户端的数据为：{"isOver":"false"}
    - 已经做完：直接调用强制交卷方法，让网页端交卷commitPracQues
    - 没有做完：弹窗原生的交卷确认弹窗，点击了交卷按钮后，再调用commitPracQues
```
方法：tellUserAnswerIsOver
参数：{"isOver":"false"}   or    {"isDown":"false"} 
说明：isOver：是否做完，isDown是否做过（参数是字符串形式的，不是布尔类型）
```

#### web调app，网页告知客户端，已经交卷，该去结果页面了
客户端要打开一个新的webview了
```
方法：answerOverAndToRes
参数：'{recordId:123}'
```

#### web调app，在答题记录页面，点击答题记录卡片进入结果页面
```
方法：answerCardGoDetail
参数：'{ recordId: recordId }'
```

#### web调app，网页告知客户端，可以正常返回了
只有客户端让保存数据，这时候才会走这个方法
```
方法：tellAppGoBackPage
参数：''
```
#### web调app，用户点击网页上的，“再次练习”按钮
点击再次练习返回到作答页面且清空用户所有输入内容
注意：这时候客户端返回上一页，记得将tab切换回做题页面，顺便调用一下网页的切换方法:changeListenPage
```
方法：againAnswerQuestion
参数：''
```
