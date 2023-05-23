# Node.js

## 一、概念

Node.js是**运行环境**，JavaScript是编程语言。使用JavaScript编写的代码可以运行在Node.js中。

## 二、架构

<div align="left">

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

</div>

## 三、事件驱动/事件循环

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

主线程主要作用：

* 任务的调度
* 对非阻塞任务的执行

工作线程：执行异步任务

## 四、传统服务器与Node.js应对高并发的区别？

<figure><img src="../.gitbook/assets/UML 图 (1).jpg" alt=""><figcaption></figcaption></figure>

理论上，Node.js对CPU的利用是100%。



## 五、单线程弊端

弊端：主线程挂掉，整个服务就会挂掉

解决：

* 部署多个节点，借助负载均衡保证服务可用
* 增加进程守护（比如PM2）









参考：

* [https://www.jianshu.com/p/674ed545280d](https://www.jianshu.com/p/674ed545280d)
