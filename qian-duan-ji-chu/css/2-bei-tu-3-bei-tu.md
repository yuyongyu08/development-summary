# 2倍图、3倍图

### 像素

组成图片的单个色块

* 物理像素：也叫设备像素，硬件设备中的真实像素
* 逻辑像素：也叫CSS像素，编程中抽象出来用于逻辑上衡量像素的单位

### 分辨率

水平方向的像素数 \* 垂直方向的像素数

*   屏幕分辨率：

    * 物理分辨率：是显示器的固有参数，不能调节，一般是指屏幕的最高可显示的像素数。
    * 显示器分辨率：就是操作系统设定的分辨率。

    > 在显示器分辨率和物理分辨率一致时，显示效果才是最佳的，一般推荐设置的分辨率就是物理分辨率。系统设置分辨率生效是通过算法进行了转换。
* 图片分辨率：



### DPR（devicePixelRatio）

它告诉浏览器需要<mark style="color:red;">多少</mark><mark style="color:red;">**物理像素**</mark><mark style="color:red;">来绘制一个</mark> <mark style="color:red;"></mark><mark style="color:red;">**CSS 像素**</mark>，可以用此属性来判断当前屏幕是几倍屏，可以通过<mark style="color:green;">`window.devicePixelRatio`</mark>获取。

DPR（devicePixelRatio， 设备像素比） = 物理像素／CSS像素



### 为什么要有2倍图、3倍图？

**问题：**

主流手机设备分辨率都是 200 x 200，苹果手机分辨率是 400 x 400，一张分辨率200 x 200 图片在主流手机上完美显示，在苹果手机上只显示一半



**目标：**

让图片在主流手机和苹果手机同时完美显示



**解决：**

DPR为2的屏幕称为2倍屏，DPR为3的屏幕称为3倍屏。

苹果手机是2倍屏，如果让2倍屏每2 x 2 个物理像素对应 1 个图片像素，这样就可以完整呈现这个分辨率为200 x 200的图片。

但带来一个新问题：图片本身的分辨率只有200 x 200，这样在2倍屏上就会出现拉伸变模糊的情况。

终极解决方案：针对不同 DPR 的 屏幕，选择不同图片

* 在1倍屏下 a.png 图片像素： 200 x 200
* 在2倍屏下 a@2x.png 图片像素 400 x 400
* 在3倍屏下 a@3x.png 图片像素 600 x 600



### 1px问题

**现象：**

css设置1px的边框，在2倍屏、3倍屏会看起来更粗



**原因：**

一般多倍的设计图设计了1px的边框，在手机上缩小呈现时，由于css最低只支持显示1px大小，导致边框太粗的效果，实际是一种视觉差，并非1px真的变粗了。



**解决：**

```html
伪元素 + transform
```

{% embed url="https://codepen.io/yuyy/full/NWBVpZE" %}
1px 解决方案
{% endembed %}









参考：

* [https://zhuanlan.zhihu.com/p/34988701](https://zhuanlan.zhihu.com/p/34988701)
* [https://segmentfault.com/a/1190000040282079](https://segmentfault.com/a/1190000040282079)
* [https://developer.mozilla.org/zh-CN/docs/Web/API/Window/devicePixelRatio](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/devicePixelRatio)
* [https://juejin.cn/post/7084220221505929230](https://juejin.cn/post/7084220221505929230)
