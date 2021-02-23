# Summary

在本章中，我们学习了二进制文件的组织：如果序列化基础的数据类型，将他们组合成 Cell，并用 Cell 来构建 Slotted Page 及在这些数据结构中进行导航。

我们还学到如何处理可变长度的数据类型，如字符串、字节序列跟数组，以及如何处理包含了这些可变长度数据的Cell。

我们讨论了 *slotted page* 分槽页的格式，他让我们可以在外部的页使用 Cell ID 来引用单独的 Cell，按照插入的顺序来保存数据，并按照 Key 的顺序来排序这些 Cell 的偏移量。

这些原则可以使用在大部分的基于磁盘的二进制格式跟网络协议中。

### 更多的阅读

如果你希望了解更多本章中所提及的概念，可以从下面引用的文献中了解更多信息

- File organization techniques

  Folk, Michael J., Greg Riccardi, and Bill Zoellick. 1997. File Structures: An Object- Oriented Approach with C++ (3rd Ed.). Boston: Addison-Wesley Longman.

  Giampaolo, Dominic. 1998. Practical File System Design with the Be File System (1st Ed.). San Francisco: Morgan Kaufmann.

  Vitter, Jeffrey Scott. 2008. “Algorithms and data structures for external memory.” Foundations and Trends in Theoretical Computer Science 2, no. 4 (January): 305-474. https://doi.org/10.1561/0400000014.