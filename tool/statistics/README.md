<!-- 模块大标题 -->
# 网页中添加神策统计
<!-- 模块说明 -->
包含了网页中如何加入神策统计，以及如何使用神策进行统计的说明


<!-- 如何将神策统计嵌入项目中 -->
### 在dom内添加点击事件
v-sa-click="['englishDetailsDownload']"
v-sa-click="['liveOrderPay', { source: 1 }]

### 在js逻辑内添加点击事件
this.$sa.track('englishPay');
this.$sa.track('liveOrderPay', { source: 1 });