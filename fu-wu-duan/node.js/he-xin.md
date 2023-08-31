# 核心

## 一、概念

Node.js是**运行环境**，JavaScript是编程语言。使用JavaScript编写的代码可以运行在Node.js中。

Node.js核心特性：

* **异步IO**：
* **事件驱动**：通过事件循环（Event Loop）调度异步任务

## 二、架构

<div align="left">

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Node.js的分层架构</p></figcaption></figure>

</div>

* 应用层：提供了业务开发中直接调用各种模块的API
* 桥：JS可以调用C/C++的关键，可以将JS传入V8，V8解析后交给libuv发起异步I/O
* 底层库：
  * V8：JS的VM
  * libuv：实现异步I/O的关键，提供了跨平台、线程池、事件池等能力
  * C-care：异步处理DNS
  * http-parser、OpenSSL、zlib：http解析、SSL、数据压缩

## 三、事件驱动/事件循环

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>异步IO</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption><p>异步IO的具体过程</p></figcaption></figure>





主线程主要作用：

* 任务的调度
* 对非阻塞任务的执行

工作线程：执行异步任务

## 四、传统服务器与Node.js应对高并发的区别

<figure><img src="../../.gitbook/assets/UML 图 (1).jpg" alt=""><figcaption><p>多线程和单线程的区别</p></figcaption></figure>

* 多线程：Java，PHP或者.net 等经典服务器端语言，用户每一次请求都会为用户创建单独的线程
* 单线程：Node.js仅仅使用一个线程（thread），当有用户连接了，就触发一个内部事件，通过非阻塞I/O、事件驱动机制，让 Node.js 程序宏观上也是并行的

理论上，Node.js对CPU的利用是100%。

> 假如一个线程需要消耗2MB的内存，一个8GB的服务器，**理论上**：
>
> * 多线程：可以支持（8 \* 1024M B）/ 2MB = 4096个连接
> * 单线程：可以支持3万-4万个连接

## 五、单线程弊端&#x20;

弊端：主线程挂掉，整个服务就会挂掉

解决：

* 部署多个节点，借助负载均衡保证服务可用
* 增加进程守护（比如PM2）









参考：

* [https://www.jianshu.com/p/674ed545280d](https://www.jianshu.com/p/674ed545280d)
* [https://mengsixing.github.io/blog/library-node.html](https://mengsixing.github.io/blog/library-node.html)
