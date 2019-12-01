
这篇文章对您有用吗？ 我希望听到您的反馈，所以请不要退缩！ 如果您对Kafka或事件流感兴趣，或者有任何疑问，请在Twitter上关注我。

总而言之，尽管有上述几点，我也不会说卡夫卡是垃圾。这恰恰相反。 当然，卡夫卡并非没有缺陷。 轻描淡写地说，工具是低于标准的。 卡夫卡（Kafka）配置选项的广度令人难以置信，默认设置中充斥着陷阱，足以震惊那些毫无戒心的初学者。 但是，作为事件流平台，Kafka改变了我们现在架构和构建复杂系统的方式。 它为我们提供了选择，这是一件好事。 它的好处超越了多余的东西，并且使那些已经被如此积极采用的技术束缚住了所有的麻烦。
![](1*xd_SSivYhyvoWf16VONHDQ.jpeg)
# 卡夫卡·格查斯
## 很好，但不完美

我曾协助数家大型客户使用Kafka作为消息传递主干构建微服务风格的体系结构，并对它的功能和真正使它们发挥作用的用例有相当好的了解。 但是我绝对不是卡夫卡的辩护律师。 经历了如此迅速的采用曲线的任何技术都必定会使其受众两极分化，并以某种错误的方式吸引某些开发人员，Kafka也不例外。 像其他任何事情一样，您需要花费大量时间来全面了解Kafka和事件流，然后才能完全熟练并可以利用其能力。 一路走来，准备面对一两个挫败感。

我整理了一些缺点，这些缺点可能会导致开发人员感到沮丧，或者赶不上毫无戒心的初学者。 没有特别的顺序：
# 可调旋钮太多

Kafka中的配置参数数量可能不计其数，不仅对于新手来说，对于经验丰富的专业人士也是如此。 可能是JVM的唯一例外，我想不出具有这么多配置参数的另一种技术。 这并不是说不需要配置选项； 但有人想知道，这些参数中有多少可以被人体工程学代替，就像Java对G1所做的那样。 因此，与其指定过多的单个阈值和公差，不如让操作员设置性能目标，并让系统得出最能满足该目标的最佳值集。
# 不安全的默认值

这是我对config选项的最大抱怨。 Kafka的作者围绕其订购和交付保证的实力提出了几项大胆的主张。 如果您认为默认值是明智的，那么您将被原谅，因为默认值应该使安全性胜于其他竞争质量。 Kafka默认值通常会针对性能进行优化，并且在安全性很关键的情况下，需要在客户端上明确覆盖默认值。 幸运的是，设置属性以保证安全性对性能仅产生很小的影响-卡夫卡仍然是野兽。 记住优化的第一条规则：不要这样做。 如果卡夫卡的创作者给予更多考虑，卡夫卡本来会更好。 我指的是一些具体示例：
+ enable.auto.commit-默认为true，这导致使用者每5秒提交一次偏移（由auto.commit.interval.ms配置），而不管使用者是否已完成处理记录。 通常，这不是您想要的，因为它可能导致混合的交付语义-在使用者失败的情况下，某些记录可能会交付两次，而另一些记录可能根本无法交付。 默认情况下，应该将其设置为false，让客户端应用程序指定提交点。
+ max.in.flight.requests.per.connection —默认为5，如果一个（或多个）排队的消息超时并重试，则可能导致消息乱序发布。 这应该默认为1。
# 令人震惊的工具

命令行参数的命名不一致，并且发布键式消息的简单操作要求您跳过圈-传递晦涩的，未记录的属性。 甚至不支持某些本机功能，例如记录标题。 内置工具的可用性是Kafka社区中众所周知的痛点。 这真是可耻。 这就像购买法拉利，只是要用塑料轮毂盖交付。 长期以来，大多数Kafka练习者都放弃了现成的CLI实用程序，而转而使用Kafdrop，Kafkacat等其他开源工具以及Kafka Tool等第三方商业产品。
# 复杂的引导过程

客户端用于建立代理连接的引导和服务发现过程很复杂，并且容易使用户感到困惑。 最初将为客户端提供代理地址和端口的列表。 然后，客户端将直接连接到一个地址，发现其余的代理节点，然后再直接建立与所发现节点的新连接。 在简单，同质的网络设置中，这非常简单，其中来自所有客户端和对等节点的所有连接都遍历单个入口。 在异构网络中，可能存在多个入口点以隔离经纪人与经纪人的通信，生活在同一本地网络上的内部客户端以及可能通过Internet连接的外部客户端。 引导/发现过程需要特殊的配置，需要专用的侦听器和一组单独的已通告的侦听器，这些侦听器将呈现给连接的客户端。
# 摇摇欲坠的客户端库

使用Java，Python，.NET和C以外的语言编写的客户端库的质量/成熟度均未达到标准。 如果您是Java开发人员，那么就已经做好了–那就是大部分开发工作的集中地。 但是Golang和其他社区在努力获取稳定的库方面一直很努力，尽管其中一些“独立”库已经存在了好几年，但我在这些语言中遇到的一些错误的数量和严重性却是 真正有关。
# 缺乏真正的多租户

据Kafka的维护者说，它支持多租户。 本设计仅限于访问控制列表（ACL）来隔离主题和维护配额，这给客户端带来了隔离的幻觉，但并未在管理平面中创建隔离。 这就意味着您的冰箱支持多租户，因为它可以让您将食物存放在不同的架子上。 真正的多租户解决方案将在较大的物理群集中提供多个逻辑群集。 这些逻辑集群可以单独管理； 例如，一个逻辑集群中ACL的配置错误对其他逻辑集群没有影响。
# 缺乏地域意识

地理复制不是内置于代理中的，并且公认的是高性能的Kafka群集和“拉伸”拓扑不会混合使用。 有一个开源项目MirrorMaker，它实际上是一个管道，用于将记录从一个集群泵送到另一个集群，而无需保留任何关键的元数据（例如偏移量）。 Confluent拥有其专有工具Replicator，该工具将保留元数据，但它是许可的Confluent Enterprise套件的一部分。