##                                       MapReduce 

##### 1.概念定义

​		MapReduce是面向大数据并行处理的计算模型、框架和平台，是一个基于集群的高性能并行计算平台，借助于函数式程序设计语言Lisp的设计思想，提供一种简便的并行程序设计方法。由Map和Reduce两个函数编程实现基本的并行计算任务，简化大规模数据的编程和计算处理。

##### 2. 主要功能

###### 2.1数据划分和计算任务调度：

​		系统自动将一个作业（Job）待处理的大数据划分为很多个数据块，每个数据块对应于一个计算任务（Task），并自动 调度计算节点来处理相应的数据块。作业和任务调度功能主要负责分配和调度计算节点（Map节点或Reduce节点），同时负责监控这些节点的执行状态，并 负责Map节点执行的同步控制。

###### 2.2系统优化

​		为了减少数据通信开销，中间结果数据进入Reduce节点前会进行一定的合并处理；一个Reduce节点所处理的数据可能会来自多个Map节点，为了避免Reduce计算阶段发生数据处理不平衡，Map节点输出的中间结果需使用一定的策略进行适当的划分处理，保证相关性数据发送到同一个Reduce节点；此外，系统还进行一些性能优化处理，如对最慢的计算任务采用多备份执行、选最快完成者作为结果。

##### 3.MapReduce的运行流程：

![img](https://img-blog.csdnimg.cn/7f50a6b1e72a4be7a2c277c1c70581f3.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAaVTlsI8u5paw,size_20,color_FFFFFF,t_70,g_se,x_16)

由上图可以看到MapReduce执行下来主要包含这样几个步骤：

1. 首先正式提交作业代码，并对输入数据源进行切片。

2. master调度worker执行map任务。

3. worker当中的map任务读取输入源切片。

4. worker执行map任务，将任务输出保存在本地。

5. master调度worker执行reduce任务，reduce worker读取map任务的输出文件。

6. 执行reduce任务，将任务输出保存到HDFS。

   ##### 4.总结

   ​		MapReduce是一种非常简单又非常强大的编程模型。其编程模型只包含map和reduce两个过程，map的主要输入是一对< key , value>值，经过map计算后输出一对< key , value>值；然后将相同key合并，形成< key , value集合>；再将这个< key , value集合>输入reduce，经过计算输出零个或多个< key , value>对。

   