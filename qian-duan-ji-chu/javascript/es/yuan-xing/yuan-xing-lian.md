# 原型链

### &#x20;**示例：**

```javascript
function Person(name) {
    this.name = name;
}

let person = new Person('yuyongyu');
```



### **原型链：**

<figure><img src="../../../../.gitbook/assets/流程图 (3).jpg" alt=""><figcaption></figcaption></figure>

### **总结：**

1. 引用类型都有`__proto__`属性，称为**原型**
2. 引用类型的原型指向构造函数的**原型对象**，即`prototype`属性
3. 构造函数的原型对象中`constructor`属性指向自身





参考：

* [https://juejin.cn/post/6934498361475072014](https://juejin.cn/post/6934498361475072014)
* [https://juejin.cn/post/6844903950001373192](https://juejin.cn/post/6844903950001373192)
