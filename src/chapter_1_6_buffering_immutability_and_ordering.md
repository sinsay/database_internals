## Buffering, Immutability, and Ordering

存储引擎都需要基于某些特定的数据结构，但是这些数据结构并没有对缓存、状态回复、事务这些存储引擎底层的组件有明确的语义定义。

在下一章节中，我们会开始讨论 B-Tree 以及试着理解为什么会有这么多的 B-Tree 变种，以及为什么一直持续不断的有新的数据存储结构出现。

存储数据结构有三个通用的变量：他们会使用 `buffering` 缓冲 *(或避免使用)*，使用 `immutable` 不可变 *(或 mutable 可变)* 的文件，按照 `order` 顺序来存储数据 *(或不按顺序)*。大部分的存储数据结构的区别跟优化都跟这三点相关。

- *Buffering*

  这部分定义了存储数据结构需不需要将在写入磁盘前某些数据缓冲在内存里。当然，每个基于磁盘的数据结构都会需要某种级别的缓冲，因为磁盘进行读写所传输的最小单元是块，这个级别描述了如何尽量写入完整的块。在这里，我们还要谈论避免缓冲，有些存储引擎的实现就是这样做的。我们在本书讨论的第一个优化是为 B-Tree 添加内存的缓冲来分摊 I/O 开销。*(在 Lazy B-Tree 中)*。但是这并不是唯一应用缓冲的地方，比如 two-component LSM Tree，尽管跟 B-Tree 有点类似，但他使用了不同的方式来使用缓冲，并最终将缓冲合并成不可变的。

- *Mutability* (or *immutability*)

  这部分定义了存储数据结构要不要实现：从文件中读取数据，更新这部分数据，然后将更新后的结果写入到文件的同一个位置。不可变的数据结构是 `append-only` 的：在写入之后，文件的内容不会再进行更改，相反的，所有的修改会以添加的信息写到文件的末端。还有其他的方式来实现不可变性，其中一个是使用 `copy-on-write` 写时复制技术，被修改的页面保存了修改后的版本，然后将它写到文件中的新的位置，而不是写到原来的位置。我们常听到 LSM 跟 B-Tree 的区别被描述成不变性跟就地更新之间的差异，但也有一些其他的数据结构 *(如 Bw-Tree)* 是从 B-Tree 启发而来但却是不可变的。

- *Ordering*

  这部分定义了数据记录记录到磁盘时需不需要跟他的 Key 保持相同的顺序。换句话说，连续的 Key 在磁盘是连续存储的。Ordering 通常定义了能不能高效的对记录进行区间扫描，而不只是用来定位独立的数据记录。数据存储时如果是乱序的 *(比如按照插入的顺序)* 有时也为写入时间的优化提供了可能性。比如 Bitcask 跟 WiscKey 存储数据的方式是通过直接附加到文件末尾。

当然，对这三个概念的粗略讨论是无法展示他们的能力的，我们将会继续在本书后续的章节中对其进行讨论。




