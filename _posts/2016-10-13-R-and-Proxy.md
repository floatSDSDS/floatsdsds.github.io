---
layout: post
title: "R与墙和平共处"
excerpt: "在天朝由于不可描述的原因，要下载的东西服务器在境外就很容易慢的让人想哭。常用幸福安心翻墙工具VPN，VPS。不过这里不是讲翻墙的，事实上由于不可描述的干预和影响，VPN和VPS经常会在不可抗力影响下间歇下线。本文内容包括：(i)利用镜像无脑安包；(ii)从github上安装包；(iii)从打包文件本地安装包；(iii)过程中遇到的一个奇妙error及其解决；(iv)为RStudio设置代理。"
tags:
  - coding
  - bugs
  - tricks
  - ZH
---

## 1. 镜像大法
- 首先最简单易用的方法是使用镜像，国内cran镜像列表如下：
```
https://mirrors.tuna.tsinghua.edu.cn/CRAN/	TUNA Team, Tsinghua University
http://mirrors.tuna.tsinghua.edu.cn/CRAN/	TUNA Team, Tsinghua University
https://mirrors.ustc.edu.cn/CRAN/	University of Science and Technology of China
http://mirrors.ustc.edu.cn/CRAN/	University of Science and Technology of China
https://mirror.lzu.edu.cn/CRAN/	Lanzhou University Open Source Society
http://mirror.lzu.edu.cn/CRAN/	Lanzhou University Open Source Society
http://mirrors.xmu.edu.cn/CRAN/	Xiamen University
```
- 在安装包时记得设置参数`repos`即可，举例：
```
install.packages("<your-package-to-install>",repos="https://mirrors.tuna.tsinghua.edu.cn/CRAN/")
```

## 2. 从github上安装
- 另一个方法是直接下载包或从github安装（发布在cran库上的包需要经过严格的审核，所以很多自由独立的包开发出来，
会直接托管在github上），从github上安装包的方法如下：
```
install.packages("devtools")  #安装devtools包
library(devtools) #载入devtools包
install_github("A","B") #其中A为包名，B为作者名
```

## 3. 网络问题的报错及外部方法解决→\_→
- 其实这篇博文的出发点是因为我连续几次正常安装包失败报错如下： 先运行安装包的命令
```
install.packages("rafalib")

```

- 会返回如下错误

``` 
Warning in install.packages :
  InternetOpenUrl failed: ''
Warning in install.packages :
  InternetOpenUrl failed: ''
Warning in install.packages :
  unable to access index for repository https://cran.rstudio.com/src/contrib:
  cannot open URL 'https://cran.rstudio.com/src/contrib/PACKAGES'
Warning in install.packages :
  InternetOpenUrl failed: ''
Warning in install.packages :
  InternetOpenUrl failed: ''
Warning in install.packages :
  unable to access index for repository http://www.stats.ox.ac.uk/pub/RWin/src/contrib:
  cannot open URL 'http://www.stats.ox.ac.uk/pub/RWin/src/contrib/PACKAGES'
Installing package into ‘C:/Users/floatSD/Documents/R/win-library/3.3’
(as ‘lib’ is unspecified)
Warning in install.packages :
  InternetOpenUrl failed: ''
Warning in install.packages :
  InternetOpenUrl failed: ''
Warning in install.packages :
  unable to access index for repository https://cran.rstudio.com/src/contrib:
  cannot open URL 'https://cran.rstudio.com/src/contrib/PACKAGES'
Warning in install.packages :
  InternetOpenUrl failed: ''
Warning in install.packages :
  InternetOpenUrl failed: ''
Warning in install.packages :
  unable to access index for repository http://www.stats.ox.ac.uk/pub/RWin/src/contrib:
  cannot open URL 'http://www.stats.ox.ac.uk/pub/RWin/src/contrib/PACKAGES'
Warning in install.packages :
  package ‘rafalib’ is not available (for R version 3.3.1)
Warning in install.packages :
  InternetOpenUrl failed: ''
Warning in install.packages :
  InternetOpenUrl failed: ''
Warning in install.packages :
  unable to access index for repository https://cran.rstudio.com/bin/windows/contrib/3.3:
  cannot open URL 'https://cran.rstudio.com/bin/windows/contrib/3.3/PACKAGES'
Warning in install.packages :
  InternetOpenUrl failed: ''
Warning in install.packages :
  InternetOpenUrl failed: ''
Warning in install.packages :
  unable to access index for repository http://www.stats.ox.ac.uk/pub/RWin/bin/windows/contrib/3.3:
  cannot open URL 'http://www.stats.ox.ac.uk/pub/RWin/bin/windows/contrib/3.3/PACKAGES'
Warning: unable to access index for repository https://cran.rstudio.com/src/contrib:
  cannot open URL 'https://cran.rstudio.com/src/contrib/PACKAGES'
Warning: unable to access index for repository http://www.stats.ox.ac.uk/pub/RWin/src/contrib:
  cannot open URL 'http://www.stats.ox.ac.uk/pub/RWin/src/contrib/PACKAGES'
```

- 网上查找类似问题，有人回复说是网络问题，防火墙问题等。根据这个思路，我推测自己遇到的原因是之前用一个API频次
不小心过高被封锁了，理由是换了VPN节点后可以正常安装包（sob）。

## 4. 为R的运行设置代理[1]
- 当然前提是有代理可以用，方法也很简单，编辑环境变量配置文件，加入代理设置：
```
file.edit('~/.Renviron')
```
- 在打开的文件中加入http代理设置如下：
```
http_proxy=http://proxy.dom.com/  #代理服务器地址
http_proxy_user=user:passwd #用户名和密码，没有用户名和密码时可省略
```
- 同理还可以设置如ftp_proxy类型代理，具体参见[官方文档](https://curl.haxx.se/libcurl/c/libcurl-tutorial.html)

-----
## Reference
[1][RStudio Support: Configuring R to Use an HTTP or HTTPS Proxy](https://support.rstudio.com/hc/en-us/articles/200488488-Configuring-R-to-Use-an-HTTP-or-HTTPS-Proxy)
