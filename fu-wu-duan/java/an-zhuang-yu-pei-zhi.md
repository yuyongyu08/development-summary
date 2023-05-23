# 安装与配置

## 下载Mac版的JDK安装器（.dmg）

[SDK版本列表](https://www.oracle.com/java/technologies/downloads/archive/)





## 默认安装目录：

```bash
/Library/Java/JavaVirtualMachines/
```

> IDEA也提供下载安装，会安装到：/Users/mac/Library/Java/JavaVirtualMachines



## 查看已安装的所有版本：

```bash
/usr/libexec/java_home -V
```

> 命令含义：在 macOS 系统中查找 Java 路径，列出系统中所有安装的 Java 版本及其安装路径，-V 表示显示版本信息

## 切换JDK版本：（只需要写主版本号）

```bash
export JAVA_HOME=`/usr/libexec/java_home -v 17` 
```



> 命令含义：
>
> 1、`/usr/libexec/java_home` 命令，并传入参数 `-v 17`，以获取 Java 17 的安装路径
>
> 2、将该路径赋值给 JAVA\_HOME 环境变量，以便其他程序可以通过该变量找到 Java 17 的安装路径



## 卸载JDK

本质：删除指定JDK的文件夹即可

```bash
rm -rf /Library/Java/JavaVirtualMachines/jdk-17.jdk
```

