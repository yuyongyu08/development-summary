---
description: 跨站脚本
---

# XSS

**跨站脚本攻击（Cross-Site Scripting）**

****

### 原理

> 恶意攻击者往 Web 页面里插入恶意可执行网页脚本代码，当用户浏览该页之时，嵌入其中 Web 里面的脚本代码会被执行，从而可以达到攻击者盗取用户信息或其他侵犯用户安全隐私的目的。

### 常见的攻击方法

* 在 HTML 中内嵌的文本中，恶意内容以 script 标签形成注入。
* 在内联的 JavaScript 中，拼接的数据突破了原本的限制（字符串，变量，方法名等）。
* 在标签属性中，恶意内容包含引号，从而突破属性值的限制，注入其他属性或者标签。
* 在标签的 href、src 等属性中，包含 `javascript:` (伪协议)等可执行代码。
* 在 onload、onerror、onclick 等事件中，注入不受控制代码。
* 在 style 属性和标签中，包含类似 `background-image:url("javascript:...");` 的代码（新版本浏览器已经可以防范）。
* 在 style 属性和标签中，包含类似 `expression(...)` 的 CSS 表达式代码（新版本浏览器已经可以防范）。





参考：

* [https://tech.meituan.com/2018/09/27/fe-security.html](https://tech.meituan.com/2018/09/27/fe-security.html)
* [https://juejin.cn/post/6844903781704925191](https://juejin.cn/post/6844903781704925191)
