---
layout: post
title: "R的那些包（2）——NMF"
excerpt: "理解R的非负矩阵分解框架：NMF"
tags:
  - r-package
  - R
  - ZH
---

> 本文为NMF包说明文档。主要参考NMF-vignette和NMF参考手册
> `{NMF}`特性如下：
>   - 11个内置NMF算法；
>   - 4中设置种子(初始化)的算法；
>   - 所有算法和种子算法的接口良好的集合在了一起；
>   - 提供了一个普适测试框架，用以比较和魔改不同的NMF算法；
>   - 可以嵌入自己的算法和设置中资的方法；
>   - 提供了绘图及可视化的解释方法；
>   - 针对并行运算进行了优化；
>   - 植入C++标准算法，对内存cost进行了优化；
>   - Optional layer for bioinformatics using BioConductor (Gentleman et al. 2004a);

## 1 概论
### 1.1 安装载入NMF
```
# 在本文的例子中需要用到一个数据集，如果要使用这个数据集，需首先安装Biobase再安装NMF(或在安装完Biobase后重新安装NMF)，安装方法如下：

# 要使用Golub数据集，需要先安装并载入Biobase
source("https://bioconductor.org/biocLite.R")
biocLite("Biobase")

# 如果出现提示更新包的版本，按自己需要选择
Update all/some/none? [a/s/n]:

# 安装NMF
install.packages("NMF")

# 载入NMF
library(NMF)
```

- 需要注意的是，NMF这个包require没写好，在调用某些方法的时候如果报错说缺少什么包，装上就是。

### 1.2 NMF包中的算法
- 使用`nmfAlgorithm()`可以查看这个框架内置的NMF算法，无参调用时返回所有内置算法的调用字符串（character key)，使用对应字符串时则返回对应算法的参数。（当使用参数`all=T`时会显示之前用R写的，没有优化过的算法。

```
# nmfAlgorithm
> nmfAlgorithm()
 [1] "brunet"    "KL"        "lee"       "Frobenius" "offset"   
 [6] "nsNMF"     "ls-nmf"    "pe-nmf"    "siNMF"     "snmf/r"   
[11] "snmf/l"   

# 测试获取其中某种算法参数  
> nmfAlgorithm("lee")
<object of class: NMFStrategyIterative>
 name: lee [NMF]
 objective: 'euclidean'
 model: NMFstd
 <Iterative schema>
  onInit: none
  Update: function (i, v, x, rescale = TRUE, copy = FALSE, eps = 10^-9,
            weight = NULL, ...)
  Stop: 'connectivity'
  onReturn: none
```
- 可以将方法的`nmfAlgorithm()`返回的值作为一个向量，同时调用多种方法。

### 1.3 设置种子
- 我们知道，初始化一个矩阵，它的维度很可能是很高的，而事实上从原理上就可以称为“全局最小化”算法的东西很遗憾，还没有出现，所以我们就需要对要迭代优化的矩阵进行初始化。一种常用的初始化方法是，随机设置一颗种子（比如使用W0或H0中的某个值），对整个矩阵按某种分布进行初始化，其中初始化的值的范围往往与目标矩阵的值域相仿。
- 既然这种初始化方式有很大的随机性，而初始化的方式对最终的结果往往是很大的，那么使用这种方式的时候，整个过程往往需要反复多次，这样会大大加大计算的时间。
- 出于此，这种简单易用的初始化方法在面对高维复杂问题的时候就容易被人嫌弃，人们开始寻找更加合理的，更加有针对性，不需要重复运行的初始化方法。
- 和查看内置NMF算法一样，也可以使用`nmfSeed()`来查看设置种子初始化的方法。

| Key | Description |
|:--------|:-------:|
| ica   |  Independent Component Analysis (ICA) (from the {fastICA} (Marchini et al. 2013)). （只有正值的部分被用来初始化向量）|
| nnsvd   | Nonnegative Double Singular Value Decomposition. The basic algorithm contains no randomization and is based on two SVD processes, one approximating the data matrix, the other approximating positive sections of the resulting partial SVD factors utilizing an algebraic property of unit rank matrices. It is well suited to initialize NMF algorithms with sparse factors. Simple practical variants of the algorithm allows to generate dense factors. Reference: (Boutsidis et al. 2008)   |
| none   | 使用none，用户可以手动调节初始值 |
| random   | 将矩阵初始化为均匀分布的值，值域范围在[0,max(V)] |

### 1.4 核心接口nmf函数
- 使用`nmf()`的形式调用包内的算法，其中
  - `X`可以是要分解的matrix，data.frame和ExpressionSet
  - `rank`是矩阵分解的秩(r)
  - `method`参数和`seed`参数代表矩阵分解的算法和初始化的方法，需填入1.3和1.4节中的关键字。
```
nmf(X,rank,method,seed...)
```
- `nmf()`返回的结果是一个NMFfit类。

## 2 使用实例
> 这一节里使用Golub数据集展示使用NMF包进行非负矩阵分解的实例。
> Golub数据集在许多NMF研究的论文中都被使用过，在`{NMF}`中Golub数据的存储在一个自定义数据结构`ExpressionSet`中。

### 2.1 使用内置模型
- 数据载入

```
data(esGolub) # 载入数据
esGolub<-esGolub[1:200,]  # 取其中前两百个基因作为测试样本（走个流程节省时间）
```

- 获取NMF结果数据及参数，例中使用ns方法和随机初始化，之后还可以根据不同模型设置参数，如例中theta=0.7。
- 可以通过`nrun`参数来设置重复跑多少次（一般会重复跑100~200次）。需要注意的是，为了节省内存，在计算时只有最优的结果会保存在内存中，默认输出也会是最好的结果，但如果要保留所有结果，在nmf中加入`.options=list(keep.all=T)`或`.options="k"`，此时返回结果是一个NMFfitXn对象。

```
> res<-nmf(esGolub,3,method="ns",seed="random",theta=0.7, nrun=5)
> res # 查看res
> algorithm(res) # 查看res模型的算法
> fit(res)  # 可以用函数fit查看模型的参数
> View(fitted(res))


> W <- basis(res)
> H <- coef(res) # 得到分解矩阵W和H

# 使用summary可以查看res的参数，如残差、计算时间等
# 同时还可以指定target和class获取更多信息。
# 需注意这里的Cell是esGolub数据集中的一个元素
> summary(res)
> summary(res,target=esGolub)
> summary(res,class=esGolub$Cell)

# 有趣的是，NMF对象就像matrix，data.frame一样，可以随意取行/列的子集
# 这样得到的结果也是一个NMFfit对象
> res[1:10,]
> res[,1:10]
> res[2:33,2:33]

```

*问题：这里metagene-specific features没有看懂*
- 一般来说NMF矩阵都稀疏性都很高，可以使用`featureScored`和`extractFeatures`方法分别获取原矩阵中每行向量贡献程度，每个提取出的隐feature对应的行。

test formula:

$$test_formula=\sum{\alpha^2}$$

### 2.2 使用自己的模型
- 这里说的是`nmf()`中的seed参数，也就是初始化的方法。前面说到可以用`nmfSeed`查看内置的初始化方法，调用方式可简单分为三类，演示如下：

```
# 直接调用关键字
> nmf(esGolub,3,seed="nndsvd")

# 使用数字种子（random）
> nmf(esGolub,3,seed=123456)

# 使用自己的初始化方法（直接传入nmfModel类的初始W/H矩阵）
> init <- nmfModel(3, esGolub, W=0.5, H=0.3)
> res <- nmf(esGolub, 3, seed=init)
# 这里查看W和H与2.1中一样使用`basis`和`coef`

```

### 2.3 并行计算
- NMF中使用了foreach并行运算框架，(依赖于`{foreach}`和`{doParallel}`包），可用于多核运算的机器。（这里不是多集群运算）
- 在不是Windos系统的机器上，内存表现会更好一些（得益于共享内存，基于`{bigmemory}`包），而在Windos机器上，内存和cpu核数是线性正相关的。
- 需要注意的是，Mac用户可能无法在MacOS x GUI上进行多核运算，因为从GUI环境中进行多核运算在某种程度上是危险的。
- 通过`nmf`中`.opt`来设置如何使用并行运算。通过形式是`v`+`P/p`+`<number>`，其中v代表将每个运算单元的信息打印出来，大写P代表强制平行运算（出错直接报错），小写p在运算出错后会转为顺序运算，<number>为申请的核数，需小于机器的核数，如`vP4`，是强制运算申请4核并行运算。

```
# 申请4个运算单元进行并行运算，如出现问题将报错
nmf(esGolub,3,nrun=5,.opt="vP4")
# 可以使用`-p`或.pdackkend=NA来强制顺序运算
nmf(esGolub,3,nrun=5,.opt="v-p",seed=123)
nmf(esGolub,3,nrun=5,.opt="v",.pbackend=NA,seed=123)
```
> NMF也可以进行集群运算（HPC cluster），但是笔者条件有限，没有进行测试，有需要的朋友可以参阅[1]中2.5.4节。

### 2.4 估计向量化的秩
- 一般来说NMF中使用的r都不唯一，而是会尝试多个值，观察哪个值效果最好，`{NMF}`中也提供了直接选择多个r进行分解，此时`nrun`的值会应用在每一个r值上；
- 当有多个rank值时，nmf返回的结果是一个NMF.rank对象，对象内会储存不同r值的评测指标。使用plot和consensusmap可以绘制对比图进行选择。

```
# 从2到6每一个r值都会跑十遍
> estim.r<-nmf(esGolub,2:6,nrun=10)

# 观察不同r值的评测指标
> plot(estim.r)

# 观察不同rank值的一致性矩阵，可以加入其他的注解信息
> consensusmap(estim.r, annCol=esGolub,labCol=NA,labRow=NA)

# 生成与esGolub同维度的随机矩阵做矩阵分解，并与真实数据NMF结果进行比较
> V.random <- randomize(esGolub)
> estim.r.random<-nmf(V.random,2:6,nrun=10)
> plot(estim.r, estim.r.random)
```

### 2.5

## 3 扩展包

## Reference
https://www.bioconductor.org/packages/release/bioc/html/Biobase.html
