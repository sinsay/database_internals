# System Synchrony

从 FLP Impossibility 中你可以看到对时间的假设在分布式系统中扮演者非常重要的角色。在一个 *Asynchronous System* 异步的系统中，我们无法知道关联处理器的速度，也无法确保消息能在指定的时间区间送达或以指定的顺序送达。某个处理可能会消耗很长的时间才能得到响应，而且处理的故障也并不总是能可靠的监测到。

对异步系统主要的批评是下面这些假设都是不可行的：处理器之间不会有明显的处理速度差别，连接不会花费不确定的时间来传递消息。对时间的依赖既简化了推理也提供对时间上界的保证。

在异步的模型中并不总是能够解决共识问题，而且，设计一个高效的同步算法也并不总是能够实现的，对于某些任务来说，实际的解决方案可能是跟时间相关的。

这些假设可以做一些放松，系统也可以考虑成是同步的，为此我们会对时间的概念进行介绍。在同步的模型中对系统来进行推论会简单得多，他假设处理器们会以相当的速率处理消息，传输的延迟是有边界的，消息的传递也不可能会花费无限长的时间。

一个同步的系统还可以呈现出具有同步的本地处理时钟的特点：两个本地处理的时间来源之间的差异具有一定的上界。

我们可以在设计使用同步模型的系统中使用超时，我们可以基于超时来构建更复杂的抽象，比如 *Leader Election* 领导者选举，*Consensus* 共识，*Failure Detection* 故障检测等。这使得设计中的最佳场景能够更加健壮，但也导致了在对时间做出的假设不成立时会产生故障。比如在 Raft 一致性算法中，我们会遇到有多个处理器都觉得自己是 *Leader* 的情况，他是通过强制将落后的处理器接受其他人是 *Leader* 来解决这个问题的；错误检测的算法也可能会错误的将正常的处理器视为发生故障。在设计我们的系统时，要确保能够考虑到这些可能性。

异步及同步模型中的属性可以进行结合，然后我们可以将系统当成具有局部的同步性。局部同步性的系统会表现出一些同步系统的属性，但消息传递、时钟偏差跟相关处理器之间的速度的边界不一定是一致的，并且只在大部分情况中是有效的。

同步性对分布式系统来说是一个必要的属性：他对性能、扩展性跟通用的处理都有影响，还有许多的因素会对系统功能的正确性产生影响。我们在书中讨论的某些算法也都是建立在同步系统的假设上运行的。