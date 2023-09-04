---
description: 组件缓存
---

# memo

### 作用：

当组件接受props没有变化时，跳过组件的re-render。

> 对比props是否有变化是一种**浅对比**，底层用的<mark style="color:green;">**`Object.is()`**</mark>
>
> * Object.is(3, 3) : true
> * Object.is({}, {}) : false
> * Object.is(\[], \[]) : false
> * Object.is(() => {}, () => {}) : false

### 示例：

{% code fullWidth="false" %}
```jsx
import { memo } from "react";

const List = memo(function ({ items }) {
  console.log("rendering children");

  return (
    <ul>
      {items.map((item) => (
        <li key={item}>{item}</li>
      ))}
    </ul>
  );
});

export default List
```
{% endcode %}



### 应该给每个组件都包裹一层memo吗？

没必要。

> Keep in mind that `memo` is completely useless if the props passed to your component are _<mark style="color:red;">always different</mark>,_ such as if you pass an object or a plain function defined during rendering. This is why you will often need [`useMemo`](https://react.dev/reference/react/useMemo#skipping-re-rendering-of-components) and [`useCallback`](https://react.dev/reference/react/useCallback#skipping-re-rendering-of-components) together with `memo`.







