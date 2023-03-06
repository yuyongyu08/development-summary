# 控制并发数

## 题目

实现一个带并发限制的异步调度器Scheduler，保证同时运行的任务最多有两个。完善下面代码的Scheduler类，使以下程序能够正常输出：

```javascript
class Scheduler {
  add(promiseCreator) { ... }
  // ...
}

function task(delay, msg) {
  return () =>
    new Promise((res, rej) => {
      setTimeout(() => {
        console.log(msg);
        res(msg);
      }, delay);
    });
}

const t1 = task(1000, "1");
const t2 = task(500, "2");
const t3 = task(300, "3");
const t4 = task(400, "4");

const scheduler = new Scheduler(2);
scheduler.add(t1);
scheduler.add(t2);
scheduler.add(t3);
scheduler.add(t4);


// output: 2 3 1 4
整个的完整执行流程：
起始1、2两个任务开始执行
500ms时，2任务执行完毕，输出2，任务3开始执行
800ms时，3任务执行完毕，输出3，任务4开始执行
1000ms时，1任务执行完毕，输出1，此时只剩下4任务在执行
1200ms时，4任务执行完毕，输出4
```

## 答案

```javascript
class Scheduler {
  constructor(maxCount) {
    this.queue = [];
    this.maxCount = maxCount;
    this.runningCount = 0;
  }
  add(promiseCreator) {
    this.queue.push(promiseCreator);
    this.runTask();
  }

  runTask() {
    if (this.queue.length > 0 && this.runningCount < this.maxCount) {
      const task = this.queue.shift();
      this.runningCount++;
      task().then(() => {
        this.runningCount--;
        this.runTask();
      });
    }
  }
}
```



## 考察点

* 递归调用
* 异步



