## Jstack命令

### 官方解释

> **jstack** prints Java stack traces of Java threads for a given Java process or core file or a remote debug server. For each Java frame, the full class name, method name, 'bci' (byte code index) and line number, if available, are printed. With the -m option, jstack prints both Java and native frames of all threads along with the 'pc' (program counter). For each native frame, the closest native symbol to 'pc', if available, is printed.
>
> ## OPTIONS
>
> - **-F**
>   Force a stack dump when 'jstack [-l] pid' does not respond.
> - **-l**
>   Long listing. Prints additional information about locks such as list of owned java.util.concurrent [ownable synchronizers](https://docs.oracle.com/javase/7/docs/api/java/util/concurrent/locks/AbstractOwnableSynchronizer.html).
> - **-m**
>   prints mixed mode (both Java and native C/C++ frames) stack trace.
> - **-h**
>   prints a help message.
> - **-help**
>   prints a help message

以上为oracle官方对jstack命令的简介和使用说明

[https://docs.oracle.com/javase/7/docs/technotes/tools/share/jstack.html](https://docs.oracle.com/javase/7/docs/technotes/tools/share/jstack.html)

从上面的信息可以得 `Jstack`主要用来查看某个Java进程内的线程堆栈信息



### 使用jstack定位运行时异常 ⭐️⭐️⭐️

当Java程序运行时出现异常，我们可以使用jstack命令来定位和分析具体问题。

下面简单介绍一下如何使用jstack定位到具体的出错的位置

共5个步骤：

1. jps 查看java进程pid
1. top -Hp pid 找出该进程内最耗费CPU的线程
1. printf "%x\n" 1787 得到十六进制值为6fb
1. jstack pid > file.log 通过jstack 把该进程的所有线程堆栈打印到file.log中
1. vi file.log 打开文件搜索 6fb 找到具体出问题的代码



## Arthas工具

// todo



## 补充

### 1. 如果服务是docker部署的方式

找到docker服务的pid

```shell
docker ps
```

进入docker

```shell
docker exec -it {pid} /bin/bash
```

再使用Jstack命令



### 2. jstack统计线程数

```shell
/opt/java8/bin/jstack -l 28367 | grep 'java.lang.Thread.State' | wc -l
```