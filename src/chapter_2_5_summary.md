# Summary

在本章中，一开始我们讨论了创建基于磁盘的数据结构的动机。二叉查找树跟 B-Tree 具有类似的复杂度特征，但他并不适用于磁盘，因为他具有较低的扇出量，以及会因为需要保持平衡，导致产生因为对指针进行重定位而产生的更新。B-Tree 通过增加子节点的数量提高了扇出量及减少了保持平衡所需的操作。

在这之后，我们讨论了 B-Tree 内部的结构以及描绘了其查找、插入及更新操作算法的实现。分裂跟合并操作能够重新构建树，以此来来维持因为添加跟删除元素而失去的平衡性。我们保持树始终具有最小化的高度，并在将新数据尽量写入有空闲空间的节点。

我们可以使用这些知识来创建基于内存的 B-Tree。为了完成基于磁盘的实现，我们深入 B-Tree 的节点在磁盘上的布局细节以及使用数据编码格式来构建磁盘的布局。

### 更多的阅读

如果你希望了解更多本章中所提及的概念，可以从下面引用的文献中了解更多信息

- Binary search trees

  Sedgewick, Robert and Kevin Wayne. 2011. Algorithms (4th Ed.). Boston: Pearson.

  Knuth, Donald E. 1997. The Art of Computer Programming, Volume 2 (3rd Ed.): Seminumerical Algorithms. Boston: Addison-Wesley Longman.

- Algorithms for splits and merges in B-Trees

  Elmasri, Ramez and Shamkant Navathe. 2011. Fundamentals of Database Systems (6th Ed.). Boston: Pearson.

  Silberschatz, Abraham, Henry F. Korth, and S. Sudarshan. 2010. Database Sys‐ tems Concepts (6th Ed.). New York: McGraw-Hill.