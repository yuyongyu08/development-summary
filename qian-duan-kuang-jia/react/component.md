---
description: React开发的代码组织单位
---

# Component

React的由类组件完全改为函数式组件，每个组件都是一个函数。

一个最基本的函数式组件包含：入参（props）、出参（JSX）

```
export default function Profile({avatarURL, name}) {
  return (
    <img src={avatarURL} alt={name}/>
  )
}
```



疑惑：

* 函数式组件每次重新渲染整个函数都会重新执行一遍
  * 是否有性能问题？
  * 对于异步数据岂不是有重新请求的问题？
