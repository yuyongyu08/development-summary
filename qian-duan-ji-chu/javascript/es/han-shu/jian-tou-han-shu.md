# 箭头函数

## 一、为啥要有箭头函数？

* 更短的函数
* 不绑定this：确定this时不用像普通函数考虑因调用方式不同而导致this指向不同

## 二、箭头函数this指向谁？

<figure><img src="../../../../.gitbook/assets/image (1) (3).png" alt=""><figcaption></figcaption></figure>

箭头函数不创建自己的this，**函数体内的this继承自**<mark style="color:red;">**作用域链的上一层**</mark>** this**，在箭头函数声明时就已经确定。但**作用域上层的this如果改变，箭头函数的this也会随之变化**。

箭头函数作用域的上层常见有两种：

* **对象**：

```javascript
window.age = 18;

let obj = {
    name: 'yuyy',
    say: ()=>{
        console.log('name: ', this.name);
        console.log('age: ', this.age);
    }
}
obj.say();
```

输出：

```
name: 
age:  18
```

解释：

say这个箭头函数作用域是obj，obj的上一层是全局，全局的this是window



* **函数**：

```javascript
window.age = 18;

let obj = {
    name: 'yuyy',
    say: function() {
        return ()=>{
            console.log('name: ', this.name);
            console.log('age: ', this.age);
        }
    }
}
obj.say()();
```

输出：

```
name:  yuyy
age:  undefined
```

解释：

此处的箭头函数的作用域是say函数，say函数的上一层是obj对象，obj的this是其自身



<mark style="color:red;">**重要！！！**</mark>

如果箭头函数作用域外层是`函数`：则箭头函数this继承函数的this，`且`<mark style="color:red;">`外层函数的this改变，箭头函数的this也会改变`</mark>（可以理解为箭头函数的this在声明时和外层函数的this建立了引用关系）

```javascript
let obj = {
    name: 'yuyy',
    say: function() {
        return ()=>{
            console.log('name: ', this.name);
        }
    }
}

let person = {
    name: 'rory'
}

obj.say()();
obj.say().call(person);
obj.say.call(person)();
```

输出：

```
name:  yuyy
name:  yuyy
name:  rory
```

解释：

第二行输出是由于<mark style="color:red;">箭头函数的 this 继承自外层作用域，通过</mark> <mark style="color:red;"></mark><mark style="color:red;">`call()`</mark> <mark style="color:red;"></mark><mark style="color:red;"></mark> <mark style="color:red;"></mark>_<mark style="color:red;">或</mark>_ <mark style="color:red;"></mark><mark style="color:red;"></mark> <mark style="color:red;"></mark><mark style="color:red;">`apply()`</mark> <mark style="color:red;"></mark><mark style="color:red;">方法调用箭头函数时，只能传递函数所需参数，不能绑定 this</mark>，所以`call()` _或_ `apply()` 的第一个参数会被忽略



## 三、箭头函数为啥不能new？

和new过程中的两个关键点有关：

* this
* 原型对象（prototype）

原因1：箭头函数不创建自己的this（函数体内的this继承自作用域链的上一层 this）

原因2：箭头函数没有原型对象（prototype）

```javascript
const Person1 = function () {
};

const Person2 = () => {
};

console.log('Person1.prototype: ', Person1.prototype);
console.log('Person2.prototype: ', Person2.prototype);
```

输出：

```
Person1.prototype: {constructor: ƒ}
Person2.prototype: undefined
```



## 四、**arguments**

箭头函数没有**arguments**

```javascript
const Person2 = () => {
    console.log(arguments)
};
Person2();
```

输出：

```javascript
Uncaught ReferenceError: arguments is not defined
```



### 箭头函数与普通函数的区别：

1. this指向：在生命阶段就已确定
2. 无原型对象
3. 不能new
4. 没有arguments



参考：

* [https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow\_functions](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow\_functions)
* [https://segmentfault.com/a/1190000010981003](https://segmentfault.com/a/1190000010981003)

