---
layout: post
title: "{igraph}网络生成封装方法"
excerpt: "整理了利用Igraph R接口生成网络方法，详细参数需要查阅文档"
tags:
  - r-package
  - R
  - ZH
---

- igraph本身是一个基于C的库，并封装了R和python的接口，可以极其简单的生成常用模型如随即图，小世界和无标度网络。文中整理部分函数名（没有整理详细的接口），具体查阅[igraph](http://igraph.org/r/doc/)文档可得，大多数模型都可以指定是否有向，有无自环。

- ER随机图，即指在给定n个顶点后，规定每两个顶点之间都有 p 的概率连起来（两两点间独立判断），经典ER可调用以下函数生成，其中gnm的m参数是指网络中的总边数。
  Erdos, P. and Renyi, A., On random graphs, Publicationes Mathematicae 6, 290–297 (1959).
    - `erdos.renyi.game()`, Generate random graphs according to the Erdos-Renyi model
    - `gnp()`/`sample_gnp()`, Generate random graphs according to the G(n,p) Erdos-Renyi model
    - `gnm()`/`sample_gnm()`, Generate random graphs according to the G(n,p) Erdos-Renyi model
- 小世界网络SmallWorld
    - WS: 一个环状的规则网络开始：网络含有N个结点，每个节点向与它最临近的K个节点连出K条边，并满足N>>K>>ln(N)>>1。之后随机化重连：以概率p随机地重新连接网络中的每个边，即将边的一个端点保持不变，而另一个端点取为网络中随机选择的一个节点。其中规定，任意两个不同的节点之间至多只能有一条边，并且每一个节点都不能有边与自身相连。这样就会产生pNK/2条长程的边把一个节点和远处的结点联系起来。改变p值可以实现从规则网络(p=0)向随机网络(p=1)转变。
    `smallworld()`/`sample_smallworld()`
    - NW：一个环状的规则网络开始：网络含有N个结点，每个结点向与它最临近K个结点连出K条边，并满足N>>K>>ln(N)>>1。之后随机化加边：以概率p在随机选取的一对节点之间加上一条边。其中，任意两个不同节点之间至多只能有一条边，并且每一个节点都不能有边与自身相连。改变p值可以实现从最临近耦合网络(p=0)向全局耦合网络(p=1)转变。当p足够小和N足够大时，NW小世界模型本质上等同于WS小世界模型。在igraph中没有直接生成NW模型的函数，可以按照定义来生成。
    ```
    library(igraph)
    g <- graph.lattice(length=100, dim=1, circular=TRUE)
    g2 <- erdos.renyi.game(100, 1/100)
    g3 <- g %u% g2
    g3 <- simplify(g3)
    plot.igraph(g3, vertex.size = 1,vertex.label = NA, layout=layout_in_circle)
    https://stackoverflow.com/questions/38202448/generate-small-world-model-in-igraph-using-newman-watts-algorithm
    ```
- 无标度网络ScaleFree
    - BA模型:从一个较小的网络开始，逐步加入新的节点，每次加入一个，并从这个新节点向原有图连出m条边，连接方式为优先考虑度高的点（preferential attachment），建立连边时，与原有某节点$s_i$连接的可能性为：
    $${\mathbb  {P}}_{i}={\frac  {d_{i}}{\sum _{{j=1}}^{n}d_{j}}}$$
    - `pa()`,`sample_pa()`
    - 按幂率分布生成网络：`sample_fitness_pl()`.
- 其他演化规则
    - 指定演化规则：`pa_age()`/`sample_pa_age()``
    - 节点不止为一种（如二分图 三分图）：
      - 二分图: `bipartite()`/`sample_bipartite()`
      - 三分图：`traits()`/`sample_traits()`/`traits_callaway()`/`sample_traits_callaway()`
    - 根据度分布建图：`degseq()`/`sample_degseq()`；
      - 其中method参数意义为:
          - "simple": 可以生成无向图和有向图，会产生重边和自环。（这些重边和自环可以被删除，但这样就不遵循期望的度分布了）
          - "simple.no.multiple":楼上的升级版，没有自环和重边，不存在迭代上限
          - "vl": 比楼上两位复杂一点，只能生成无向网络，用这个方法时不能使用`in.deg`参数，首先生成一个符合度分布的无向图，然后进行部分重连，然后使用Monte-Carlo算法把整个图随机化。
    - `sample_k_regular()`, 每个节点拥有相同的度的图，regular graph
    - `growing()`, `sample_growing()`, create a random graph by simulating its stochastic evolution.
    - `sample_grg()`, `grg()`, Generate a random graph based on the distance of random point on a unit square
    - `sample_last_cit()`, creates a graph, where vertices age, and gain new connections based on how long ago their last citation happened.



- p.s. 实际测试在Windows上用R调用同样的数据时间和内存占用都远远差于在ubuntu上用C调用（即使是在ubuntu上用R调用，表现也出色很多），only吐槽。
