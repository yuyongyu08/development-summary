# race和any

## 一、关系

any是对race的补充：尽可能等一个fulfilled的结果

## 二、区别

<table><thead><tr><th width="178.33333333333331">场景</th><th>Promise.race()</th><th>Promise.any()</th></tr></thead><tbody><tr><td>全fulfilled</td><td>onResolve，返回最早的fulfilled</td><td>onResolve，返回最早的fulfilled</td></tr><tr><td>fulfilled+rejected</td><td>不定，返回最早的rejected/fulfilled</td><td>onResolve，返回最早的fulfilled</td></tr><tr><td>全rejected</td><td>onRejected，返回最早的rejected</td><td>onRejected，返回所有的rejected</td></tr></tbody></table>

## 三、详解

### 1、Promise.race(\[promise, promise2, ...])

* 并发，返回最早完成的那个任务的结果；
* <mark style="color:red;">始终返回最早的那个任务：如果fulfiled则执行onResolve，如果rejected则执行onReject</mark>

```javascript
let p1 = new Promise(function (resolve, reject) {
  setTimeout(resolve, 500, "one");
});
let p2 = new Promise(function (resolve, reject) {
  setTimeout(reject, 100, "two");
});

Promise.race([p1, p2]).then(
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

### 2、Promise.any(\[promise, promise2, ...])

* 尽可能返回fulfiled的任务的结果
* <mark style="color:red;">只要有一个fulfiled的任务，则执行onResolve；只有全都rejected时才执行onReject</mark>

```javascript
let p1 = new Promise(function (resolve, reject) {
  setTimeout(resolve, 500, "one");
});
let p2 = new Promise(function (resolve, reject) {
  setTimeout(reject, 100, "two");
});

Promise.any([p1, p2]).then(
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
onResolve:  one
```

## 四、手写

### 1、Promise.race

```javascript
Promise.myRace = function (taskList) {
  if (!Array.isArray(taskList)) throw new Error("参数必须为数组");
  return new Promise((resolve, reject) => {
    taskList.forEach((task, index) => {
      Promise.resolve(task).then(
        (value) => {
          resolve(value);
        },
        (reason) => {
          reject(reason);
        }
      );
    });
  });
};
```

### 2、Promise.any

```javascript
Promise.myAny = function (taskList) {
  if (!Array.isArray(taskList)) throw new Error("参数必须为数组");
  return new Promise((resolve, reject) => {
    let reasons = [];
    taskList.forEach((task, index) => {
      Promise.resolve(task).then(
        (value) => {
          resolve(value);
        },
        (reason) => {
          reasons[index] = reason;
          if (reasons.length === taskList.length) reject(reasons);
        }
      );
    });
  });
};
```
