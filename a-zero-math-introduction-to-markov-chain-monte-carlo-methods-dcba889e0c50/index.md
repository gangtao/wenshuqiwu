
回想一下“什么是马尔可夫链蒙特卡罗方法？”这个问题的简短答案，这里又是TL; DR：

MCMC方法用于通过概率空间中的随机采样来估算目标参数的后验分布。

希望我已经解释了这个简短答案，为什么要使用MCMC方法以及它们如何工作。 这篇文章的灵感来自我在华盛顿特区举行的大会“数据科学沉浸式”课程中的一次演讲。 演讲的目的是向非技术人员介绍马尔可夫链蒙特卡洛方法，我在这里也尝试这样做。 如果您认为此解释在某种程度上不合时宜，或者可以使其更加直观，请发表评论。

有了蒙特卡洛仿真和马尔可夫链的一些知识，我希望MCMC方法如何工作的无数学解释非常直观。

回想一下，我们正在尝试估算我们感兴趣的参数的平均人身高度的后验分布：
![I am not a visualization expert, nor apparently am I any good at keeping my example within the bounds of common sense: my example of the posterior distribution seriously overestimates average human height.](0*XeUN0u_-EPh6MMCV.)
> I am not a visualization expert, nor apparently am I any good at keeping my example within the bounds of common sense: my example of the posterior distribution seriously overestimates average human height.


我们知道后验分布在我们先验分布和似然分布的范围内，但是由于某种原因，我们无法直接对其进行计算。 使用MCMC方法，我们将有效地从后验分布中抽取样本，然后计算统计数据，例如抽取样本的平均值。

首先，MCMC方法选择一个要考虑的随机参数值。 模拟将继续生成随机值（这是“蒙特卡洛”部分），但要遵循确定确定良好参数值的规则。 诀窍在于，根据我们先前的信念，对于一对参数值，可以通过计算每个值解释数据的可能性来计算哪个参数值更好。 如果随机生成的参数值好于最后一个参数值，则会以一定的概率将其添加到参数值链中，概率由其好多少决定（这是马尔可夫链部分）。

为了直观地说明这一点，让我们回想一下，某个值处的分布高度表示观察该值的概率。 因此，我们可以想到在y轴上显示高和低概率区域的参数值（x轴）。 对于单个参数，MCMC方法从沿x轴随机采样开始：
![Red points are random parameter samples](0*fqwsnMwAXnAdWxDH.)
> Red points are random parameter samples


由于随机样本具有固定的概率，因此一段时间后，对于我们感兴趣的参数，它们趋于收敛在最高概率范围内：
![Blue points just represent random samples after an arbitrary point in time, when convergence is expected to have occurred. Note: I’m stacking point vertically purely for illustrative purposes.](0*aYE_6eWzDWfVCOsQ.)
> Blue points just represent random samples after an arbitrary point in time, when convergence is expected to have occurred. Note: I’m stacking point vertically purely for illustrative purposes.


收敛发生后，MCMC采样会得出一组点，这些点是来自后验分布的样本。 围绕这些点绘制直方图，并计算所需的任何统计量：
![](0*fMEvHsN-xlVzLw1H.)

根据MCMC模拟生成的样本集计算出的任何统计量，都是我们对真实后验分布的统计量的最佳猜测。

MCMC方法也可以用于估计多个参数（例如人体的身高和体重）的后验分布。 对于n个参数，在n维空间中存在高概率区域，其中某些参数值集可以更好地解释观察到的数据。 因此，我认为MCMC方法是在概率空间内随机采样以近似后验分布。

理解MCMC方法的第二个要素是马尔可夫链。 这些只是事件序列，它们在概率上相互关联。 每个事件都来自一组结果，每个结果根据一组固定的概率确定下一个结果。

马尔可夫链的一个重要特征是它们没有记忆力：在当前状态下，您可能需要用来预测下一个事件的所有信息都是可用的，并且不知道事件的历史就可以得到新的信息。 像《溜槽》和《阶梯》之类的游戏就表现出这种无记忆性或“马尔可夫特性”，但是现实世界中很少有东西可以这样工作。 然而，马尔可夫链是理解世界的有力方法。

在19世纪，钟形曲线被视为自然界中的常见图案。 （例如，我们注意到人类的身高遵循钟形曲线。）高尔顿板通过将大理石从装有钉子的板上掉下来来模拟重复随机事件的平均值，从而再现了大理石分布的正态曲线：
![](0*HDeFoQPFGs9ueUI0.)

俄国数学家和神学家帕维尔·涅克拉索夫（Pavel Nekrasov）认为，钟形曲线以及更广泛的说是大数定律，只是儿童游戏和琐碎难题的产物，而每个事件都是完全独立的。 他认为现实世界中相互依存的事件（例如人类行为）不符合良好的数学模式或分布。

以马尔可夫链命名的安德烈·马尔科夫（Andrey Markov）试图证明非独立事件也可能符合模式。 他最著名的例子之一是从俄罗斯诗歌作品中数以千计的两个字符组成的对。 利用这些对，他计算了每个角色的条件概率。 也就是说，给定特定的前一个字母或空白，则很有可能下一个字母将是A或T或空白。 使用这些概率，Markov能够模拟任意长的字符序列。 这是一个马尔可夫链。 尽管前几个字符在很大程度上取决于起始字符的选择，但马可夫（Markov）表明，从长远来看，字符的分布会稳定在一个模式中。 因此，即使相互依存的事件具有固定的概率，也要符合平均值。

举一个更有用的例子，假设您住在一间有五个房间的房子里。 您有一间卧室，浴室，客厅，饭厅和厨房。 让我们收集一些数据，假设在任何给定时间点您所处的房间就是我们接下来要说的您可能进入的房间。 例如，如果您在厨房里，则有30％的机会留在厨房，有30％的机会进入饭厅，有20％的机会进入客厅，有10％的机会去 进入浴室，有10％的机会进入卧室。 使用每个房间的一组概率，我们可以构建一系列预测，以预测您接下来可能会占用哪些房间。

如果我们要预测房子里某个人在厨房里待一会儿的位置，那么做出一些陈述可能会很有用。 但是，由于我们的预测只是基于对某人在房屋中的位置的一种观察，因此有理由认为他们的状况不会很好。 例如，如果有人从卧室去洗手间，那么比起从厨房来的人，他们更有可能马上回到卧室。 因此，马尔可夫财产通常不适用于现实世界。

但是，运行Markov链进行数千次迭代，确实可以对您可能位于的房间进行长期预测。更重要的是，此预测完全不受此人开始进入哪个房间的影响！ 从直觉上讲，这是有道理的：在某个时间点某人在房屋中的哪个位置，以模拟并描述他们长期或总体上可能位于的位置，都没有关系。 因此，如果我们了解控制变量行为的概率，则马尔可夫链似乎是在几个周期内对随机变量建模的一种不合理的方法，可以用来计算该变量的长期趋势。

蒙特卡洛模拟只是通过重复生成随机数来估算固定参数的一种方法。 通过获取所生成的随机数并对其进行一些计算，蒙特卡洛模拟提供了一个参数的近似值，其中直接计算它是不可能的，也可能是非常昂贵的。

假设我们要估算跟随圈的面积：
![](0*OVzsV_Mw2OGi1mQ4.)

由于该圆在边长为10英寸的正方形内，因此可以轻松地将面积计算为78.5平方英寸。 但是，我们可以在正方形内随机放置20个点。 然后，我们计算落入圆内的点的比例，然后乘以正方形的面积。 该数字非常近似于圆的面积。
![](0*OuLZBu6HPdhignVB.)

由于20个点中的15个位于圆内，因此该圆大约为75平方英寸。 对于只有20个随机点的Monte Carlo模拟来说还不错。

现在，假设我们要计算蝙蝠侠方程式绘制的形状的面积：
![](0*5ahw9HtOjbMK0tmO.)

这是我们从未学过方程式的形状！ 因此，很难找到蝙蝠信号的区域。 不过，通过将点随机地拖放到包含该形状的矩形中，蒙特卡洛模拟可以非常轻松地提供该区域的近似值！

蒙特卡洛模拟不仅用于估算困难形状的面积。 通过生成许多随机数，它们可以用于对非常复杂的过程进行建模。 实际上，它们是用来预测天气或估算赢得选举的可能性。

那么，什么是马尔可夫链蒙特卡罗（MCMC）方法？ 简短的答案是：

MCMC方法用于通过概率空间中的随机采样来估算目标参数的后验分布。

在本文中，我将不带任何数学解释简短的答案。

首先，一些术语。 感兴趣的参数只是一些数字，它概括了我们感兴趣的现象。通常，我们使用统计信息来估计参数。 例如，如果我们想了解成年人的身高，我们感兴趣的参数可能是以英寸为单位的平均身高。 分布是参数的每个可能值以及我们观察每个参数的可能性的数学表示。 最著名的例子是钟形曲线：
![Courtesy M. W. Toews](0*ZnhfX8oUe0biQRR6.)
> Courtesy M. W. Toews


在贝叶斯统计方法中，分布具有其他解释。 贝叶斯不仅仅表示一个参数的值以及每个参数成为真实值的可能性，还认为分布描述了我们对参数的信念。 因此，上面的钟形曲线表明我们很确定该参数的值非常接近零，但是我们认为真实值在该点之上或之下的可能性均相等。

碰巧的是，人类的身高确实遵循一条正常曲线，所以可以说，我们认为人类平均身高的真实值遵循如下的钟形曲线：
![](0*tlqbgInNAYyi3dgx.)

显然，此图表示的具有信念的人已经在巨人中生活了多年，因为据他们所知，最有可能的成年人平均身高是6'2“（但他们对某一方向并不超级自信）。

让我们想象这个人去收集了一些数据，他们观察到范围在5'和6'之间的人。 我们可以在下面表示该数据，以及另一条正常曲线，该曲线显示哪些平均人类身高值最能解释该数据：
![](0*kkaO7QpZeGOg9DRf.)

在贝叶斯统计中，代表我们对参数的信念的分布称为先验分布，因为它可以在查看任何数据之前捕获我们的信念。 可能性分布通过表示一系列参数值以及每个参数解释我们正在观察的数据的可能性，来总结观察到的数据告诉我们的内容。 估计最大化似然分布的参数值只是在回答这个问题：什么参数值将使其最有可能观察到我们所观察到的数据？ 在没有先验信念的情况下，我们可能会停在那里。

但是，贝叶斯分析的关键是结合先验分布和似然分布来确定后验分布。 这告诉我们，考虑到我们先前的信念，哪些参数值使观察我们所做的特定数据的机会最大化。 在我们的例子中，后验分布看起来像这样：
![](0*3M3HCM8goJjlS-KX.)

上方的红线表示后验分布。 您可以将其视为先验分布和似然分布的平均值。 由于先前的分布更短且分布更广，因此它代表了一组“无法确定”平均人类身高的真实价值的信念。 同时，可能性在相对狭窄的范围内汇总了数据，因此它表示对真实参数值的“更有把握”的猜测。

当先验可能性组合时，数据（由可能性表示）支配了在巨人中成长的假设个体的弱先验信念。 尽管该人仍然认为人的平均身高略高于数据告诉他的高度，但他还是对数据深信不疑。

在两个钟形曲线的情况下，求解后验分布非常容易。 有一个简单的方程式将两者结合起来。 但是，如果我们的先验分布和似然分布不是那么良好怎么办？ 有时，使用没有方便形状的分布来对我们的数据或我们先前的信念建模是最准确的。 如果我们的可能性最好用两个峰值的分布来最好地表示，又由于某种原因，我们想解释一些确实古怪的先前分布，该怎么办？ 我通过手工绘制一个丑陋的先前分布图来可视化以下情况：
![Visualizations rendered in Matplotlib, enhanced using MS Paint](0*PcWai087HhpJtbkm.)
> Visualizations rendered in Matplotlib, enhanced using MS Paint


如前所述，存在一些后验分布，这些后验分布给出了每个参数值的可能性。 但是很难看到它的外观，并且无法通过解析来解决。 输入MCMC方法。

MCMC方法可让我们估算后验分布的形状，以防无法直接计算后验分布。 回想一下，MCMC代表马尔可夫链蒙特卡罗方法。 为了了解它们的工作原理，我将首先介绍蒙特卡洛模拟，然后讨论马尔可夫链。
# 马尔可夫链蒙特卡罗方法的零数学介绍

对于我们中的许多人而言，贝叶斯统计数据充其量是巫术魔术，或者最坏的情况是完全主观的废话。 在贝叶斯方法的商标中，马尔可夫链蒙特卡洛方法尤其神秘。 它们肯定是数学运算繁重且计算量很大的过程，但是它们背后的基本推理（就像数据科学中的许多其他事物一样）可以变得直观。 这是我的目标。
```
(本文翻译自Ben Shaver的文章《A Zero-Math Introduction to Markov Chain Monte Carlo Methods》，参考：https://towardsdatascience.com/a-zero-math-introduction-to-markov-chain-monte-carlo-methods-dcba889e0c50)
```