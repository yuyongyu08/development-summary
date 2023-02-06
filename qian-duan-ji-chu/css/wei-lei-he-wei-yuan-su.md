# 伪类和伪元素

## 一、伪类

用于选择处于特定状态的元素，伪类表现得会像是在文档的某个部分应用了一个类一样。

前缀用**单冒号**（由于历史原因，某些伪元素比如::before用单冒号也支持，主要是为了向下兼容）

### 常见选择器伪类：

*   p:first-child（选择器匹配属于任意元素的第一个子元素的

    元素）
* p:last-child（选择所有p元素的最后一个子元素）
* p:first-of-type（选择的每个 p 元素是其父元素的第一个 p 元素）
* p:last-of-type（选择每个p元素是其母元素的最后一个p元素）
* :not(p)（选择所有p以外的元素）
* p:nth-child(2)（选择所有 p 元素的父元素的第二个子元素）
* p:nth-last-child(2)（选择所有p元素倒数的第二个子元素）
* p:nth-of-type(2)（选择所有p元素第二个为p的子元素）
* p:nth-last-of-type(2)（选择所有p元素倒数的第二个为p的子元素）

> <mark style="color:red;">易错点：child和of-type的区别</mark>
>
> child：只要求是子元素，不限定类型
>
> of-type：先限定元素类型，然后再查数量

{% embed url="https://codepen.io/yuyy/full/bGjZZeq" %}
child和of-type的区别
{% endembed %}

应用：奇数行、偶数行

```css
p:nth-child(odd)
{
	background:#ff0000;
}
p:nth-child(even)
{
	background:#0000ff;
}
```

### 常见用户行为伪类：

* a:link（选择所有未访问链接）
* a:visited（选择所有访问过的链接）
* a:active（选择正在活动链接）
* a:hover（把鼠标放在链接上的状态）
* imput:focus（选择元素输入后具有焦点）





## 二、伪元素

对元素中的特定内容进行操作，它控制的内容实际上和元素是相同的，但是它本身只是基于元素的抽象，并不存在于文档中，表现得是像在选定元素中加入新的元素一样。

前缀用**双冒号**

> 一些早期的伪元素曾使用单冒号的语法，浏览器为了保持后向兼容，支持早期的带有单双冒号语法的伪元素。**CSS3规范是用双冒号**。

常见伪元素：

* p::before（在每个元素之前插入内容）
* p::after（在每个元素之后插入内容）
* p::first-letter（选择每个元素内容的第一个字母）
* p::first-line（选择每个元素内容的第一行）



应用：尾部添加省略号、下拉项尾部的三角形



参考：

* [https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building\_blocks/Selectors/Pseudo-classes\_and\_pseudo-elements](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building\_blocks/Selectors/Pseudo-classes\_and\_pseudo-elements)
