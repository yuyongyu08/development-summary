---
description: 跨站请求伪造
---

# CSRF

跨站请求伪造（Cross Site Request Forgery）

### 原理

假如攻击者想让你给她的idol在新浪微博投票。

第一步：假如你新浪微博网页版是登录状态

第二步：通过邮件等方式诱导你点击第三方网站的链接

链接打开后页面如下：

```html
<body style="display: none;">
    <form target="myIframe" id="csrf" action="新浪投票接口" method="POST">
        <input type="text" name="content" value="csrf攻击" />
    </form>

    <!-- iframe 用来防止页面跳转 -->
    <iframe id="myIframe" name="myIframe"></iframe>

    <script>
        var form = document.querySelector('#csrf');
        form.submit();
    </script>
</body>
```

第三步：页面打开后，自动发送携带新浪cookie的投票接口，新浪服务器验证cookie合法，接口请求成功

一次CSRF攻击成功完成～

### 特点

* 攻击发生在第三方网站，而不是被攻击网站
* 攻击是利用受害者在被攻击网站的登录凭证，冒充受害者提交操作，仅仅是“冒用”，而不是直接窃取数据。
* 攻击者预测出被攻击的网站接口的所有参数，成功伪造请求

### 防御

* Cookie 设置 SameSite 属性
* 服务器校验请求头的referer
* 将Token作为请求参数在服务器端校验







参考：

* [https://juejin.cn/post/6844903681591083015](https://juejin.cn/post/6844903681591083015)
* [https://juejin.cn/post/6844904004288249870](https://juejin.cn/post/6844904004288249870)
