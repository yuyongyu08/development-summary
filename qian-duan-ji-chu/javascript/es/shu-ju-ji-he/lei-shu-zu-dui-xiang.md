# 类数组对象

## 一、什么是类数组对象？

本身是一个对象，key是从零开始的索引值，有length属性

形如：

```javascript
let arrayLikeObj = {
    0: 'rory',
    1: 18
}
```

## 二、常见类数组

* arguments
* DOM获取元素方法返回的结果

## 三、将类数组转成数组

1、展开运算符

```javascript
function show(...params) {
    console.log([...arguments])
}
```

2、Array.from

```javascript
function show(...params) {
    console.log(Array.from(arguments))
}
```

3、间接调用Array原型函数

```javascript
function show() {
    console.log(Array.prototype.slice.call(arguments));
    console.log(Array.prototype.concat.apply([], arguments));
    console.log(Array.prototype.splice.call(arguments, 0))
}
```





