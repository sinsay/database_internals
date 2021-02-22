## Summary

在本章我们讨论了数据库管理系统的架构以及主要的几个组件。

还重点讨论了基于磁盘的数据结构的重要性，以及他跟基于内存的数据结构的区别。对此我们总结基于磁盘的数据结构对两种类型的存储都是非常重要的，只是他们会用来达成不同的目标。

为了理解访问模式对数据库系统设计的影响，我们讨论了基于行跟基于列的数据库管理系统以及导致他们之间有所区别的因素。还从数据文件跟索引文件作为起点，开始了对数据是如何进行存储的讨论。

最后我们介绍了三个核心的概念：*Buffering* 、*Immutability* 跟 *Ordering*。我们使用他们来贯穿整本书的核心属性跟使用他们的存储引擎。

### 更多的阅读

如果你想对我们本章中讨论的概念有更多的了解，可以通过下面的引用获取相关信息

- Database architecture

  Hellerstein, Joseph M., Michael Stonebraker, and James Hamilton. 2007. “Archi‐ tecture of a Database System.” Foundations and Trends in Databases 1, no. 2 (Feb‐ ruary): 141-259. https://doi.org/10.1561/1900000002.

- Column-oriented DBMS

  Abadi, Daniel, Peter Boncz, Stavros Harizopoulos, Stratos Idreaos, and Samuel Madden. 2013. The Design and Implementation of Modern Column-Oriented Database Systems. Hanover, MA: Now Publishers Inc.

- In-memory DBMS

  Faerber, Frans, Alfons Kemper, and Per-Åke Alfons. 2017. Main Memory Data‐ base Systems. Hanover, MA: Now Publishers Inc.