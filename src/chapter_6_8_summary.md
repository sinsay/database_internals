## Summary

原始的 B-Tree 设计在机械硬盘中可能可以高效的运行，但在 SSD 上可能会丢失一部分性能。B-Tree 具有比较高的 *write amplification* 写放大 *(因为页会被重写)* 以及较高的 *space overhead* 空间开销，因为 B-Tree 需要预先申请一些空间来存储未来需要用到的节点。

写放大可以通过使用 *buffering* 缓冲来减少，Lazy B-Tree 如 WiredTiger 跟 LA-Tree，通过为独立的节点一组节点添加内存中的缓存，将连续的更新操作缓存起来，来减少所需的 I/O 操作。

为了减少空间放大，FD-Tree 使用了不可变性：数据记录被存在了不可变的轮次中，并控制 B-Tree 可变的部分的大小是受限制的。

Bw-Tree 也使用不可变性来解决空间放大的问题，B-Tree 的节点跟他们的更新被独立的存在了不同的磁盘位置中的结构化日志存储中。写放大相对于原始的 B-Tree 也有了一定的减缓，因为将数据记录整合到一个单独的逻辑节点并不会被频繁的执行。Bw-Tree 不需要在并发访问时使用 Laches 来保护页，因为不同节点间的虚拟指针是存在内存中的。



### 更多的阅读

如果你希望了解更多本章中所提及的概念，可以从下面引用的文献中了解更多信息

- Copy-on-Write B-Trees

  Driscoll, J. R., N. Sarnak, D. D. Sleator, and R. E. Tarjan. 1986. “Making data structures persistent.” In Proceedings of the eighteenth annual ACM symposium on Theory of computing (STOC ’86), 109-121. https://dx.doi.org/ 10.1016/0022-0000(89)90034-2.

- Lazy-Adaptive Trees

  Agrawal, Devesh, Deepak Ganesan, Ramesh Sitaraman, Yanlei Diao, and Shashi Singh. 2009. “Lazy-Adaptive Tree: an optimized index structure for flash devices.” Proceedings of the VLDB Endowment 2, no. 1 (January): 361-372. https://doi.org/ 10.14778/1687627.1687669.

  

- FD-Trees 

  Li, Yinan, Bingsheng He, Robin Jun Yang, Qiong Luo, and Ke Yi. 2010. “Tree Indexing on Solid State Drives.” Proceedings of the VLDB Endowment 3, no. 1-2 (September): 1195-1206. https://doi.org/10.14778/1920841.1920990.

  

- Bw-Trees

  Wang, Ziqi, Andrew Pavlo, Hyeontaek Lim, Viktor Leis, Huanchen Zhang, Michael Kaminsky, and David G. Andersen. 2018. “Building a Bw-Tree Takes More Than Just Buzz Words.” Proceedings of the 2018 International Conference on Management of Data (SIGMOD ’18), 473–488. https://doi.org/ 10.1145/3183713.3196895

  

  Levandoski, Justin J., David B. Lomet, and Sudipta Sengupta. 2013. “The Bw- Tree: A B-tree for new hardware platforms.” In Proceedings of the 2013 IEEE International Conference on Data Engineering (ICDE ’13), 302-313. IEEE. https:// doi.org/10.1109/ICDE.2013.6544834.

Cache-Oblivious B-Trees

Bender, Michael A., Erik D. Demaine, and Martin Farach-Colton. 2005. “Cache- Oblivious B-Trees.” SIAM Journal on Computing 35, no. 2 (August): 341-358. https://doi.org/10.1137/S0097539701389956.

