# Data Parallel C++
*Mastering DPC++ for Programming of Heterogeneous Systems using C++ and SYCL（掌握DPC++：使用C++和SYCL语言进行异构编程）*

* 作者：

  James Reinders 

  Ben Ashbaugh

  James Brodman

  Michael Kinsner

  John Pennycook

  Xinmin Tian

* 译者：陈晓伟

* 原文发布时间：2020年09月02日

> 翻译是译者用自己的思想，换一种语言，对原作者想法的重新阐释。鉴于我的学识所限，误解和错译在所难免。如果你能买到本书的原版，且有能力阅读英文，请直接去读原文。因为与之相较，我的译文可能根本不值得一读。
>
> <p align="right"> — 云风，程序员修炼之道第2版译者</p>

## 本书概述

本书是关于使用C++编写数据并行程序的。如果你是并行编程的新手，也没关系。如果从未听说过SYCL或DPC++编译器，也没有关系。

SYCL是一个行业驱动的Khronos标准，在异构系统为C++中添加原生的数据并行性。DPC++是一个开源编译器项目，它基于SYCL、编译器扩展和异构支持组成，其中包括GPU、CPU和FPGA支持。本书中的所有例子都是用DPC++编译器编译的。

如果你是一个不精通C++的C程序员，不用太担心。本书的几位作者会告诉你，他们是通过阅读使用C++的书籍来学习C++的，就像这本书一样。只要有一点耐心，这本书对于想要编写现代C++程序的C程序员来说应该是很容易的。

本书项目始于2019年，对于完全支持C++和数据并行的需要大量的扩展，超出当时的SYCL 1.2.1标准。DPC++编译器需要支持这些扩展，包括对统一共享内存(USM)的支持、通过SYCL完成三级层次结构的子组、匿名lambdas和许多编程简化。

本书出版的时候(2020年末)，会有一个临时的SYCL 2020规范可供公众评论。临时规范包括对USM、子组、匿名lambdas的支持，以及对编码的简化(类似于C++ 17 CTAD)。可以通过本书中SYCL的扩展，以大致了解SYCL将来的发展方向，这些扩展都会在DPC++编译器项目中实现。我们希望与本书的内容相比，SYCL的变化不会太大，但随着社区的发展，SYCL将会有一些变化。更新信息的重要资源包括本书GitHub和勘误表，可以从本书的网页(www.apress.com/9781484255735)找到，以及oneAPI DPC++参考(tinyurl.com/dpcppref)。

SYCL和DPC++的发展仍在继续。在学习了如何使用DPC++为使用SYCL的异构系统创建程序之后，会在之后讨论对未来的展望。

希望我们的书能够支持和帮助SYCL社区的发展，并帮助推广C++中的数据并行编程。

## 作者简介

**James Reinders**是并行计算领域有30多年经验的专家，参与编纂了十余本与并行编程相关的技术书籍，以及为世界上最快的两台计算机(500强中排名第一)以及许多其他超级计算机和软件开发工具做出了重要贡献。2016年中期结束在Intel的任期(已经在Intel工作了10,001天(超过27年)），不过还继续在并行计算(高性能计算和人工智能)相关的领域进行写作、教学和编程。

**Ben Ashbaugh**是Intel公司的软件架构师，他工作了20多年，为Intel图形产品开发软件驱动程序。在过去的10年里，Ben专注于并行编程模型，用于图形处理器上的通用计算，包括SYCL和DPC++。Ben活跃于Khronos SYCL、OpenCL和SPIR工作组，帮助定义并行编程的行业标准，他编写了许多扩展来展示Intel GPU独特的魅力。

**James Brodman**是Intel公司的软件工程师，专注于并行编程的运行时和编译器开发，并且是DPC++的架构师之一。他拥有伊利诺伊大学厄巴纳-香槟分校的计算机博士学位。

**Michael Kinsner**是Intel公司的首席工程师，为各种架构开发并行编程语言和模型，也是DPC++的架构师之一。他对空间编程模型和编译器做出了重要的贡献，是Khronos组织中的Intel代表，他致力于制定SYCL和OpenCL并行编程行业标准。Mike拥有麦克马斯特大学(McMaster University)的计算机工程博士学位，并且热衷于编写跨架构的编程模型(同时能够保证性能)。

**John Pennycook**是Intel公司的一名HPC应用工程师，专注于让开发人员充分利用现代处理器中的并行性。他在一系列科学领域的应用程序优化和并行方面有丰富的经验，此前曾担任Intel极端性能用户组(IXPUG)指导委员会的代表。John拥有华威大学计算机科学博士学位。他的研究点很多，主要在于跨不同硬件架构实现应用“性能可移植性”的能力。

**Xinmin Tian**是Intel公司高级首席工程师和编译架构师，在OpenMP架构审查委员会(ARB)担任Intel代表。他负责为Intel架构驱动对OpenMP进行装载、向量化和并行化编译器技术。他目前的重点是基于llvm的OpenMP装载，使用oneAPI工具包的DPC++编译器对CPU和Xe加速器进行优化，以及优化HPC/AI应用程序性能。他拥有计算机科学博士学位，拥有27项美国专利，发表了60多篇技术论文，被1200多次引用，并在其专业领域与他人合著了两本书。

## 本书相关

* github翻译地址：https://github.com/xiaoweiChen/Data-Paralle-Cpp
* 英文原版PDF：https://www.apress.com/gp/book/9781484255735
* 相关教程：https://github.com/jeffhammond/dpcpp-tutorial
* Latex环境搭建：https://www.cnblogs.com/1625--H/p/11524968.html
