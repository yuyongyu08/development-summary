---
description: webpack
---

# webpack

核心部分：

* entry
* output
* loader
* plugin

函数注册在webpack的生命周期钩子上，在生成最终文件之前可以对编译的结果做一些特殊的处理，例如模块分包、插入html文件等功能



## 打包优化

源码：

1. 避免引入没有用到的文件/api，减少 tree shaking的时间
2. 避免工具库（例如Element UI）全量引入，减少打包时间
3. 指定文件后缀，缩短查找时间

工具

1. 升级工具和环境版本
2. 通过include、exclude设置loader尽量只对源码编译，排除第三方文件
3. 借助工具合理缓存（例如`cache-loader`）
4. 开启多线程（例如借助thread-loader、HappyPack）





参考：

* [https://jelly.jd.com/article/5f0de6dad5205e015b87c128](https://jelly.jd.com/article/5f0de6dad5205e015b87c128)
* [https://zhuanlan.zhihu.com/p/363928061](https://zhuanlan.zhihu.com/p/363928061)
* [https://segmentfault.com/a/1190000021494964](https://segmentfault.com/a/1190000021494964)
* [https://juejin.cn/post/6984314261354856455](https://juejin.cn/post/6984314261354856455)
