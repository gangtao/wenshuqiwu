# Occam的Razor：使代码简洁明了
![](1*MiZt64Bfp287J6ej1pIk1g.jpeg)
# 背景

在我的Group Randomizer应用程序中，我的MVP（最低可行产品）的功能之一是创建保存组功能。 当用户单击“保存组”按钮时，它将当前选项列表保存为新组。 但是，此功能的核心功能是，如果找到一个具有相同选项的现有保存组，而不考虑顺序，则将显示一条警报，指出具有您当前选项列表的组已经存在。

例如，“保存的组＃1”具有人员列表，即“山姆”和“鲍勃”。 如果我当前的选项列表是“ Bob”和“ Sam”，并且我尝试将其另存为新组，则会弹出警报，提示“具有当前选项列表的已保存组已存在。 它是保存的组＃1”。

对于本博客，我将介绍如何创建算法来创建此检查功能以及Occam剃刀的应用。 如果您不熟悉Occam的剃刀，则Wikipedia的定义是：

奥卡姆（Occam）的剃刀……是解决问题的原则，其中指出“不应在没有必要的情况下复制实体”。
# 尝试检查组算法

下面的代码是我第一次尝试检查组算法。
```
function checkGroups(savedGroup, currentListOfOptions) {  savedGroupHash = {}  // populates the savedGroupHash based on the contents of the   savedGroup array parameter  for (let i = 0; i < savedGroup.length; i++){    savedGroupHash[savedGroup[i]] = true  }  // checks the savedGroupHash against the current list of options to check if savedGroupHash contains all of the list of options  for (let j = 0; j < currentListOfOptions.length; j++) {    if (!savedGroupHash.hasOwnProperty(currentListOfOptions[j])) {      return false    }  }    return true}
```

注意：此算法的参数均为数组。 每当下面提到“选项”时，它就是指它们各自数组中的元素。

为了提供有关如何使用该算法的总体信息，我创建了两个for循环。 第一个for循环根据savedGroup参数的内容填充了saveGroupHash。 对于键值对，键是默认值为true的选项。 此值（或缺少该值）将在第二个for循环中用作布尔值。 在第二个for循环中，我对照了savedGroupHash检查了currentListOfOptions参数中的每个选项。 只要currentListOfOptions中的选项未包含在savedGroupHash中，我将返回false，这将立即退出该函数。 如果不是，那么最后一行将返回true，因为从第二个for循环开始它没有返回false。
# 在检查组算法中测试首次尝试

根据我在上一个博客中进行正确测试的经验，我决定创建一些测试用例以彻底测试我的算法。 在这种情况下，想到了三种情况。

1. savedGroup和currentListOfOptions实际上具有完全相同的选项，但顺序不同。 这应该返回true.2。 savedGroup包含与currentListOfOptions相同的选项，但具有比currentListOfOptions更多的选项。 这应该返回false.3。 currentListOfOptions包含与saveGroup相同的选项，但具有比saveGroup更多的选项。 这应该返回false。

在第一种情况下，我们使用saveGroup = [“ Sam，” Bob“]和currentListOfOptions = [” Bob“，” Sam“]。 接下来，让我们将这两个变量作为参数输入到算法中，然后控制台记录返回值。
```
const savedGroup = ["Sam", "Bob"]const currentListOfOptions = ["Bob", "Sam"]console.log(checkGroups(savedGroup, currentListOfOptions)) //true
```

看起来这已经通过了我们的第一个测试用例。 让我们继续第二个测试用例。

在第二种情况下，我们使用savedGroup = [“ Sam”，“ Bob”，“ Jane”]和currentListOfOptions = [“ Bob”，“ Sam”]。 接下来，让我们将这两个变量输入算法，然后控制台记录返回值。
```
const savedGroup = ["Sam", "Bob", "Jane"]const currentListOfOptions = ["Bob", "Sam"]console.log(checkGroups(savedGroup, currentListOfOptions)) //true
```

看起来这没有通过我们的第二个测试案例。 让我们继续第三个测试案例。

在第三种情况下，我们使用savedGroup = [“ Sam”，“ Bob”]和currentListOfOptions = [“ Bob”，“ Sam”，“ Jane”]。 接下来，让我们将这两个变量输入算法，然后控制台记录返回值。
```
const savedGroup = ["Sam", "Bob"]const currentListOfOptions = ["Bob", "Sam", "Jane"]console.log(checkGroups(savedGroup, currentListOfOptions)) //false
```

看起来这已经通过了我们的第三个测试用例。

嗯……看来此算法无法正常工作。 在分析完我的代码后，看起来每个参数的长度差异可能会使其丢掉。 如果是这种情况，请更改算法以适应这种情况。
# 检查组算法的第二次尝试

下面的代码是我第二次尝试检查组算法。
```
function checkGroups(savedGroup, currentListOfOptions) {  const savedGroupHash = {}  for (let i = 0; i < savedGroup.length; i++) {    savedGroupHash[savedGroup[i]] = 1  }  for (let j = 0; j < currentListOfOptions.length; j++) {    if (savedGroupHash.hasOwnProperty(currentListOfOptions[j])) {      savedGroupHash[currentListOfOptions[j]] -= 1    } else {      savedGroupHash[currentListOfOptions[j]] = 1    }  }    let sum = Object.values(savedGroupHash).reduce( (acc, current) => acc += current)  if (sum === 0) {    //this means the same group already exists    return true  } else {    //this means the group does not already exist    return false  }}
```

为了提供对该算法的总体概述，有两个for循环，一个累加器和一个if / else语句。 第一个for循环与第一个算法中的第一个for循环几乎具有相同的功能，但是，它提供了默认值1。第二个for循环为currentListOfOptions中的每个选项操纵saveedGroupHash。 如果该选项位于SavedGroupHash中，则将值减1，结果为0；否则，添加一个新的键值对，其中键为选项本身，值为1，类似于第一个 for循环。

接下来，使用累加器，它将获取saveGroupHash中所有值的总和。 sum的目的是帮助确定saveGroup数组和currentListOfOptions数组之间的长度是否存在差异。 我在if / else语句的条件比较中使用总和，以便返回true或false。

现在是令人不安的部分：测试此新算法。
# 在检查组算法中测试第二次尝试

为了保持一致性，我将使用与首次尝试该算法时相同的测试用例。 为简洁起见，我还将结合所有三个测试用例的代码和结果。
```
//Test Case #1const savedGroup = ["Sam", "Bob"]const currentListOfOptions = ["Bob", "Sam"]console.log(checkGroups(savedGroup, currentListOfOptions)) //true//Test Case #2const savedGroup = ["Sam", "Bob", "Jane"]const currentListOfOptions = ["Bob", "Sam"]console.log(checkGroups(savedGroup, currentListOfOptions)) //false//Test Case #3const savedGroup = ["Sam", "Bob"]const currentListOfOptions = ["Bob", "Sam", "Jane"]console.log(checkGroups(savedGroup, currentListOfOptions)) //false
```

是! 看起来该算法正在按预期工作！ 我们终于可以称之为一天了，但是…
# 奥卡姆剃刀

第二天，当我在Group Randomizer应用程序上工作时，我再次查看了检查组算法。 我一直为这个算法的成功而苦恼（因为我花了1-2个小时来开发它），直到我意识到第二种算法完全是矫kill过正。 我是什么意思

让我们再次看看测试用例，以及为什么我改变了对算法的第一次尝试。 导致测试失败的根本原因的原始假设是每个参数的数组长度（如测试用例2所示）。 在该算法的第二次尝试中，我操纵了savedGroupHash哈希值，以便跟踪saveGroup和currentListOfOptions之间的数组长度差异。 总和是数组长度之间的差。 如果sum为0，则数组长度相同，并返回true。 其他任何值都将返回false。

换一种方式来看，我本质上是在检查saveGroup和currentListOfOptions的长度是否相同。 由于我知道这两个参数是数组类型，因此我只需在每个参数上调用.length即可确认它们的长度是否相等。 如果这些长度不一样，我可以立即返回false。 下面的代码表示此实现。
```
if (savedGroup.length !== currentListOfOptions.length) {  return false}
```

现在，我可以使用上面的代码修改算法的首次尝试。
```
function checkGroups(savedGroup, currentListOfOptions) {  //insert new code here  if (savedGroup.length !== currentListOfOptions.length) {    return false  }  savedGroupHash = {}  for (let i = 0; i < savedGroup.length; i++){    savedGroupHash[savedGroup[i]] = true  }  for (let j = 0; j < currentListOfOptions.length; j++) {    if (!savedGroupHash.hasOwnProperty(currentListOfOptions[j])) {      return false    }  }    return true}
```

您可能接下来会猜到，我使用此算法运行了所有三个测试用例，并通过了所有三个测试用例！

我能够简化从中检查数组长度的代码
```
for (let j = 0; j < currentListOfOptions.length; j++) {    if (savedGroupHash.hasOwnProperty(currentListOfOptions[j])) {      savedGroupHash[currentListOfOptions[j]] -= 1    } else {      savedGroupHash[currentListOfOptions[j]] = 1    }  }    let sum = Object.values(savedGroupHash).reduce( (acc, current) => acc += current)if (sum === 0) {    //this means the same group already exists    return true  } else {    //this means the group does not already exist    return false  }}
```

至
```
if (savedGroup.length !== currentListOfOptions.length) {  return false}
```
# 第一次尝试检查组算法的意外结果

在测试第一个未修改算法和第二个算法之间的过程中，我意识到了第一个未修改算法的实际作用。 尽管它没有达到检查组是否相同的目的，但它检查了一个组currentListOfOptions是否是另一组saveGroup的子集。 我无意间创建了一种检查子集的算法，而不是检查整个集合的算法。 现在，如果将来需要检查子集，则无需从头开始重新创建算法，也不需要使用第一个未修改的算法来利用它。
# 重要要点

创建此算法时，我学了两个主要课程。
+ 不要因为过于复杂而陷入困境。

在算法的第二次尝试中，我一直在想着该算法必须包含某种复杂的解决方案，因为这不是一个共同的功能（可能不正确）。 如您所知，当可以用三行代码（如果我不使用大括号的话，则只需一行）完成此错误时，我就以一种about回的方式解决了该错误。 如果您开始认为您的解决方案开始变得复杂，请退后一步，重新评估您要达到的目标，然后看看是否可以用其他方式表达它，以寻求更好的方法。

2.研究算法实际上是有帮助的。

像许多有抱负的软件开发人员一样，我将研究不同的数据结构和算法，并在LeetCode等网站上练习求解算法。 起初，我并没有真正了解研究这些算法的目的，因为我觉得我永远不会在技术面试之外应用这些算法。 但是，在我第一次尝试创建检查组算法时，我凭直觉将哈希值用于比较目的。 当我想到为什么这样做时，我突然意识到这是因为使用哈希是解决LeetCode算法以将时间复杂度从O（n²）提升到O（n）的一种常用方法。 现在，我发现我最想不到的算法可能适用于我的代码。
```
(本文翻译自Samuel Guo的文章《Occam’s Razor: Keeping the Code Short and Simple》，参考：https://levelup.gitconnected.com/occams-razor-keeping-the-code-short-and-simple-7ce4b60f87d4)
```
