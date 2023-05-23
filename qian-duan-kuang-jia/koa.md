---
description: koa
---

# Koa

## 一、洋葱模型

<div align="left">

<figure><img src="../.gitbook/assets/UML 图.jpg" alt=""><figcaption></figcaption></figure>

</div>

## 二、洋葱模型原理

洋葱模型可以理解成**函数嵌套调用**。

在 `koa` 中，中间件被 `next()` 方法分成了两部分。`next()` 方法上面部分会先执行，下面部分会在后续中间件执行全部结束之后再执行。

### 原理模拟：

```javascript
function A(next) {
  console.log("A start");
  typeof next === "function" && next();
  console.log("A end");
}

function B(next) {
  console.log("B start");
  typeof next === "function" && next();
  console.log("B end");
}

function C(next) {
  console.log("C start");
  typeof next === "function" && next();
  console.log("C end");
}

function D() {
  console.log("D start");
  console.log("D end");
}

A(B.bind(null, C.bind(null, D)));
```

运行结果：

```
A start
B start
C start
D start
D end
C end
B end
A end
```



### compose函数模拟

koa是通过koa-compose库进行中间件调用的，我们可以通过写一个简版compose函数模拟下

#### 方式1：Array.prototype.reduceRight

```javascript
const mws = [A, B, C, D];
function compose(allMW) {
  return allMW.reduceRight((pre, cur) => {
    return cur.bind(null, pre);
  });
}

let mwFn = compose(mws);
mwFn();
```

#### 方式2：柯里化方式（递归）

```javascript
const mws = [A, B, C, D];
function compose(allMW) {
  function dispatch(i) {
    let middleware = allMW[i];
    if (!middleware) return;
    return middleware.bind(null, dispatch(i + 1));
  }

  return dispatch(0);
}

let mwFn = compose(mws);
mwFn();
```



## 三、简版koa

```javascript
class Koa {
  constructor() {
    this.middlewareList = [];
    this.context = {
      request: null,
      response: null,
    };
  }

  use(middleware) {
    this.middlewareList.push(middleware);
  }

  compose(middlewareList) {
    return function (ctx) {
      function dispatch(index) {
        const middleware = middlewareList[index];
        if (!middleware) return;
        return middleware(ctx, dispatch.bind(null, index + 1));
      }

      return dispatch(0);
    };
  }
}
```

测试代码：

```javascript
const app = new Koa();

app.use((ctx, next) => {
  console.log("A start");
  next();
  console.log("A end");
});

app.use((ctx, next) => {
  console.log("B start");
  next();
  console.log("B end");
});

app.use((ctx, next) => {
  console.log("C start");
  next();
  console.log("C end");
});

app.use((ctx, next) => {
  console.log("D start");
  next();
  console.log("D end");
});

const run = app.compose(app.middlewareList);
run();
```

运行结果：

```
A start
B start
C start
D start
D end
C end
B end
A end
```



**koa-compose源码**：[入口](https://github.com/koajs/compose/blob/master/index.js)



参考：

* [https://www.ruanyifeng.com/blog/2017/08/koa.html](https://www.ruanyifeng.com/blog/2017/08/koa.html)
* [https://koajs.com/](https://koajs.com/)
