<!-- 模块大标题 -->
# 英语故事2.0，做题模块
<!-- 模块说明 -->
包含英语将中国故事2.0后的页面说明

<!--项目功能模块说明-->
## 模块页面链接说明
| 页面名称 | 页面路径 | 传参说明 | 支持平台 |
|--------|---------|---------|---------|
| 听力测试页面 | https://jztest.jinghangapps.com/live/h5/story/practice/index?seasonId=1&quesIndex=2&type=check |  | webview | 


## 诵读提，用户语音输入的时候与客户端的交互

#### web调app，web在诵读题页面告知app初始化ws连接或释放ws的动作通知
web开始进入第一个诵读题页面（app初始化ws连接）
web结束最后一个诵读题页面（app释放ws连接）
```
方法：storyPracticeSocketOpenOrClose
参数：'open'  or   'close'
```

#### web调app，点击开始录音的开始事件
点击话筒，开始诵读的开始事件，告知客户端相关数据，开始录音
```
方法：storyPracticeRecord
参数：后台返回的题目List的当前题item[object]数据
```

#### web调app，点击告诉客户端停止录音开始进入评分中
web会主动告知客户端录音停止
```
方法：storyTellAppPracticeRecordStop
参数：后台返回的题目List的当前题item[object]数据
```

#### app调web，告知web端，当前诵读录音的相关信息
客户端通过此接口告知所有录音的相关情况，包括不限于：异常情况、评分中等
不管是主动停止还是web端告知停止录音，都会调用此接口，告知web端相关情况
```
方法：storyTellWebPracticeRecordStatus
参数：有如下情况
0. {"status":"recordStart"}  告知web端开始录音中了
1. {"status":"connecting"}  音频流尚未成功建立连接【客户端自己处理了】
2. {"status":"cancel"}      录音被打断（取消）
3. {"status":"recordFinish"}  录音完成，app端开始等待打分
4. {"status":"scoreTimeout"}  app检测打分超时（30s）
5. {"status":"scoreSuccess", "data":算法段返回数据}
情况5中，也包含算法段认为数据异常的情况（例：音频时长过短/跑题）
```

#### app调web，告知web端，当前录音的音量大小【废弃】
web端页面上有一个波纹展示，此波纹通过客户端传输音量大小来控制
```
方法：storyTellWebRecordDecibel
参数：'12'
```

## 断网逻辑交互页面需求

#### web调app，告知客户端，要重新连接ws了
```
方法：storyPracticeSocketReconnect
参数：''
```
