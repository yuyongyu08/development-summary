---
description: ESM和CommonJS共存如何打包
---

# 打包ESM和CommonJS

ESM和CommonJS混用

[https://juejin.cn/post/6844904114183208968?from=search-suggest](https://juejin.cn/post/6844904114183208968?from=search-suggest)



对于`es6`规范和`commonjs`规范来说，经过`babel`编译以后，都会转化成`commonjs`规范，然后在此基础上，用`__esModule`区分了是属于`es6`模块还是`commonjs`模块。

并切为了保证`es6`规范用`import`导入值的正确性和统一性，`babel`还做了一些策略去处理这两者之前的差异。\






参考：

* [https://nodejs.org/api/modules.html#modules\_all\_together](https://nodejs.org/api/modules.html#modules\_all\_together)
