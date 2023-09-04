# 子组件的无效渲染

### 什么是无效渲染？

组件重新渲染后结果和渲染前没有差异



### 为什么会无效渲染？

父组件传递给子组件的props（比如对象、数组、函数）可能只是引用地址变了，但value并没有变化，导致子组件渲染前后没有不同。

例如：

```jsx
export default function () {
  let [checked, setChecked] = useState(false);
  
  const items = useMemo(() => ["one", "two", "three"].map((item) => item.toUpperCase()), []);
  
  function handleCheck() {
    setChecked(!checked);
  }

  return (
    <div>
      <input type="checkbox" checked={checked} onChange={handleCheck} /> 大小写敏感
      <List items={items} />
    </div>
  );
}


function List ({ items }) {
  console.log("rendering children");
  return (
    <div>
      <h3>List:</h3>
      <ul>
        {items.map((item) => (
          <li key={item}>{item}</li>
        ))}
      </ul>
    </div>
  );
};
```

###

### 如何避免无效渲染？

可以从父组件和子组件两个维度，结合子组件的props分析，给出对应的解决方案。

**1、父组件要做的优化：**

props的值类型：

* 数据
  * 基本类型：无需处理
  * 引用类型
    * 普通引用类型：<mark style="color:green;">**useMemo()**</mark>
    * 计算后得到的引用类型：<mark style="color:green;">**useMemo()**</mark>
* 函数：<mark style="color:green;">**useCallback()**</mark>



**2、子组件要做的优化：**

* 用<mark style="color:green;">**memo()**</mark>包裹



注意两者优化的优化必须同时生效才能避免无效渲染，即：<mark style="color:green;">**useMemo() + useCallback() 、useCallback() + useCallback()**</mark>





