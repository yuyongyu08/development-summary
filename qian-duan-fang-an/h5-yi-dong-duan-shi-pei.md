# H5移动端适配

### 一、flexible方案（废弃）

早期viewport兼容性差，借助[flexible](https://github.com/amfe/lib-flexible)方案（现在官方已不推荐此方案）

### 二、rem +  viewport 方案（推荐）

* 第一步：设置viewport；

```markup
<meta name="viewport" content="width=device-width,initial-scale=1">
```

* 第二步：设置html的font-size

主要原理：通过设计稿和屏幕大小确定缩放比例，然后用缩放比例乘以设计稿基准字体大小，得出网页的基准字体大小

```javascript
// 设置基准大小
const baseSize = 32
function setRem () {
  // 当前页面宽度相对于 750 宽的缩放比例
  const scale = document.documentElement.clientWidth / 750
  document.documentElement.style.fontSize = (baseSize * Math.min(scale, 2)) + 'px'
}
// 初始化
setRem()
window.onresize = function () {
  setRem()
}
```

* 第三步：借助插件将单位px转成rem

postcss-pxtorem



### 三、vw +  viewport 方案

设置viewport；尺寸单位借助插件转为vw（view width），此单位以设备宽度的1/100为基准



### 总结：

rem相比于vw方案最的优点：参照物可以修改。

即rm可以人为改动根元素的font-size；vw方案无法改动设备的vw



参考：

* [https://juejin.cn/post/6953091677838344199](https://juejin.cn/post/6953091677838344199)
* [https://juejin.cn/post/7085931616136069156](https://juejin.cn/post/7085931616136069156)
* [https://cloud.tencent.com/developer/article/2020264](https://cloud.tencent.com/developer/article/2020264)



