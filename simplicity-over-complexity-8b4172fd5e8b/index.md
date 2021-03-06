# 外部资源
+ 最低可行产品
+ 帕累托原理
+ 奥卡姆剃刀
+ 简单还是复杂？
# 而且，简单性更好

而且，我们仍然需要知道理想是什么。 我们需要知道我们正在争取什么，以便我们知道何时弯曲它，以便我们知道为什么弯曲它。

没有神奇的解决方案。 没有三步指南。 在简单性和复杂性之间是否达到了良好的平衡，只有在以后才能看到。 一旦做出决定，通常就无法更改或更改成本很高。

但是，如果我们计划继续进行某个项目至少更长的时间，那么我们应该考虑我们自己的未来，他们将不得不接受这个决定。

从长远来看，此功能真的很好吗？
# 每个异常都是邪恶的吗？

另一方面，在编写代码时，我们希望现实生活中的人将其用于现实生活中的问题。 现在，向我展示自然界中的一个问题，它有一个干净，简单的解决方案，无一例外！ 没有了。 生活很复杂，代码也很复杂。

只有在理论上，我们才能“忽略此物理公式中的空气阻力”。
# 增加复杂性的充分理由是什么？

在纸上，以上所有似乎都是合乎逻辑的。 但这也很模糊。 甚至没有什么类似于复杂性或简单性的实际定义，没有任何经验可以用来判断哪个功能值得一个月的努力，哪个六个月值得一天的努力。 这是开始起雾和争吵的地方。

开发人员和管理人员不喜欢该准则的真正原因是我们不同意“简单”的含义。

如果我正在开会，并且最大的客户说服我，如果我们在本季度末不交付X，他们将离开我们的公司，那么在我看来，这就像“我们的公司在 在线”是增加复杂性的疯狂理由。

但是，如果我是该项目的新开发人员，并且我可以看到该软件因拙劣的通过项目而备受打击，那么我也可以确信，如果我们现在不采取行动并开始为过去的错误判断付出代价，那么这个项目就是 无论哪种方式注定的失败。

那么我们该怎么办？

我们提前计划。

这种情况可能无法解决。 解决它的最有效方法是避免它。 我们不希望自己的位置变得如此复杂，以至于我们在维护该项目时遇到困难。

undefined

项目越复杂，新人们有意义地帮助所需的时间就越长。 该项目越来越依赖其原始作者，这是唯一仍然知道在何处以及为什么增加了复杂性的人。 但是由于忘记了功能和流程，该项目也变得越来越麻烦。 而且，随着越来越多的越野车出现，它还使用了灵活性。 迟早会有很多错误成为功能。 用户不知道要使用的功能，不知道要使用的功能。 他们开始依赖于已损坏的功能，从此以后的每项更改都是不可靠的承诺。

有趣的是，团队有时使用测试来缓解此问题。 即使是无意的事情，只要测试有效，只要我们不小心改变了逻辑，它就会警告我们。 但是我认为这是徒劳的。 正确阅读，理解或维护的测试很少。 这些测试就像派遣醉酒的边防人员到边境一样。 我们看到了它们，但我们并不认真对待它们。
# 复杂性如何影响项目

在项目开始时，没有代码，没有规范。 未来（我们将要创造的东西）令人生畏，但过去（我们确实创造的东西）很简单。 到目前为止，我们还没有创建任何东西，这很简单； 任何人都可以做到🙃。

现在我们需要创建一些东西。 我们无法一次创建所有内容； 我们应该从什么开始呢？

如果我们相信蓬勃发展的启动场景，那么务实的方法是从MVP开始。 MVP代表最低限度可行的产品，该产品具有足够有用的功能，可以成功完成其主要任务。 此阶段的目标是保持开发项目的成本低廉，直到我们有证据证明我们正在开发正确的功能。

MVP原理只是“简单胜于复杂”的表述。应该使用能够解决问题的最简单解决方案。 在没有充分理由之前，不要增加复杂性（即成本）。

帕累托原理中也存在类似的概念，也称为80/20法则或少数几个人的法则。 《帕累托原理》指出，在许多事件中，大约80％的影响来自20％的原因，即80％的错误报告是由20％的错误引起的； 80％的时间使用了20％的功能。

帕累托原理起源于统计学，经济学，但已应用于广泛的主题。 它很好地支持了我们的“简单性而不是复杂性”概念。 如果80％的客户仅使用20％的可能工作流程，为什么还要麻烦地为我们的软件支持所有可能的工作流程？

因此，要确定首先开发哪些功能，我们必须保持谨慎。 我们构建的所有内容都将需要一段时间的支持。 我们添加到软件中的所有内容都会产生维护成本，并且会影响我们构建其他完全无关的新事物的方式和成本。
# 那么“简单胜于复杂”到底意味着什么？

本指南希望您倾向于使用更简单的解决方案。 您应该经常问自己：您是否可以简化代码并仍然达到相同的结果？ 您可以简化设计并仍然达到相同的目标吗？

可能是一些小事情，例如：您是否过度使用了强大的语言结构？ 您将从try-except语句中受益，还是简单的if语句更适合您的流程？

或者可能是更大的事情：您是否应该真正支持20种不同的方案，还是仅提供最常见的三种方案就可以实现可比的用户体验？

该指南促使您对复杂性保持警惕，并要求增加它的充分理由。
# 简单而不是复杂！
## 或者是周围的其他方式？
![](1*axRvj6wF1-L28insQaqjuA.jpeg)

今天，我得出了两个认识，它们都令人惊讶，而且都至关重要。 在关于代码审查的无害辩论中，我突然发现，只有很少的基本思想是我所有与编码有关的决定的基础。 其中之一是：简单胜于复杂。 大约三秒钟后，我意识到这既不是众所周知的口头禅，也不是可以快速解释的口头禅。 坚定了自己的信念。 但是不必等待几年，我如何向队友解释呢？

对我而言，“简单而不是复杂”是对多种口味的实用答案，这是一把简单的Occam剃刀。 它给了我两个好处：
+ 它使我可以将问题分为现在需要解决的部分和可以推迟的部分。
+ 它使我对自己的决定充满信心，因为它得到了许多其他定理，原则，规则和准则的支持。
```
(本文翻译自Ines Panker的文章《Simplicity Over Complexity!》，参考：https://medium.com/better-programming/simplicity-over-complexity-8b4172fd5e8b)
```
