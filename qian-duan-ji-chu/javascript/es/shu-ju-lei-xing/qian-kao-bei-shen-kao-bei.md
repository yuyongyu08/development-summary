# 浅拷贝、深拷贝

## 一、浅拷贝

### 方式1：直接赋值



### 方式2：Object.assign()







## 二、深拷贝

### 方式1：手动实现

###

### 方式2：借助JSON

<pre class="language-javascript"><code class="lang-javascript"><strong>const copy = JSON.parse(JSON.stringify(source));
</strong></code></pre>

```
弊端：会抛弃对象的constructor
适用：能够被json直接表示的数据结构（对象中只包含number、string、boolean、array、扁平对象）
不适用：含有function、regexp的数据结构
```

### 方式3：借助第三方工具库

* loash：\_.cloneDeep
* jquery：$.extend







参考：

* [https://juejin.cn/post/6844904197595332622](https://juejin.cn/post/6844904197595332622)
* [https://segmentfault.com/a/1190000020255831](https://segmentfault.com/a/1190000020255831)

