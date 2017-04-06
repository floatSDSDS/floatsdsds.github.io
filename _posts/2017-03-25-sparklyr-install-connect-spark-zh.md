---
layout: post
title: "用sparklyr安装并连接Spark"
excerpt: "嘛，一开始是跟官方教程走的，然而很明显官方教程中并未包含环境配置，`spark_install`命令也没有对断点传输进行优化"
tags:
  - coding
  - bugs
  - R
  - ZH
---



## 梗概
- 本文主要描述在纯使用R的相关包`sparklyr`安装并连接Spark的经验，并主要解决两个官方教程和网上教程中没有的两个问题：
  1. 在不稳定的网络环境下用压缩包*.tar安装Spark
  2. 设置系统环境变量JAVA_HOME
- 环境：
  - system: x86_64, linux-gnu, Ubuntu 16.04
  - R version 3.3.3 (2017-03-06)
  - RStudio version 1.0.136
  - sparklyr version 0.5.3

## 安装

直接跟着教程走的话，只需要运行以下代码：
```
install.packages("sparklyr")
library(sparklyr)
spark_install(version = "1.6.2")
```
但由于网络不稳定，每次没有下载完就会报错，并重新下载，而实际上，sparklyr是提供了从压缩包进行安装的指令的，下载地址我使用spark_install()函数的默认版本。
在运行后会看到提示信息，得到安装包临时缓存目录和下载链接，将下载链接丢到下载器中运行。文中使用的下载器是FlareGet，
注意FlareGet是收费的，只有10天免费使用期限，其实ubuntu下还有许多其他好用的下载器，如uGet，SteadyFlow，kGet和XDM。下载好后填入tarfile如
```
spark_install_tar(“<your-tarfile-path>")

```
安装好后检查安装路径和版本
```
spark_installed_versions()
spark_install_dir()
```

## 连接
在连接过程我又遇到了问题，事实上，我已经在`/etc/profile`
和 `/etc/environment` 加入了环境变量并source过，但是sparklyr还是返回报告说我没有设置JAVA_HOME
```
export JAVA_HOME=/usr/lib/jdk/jdk1.8.0_121
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
```
运行官方教程代码如下：
```
> sc <- spark_connect(master = "local")
```
返回错误显示没有设置JAVA_HOME
```
Error in force(code) :
  Failed while connecting to sparklyr to port (8880) for sessionid (6026): Gateway in port (8880) did not respond.
Path: /home/floatsd/.cache/spark/spark-1.6.2-bin-hadoop2.6/bin/spark-submit
Parameters: --class, sparklyr.Backend, --jars, '/home/floatsd/R/x86_64-pc-linux-gnu-library/3.3/sparklyr/java/spark-csv_2.11-1.3.0.jar','/home/floatsd/R/x86_64-pc-linux-gnu-library/3.3/sparklyr/java/commons-csv-1.1.jar','/home/floatsd/R/x86_64-pc-linux-gnu-library/3.3/sparklyr/java/univocity-parsers-1.5.1.jar', '/home/floatsd/R/x86_64-pc-linux-gnu-library/3.3/sparklyr/java/sparklyr-1.6-2.10.jar', 8880, 6026


---- Output Log ----
  JAVA_HOME is not set

---- Error Log ----
```

最终解决方式是在R Console中运行`Sys.setenv`设置变量如下：设置完后连接成功
```
Sys.setenv(JAVA_HOME="/usr/lib/jdk/jdk1.8.0_121")
```

-----
#### 问题遗留：其实我还是没有搞清楚这两者变量间的关系，以及在R中Sys.setenv改变的变量存储在哪里
