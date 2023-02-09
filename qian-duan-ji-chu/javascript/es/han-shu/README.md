# 函数



## 参数：

**形参**：function.length

**实参**：arguments.length

```javascript
function sum(a, b, c) {
    console.log('实参：', arguments.length)

    return a + b + c
}

console.log('形参：', sum.length);
sum(1, 2)
```

输出：

> 形参： 3&#x20;
>
> 实参： 2





参考：

* [https://juejin.cn/post/6864378349512065038](https://juejin.cn/post/6864378349512065038)
