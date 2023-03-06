---
description: this
---

# 箭头函数this-2

## 题目

说明代码输出结果

```javascript
let tom = {
    name: 'Tom',
    say: function() {
        return ()=>{
            console.log('name: ', this.name);
        }
    }
}

let jerry = {
    name: 'Jerry'
}

tom.say()();
tom.say().call(jerry);
tom.say.call(jerry)();
```

## 答案

输出：

```
name:  Tom
name:  Tom
name:  Jerry
```



## 知识点

* 箭头函数this指向
* call、apply对箭头函数的this影响

