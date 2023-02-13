# 闭包

## 一、什么是闭包？

内部函数访问外部函数的作用域



## 二、闭包可以用来干什么？

* [柯里化](ke-li-hua.md)
* [防抖、节流](fang-dou-he-jie-liu.md)
* 数据隐藏和封装



## 三、循环中创建的闭包

**示例：**

```javascript
for (var i = 1; i <= 5; i++) {
  setTimeout(function () {
    console.log(i);
  }, 1000);
}
```

**输出：**

1秒后输出

```
6
6
6
6
6
```

**原因：**

setTimeout的回调与for循环（局部作用域）形成了闭包，每次循环都产生一个闭包，这些闭包共享了for循环的词法作用域中的i。i在经过6次计算后变成了6，所以后续每个闭包再打印i时都会显示6。



**解决：**

方案1：var -> let，创建局部作用域

```javascript
for (let i = 1; i <= 5; i++) {
  setTimeout(function () {
    console.log(i);
  }, 1000);
}
```

方案2：借助setTimeout第3个参数提前锁定参数

```javascript
for (var i = 1; i <= 5; i++) {
    setTimeout(function (index) {
        console.log(index);
    }, 1000, i);
}
```



方案3：通过立即执行函数创建二级闭包

```javascript
for (var i = 1; i <= 5; i++) {
    (function (index) {
        setTimeout(function () {
            console.log(index);
        }, 1000);
    })(i)
}
```



方案4：借助bind提前收集参数

```javascript
for (var i = 1; i <= 5; i++) {
    function timer(index) {
        console.log(index);
    }
    setTimeout(timer.bind(this, i), 1000);
}
```



方案5：借助箭头函数的this特性

```javascript
for (var i = 1; i <= 5; i++) {
    this.j = i
    setTimeout(() => {
        console.log(this.j);
    }, 1000);
}
```



## 四、闭包有什么弊端

* 处理速度
* 内存消耗



参考：

* [https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures)
