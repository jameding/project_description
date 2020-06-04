<!-- 页面大标题 -->
# AI外教口语课详情落地页

<!-- 页面说明 -->
AI外教口语课详情落地页，支持在app内展示，也支持分享出去展示
> 立即报名：webview和h5都去购买此活动，购买完成后显示去学习
> 去学习：webview点击去原生学习页面，h5点击去下载页面

<!--页面路径说明-->
## 页面路径说明
- 测试地址：https://jztest.jinghangapps.com/live/h5/spoken/courseDetails?courseId=1&source=1&webview=1&token=123
- 生产地址：https://live.jinghangapps.com/live/h5/spoken/courseDetails?courseId=1&source=1&webview=1&token=123
### 参数说明
| 参数 | 有效值 | 传参说明 |
|--------|---------|---------|
|courseId | 1 | 课程的ID | 
|source | 1 | AI列表页进入(0)、课程页-我的课程-为你推荐(1)、课程页-我的课程-已预约(2)、详情页推荐进入(3)、学习完成页推荐进入(4)、我的课程(5)、APP外打开(6) | 
|webview | 1 | 1的时候，说明是webview内嵌网页 | 
|token | xxxxx | webview=1的时候，需要传入token | 

<!-- 页面bridge交互说明 -->
## 页面和客户端(app)数据交互
#### 点击“去学习”按钮，h5→app
```
接口：goToAISpokenLearning
参数：暂无
```
