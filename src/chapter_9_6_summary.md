# Summary

故障检测器是分布式系统中必须的组件，就如在 FLP Impossibility 展示的结果，在异步的系统中没有协议能够对一致性做出保证。错误检测器有助于扩充我们的模型，让我们可以通过在精准度跟完整性上做去权衡来解决一致性的问题。另一个在这个领域的重要发现是在 CHANDRA96 中证明故障检测器无效的方法，他展示了就算故障检测器产生了无数错误的情况下，也可以解决一致性问题。

我们还覆盖了几个用来进行故障检测的算法，他们每个都使用了不同的方式：有些专注于通过直接通信来检测故障，有些通过广播或 Gossip 流言来传播信息，有一些使用休眠 *(也叫做缺失的通信)* 作为传播的方式。我们现在知道可以使用心跳或 Ping，固定的限期或是可持续扩展等方法，每种方法都有他们自己的优点：简易性、精确度或是清晰性。

### 更多的阅读

如果你想对我们本章中讨论的概念有更多的了解，可以通过下面的引用获取相关信息

- Failure detection and algorithms
  - Chandra, Tushar Deepak and Sam Toueg. 1996. “Unreliable failure detectors for reliable distributed systems.” Journal of the ACM 43, no. 2 (March): 225-267. https://doi.org/10.1145/226643.226647.
  - Freiling, Felix C., Rachid Guerraoui, and Petr Kuznetsov. 2011. “The failure detector abstraction.” ACM Computing Surveys 43, no. 2 (January): Article 9. https://doi.org/10.1145/1883612.1883616.
  - Phan-Ba, Michael. 2015. “A literature review of failure detection within the con‐ text of solving the problem of distributed consensus.” https://www.cs.ubc.ca/~best chai/theses/michael-phan-ba-msc-essay-2015.pdf