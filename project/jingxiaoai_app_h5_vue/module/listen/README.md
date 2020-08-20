<!-- 模块大标题 -->
# 听力做题模块
<!-- 模块说明 -->
包含听力做题页面、听力原文页面、听力答案页面

<!--项目功能模块说明-->
## 模块页面链接说明
| 页面名称 | 页面路径 | 传参说明 | 支持平台 |
|--------|---------|---------|---------|
| 听力详情页面 | https://jztest.jinghangapps.com/live/h5/listening?pageType=answer&pageIndex=0 | pageType=answer<br/>pageIndex=1 | webview | 
| 口语听力页 | https://jztest.jinghangapps.com/live/h5/listening?pageType=answer&pageIndex=0&payCate=spoken | pageType=answer<br/>pageIndex=1<br/>payCate=spoken | webview | 
| 精听详情页面 | https://jztest.jinghangapps.com/live/h5/listening?pageType=listen&pageIndex=0&test=1 | pageType=listen<br/>pageIndex=0 | webview | 
| 点选/显示、纸练 | https://jztest.jinghangapps.com/live/h5/listen/training/index?page=clickShow | page=clickShow | webview | 

## 各种题型的功能划分
单选：单选题 -- <br/>
多选：多选题 -- <br/>
填空：表格填空题、图片填空题、完成句子 -- 流程图题、笔记填空题<br/>
调客户端：配对选择题 -- 地图题、排序题<br/>


## 精听页面长按选词的时候与客户端的交互

#### web调app，长按选中单词后，发给客户端，让其展示出来
长按选中后，web端先调用后端接口，
- 接口返回了数据就告诉客户端
- 接口返回了空的数据，就忽略掉当做什么也没发生
```
方法：showVocabularyCard
参数：后端给的单词数据，我也不知道啥
```

#### 【暂时无用】web调app，长按选中单词后，提示客户端隐藏掉弹出的单词释义弹窗
web端点击页面隐藏掉选中的单词后，客户端也要隐藏弹窗，并开始播放声音（如果弹出前在播放的情况下）
```
方法：hideSelectWordByApp
参数：''
```
#### app调web，告知web关闭精听模式下选中的单词
web页面上方点击可以自己隐藏，但是用户点击弹出的单词示意弹窗，web就无法取消选中的单词了，所以要写个方法暴露给客户端，以便客户端能够主动取消web中的单词选中
```
方法：resetSelectWordForWeb
参数：无
```

## 练习模式（点选、点显、纸练模式）的页面控制

#### 页面进入的路径
http://localhost:8080/live/h5/listen/training/index?page=paperSet
- 参数page：点显(clickShow)、点选(clickSelect)、纸练设置(paperStart)、纸练(paperGame)
- 参数textId：测试环境下，网页打开直接通过textId获取后端数据，客户端不要加此字段

#### web调app，页面加载完毕后告知客户端，web准备好了
```
方法：onPageFinish
参数：'true'
```
#### app调web，进入到（点选、点显、纸练）页面下，传递给web初始化的数据
这个数据是客户端拿到后端接口，传递给web的
```
方法：trainingPageInit
参数：getOriginalsData接口获取到的字符串数据
```
#### app调web，控制切换点选、点显、纸练模式
原生页面顶部有三个tab按钮，通过按钮控制web页面的切换
```
方法：setTrainingPageByApp
参数：'clickShow'
参数说明：点显(clickShow)、点选(clickSelect)、纸练设置(paperStart)、纸练(paperGame客户端不需要调用这个)
```

#### web调app，点击开始训练的时候，弹出3、2、1倒计时
纸练开始页面，点击开始的时候，弹出倒计时的原生页面
```
方法：paperPenCountDownByApp
参数：无
```

#### web调app，网页自动切换做题模式的时候 ，让原生的顶部tab跟着动
纸练模式结束后，点击结束按钮会跳转到点选模式，这个时候要让原生的顶部tab也切换
```
方法：changeTrainingPageByApp
参数：'clickShow'
参数说明：点显(clickShow)、点选(clickSelect)、纸练设置(paperStart)
```

#### app调web，进入纸练模式后，控制页面自动播放声音
纸练开始页面，点击开始的时候，弹出倒计时的原生页面
```
方法：paperGamePlayMusic
参数：'play' or 'pause'
```
