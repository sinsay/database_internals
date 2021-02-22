# Chapter 2

## B-Tree Basics

在前面的章节我们将存储的数据结构分成了类：*mutable* 可变的跟 *immutable* 不可变的，并且确认了不可变性是其中一个会影响到具体设计与实现的核心概念。大部分的可变数据存储结构都使用了就地更新的机制。在发生插入、删除或更新操作时，数据记录会在目标文件的原位置上直接更新。

存储引擎通常允许在数据库中存在一条数据记录的多个版本；比如在使用了 *Multiversion Concurrency Control* *(MVCC 多版本并发控制)* 或 *Slotted Page* 组织时。为了简化的目的，现在我们先假定每个 Key 只会关联到唯一的一条数据记录，并且只有一个唯一的位置信息。

现在最流程的存储数据结构之一就是 B-Tree。许多开源的数据库都是基于 B-Tree 的，并且经过了多年的验证，他确实适用于大部分的场景。

B-Tree 并不是近期才发明的：他在 1971 年时已经被 Rudolph Bayer 及 Edward M. McCreight 进行了介绍并一直流行到现在。在 1979 年时已经出现了不少 B-Tree 的变种。Douglas Comer 在 [Douglas Comer](https://lwn.net/Articles/752063) 中对其进行了系统性的整理。

在深入 B-Tree 之前，先来讨论为什么我们要用他来替代传统的搜索树，比如 `Binary search tree` 二叉搜索树、2-3-Trees 跟 `AVL Tree` 平衡搜索树。现在我们先来回顾下什么是二叉搜索树。