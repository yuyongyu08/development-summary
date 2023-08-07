---
description: 跨域解决方案
---

# 跨域

## 同源策略

协议+域名+端口有一个不同，则跨域

> 注意：http和https属于不同协议，所以也会跨域

## 一、CORS

* 服务端配置字段：<mark style="color:red;">Access-Control-Allow-</mark>\*
  * Access-Control-Allow-Origin
  * Access-Control-Allow-Methods
  * Access-Control-Allow-Headers
* 简单请求、非简单请求：是否会预检（OPTIONS）
* 是否允许携带cookie：Access-Control-Allow-<mark style="color:red;">Credentials</mark>

## 二、JSONP

* 声明一个全局回调函数handleResponse(data)
* 动态脚本发起一个请求，参数是全局回调函数：?jsonpCallback=handleResponse
* 服务端返回一个handleResponse(data)的字符串
* 客户端拿到字符串进行执行

## 三、反向代理

* 增加一个代理服务器（nginx）
* 将所有的请求都代理到此服务器上
* 此代理服务器内部做服务分发

参考：

* [https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS)
