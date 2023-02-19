---
description: 块级格式化上下文(Block Formatting Context)
---

# BFC(块级格式化上下文)

### 概念

BFC可以理解成页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。



### 常见形成条件

* 元素左右浮动
* 绝对定位
* display属性为table-cell、table-caption、inline-block
* flex布局
* overflow属性不为visible.

### 作用

* 解决margin折叠问题
* 解决float元素父容器高度塌陷







参见：

* [https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS\_Flow\_Layout/Intro\_to\_formatting\_contexts](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS\_Flow\_Layout/Intro\_to\_formatting\_contexts)
