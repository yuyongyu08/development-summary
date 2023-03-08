# 变量提升

## 一、变量为什么会提升？

JavaScript代码是先编译再执行，即分为**编译阶段**和**执行阶段。**编译阶段需要将变量声明提升到作用域顶部，以确保后续代码能正常编译。

<figure><img src="../../../../.gitbook/assets/image (12) (1).png" alt=""><figcaption></figcaption></figure>

执行上下文是 JavaScript 执行一段代码时的运行环境，它定义了变量或函数有权访问的其他数据，决定了它们各自的行为。

每个执行上下文都有三个重要属性：

* 变量对象
* 作用域链
* this 指向



## 二、同名变量和同名函数

<mark style="color:red;">**后面的覆盖前面的**</mark>

```javascript
console.log(myName)
var myName = 'yuyy';
var myName = 'rory';


showName();
function showName() {
  console.log("Tom");
}
function showName() {
  console.log("Jerry");
}
```

输出：（浏览器环境运行，node.js运行报错）

```
rory
Jerry
```

## 三、变量与函数同名

变量和函数同名，不论谁先声明，<mark style="color:red;">**函数始终覆盖变量**</mark>

```javascript
showName();
function showName() {
    console.log('Tom');
}
var showName = 'Jerry';
```

```javascript
showName();
var showName = 'Jerry';
function showName() {
    console.log('Tom');
}
```

```javascript
showName();
function showName() {
    console.log('Tom')
}

var showName = function() {
    console.log('Jerry')
}
```

以上3段代码输出都是：

```
Tom
```



