# 常见遍历方式

## 一、对象

1、for...in + hasOwnProperty

2、先通过Object.entries()、Object.keys()、Object.values()转成数组，然后forEach <mark style="color:red;">【推荐】</mark>

## 二、数组

1、Array.prototype.forEach((item, index, arr) => {}, thisArg) <mark style="color:red;">【推荐】</mark>

2、for...of

3、for

## 三、Map

1、Map.prototype.forEach((item, index, arr) => {}, thisArg) <mark style="color:red;">【推荐】</mark>

## 四、Set

1、Set.prototype.forEach((item, index, arr) => {}, thisArg) <mark style="color:red;">【推荐】</mark>
