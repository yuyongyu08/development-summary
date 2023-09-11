---
description: react的逃生舱
---

# useEffect

### 作用

和非React的外部系统交互，比如发起请求（建立服务器连接）、调用浏览器API（设置定时器）等



#### `useEffect(setup, dependencies?)` <a href="#useeffect" id="useeffect"></a>

setup函数包含两部分：

* **setup** code：组件挂载（插入到DOM中）时调用
* **cleanup** code（可选）：组件卸载（从DOM中移除）时调用，主要用于清除遗留逻辑，比如清除定时器、断开服务器连接等

执行顺序：

* 首次挂载（开发模式）：setup => cleanup => setup
* 首次挂载（生产模式）：setup
* 重新渲染：cleanup（旧值） => setup（新值）
* 组件卸载：cleanup

> After every re-render with changed dependencies, React will first run the cleanup function (if you provided it) with the old values, and then run your setup function with the new values.

### 示例

<pre class="language-jsx"><code class="lang-jsx">import { useEffect } from 'react';
import { createConnection } from './chat.js';

function ChatRoom({ roomId }) {
  const [serverUrl, setServerUrl] = useState('https://localhost:1234');

  useEffect(() => {
    const connection = createConnection(serverUrl, roomId);
    connection.connect();
    return () => {
<strong>      connection.disconnect();
</strong>    };
  }, [serverUrl, roomId]);
  // ...
}
</code></pre>



### 关键点

* 只可在组件顶层执行，不可放到循环或条件中
* 如果不和外部系统通信，没必要使用Effect
* 使用`useLayoutEffect`代替：（没理解～）

> If your Effect wasn’t caused by an interaction (like a click), React will let the browser **paint the updated screen first before running your Effect.** If your Effect is doing something visual (for example, positioning a tooltip), and the delay is noticeable (for example, it flickers), replace `useEffect` with [`useLayoutEffect`.](https://react.dev/reference/react/useLayoutEffect)



> Even if your Effect was caused by an interaction (like a click), **the browser may repaint the screen before processing the state updates inside your Effect.** Usually, that’s what you want. However, if you must block the browser from repainting the screen, you need to replace `useEffect` with [`useLayoutEffect`.](https://react.dev/reference/react/useLayoutEffect)





