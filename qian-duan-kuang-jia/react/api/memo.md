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

每次操作复选框都会出发子组件的重新渲染，一定要配合父组件中对props进行useMemo()包裹使用才有效。

### 应该给每个组件都包裹一层memo吗？

官方原文：

> If there is no perceptible lag when your component re-renders, `memo` is unnecessary.Keep in mind that `memo` is completely useless if the props passed to your component are _<mark style="color:red;">always different</mark>,_ such as if you pass an object or a plain function defined during rendering. This is why you will often need [`useMemo`](https://react.dev/reference/react/useMemo#skipping-re-rendering-of-components) and [`useCallback`](https://react.dev/reference/react/useCallback#skipping-re-rendering-of-components) together with `memo`.

没必要。

* 捆绑优化：memo必须配合useMemo和useCallback一起使用才有效，这样就要求虽有props都要做额外的处理
* 代码质量：处处都是用memo可能让组件的难以debug，以及可读性降低



