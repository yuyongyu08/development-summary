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



<mark style="color:red;">注意：对于不定参数的函数，其形参长度为0</mark>

```javascript
function test (...args){
  console.log('形参（内部计算）:', test.length);
  console.log('实参:', arguments.length);
}
console.log('形参（外部计算）:',test.length);
test(1,2);
```

输出：

> 形参（外部计算）: 0&#x20;
>
> 形参（内部计算）: 0&#x20;
>
> 实参: 2



参考：

* [https://juejin.cn/post/6864378349512065038](https://juejin.cn/post/6864378349512065038)
