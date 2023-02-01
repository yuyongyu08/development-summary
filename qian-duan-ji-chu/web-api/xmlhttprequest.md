---
description: 使用XMLHttpRequest实现一个Ajax（Asynchronous JavaScript And XML）
---

# XMLHttpRequest

### 第一步：获取实例

```javascript
let xhr;
if(window.XMLHttpRequest){
    xhr = new XMLHttpRequest();
}else{
    xhr = new ActiveXObject('Microsoft.XMLHTTP');
}
```

### 第二步：发送请求

* **初始化请求：**

```
xhr.open(method, url, async, user, password)
```

async默认为true，Ajax存在的意义就是发异步请求，所以第三个参数可以默认不传。

* **发送参数：**

<pre><code><strong>xhr.send(body)
</strong></code></pre>

特别注意的是： 如果发送`POST`请求，请使用`setRequestHeader()`来添加 `HTTP`请求头，并在`send()`方法中传递要发送的数据：

```javascript
xhr.open("POST","ajax_test.html",true); 
xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded"); 
xhr.send("fname=Henry&lname=Ford");
```

### 第三步：处理返回结果

* 使用`onreadystatechange`事件监听状态变化

```javascript
xmlhttp.onreadystatechange = function () {
    // todo
}
```

*   使用`xhr.readyState`判断请求状态，状态值含义：

    `0`: 表示请求未初始化，还没有调用 `open()`

    `1`: 服务器连接已建立，但是还没有调用 `send()`

    `2`: 请求已接收，正在处理中（通常现在可以从响应中获取内容头）

    `3`: 请求处理中，通常响应中已有部分数据可用了，没有全部完成

    `4`: **`请求已完成；此阶段确认全部数据都已经解析完毕，可以通过异步对象的属性获取对应数据`**


* 使用`xhr.state`判断http状态

表示成功的http状态码有`xmlhttp.status >= 200 && xmlhttp.status < 300 || xmlhttp.status == 304`

* 使用`xhr.response`作为请求结果返回



### 简约版

```javascript
function myAjax(option = { method: "get", url: "", param: {}, onSuccess: (data) => {}, onError: (err) => {} }) {
  const { method, url, param } = option;

  const xhr = new XMLHttpRequest();

  xhr.open(method, url);
  xhr.send(param);

  xhr.onreadystatechange = function () {
    if (xhr.readyState === 4) {
      if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304) {
        onSuccess(xhr.response);
      } else {
        onError("请求失败！");
      }
    }
  };
}
```



参考：

* [https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)
