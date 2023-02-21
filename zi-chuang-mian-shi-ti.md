# 经典面试题

### 1、箭头函数的this

运行结果及原因

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

**运行结果：**

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

<mark style="color:red;">箭头函数的this指向其声明时作用域的上一层。</mark>

浏览器环境：Jerry的sayHi函数的作用域的上一层是全局，此时this.name应该是window上的name，但是window上没有声明name属性，所以为空；

Node环境：node环境的全局this是undefined，所以报错



## 2、数据类型转换

实现一个函数，将input转成output

```javascript
const input = [
  { id: "1", data: "中国", pid: null },
  { id: "2", data: "北京", pid: "1" },
  { id: "3", data: "上海", pid: "1" },
  { id: "4", data: "海淀", pid: "2" },
];

const output = [
  {
    id: "1",
    data: "中国",
    pid: null,
    children: [
      { id: "2", data: "北京", pid: "1", children: [{ id: "4", data: "海淀", pid: "2" }] },
      { id: "3", data: "上海", pid: "1" },
    ],
  },
];
```

解法1：自下而上构造

```javascript
function list2tree(list) {
  let arr = [];
  let map = new Map();
  list.forEach((item) => map.set(item.id, item));

  list.forEach((item) => {
    if (item.pid) {
      let parent = map.get(item.pid);
      parent.children = parent.children || [];
      parent.children.push(item);
    } else {
      arr.push(item);
    }
  });

  return arr;
}
```

解法2：自上而下构造

```javascript
function list2tree(arr, id = null, link = "pid") {
  return arr.filter((item) => item[link] === id).map((item) => ({ ...item, children: list2tree(arr, item.id) }));
}
```







