# DOM事件

## 一、DOM级别

即DOM的版本：

* DOM0级：未被W3C标准化之前
* DOM1级：成为W3C标准，两个核心模块：DOM Core和DOM HTML
* DOM2级：为DOM节点添加了更多方法和属性
* DOM3级：增加了XPath模块、加载和保存（DOM Load and Save）模块等

## 二、DOM事件级别

DOM事件分为3个级别：

* DOM0级事件
* DOM2级事件
* DOM3级事件

> 由于DOM1级中没有事件的相关内容，所以没有DOM1级事件。

### 1、DOM0级事件

<pre class="language-html"><code class="lang-html">&#x3C;button id="btn" type="button">&#x3C;/button> 
 
var btn = document.getElementById('btn')
<strong>
</strong>// DOM0级事件新建：将一个函数赋值给了一个事件处理属性(例如onclick)
<strong>btn.onclick = function() { 
</strong>    console.log('Hello World')
}

// DOM0级事件解绑：通过给事件处理属性赋值null。
btn.onclick = null;
</code></pre>

### 2、DOM2级事件

DOM2事件主要包括：

* 新增了事件API：&#x20;
  * [addEventListener(eventName, fn, useCapture) ](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
  * [removeEventListener (eventName, fn, useCapture) ](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener)
* 支持绑定多个事件处理函数

```html
<button id="btn" type="button"></button> 
 
var btn = document.getElementById('btn')
function showFn() { 
    alert('Hello World')
}
function LogFn() { 
    alert('Hello World')
}
// 同时绑定多个事件处理函数
btn.addEventListener('click', showFn);
btn.addEventListener('click', LogFn);

// 解绑事件 
btn.removeEventListener('click', showFn); 
```

### 3、DOM3级事件

DOM3级事件核心：

* 新增了更多事件类型（文本事件、焦点事件等）
* 支持自定义事件

自定义事件：

```javascript
var event = new Event('build');

// 监听事件
elem.addEventListener('build', function (e) { ... }, false);

// 触发事件
elem.dispatchEvent(event);

```

要向事件对象添加更多数据，可以使用 [CustomEvent](https://developer.mozilla.org/zh-CN/docs/Web/API/CustomEvent) 接口，detail 属性可用于传递自定义数据。 例如：

```javascript
var event = new CustomEvent('build', { bubbles: true, detail: elem.dataset.time });
```

## 三、DOM事件模型

DOM2级事件规定事件流包括3个阶段：

* 捕获阶段
* 目标阶段
* 冒泡阶段

代码验证：

{% embed url="https://codepen.io/yuyy/full/OJorrzb" %}

点击最内层的div时，输出结果：

```
爷级捕获
父级捕获 
子级捕获 
子级冒泡
父级冒泡 
爷级冒泡
```



## 四、event.target、event.currentTarget、this

{% embed url="https://codepen.io/yuyy/full/YzOddjX" %}

结论：

```javascript
father.addEventListener('click', function(event){
  // event.target：触发事件的元素（罪魁祸首）
  // event.currentTarget：事件发生所在的元素
  // this：绑定事件的元素，始终指向 event.currentTarget。注意如果用this时不要用箭头函数！！！
}, false);
```

**`event.target`  **<mark style="color:red;">**不一定等于**</mark>**  `event.currentTarget`    **<mark style="color:green;">**一定等于**</mark>**  `this`**



参考：

* [https://zh.javascript.info/events](https://zh.javascript.info/events)
* [https://juejin.cn/post/6984357222427918372](https://juejin.cn/post/6984357222427918372)
