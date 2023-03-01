# all和allSettled

## 一、关系

allSettled是对all的补充：rejected的也返回



## 二、区别

| 场景                 | Promise.all()            | Promise.allSettled()              |
| ------------------ | ------------------------ | --------------------------------- |
| 全fulfilled         | onResolve，返回所有的fulfilled | onResolve，返回所有的fulfilled          |
| fulfilled+rejected | onRejected，返回最早的rejected | onResolve，返回所有的fulfilled+rejected |
| 全rejected          | onRejected，返回最早的rejected | onResolve，返回所有的rejected           |

## 三、详解

### 1、Promise.all(\[promise, promise2, ...])

* 并发，所有任务都完成才返回结果，返回所有结果作为元素的数组
* <mark style="color:red;">有一个失败，则全失败，直接执行onReject</mark>

```javascript
let p1 = new Promise(function (resolve, reject) {
  setTimeout(resolve, 100, "one");
});
let p2 = new Promise(function (resolve, reject) {
  setTimeout(reject, 200, "two");
});
let p3 = new Promise(function (resolve, reject) {
  setTimeout(resolve, 300, "three");
});

Promise.all([p1, p2, p3]).then(
  (value) => {
    console.log("onResolve: ", value);
  },
  (reason) => {
    console.log("onRejected: ", reason);
  }
);
```

输出：

```
onRejected:  two
```

### 2、Promise.allSettled(\[promise, promise2, ...])

* <mark style="color:red;">始终执行onResolve，不管有没有rejected的任务</mark>

```javascript
let p1 = new Promise(function (resolve, reject) {
  setTimeout(resolve, 100, "one");
});
let p2 = new Promise(function (resolve, reject) {
  setTimeout(reject, 200, "two");
});
let p3 = new Promise(function (resolve, reject) {
  setTimeout(resolve, 300, "three");
});

Promise.allSettled([p1, p2, p3]).then((value) => {
  console.log("onResolve: ", value);
});
```

输出：

```
onResolve:  [
  { status: 'fulfilled', value: 'one' },
  { status: 'rejected', reason: 'two' },
  { status: 'fulfilled', value: 'three' }
]
```



## 四、手写

### 1、Promise.all

{% code lineNumbers="true" %}
```javascript
Promise.myAll = function (taskList) {
  if (!Array.isArray(taskList)) throw new Error("参数必须为数组");
  return new Promise((resolve, reject) => {
    let result = [];
    taskList.forEach((task, index) => {
      Promise.resolve(task).then(
        (data) => {
          result[index] = data;
          if (result.length === taskList.length) resolve(result);
        },
        (reason) => {
          reject(reason);
        }
      );
    });
  });
};
```
{% endcode %}

关键点：

* 入参校验
* 返回Promise实例
* 循环执行任务，借助Promise.resolve
* 处理返回数据，并判断是resolve还是reject

### 2、Promise.allSettled

{% code lineNumbers="true" %}
```javascript
Promise.myAllSettled = function (taskList) {
  if (!Array.isArray(taskList)) throw new Error("参数必须为数组");
  return new Promise((resolve, reject) => {
    let result = [];
    taskList.forEach((task, index) => {
      Promise.resolve(task).then(
        (value) => {
          result[index] = { state: "fulfilled", value };
          if (result.length === taskList.length) resolve(result);
        },
        (reason) => {
          result[index] = { state: "rejected", reason };
          if (result.length === taskList.length) resolve(result);
        }
      );
    });
  });
};
```
{% endcode %}

关键点：

* rejected的结果也会被收录到最终结果
* 最终结果都是通过resolve传递出去

