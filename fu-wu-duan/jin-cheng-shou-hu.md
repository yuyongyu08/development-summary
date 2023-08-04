# 进程守护

## 一、为什么要守护进程

在终端启动一个node应用后，如果关闭终端，则node应用也会被kill掉。

所以，为了后台运行不受终端关闭的影响，需要启动守护进程。一般的网络服务都是以守护进程的方式运行。

## 二、进程的原理

1. 父进程通过 `fork` 等方法创建子进程
2. 在子进程中创建新回话（调用系统函数 setsid）
3. 改变子进程工作目录（如：`"/"` 或 `"/usr"` 等）
4. 父进程终止，子进程由 init 进程接管

## 三、常用第三方工具

* [pm2](https://github.com/Unitech/pm2)
* [forever](https://github.com/foreversd/forever)
* [supervisor](https://github.com/Supervisor/supervisor)



参见：

* [https://tsejx.github.io/node-guidebook/system/process/daemon/](https://tsejx.github.io/node-guidebook/system/process/daemon/)
* [https://cnodejs.org/topic/57adfadf476898b472247eac](https://cnodejs.org/topic/57adfadf476898b472247eac)

