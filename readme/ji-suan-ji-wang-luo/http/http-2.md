---
description: HTTP2
---

# HTTP/2

## 一、HTTP发展历程

* [HTTP/0.9——单行协议](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics\_of\_HTTP/Evolution\_of\_HTTP#http0.9%E2%80%94%E2%80%94%E5%8D%95%E8%A1%8C%E5%8D%8F%E8%AE%AE)
* [HTTP/1.0——构建可扩展性](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics\_of\_HTTP/Evolution\_of\_HTTP#http1.0%E2%80%94%E2%80%94%E6%9E%84%E5%BB%BA%E5%8F%AF%E6%89%A9%E5%B1%95%E6%80%A7)
* [HTTP/1.1——标准化的协议](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics\_of\_HTTP/Evolution\_of\_HTTP#http1.1%E2%80%94%E2%80%94%E6%A0%87%E5%87%86%E5%8C%96%E7%9A%84%E5%8D%8F%E8%AE%AE)
* [超过 15 年的扩展](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics\_of\_HTTP/Evolution\_of\_HTTP#%E8%B6%85%E8%BF%87\_15\_%E5%B9%B4%E7%9A%84%E6%89%A9%E5%B1%95)
* [HTTP/2——为了更优异的表现](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics\_of\_HTTP/Evolution\_of\_HTTP#http2%E2%80%94%E2%80%94%E4%B8%BA%E4%BA%86%E6%9B%B4%E4%BC%98%E5%BC%82%E7%9A%84%E8%A1%A8%E7%8E%B0)
* [后 HTTP/2 进化](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics\_of\_HTTP/Evolution\_of\_HTTP#%E5%90%8E\_http2\_%E8%BF%9B%E5%8C%96)
* [HTTP/3——基于 QUIC 的 HTTP](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics\_of\_HTTP/Evolution\_of\_HTTP#http3%E2%80%94%E2%80%94%E5%9F%BA%E4%BA%8E\_quic\_%E7%9A%84\_http)



## 二、HTTP/1.1有哪些问题？

1、线头阻塞



2、不支持多路复用



3、头部冗余



4、仅支持单向请求





## 三、HTTP/2有哪些改进？

HTTP/1.1与HTTP/2的性能对比：[demo](https://http2.akamai.com/demo)



涉及到的概念：

* 流（Stream）：可以承载一个或多个消息，一个TCP连接上可以有任意数量的流。
* 消息（Message）：一个消息由一个或多个帧组成。一个完整的HTTP请求或响应就是一个消息，同一个HTTP的消息只能在同一个流上发送。
* 帧（Frame）：通信的基本单位。

现实情景类比：

* 物流车 -> 客户端（浏览器）
* 物流仓库 -> 服务器
* 物流车停在物流仓库口 -> 建立的 TCP 连接
* 传送带 -> 流 （可能有多条传送带给物流车提供装卸服务）
* 传送带上的包裹 -> 消息 （如果是卸货则就request消息，如果是装货则就是response消息）
* 包裹里的物品  ->  帧&#x20;



### 1、二进制分帧

HTTP/2将消息划分为两个帧：HEADERS、DATA，并应二进制进行编码；HTTP/1.1采用的是文本格式

<div align="left">

<figure><img src="../../../.gitbook/assets/http2.svg" alt=""><figcaption></figcaption></figure>

</div>

### 2、多路复用

一个TCP可以同时支持多个流存在，这是HTTP/2其他功能和性能优化的基础

<div align="left">

<figure><img src="../../../.gitbook/assets/http2-stream.svg" alt=""><figcaption></figcaption></figure>

</div>

### 3、头部压缩

首次请求后，客户端和服务端会建立一个关于header字段的字典，后续再请求只需传输对应字段的索引即可。

<div align="left">

<figure><img src="../../../.gitbook/assets/http2-header.svg" alt=""><figcaption></figcaption></figure>

</div>

### 4、服务端推送









参考：

* [https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics\_of\_HTTP/Evolution\_of\_HTTP](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics\_of\_HTTP/Evolution\_of\_HTTP)
* [https://juejin.cn/post/6844903734670000142](https://juejin.cn/post/6844903734670000142)
* [https://web.dev/performance-http2/](https://web.dev/performance-http2/)
