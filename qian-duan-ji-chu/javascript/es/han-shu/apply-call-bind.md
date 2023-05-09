---
description: apply、call、bind实现原理
---

# apply、call、bind

## 一、apply

#### **语法：**

```
fn.apply(thisArg[, argsArray])
```

注：有时候容易搞混apply和call的传参数到底谁接受的是数组，记忆小诀窍：apply和Array开头都是字母a，所以apply接受数组\


#### **实现：**

```javascript
Function.prototype.myApply = function (context, args) {
    //第一个参数为null或者undefined时，this指向全局对象window；值为原始值时（例如fn.apply('hello')），this指向该原始值的自动包装对象，如 String、Number、Boolean
    context = (context ?? window) || Object(context);

    //第二个参数可以不传，但类型必须为数组或者类数组
    if (args && !Array.isArray(args)) {
        throw new Error('第二个参数必须为数组')
    }

    //为了避免函数名与上下文(context)的属性发生冲突，使用Symbol类型作为唯一值
    const key = Symbol();
    context[key] = this; // this === fn

    const result = args ? context[key](...args) : context[key]();

    //函数执行完成后删除该属性
    delete context[key];

    return result;
}

function sayHi(msg) {
    console.log(this);
    console.log(`Hi, ${this.name} ${msg}`);
}
sayHi.myApply(undefined) // window
sayHi.myApply(null) // window
sayHi.myApply(1) // Number
sayHi.myApply('11') // String
sayHi.myApply(true) // Boolean
sayHi.myApply({ name: 'yuyy' }, ['how old are you?'])
```

#### **思路：**

1. 确定参数，并绑定到Function的原型上
2. 完善第一个参数：如果为null或者undefined，则默认值是window；否则，需要用对象包裹。

```
context = (context ?? window) || Object(context);
```

3. 校验第二个参数是否为数组，否则报错
4. 将this绑定到context上，避免重复用symbol作为key，然后对函数进行执行
5. 恢复context：将this从context上删除
6. 返回结果



## 二、call

#### **语法：**

```javascript
fn.call(thisArg[, arg1, arg2, ...])
```

#### **实现：**

```javascript
Function.prototype.myCall = function (context, ...args) {
    context = (context ?? window) || Object(context);

    const key = Symbol();
    context[key] = this;

    const result = context[key](...args);

    delete context[key];

    return result
}

function sayHi(msg) {
    console.log(`Hi, ${this.name} ${msg}`);
}

sayHi.myCall({ name: 'yuyy' }, 'how old are you?')
sayHi.myCall(null, 'how old are you?')
```

#### **思路：**

除了不需要校验参数，其他同apply

## 三、bind

#### **语法：**

```javascript
fn.bind(thisArg[, arg1[, arg2[, ...]]])
```

注：<mark style="color:red;">`没有对函数进行执行`</mark>，而是指定了this后，生成了一个函数的拷贝

#### **实现：**

<pre class="language-javascript"><code class="lang-javascript">Function.prototype.myBind = function (context, ...args) {
    const _self = this; // this指向原始函数

    // 关键点1: 声明一个新函数
    const newFn = function (...rest) {
        return _self.call(context, ...args, ...rest)
    }

    // 关键点2: 补全原型对象（原始函数如果是箭头函数，没有原型对象，会导致new报错）
    if (_self.prototype) {
        newFn.<a data-footnote-ref href="#user-content-fn-1">prototype</a> = Object.create(_self.prototype)
    }

    return newFn
}

function sayHi(msg) {
    console.log(`Hi, ${this.name} ${msg}`);
}
const newSayHi = sayHi.myBind({ name: 'yuyy' }, 'how old are you?')
newSayHi()
</code></pre>



#### **思路：柯里化方式实现**

1. 拷贝this（<mark style="color:red;">为什么要拷贝？避免newFun中出现this.call()</mark>）

```
const _self = this
```

2. 生成新函数，将参数传入，this来自源于绑定时的上下文

```
const newFn = function (...rest) {
    return _self.call(context, ...args, ...rest)
}

```

3. 判断函数是否有原型，有则复制给newFn，有些函数是没有原型的，比如箭头函数

```
if (_self.prototype) {
    newFn.prototype = Object.create(_self.prototype)
}
```

4. 返回新函数



## **总结**

* 三者都是Function原型对象的函数，每个函数都会默认继承
* 三折的作用都是显式改变函数的this指向
* apply和call除了接收参数方式不同，效果相同，都会执行当前函数
* bind只是对当前函数做了一次柯里化，并不执行当前函数

[^1]: 
