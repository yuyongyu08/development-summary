# 动态规划-二维数组全排列

### 题目

```
请编写二维数组的全排列，二维数组中的元素固定两个，数组长度不定，例如：
输入：[[1,2],[3,4],[a,b],[c,d]]
输出：13ac,13ad,13bc,13bd …
```

### 答案

```javascript
function printAllCombination(arr) {
  let pre = arr[0];

  for (let i = 1; i < arr.length; i++) {
    let temp = [];
    pre.forEach((item) => {
      arr[i].forEach((val) => {
        temp.push(`${item}${val}`);
      });
    });
    pre = temp;
  }
  return pre.join(",");
}

console.log(printAllCombination(input));
```

输出结果：

```
13ac,13ad,13bc,13bd,14ac,14ad,14bc,14bd,23ac,23ad,23bc,23bd,24ac,24ad,24bc,24bd
```

### 解析

动态规划，本次的结果以来上次的结果。

两层循环：

* 外层：主要用于取每次被组合元素
* 内层：记录本次组合结果，并作为新的遍历对象

