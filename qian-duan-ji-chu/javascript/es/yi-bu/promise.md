# Promise

## 一、方法

### 1、静态方法：

* Promise.**all**(\[promise, promise2, ...])
* Promise.**allSettled**(\[promise, promise2, ...])
* Promise.**race**(\[promise, promise2, ...])
* Promise.**any**(\[promise, promise2, ...])
* Promise.**resolve**(value)
* Promise.**reject**(reason)

### 2、原型方法：

* Promise.prototype.**then**(onResolved, onRejected)
* Promise.prototype.**catch**(onRejected)
* Promise.prototype.**finally**(onFinally)



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
