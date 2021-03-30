# Summary

结构化日志存储现在已经随处可见了：从 *Flash Translation Layer* 闪存转换层到文件系统跟数据库系统，他通过在内存中合并随机小写入进行批量的执行，来减少写放大的问题。LSS 还会通过周期性的执行垃圾回收来回收那些已经被删除的段。

LSM Tree 从 LSS 中汲取了一些想法，使用了结构化日志的方式来构建索引数据结构：批量的将内存中的数据写入到磁盘；被覆盖的数据记录在压缩的时候会被清除。

有一点很重要的是许多的软件层次都使用了 LSS，要保证各层级之间的叠加是合适的，否则的话，还可以考虑完全跳过文件系统的级别来手动的直接访问硬件。

### 更多的阅读

如果你想对我们本章中讨论的概念有更多的了解，可以通过下面的引用获取相关信息

- Overview

  Luo, Chen, and Michael J. Carey. 2019. “LSM-based Storage Techniques: A Sur‐ vey.” The VLDB Journal https://doi.org/10.1007/s00778-019-00555-y.

- LSM Trees

  O’Neil, Patrick, Edward Cheng, Dieter Gawlick, and Elizabeth O’Neil. 1996. “The log-structured merge-tree (LSM-tree).” Acta Informatica 33, no. 4: 351-385. https://doi.org/10.1007/s002360050048.

- Bitcask

  Justin Sheehy, David Smith. “Bitcask: A Log-Structured Hash Table for Fast Key/ Value Data.” 2010.

- WiscKey

  Lanyue Lu, Thanumalayan Sankaranarayana Pillai, Hariharan Gopalakrishnan, Andrea C. Arpaci-Dusseau, and Remzi H. Arpaci-Dusseau. 2017. “WiscKey: Sep‐ arating Keys from Values in SSD-Conscious Storage.” ACM Trans. Storage 13, 1, Article 5 (March 2017), 28 pages.

- LOCS

  Peng Wang, Guangyu Sun, Song Jiang, Jian Ouyang, Shiding Lin, Chen Zhang, and Jason Cong. 2014. “An efficient design and implementation of LSM-tree based key-value store on open-channel SSD.” In Proceedings of the Ninth Euro‐ pean Conference on Computer Systems (EuroSys ’14). ACM, New York, NY, USA, Article 16, 14 pages.

- LLAMA

  Justin Levandoski, David Lomet, and Sudipta Sengupta. 2013. “LLAMA: a cache/ storage subsystem for modern hardware.” Proc. VLDB Endow. 6, 10 (August 2013), 877-888.