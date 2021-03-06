# Part 1

## Storage Engine 存储引擎

数据库管理系统的的主要工作是可靠的将数据进行存储，并在需要时提供给用户使用。我们使用数据库作为主要的数据来源，帮助我们在应用的各个模块间共享数据。我们倾向于使用数据库，而不是每次创建新应用时都尝试新的方法来存储、获取跟管理数据。这样我们就能够将精力集中在应用的逻辑而不是底层设施上了。

因为 **数据库管理系统** *(DBMS)* 这个词所表达的含义已经越来越复杂了，在本书中我们将使用更简洁的名词，**数据库系统跟数据库** 来表达跟他一样的概念。

数据库是个多部件的系统，他由多个不同的组件组成：包括传输层接收请求，查询处理器确认查询最有效的实现方式，执行引擎处理所有的操作，以及存储数据的存储引擎。

数据库管理系统使用存储引擎来存储、查询以及管理内存或磁盘中的数据，他被设计来持久化每个服务节点的内存中的数据。为了让数据库能够响应各种复杂的查询，存储引擎提供了许多细粒度的简洁的 API 接口，让用户能够创建、更新、删除跟获取数据记录。因此数据库管理系统基于存储引擎来构建，提供了结构定义、查询语言、索引、事务及其他各种有用的特性。

为了灵活性，键跟值并没没预定的格式，而是都被看待为严格的字节序列。因此那些排序或表示的语义都在更高层级的子系统中定义。比如可以使用 `int32` *(32-bit integer)* 作为一个表的键，然后其他的都是 `ascii` 值，而从存储引擎的角度来看，这些键都只是需要序列化的条目而已。

存储引擎如 `BerkeleyDB` 、`LevelDB` 及他们的衍生数据库如 `RocksDB`、`LMDB` 及他们的衍生数据库如 `libmbx` 、`Sophia`、`HaloDB`，都作为一些独立的存储引擎插件被使用。使用插件化的存储引擎让数据库的管理员在能够管理数据库能够从现有的一些存储引擎中做选择，并考虑其他子系统的状况。

同时，数据库系统中清晰分离的组件机制给了每个人机会去选择自己的存储引擎，比如从用例中选择合适的存储引擎，比如 `MySQL` 这个最流行的数据库管理系统，拥有数种存储引擎，其中包括了 `InnoDB` 、`MyISAM` 及 `RocksDB` ，`MongoDB` 则允许我们从 `WiredTiger`、内存是的或已弃用的 `MMAPv1` 等存储引擎。

### Comparing Databases

对数据库系统的挑选可能是因为一系列的因果选择。如果所挑选的数据库可能会因为性能不够好、一致性问题或一些操作上的挑战，那最好是能在开发阶段就发现这些问题，因为迁移到另一种数据库系统可能并不容易。在某些情况下，可能还会导致需要对应用的代码进行大量的修改。

每个数据库系统都有他的优点及缺点，为了减少迁移可能造成的风险，你最好先花费一些时间来调研数据库的各项能力是否能够满足所需要构建的应用。

一般来说我们会使用数据库的基本组件来对他们进行各个范围的比较 *(比如使用了哪种存储引擎，数据是如何分片、复制跟分布的等等)*，他们的排位 (如其在一些咨询公司如 **ThoughtWorks** 或者一些数据库比较的站点如 **DB-Engine**、**Database of Database** 上的 流行程度)，或是他们实现所用的编程语言 *(C++、Java 或 Go 等)* 都能够导致无效或过早的抉择。这些因素都只能用在较高层次上的比较，或是用来做一些粗略的选择，比如从 HBase 跟 SQlite 上做选择，因此对数据库的功能或其内在实现进行一些粗略的了解，可能都比上面的那些比较方式来得更加有用。

每一个比较方式都应该从一个定义清晰的目标开始，因为就算是一些轻微的偏向性都可能会导致所作的选择全盘失效。如果你在寻找一个匹配你现在正在进行的工作负载量 *(或计划中)*，你能做的最好的事情就是在不同的数据库系统中模拟你所需具体的负载量，确认具体的性能指标对你以及比较的结果都是非常重要的。有些问题，特别是像性能或是扩展性上的只会在一段时间或是数据量不断增长后出现。为了能够发现这些潜在的问题，最好的方法就是有一个能够长时间运行的并尽可能模拟真实产品运行场景的测试环境。

模拟真实环境的负载不知能够让你了解到数据库的运行状况，还能够帮助你学习到如何操作、调试及发现相关社区的友好及帮助的氛围。数据库的选择常常都是由这些因素组成的，而性能往往最后不是那最重要的因素：数据库最终能够提供一个较慢的处理性能，总好过完全不可用。

为了比较数据库，了解现在以及将来所需要使用具体的用例是非常有帮助的，比如：

- 数据结构及记录的数据量
- 客户端的数量
- 查询的类型及访问的模式
- 读取与写入之间的比例
- 以上这些信息可能会改变的是哪些

了解了上述的这些变量能够帮助我们回答下列的这些问题：

- 数据库是否支持我们所需的查询
- 数据库是否能够处理我们预计需要存储的数据量
- 单个的数据库节点能够处理多少读取跟写入的操作
- 我们的系统会需要多少个数据库节点
- 在预定的增长率上，如何来扩展数据库集群
- 数据库需要哪些管理操作

回答了这些问题后，就能够构建一个测试的集群，然后来模拟具体的负载了。大部分的数据库都会有压力测试工具用来构建一些特定的使用场景。如果对应的数据库没有标准的测试工具能够用来生成实际的随机工作负载测试，那这可能是一个危险的信号。如果基于某些原因无法使用默认的工具，那你可以尝试一些已经广泛使用的工具，或是自己去实现一套。

如果测试最终都有比较良好的结果，去了解数据库的代码可能会非常有用。查看这些代码，首先看看数据库各个部分各个模块的代码是有用的，找到数据库的各个模块的代码，然后导航过去看看。就算只是对代码有个粗略的了解，也能够帮助你更好的了解那些日志是如何产生的、有哪些配置项，还能够帮助你去定位应用中使用数据库所产生的问题，或是数据库本身有什么问题。

如果能够把数据库当成一个黑盒子来使用，并且永远都不去查看他的内部当然很好，但实际的经验告诉我们，最好是对或早、或晚肯定会出现 Bug、运行中断了、性能倒退了或是其他的一些问题提前做好准备。如果你对数据库的内部有所了解，你能够减少这些工作上的风险并且提高能够快速修复他们的机会。

有一个流行的用来进行基准性能测试的比较工具是 `Yahoo! Cloud Serving Benchmark`(YCSB)。YCSB 提供了一个框架及一些可以用来应用到不同数据存储的常见负载集合。跟很多其他的通用工具一样，我们需要谨慎的使用他，因为他可能很容易就给我们下一个错误的结论。为了能够的带一个公平的比较结果跟做一个合适的选择，我们需要投入足够的时间来了解不同数据库在真实场景中的表现，并为他们定制基准测试。

> ### TPC-C Benchmark
>
> Transaction Processing Performance Council (TPC) 有一系列基准提供给数据库开发商用来比较跟发布他们自身产品的测试结果。TPC-C 是一个在线事务处理 (OLTP) 基准，混合了读取及写入的事务来模拟常见的应用工作负载。
>
> 该基准关注并发事务的性能及正确性，其中主要的性能指标是 `throughput` 吞吐量: 即数据库系统在每分钟能够处理的事务量。该基准在执行事务需要维持 ACID 属性并遵从这些属性所做的定义。
>
> 该基准不关注那些特定的商业场景，它只是提供了一些抽象的对于大部分使用 OLTP 数据库的应用来说非常重要的操作集合。其中包含了一些仓储、股票、客户跟订单管理的表跟实体，具体的数据表布局、事务的详情都能在这些表信息的周围获取到，还包括了每个表最少的数据量跟数据跟数据可靠性的限制。

这并不意味着这些基准只适用于对数据库进行比较，基准测试对于服务级别的一致性、了解系统要求、容量规划等细节都是非常有用的。在使用数据库前对他了解得越多，在真实的产品运行中所需要花的时间就越少。

选择一个数据库是一个耗时长久的决定，最好还能够对其版本的更新迭代保持跟踪，去明白每次更新的内容跟思考其具体的原因，然后制定好升级的策略。新的版本通常都会包含一些提升或修复一些 Bug 或者安全性之类的问题，但同时也可能会产生新的 Bug、性能的回归或一些未定义的行为，因此在升级前对新版本进行完善的测试也是非常重要的。回顾数据库的实施人员以前是如何处理升级的能够帮助我们了解以后可能会遇到的各种情况。过去那些平滑的升级不代表以后的升级都会是平滑的，但过去如果有复杂的升级过程意味着以后的升级也可能没那么容易。

### Understanding Trade-Offs

作为用户，我们需要看到数据库在不同的环境中会有什么不同的表现，但当我们在使用数据库时，需要针对这些行为来做出具体的决定。

设计存储引擎比实现哪些教科书中的数据结构要难得多，因为很难在一开始就把太多的细节跟边界场景考虑清晰。我们需要去设计物理上的数据布局跟如何组织那些指针信息，要设计那些序列化的数据格式，要了解数据将会如何进行垃圾回收，要了解存储引擎如何去适配整个数据库的语义，要解决如何运行在并行的环境中，最后还要确保在任何情况下都不会有数据丢失的情况发生。

其中不只要对很多事情做决定，更重要的是其中的大部分决定都需要进行权衡。比如，如果我们以数据保存的顺序来存储到数据库，那我们可以以较快的速度来完成存储，但如果后续想按照字符的顺序来获取这些数据，那我们需要在将数据返回给客户端之前对他们重新排序。在本书后续我们可以看到，有很多设计存储引擎的方式，每种不同的实现都有着他的优点跟缺点。

在我们调研一个不同的存储引擎时，会同时对他的优点跟缺点进行分析。如果有一个符合所有我们所需要的场景的存储引擎，谁都会选择使用它，很遗憾的是并不存在这样的引擎，因此我们需要理智的，基于我们具体的负载跟所需的场景来进行选择。

现在有非常多的存储引擎，使用各种不同的数据结构，不同的开发语言，从 C 这种底层类别的语言到 Java 这种高层语言都有。但所有的存储引擎面对的都是相同的挑战跟约束。跟城市规划做类比，我们可能会为了特定的人群选择建立高楼或是往外扩展。在这两种处理方式中，这座城市能够容纳同样的人数，但两种做法可能会为他们带来不一样的人生。当我们选择了高楼，人们可能会住公寓并且因为人群集中导致更大的交通压力；如果是往外扩展，人们可能会住在自己的房子中，但人与人之间的交流距离可能会变得更远。

同样的，开发人员在存储引擎中所作的选择可能也是会偏向于某些类型: 有些优化是为了更低的读写延迟，有些是为了提供更大的数据密度 *(比如为了让单个节点存储更多数据)*，而有些则可能集中于如何让操作更加简单快捷。

在本书每章的总结中你可以找到具体算法的实现以及其相关的引用信息，通过本书能够让你具有充分利用这些资源的能力，并对其中所描述的各种概念有深刻的理解。