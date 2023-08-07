---
description: 块级格式化上下文(Block Formatting Context)
---

# BFC(块级格式化上下文)

### 概念

BFC是一个独立的布局环境，可以理解为一个容器，在这个容器中按照一定规则进行物品摆放，并且不会影响容器外的元素摆放。如果一个元素符合触发BFC的条件，则BFC中的元素布局不受外部影响。



### 常见形成条件

* 左右浮动
* 绝对定位
* flex布局
* display属性为table-cell、table-caption、inline-block
* overflow属性不为visible.

### 特点

* 相邻的两个BFC的margin不会重叠
* BFC的高度包含内部浮动元素的高度

### 应用

* 解决margin折叠问题：将其中一个元素构造成BFC
* 解决float元素父容器高度塌陷：将父元素构造成BFC



参见：

* [https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS\_Flow\_Layout/Intro\_to\_formatting\_contexts](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS\_Flow\_Layout/Intro\_to\_formatting\_contexts)
