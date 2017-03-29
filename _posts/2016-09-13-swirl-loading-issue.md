---
layout: post
title: "R-swirl无法正确载入问题"
excerpt: "Error in library(swirl) : there is no package called swirl"
tags:
  - coding
  - bugs
  - R
  - ZH
---

```
> library(swirl)
Error in library(swirl) : there is no package called 'swirl'
```
- 官方给出的在我电脑上然并卵的解决方案
	- Did you install swirl with install.packages("swirl")? If so, then something went wrong with installation. There are a few reasons this might occur. 是否安装swirl包，如果没有请正确安装；
	- Do you have R version 3.0.2 or later? This is required for the most recent version of swirl. 确保R版本在3.0.2以上；
	- Are you behind a firewall or proxy server at work? If you have access to a personal computer, that's often the easiest fix. 关闭防火墙，也可能是网络代理问题，或者如校园网，公司内网等可能造成问题；
	- Do you have full permissions on your computer? Again, using a personal computer may be your best bet. 电脑权限问题；

- 最后使用解决方案：
	- 重新安装`swirl`，安装时改变dependencies变量， 如
	```
	install.packages("swirl",dependencies = T)
	```
