---
description: qiankun原理
---

# Qiankun

### 一、主要原理

通过监听路由变化，动态装载、销毁子应用。

qiankun是对[single-spa](https://single-spa.js.org/)的封装，在其基础上主要做了两方面的扩展

* **子应用的加载方式**：只需配置子应用入口，自动解析并加载其资源
* **沙箱隔离**：对JS和样式都提供了隔离机制

### 二、主要架构

* 基座：负责子应用的注册、卸载、通信
* 子应用

### 三、核心技术点

#### 1、子应用加载

借助import-html-entry从子应用的首页解析出对应的资源进行请求，无需用户手动配置。

#### 2、JS隔离

1. **代理沙箱（Proxy Sandbox）**

它将window上的所有属性遍历拷贝生成一个新的fakeWindow对象，紧接着使用proxy代理这个fakeWindow，用户对window操作全部被拦截下来，只作用于在这个fakeWindow之上。每个子应用分配一个fakeWindow。

2. **快照沙箱（Snapshot Sandbox）**

* windowSnapshot： window对象的浅拷贝
* modifyPropsMap ：存储子应用的修改

子应用mount时，先将window存储到快照windowSnapshot上，然后将子应用之前的修改modifyPropsMap（如果有的话）应用到window上；

子应用unmount时，先将当前window和快照windowSnapshot做diff，将diff结果存储到modifyPropsMap上，然后用快照windowSnapshot恢复window；

3. **遗留沙箱（Legacy Sandbox）**

#### 3、CSS隔离

（都没有完美解决弹窗挂在到body下的问题，解决方法：子应用自行隔离）

* shadow DOM
* Scoped CSS



### 四、通信方式

基座 <=>子应用，发布订阅模式实现

* onGlobalStateChange()
* setGlobalState()
* offGlobalStateChange()



### 五、qiankun VS single-spa

| 优化点     | single-spa                | qiankun            |
| ------- | ------------------------- | ------------------ |
| 子应用加载方式 | 用户自行配置子应用的加载方式和具体资源       | 用户仅配置子应用入口         |
| 应用间的隔离  | 无隔离机制                     | 内置了JS和CSS隔离        |
| 应用间的通信  | 基座通过customProps向子应用传递静态参数 | 基座和子应用通过发布订阅进行信息通信 |



### 六、实践中的注意点

1.本地调试

接入多个子应用时，将需要调试的那个子应用本地启动，接入链接设置成本地url，其他设置成dev环境。可以考虑用vite的env来管理接入链接。



2.样式隔离

自身提供的两种隔离方案（shadowDOM、类Scoped CSS），无法解决一些特定场景，比如一些第三方库将弹窗等挂载到子应用根结点外（一般都是body下），弹窗内的样式没法从架构层面做隔离。



3.共享依赖

比较难抽取，尤其是各个子应用依赖的同一个第三方资源的版本再有区别的话，更增加了资源抽离的难度



参考：

* [https://qiankun.umijs.org/zh](https://qiankun.umijs.org/zh)
* [https://single-spa.js.org/](https://single-spa.js.org/)
* 样式隔离问题：[https://juejin.cn/post/7184419253087535165](https://juejin.cn/post/7184419253087535165)
* [https://juejin.cn/post/7197608023429922871](https://juejin.cn/post/7197608023429922871)
* [https://juejin.cn/post/7148075486403362846](https://juejin.cn/post/7148075486403362846)
