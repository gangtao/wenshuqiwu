## 为什么样本方差被n-1除
### 解释您的老师没有教过的高中统计资料
## 使用交互式地图和动画可视化伦敦的自行车出行
### 探索Python中的数据可视化工具
## 相关文章

感谢您的阅读。 如果您对数据科学感兴趣，则以下文章可能会有用：
## 使用交互式地图和动画可视化伦敦的自行车出行
### 探索Python中的数据可视化工具
## 为什么样本方差被n-1除
### 解释您的老师没有教过的高中统计资料

最初发布于edenau.github.io。
# 5.虚拟环境-隔离

如果您只记得本文中的一件事，那么应该是使用虚拟环境。
![Photo by Matthew Kwong on Unsplash](0*Uor0K35XCR88rGix)
> Photo by Matthew Kwong on Unsplash


Python应用程序经常使用来自具有复杂依赖关系的各种开发人员的许多不同软件包。 使用特定的库设置开发了不同的应用程序，在该应用程序中，无法使用其他库版本来复制结果。 没有一个可以满足所有应用程序要求的安装。
```
conda create -n venv pip python=3.7  # select python versionsource activate venv...source deactivate
```

因此，为每个应用程序创建单独的独立虚拟环境至关重要，这可以使用pip或conda来完成。
# 4.生成器-内存效率

当我们打算计算大量结果但希望避免同时分配所有结果所需的内存时，将使用生成器。 换句话说，它们会即时生成值，并且不会将先前的值存储在内存中，因此我们只能对其进行一次迭代。

当读取大文件或使用关键字yield生成无限序列时，通常使用它们。 我经常在大多数数据科学项目中发现它很有用。
```python
def gen(n):    # an infinite sequence generator that generates integers >= n
    while True:
        yield n
        n += 1
        
G = gen(3)     # starts at 3
print(next(G)) # 3
print(next(G)) # 4
print(next(G)) # 5
print(next(G)) # 6
```
# 3.压缩和枚举-for循环

Zip函数创建一个迭代器，该迭代器聚合来自多个列表的元素。 它允许在for循环中并行遍历列表并并行排序。 可以使用星号将其解压缩。
```python
numList = [0, 1, 2]
engList = ['zero', 'one', 'two']
espList = ['cero', 'uno', 'dos']
print(list(zip(numList, engList, espList)))
# [(0, 'zero', 'cero'), (1, 'one', 'uno'), (2, 'two', 'dos')]

for num, eng, esp in zip(numList, engList, espList):
    print(f'{num} is {eng} in English and {esp} in Spanish.')
# 0 is zero in English and cero in Spanish.
# 1 is one in English and uno in Spanish.
# 2 is two in English and dos in Spanish.
```
```python
Eng = list(zip(engList, espList, numList))
Eng.sort() # sort by engList
a, b, c = zip(*Eng)

print(a)
print(b)
print(c)
# ('one', 'two', 'zero')
# ('uno', 'dos', 'cero')
# (1, 2, 0)
```
![Photo by Erol Ahmed on Unsplash](0*Lo8gYJqEXB0wswOL)
> Photo by Erol Ahmed on Unsplash


枚举起初可能看起来有些吓人，但在许多情况下变得非常方便。 这是一个自动计数器，通常在for循环中使用，因此不再需要通过counter = 0和counter + = 1在for循环中创建和初始化计数器变量。枚举和zip是两个 构建for循环时最强大的工具。
```python
upperCase = ['A', 'B', 'C', 'D', 'E', 'F']
lowerCase = ['a', 'b', 'c', 'd', 'e', 'f']
for i, (upper, lower) in enumerate(zip(upperCase, lowerCase), 1):
    print(f'{i}: {upper} and {lower}.')
# 1: A and a.
# 2: B and b.
# 3: C and c.
# 4: D and d.
# 5: E and e.
# 6: F and f.
```
# 2.列表操作-循环列表

Python允许负索引，其中aList [-1] == aList [len（aList）-1]。 因此，我们可以通过调用aList [-2]来获得列表中的倒数第二个元素。

我们还可以使用aList [start：end：step]语法对列表进行切片，其中包括开始元素，但没有结束元素。 因此，调用aList [2：5]会得到[2，3，4]。 我们也可以简单地通过调用aList [::-1]来反转列表，我发现这种技术非常优雅。
![Photo by Martin Shreder on Unsplash](0*zP9ed3vNtn75tBd6)
> Photo by Martin Shreder on Unsplash


列表也可以解包为单独的元素，或者使用星号将元素和子列表混合在一起。
```python
a, b, c, d = aList[0:4]
print(f'a = {a}, b = {b}, c = {c}, d = {d}')
# a = 0, b = 1, c = 2, d = 3

a, *b, c, d = aList
print(f'a = {a}, b = {b}, c = {c}, d = {d}')
# a = 0, b = [1, 2, 3, 4, 5, 6, 7], c = 8, d = 9
```
# 1.列表理解-紧凑代码

很多人会把lambda，map和filter称为Python的“技巧”，这是每个初学者都应该学习的。 尽管我认为它们是我们应该意识到的功能，但由于它们缺乏灵活性，因此在大多数情况下它们并不是特别有用。

Lambda是一种将功能组合在一行中以供一次性使用的方法。 如果多次调用函数，则会降低性能。 另一方面，映射将函数应用于列表中的所有元素，而过滤器获取集合中满足用户定义条件的元素子集。
```python
add_func = lambda z: z ** 2
is_odd = lambda z: z%2 == 1
multiply = lambda x,y: x*y

aList = list(range(10))
print(aList)
# [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```
![Photo by Anastase Maragos on Unsplash](0*RfIH7u1HS0u3gWdl)
> Photo by Anastase Maragos on Unsplash


列表理解是一种简洁而灵活的方法，可以从其他具有灵活表达式和条件的列表中创建列表。 它由方括号构造，带有表达式或函数，仅当元素满足特定条件时，该表达式或函数才应用于列表中的每个元素。 它也可以嵌套以处理嵌套列表，并且比使用地图和过滤器灵活得多。
```
# Syntax of list comprehension[ expression(x) for x in aList if optional_condition(x) ]
```
```python
print(list(map(add_func, aList)))
print([x ** 2 for x in aList])
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

print(list(filter(is_odd, aList)))
print([x for x in aList if x%2 == 1])
# [1, 3, 5, 7, 9]
# [1, 3, 5, 7, 9]
```
# 我希望我早先知道的5个Python功能
## Python技巧超越了lambda，map和filter
![Photo by Kirill Sharkovski on Unsplash](0*JkIdrMMRaiMK2PH1)
> Photo by Kirill Sharkovski on Unsplash


Python可以说是十年来新兴的编程语言，并且被证明是一种非常强大的语言。 从交互式地图到区块链，我已经使用Python构建了许多应用程序。 Python有许多功能，对于初学者来说，一开始很难掌握所有功能。

即使您是从其他语言（例如C或MATLAB）切换来的程序员，使用Python进行更高级别抽象的编码绝对是另一种体验。 我希望我早先了解一些Python功能，并重点介绍了五个最重要的功能。
```
(本文翻译自Eden Au的文章《5 Python features I wish I had known earlier》，参考：https://towardsdatascience.com/5-python-features-i-wish-i-had-known-earlier-bc16e4a13bf4)
```
