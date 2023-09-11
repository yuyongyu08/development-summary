---
description: hook
---

# hook依赖列表

### 语法

useXXX(**target** any, **dependences** \[])



### 参数

**dependences**的不同写法，决定了对**target**的处理

* 如果dependences不传：每次渲染，target都会被处理
* 如果dependences传空数组：只有在首次渲染，target才会被处理，之后的渲染都不再处理
* 如果dependences按需传值：依赖项有变化，target就会被处理

