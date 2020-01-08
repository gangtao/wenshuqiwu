# 进一步阅读

如果您认为这是您想尝试了解的更多信息，请查看以下内容：
+ http://www.oreilly.com/webops-perf/free/chaos-engineering.csp
+ http://principlesofchaos.org/
+ https://www.gremlin.com/the-discipline-of-chaos-engineering/
# 小心

请记住要先理解，然后才能进行混沌实验。 您应对自己的行为负责。
# 如何设计混沌实验？

如书中所建议，可以通过考虑以下步骤来设计混乱：
+ 选择一个假设。
+ 选择实验范围。
+ 确定您要观看的指标。
+ 通知组织。
+ 运行实验。
+ 分析结果。
+ 增加范围。
+ 自动化。

步骤和细节可能因系统而异，但总体设计应围绕上述步骤进行。
# 混沌工程高级原理

根据http://principlesofchaos.org/，以下是混沌工程学的高级原理。
## 1.建立关于稳态行为的假设

关注于系统的可测量输出，而不是系统的内部属性。

通过关注实验过程中的系统行为模式，混乱可以验证系统是否有效，而不是试图验证其工作方式。
## 2.改变现实世界中的事件

混沌变量反映了现实世界中的事件。 通过潜在影响或估计频率对事件进行优先级排序。

考虑与硬件故障（例如服务器死机），软件故障（例如格式错误的响应）以及非故障事件（如流量高峰或扩展事件）相对应的事件。

在混乱的实验中，任何能够破坏稳态的事件都是潜在的变量。
## 3.在生产中进行实验

系统的行为会有所不同，具体取决于环境和流量模式。 混沌强烈希望直接对生产流量进行试验。
## 4.自动化实验以连续运行

混沌实验应该连续进行，而不是一次性或定期检查。
## 5.最小化爆炸半径

在生产中进行试验有可能导致不必要的客户痛苦。 因此，混乱的工程师需要确保实验的影响是可管理的。
# 我们应该练习混沌工程吗？

从书中引用：

“您的系统是否能够应对诸如服务故障和网络延迟峰值之类的现实事件？”

如果答案是否定的，则需要练习混沌工程。 您应该拥有强大的监视系统来了解系统状态。

随着我们越来越趋向于基于微服务的体系结构，实践混沌工程变得至关重要。
# 谁来实践混沌工程？

已经建立了专门针对该工程学科的社区，例如http://chaos.community/。

社区显示，混沌工程的从业者来自Google，Amazon，Uber，Yahoo！，Dropbox，Visa，New Relic等公司，而且这一数字每天都在增长。

这种做法不仅限于基于软件的公司，而且还在国防，制造，农业，医疗，金融等领域不断发展。
# 混沌实验

现在，让我们尝试了解什么是混乱的实验。
+ 如果您正在运行Hadoop环境，请关闭Hadoop集群的几个节点，甚至通过关闭高可用性组件而造成混乱。
+ 在Kafka群集上，从特定分区或主题中删除消息。
+ 使系统伪装不同步。
+ 在Elasticsearch群集，NoSQL群集，Web服务器等上消耗CPU /内存。
+ 在功能上注入混乱。

这些是一些示例，对系统的正确研究将有助于确定系统的实验。
# 测试与混沌工程

大多数时候，一个好的测试计划会讨论负载测试，安全性测试和负载时的功能测试。

不幸的是，我们仅在非生产环境中进行这些测试。 我们仅测试非生产环境，并希望系统在生产环境中的行为相同。

这是混乱工程试图通过尽可能接近生产环境甚至有时在生产环境中进行实验来准备我们的地方。

测试和混乱工程之间的另一个区别是，混乱工程的结果带来了有关系统的新知识，即使开发人员或测试人员也可能不知道。
# 为什么每个软件开发人员都需要学习混沌工程
## 混沌工程是在生产中的软件系统上进行实验的学科
![Photo by Markus Spiske on Unsplash](1*PIrXG7XzvHAg1B8Ti2qi1w.jpeg)
> Photo by Markus Spiske on Unsplash


作为负责管理大型系统的技术人员，您始终需要考虑系统的连续性，安全性和可管理性。

最近，我花了很多时间来更好地了解如何为大型分布式系统制定适当的灾难恢复（DR）和业务连续性计划（BCP）。

我寻求更多有关该主题的追求最终导致被介绍给每个系统都应采用的新工程流-混沌工程！

最后，我读了O'Reilly的一本名为《混沌工程》的免费书—通过实验建立了系统行为的信心。 我已经知道Netflix的Chaos Monkey已有很多年了，但是我选择永远不要说自己正在建立另一个Netflix，直到最终读完这本书。

这本书从对混沌工程的非常有趣的定义开始-

“混沌工程学是在分布式系统上进行实验的学科，目的是建立对该系统在生产中承受动荡条件的能力的信心。” —混沌原理

Gremlin的另一个非常简单但有意义的定义是：

“故意破坏事物以构建更具弹性的系统！”

我从没想过混乱可以用来带来纪律。

在分布式系统中，您将永远无法避免所有故障，但始终可以为此做好准备。 在基础架构上进行试验时，您会了解系统的弱点，并可以更好地计划避免这些弱点。

现在，您一定想知道-混沌工程与测试有何不同？ 让我们尝试更好地理解这一点。
```
(本文翻译自Tanmay Deshpande的文章《Why Every Software Developer Needs to Learn Chaos Engineering》，参考：https://medium.com/better-programming/why-every-software-developer-needs-to-learn-chaos-engineering-ef08992f4354)
```