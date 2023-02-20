---
description: string
---

# 1-string

## String原型方法

### 1、操作

* [String.prototype.repeat(times)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/repeat): 【重复times次后拼接返回，time是大于0的正数，1则不重复】
* [String.prototype.replace(regexp|substr, newSubStr|function)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/replace)：【对第一个匹配项进行替换】
* [String.prototype.replaceAll(regexp|substr, newSubStr|function)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/replaceAll)：【对所有匹配项进行替换】

### 2、截取

* [String.prototype.slice(start, end)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/slice)：【截取\[start, end)之间的字符】
* [String.prototype.substr(start\[, length\]) ](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/substr)<mark style="color:red;">`[待废弃]`</mark>
* [String.prototype.substring(start, end)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/substring)：【截取\[start, end)之间的字符】

### 4、拼接

* [String.prototype.concat(str0\[, str1, ...)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/concat)：【拼接字符串】
* [String.prototype.padStart(targetLen\[, str\])](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/padStart)：【用str进行从头部填充到最长targetLen的字符串，默认用空格填充】
* [String.prototype.padEnd(targetLen\[, str\])](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/padEnd)：【同padStart，区别从尾部开始填充】

### 3、查找

* [String.prototype.search(regexp)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/search)：【返回符合规则的索引，否则返回-1】
* [String.prototype.startsWith(str\[, start\]) ](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/startsWith)：【判断字符串是否从start开始以str开头】
* [String.prototype.endsWith(str\[, start\])](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/endsWith)：【判断字符串是否从start开始以str结尾】
* [String.prototype.match(regexp)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/match)：【返回所有符合规则的结果组成的数组】
* [String.prototype.includes(str\[, start\])](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/includes)：【从start位置开始算是否包含str】

### 6、位置

* [String.prototype.charAt(index)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/charAt)：【返回index位置的字符】
* [String.prototype.charCodeAt(index)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/charCodeAt)：【返回index位置的字符的UTF-16 编码单元】
* [String.prototype.indexOf(str\[, start\])](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/indexOf)：【返回str从start开始算第一次出现的位置】
* [String.prototype.lastIndexOf(str\[, start\])](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/lastIndexOf)：【同indexOf，从后往前查】

### 5、去空

* [String.prototype.trim()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/Trim)：【返回清除两端空格后的字符串】
* [String.prototype.trimStart()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/trimStart)：【返回清除头部空格后的字符串】
* [String.prototype.trimEnd()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/trimEnd)：【返回清除尾部空格后的字符串】

### 7、转换

* [String.prototype.split(](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/split)separator\[, limit])：【按照separator进行拆分成数组，limit是数组最大长度】
* [String.prototype.toLowCase()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/toLowerCase)：【返回全小写后的字符串】
* [String.prototype.toUpperCase()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String/toUpperCase)：【返回全大写后的字符串】





## String和Array的同名函数

| String                         | Array                         |
| ------------------------------ | ----------------------------- |
| String.prototype.concat()      | Array.prototype.concat()      |
| String.prototype.includes()    | Array.prototype.includes()    |
| String.prototype.indexOf()     | Array.prototype.indexOf()     |
| String.prototype.lastIndexOf() | Array.prototype.lastIndexOf() |
| String.prototype.slice()       | Array.prototype.slice()       |





