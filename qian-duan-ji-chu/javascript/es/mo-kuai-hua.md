# 模块化

## 一、模块化规范

<table><thead><tr><th width="141">规范</th><th width="152">导出（定义）</th><th>导入（引用）</th><th>代表（实现）</th><th>加载方式</th><th>使用环境</th></tr></thead><tbody><tr><td>CommonJS</td><td>module.exports/exports</td><td>require</td><td>Node.js</td><td>同步，动态（运行时）</td><td>服务器、桌面</td></tr><tr><td>AMD</td><td>define</td><td>require</td><td>RequireJS</td><td>异步</td><td>浏览器</td></tr><tr><td>CMD</td><td>define</td><td>require</td><td>Sea.js</td><td>异步</td><td>浏览器</td></tr><tr><td>ES6 Module</td><td>export/export default</td><td>import from</td><td>-</td><td>同步，静态（编译时）</td><td>服务器、浏览器（需要转译才支持）</td></tr></tbody></table>



## 二、CommonJS 与ES6 Module的区别

### 1、语法

* CommonJS：
  * 导出：module.exports/exports
  * 导入：require
* ES6 Module：
  * 导出：export（default）
  * 导入：
    * import..from…
    * import()：新提案，动态导入新提案，适用场景：按需加载，条件加载，模块路径变量

### 2、运行环境

原生支持，无需编译的情况下：

* CommonJS：服务器
* ES6 Module：浏览器

### 3、加载方式

* CommonJS：动态加载（运行时加载）
* ES6 Module：静态加载（编译时加载；必须先于其他语句执行，只能模块顶层，不可放到if语句中）

### 4、变量

* CommonJS：值拷贝（不会变）
* ES6 Module：值引用（会变，<mark style="color:red;">**单例**</mark>）

### 5、是否可修改

* CommonJS：可修改
* ES6 Module：不可修改（因为是值引用，如果修改，会引起其他模块的运行时拿到的不再是期望值）

\


参考：

* [https://www.cnblogs.com/lvdabao/p/js-modules-develop.html](https://www.cnblogs.com/lvdabao/p/js-modules-develop.html)
* [ES6模块](https://es6.ruanyifeng.com/#docs/module-loader)
* CommonJS规范：[http://javascript.ruanyifeng.com/nodejs/module.html](http://javascript.ruanyifeng.com/nodejs/module.html)

