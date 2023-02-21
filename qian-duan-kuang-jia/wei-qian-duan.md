---
description: qiankun原理
---

# 微前端

### 主要原理

监听路由变化，动态装载、销毁子应用



### 主要架构

* 基座：负责子应用的注册、卸载、通信
* 子应用



### 核心技术点

*   JS隔离

    * 代理沙箱（Proxy Sandbox）

    它将window上的所有属性遍历拷贝生成一个新的fakeWindow对象，紧接着使用proxy代理这个fakeWindow，用户对window操作全部被拦截下来，只作用于在这个fakeWindow之上

    * 快照（Snapshot Sandbox）沙箱：

    用两个对象变量`windowSnapshot`和`modifyPropsMap` ，分别存储子应用挂载前原始`window`对象上的全部属性以及子应卸载时被其修改过的`window`对象上的相关属性

    * 遗留沙箱（Legacy Sandbox）
* CSS隔离（都没有完美解决弹窗挂在到body下的问题，解决方法：子应用自行隔离）
  * shadow DOM
  * Scoped CSS



### 通信方式

基座 <=>子应用，发布订阅模式实现

* onGlobalStateChange()
* setGlobalState()
* offGlobalStateChange()



### qiankun VS single-spa

| 优化点     | single-spa                | qiankun            |
| ------- | ------------------------- | ------------------ |
| 子应用加载方式 | 用户自行配置子应用的加载方式和具体资源       | 用户仅配置子应用入口         |
| 应用间的隔离  | 无隔离机制                     | 内置了JS和CSS隔离        |
| 应用间的通信  | 基座通过customProps向子应用传递静态参数 | 基座和子应用通过发布订阅进行信息通信 |







参考：

* [https://juejin.cn/post/7184419253087535165](https://juejin.cn/post/7184419253087535165)
* [https://juejin.cn/post/7197608023429922871](https://juejin.cn/post/7197608023429922871)
