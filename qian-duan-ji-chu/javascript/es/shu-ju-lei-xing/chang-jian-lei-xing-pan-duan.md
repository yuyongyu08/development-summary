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

| 类型        | typeof                                        | instanceof \[constructor]              | Object.prototype.toString.call |
| --------- | --------------------------------------------- | -------------------------------------- | ------------------------------ |
| string    | <mark style="color:green;">"string"</mark>    | false                                  | "\[object String]"             |
| number    | <mark style="color:green;">"number"</mark>    | false                                  | "\[object Number]"             |
| boolean   | <mark style="color:green;">"boolean"</mark>   | false                                  | "\[object Boolean]"            |
| null      | <mark style="color:green;">"object"</mark>    | false                                  | "\[object Null]"               |
| undefined | <mark style="color:green;">"undefined"</mark> | false                                  | "\[object Undefined]"          |
| symbol    | <mark style="color:green;">"symbol"</mark>    | false                                  | "\[object Symbol]"             |
| bigint    | <mark style="color:green;">"bigint"</mark>    | false                                  | "\[object BigInt]"             |
| function  | <mark style="color:green;">"function"</mark>  | <mark style="color:green;">true</mark> | "\[object Function]"           |
| array     | "object"                                      | <mark style="color:green;">true</mark> | "\[object Array]"              |
| object    | "object"                                      | <mark style="color:green;">true</mark> | "\[object Object]"             |
| map       | "object"                                      | <mark style="color:green;">true</mark> | "\[object Map]"                |
| weakMap   | "object"                                      | <mark style="color:green;">true</mark> | "\[object WeakMap]"            |
| set       | "object"                                      | <mark style="color:green;">true</mark> | "\[object Set]"                |
| weakSet   | "object"                                      | <mark style="color:green;">true</mark> | "\[object WeakSet]"            |



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



