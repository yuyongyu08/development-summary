# 常见类型判断

## 一、判断方法总结

**数据举例：**

```javascript
const types = {
  str: 'hello',
  strObj: new String('hello'),
  num: 123,
  bool: true,
  'null': null,
  'undefined': undefined,
  symbol: Symbol(),
  bigInt: 9007199254740991n,
  fun: function () {},
  arr: [],
  obj: {},
  map: new Map(),
  weakMap: new Map(),
  set: new Set(),
  weakSet: new Set()
}
```

**结果统计：**

<table><thead><tr><th width="133">类型</th><th width="125">typeof</th><th width="220">instanceof [constructor]</th><th>Object.prototype.toString.call</th></tr></thead><tbody><tr><td><mark style="color:red;">string</mark></td><td>"string"</td><td>false</td><td>"[object String]"</td></tr><tr><td><mark style="color:red;">number</mark></td><td>"number"</td><td>false</td><td>"[object Number]"</td></tr><tr><td><mark style="color:red;">boolean</mark></td><td>"boolean"</td><td>false</td><td>"[object Boolean]"</td></tr><tr><td><mark style="color:red;">null</mark></td><td>"object"</td><td>false</td><td>"[object Null]"</td></tr><tr><td><mark style="color:red;">undefined</mark></td><td>"undefined"</td><td>false</td><td>"[object Undefined]"</td></tr><tr><td><mark style="color:red;">symbol</mark></td><td>"symbol"</td><td>false</td><td>"[object Symbol]"</td></tr><tr><td><mark style="color:red;">object</mark></td><td>"object"</td><td><mark style="color:green;">true</mark></td><td>"[object Object]"</td></tr><tr><td>bigint</td><td>"bigint"</td><td>false</td><td>"[object BigInt]"</td></tr><tr><td>function</td><td>"function"</td><td><mark style="color:green;">true</mark></td><td>"[object Function]"</td></tr><tr><td>array</td><td>"object"</td><td><mark style="color:green;">true</mark></td><td>"[object Array]"</td></tr><tr><td>map</td><td>"object"</td><td><mark style="color:green;">true</mark></td><td>"[object Map]"</td></tr><tr><td>weakMap</td><td>"object"</td><td><mark style="color:green;">true</mark></td><td>"[object WeakMap]"</td></tr><tr><td>set</td><td>"object"</td><td><mark style="color:green;">true</mark></td><td>"[object Set]"</td></tr><tr><td>weakSet</td><td>"object"</td><td><mark style="color:green;">true</mark></td><td>"[object WeakSet]"</td></tr></tbody></table>



**总结：**

* **`Object.prototype.toString.call`**是通用判断方法（万金油😂），可以作为兜底方案
* 其他推荐判断方式：
  * 基本数据类型（除了null）、BigInt ：用 **`type of`**判断
  * null：用**`Object.prototype.toString.call`**判断
  * 函数：优先用**`type of`**
  * Array：优先使用**`Array.isArray`**
  * Object：精准判断用**`Object.prototype.toString.call`**
  * Map、WeakMap、Set、WeakSet：优先使用**`instanceof`**



## 二、应用：深拷贝

[深拷贝](qian-kao-bei-shen-kao-bei.md)主要考查：类型判断 + 递归



