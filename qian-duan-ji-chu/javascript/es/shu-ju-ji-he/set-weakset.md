# Set、WeakSet

## 一、Set

直观上**和数组类似**，最大的特点是**自动去重**，去重时对比的方式类似于恒等（<mark style="color:red;">`===`</mark>）。

> Set判断成员是否相同与严格相等（<mark style="color:red;">`===`</mark>）区别：
>
> * 0和-0：Set是同一个key，<mark style="color:red;">`===`</mark> 认为不相等
> * NaN和NaN：Set是同一个key，<mark style="color:red;">`===`</mark> 认为不相等

### 1、实例属性及方法

* Set.prototype.add(value)
* Set.prototype.has(value)
* Set.prototype.delete(value)
* Set.prototype.clear()
* Set.prototype.size

### 2、遍历方法

* Set.prototype.forEach((value, key, set) => {}, thisArg) <mark style="color:red;">【推荐】</mark>
* Set.prototype.entries()
* Set.prototype.keys()：Set.prototype.values的别名
* Set.prototype.values()

<mark style="color:red;">**注意**</mark>：Set的遍历顺序就是插入顺序

### 3、类型转换

* Array => Set

```javascript
let set = new Set(array)
```

* String => Set

```
let set = new Set(string)
```

* Set => Array

```javascript
let set = new Set([1,2,3])

// 方式1
let arr1 = [...set];

// 方式2
let arr2 = Array.from(set);
```

### 4、应用

* 数组去重

```javascript
let arr = [...new Set(arr)]
```

* 字符串去重

```javascript
let str = [...new Set(str)].join('');
```

* 数组的交、并、补集

```javascript
let a = [1, 2, 3];
let b = [3, 4, 5];

// 交集
let intersect = a.filter(item => b.includes(item));

// 并集
let union = [...new Set([...a, ...b])];

// 补集
let difference = [...a.filter(item => !b.includes(item)), ...b.filter(item => !a.includes(item))]
```

## 二、WeakSet

### 1、成员类型只能是对象

<pre class="language-javascript"><code class="lang-javascript">const ws = new WeakSet();
<strong>
</strong><strong>ws.add(1); // TypeError: Invalid value used in weak set
</strong>ws.add('1'); // TypeError: Invalid value used in weak set
ws.add(true); // TypeError: Invalid value used in weak set
ws.add(null); // TypeError: Invalid value used in weak set
ws.add(undefined); // TypeError: Invalid value used in weak set

ws.add(Symbol());
ws.add({});

ws.add(() => {});
ws.add([]);
ws.add(new Map());
</code></pre>

### 2、成员是弱引用

WeakSet 中的对象都是**弱引用**，**不计入垃圾回收机制**，如果其他地方都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于 WeakSet 之中。

### 3、不支持遍历

由于成员对象随时有可能被回收掉，成员数量不可预测，所以没有提供size属性，无法进行对WeakSet进行遍历。

仅以下3个实例方法：

* Set.prototype.add(value)
* Set.prototype.has(value)
* Set.prototype.delete(value)

## 三、对比

<table><thead><tr><th width="114.33333333333331">区别</th><th>Set</th><th>WeakSet</th></tr></thead><tbody><tr><td>成员类型</td><td>不限</td><td>对象</td></tr><tr><td>成员函数和属性</td><td><ul><li>Set.prototype.add(value)</li><li>Set.prototype.has(value)</li><li>Set.prototype.delete(value)</li><li><mark style="color:red;">Set.prototype.size</mark></li><li><mark style="color:red;">Set.prototype.clear()</mark></li><li><mark style="color:red;">Set.prototype.forEach()</mark></li><li><mark style="color:red;">Set.prototype.values()</mark></li><li><mark style="color:red;">Set.prototype.keys()</mark></li><li><mark style="color:red;">Set.prototype.entries()</mark></li></ul></td><td><ul><li>WeakSet.prototype.add(value)</li><li>WeakSet.prototype.has(value)</li><li>WeakSet.prototype.delete(value)</li></ul></td></tr><tr><td>遍历</td><td>支持</td><td>不支持</td></tr><tr><td>适用场景</td><td>有去重需求的数据</td><td>不关心垃圾回收机制（比如存储DOM节点）</td></tr></tbody></table>



参考：

* [https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/Set](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/Set)
* [https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/WeakSet](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/WeakSet)
* [https://es6.ruanyifeng.com/#docs/set-map#Set](https://es6.ruanyifeng.com/#docs/set-map#Set)
