
大家好，我叫Justin Fuller。 我很高兴您阅读我的帖子！ 我需要让您知道，我在这里写的所有内容都是我个人的观点，并不代表我的雇主。 所有代码示例都是我自己的。

我也希望收到您的来信，请随时在Github或Twitter上关注我。 再次感谢您的阅读！
# 去做我喜欢的事情：任何类型的方法

该帖子最初出现在JustinDFuller.com上。

现在，我已经在《纽约时报》上使用Go作为主要语言，现在，我想探索一下我最喜欢的语言功能。 我不想以此来揭示以前未知的功能或最佳做法； 我只想分享一些喜欢使用该语言的原因。
![Go Things I Love: Methods On Any Type](1*KQgxJN65k173fJ0Q0zRQrA.png)
> Go Things I Love: Methods On Any Type

## 方法

通常，方法定义为属于对象或类的函数。 这意味着您不必向字符串，布尔值或数字添加方法。

此限制可能导致开发人员生成如下代码：
```
const LastOldSchoolID = 23959if id < LastOldSchoolID { // allow access to the old school version of the game}// and elsewhereif id < LastOldSchoolID { // allow access to the old school version of the forum // or some other custom logic for old school players}
```

在这个愚蠢的例子中，有一个游戏最近发布了一个新版本。 在发行前创建帐户的玩家仍然可以玩旧游戏并使用旧论坛。 为此，开发人员遍历了代码库并添加了一个检查：用户的ID是否低于上一个老学校玩家的ID？ 如果是这样，他们可以访问旧游戏。
## 封装形式

不幸的是，社区立即发现了一个错误。 具体来说，单个用户会注意到此错误。 最后一位老派球员被拒登游戏！

开发人员到处都使用检查ID <LastOldSchoolID。 因此，它适用于除最后一位玩家以外的所有玩家。

此时，开发人员被迫搜索该检查的每个实例（很幸运，搜索的实例并不多，只有十几个左右），他们用id <= LastOldSchoolId替换了逻辑。 一切再次恢复正常。

除非不是。 为旧学校登录页面编写逻辑代码的开发人员包括以下代码段：
```
if id >= LastOldSchoolId { return httperrors.Unauthorized(“We’re sorry but you don’t have access to the old school game.”)}
```

因此，不幸的是，该错误仍然存在。

只需封装一下就可以防止一切。 开发人员不应该在整个代码库中重复此逻辑来确定ID是否对旧学校有效。 逻辑应该只存在于一个地方。

值得庆幸的是，Go确实提供了所需的东西。
## 使用自定义类型

用户ID将作为自定义类型实现。 该类型可以单独使用，也可以作为用户结构的一部分使用。 最重要的是，它可以具有自定义方法。

运作方式如下：
```
const LastOldSchoolID = 23959type UserID intfunc (id UserID) IsOldSchool() bool { return id <= LastOldSchoolID // The last oldschool player}func (id UserID) IsNotOldSchool() bool { return !id.IsOldSchool()}
```

请注意，直接添加到UserID类型（即int）的自定义方法。 现在可以重写应用程序周围的代码。
```
if id.IsOldSchool() { // allow access to the old school version of the game}// elsewhereif id.IsNotOldSchool() { return httperrors.Unauthorized(“Please join us playing the new version at game.com/v2.”)}
```

如果仅要做到这一点，那么将为几天之内无法访问游戏的可怜用户节省很多痛苦。 开发人员本可以在代码中的单个位置进行修复，并且该修复将在各处得到应用。
## 更多封装，委托。

有人可能会指出，该代码仍在揭示有关用户和旧式逻辑的太多细节。

为什么其余代码需要知道旧访问权限是由ID确定的？ 如果企业决定更改规则以改为使用创建日期怎么办？ 如果开发人员决定对用户创建IsOldSchool属性，该怎么办？

这些都是有效点。 首先，我请您记住，这只是一个展示Go强大功能的示例。

接下来，我想指出两点。
+ 将方法添加到非结构类型（如int或字符串）可能是一种代码味道，您不必要地泄漏了实现细节或其他应为私有的逻辑。
+ 如果需要隐藏细节，则仍然可以将方法添加到自定义类型中，同时隐藏该逻辑的来源。

请允许我示范。
```
type User struct { UserID}func (u User) IsOldSchool() bool { return u.UserID.IsOldSchool()}func (u User) IsNotOldSchool() bool { return u.UserID.IsNotOldSchool()}
```

在User结构中使用委托。 用户甚至不知道ID如何计算旧学校的详细信息。

现在，实现细节（以前的访问是基于ID的）可以从其余代码中隐藏。
```
if user.IsOldSchool() { // allow access to the old school version of the game}// elsewhereif user.IsNotOldSchool() { return httperrors.Unauthorized(“Please join us playing the new version at game.com/v2.”)}
```

同样，在内部，User结构将利用ID上的方法，进一步封装逻辑。

您可以在Go Playground上玩这些示例。
```
(本文翻译自Justin Fuller的文章《Go Things I Love: Methods On Any Type》，参考：https://medium.com/swlh/go-things-i-love-methods-on-any-type-8aee0c3bc03d)
```
