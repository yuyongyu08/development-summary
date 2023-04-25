---
description: vuer-outer
---

# vue-router

### 特点

SPA => 前端路由：URL变化页面不刷新（不和服务器交互）



### 原理

#### hash模式

```javascript
window.addEventListener('hashchange', function matchAndUpdate(){
    // 匹配hash，做页面渲染
})
```



#### history模式

```javascript
window.addEventListener('pushState', function matchAndUpdate(){ 
    // 路由跳转
})

window.addEventListener('replaceState', function matchAndUpdate(){ 
    // 路由跳转
})
```

```javascript
window.addEventListener('popstate', function matchAndUpdate(){ 
    // 匹配路由，做页面渲染 
})
```
