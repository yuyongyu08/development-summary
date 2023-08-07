# Array

## 一、常用静态函数

* Array.from(arrayLike, mapFn, thisArg)：浅拷贝的数组实例
* Array.isArray(value)：检测是否为数组
* Array.of(element0, \[element1, element2, ...])：创建数组示例

## 二、常用原型函数

### 1、操作

* Array.prototype.concat(val0, \[val1, val2, ...]): newArr
* Array.prototype.copyWith(target, start, end): newArr 【将\[start,end)间的元素拷贝到target处】
* Array.prototype.fill(value, start, end): newArr 【将\[start,end)间的元素都替换成value】
* Array.prototype.flat(depth): newArr 【递归到depth层将所有元素放到一个数组中】
* Array.prototype.slice(start, end): newArr 【截取\[start,end)间的元素】
* Array.prototype.splice(start, deleteCount, \[item0, ...]): newArr 【通过删除或替换插入元素】 <mark style="color:red;">`[改变原数组]`</mark>

### 2、查找

* Array.prototype.find((item, index, array) => {}): 返回符合规则的第一个元素，否则返回undefined
* Array.prototype.findIndex((item, index, array) => {})：返回符合规则的第一个元素的索引，否则返回-1
* Array.prototype.findLast((item, index, array) => {})：同find，查找方向从后往前
* Array.prototype.findLastIndex((item, index, array) => {})：同findIndex，查找方向从后往前
* Array.prototype.includes(searchItem, from)：true/false 【从制定位置开始查找是否包含指定元素】
* Array.prototype.filter((item, index, array) => {})：newArr【返回所有符合条件的元素】

### 3、位置

* Array.prototype.indexOf(searchItem, from)：【同findIndex，语法不同】
* Array.prototype.lastIndexOf(searchItem, from)：【同findLastIndex，语法不同】

### 4、遍历

* Array.prototype.forEach((item, index, array) => {})
* Array.prototype.every((item, index, array) => {})：所有元素都符合规则返回true，否则返回false
* Array.prototype.some((item, index, array) => {})：只要有一个元素符合规则返回true，否则返回false
* Array.prototype.map((item, index, array) => {})：newArr&#x20;

### 5、归并

* Array.prototype.reduce((pre, cur, curIndex, array) => {}, initVal)
* Array.prototype.[reduceRight](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/reduceRight)((pre, cur, curIndex, array) => {}, initVal)

### 6、排序

* Array.prototype.sort(compareFn): newArr&#x20;
  * compareFn(a, b) > 0，b排在a前面
  * compareFn(a, b) = 0，位置不变
  * compareFn(a, b) < 0，a排在b前面
* Array.prototype.reverse()

### 7、栈方法

* Array.prototype.push(item0\[, item1, ...])：newLen 【尾部追加】 <mark style="color:red;">`[改变原数组]`</mark>
* Array.prototype.pop()：newLen 【删除最后一个元素】 <mark style="color:red;">`[改变原数组]`</mark>
* Array.prototype.unshift(item0\[, item1, ...])：newLen 【头部插入】 <mark style="color:red;">`[改变原数组]`</mark>
* Array.prototype.shift()：【删除第一个元素】 <mark style="color:red;">`[改变原数组]`</mark>

### 8、转换

* Array.prototype.join(str)：str 【将所有元素用str分割连接成字符串，默认用逗号分隔】
* Array.prototype.toString() 【内部调用了join函数】
* Array.prototype.toLocalString



## 三、遍历方式

1、arr.forEach((item, index, array) => {})

2、for...of



参考：

* [https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/Array](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/Array)
