---
description: 变量缓存
---

# useMemo

### 作用

缓存计算结果



### 示例

```jsx
import { useMemo } from 'react';

function TodoList({ todos, tab, theme }) {
  const visibleTodos = useMemo(() => filterTodos(todos, tab), [todos, tab]);
  // ...
}
```



### 是用场景

* 数值计算函数确实很慢，并且依赖项变化较少
* 为了防止包裹了`memo`的子组件无效渲染
* 计算结果作为其他hook（比如`useMemo`、`useEffect`）的依赖项



### 是否有必要所有的计算都用`useMemo`？

没有必要。

处处是用useMemo是一种过度优化，有时候会适得其反



> Also, not all memoization is effective: a single value that’s “always new” is enough to break memoization for an entire component.

（没有特别理解官方这句话的意思）



