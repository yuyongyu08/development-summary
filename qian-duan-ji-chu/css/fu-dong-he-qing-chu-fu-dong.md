---
description: float
---

# 浮动和清除浮动

## 一、浮动

{% embed url="https://codepen.io/yuyy/full/WNgQMBp" %}

**要点：**

1. 元素的水平方向浮动，意味着元素只能左右移动而不能上下移动。
2. 一个浮动元素会尽量向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止，比如示例的float-left-2、float-right-1
3. 浮动元素之后的元素将围绕它，比如示例的\<p>
4. 浮动元素之前的元素将不会受到影响，比如示例的\<h1>

<mark style="color:red;"></mark>

## **二、浮动元素引起的问题**

* 高度塌陷：父元素的高度无法被撑开，影响与父元素同级的元素
* 与浮动元素同级的非浮动元素会跟随其后
* 若浮动的元素不是第一个元素，则该元素之前的元素也要浮动，否则会影响页面的显示结构

## 三、清除浮动

元素浮动之后，周围的元素会重新排列，为了避免这种情况，使用 clear 属性。

注意观察上面示例\<p>上clear属性为left和right的不同变化







参考：

* [https://www.runoob.com/css/css-float.html](https://www.runoob.com/css/css-float.html)
* [https://developer.mozilla.org/zh-CN/docs/Web/CSS/float](https://developer.mozilla.org/zh-CN/docs/Web/CSS/float)
* [https://juejin.cn/post/6844903519040831496](https://juejin.cn/post/6844903519040831496)
