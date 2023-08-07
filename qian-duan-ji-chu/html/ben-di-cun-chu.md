---
description: cookie、localStorage、sessionStorage
---

# 本地存储

### Cookie

cookie的出现主要是解决http无状态带来的一些问题

**主要特征：**

* 服务器生成，存储在客户端
* 每次的请求会默认携带上同源的cookie
* 过期时间可以设置



**重要参数：**

1. domain：cookie所属的域名
2. path：页面级别的访问限制，如果设置了path，只有同域同页面下的cookie才共享
3. expires：具体的过期时间点，逐渐废弃，由max-age代替
4. max-age：过期时间段，以秒为单位
   * 负数：会话结束即失效
   * 0：删除cookie
   * 正数：n秒后失效
5. secure：只能被 HTTPS 协议加密过的请求发送给服务端
6. httpOnly：拒绝http携带之外的方式访问，比如通过JavaScript脚本无法访问
7. sameSite：请求的url和当前页面url不一致时是否允许携带cookie，防止[CSRF](../../readme/ji-suan-ji-wang-luo/chang-jian-wang-luo-gong-ji/csrf.md)攻击



### Storage

api:

```javascript
// 保存数据到 Storage
Storage.setItem('key', 'value');

// 从 Storage 获取数据
let data = Storage.getItem('key');

// 从 sessionStorage 删除保存的数据
Storage.removeItem('key');

// 从 Storage 删除所有保存的数据
Storage.clear();
```

#### localStorage

1. 数据长期存储，没有过期时间，只能用户手动清除
2. 各个tab页间数据共享，注意数据一致性的问题

#### sessionStorage

1. 页面会话在浏览器打开期间一直保持，并且重新加载或恢复页面仍会保持原来的页面会话。
2. **通过脚本，在新标签或窗口打开一个页面时会**<mark style="color:red;">**复制**</mark>**顶级浏览会话的上下文作为新会话的上下文**
3. 打开多个相同的 URL 的 Tabs 页面，会创建各自的 `sessionStorage`。
4. 关闭对应浏览器标签或窗口，会清除对应的 `sessionStorage`。

#### <mark style="color:red;">如何理解第2点？</mark>

**父页面：**

{% embed url="https://codepen.io/yuyy/full/QWBozmP" %}

**子页面：**

{% embed url="https://codepen.io/yuyy/full/LYBaMJL" %}

演示步骤：

第1步：跳转到子页面

*   通过\<a>标签的方式跳转到子页面，子页面的控制台输出：`parent_1:null`


* 通过window.open的方式跳转到子页面，子页面的控制台输出：`parent_1:123`

第2步：点击父页面`新增sessionStorage`按钮，然后点击各个子页面的`获取新sessionStorage`按钮

* 通过\<a>标签的方式跳转到子页面，子页面的控制台输出：`parent_2:null`
* 通过window.open的方式跳转到子页面，子页面的控制台输出：`parent_2:456`



**总结：**

* **通过\<a>标签方式打开的子页面和父级页面完全独立，`sessionStorage`始终不共享**
* **通过window.open方式打开的子页面会复制父页面的`sessionStorage`，父级页面后续更新的`sessionStorage`和子级页面共享同步**









参考：

* [https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Cookies](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Cookies)
* [https://developer.mozilla.org/zh-CN/docs/Web/API/Document/cookie](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/cookie)
* [https://developer.mozilla.org/zh-CN/docs/Web/API/Web\_Storage\_API/Using\_the\_Web\_Storage\_API](https://developer.mozilla.org/zh-CN/docs/Web/API/Web\_Storage\_API/Using\_the\_Web\_Storage\_API)

