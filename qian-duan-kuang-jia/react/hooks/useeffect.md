---
description: react的逃生舱
---

# useEffect

### 作用

和非React的外部系统交互，比如发起请求（建立服务器连接）、调用浏览器API（设置定时器）等



#### `useEffect(setup, dependencies?)` <a href="#useeffect" id="useeffect"></a>

setup函数包含两部分：

* 函数体：组件挂载（插入到DOM中）时调用
* 清除函数（可选）：组件卸载（从DOM中移除）时调用，主要用于清除遗留逻辑，比如清除定时器、断开服务器连接等

执行顺序：

每次重新渲染，先用旧值执行cleanup函数，然后用新值执行setup函数

> After every re-render with changed dependencies, React will first run the cleanup function (if you provided it) with the old values, and then run your setup function with the new values.

### 示例

```jsx
import { useEffect } from 'react';
import { createConnection } from './chat.js';

function ChatRoom({ roomId }) {
  const [serverUrl, setServerUrl] = useState('https://localhost:1234');

  useEffect(() => {
    const connection = createConnection(serverUrl, roomId);
    connection.connect();
    return () => {
      connection.disconnect();
    };
  }, [serverUrl, roomId]);
  // ...
}
```



### 关键点

