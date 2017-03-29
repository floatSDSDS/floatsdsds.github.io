---
layout: post
title: "今天的主题是安利——文献搜索管理"
excerpt: "搬砖学术居家旅行必备良品，文献检索管理一条龙贴心到家。"
tags:
  - tools
  - productive
  - ZH
---

> Warning: 本文只提供关键词、概括和成吨的传送门，是安利不是教程ლ(╹◡╹ლ)

- 老实说，第一次建立起知识管理的概念也才二月初，在知网批量导出文献目录时，知网向我推荐了E-study。这应该是我使用过的第一款知识管理工具，从此打开新世界的大门。赞美知网（而且能读取*.caj的知识管理工具人家垄断了→_ →）。
- 本文按文献检索，知识管理工具和RSS三大部分来介绍打开新世界大门后，无比亢奋的作者头顶deadline折腾出的一些经验。

## 1. 文献检索
- 这里的检索不是指下载文献本身，可以理解为在初入领域或者要查对应课题时，得到如文献的标题，发表年份，作者、被引量、引用文献和DOI等文献的属性。利用这些信息可以进行进一步的分析，快速建立起对本领域的overview，直观了解最近的热点问题等。

### 得到文献索引
- [Web of Science, WOS](https://login.webofknowledge.com/error/Error?PathInfo=%2F&Alias=WOK5&Domain=.webofknowledge.com&Src=IP&RouterURL=https%3A%2F%2Fwww.webofknowledge.com%2F&Error=IPError)检索并导出列表。这里注意，WOS需要你注册登录，而且很多机构的账号不能远程访问，只能在注册ip下进行访问。
- 同样原理如知网也可以批量导出文献检索信息，免费的哟☆。
- [publish or perish](http://www.harzing.com/resources/publish-or-perish)，这是一款学术爬虫工具，每次可以爬取一段时间内高影响力的论文，我一般使用的引擎是谷歌学术，一次有一千条的上限。

### 文献分析工具
- [citespace](http://cluster.cis.drexel.edu/~cchen/citespace/)
  - 正宗国人出品，赞美陈老师李老师。
  - 可以分析共同关键词、高引论文、机构作者研究实力、时间线上的热点迁移、学术资源迁移等问题，以网络图、时序图等方式可视化体现，在帮助自己快速理解的同时可以出报表。缺点是内存优化糟糕，我的老电脑根本用不起来，共被引网络分析基本一年暑假电脑就炸了。
- [hitcite](https://zhuanlan.zhihu.com/p/20902898)
  - 和citespace同性质，不过我还没试过。原作者已经不维护了，所幸作者的学生是个好同志，链接中是他新放出来的发布链接，修复了bugsss。
- 当然了还有大量替代软件：Bibexcel, CoPalRed, IN-SPIRE等等，放一个[老司机横向测评](http://blog.hit.edu.cn/rjx/post/114.html)，不瞒你们说还有一篇这玩意还有一篇[综述](http://s3.amazonaws.com/academia.edu.documents/30896322/mjcobo-softwareReview-2011.pdf?AWSAccessKeyId=AKIAIWOWYYGZ2Y53UL3A&Expires=1490797449&Signature=MMG%2BHktEP6ljJyW1a8AKCIyYxKU%3D&response-content-disposition=inline%3B%20filename%3DScience_mapping_software_tools_Review_an.pdf)，这里还有[一个亲切的整理页面](http://sci2s.ugr.es/scimat/links.html)。
- 数据下下来技能点够的小伙伴还可以自己做个小分析嘛。#时间序列、文本挖掘、图挖掘走起✧(≖ ◡ ≖✿)。

### 文献获取渠道
- [谷歌学术](http://scholar.google.com/)，有了他，其他免费论文库如re*chgate，seman*cholar就都可以不用上了，毕竟都集成在谷歌学术里了（还包括部分学校的论文库，作者自己公开出来的open access，总之就是赞美谷歌）。许多论文可以直接找到pdf。
- 学校：但凡高校基本都会给各大出版社及机构上税，有的高校还出了自己的内部学术搜索引擎，总的来说通过这些机构的服务器就能愉快的免费下论文，简直福利满满。
- 图书馆：没有楼上福利的么，找一处离家近的图书馆，这个我没用过，是网上看来听别人讲的也没考证。图书馆也有购买部分数据库，并且全国和国图联网共用数据库？我倒是上国图整了个账号，但没能用起来……
- 其实吧，真没渠道没资源还急用的可以某宝呀╰(*°▽°*)╯！

####p.s.当然还有一种更简易不用学的方法是找牛逼的综述，或者关键词检索后，看几篇高引的引用本领域牛逼的文章基本就找到了：）。

## 知识管理工具
- 知识（文献）管理工具（reference management software），
- [搜索Comparison of reference management software、*attribute matrix](http://guides.library.utoronto.ca/c.php?g=250610&p=1671260)等关键词可得，维基百科上还有个大个儿的，信息量大到让你一眼都不想看的那种。不过我找了一下发现有对比数据库的也只有[维基](https://en.wikipedia.org/wiki/Comparison_of_reference_management_software)
- 先说目前主流普适全能文献管理工具的基本features：
  - 它应该是一个牛逼的pdf阅读器，注释当然要美观让人心情舒畅；
  - 如果界面能好看一点就更好了（Endnote躺枪）；
  - 要能够让用户设置个性化tag；
  - 它可以识别论文的doi和基础信息，在文献库内自动建立文献信息索引，并实现各种搜索，比如按作者按机构按关键词按年份；
  - 可以与本地PC文件系统完美融合在一起（监视本地文件夹）；
  - 云端功能可以加分，不过云端服务往往要加钱(: )～；
  - 文献索引批量导入导出。
- 我自己使用的是mendeley，因为颜值高还免费<(*￣▽￣*)/。

## RSS

> - RSS（简易信息聚合）是一种消息来源格式规范，用以聚合经常发布更新数据的网站，例如博客文章、新闻、音频或视频的网摘。RSS文件（或称做摘要、网络摘要、或频更新，提供到频道）包含全文或是节录的文字，再加上发布者所订阅之网摘数据和授权的元数据。
> - Really Simple Syndication“聚合真的很简单”就是RSS的英文原意。把新闻标题、摘要（Feed）、内容按照用户的要求，“送”到用户的桌面就是RSS的目的。RSS一词有时候大体上意为社会性书签，包括各种RSS的不同格式。例如，Blogspace对使用网摘于一集成器内之动作标为RSS info和RSS reader。虽然它的第一个句子就包含明确的Atom格式：“RSS和Atom文件能够用简单的格式从网站更新消息至你的电脑!”
> - RSS摘要可以借由RSS阅读器、feed reader或是aggregator等网页或以桌面为架构的软件来阅读。标准的XML档式可允许信息在一次发布后通过不同的程序阅览。用户借由将网摘输入RSS阅读器或是用鼠标点取浏览器上指向订阅程序的RSS小图标之URI（非通常称为URL）来订阅网摘。RSS阅读器定期检阅是否有更新，然后下载给监看用户界面。
> - RSS可以是以下三种解释中任一种的缩写，但其实这三者都是指同一种不联合供稿（Syndication）的技术：
RSS 1.0（Really Simple Syndication）
RSS 0.91, RSS 1.0（RDF（Resource Description Framework）Site Summary）
RSS 0.9 and 1.0（Rich Site Summary）

- 说人话就是：所有内容发布者通用的发布格式，就跟小广播一样，什么牌子的录音机都能听，打比方的话大概可以理解为自定义超高度个性化定制但不带推荐功能的知乎日报。可以拿它追很多独立内容生产者如我这样的小透明的发布内容→_→，很多期刊会议实验室都会发布自己的RSS。检索一遍的印象是，现在大多数人已经不怎么用RSS了但这玩意不那么容易死，学术界还蛮心水他的。大概是这么个意思。
