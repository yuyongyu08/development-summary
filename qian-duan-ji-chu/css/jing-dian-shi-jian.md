---
description: 常见图形、文本溢出等
---

# 经典实践

### 一、三角形

{% embed url="https://codepen.io/yuyy/full/oNPXGoV" %}

思路：

* 宽高都设置成0
* border设置成透明，边框粗细即时三角形的边长
* 把要显示的边进行边框重置



### 二、文本溢出

#### 单行：

{% embed url="https://codepen.io/yuyy/live/xxaGPZv" %}

要点：

* 定宽
* 不换行
* 超出隐藏
* 文本末尾加省略号

#### 多行：

{% embed url="https://codepen.io/yuyy/full/RwYPjoo" %}

### 三、判断元素是否到达可视区域

#### 方式一：高度计算

原理：元素距离文档顶部的高度 < 页面滚动过的高度 + 浏览器可视高度

```javascript
img.offsetTop < window.innerHeight + document.body.scrollTop;
```

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>



#### 方式二：借助[IntersectionObserver](https://developer.mozilla.org/zh-CN/docs/Web/API/IntersectionObserver)



#### 应用：

* 曝光埋点

