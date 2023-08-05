# 错误上报

## 一、JS运行时错误

### 方式1：window.onerror（推荐）

含有详细的error堆栈信息

```javascript
window.onerror = function (msg, url, lineNo, columnNo, error) {
    // 处理错误信息
}
```

### 方式2：window.addEventListener('error', event => {})

```javascript
window.addEventListener('error', event => (){ 
  // 处理错误信息
}, false);
```

## 二、资源加载错误

使用window.addEventListener('error', event => {})，但要限制错误类型：

```javascript
window.addEventListener('error', event => (){ 
  // 过滤js error
  let target = event.target || event.srcElement;
  let isElementTarget = target instanceof HTMLScriptElement || target instanceof HTMLLinkElement || target instanceof HTMLImageElement;
  if (!isElementTarget) return false;
  // 上报资源地址
  let url = target.src || target.href;
  console.log(url);
}, true);
```



## 三、未处理的Promise错误

使用`unhandledrejection`事件监听处理

```javascript
window.addEventListener("unhandledrejection", event => {
  console.warn(`UNHANDLED PROMISE REJECTION: ${event.reason}`);
});
```

## 四、异步请求（fetch、xhr）错误

对两个API封装时增加错误捕获：

* fetch：在then后面增加catch
* xhr：增加xhr上的`error`事件监听

## 五、框架

* vue：`app.config.errorHandler`
* react：`componentDidCatch`

## 六、script error

跨域错误，请求第三方域名下的脚本可能发生错误，浏览器处于安全考虑隐藏了具体的错误信息。

如果想拿到具体的信息，解决方法：

**方法1:**

\<script>上添加 crossorigin="anonymous" 属性

```javascript
<script src="http://another-domain.com/app.js" crossorigin="anonymous"></script>
```

**方法2:**

如果第三方资源是通过JS动态加载的，使用`try...catch`包裹用于加载的代码块





参考：

* [https://cloud.tencent.com/developer/article/1460542](https://cloud.tencent.com/developer/article/1460542)
