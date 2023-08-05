# 性能优化

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

[timing模型](https://w3c.github.io/navigation-timing/#processing-model)



### 一、重要指标

* 白屏时间（FC，First Paint）
* 首屏时间（FCP，First Contentful Paint）
* 可操作时间（DOMContentLoaded）：DOM渲染完成，用户可操作
* 页面加载完成时间（window.onload）



### 二、优化阶段

#### 1、资源加载阶段

* 更少：
  * 静态资源合并（雪碧图）
  * 接口请求合并
  * 懒加载（图片、js）
* 更小：
  * 静态资源压缩
*   更快：

    * 浏览器缓存
    * CDN加速



#### 2、页面渲染阶段

* 合理利用\<script>的async和defer属性
* 减少重排操作



#### 3、页面交互阶段

具体问题具体分析

* 防抖、节流









参考：

* [https://juejin.cn/post/6844904020482457613](https://juejin.cn/post/6844904020482457613)
* [https://developer.mozilla.org/zh-CN/docs/Web/API/Performance](https://developer.mozilla.org/zh-CN/docs/Web/API/Performance)

