---
description: 抽离复用逻辑的方式
---

# Hooks

### 定义：

* 是一个函数
* 函数名：必须已use开头
* 入参：接受响应式变量、事件处理函数
* 出参：按需返回，也可以不返回

### 示例：

```jsx
export function useChatRoom({ serverUrl, roomId, onReceiveMessage }) {
  const onMessage = useEffectEvent(onReceiveMessage);

  useEffect(() => {
    const options = {
      serverUrl: serverUrl,
      roomId: roomId
    };
    const connection = createConnection(options);
    connection.connect();
    connection.on('message', (msg) => {
      onMessage(msg);
    });
    return () => connection.disconnect();
  }, [roomId, serverUrl]);
}
```



### 作用：

* 复用性：将通用的逻辑抽离封装，方便复用
* 可读性：将独立的逻辑抽离，降低组件复杂度，方便维护

