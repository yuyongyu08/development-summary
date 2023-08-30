---
description: 模块打包器-前端工程化里程碑式的工具
---

# webpack

## 核心部分

* Entry
* Loader（真正干活的主力）

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

* Plugin（干预构建过程的钩子）
* Output



## 构建过程

分为3个大的阶段：

1. 初始化阶段：读取配置文件中的option参数，并做合并（merge）
2. 编译构建阶段：
   1. 从Entry出发，构建依赖图谱
   2. 对于每一个Module（被依赖的文件），按照文件类型调用相应的Loader去编译文件内容
   3. 串行处理每一个Module，递归地处理完所有依赖
3. 输出阶段：对编译后的模块进行组合，生成chunk，并转换成文件，输出到Output指定的位置



编译原理3阶段：

* 解析阶段：生成AST
* 转译阶段：将AST安装插件提供的规则转成目标产物
* 生成阶段：将目标产物处理生成指定文件





## 核心功能

* code spliting
* tree shaking
* dev server
* HMR
* module federation（模块联邦，跨应用模块共享）&#x20;

## 打包优化

源码：

1. 避免引入没有用到的文件/api，减少 tree shaking的时间
2. 工具库（例如Element UI）按需引入，减少打包时间
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
