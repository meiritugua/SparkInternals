## Introduction

> 本开源书 forked from [Apache Spark 的设计与实现](https://github.com/yourtion/SparkInternals)，作者为 [yourtion](https://github.com/yourtion)，欢迎大家 star 原作者的 [repo](https://github.com/yourtion/SparkInternals)，以便获得最新更新，谢谢！

本文主要讨论 Apache Spark 的设计与实现，重点关注其设计思想、运行原理、实现架构及性能调优，附带讨论与 Hadoop MapReduce 在设计与实现上的区别。不喜欢将该文档称之为“源码分析”，因为本文的主要目的不是去解读实现代码，而是尽量有逻辑地，从设计与实现原理的角度，来理解 job 从产生到执行完成的整个过程，进而去理解整个系统。

讨论系统的设计与实现有很多方法，本文选择 **问题驱动** 的方式，一开始引入问题，然后分问题逐步深入。从一个典型的 job 例子入手，逐渐讨论 job 生成及执行过程中所需要的系统功能支持，然后有选择地深入讨论一些功能模块的设计原理与实现方式。也许这样的方式比一开始就分模块讨论更有主线。

本文档面向的是希望对 Spark 设计与实现机制，以及大数据分布式处理框架深入了解的 Geeks。

因为 Spark 社区很活跃，更新速度很快，本文档也会尽量保持同步，文档号的命名与 Spark 版本一致，只是多了一位，最后一位表示文档的版本号。

由于技术水平、实验条件、经验等限制，当前只讨论 Spark core standalone 版本中的核心功能，而不是全部功能。诚邀各位小伙伴们加入进来，丰富和完善文档。

关于学术方面的一些讨论可以参阅相关的论文以及 Matei 的博士论文，也可以看看我之前写的这篇 [blog](http://www.cnblogs.com/jerrylead/archive/2013/04/27/Spark.html)。

好久没有写这么完整的文档了，上次写还是三年前在学 Ng 的 ML 课程的时候，当年好有激情啊。这次的撰写花了 20+ days，从暑假写到现在，大部分时间花在 debug、画图和琢磨怎么写上，希望文档能对大家和自己都有所帮助。
