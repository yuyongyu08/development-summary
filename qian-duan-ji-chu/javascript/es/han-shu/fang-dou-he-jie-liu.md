# 防抖和节流

## 一、防抖（debounce）

**概念：**

在约定的延迟时间后响应，如果在等待期间重复触发，则重置等待时间



**实现：**

```javascript
function debounce(callback, delay) {
    let timer = null;

    return (...args) => {
        clearTimeout(timer); // 必须先清除已存在的宏任务，否则重复触发时回调有可能被执行
        timer = setTimeout(() => {
            callback(...args)
        }, delay)
    }
}
```

**简析：**

* 利用柯里化返回函数
* 函数每次被执行时，先清除老的定时器，然后重新生成新的定时器

**应用：**

手机号、邮箱的输入校验；防止按钮重复点击



## 二、节流（throttle）

**概念：**

以约定的延迟时间作为执行间隔，其执行节奏不受重复触发影响

**实现：**

```javascript
function throttle(callback, delay) {
    let timer = null;

    return (...args) => {
        if (!timer) {
            timer = setTimeout(() => {
                callback(...args)
                timer = null; // 不能使用clearTimeout，否则最后一次触发注册的宏任务会丢失
            }, delay)
        }
    }
}
```

**简析：**

* 利用柯里化返回函数
* 函数每次被执行时，判断定时器是否存在
  * 存在：则直接跳过
  * 不存在：重新生成新的定时器，并在回调生成后重置定时器

**应用：**

收集用户鼠标轨迹；检索输入框下拉联想



## 三、可视化演示

入口：[https://yuyongyu08.github.io/debounce-vs-throttle/](https://yuyongyu08.github.io/debounce-vs-throttle/)
