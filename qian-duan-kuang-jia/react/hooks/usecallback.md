---
description: 函数缓存
---

# useCallback

### 作用

缓存函数，重新渲染时，如果依赖项有变化，将新函数返回；如果没有变化，将上次计算所得的函数返回。



### 示例

```jsx
import { useCallback } from 'react';

function ProductPage({ productId, referrer, theme }) {
  const handleSubmit = useCallback((orderDetails) => {
    post('/product/' + productId + '/buy', {
      referrer,
      orderDetails,
    });
  }, [productId, referrer]);
  // ...
}
```



### 原理

```jsx
function useCallback(fn, dependencies) {
  return useMemo(() => fn, dependencies);
}
```



### 适用场景

* 为了防止用`memo`包裹的子组件无效渲染
* 目标函数是其他hook的依赖项，比如`useCallback`、`useEffect`

### 是否有必要所有函数都包裹`useCallback`？

没必要。

> Also, not all memoization is effective: a single value that’s “always new” is enough to break memoization for an entire component.

（没太理解这句话）

###

### &#x20;
