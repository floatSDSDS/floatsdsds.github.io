---
layout: post
title: "Naming Game文献整理"
excerpt: "对Naming Game做Introduction时的文献笔记及整理"
tags:
  - Note
  - ZH-EN
---

## 1. 定义
- Consensus emerges through local negotiations between pairs of agents, **in the absence of any central co-ordination**[1].
- is characterized by three temporal regions:[1]
  1. initially the words are invented
  2. they spread throughout the system inducing a reorganization process of the inventories
  3. this process eventually triggers the final convergence towards the global consensus
- **configuration is always reached for finite systems**
## 2. 意义&作用
- Captures the essential features leading a population to agree on the use of a semiotic convention[1].
- allows to study the self-organized mechanism leading to the emergence of a linguistic convention or a communication system in a population of agents.[1]
- 特点在于，in which an agent takes the state of a neighbor, is replaced by a two-step negotiation process, memory effects play a central role **（这里没有看懂）**
- social interactions[1]
- web tagging systems[1]
- sensor networks[1]
- emergence of communication conventions[2]
- robots will have to build up and negotiate their own communication systems[2]

## 3. 延伸
### 3.1. 历史
- First proposed(minimal naming game): [2] (originally introduced in the field of robotics)
### 3.2. 意见动力学
#### 3.2.1 定义
- An interesting problem consists in determining whether a population of individuals reaches a consensus state and, in case, which process leads to such a situation.
#### 3.2.2 物理意义&应用
- Evolution of language[1]
- New language constructs usually propagate along an S-shaped curve with a rather sudden transition towards global agreement[2]
- social tagging system for the web[1,2]
- optimize artificial semiotic dynamics[2]
### 3.3. 同类模型
- [1] Ising-like models(applied to study of the social behavior of individuals).
- [1] Voter model
## 4. 摘抄
- [1] a population of N identical agents on the vertices of a generic undirected graph.
- [1] each agent disposes of an **internal inventory**
- [1] underlying graph(初始网络)
- Nw定义：
  - [1]the total number of words in the system
- Nd定义：
  - [1] the number of different words
- S定义：
  - [1] defined as the probability of a successful interaction at a given time.
- Before the transition, the system builds up non-trivial scale-invariant correlations[2]
- Zipf-like law 它可以表述为：在自然语言的語料庫裡，一个单词出现的频率与它在频率表里的排名成反比。所以，频率最高的单词出现的频率大约是出现频率第二位的单词的2倍，而出现频率第二位的单词则是出现频率第四位的单词的2倍。这个定律被作为任何与冪定律概率分布有关的事物的参考。
- global coordination[2]


## 2. 按文章概要
- [1]
  - 仿真规模参数设计：N=1000, k=10,
  - 分析方法：使用系统总词数Nw(t)，总unique词数Nd(t)，成功率S(t)，按时间画图，文中总结出gaimng演化动态三个阶段
  - 所得结论：①动态三个时间段 ②Naming Game模型受到初始网络拓扑结构影响很大 ③小世界属性和联通属性能够得到较短的收敛时间和memory占用（③存疑）
  - 可用观点：
    1. This final configuration is always reached for finite systems. However, the dynamical process leading to the final homogeneous configuration depends strongly on the topological properties of the underlying graph.
    2. the model converges very slowly, and the reason is related to the formation of many different local clusters of agents with the same unique word, that grow by means of coars- ening dynamics.
    3. 在complete graph中，第二阶段的时间为O(N^1.5)
    4. consensus is reached in a time $t_{conv}/N~N^{2/d}$
  - 疑问和没看懂：
    - clusters of agents with the same unique word grow by means of coarsenring dynamics. 包括这里说的average cluster size grows. 所以这里cluster是指同观点的节点簇？那么类簇的边界是怎么定义的。
    - in a d-dimensional lattice, the maximum memory per agent is finite(while it scales as $\sqrt(N)$ for the complete graph)
    - finite connectivity combined with the small-world property ensure the best performances in terms of memory usage and time to reach convergence. 但是没有看到文中说infinite的情况是什么意思
    - t/N取log后收敛时间不为1.5
    - 文中小世界网络使用complete graph，（mean-field case-MF?
    - 文中得出了memory和N无关，只和平均度有关的结论，但并没有做相关的实验
- [2] 听说这是naming Game开山之作来着（趴）
  - 仿真规模参数设计：
  - 分析方法：
  - 所得结论：
  - 可用观点：
  - 疑问和没看懂：

## 参考文献
[1] Baronchelli, A., Dall'Asta, L., Barrat, A. & Loreto, V. (2007). The role of topology on the dynamics of the Naming Game. European Physical Journal: Special Topics, 143(1), pp. 233-235. doi: 10.1140/epjst/e2007-00092-0
[2] Baronchelli, A., Felici, M., Loreto, V., Caglioti, E. Steels, LucSharp transition towards shared vocabularies in multi-agent systems, 2006 P06014
