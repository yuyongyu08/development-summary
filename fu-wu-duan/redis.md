---
description: Redis
---

# Redis

### 安装

```bash
brew install redis
```

### 启动&停止

此方式关闭会停止

```bash
redis-server
```

后台启动（关闭命令窗口依然在运行，<mark style="color:green;">推荐</mark>）：

```bash
brew services start redis
```

停止：

```
brew services stop redis
```

查看redis信息:

```bash
brew services info redis
```

### 交互

模式一：`redis-cli` + 命令



模式二（沉浸式，有语法提示，<mark style="color:green;">推荐</mark>）：

```bash
redis-cli -h [host] -p [port]
```

建立连接后，进入Redis REPL，开始使用redis命令

### 命令

```bash
# 增
SET my-key 'hello redis!'


# 删

# 改
SET my-key 'hi redis'

# 查
keys * 
get my-key

```

#### 增

```bash
# string
SET my-key 'hello redis!'

#hash
HSET my-hash-key name rory age 18
```

#### 删

```bash
DEL my-key
```

#### 改

```bash
SET my-key 'hi redis'
```

#### 查

<pre class="language-bash"><code class="lang-bash"><strong>keys * 
</strong><strong>get my-key
</strong>
# 确定key的类型
TYPE mykey

# hash
HGET my-hash-key name
HGETALL  my-hash-key
</code></pre>

