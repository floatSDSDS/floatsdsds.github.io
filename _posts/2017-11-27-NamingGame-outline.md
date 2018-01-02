---
layout: post
title: "Naming Game文献整理"
excerpt: "对Naming Game做Introduction时文章outline"
tags:
  - Note
  - ZH-EN
---

## Naming Game Related
### A self-organizing spatial vocabulary(1995)
- 思路流程
  - This paper explores self-organization as the primary mechanism for the formation of a vocabulary. the work reported on the computational experiment in which a group of distributed agents develop ways to **identify each other using names or spatial descriptions**
  - 该机制可以应对新加进来的agents，和系统需要概念的未知膨胀
  - 文中作者进行了一系列基于以下两个假设的实验：
    - 语言是一个自适应系统，因此语言学可以与其他自适应系统如生物系统，鸟群蚁群等。没有一个个体可以控制整个族群，也没有哪一个个体可以看到语言的全貌。
    - 语言会自发的变得复杂。
  - 本文的实验主要基于第一个假设
- 可用观点
  - 语言的演化会变得复杂是出于优化交流效率的目的和需求。同时应对现实生活中严苛的环境。
- 实验设计
  - agents之间以
- 引述
  - Grammar is innate[1]
- 疑问
  - it says there has been put forward some hypothesis that language arises and develops as a consequence of genetic mutations[8].
  - 如果没有看错的话，这个虽然也是agent之间的命名，但与namingGame的规则还存在较大差异。只能说



### Sharp transition towards shared vocabularies in multi-agent systems（2006）
- 思路流程
  - 摘要：如何解释人们对某个词汇的使用能够自发收敛（已知现象：语言学研究中表明，语言中新生词汇或用法往往沿S形曲线增长）。本文设计了一个自组织的微观模型。随着系统（网络）规模的增长，收敛曲线愈发陡峭(phenomena of slow spreading followed by a sudden transitions to a global conventions)。这一现象可以解释人类语言可以在广泛的人群中流行；可以优化人造符号的传播过程。two-word [The origins of ontologies and communication conventions in multi-agent systems, 1998], 使系统可以依据环境自发创造交流词汇(emergent communication systems)，而不依赖于预先定义，可以适应未知的环境。
      - 简述语言的传播过程
      - 在线打标签与语言传播过程的不谋而合
      - agents的自组织实验[The synthetic modeling of language origins,1997; Natural language from artificial life,2002]
    - 本文中没有underlying topology，视为全联通网络（文中描述为interaction后建立连边的动态网络）
  - Naming Game的三个假设
    - 全联通网络
    - dictionary无限大
    - speaker和hearer可以知道本次interaction是否成功

- 可用观点
  - Naming Game的定义：
    - agents have only local peer-to-peer interactions without central control or fitness-based selection, but nevertheless manage to reach a global consensus.
    - All agents will be considered peers that have the right to invent and negotiate language use.
    - There can be a flux in the population, but generation change is not necessary for reaching coherence.
    - 本文没有定义namingGame的dictionary一定无限，lexicon could be any entity. 但是在本文的模型中假设其为无限
    - 这里定义的naming game里，agents do not maintain information about the success rate of individual words and do not use any intelligent heuristics like choice of best word sofar or cross-situational learning. 目的在于研究节点交互中的微观动力是如何影响
  - lexicographers agree that there is a period in which novelty spreads and different words compete[historical linguistics and language change, 1997].
  - 语言学中符号传播与网络打标签的行为产生了相似的现象，phenomena of slow spreading followed by a sudden transitions to a global conventions
  - 定义memory交互成功与否的过程为Inventory dynamics
  - we assume that the number of possible words is so huge that the probability that two players invent the same word at two different times for two different objects is practically negligible (this means that homonymy is not taken into account here) **and so the choice dynamics among the possible words associated with a specific object are completely independent**.
  - The key question now is whether one can prove that this transition will always take place and on what timescale.
  - For our model, it is easy to prove that an absorbing state will be eventually reached with **unit probability**(在我们的试验中，没有出现global coherence，但是的确有absorbing state，不过本文中的absorbing state是指所有agents只有one word)
  - 基于忽略inventories之间相关性，假设词词与词之间相互独立，以及q（hearer拥有word2pass的概率）与hearer inventory词数成正比的假设下构建了Nw(t)变化的模型
  - evolution towards convergence proceeds in a multiplicative fashion pushing further the popularity of the  most common word while decreasing that of the others
  - Naming Game的意义：
    - 解释人类语言学传播，符号传播
    - 有助于分析设计自组织的交流系统，如Social tagging systems for the web
    - 设计机器人交流系统以适应不可预见的任务(orchestrating emergent semantics)
  - 把上升的曲线成为disorder/order transition
- 实验设计
  - 参数：1000agents，3000runs（等同于全联通网络）
  - 变量：
    - Nw(t)，Nd(t)，S(t)
  - 分析方法：观察现象，绘制Nw, Nd, S的曲线，其中Nw和Nd绘制了均值和两条single run。S绘制了均值和
  - 实验结论：
    - Nd最大值为N/2
    - 在无序到有序转变前成功率S(t)=3t/N^2
    - 概述NamingGame动态特性的三个时间段
      1. pairs of agents play almost uncorrelated games and Nw,Nd increase over time. Nw(t)=2t, Nd(t)=t, one can look at the system as a random graph(adding edges). 这个时间段的时长t~N, *after t~NlogN, only the giant component surviving*
      2. Starts building correlations. S(t)≈3t/N^2
      3. disorder/order transition emerges.(**close to the time when Nw reaches its maximum.**)，本文重点在于发现了一个sudden transition and the population gets steeper and steeper as the population size increases.
    - 通过分析N关于tmax，tconv，的关系，**tconv和tmax符合power law分布约合为t=0.6×N^1.5**，同时，tconv/tmax满足一个震荡波动的关系（文中没有提到实验重复了多少次，怀疑波动可能是因为没有足够的重复次数作为平滑）
    - 分析了Nw(tmax)和N的关系，拟合Nwmax满足Nwmax=0.3*N^1.5
    - 分析了S(t)和时间t的关系，其中，画图t=t/t_S(t)=0.5(类似归一化, in order to take into account the deviations from the pure power law)，可以看出N越大，S(t)上升的曲线越陡峭
    - 分析了S(t)和(t-t_S(t)=0.5)/(t_S(t)=0.5)^5/6的关系
    - 分析了按时间的每个agent inventory size k分布（直方图），发现在系统开始收敛前，the normalized distribution deviates from a relatively flat structure to exhibit a power law behavior
    - 分析了单个词的population并进行排名（直方图统计）的时序变化。从相对均匀的分布向指数分布转移，同时排名第一的词会越来越多，完全偏离指数分布
- 引述
  - languages with homonymy are evolutionary unstable[Optimizing the mutual intelligibility of linguistic agents in a shared world(2004)]
- 疑问
  - M=Nd(t)?
  - The model is perfectly applicable to the case where any number of agents interact simultaneously(不一样）
  - after t~NlogN, only the giant component surviving(这个说法听起来像是会舍弃一部分节点)
  - where pairs of agents are connected if they have a word in common. (不是after a failure么)

### Role of feedback and broadcasting in the naming game(2011)
- 思路流程
- 可用观点
- 实验设计
- 引述
- 疑问

### The role of topology on the dynamics of the Naming Game
- 思路流程
  - Consensus emerges through local negotiations between pairs of agents, in the absence of any central coordination
  - 两个问题：①whether a population of individuals reaches a consensus state（能不能）; ②which process leads to such a situation（怎么到）
  - 本文主要是Sharp transition的延伸，有较多重复的内容，如说了一下应用（tagging systems， sensor networks等），然后又重播了一下前文中提到的三个动态过程，stress第三个过程 triggers the final convergence。
  - 本文的主要观点在于
    - Naming Game的动态过程受underlying graph影响很大
    - low connectivity让记忆有穷
    - small-worldproperty加速收敛
    - 所以low connectivity+small world property可以优化multiagent系统达成共识的时间。
- 可用观点
  - In naming game, with respect to other models of social interactions such as the Voter model, is that the usual imitation process, in which an agent takes the state of a neighbor, is replaced by a two-step negotiation process, in which memory effects play a central role.
  - 文中表明全局共识总能在有穷系统中被达到
  - successful interactions eventually lead the system to converge
  - finite connectivity allows for a faster initial growth in the success rate(fig.1.)
  - Maximum memory是有限的，对于全联通图来说是N^0.5
- 实验设计
  - 本文用Nw，Nd和S来描述（定义）系统的动态过程。
  - 1000个点，在均度为10的complete graph，ER和BA上进行最小NG
- 引述
- 疑问
  - complete graph(mean-field case-MF)里的MF和完全图有什么关系
  - 文中smallWorld property是怎么定义的。but the small-world property gives rise to the same exponential convergence observed in the fully connected graph. 文中的三个模型只有MF（complete graph）的小世界属性更强？那么smallworld比fully connected graph是怎么做出来的

### Naming Game with Multiple Hearers(2012)
- 思路流程
- 可用观点
- 实验设计
- 引述
- 疑问


### The spontaneous emergence of conventions: An experimental study of cultural evolution(2015)
- 思路流程
  - 摘要：
    - shared conventions, social conventions
      - fields: linguistics, sociology, cognitive science
      - empirical attempts: incentives for global agreement, coordinated leadership, aggregated information about the population.
      - 集中的一些社会学现象（理论）可以解释全局的协作，但是不能解释在更初始状态下，方案和意见的产生和同意。
      - social evolution（networks of locally interacting individuals can spontaneously self-organize to produce global coordination）
    - study the effects of social network structure on the spontaneous evolution of social conventions
    - 本文进行了一次在线实验，来实验上的证明universally accepted conventions are the unitended consequence of individuals' efforts to coordinate locally with one another.
    - 本文以实验形式证明了social conventions可以自发达到收敛，越大的population和越好的连通性能够有助于收敛
- 可用观点
  - 实验在不同范围的agents间重复，结果证明了普遍社会共识可以自发产生，并表明网络结构的微小变化可以
  - 对于conventions的问题给出了如下实际生活中的应用：
    - linguistic conventions:
      - accepted names for children and pets
      - common names for colors
      - popular terms for novel cultural artifacts
    - economic conventions
      - bartering systems
      - beliefs about fairness
      - consensus regarding the ex-changeability of goods and services
  - local dynamics的研究有很多限制，其中最大的一点就是规模
  - 先有机制中大多基于一些全局假设，因此全局的协调和局部演化之间的关系难以论证
  - 文中把全局收敛的过程称为convention formation
  - repeated interaction leads to local coordination, 而local interaction produce clusters of coherent. homoNet最终可以达成收敛是因为全联通网络中repeated interaction被抑制了
- 实验设计
  - 设计在线实验，参与者were rewarded for coordinating locally. none of the options had any a priori value over the others.（为pictured object(a human face in the case)命名）
  - 24个人(图中只见21个节点？)，分别在三种不同的网络下（Spatial Net, Random Net和Hom.Mixing）两两进行交互实验（不知道总人口的规模等全局信息，也不知道自己的邻居有多少个），每次交互完可以知道成功与否。在n=24的情况下，每次试验重复了8次
  - 实验中测试了success rate和norm frequency
  - 在前两种网络中，都自发形成了小的集体，coordination rate无法高于75%（**local group competition will impeded the emeergence of global conventions**），相对的，在homogeneously网络中，一开始成功率没有变化很快(actors did not have repeated interactions with their partners)，但最终总能达到收敛（local failure accelerated global coordination）
  - 测试了不同大小的population下，不同时序下词语的分布变化，large homogenously mixing populations were significantly more likely to spontaneously create social conventions than smaller populations with less connectivity.
  - 通过问卷的形式测试了信息暴露程度
- 引述
- 疑问
  - Fig2中只数出21个节点


### Naming game on networks: Let everyone be both speaker and hearer

### PhotoSlap: A Multi-player Online Game for Semantic Annotation

### Naming Game on Adaptive Weighted Networks
- 思路流程
  - 模型：节点间的连边权重由成功率决定，连边权重同时决定了agents交流的可能性。
  - 同样是从evolution of human language物理意义出发，了解语言产生的机理有助于人造communication systems（已有software agents collecting and exchanging information without any human intervention）。同时提到了biological context of language emergence and its subsequent evolution.
  - examine such stable multi-language structures
- 可用观点
  - 在最初的(a self-organizing spatial language game)naming game模型中，对一系列对象建立vocabulary，但是为了sufficient to capture the essence of the dynamics also in a more general case, 许多研究的实验中经常只设置一个object
  - 列出了minimal version of the naming game， 并表示该规则在一定程度上artificial. (an immediate obliteration of all the words except the communicated one)
  - we talk most preferably with those with whom we already have communicated successfully
  - 比较了weber's distribution中20种常用语言使用人数的分布
  - One can consider multi- language states as metastable states of the dynamics and perhaps there is some analogy with metastable states in a certain voter model on complex networks with a strong community structure
- 实验设计
  - 规则：随机选取speaker后，hearer选取规则遵循轮盘赌（pij=wij/sum(wik)）优先选择，wij(i!=j)为两agent历史成功率，初始化时wij=e
  - 除非N和e都很大（权重偏移量很大），会得到全局统一，否则很快系统中的词数会保持一个常数，表明multilanguage regime的稳定性很强
  - N从100到10000（100,300,500,1000,5000,10000），e为10e-4,10e-5，Ne^2=10e-5, 100次
  - e变大，cluster外部的交流强度更高
  - 当success rate接近于1时，L/N drops to 0
  - 成功率会很快的上升接近至1，这个过程很快并且不随N的增加而增加，可能在部分情况下无法达成全局收敛（10^5次时还有不止一个词），但总会有一个词获取极其优势。
  - 为multi-language regime分出了三个时间段（phases），分别是①成功率从0达到1（t<1e3）②语言竞争，数目减少，(1e3~3e4)③系统趋向稳定。其中当N越大，dominant词汇的上升的transition显得更陡峭
  - 测试了average maximum number和N的关系
  - 绘制了一幅图中词汇bilibili随时间变化的情况
- 引述
  - [42, 1990]中主张an adaptive role of language and has catalysed many linguistic and biological studies.
  - control parameter: Ne^2(当Ne^2大时，聚类外交流更为频繁，模型动态行为更接近于全联通图)
  - [18, 23, 26]dynamics 最终进入multilanguage state比较像opinio-formation models（adaptive惹我日那个mechanisms generate strong community structure）
- 疑问
  - Ne^2怎么得出的（实验结果拟合？），fixN或e进行的测试也没有

### Naming game with biased assimilation over adaptive networks
- 思路流程
  - 实验核心：只有AB两个观点，hearer可能会拒听，只有hearer会改变memory，当观点里没有该观点时会断边，并随机重连
- 可用观点
- 实验设计
  - 2 word only interaction
  - 重点研究了收敛时间的相关性
- 引述
- 疑问
  - 264页下半页，感觉像是有地方写错了，hearer没有该词汇时，断边？

-----
## Consensus on adaptive Networks

### Coevolution of agents and networks: Opinion spreading and community disconnection（non-naming Game, Opinion Dynamic）
- 思路流程
  - 模型：一开始，每一对节点之间都可以建立连接,每个节点随机初始化为两种观点，观点相同时，什么都不发生；观点不同时，以p1为概率两agent观点变为一致，否则观点不变，(1-p1)p2的概率下两agents断连。(The statistical properties of the final state completely determined by the the combinations of p1 and p2)
  - 每步发生变化的概率仅和p1、p2有关
- 可用观点
  - 得到了分离的多个communities，其中最大的两个community总是有相反的观点（整个系统中只有两种观点）
  - 研究了小的q与最终拓扑上分离的components的状态的关系，（q较小时偏向于有两个连通的社区，随后会产生较多的小clusters，再变大（大于一个qmin）系统趋向于最终只有一个component）
  - 当N变大，class2,3的起始线趋向于零，则系统趋向于全局统一意见
- 实验设计
  - q：每步发生变化（两种变化①达成共识 ②一刀两断）的概率中，变化①的比例
  - r：剩余连边数
  - 测试了第一第二大社区人口的散点图，得到了随着q的改变，拓扑上会逐渐产生三种状态。
  - 测试了随N的变化最大的两个community
- 引述
- 疑问
- 因此

### Nonequilibrium phase transition in the coevolution of networks and opinions
- 思路流程
  - 模型
- 可用观点
- 实验设计
- 引述
- 疑问
