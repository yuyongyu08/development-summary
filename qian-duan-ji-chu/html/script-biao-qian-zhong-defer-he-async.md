# script标签中defer和async

<figure><img src="../../.gitbook/assets/async-defer.png" alt=""><figcaption><p>async VS defer</p></figcaption></figure>

### 概述

async：异步下载，下载完立即执行（完全独立的脚本，DOM 和其他脚本不会等待它们，它们也不会等待其它的东西）

defer：异步下载，等页面解析完后再执行

### 两者区别

* 对页面解析的影响：async由于下载完成就执行**会**阻塞页面解析；defer**不会**阻塞页面解析
* 执行顺序：多个带async属性的脚本的**执行顺序随机**，取决于各自下载完成的事件；多个带defer属性的脚本则严格按照各自出现在文档的先后**顺序执行**
* `DOMContentLoaded` ：async和`DOMContentLoaded` 事件不会彼此等待，不能保证谁先谁后；defer在 `DOMContentLoaded` 事件之前执行

### 与动态脚本关系

```javascript
let script = document.createElement('script');
script.src = "/article/script-async-defer/long.js";
document.body.append(script);
```

默认情况下，动态脚本的行为是**异步**的，相当于async。如果像达到defer的效果，可以显式地设置 `script.async=false`。

### 应用场景

* async：不依赖当前页面的第三方脚本，比如数据统计、广告等
* defer：严格控制脚本的执行顺序，比如先加载基础库文件再加载业务文件

### 延伸：页面生命周期

* DOMContentLoaded：DOM准备完毕时触发
* window.onload：页面所有资源加载完成时触发
* window.onbeforeunload：用户想要离开时触发，常用于用户未保存提示
* window.onunload：用户最终离开时触发

`document.readyState` 是文档的当前状态，可以使用`readystatechange`事件监听状态变化：

```javascript
document.addEventListener("readystatechange", () => {
    switch (true) {
      case document.readyState === "loading":
        console.log("文档加载中");
        break;
      case document.readyState === "interactive":
        console.log("文档已被解析完成，与 DOMContentLoaded 几乎同时发生，但是在 DOMContentLoaded 之前发生");
        break;
      case document.readyState === "complete":
        console.log("文档加载中，文档和资源均已加载完成，与 window.onload 几乎同时发生，但是在 window.onload 之前发生");
        break;
      default:
        break;
    }
  });
```

tips：XMLHttpRequest中也有个`onreadystatechange`事件。



参考：

* [https://zh.javascript.info/script-async-defer](https://zh.javascript.info/script-async-defer)
* [https://zh.javascript.info/onload-ondomcontentloaded](https://zh.javascript.info/onload-ondomcontentloaded)
