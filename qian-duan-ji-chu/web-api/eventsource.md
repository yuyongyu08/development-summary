---
description: AI 打印机效果
---

# EventSource

HTTP协议中服务端的推送

## 服务端

```javascript
const http = require('http');

// 将歌词变成一个数组
let song = [
  '我', '懒', '得', '写', '你', '谷', '搜', '到', '处', '皆', '只', '因', '你', 
  '太', '美', '浅', '唱', '动', '人', '说', '不', '出', '我', '试', '着', '多', 
  '看', '你', '一', '眼', '却', '发', '现', '我', '已', '沉', '溺', '于', '你', 
  '的', '镜', '头', '里', '只', '因', '你', '太', '美', '所', '以', '我', '多', 
  '看', '了', '一', '眼', '只', '因', '我', '太', '傻', '所', '以', '我', '放', 
  '不', '开', '你', '的', '手', '只', '因', '你', '太', '美', '所', '以', '我', 
  '做', '了', '个', '梦', '梦', '见', '你', '在', '微', '笑', '我', '在', '注', 
  '视', '只', '因', '你', '太', '美', '所', '以', '我', '放', '了', '你', '的', 
  '手', '所', '以', '我', '会', '微', '笑', '因', '为', '你', '太', '美', 'end'
];

http.createServer((req, res) => {

  if (req.url === '/article') {
    res.writeHead(200, {
      // 开启 Server-sent events
      'Content-Type': 'text/event-stream',
      'Cache-Control': 'no-cache',
      // 保持连接
      'Connection': 'keep-alive',
      // 允许跨域
      'Access-Control-Allow-Origin': '*'
    });
    let index = 0;

    // 模拟每隔0.5s向前端推送一次
    setInterval(() => {
      const s = song[index];

      if (s) {
        res.write(`data: ${song[index]}\n\n`);
      } else {
        res.write('0');
      }
      index++;
    }, 500);
  }
}).listen(3000);

console.log('Server running at http://localhost:3000/');
```

**关键点**：<mark style="color:red;">`'Content-Type': 'text/event-stream'`</mark>

## 客户端

```javascript
// 建立连接
const source = new EventSource('http://localhost:3000/article');
let str = '';
// 接收信息
source.onmessage = function (e) {
  if (e.data === 'end') {
    // 判断end，关闭连接
    source.close()
  }

  str += e.data
  // 实时输出字符串
  console.log(str)
};
```

关键点：使用`EventSource`API发起请求，并通过监听事件做相应操作

参考：

* [https://mp.weixin.qq.com/s/4lVYGfq26ckpDds297XxXg](https://mp.weixin.qq.com/s/4lVYGfq26ckpDds297XxXg)
* [https://www.ruanyifeng.com/blog/2017/05/server-sent\_events.html](https://www.ruanyifeng.com/blog/2017/05/server-sent\_events.html)
* [https://developer.mozilla.org/en-US/docs/Web/API/Server-sent\_events/Using\_server-sent\_events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent\_events/Using\_server-sent\_events)
