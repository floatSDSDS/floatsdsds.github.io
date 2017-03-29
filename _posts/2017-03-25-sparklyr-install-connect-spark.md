---
layout: post
title: "sparklyr finally connected to Spark"
excerpt: "I followed offical tutorial at first,
but it does not work will either with a unstable network environment or
a fresh system."
tags:
  - coding
  - bugs
  - R
  - EN
---


I was trying to use R package `sparklyr` to install Spark and
connect to it. Since it is my second day with my new
laptop@Thinkpad_T460P, just installed Ubuntu 16.04 alongside
Windows 10. Apparently, I had not installed Java JDK yet.


## Introduction
- This passage may help you with the following 2 problems:
  1. Easily Install Spark with `sparklyr` under a unstable
  network environment.
  2. Solve the problem "JAVA_HOME is not set" when connecting to Spark.
- This passage works under the following environment:
  - system: x86_64, linux-gnu, Ubuntu 16.04
  - R version 3.3.3 (2017-03-06)
  - RStudio version 1.0.136
  - sparklyr version 0.5.3

## Easily Install
At first, I followed the official tutorial as every one else
would prefer. It seems pretty simple, the only thing I need to
do is running the following code.

```
install.packages("sparklyr")
library(sparklyr)
spark_install(version = "1.6.2")
```
Then here comes out the first problem: I can't successfully download the Spark
*.tar when ever the network breaks for more than a threshold time, the downloading process
would break off.

To solve the problem I found another command when typing `?spark_install`,
install spark from a tar file.

```
spark_install_tar(tarfile)
```
So I used a download manager(there are lots of good Linux download
managers like uGet, SteadyFlow, kGet, XDM, etc.). After installing, we can
check for the installing path and version.

```
spark_installed_versions()
spark_install_dir()
```

## Easily Connect
Speak at the first: I had set JAVA_HOME variables both in `/etc/profile`
and `/etc/environment`, along with sourcing the configuration.

```
> sc <- spark_connect(master = "local")
```
I met the second problem when connecting to Spark.

```
Error in force(code) :
  Failed while connecting to sparklyr to port (8880) for sessionid (6026): Gateway in port (8880) did not respond.
Path: /home/floatsd/.cache/spark/spark-1.6.2-bin-hadoop2.6/bin/spark-submit
Parameters: --class, sparklyr.Backend, --jars, '/home/floatsd/R/x86_64-pc-linux-gnu-library/3.3/sparklyr/java/spark-csv_2.11-1.3.0.jar','/home/floatsd/R/x86_64-pc-linux-gnu-library/3.3/sparklyr/java/commons-csv-1.1.jar','/home/floatsd/R/x86_64-pc-linux-gnu-library/3.3/sparklyr/java/univocity-parsers-1.5.1.jar', '/home/floatsd/R/x86_64-pc-linux-gnu-library/3.3/sparklyr/java/sparklyr-1.6-2.10.jar', 8880, 6026


---- Output Log ----
  JAVA_HOME is not set

---- Error Log ----
```

Since it claimed `JAVA_HOME is not set`, I set JAVA_HOME using R
command `Sys.setenv`as below.

```
Sys.setenv(JAVA_HOME="/usr/lib/jdk/jdk1.8.0_121")
```

-----
#### Problem remains: I still get confused with where this system environment stored, I thought it should be `/etc/environment` before.
