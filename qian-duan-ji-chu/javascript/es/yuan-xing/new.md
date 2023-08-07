---
description: new详解
---

# new

## 一、实例化

形式1：**构造函数（ES5）**

```javascript
function Person(name) {
    this.name = name
}
Person.prototype.sayHi = function() {
    console.log('hi,', this.name)
}

let p = new Person('rory');
p.sayHi(); // hi, rory

console.log(p.__proto__ === Person.prototype); // true
```

形式2：**类（ES6）**

```javascript
class Person {
  constructor(name) {
      this.name = name;
  }

  sayHi() {
      console.log('hi,', this.name)
  }
}

let p = new Person('rory');
p.sayHi(); // hi, rory

console.log(p.__proto__ === Person.prototype); // true
```

## 二、构造函数实例化过程：

1. 声明一个空对象
2. 改变原型：将空对象的原型（\_\_proto\_\_）指向构造函数的原型对象（prototype）
3. 改变this：将构造函数的this指向空对象
4. 返回结果：<mark style="color:red;">判断构造函数执行结果是否是对象，是则直接返回执行结果，否则返回声明的那个空对象</mark>

## 三、手动实现new：

```javascript
function myNew(constructor, ...args) {
    // 1.声明一个实例对象
    let obj = {};

    // 2.将实例对象的原型指向构造函数的原型对象
    Object.setPrototypeOf(obj, constructor.prototype)

    // 3.将构造函数的this指向此实例对象
    const result = constructor.call(obj, ...args)

    // 4.返回此实例对象
    return typeof result === 'object' ? result : obj
}
```

验证：构造函数有返回值的情况

```javascript
function Person() {
    this.name = 'yuyy'
}
const p = new Person();
console.log(p); // Person { name: 'yuyy' }

function Person1() {
    this.name = 'yuyy'
    return { age: 18 }
}
const p1 = new Person1();
console.log(p1); // { age: 18 }

function Person2() {
    this.name = 'yuyy'
    return 1
}
const p2 = new Person2();
console.log(p2); // Person2 { name: 'yuyy' }
```



## 四、new.target

检测函数或构造方法是否是通过[new](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/new)运算符被调用的

* 普通的函数调用：new -> undefined
* 有[new](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/new)的构造函数调用：new -> 构造函数名

```javascript
function Foo() {
    console.log(new.target?.name);
}

Foo();
new Foo();
```

输出：

> undefined
>
> Foo





参考：

* [https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/new](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/new)
* [https://juejin.cn/post/6850037282319204360](https://juejin.cn/post/6850037282319204360)
* [https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/new.target](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/new.target)
