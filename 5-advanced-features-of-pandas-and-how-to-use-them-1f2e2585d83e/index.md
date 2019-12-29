# 结论

所以你有它！ 您的Pandas的5种高级功能以及如何使用它们！

如果您渴望更多，请不用担心！ 还有更多有关熊猫和数据科学的知识。 作为推荐阅读，KDNuggets网站当然是该主题的最佳资源！
# 喜欢学习吗？

在Twitter上关注我，在其中发布有关最新，最出色的AI，技术和科学的所有信息！ 也在LinkedIn上与我联系！
# 5大熊猫的高级功能以及如何使用它们
![](1*DAU1i8-8GsyGqrC-rabuKg.jpeg)

熊猫是万物数据的黄金标准库。 拥有加载，过滤，操作和浏览数据的功能，因此毫无疑问它是数据科学家的最爱。

我们大多数人自然会坚持熊猫的基本知识。 从CSV文件加载数据，过滤几列，然后直接跳入数据可视化。 然而，Pandas实际上具有许多鲜为人知但有用的功能，这些功能可以使处理数据变得更加轻松和整洁。

本教程将指导您完成其中5个更高级的功能-它们的作用和使用方法。 数据带来更多乐趣！
# （1）配置选项和设置

熊猫带有一组用户可配置的选项和设置。 它们可以极大地提高生产力，因为它们使您可以根据自己的喜好定制熊猫环境。

例如，我们可以更改某些Pandas的显示设置，以更改显示的行数和列数以及显示的精度浮点数。
```python
import pandas as pd

display_settings = {
    'max_columns': 10,
    'expand_frame_repr': True,  # Wrap to multiple pages
    'max_rows': 10,
    'precision': 2,
    'show_dimensions': True
}

for op, value in display_settings.items():
    pd.set_option("display.{}".format(op), value)
```

上面的代码确保Pandas始终最多显示10行和10列，浮点值最多显示2个小数位。 这样，当我们尝试打印大的DataFrame时，我们的终端机或Jupyter Notebook不会看起来一团糟！

那只是一个基本的例子。 除了简单的显示设置之外，还有很多其他可以探索的内容。 您可以查看官方文档中的所有选项。
# （2）合并数据框

Pandas DataFrames的一个相对未知的部分是实际上有2种不同的方式来组合它们。 每种方法都会产生不同的结果，因此，根据您要实现的目标选择合适的方法非常重要。 此外，它们包含许多可进一步自定义合并的参数。 让我们检查一下。
## 级联

串联是组合DataFrame的最著名方法，可以直观地认为是“堆栈”。 该堆叠可以水平或垂直进行。

假设您有一个庞大的CSV格式的数据集。 将其拆分为多个文件以便于处理是很有意义的（这是大型数据集的常见做法，称为分片）。

将其加载到熊猫中时，您可以垂直堆叠每个CSV的DataFrame来为所有数据创建一个大的DataFrame。 例如，如果我们有3个分片，每个分片有500万行，那么在垂直堆叠所有分片之后，最终的DataFrame将有1500万行。

下面的代码显示了如何在Pandas中垂直连接DataFrame。
```python
# Vertical concat
pd.concat([october_df, november_df, december_df], axis=0)
```

您可以通过按列而不是行拆分数据集来执行类似的操作-每个CSV文件有几列（包含数据集的所有行）。 就像我们将数据集的功能划分为不同的碎片一样。 然后，您将水平堆叠它们以合并那些列/要素。
```python
# Horizontal concat
pd.concat([features_1to5_df, features_6to10_df, features_11to15_df], axis=1)
```
## 合并中

合并更复杂但功能更强大，以类似于SQL的样式合并Pandas DataFrame。 也就是说，DataFrames将通过一些公共属性加入。

想象一下，您有2个描述YouTube频道的数据框。 其中一个包含用户ID列表以及每个用户在您的频道上总共花费了多少时间。 另一个包含类似的用户ID列表以及每个用户观看过多少个视频。 合并使我们可以通过匹配用户ID，然后将ID，花费的时间和视频计数放在每个用户的一行中，将2个DataFrame组合为一个。

熊猫中的两个数据框的合并是通过合并功能完成的。 您可以在下面的代码中看到有关其工作方式的示例。 左右参数指的是您要合并的2个数据框，而on则指定要用于匹配的列。
```python
pd.merge(left=ids_and_time_df,
         right=ids_and_videos_df,
         on="id")
```

为了进一步模拟SQL联接，how参数可让您选择要执行的SQL样式联接的类型：内部，外部，左侧或右侧。 要了解有关SQL连接的更多信息，请参见W3Schools教程。
# （3）重塑数据帧

有几种方法可以重塑和重组Pandas DataFrame。 这些范围从简单易用到功能强大和复杂。 让我们看看最常见的3种。 对于以下所有示例，我们将使用此超级英雄数据集！
```python
import pandas as pd

players_data = {'Player': ['Superman', 'Batman', 'Thanos', 'Batman', 'Thanos',
   'Superman', 'Batman', 'Thanos', 'Black Widow', 'Batman', 'Thanos', 'Superman'],
   'Year': [2000,2000,2000,2001,2001,2002,2002,2002,2003,2004,2004,2005],
   'Points':[23,43,45,65,76,34,23,78,89,76,92,87]}
   
df = pd.DataFrame(players_data)

print(df)

"""
         Player  Year  Points
0      Superman  2000      23
1        Batman  2000      43
2        Thanos  2000      45
3        Batman  2001      65
4        Thanos  2001      76
5      Superman  2002      34
6        Batman  2002      23
7        Thanos  2002      78
8   Black Widow  2003      89
9        Batman  2004      76
10       Thanos  2004      92
11     Superman  2005      87
"""
```
## 转置

所有这些中最简单的。 转置将DataFrame的行与其列交换。 如果您有5000行和10列，然后转置DataFrame，则最终将得到10行和5000列。
```python
df = df.T

print(df)

"""
              0       1       2       3       4         5       6       7            8       9       10        11
Player  Superman  Batman  Thanos  Batman  Thanos  Superman  Batman  Thanos  Black Widow  Batman  Thanos  Superman
Year        2000    2000    2000    2001    2001      2002    2002    2002         2003    2004    2004      2005
Points        23      43      45      65      76        34      23      78           89      76      92        87

"""
```
## 通过...分组

Groupby的主要用途是根据某些键将DataFrame分为多个部分。 将DataFrame拆分为多个部分后，您可以循环浏览并在每个部分上独立应用一些操作。

例如，我们可以看到在下面的代码中如何创建具有相应年份和积分的玩家数据框。 然后，我们根据播放器进行了分组，将DataFrame分为多个部分。 因此，每个玩家都有自己的群组，显示该玩家每年在活动中获得的积分。
```python
groups_df = df.groupby('Player')

for player, group in groups_df:
   print("----- {} -----".format(player))
   print(group)
   print("")
   
### This prints out the following
"""
----- Batman -----
   Player  Year  Points
1  Batman  2000      43
3  Batman  2001      65
6  Batman  2002      23
9  Batman  2004      76

----- Black Widow -----
        Player  Year  Points
8  Black Widow  2003      89

----- Superman -----
      Player  Year  Points
0   Superman  2000      23
5   Superman  2002      34
11  Superman  2005      87

----- Thanos -----
    Player  Year  Points
2   Thanos  2000      45
4   Thanos  2001      76
7   Thanos  2002      78
10  Thanos  2004      92

"""
```
## 堆码

堆叠将DataFrame转换为具有多级索引，即每行具有多个子部分。 这些子部分是使用DataFrame的列创建的，并将其压缩为多索引。 总体而言，可以将堆栈视为将列压缩为多索引行。

最好通过一个示例来说明，如下所示。
```python
df = df.stack()

print(df)

"""
0   Player       Superman
    Year             2000
    Points             23
1   Player         Batman
    Year             2000
    Points             43
2   Player         Thanos
    Year             2000
    Points             45
3   Player         Batman
    Year             2001
    Points             65
4   Player         Thanos
    Year             2001
    Points             76
5   Player       Superman
    Year             2002
    Points             34
6   Player         Batman
    Year             2002
    Points             23
7   Player         Thanos
    Year             2002
    Points             78
8   Player    Black Widow
    Year             2003
    Points             89
9   Player         Batman
    Year             2004
    Points             76
10  Player         Thanos
    Year             2004
    Points             92
11  Player       Superman
    Year             2005
    Points             87

"""
```
# （4）处理时间数据

Datetime库是Python的主要组成部分。 每当您处理与现实世界中的日期和时间信息相关的任何内容时，它都是您的转库。 幸运的是，Pandas还具有使用Datetime对象的功能。

让我们举例说明。 在下面的代码中，我们首先创建一个包含4列的DataFrame：Day，Month，Year和data，然后按年和月对它进行排序。 如您所见，这非常混乱。 我们只用3列来存储日期，而实际上我们知道日历日期只是1个值。
```python
from itertools import product
import pandas as pd
import numpy as np

col_names = ["Day", "Month", "Year"]

df = pd.DataFrame(list(product([10, 11, 12], [8, 9], [2018, 2019])),
                   columns=col_names)

df['data'] = np.random.randn(len(df))

df = df.sort_values(['Year', 'Month'], ascending=[True, True])

print(df)


"""
    Day  Month  Year      data
0    10      8  2018  1.685356
4    11      8  2018  0.441383
8    12      8  2018  1.276089
2    10      9  2018 -0.260338
6    11      9  2018  0.404769
10   12      9  2018 -0.359598
1    10      8  2019  0.145498
5    11      8  2019 -0.731463
9    12      8  2019 -1.451633
3    10      9  2019 -0.988294
7    11      9  2019 -0.687049
11   12      9  2019 -0.067432
"""
```

我们可以用datetime清理事情。

Pandas方便地附带了一个名为to_datetime（）的函数，该函数可以将多个DataFrame列压缩并将其转换为单个Datetime对象。 采用这种格式后，就可以使用Datetime库的所有灵活性。

要使用to_datetime（）函数，您需要将相关列中的所有“日期”数据传递给它。 那就是“日”，“月”和“年”列。 一旦有了Datetime格式的内容，我们就不再需要其他列，只需删除它们即可。 看看下面的代码，看看它们如何工作！
```python
from itertools import product
import pandas as pd
import numpy as np

col_names = ["Day", "Month", "Year"]

df = pd.DataFrame(list(product([10, 11, 12], [8, 9], [2018, 2019])),
                   columns=col_names)

df['data'] = np.random.randn(len(df))

df = df.sort_values(['Year', 'Month'], ascending=[True, True])

df.insert(loc=0, column="date", value=pd.to_datetime(df[col_names]))
df = df.drop(col_names, axis=1).squeeze()

print(df)

"""
         date      data
0  2018-08-10 -0.328973
4  2018-08-11 -0.670790
8  2018-08-12 -1.360565
2  2018-09-10 -0.401973
6  2018-09-11 -1.238754
10 2018-09-12  0.957695
1  2019-08-10  0.571126
5  2019-08-11 -1.320735
9  2019-08-12  0.196036
3  2019-09-10 -1.717800
7  2019-09-11  0.074606
11 2019-09-12 -0.643198
"""
```
# （5）将项目映射到组

映射是一个巧妙的技巧，有助于组织分类数据。 例如，想象一下，我们有一个巨大的DataFrame，其中包含成千上万的行，其中一列包含我们要分类的项目。 这样做可以大大简化机器学习模型的训练和有效地可视化数据。

请查看下面的代码以获取一个迷你示例，其中有我们要分类的食品列表。
```python
import pandas as pd

foods = pd.Series(["Bread", "Rice", "Steak", "Ham", "Chicken",
                       "Apples", "Potatoes", "Mangoes", "Fish",
                       "Bread", "Rice", "Steak", "Ham", "Chicken",
                       "Apples", "Potatoes", "Mangoes", "Fish",
                       "Apples", "Potatoes", "Mangoes", "Fish",
                       "Apples", "Potatoes", "Mangoes", "Fish",
                       "Bread", "Rice", "Steak", "Ham", "Chicken",
                       "Bread", "Rice", "Steak", "Ham", "Chicken",
                       "Bread", "Rice", "Steak", "Ham", "Chicken",
                       "Apples", "Potatoes", "Mangoes", "Fish",
                       "Apples", "Potatoes", "Mangoes", "Fish",
                       "Apples", "Potatoes", "Mangoes", "Fish",
                       "Bread", "Rice", "Steak", "Ham", "Chicken",
                       "Bread", "Rice", "Steak", "Ham", "Chicken",])

groups_dict = {
    "Protein": ["Steak", "Ham", "Chicken", "Fish"],
    "Carbs": ["Bread", "Rice", "Apples", "Potatoes", "Mangoes"]
}
```

在上面的代码中，我们将列表放入了pandas系列。 我们还创建了一个字典，其中显示了我们想要的映射，将每个食品分类为“蛋白质”或“碳水化合物”。 这是一个玩具的例子，但是如果这个系列是大规模的，比如说长度为1,000,000件，那么遍历它根本是不实际的。

除了基本的for循环，我们还可以使用Pandas内置的.map（）函数编写函数，以优化的方式执行映射。 请查看下面的代码，以查看该功能及其应用方式。
```python
def membership_map(pandas_series, groups_dict):
    groups = {x: k for k, v in groups_dict.items() for x in v}
    mapped_series = pandas_series.map(groups)
    return mapped_series
    
mapped_data = membership_map(foods, groups_dict)
print(list(mapped_data))
```

在函数中，我们首先遍历字典以创建一个新的字典，其中的键代表熊猫系列中每个可能的项目，其值代表新的映射项目“蛋白质”或“碳水化合物”。 然后，我们只需应用Pandas的内置map函数来映射系列中的所有值

查看下面的输出以查看结果！
```
['Carbs', 'Carbs', 'Protein', 'Protein', 'Protein', 'Carbs', 'Carbs', 'Carbs', 'Protein', 'Carbs', 'Carbs', 'Protein', 'Protein', 'Protein', 'Carbs', 'Carbs', 'Carbs', 'Protein', 'Carbs', 'Carbs', 'Carbs', 'Protein', 'Carbs', 'Carbs', 'Carbs', 'Protein', 'Carbs', 'Carbs', 'Protein', 'Protein', 'Protein', 'Carbs', 'Carbs', 'Protein', 'Protein', 'Protein', 'Carbs', 'Carbs', 'Protein', 'Protein', 'Protein', 'Carbs', 'Carbs', 'Carbs', 'Protein', 'Carbs', 'Carbs', 'Carbs', 'Protein', 'Carbs', 'Carbs', 'Carbs', 'Protein', 'Carbs', 'Carbs', 'Protein', 'Protein', 'Protein', 'Carbs', 'Carbs', 'Protein', 'Protein', 'Protein']
```
```
(本文翻译自George Seif的文章《5 Advanced Features of Pandas and How to Use Them》，参考：https://towardsdatascience.com/5-advanced-features-of-pandas-and-how-to-use-them-1f2e2585d83e)
```
