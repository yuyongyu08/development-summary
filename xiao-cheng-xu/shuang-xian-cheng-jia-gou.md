# 双线程架构

<figure><img src="../.gitbook/assets/mp-struct.png" alt=""><figcaption><p>微信小程序双线程架构图</p></figcaption></figure>

#### 1、什么是微信小程序双线程架构？

小程序框架系统分为两部分：**逻辑层**（App Service）和 **视图层**（View）

小程序的渲染层和逻辑层分别由2个线程管理：

* 渲染层：使用了WebView 进行渲染；每个页面对应一个WebView（这也是为什么小程序页面切换流畅度接近原生的原因，同时也限定了小程序的页面不宜过多）
* 逻辑层：采用 JsCore 线程运行 JS 脚本

这两个线程的通信会经由微信客户端做中转。



#### 2、微信小程序为什么采用双线程架构？

**产品定位**决定了**技术目标**，继而决定了**系统架构**

| 产品定位      | 技术目标 | 系统架构                         |
| --------- | ---- | ---------------------------- |
| 运行在微信App中 | 安全   | 逻辑层不可直接操作视图，两者通信由宿主（微信客户端）中转 |
| 体验接近原生应用  | 高效   | 视图层每个页面都是一个单独的webview        |



#### 3、双线程下微信小程序的界面是如何渲染的？ <a href="#3-1-4" id="3-1-4"></a>

在渲染层，宿主环境会把WXML转化成对应的JS对象，在逻辑层发生数据变更的时候，我们需要通过宿主环境提供的setData方法把数据从逻辑层传递到渲染层，再经过对比前后差异，把差异应用在原来的DOM树上，渲染出正确的UI界面

<figure><img src="../.gitbook/assets/mp-msg.png" alt=""><figcaption><p>微信小程序页面渲染</p></figcaption></figure>

#### 4、渲染层和逻辑层是如何通信的？

<figure><img src="../.gitbook/assets/mp-tx.png" alt=""><figcaption><p>渲染层和逻辑层通信过程</p></figcaption></figure>

渲染层和逻辑层的通信通过**事件驱动**的方式由**微信客户端进行中转。**具体方式：

1. 用户通过视图层的交互触发特定的事件 event
2. 然后 event 通过 native 中转传递给逻辑层
3. 逻辑层继而通过一系列的逻辑处理、数据请求、接口调用等行为，将所需要的数据 data 加工好
4. 数据 data 通过 native 中转传递给渲染层
5. 最后渲染层将 data 渲染为可视化的 UI（先进行数据diff，然后将差异进行渲染）

#### 5、微信小程序的运行环境

| 运行环境                 | 渲染层              | 逻辑层                       |
| -------------------- | ---------------- | ------------------------- |
| iOS、iPadOS 和 Mac OS  | WKWebView        | JavaScriptCore            |
| Android              | XWeb             | v8                        |
| Windows              | Chromium 内核      | Chromium 内核               |
| 开发工具上                | Chromium Webview | [NW.js](https://nwjs.io/) |



参考：

* [https://cloud.tencent.com/developer/article/1826156](https://cloud.tencent.com/developer/article/1826156)
* [https://developers.weixin.qq.com/ebook?action=get\_post\_info\&volumn=1\&lang=zh\_CN\&book=miniprogram\&docid=0006a2289c8bb0bb0086ee8c056c0a](https://developers.weixin.qq.com/ebook?action=get\_post\_info\&volumn=1\&lang=zh\_CN\&book=miniprogram\&docid=0006a2289c8bb0bb0086ee8c056c0a)
* [https://developers.weixin.qq.com/ebook?action=get\_post\_info\&volumn=1\&lang=zh\_CN\&book=miniprogram\&docid=0000286f908988db00866b85f5640a](https://developers.weixin.qq.com/ebook?action=get\_post\_info\&volumn=1\&lang=zh\_CN\&book=miniprogram\&docid=0000286f908988db00866b85f5640a)
* [https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/framework.html](https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/framework.html)

