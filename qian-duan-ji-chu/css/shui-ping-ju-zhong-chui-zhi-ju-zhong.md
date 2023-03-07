# 水平居中、垂直居中

## 一、行内元素

* 水平：`text-align: center`
* 垂直：`line-height: {父元素高度}px`

## 二、块状元素

### 1、子元素宽高确定：

方式1：绝对定位 + 各方向为0 + margin:auto

{% embed url="https://codepen.io/yuyy/full/GRXvajY" %}

方式2：left/top:50% + margin-left/margin-top: 宽/高一半

{% embed url="https://codepen.io/yuyy/full/XWPerMp" %}

### 2、子元素宽高不确定

left/top + translate

{% embed url="https://codepen.io/yuyy/full/rNZzgJy" %}

## 三、万能方案

flex

```css
.center{
    display: flex;
    justify-content: center;
    align-items: center;
}
```

