---
layout: post
title: "CRAN Task View——时空数据"
excerpt: "顾名思义，时空数据即是指同时带有时间属性和地理属性的数据。本文主要介绍了与时空数据处理有关的包和他们的简介。主体为CRAN Task View中SpatioTemporal的翻译，在翻译的基础上加入了个人的理解，尽量让他像人话。"
tags:
  - translate
  - R
  - ZH
---


> 顾名思义，时空数据即是指同时具有时间属性和地理属性的数据。本文主要介绍了R中与时空数据处理有关的包和他们的简介。主体为CRAN Task View中SpatioTemporal的翻译，以后有空会改成更好看的形式，比如“对比矩阵”和可视化表示，帮助理解。
> [CRAN Task View - SpatioTemporal](https://cran.r-project.org/web/views/SpatioTemporal.html)
> 文中用花括号`{}`表示包名
> 文中有一些奇妙的术语或小词，大概意思知道但不敢乱翻，就保留了英文。

- 一键安装文中出现的所有包（）：
```C
install.packages("ctv")
library("ctv")
install.views("SpatioTemporal")
# 没有翻墙情况下请使用镜像
install.views("SpatioTemporal"，repos = <choose-a-mirror>)
```


## 介绍常用的时空类型数据格式
- **表格（data.frame）**
  表格形式包括长表格，时间类型表格和空间类型表格，其中时间类型表格中，一张表只表示一个属性（特征），行表示地点，列表示时间；空间类型表格反过来，行为时间序列，列则为不同地点。长表格中包含多个属性，空间、时间和各个特征都是独立的字段。
  - **长表格**：时空数据可以由长数据来表示，包含经度、纬度、时间的三个字段，或者经纬度由一个地理地区的标识来代替。比如[plm](https://cran.r-project.org/web/packages/plm/index.html)中的linear panel models数据集，对象就是与索引（如国家，州）对应的。这些索引（包括地理名字或数字）可以与空间上的坐标或多边形对应起来。如[Pebesma](http://www.jstatsoft.org/v51/i07/)([(2012, Journal of Statistical Software)](http://www.jstatsoft.org/v51/i07/))中的例子。这些表格类型的数据集往往包含多个属性，一般以二维长表格形式存储，每条记录通常包含记录的索引，时间和所有属性。
  - **时间类型表格**：当考虑属性为单一属性时，另一种数据存储形式为时间范围意义上的表格，每条记录单元由记录本身和时间组成（每一行为记录单元，列则为时间）。利用[googleVis](http://www.gapminder.org/world/)可以利用R来像[gapminder](http://www.gapminder.org/)一样分析数据。
  - **空间类型表格**：典型例子如Irish Wind数据集（加载`{gstat}`包，用`data(wind)`进行调取。），行为时间序列，列则为不同的地点。`stConstruct{spacetime}`可以处理上述的三种长、时间范围和空间范围的表格。
- **类**
  - **通用类**：`{spacetime}`中提供了多种S4型的时空数据标准类，包括`full space-time grids`（每条记录包含所有的记录和时间），`sparse space-time grids`（定期数据，但可能有部分缺失数据，所有的观察对象是同步的），`irregular space-time data`（每一个观察有自己的时间序列），同时还有轨迹类型的数据。同时，`{spacetime}`也可处理`sp`、`xts`类型对象，可以处理所有的所有的`sp`空间类型（包括点、线、多边形和网格），同步或非同步（regular and irregular）的时间序列，同时提供一些拓展的分析方法（数据拆选，数据融合，各种数据类型的画图等）。
  - **专用类**：
    - **地理统计数据(Geostatistiacl)**：`{SpatioTemporal}`实现了一个S3类`STdata`，可以处理多种空间数据、时间数据或时空数据，以实现对时空模型的分析。具体的介绍在其CRAN页面的[vignettes](https://cran.r-project.org/web/packages/SpatioTemporal/vignettes/ST_intro.pdf)中有。
    - **栅格数据(Gridded/raster)**：`{raster}`可以处理一系列的rasters数据，每一个数据集可以反映为一系列时间序列模型（use `setZ` on brick or stack）。
    - **网格数据(Lattice)**：`{surveillance}`实现了`sts`类，来表示一个地区的情况，这里用数字来表示定期的时间序列（和`POSIXct`一样不存在对象）。
    - **点的特征(Point patterns)**：`{stpp}`提供了类`stpp`来表示一个时空点的特征。`{stppResid}`提供了`stwin`类，类中定义了一个长方形时空窗口，和包括了点的特征的`stpp`类。`{spatstat}`实现了`ppx`类来处理时空坐标，这些特征点类都没有表示自己支持明确的时间参考系统。\*这里一段整个都很虚
    - **轨迹数据(Trajectory)**：`{adehabitatLT}`中提供了一种轨迹类`ltraj`和部分分析方法，`{move}`和`{trip}`则分别实现了`{sp}`类轨迹拓展类。

## 不同格式对应的分析方法（包）
- **地理学统计数据**
- **点的特征**
- **网格数据**
- **移动对象，轨迹数据**
  - `{adehabitatLT}`提供了一系列分析动物行为轨迹的工具，包括随机游走仿真和住址估计。
  - `{trip}`提供了一系列访问、操作追踪动物轨迹的工具，可以根据动物轨迹起始时间、速度进行筛选。

## 可视化
- `{rasterVis}`提供了一系列`z`数据格式（`RasterStack`和`RasterBrick`）的可视化功能，它的[官方页面](https://oscarperpinan.github.io/rastervis/)提供了很多实例。
- `{plotKML}`提供了一系列将时空数据转换为KML文件形式的方法，利用kML文件可以使用如Google Earth等扩展可视化工具来展示数据。
- `{googleVis}`是谷歌图表的R接口，其中提供了一系列`spacetime`类的绘制实例。
- `{stpp}`和`{splancs}`提供了动画和3D交互图表的绘制方法（使用rgl）展示时空数据点的特征。
- `{mvtsplot}`提供了杜仲时间序列绘图，也包含时空数据的例子。
