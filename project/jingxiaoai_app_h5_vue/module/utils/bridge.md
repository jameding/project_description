<!-- 模块大标题 -->
# 公共的h5和app方法调用说明
<!-- 模块说明 -->
包含了全局的h5和app之间相互调用的方法


<!-- 页面bridge交互说明 -->
## H5调用客户端的方法
#### 点击打开微信，h5→app
```
接口：openWeixin
参数：""
结果：无
用法：this.$bridge.callhandler('openWeixin');
说明：点击打开微信，如果没有安装就没反应
```
#### 加载完页面后，调用此方法打开分享按钮，h5→app
1、放到了全局路由中，进入新页面的时候，会发送空信号给客户端<br />
2、进入单个页面后，再根据逻辑判断是否要设置分享按钮的数据
```
接口：setShareByApp
参数："{
        shareTitle: '',
        shareUrl: '',
        shareImgUrl: '',
        shareContent: ''
    }"
用法：this.$bridge.callhandler('setShareByApp', JSON.stringify(shareInfo));
结果：调用客户端，让客户端打开分享按钮，并顺便将分享信息传给客户端
```

#### 点击跳转到直播详情页webview的方法，h5→app
1、现在广告页面里有需求是点击按钮，跳转到直播详情页面
```
接口：goToWebviewLiveLessonDetail
参数："{
        courseId: '',
        url: '',
    }"
用法：this.$bridge.callhandler('goToWebviewLiveLessonDetail', JSON.stringify(data));
结果：调用客户端，让客户端打开直播详情webview
```

