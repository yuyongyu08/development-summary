# Map、WeakMap

## 一、Map

类似于对象，也是键值对的集合，由于ES6之前对象的键只能是字符串，所以为了解决这种限制推出了Map。

> ES6之后对象的key也支持了其他类型

添加成员时，如果key相同，后来的value会覆盖之前的value，判断key是否相同类似于严格相等（<mark style="color:red;">`===`</mark>）

> Map对key是否相同与严格相等（<mark style="color:red;">`===`</mark>）区别：
>
> * 0和-0：Map是同一个key，<mark style="color:red;">`===`</mark> 认为不相等
> * NaN和NaN：Map是同一个key，<mark style="color:red;">`===`</mark> 认为不相等

### 1、实例属性及方法

* Map.prototype.set(key, value)
* Map.prototype.get(key)
* Map.prototype.has(key)
* Map.prototype.delete(value)
* Map.prototype.clear()
* Map.prototype.size

### 2、遍历方式

* Map.prototype.forEach((value, key, set) => {}, thisArg) <mark style="color:red;">【推荐】</mark>
* Map.prototype.entries()
* Map.prototype.keys()：Map.prototype.values的别名
* Map.prototype.values()

<mark style="color:red;">**注意**</mark>：Map的遍历顺序就是插入顺序

### 3、数据类型转换

todo

## 二、WeakMap

### 1、只能用对象作为key

```javascript
const wm = new WeakMap();

wm.set(1, 1); // TypeError: Invalid value used in weak set
wm.set('1', '1'); // TypeError: Invalid value used in weak set
wm.set(true, 'true'); // TypeError: Invalid value used in weak set
wm.set(null, null); // TypeError: Invalid value used in weak set
wm.set(undefined, undefined); // TypeError: Invalid value used in weak set

wm.set(Symbol(), 'symbol');
wm.set({}, 'obj');

wm.set(() => {}, 'fn');
wm.set([], 'array');
wm.set(new Map(), 'map');
wm.set(new Set(), 'set');
```

### 2、key是弱引用

Map的key是对象，使用完很容易忘记清除，增加内存泄漏的风险，WeakMap就是为解决此问题而诞生的。WeakMap的key都是弱引用（这也是叫Weak的原因），即不参与引用计数，垃圾回收机制运行时直接忽略此处引用。

<mark style="color:red;">**注意：**</mark>WeakMap 弱引用的只是key，value依然是正常引用。

### 3、无法遍历

因为key又可能随时会被回收，所以WeakMap内部的成员数量不稳定，所以没有提供size属性，也不支持遍历。

## 三、区别

<table><thead><tr><th width="114.33333333333331">区别</th><th>Map</th><th>WeakMap</th></tr></thead><tbody><tr><td>成员类型</td><td>不限</td><td>对象</td></tr><tr><td>成员函数和属性</td><td><ul><li>Map.prototype.set(key, value)</li><li>Map.prototype.get(key)</li><li>Map.prototype.has(key)</li><li>Map.prototype.delete(key)</li><li>Map<mark style="color:red;">.prototype.size</mark></li><li>Map<mark style="color:red;">.prototype.clear()</mark></li><li>Map<mark style="color:red;">.prototype.forEach()</mark></li><li>Map<mark style="color:red;">.prototype.values()</mark></li><li>Map<mark style="color:red;">.prototype.keys()</mark></li><li>Map<mark style="color:red;">.prototype.entries()</mark></li></ul></td><td><ul><li>WeakMap.prototype.set(key, value)</li><li>WeakMap.prototype.get(key)</li><li>WeakMap.prototype.has(key)</li><li>WeakMap.prototype.delete(key)</li></ul></td></tr><tr><td>遍历</td><td>支持</td><td>不支持</td></tr><tr><td>适用场景</td><td>对key的类型要求宽松，尽量替代对象</td><td>不关心垃圾回收机制（比如存储DOM节点）</td></tr></tbody></table>



参考：

* [https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/Map](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/Map)
* [https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/WeakMap](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/WeakMap)
* [https://es6.ruanyifeng.com/#docs/set-map#Map](https://es6.ruanyifeng.com/#docs/set-map#Map)
