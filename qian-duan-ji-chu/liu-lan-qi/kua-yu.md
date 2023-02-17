---
description: 跨域解决方案
---

# 跨域

## 同源策略

协议+域名+端口有一个不同，则跨域



> 注意：http和https属于不同协议

## 一、CORS

* 服务端配置字段：Access-Control-Allow-\*
* 简单请求、非简单请求：是否会预检

## 二、JSONP

* 声明一个全局回调函数handleResponse(data)
* 动态脚本发起一个请求，参数是全局回调函数：?jsonpCallback=handleResponse
* 服务端返回一个handleResponse(data)的字符串



参考：

* [https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS)
