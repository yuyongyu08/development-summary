# 箭头函数this-1

## 题目

说明运行结果及原因

```javascript
let Tom = {
  name: "Tom",
  sayHi: function () {
    console.log(`Hi, I am ${this.name}!`);
  },
  showTitle(...titles) {
    this.sayHi();
    console.log(`my title: ${[...titles].join("、")}`);
  },
};

let Jerry = {
  name: "Jerry",
  sayHi: () => console.log(`Hi, I am ${this.name}!`),
};

Tom.showTitle.call(Jerry, "developer", "engineer");

```

## **答案**

浏览器环境：

> Hi, I am !
>
> my title: developer、engineer

node环境（v16.17.1）：

> <mark style="color:red;">TypeError: Cannot read properties of undefined (reading 'name')</mark>
>
> <mark style="color:red;">sayHi: () => console.log(</mark><mark style="color:red;">`Hi, I am ${this.name}!`</mark><mark style="color:red;">)</mark>
>
> &#x20;                                                                             <mark style="color:red;">^</mark>

解释：

浏览器环境：Jerry的sayHi函数的作用域的上一层是全局，此时this.name应该是window上的name，但是window上没有声明name属性，所以为空；

Node环境：node环境的全局this是undefined，所以报错



## 知识点

* <mark style="color:red;">箭头函数的this指向其声明时作用域的上一层。</mark>
* <mark style="color:red;">函数的call作用</mark>
