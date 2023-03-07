# 常见异步

## &#x20;一、常见宏任务和微任务

| 宏任务（macro task）                                                                                        | 微任务（micro task）                                                                                         |
| ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------- |
| <ul><li>同步代码</li><li>setTimeout/setInterval/setImmediate</li><li>UI交互事件</li><li>I/O（node.js）</li></ul> | <ul><li>process.nextTick（node.js）</li><li>Promise</li><li>async/await</li><li>MutaionObserver</li></ul> |



## 二、在事件循环中的应用

### 面试题1:

```javascript
console.log('1');
setTimeout(function() {
    console.log('2');
    process.nextTick(function() {
        console.log('3');
    })
    new Promise(function(resolve) {
        console.log('4');
        resolve();
    }).then(function() {
        console.log('5')
    })
})
process.nextTick(function() {
    console.log('6');
})
new Promise(function(resolve) {
    console.log('7');
    resolve();
}).then(function() {
    console.log('8')
})
setTimeout(function() {
    console.log('9');
    process.nextTick(function() {
        console.log('10');
    })
    new Promise(function(resolve) {
        console.log('11');
        resolve();
    }).then(function() {
        console.log('12')
    })
})
```

输出：

```
1
7
6
8
2
4
3
5
9
11
10
12
```



### 面试题2:

```javascript
async function async1() {
    console.log('async1 start');
    await async2();
    console.log('async1 end');
}

async function async2() {
    console.log('async2');
}

console.log('script start');

setTimeout(function () {
    console.log('setTimeout');
}, 0)

async1();

new Promise(function (resolve) {
    console.log('promise1');
    resolve();
}).then(function () {
    console.log('promise2');
}).then(function () {
    console.log('promise3');
})


new Promise(function (resolve) {
    console.log('promise4');
    resolve();
}).then(function () {
    console.log('promise5');
});

console.log('script end');
```

输出：

```
script start
async1 start
async2
promise1
promise4
script end
async1 end
promise2
promise5
promise3
setTimeout
```

> **为什么promise3出现在promise5？**
>
> promise3是在promise2执行完成后加入到微任务队列的，此时promse5已经在微任务队列中了





### setTimeout(callback, delay)的delay如何理解？

这个时间值代表了消息被实际加入到队列的最小延迟时间，而非确切的等待时间。

例如：setTimeout(() => console.log('called'), 100)代表100毫秒后放入到宏任务队列，如果在这之前微任务队列有其他任务，则等待时间一定大于100毫米。

```javascript
const s = new Date().getSeconds();

setTimeout(function() {
  // 输出 "2"，表示回调函数并没有在 500 毫秒之后立即执行
  console.log("Ran after " + (new Date().getSeconds() - s) + " seconds");
}, 5000);

while(true) {
  if(new Date().getSeconds() - s >= 2) {
    console.log("Good, looped for 2 seconds");
    break;
  }
}
```

详解参见：[入口](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/EventLoop#%E6%B7%BB%E5%8A%A0%E6%B6%88%E6%81%AF)



### await后面的代码为啥是微任务？

async-await 只是 Promise+generator 的一种语法糖而已。

例如：

```javascript
async function B() { 
    console.log(Math.random()); 
    let now = await A(); 
    console.log(now); 
}
```

等同于：

```javascript
function B() {
    console.log(Math.random());
    A().then(function(now) {
        console.log(now);
    })
}
```



### Promise的微任务什么时候加入到微任务队列？

Promise的微任务必须是实例的状态<mark style="color:red;">**变成非pending之后加入**</mark>到微任务队列

注意观察promise3和promise4的输出顺序

```javascript
new Promise(function(resolve) {
    console.log('promise1');
    resolve();
}).then(function() {
    setTimeout(() => console.log('promise2'), 1000)
}).then(function() {
    console.log('promise3');
})


Promise.resolve('promise4').then(function(value) {
    console.log(value);
})
```

输出：

```
promise1
promise4
promise3
promise2
```







参见：

* [https://developer.mozilla.org/zh-CN/docs/Web/API/setTimeout](https://developer.mozilla.org/zh-CN/docs/Web/API/setTimeout)

