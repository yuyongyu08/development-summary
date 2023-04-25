# Nginx

官网：[入口](https://nginx.org/)



### 基本原理

nginx由两种进程组成；

* 主进程（master process）：一个，负责读取、计算配置文件，维护工作进程
* 工作进程（work process）：多个，负责处理处理请求

### 安装：

通过brew：

```bash
brew install nginx 
```

> <mark style="color:red;">注意安装后的提示信息</mark>，配置文件一般在/usr/local/nginx/conf/nginx.conf，通过homebrew安装的nginx，则在/opt/homebrew/etc/nginx/nginx.conf

### 查看进程

```bash
ps -ax | grep nginx
```

### 主要命令

<pre class="language-bash"><code class="lang-bash">sudo nginx                    # 启动 Nginx
<strong>sudo nginx -s reload          # 热重启，向主进程发送信号，重新加载配置文件
</strong>sudo nginx -s reopen.         # 重启 Nginx
<strong>sudo nginx -s stop            # 快速关闭
</strong>sudo nginx -s quit            # 等待工作进程处理完成后关闭
sudo nginx -T                 # 查看当前 Nginx 最终的配置
sudo nginx -t -c &#x3C;配置路径>    # 检查配置是否有问题，如果已经在配置目录，则不需要-c
</code></pre>

> 可以通过访问[http://localhost:8080/](http://localhost:8080/)验证是否启动成功

> 配置文件更新原理：主进程接收到重载信号，它会校验并应用新配置文件。如果校验通过，主进程会启动一个新工作进程并停掉老的工作进程；如果校验失败，则会回滚到老的配置文件，老的工作进程会接收到一个停止接收新请求连接的命令，将当前请求处理完后退出。

### 指令集

参见：[入口](https://nginx.org/en/docs/http/ngx\_http\_proxy\_module.html#proxy\_pass)



参考资料：

* [https://juejin.cn/post/6844904144235413512](https://juejin.cn/post/6844904144235413512)
* [https://juejin.cn/post/7082655545491980301](https://juejin.cn/post/7082655545491980301)
* [https://juejin.cn/post/7152812186937589773](https://juejin.cn/post/7152812186937589773)

