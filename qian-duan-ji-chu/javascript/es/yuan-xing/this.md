---
description: this详解
---

# this

## 一、为什么要有this <a href="#e4-b8-80-e4-b8-ba-e4-bb-80-e4-b9-88-e8-a6-81-e6-9c-89this" id="e4-b8-80-e4-b8-ba-e4-bb-80-e4-b9-88-e8-a6-81-e6-9c-89this"></a>

#### 原因1：不用每次都传上下文（context）

有this的情况：

```javascript
function uppercaseName() {
    return this.name.toUpperCase();
}

function sayHi() {
    console.log(`Hello, I am ${uppercaseName.call(this)}, and ${this.age} years old.`);
}

let Tom = {
    name: 'tom',
    age: 8
};

let Jerry = {
    name: 'jerry',
    age: 9
};

sayHi.call(Tom);
sayHi.call(Jerry);
```

没有this的情况：

```javascript
function uppercaseName(that) {
    return that.name.toUpperCase();
}

function sayHi(that) {
    console.log(`Hello, I am ${uppercaseName(that)}, and ${that.age} years old.`);
}

let Tom = {
    name: 'tom',
    age: 8
};

let Jerry = {
    name: 'jerry',
    age: 9
};

sayHi(Tom);
sayHi(Jerry);
```

#### 原因2：没有this，class无法实现

```javascript
class Person {
    constructor(name, age){
        this.name = name;
        this.age = age;
    }

    uppercaseName() {
        return this.name.toUpperCase();
    }

    sayHi() {
        console.log(`Hello, I am ${this.uppercaseName()}, and ${this.age} years old.`);
    }
}
```

如果没有this，没办法将属性挂载到实例上，属性函数内部也无法相互调用

## 二、this指向谁 <a href="#e4-ba-8cthis-e8-af-af-e5-8c-ba" id="e4-ba-8cthis-e8-af-af-e5-8c-ba"></a>

this一般出现在函数中，this的指向取决于函数执行场景，一般分为4个场景：

#### 1、默认：<mark style="color:green;">this -> 全局变量(非严格模式)/上下文</mark>

```
var name = 'Tom';

function sayName() {
    console.log(`Hi, I am ${this.name}!`);
}

//this隐式指向全局
sayName(); //严格模式指向undefined，非严格模式下正常
```

输出：

浏览器：

> Hi, I am Tom!

node.js：

> <mark style="color:red;">TypeError: Cannot read properties of undefined (reading 'name')</mark>



全局中this的指向：

* 浏览器：this -> window
* node.js：this -> undefined

#### 2、隐式：<mark style="color:green;">this -> 调用对象</mark>

```javascript
let Tom = {
  name: "Tom",
  sayName: function () {
    console.log(`Hi, I am ${this.name}!`);
  },
};

Tom.sayName();

function sayHi() {
  console.log(`Hi, I am ${this.name}!`);
}
let Jerry = {
  name: "Jerry",
  sayName: Tom.sayName,
  sayHi: sayHi,
};

Jerry.sayName(); //this隐式指向Jerry
Jerry.sayHi();
```

输出：

> Hi, I am Tom!&#x20;
>
> Hi, I am Jerry!&#x20;
>
> Hi, I am Jerry!

#### 3、显式：<mark style="color:green;">this -> 指定对象</mark>

```javascript
let Tom = {
  name: "Tom",
  sayName: function () {
    console.log(`Hi, I am ${this.name}!`);
  },
  sayTitle(...titles) {
    this.sayName();
    console.log(`my title: ${[...titles].join("、")}`);
  },
};

Tom.sayName();
Tom.sayTitle("developer");

let Jerry = {
  name: "Jerry",
  sayName: function () {
    console.log(`Hi, I am ${this.name}!`);
  },
};
let Jack = {
  name: "Jack",
};

//this显式指向Jery
Tom.sayTitle.apply(Jerry, ["developer", "programmer", "engineer"]);
Tom.sayTitle.apply(Jack, ["developer", "programmer", "engineer"]);
```

输出：

> Hi, I am Tom!&#x20;
>
> Hi, I am Tom!&#x20;
>
> my title: developer&#x20;
>
> Hi, I am Jerry!&#x20;
>
> my title: developer、programmer、engineer
>
> <mark style="color:red;">TypeError: this.sayName is not a function</mark>

#### 4、new：<mark style="color:green;">this -> 新对象</mark>

new实例化时经典4步中的第3步

```javascript
function Person(name) {
    this.name = name;
    this.sayName = function () {
        console.log(`Hi, I am ${this.name}!`);
    }
}

//this显式指向Person的实例
let Tom = new Person('Tom');
Tom.sayName();

let Jerry = new Person('Jerry');
Jerry.sayName();
```



## 三、破解this的困局

函数的调用方式决定了 `this` 的值（运行时绑定），`this` 不能在执行期间被赋值，并且在每次函数被调用时 `this` 的值也可能会不同：

* ES5 引入了 [bind](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/Function/bind) 方法来设置函数的 `this` 值，而不用考虑函数如何被调用的。
* ES6 引入了[箭头函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow\_functions)，箭头函数不提供自身的 this 绑定（`this` 的值将保持为闭合词法上下文的值）。







参考：

* [https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this)
