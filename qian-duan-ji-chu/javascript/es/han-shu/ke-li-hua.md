# 柯里化

## &#x20;概念

柯里化（Currying）是把接受多个参数的函数变换成接受一个单一参数(最初函数的第一个参数)的函数，并且返回接受余下的参数且返回结果的新函数的技术。

**要点：**

1. 将多参数的函数进行变换，让其变成每次只接受1个参数
2. 返回一个新函数，此函数可以接受余下的参数，并且返回结果

**柯里化是一个逐步接收参数的过程。**



<mark style="color:red;">为啥要柯里化？</mark>

`Function.protoype.bind`就是一个柯里化的实现



## 实现

### 形参定长：

```javascript
function curry(fn){
  let allArgs = [];

  return function next(...args){
    allArgs = allArgs.concat(...args)

    if(fn.length === allArgs.length){
      const result = fn(...allArgs);
      allArgs = []; // 结果计算完后要清空参数容器，避免柯里化后的函数再次调用后受影响
      return result
    }else{
      return next
    }
  }
}


function add(a, b, c){
  return a+ b+c
}
console.log(add(1,2,3))

let curryingAdd = curry(add);
console.log(curryingAdd(1,2,3));
console.log(curryingAdd(1)(2,3));
console.log(curryingAdd(1)(2)(3));
```



### 形参不定长：

（待补充，目前没有看到比较完美实现）

难点：不确定函数什么时候调用结束，所以，柯里化内部实现的时候，无法判断是直接返回结果还是继续返回函数。

一种思路是通过改写toString或valueOf，但验证并不可行。

```javascript
function curry(fn){
  let allArgs = [];

  function next(){
    allArgs = allArgs.concat(...arguments)
    return next
  }

  next.toString = next.valueOf = function(){
    return fn(allArgs)
  }

  return next
}
```



## 应用

### 1、参数复用

常规实现：

```javascript
function check(reg, text) {
    return reg.test(text)
}

console.log(check(/\d+/g, 'test'));
console.log(check(/[a-z]+/g, 'test'));
```

柯里化实现：

```javascript
function curryingCheck(reg) {
    return function (text) {
        return reg.test(text)
    }
}

let check = curryingCheck(/\d+/g)
let checkLetter = curryingCheck(/[a-z]+/g)

console.log(checkNumber('test'));
console.log(checkLetter('test123'));
```

### 2、兼容逻辑提前确认

常规实现：

```javascript
const on = function (ele, eventName, handler) {
  if (document.addEventListener) {
    ele.addEventListener(eventName, handler, false);
  } else {
    ele.attachEvent("on" + eventName, handler);
  }
};

on(document.querySelector(".demoe"), "click", () => console.log("clicked"));
```

柯里化实现：只需要做一次兼容判断，无需每次调用都判断

```javascript
const curry = function () {
  if (document.addEventListener) {
    return (ele, eventName, handler) => ele.addEventListener(eventName, handler, false);
  } else {
    return (ele, eventName, handler) => ele.attachEvent("on" + eventName, handler);
  }
};

const curringOn = curry();
curringOn(document.querySelector(".demoe"), "click", () => console.log("clicked"));
```

### 3、延迟执行

```javascript
Function.prototype.myBind = function(context){
    let _this = this;

    return function(...args){
        return _this.apply(context, args)
    }
}

function sum(x, y, z){
    return x + y + z
}

let newSum = sum.myBind(null)

console.log(newSum(1, 2, 3))
```



参考：

* [https://zh.javascript.info/currying-partials](https://zh.javascript.info/currying-partials)
* [https://juejin.cn/post/6864378349512065038#heading-27](https://juejin.cn/post/6864378349512065038#heading-27)
* [https://juejin.cn/post/6844903882208837645](https://juejin.cn/post/6844903882208837645)
