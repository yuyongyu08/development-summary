# 柯里化

### 题目

```javascript
function add(n){
    return n + 2
}

function sub(n){
    return n -3
}

function square(n){
   return  n * 3
}

function cube(n){
   return  n * 3
}

const r1 = add(sub(square(cube(2))));
const r2 = compose(add, sub, square, cube)(2);

// 实现此函数，使r2和r1的结果相等
function compose(){

}
```

### 答案

```javascript
function compose(...params){
  return function (arg){
    return Array.from(params).sort(() => -1).reduce((pre, next) => next(pre), arg)
  }
}
```



### 解析

* 主要考察柯里化（提前收集参数）
* 考察数组的reduce
