<!-- 页面大标题 -->
# 听力备考计划，入学测试 or 阶段测试页面

<!-- 页面说明 -->
听力备考计划，内置的入学测试属于h5写的，题目来源
- 剑雅+九分达人+og
- 从对应的section进行组合
- 优先测试剑雅-og-九分达人
- 优先展示用户未做过的section，若都做过则展示做的次数少的，若次数都一样，则随机展示


<!--页面路径说明-->
## 页面路径说明
- 测试地址：https://jztest.jinghangapps.com/live/h5/listen/examination/test?pagetype=stage&cardId=1
- 生产地址：https://live.jinghangapps.com/live/h5/listen/examination/test?pagetype=stage&cardId=1
### 参数说明
| 参数 | 有效值 | 传参说明 |
|--------|---------|---------|
|webview | 1 | 1的时候，说明是webview内嵌网页 | 
|token | xxxxx | webview=1的时候，需要传入token | 
|pagetype | 'test' or 'stage' | test：入学测试题目<br/>stage：阶段测试题目 | 
|cardId | 1 | pagetype = test的时候不用传 | 

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
客户端从接口v1/discover/listenPlan/getInTestQuestionsInfo获取的数据，传给web端
```
方法：listenTestPageInit
参数：'{"userAnswer":"{testId: 123,textId: 1232,answerObj: {}}","questionData":"res.data中的数据"}'
-----------------
userAnswer= "xx" or ""(如果没有请传"")
```

#### web→app，告知客户端应该播放当前sectioon的音频并且倒计时了
不管有多少个section步骤的题要做，都通过h5发起开始计时并播放音频的信息
```
方法：begainSectionExamination
参数：'{section:单个section数据,countDown:boolean}'
countDown: 是否展示3、2、1倒计时
```

#### app→web，用户中途退出的时候，保存当前做题进度，客户端通知web端告知用户做题数据的信号
这是一个通知信号，真正的web想app端报告做题数据的接口是下一个
```
方法：askExaminationUserAnswer
参数：''
```

#### web→app，客户端问当前做题数据的时候，web端通过此接口将做题记录发给客户端
保存的嘿嘿，客户端只有在收到此数据通知后，才可以真正的退出做题页面，如果传输的数据为空不要保存直接退出
```
方法：setExaminationUserAnswer
参数：'{testId: 123,textId: 1232,answerObj: {}}'  or  ''
```

#### web→app，通知客户端，测试结束，应该跳去结果页面了
交卷成功后，web端会通过此方法，让客户端去结果页面
```
方法：examinationIsOver
参数：''
```

#### web→app，通知客户端展示：“你确定现在交卷吗”弹窗
弹出弹窗后，用户如果选择交卷，客户端调用setExaminationHandIn，直接可以交卷
```
方法：examinationHandInAlert
参数：''
```


#### web→app，web端通客户端暂停/开始音频和倒计时
在用户完成每一个section的时候，通知客户端暂停音频和倒计时，如果出现提交错误，再打开音频和倒计时
如果倒计时结束了，重新开启是无效的，客户端注意下
```
方法：setExaminationAudioAndCountDown
参数：'stop' or 'play'
```

#### app→web，客户端通知web端，保存当前的sectionx的答题状态到后台
不管任何情况（主动交卷、倒计时结束）调用此方法，都会直接交卷，并且去结果页面
```
方法：setExaminationHandIn
参数：0 or 1  
----
如果是前边几个sectionx，就传0，如果是最后要强制交卷，就传1
```

#### web→app，通知客户端展示：“很抱歉数据出现异常，请重新答题”弹窗【作废】
这个地方，如果向后端保存做题数据接口出错，web端就会调用
- 有个坑：如果倒计时结束强制交卷，但是用户网络出现问题交卷出现错误，会出现错误弹窗，用户点击弹窗重新做题，此时倒计时已经结束了。。。可以讨论下方案
```
方法：examinationIsError
参数：''
```

##### web→app，告知客户端是“重新测试”or“继续学习”
阶段测试完毕到测试结果页面后，页面的按钮
``
方法：customizeStagePageAction
参数："retest" or "continueLearn"
```