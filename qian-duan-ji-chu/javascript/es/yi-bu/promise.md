# Promise

## 一、方法

### 静态方法：

* allSettled是对all的补充
* any是对race的补充

主要解决有rejected任务时的场景。

#### 1、Promise.all(\[promise, promise2, ...])

* 并发，所有任务都完成才返回结果，返回所有结果作为元素的数组
* 有一个失败，则全失败，直接执行onReject

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

#### 2、Promise.allSettled(\[promise, promise2, ...])

* 返回结果同Promise.all()
* 区别：有reject的任务，依然执行onResolve，失败的任务结果也一并返回

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



#### 3、Promise.race(\[promise, promise2, ...])

* 并发，返回最早完成的那个任务的结果；
* 最早那个任务：如果fulfiled则执行onResolve，如果rejected则执行onReject

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

#### 4、Promise.any(\[promise, promise2, ...])

* 返回结果同Promise.all()
* 区别：有一个fulfiled的任务，则执行onResolve；全都rejected时才执行onReject

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

#### 5、Promise.resolve(value)

```javascript
Promise.resolve("fulfiled").then((value) => {
  console.log("onResolve: ", value);
});
```

#### 6、Promise.reject(reason)

* 有onRejected时，不再执行catch

```javascript
Promise.reject("fulfiled")
  .then(
    (value) => {
      console.log("onResolve: ", value);
    },
    (reason) => {
      console.log("onRejected: ", reason);
    }
  )
  .catch((err) => {
    console.log("catch: ", err);
  });
```

输出：

```
onRejected:  fulfiled
```

* 无onRejected时，执行catch

```
Promise.reject("fulfiled")
  .then((value) => {
    console.log("onResolve: ", value);
  })
  .catch((err) => {
    console.log("catch: ", err);
  });
```

输出：

```
catch:  fulfiled
```

### 原型方法：

* Promise.prototype.then(onResolved, onRejected)
* Promise.prototype.catch(onRejected)
* Promise.prototype.finally(onFinally)



## 二、手写

```javascript
export default class MyPromise {
  constructor(executor) {
    this._stateSet = {
      pending: "PENDING",
      fulfiled: "FULFILED",
      rejected: "REJECTED",
    };
    this._state = this._stateSet.pending;
    this._value;

    this._resolveCallbacks = [];
    this._rejectCallbacks = [];

    // 一定要用箭头函数，目的是对this进行绑定
    const _resovle = (val) => {
      if (this._state === this._stateSet.pending) {
        // 做3件事：1.改状态 2.赋值 3.遍历执行回调
        this._state = this._stateSet.fulfiled;
        this._value = val;
        this._resolveCallbacks.forEach((fn) => fn(val));
      }
    };
    const _reject = (err) => {
      if (this._state === this._stateSet.pending) {
        this._state = this._stateSet.rejected;
        this._value = err;
        this._rejectCallbacks.forEach((fn) => fn(err));
      }
    };

    try {
      executor(_resovle, _reject);
    } catch (error) {
      _reject(error);
    }
  }

  then(onFulfiled, onRejected) {
    return new MyPromise((resovle, reject) => {
      const resovleFn = (val) => {
        try {
          const x = onFulfiled && onFulfiled(val);
          x instanceof MyPromise ? x.then(val) : resovle(val);
        } catch (error) {
          reject(error);
        }
      };

      const rejectFn = (err) => {
        try {
          const x = onRejected && onRejected(err);
          x instanceof MyPromise ? x.then(err) : reject(err);
        } catch (error) {
          reject(error);
        }
      };

      switch (this._state) {
        case this._stateSet.fulfiled:
          resovleFn(this._value);
          break;
        case this._stateSet.rejected:
          rejectFn(this._value);
          break;
        case this._stateSet.pending:
          this._resolveCallbacks.push(onFulfiled);
          this._rejectCallbacks.push(onRejected);
          break;
      }
    });
  }

  static resovle(value) {
    if (value instanceof MyPromise) {
      return value;
    } else if (value instanceof Object && "then" in value) {
      return new MyPromise((resovle, reject) => {
        value.then(resovle, reject);
      });
    }

    return new MyPromise((resovle) => {
      resovle(value);
    });
  }

  static reject(reason) {
    return new MyPromise((resovle, reject) => {
      reject(reason);
    });
  }

  catch(onRejected) {
    return this.then(undefined, onRejected);
  }

  finally(callback) {
    return this.then(callback, callback);
  }

  all(taskList) {
    // step 1: 返回的是MyPromise实例
    return new MyPromise((resovle, reject) => {
      // step 2: 判断入参
      if (Array.isArray(taskList)) {
        let count = 0;
        let result = [];
        // step 3: 迭代数组
        taskList.forEach((task, index) => {
          // step 4: 用MyPromise.resovle处理任务
          MyPromise.resovle(task).then(
            (value) => {
              count++;
              result[index] = value;
              // step 5: 所有任务都完成则返回
              if (count === taskList.length) {
                resovle(result);
              }
            },
            (reason) => {
              reject(reason);
            }
          );
        });
      } else {
        throw new Error("入参必须是数组");
      }
    });
  }

  race(taskList) {
    return new MyPromise((resovle, reject) => {
      if (Array.isArray(taskList)) {
        taskList.forEach((task) => {
          MyPromise.resovle(task).then(resovle, reject);
        });
      } else {
        throw new Error("入参必须是数组");
      }
    });
  }
}
```



参见：

* [https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/Promise)
* [https://juejin.cn/post/6844903625769091079](https://juejin.cn/post/6844903625769091079)
