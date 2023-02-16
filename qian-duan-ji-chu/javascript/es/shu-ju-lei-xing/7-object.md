# 7-object

## &#x20;一、万物皆对象

todo

## 二、对象的遍历方法

### 1、for...in

```javascript
for (const key in object) {
  if (Object.hasOwnProperty.call(object, key)) {
    const element = object[key];
    // todo
  }
}
```

用for...in遍历对象之所以要<mark style="color:red;">**用hasOwnProperty()过滤下**</mark>，是因为for...in会将原型的属性遍历出来，例：

```javascript
function Person(name, age){
  this.name = name;
  this.age = age;
}
Person.prototype.job = 'development'
let p = new Person('yuyy', 18);

for (const key in p) {
  if (Object.hasOwnProperty.call(p, key)) {
    console.log(`${key}: ${p[key]}`);
  }
}
```

输出：

```
name: yuyy
age: 18
job: development
```



> 对象的遍历使用for..in还是for...of容易记混，记忆小技巧：for..<mark style="color:red;">**i**</mark>n和<mark style="color:red;">**o**</mark>bject组成I/O（输入输出的简称）

### 2、Object.entries(obj)

```javascript
Object.entries(obj).forEach(([key, value]) => {
  console.log(`${key}: ${value}`);
});
```

或者

```javascript
for (const [key, value] of Object.entries(obj)) {
  console.log(`${key}: ${value}`);
}
```

注意：Object.entries()返回的是二维数组（\[\[key1, value1], \[key2, value2]....]），所以遍历时记得使用结构赋值



### 3、Object.keys(obj)

使用方式同上

### 4、Object.values(obj) （较少使用）

使用方式同上



## 三、instanceof

**实现：**

```javascript
function myInstanceOf(left, right) {
    if (typeof left !== 'object') {
        return false
    }
    if (Object.prototype.toString.call(right) === '[Object Object]') {
        throw new TypeError('右边必须是对象')
    }

    let leftValue = Object.getPrototypeOf(left);
    const rightValue = right.prototype;

    while (true) {
        if (leftValue === rightValue) {
            return true
        } else if (leftValue === null) {
            return false
        } else {
            leftValue = Object.getPrototypeOf(leftValue)
        }
    }
}
```



**原理：**

1. 先校验参数：左侧参数不能式基本数据类型，右侧参数必须时对象
2. 获取对比值：获取左侧参数的原型，获取右侧参数的原型对象
3. 递归判断：
   1. 如果左侧值和右侧值相同，直接返回true
   2. 如果左侧值为null，说明已经到了原型链的尽头（[参见](../yuan-xing/yuan-xing-lian.md)），仍然和右侧不相同，直接返回false
   3. 上面两种情况都不符合，则继续沿着原型链向上遍历



参见：

* [https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/Object](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/Object)
* [https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...in](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...in)
