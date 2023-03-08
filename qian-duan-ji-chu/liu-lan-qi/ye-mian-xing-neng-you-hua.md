# 性能优化

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

[timing模型](https://w3c.github.io/navigation-timing/#processing-model)



重要指标：

* 白屏时间：（FC，First Paint），
* 首屏时间：（FCP，First Contentful Paint）
* 可操作时间：DOMContentLoaded
* 页面加载完成时间：window.onload



通用方案：

* 更少：
  * 静态资源合并（雪碧图）
  * 接口请求合并
  * 防抖、节流
  * 懒加载（图片、js）
* 更小：
  * 静态资源压缩
  * 动态加载
*   更快：

    * CDN加速



参考：

* [https://juejin.cn/post/6844904020482457613](https://juejin.cn/post/6844904020482457613)
* [https://developer.mozilla.org/zh-CN/docs/Web/API/Performance](https://developer.mozilla.org/zh-CN/docs/Web/API/Performance)
*
