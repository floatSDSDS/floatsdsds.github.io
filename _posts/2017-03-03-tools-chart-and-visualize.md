---
layout: post
title: "今天的主题是安利————图表图标流程图"
excerpt: "搬砖学术居家旅行必备良品，图表图标流程图无脑拿下，数据做出来要也要美美的画。"
tags:
  - tools
  - productive
  - ZH
---

> Warning: 本文只提供关键词、概括和成吨的传送门，是安利不是教程ლ(╹◡╹ლ)
> 如果你要问为什么全文没有一张预览图，大概是因为我懒吧 #待补图

- 其实啦要说代码画图我只会用R，用python和js等其他语言的小伙伴请左转搜索[* data visualization](https://www.google.co.jp/search?newwindow=1&rlz=1C1CHZL_zh-CN__738JP738&espv=2&q=*+data+visualization&oq=*+data+visualization&gs_l=serp.3..0i7i30k1l10.4666.5046.0.5437.2.2.0.0.0.0.239.447.2-2.2.0....0...1c.1.64.serp..0.2.445.AarteUU3uMQ)，\*可以替换成自己常用的语言╭( ･ㅂ･)و ̑̑。
- 咦一搜怎么这里好像有个现成的很fancy的整理贴#[The 38 best tools for data visualization](http://www.creativebloq.com/design-tools/data-visualization-712402)，和我下面说的有重叠，以及我发现里面好多看起来都很有趣，有的看起来比我用过的那些还牛逼……一起来拔草见者有份啊。
- 本文分两节，第一节推荐的工具不需要编程知识，第二节推荐的工具都有R的调用接口或者为R的包。

## 最喜欢鼠标点点的轻量化在线网页工具了对不对！
- 如果你也一样喜欢轻量化在线工具╭( ･ㅂ･)و ̑̑,保持电脑的干净清爽， 在新工作开始前试着搜索 `* online` 吧，虽然熟悉一款好工具往往能用很久，但是总是有那么多新生代作品值得发掘，总有那么多闲的蛋疼的开发者们喜欢脑洞大开，让我们说生出Wow还能这样的惊喜和赞叹。
  - [chartblocks](http://www.chartblocks.com/en/)
    - 常见图表，柱状图堆叠图饼图等常用静态图，优点是极端容易操作，但免费web版功能较少，而且只能到处png格式。
  - [amcharts](https://www.amcharts.com/)
    - 在线动态交互式图表绘制，数据轻松导入，基础图表类型随意组合，可调参数极为丰富，可以下载可以发布到网页。
  - [processon](https://www.processon.com/diagrams)
    - 国人制作的在线流程图，思维导图绘制工具。特点同样是极端容易操作，控件基本够用，泳道图稍稍有点蠢，思维导图布局不够灵活。
  - [youidraw](http://youidraw.com/)
    - 最后来乱入一个在线绘图工具。操作流畅，可以针对绘图或logo进行优化（有不同画笔和控件可以选择，logo有不同设计库），手残党的福音，非专业设计人士的福音，不想装笨重的photoshop偶尔想临时画个小图标时的福音。嘛，其实拿矩形框就可以做出所有的logo了（双击，在边上拉点魔改，有自动对齐），比如我的撞月蠢鸟logo。需要注意的是有水印，有背景，请结合其他可以透明化背景工具食用。


## 赞美R
- ggplot2
  - 八卦：Hadeley Wickham的作品，男神级书呆，使用R的小伙伴即使即使可能还没听过他的名字，但大概每个人都得接触他开发的包。httr、dplyr、ggplot、reshape2、devtools都是他的作品。
  - features：注意ggplor2处理的数据要整理成长数据格式，绘制各种静态图表。
- plotly
  - features：绘图！绘动态的图！可以让ggplot2绘制的图表动起来！本身也有独立的绘图功能，另外有多种语言的接口。
  - 接口：R、python、matlab、javascript
- igraph
  - features：网络分析及可视化的包，可视化其实只是它的一部分功能，它还集成了大量图和网络的分析工具。
  - 接口：R、python、C
- networkD3
  - features：网络分析及可视化包，生成交互式网络可视化，我觉得他的可视化颜值比igrap要高。
- leaflet
  - features：生成交互式可视化地图，颜值极高，操作极简单，可以和shiny结合食用；遗憾的是我还没找到将它和igraph一起用起来的方法。
  - 接口：R、python、js
