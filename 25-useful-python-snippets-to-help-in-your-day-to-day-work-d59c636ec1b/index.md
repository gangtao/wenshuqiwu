# 参考书目/其他读物

30秒/ 30秒python —精选的有用的Python代码片段集合，您可以在30秒或更短的时间内理解。
# 联络人

如果您想随时了解我的最新文章和项目，请在Medium上关注我。 这些是我的一些联系方式：
+ 个人网站
+ 领英
+ 中档
+ 的GitHub
+ 卡格勒

阅读愉快，学习愉快，编码愉快！
# 结论

在本文中，我介绍了25个简短的Python代码段，可用作您日常工作中的参考。 请继续关注我的下一篇文章“ 25种有用的SQL查询，以帮助您进行日常工作。”
# 代码段

在本文中，我将介绍25个简短的代码段，这些代码段可以帮助您完成日常任务。
## 1.在两个变量之间交换值

在其他语言中，要在两个变量之间交换值而不使用第三个变量，我们必须使用算术运算符或按位XOR。 在Python中，它要简单得多，如下所示。
```
a = 5                               b = 10                                                                a, b = b, a                                                                 print(a) # 10                               print(b) # 5
```
## 2.检查给定数字是否为偶数

如果给定数字为偶数，则以下函数返回True，否则返回False。
```
def is_even(num):  return num % 2 == 0is_even(10) # True
```
## 3.将多行字符串拆分为行列表

以下函数可用于将多行字符串拆分为行列表。
```
def split_lines(s):  return s.split('\n')split_lines('50\n python\n snippets') # ['50', ' python', ' snippets']
```
## 4.查找对象使用的内存

标准库的sys模块提供了getsizeof（）函数。 该函数接受一个对象，调用该对象的sizeof（）方法，然后返回结果，以便使您的对象可检查。
```
import sysprint(sys.getsizeof(5)) # 28print(sys.getsizeof("Python")) # 55
```
## 5.反转字符串

Python字符串库不像其他Python容器（如list）那样支持内置的reverse（）。 有许多种反转字符串的方法，最简单的方法是利用切片运算符。
```
language = "python"                                reversed_language = language[::-1]                                                                 print(reversed_language) # nohtyp
```
## 6.打印一个字符串n次

如下所示，不使用循环将字符串打印n次非常容易。
```
def repeat(string, n):  return (string * n)repeat('python', 3) # pythonpythonpython
```
## 7.检查字符串是否是回文

以下函数用于检查字符串是否为回文。
```
def palindrome(string):    return string == string[::-1]palindrome('python') # False
```
## 8.将字符串列表合并为一个字符串

下一个代码段将字符串列表组合为单个字符串。
```
strings = ['50', 'python', 'snippets']print(','.join(strings)) # 50,python,snippets
```
## 9.查找列表的第一个元素

此函数返回传递的列表的第一个元素。
```
def head(list):  return list[0]print(head([1, 2, 3, 4, 5])) # 1
```
## 10.查找两个列表之一中存在的元素

此函数返回两个列表之一中存在的每个元素。
```
def union(a,b):  return list(set(a + b))union([1, 2, 3, 4, 5], [6, 2, 8, 1, 4]) # [1,2,3,4,5,6,8]
```
## 11.查找给定列表中存在的所有唯一元素

此函数返回给定列表中存在的唯一元素。
```
def unique_elements(numbers):  return list(set(numbers))unique_elements([1, 2, 3, 2, 4]) # [1, 2, 3, 4]
```
## 12.查找数字列表的平均值

此函数返回列表中存在的两个或多个数字的平均值。
```
def average(*args):  return sum(args, 0.0) / len(args)average(5, 8, 2) # 5.0
```
## 13.检查列表是否包含所有唯一值

此函数检查列表中的所有元素是否唯一。
```
def unique(list):    if len(list)==len(set(list)):        print("All elements are unique")    else:        print("List has duplicates")unique([1,2,3,4,5]) # All elements are unique
```
## 14.跟踪列表中元素的频率

Python计数器跟踪容器中每个元素的频率。 Counter（）返回一个字典，其中元素作为键，其出现频率作为其值。
```
from collections import Counterlist = [1, 2, 3, 2, 4, 3, 2, 3]count = Counter(list)print(count) # {2: 3, 3: 3, 1: 1, 4: 1}
```
## 15.在列表中查找最频繁的元素

此函数返回出现在列表中的最频繁的元素。
```
def most_frequent(list):    return max(set(list), key = list.count)numbers = [1, 2, 3, 2, 4, 3, 1, 3]most_frequent(numbers) # 3
```
## 16.将角度从度转换为弧度

下一个功能用于将角度从度转换为弧度。
```
import mathdef degrees_to_radians(deg):  return (deg * math.pi) / 180.0degrees_to_radians(90) # 1.5707963267948966
```
## 17.计算执行一段代码所花费的时间

以下代码段用于计算执行一段代码所需的时间。
```
import timestart_time = time.time()a,b = 5,10c = a+bend_time = time.time()time_taken = (end_time- start_time)*(10**6)print("Time taken in micro_seconds:", time_taken) # Time taken in micro_seconds: 39.577484130859375
```
## 18.找到数字列表的gcd

此函数计算数字列表的最大公约数。
```
from functools import reduceimport mathdef gcd(numbers):  return reduce(math.gcd, numbers)gcd([24,108,90]) # 6
```
## 19.查找字符串中的唯一字符

该代码段可用于查找字符串中存在的所有唯一字符。
```
string = "abcbcabdb"   unique = set(string)new_string = ''.join(unique)print(new_string) # abcd
```
## 20.使用lambda函数

Lambda是一个匿名函数，只能保存单个表达式。
```
x = lambda a, b, c : a + b + cprint(x(5, 10, 20)) # 35
```
## 21.使用地图功能

在将给定函数应用于给定iterable的每个项目（列表，元组等）之后，此函数返回结果列表。
```
def multiply(n):     return n * n   list = (1, 2, 3) result = map(multiply, list) print(list(result)) # {1, 4, 9}
```
## 22.使用过滤器功能

此功能借助一个功能来过滤给定的序列，该功能会测试序列中的每个元素是否正确。
```
arr = [1, 2, 3, 4, 5]arr = list(filter(lambda x : x%2 == 0, arr))print (arr) # [2, 4]
```
## 23.使用列表理解

列表理解为我们提供了一种基于可迭代的列表创建的简单方法。 在创建期间，可将iterable中的元素有条件地包含在新列表中，并根据需要进行转换。
```
numbers = [1, 2, 3]squares = [number**2 for number in numbers]print(squares) # [1, 4, 9]
```
## 24.使用切片运算符

切片用于从给定序列中提取元素的连续序列或子序列。 以下函数用于合并两个切片操作的结果。 首先，我们将列表从索引d切到末尾，然后从开始切成索引d。
```
def rotate(arr, d):  return arr[d:] + arr[:d]  if __name__ == '__main__':  arr = [1, 2, 3, 4, 5]  arr = rotate(arr, 2)  print (arr) # [3, 4, 5, 1, 2]
```
## 25.使用链接函数调用

最后的代码段用于从一行开始调用多个函数并评估结果。
```
def add(a, b):    return a + bdef subtract(a, b):       return a - ba, b = 5, 10print((subtract if a > b else add)(a, b)) # 15
```
![Photo by Sean Lim on Unsplash](1*E8dtcW7fEoJc7qw20_rTKg.jpeg)
> Photo by Sean Lim on Unsplash

# 25个有用的Python代码段可帮助您进行日常工作
## Python片段，可以作为您日常工作的参考

Python是一种通用的高级编程语言。 您可以使用Python开发桌面GUI应用程序，网站和Web应用程序，进行数据科学等。此外，Python作为一种高级编程语言，使您可以通过注意通用来专注于应用程序的核心功能。 编程任务。 编程语言的简单语法规则使您更容易保持代码库的可读性和应用程序的可维护性。

与其他编程语言相比，使用Python的优势在于：
+ 与主要平台和操作系统兼容
+ 许多开源框架和工具
+ 可读且可维护的代码
+ 强大的标准库
+ 标准测试驱动的开发
