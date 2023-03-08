---
description: vite原理
---

# vite

> 以下截图来自于以官方[ Quick Start](https://vuejs.org/guide/quick-start.html#creating-a-vue-application) 的demo

## vite核心

* 本地阶段：使用[esbuild](https://esbuild.github.io/)预编译，没有打包过程
* 生产阶段：使用rollup进行编译打包

## 一、本地启动

本地启动时，主要做两件事情：

### 1、依赖预构建

对依赖（如vue.js、lodash等）进行预构建的目的：

* **模块化兼容**：将CommonJS 或 UMD 风格的依赖项转换为 ESM
* **对依赖进行整合**：将依赖和它自身的依赖整合成一个文件，避免页面加载时产生大量HTTP请求

依赖预构建之后的产物缓存在：node\_modules/.vite/deps，只有一定的触发条件（比如lockfile有变化）才会触发重发预构建。

> 这些依赖属于不常变动的资源，如果需要强制预构建：
>
> 方法1：启动命令加`--force`
>
> 方法2：手动删除node\_modules/.vite文件夹

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

### 2、启动本地服务器

本地服务器主要的作用是

* **响应资源请求**
* **推送修改的资源**：通过websocket将变动的资源推送给客户端，实现热更新

## 二、浏览器加载

### 1、打包后的入口模版

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

### 2、资源加载规则

通过入口文件进行解析，遇到`import`，则会发送一个对应请求，开发服务器返回后继续递归找出其他依赖

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

对于资源的分情况处理：

* 依赖：进行强缓存（通过`cache-control= max-age=31536000,immutable` 进行控制）
* 源码：进行协议缓存（根据`304 Not Modified`）

## 三、热更新

原理类似于webpack的dev-server，只是同步的是没有经过构建打包的源文件。



参考：

* [https://vitejs.dev/](https://vitejs.dev/)
* [https://juejin.cn/post/7064853960636989454](https://juejin.cn/post/7064853960636989454)

