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
#### 加载完页面后，调用此方法打开分享按钮
```
接口：setShareInfo
参数："{
        shareTitle: '',
        shareUrl: '',
        shareImgUrl: '',
        shareContent: ''
    }"
用法：this.$bridge.callhandler('setShareInfo', JSON.stringify(shareInfo));
结果：调用客户端，让客户端打开分享按钮，并顺便将分享信息传给客户端
```
