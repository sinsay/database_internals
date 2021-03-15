## Summary

本章中我们讨论了基于磁盘实现的 B-Tree 的特定的概念，如

- *Page header*

  页的头部信息通常用来存储元数据

- *Rightmost pointers*

  不与分隔键成对的指针，以及如何对其进行处理

- *High keys*

  用来确认节点中能够存储的最大的 Key

- *Overflow pages*

  溢出页让我们可以存储尺寸大于固定页大小的可变长度记录

在这些之后，我们还有一些关于从根下降到叶子节点的讨论

- 如何使用间接指针来应用二分查找
- 如何通过父节点指针或是导航信息来跟踪树的层级结构

最后，还讨论跟优化及维护相关的技术

- *Rebalancing*

  移动相邻节点的元素来减少分裂跟合并的次数

- *Right-only appends*

  在某些假设中，不进行分裂，而是将新 Cell 添加到页的最右侧能够快速的填充数据

- *Bulk loading*

  一个使用将有序数据来高效构建 B-Tree 的技术。

- *Garbage collection*

  处理页重写，将 Cell 变为以 Key 同序，跟回收不可用 Cell 的技术。

这些概念构建了基础的 B-Tree 算法与真实实现之间的桥梁，帮助我们更好的理解基于 B-Tree 的存储系统是如何工作的。

### 更多的阅读

如果你希望了解更多本章中所提及的概念，可以从下面引用的文献中了解更多信息

- Disk-based B-Trees

  Graefe, Goetz. 2011. “Modern B-Tree Techniques.” Foundations and Trends in Databases 3, no. 4 (April): 203-402. https://doi.org/10.1561/1900000028.

  Healey, Christopher G. 2016. Disk-Based Algorithms for Big Data (1st Ed.). Boca Raton: CRC Press.