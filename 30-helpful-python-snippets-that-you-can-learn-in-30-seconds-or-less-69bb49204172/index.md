
感谢您抽出宝贵的时间阅读。 请不要忘记给它鼓掌👏（您也可以鼓掌多次），并在below以下进行注释。 我真的很感激。

这是一小段摘要，您可能会发现它们对您的日常工作很有用。 它高度基于此GitHub存储库，您可以在其中找到许多其他有用的Python和其他语言与技术的代码段。
# 您可以在30秒或更短的时间内学习到的30个有用的Python代码段
![Photo by Jantine Doornbos on Unsplash](0*a4SfQa9ogzbuspzy)
> Photo by Jantine Doornbos on Unsplash


Python代表了许多人在数据科学和机器学习，Web开发，脚本，自动化等中使用它的最受欢迎的语言之一。

这种流行的部分原因是它的简单性和易学性。

如果您正在阅读本文，那么很可能您已经在使用Python或至少对它感兴趣。

在本文中，我们将简要介绍30个简短的代码片段，您可以在30秒或更短的时间内理解和学习这些代码片段。
# 1.所有独特

以下方法检查给定列表是否具有重复的元素。 它使用set（）的属性，该属性从列表中删除重复的元素。
```python
def all_unique(lst):
    return len(lst) == len(set(lst))


x = [1,1,2,2,3,2,3,4,5,6]
y = [1,2,3,4,5]
all_unique(x) # False
all_unique(y) # True
```
# 2.字谜

此方法可用于检查两个字符串是否为字谜。 字谜是通过重新排列不同单词或短语的字母而形成的单词或短语，通常只使用所有原始字母一次。
```python
from collections import Counter

def anagram(first, second):
    return Counter(first) == Counter(second)


anagram("abcd3", "3acdb") # True
```
# 3.记忆

该代码段可用于检查对象的内存使用情况。
```python
import sys 

variable = 30 
print(sys.getsizeof(variable)) # 24
```
# 4.字节大小

此方法返回以字节为单位的字符串长度。
```python
def byte_size(string):
    return(len(string.encode('utf-8')))
    
    
byte_size('😀') # 4
byte_size('Hello World') # 11    
```
# 5.打印一个字符串N次

此代码段可用于打印字符串n次，而不必使用循环来完成。
```python
n = 2
s ="Programming"

print(s * n) # ProgrammingProgramming
```
# 6.首字母大写

此代码段仅使用方法title（）将字符串中每个单词的首字母大写。
```python
s = "programming is awesome"

print(s.title()) # Programming Is Awesome
```
# 7.块

此方法将一个列表分块为指定大小的较小列表。
```python
def chunk(list, size):
    return [list[i:i+size] for i in range(0,len(list), size)]
```
# 8.紧凑

此方法通过使用filter（）从列表中删除虚假值（False，None，0和“”）。
```python
def compact(lst):
    return list(filter(None, lst))
  
  
compact([0, 1, False, 2, '', 3, 'a', 's', 34]) # [ 1, 2, 3, 'a', 's', 34 ]
```
# 9.计数

该代码段可用于转置2D数组。
```python
array = [['a', 'b'], ['c', 'd'], ['e', 'f']]
transposed = zip(*array)
print(transposed) # [('a', 'c', 'e'), ('b', 'd', 'f')]
```
# 10.链式比较

您可以在一行中与各种运算符进行多次比较。
```python
a = 3
print( 2 < a < 8) # True
print(1 == a < 2) # False

```
# 11.逗号分隔

该代码段可用于将字符串列表转换为单个字符串，列表中的每个元素均以逗号分隔。
```python
hobbies = ["basketball", "football", "swimming"]

print("My hobbies are:") # My hobbies are:
print(", ".join(hobbies)) # basketball, football, swimming
```
# 12.获取元音

此方法可在字符串中找到元音（“ a”，“ e”，“ i”，“ o”，“ u”）。
```python
def get_vowels(string):
    return [each for each in string if each in 'aeiou'] 


get_vowels('foobar') # ['o', 'o', 'a']
get_vowels('gym') # []
```
# 13.削减资本

此方法可用于将给定字符串的首字母转换为小写。
```python
def decapitalize(str):
    return str[:1].lower() + str[1:]
  
  
decapitalize('FooBar') # 'fooBar'
decapitalize('FooBar') # 'fooBar'
```
# 14.展平

下列方法使用递归展平潜在的深层列表。
```python
def spread(arg):
    ret = []
    for i in arg:
        if isinstance(i, list):
            ret.extend(i)
        else:
            ret.append(i)
    return ret

def deep_flatten(xs):
    flat_list = []
    [flat_list.extend(deep_flatten(x)) for x in xs] if isinstance(xs, list) else flat_list.append(xs)
    return flat_list


deep_flatten([1, [2], [[3], 4], 5]) # [1,2,3,4,5]
```
# 15.差异

此方法通过仅保留第一个变量中的值来找到两个可迭代变量之间的差异。
```python
def difference(a, b):
    set_a = set(a)
    set_b = set(b)
    comparison = set_a.difference(set_b)
    return list(comparison)


difference([1,2,3], [1,2,4]) # [3]
```
# 16.差异

在将给定函数应用于两个列表的每个元素之后，以下方法返回两个列表之间的差。
```python
def difference_by(a, b, fn):
    b = set(map(fn, b))
    return [item for item in a if fn(item) not in b]


from math import floor
difference_by([2.1, 1.2], [2.3, 3.4], floor) # [1.2]
difference_by([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], lambda v : v['x']) # [ { x: 2 } ]
```
# 17.链接函数调用

您可以在一行中调用多个函数。
```python
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

a, b = 4, 5
print((subtract if a > b else add)(a, b)) # 9   
```
# 18.有重复项

以下方法通过使用set（）仅包含唯一元素的事实来检查列表是否具有重复值。
```python
def has_duplicates(lst):
    return len(lst) != len(set(lst))
    
    
x = [1,2,3,4,5,5]
y = [1,2,3,4,5]
has_duplicates(x) # True
has_duplicates(y) # False
```
# 19.合并两个字典

可以使用以下方法合并两个字典。
```python
def merge_two_dicts(a, b):
    c = a.copy()   # make a copy of a 
    c.update(b)    # modify keys and values of a with the ones from b
    return c


a = { 'x': 1, 'y': 2}
b = { 'y': 3, 'z': 4}
print(merge_two_dicts(a, b)) # {'y': 3, 'x': 1, 'z': 4}
```

在Python 3.5及更高版本中，您还可以像下面这样进行操作：
```python
def merge_dictionaries(a, b):
   return {**a, **b}


a = { 'x': 1, 'y': 2}
b = { 'y': 3, 'z': 4}
print(merge_dictionaries(a, b)) # {'y': 3, 'x': 1, 'z': 4}
```
# 20.将两个列表转换成字典

可以使用以下方法将两个列表转换为字典。
```python
def to_dictionary(keys, values):
    return dict(zip(keys, values))
    

keys = ["a", "b", "c"]    
values = [2, 3, 4]
print(to_dictionary(keys, values)) # {'a': 2, 'c': 4, 'b': 3}
```
# 21.使用枚举

此代码段显示您可以使用枚举获取列表的值和索引。
```python
list = ["a", "b", "c", "d"]
for index, element in enumerate(list): 
    print("Value", element, "Index ", index, )
# ('Value', 'a', 'Index ', 0)
# ('Value', 'b', 'Index ', 1)
#('Value', 'c', 'Index ', 2)
# ('Value', 'd', 'Index ', 3)    
```
# 22.花时间

该代码段可用于计算执行特定代码所需的时间。
```python
import time

start_time = time.time()

a = 1
b = 2
c = a + b
print(c) #3

end_time = time.time()
total_time = end_time - start_time
print("Time: ", total_time)

# ('Time: ', 1.1205673217773438e-05)
```
# 23.尝试其他

您可以将else子句作为try / except块的一部分，如果未引发任何异常，则执行该子句。
```python
try:
    2*3
except TypeError:
    print("An exception was raised")
else:
    print("Thank God, no exceptions were raised.")

#Thank God, no exceptions were raised.
```
# 24.最常

此方法返回出现在列表中的最频繁的元素。
```python
def most_frequent(list):
    return max(set(list), key = list.count)
  

numbers = [1,2,1,2,3,2,1,4,2]
most_frequent(numbers)  
```
# 25.回文

此方法检查给定的字符串是否是回文。
```python
def palindrome(a):
    return a == a[::-1]


palindrome('mom') # True
```
# 26.不带if-else的计算器

以下代码片段显示了如何编写简单的计算器而无需使用if-else条件。
```python
import operator
action = {
    "+": operator.add,
    "-": operator.sub,
    "/": operator.truediv,
    "*": operator.mul,
    "**": pow
}
print(action['-'](50, 25)) # 25
```
# 27.随机播放

该代码段可用于随机化列表中元素的顺序。 请注意，随机播放在适当的地方起作用，并返回None。
```python
from random import shuffle

foo = [1, 2, 3, 4]
shuffle(foo) 
print(foo) # [1, 4, 3, 2] , foo = [1, 2, 3, 4]
```
# 28.传播

该方法将列表变平，类似于JavaScript中的[] .concat（…array）。
```python
def spread(arg):
    ret = []
    for i in arg:
        if isinstance(i, list):
            ret.extend(i)
        else:
            ret.append(i)
    return ret


spread([1,2,3,[4,5,6],[7],8,9]) # [1,2,3,4,5,6,7,8,9]
```
# 29.交换价值

交换两个变量而无需使用其他变量的一种非常快捷的方法。
```python
a, b = -1, 14
a, b = b, a

print(a) # 14
print(b) # -1
```
# 30.获取缺少键的默认值

此代码段显示了如何在字典中未包含要查找的键的情况下获取默认值。
```python
d = {'a': 1, 'b': 2}

print(d.get('c', 3)) # 3
```
