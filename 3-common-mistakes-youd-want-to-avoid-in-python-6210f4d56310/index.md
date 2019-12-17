# 问题和解决方案：命名文件

切勿使用要使用的库命名python文件。

例如，如果您将文件命名为random.py，则程序将对您要执行的操作感到困惑。
```
import randomprint(random.random())
```

输出：

<module> print（random.random（））中第3行的文件“ C：\ Users \HalilibrahimYıldırım\ Desktop \ medium \ Python \ random.py” TypeError：'module'对象不可调用

检查我的GitHub呼吸并对其进行标记。 您会找到有用的python代码，我会尽可能地对其进行更新。
# 解决方案：复制

当您说b = a时，您基本上说b和a指向同一个对象。 如果两者都指向同一个对象，则对b或a进行某些操作都没关系。 两者都会影响这个{'a'：5，'b'：4，'c'：8}对象。

一个办法：
```
import copya = {'a': 5, 'b': 4, 'c': 8}b = copy.copy(a)del b['a']print(b)print(a)
```

输出：

{'b'：4，'c'：8} {'a'：5，'b'：4，'c'：8}
# 问题：复制

让我们用Python创建一个字典。
```
a = {'a': 5, 'b': 4, 'c': 8}
```

让我们将b设置为a：
```
a = {'a': 5, 'b': 4, 'c': 8}b = a
```

让我们用键a删除第一个元素。
```
del b['a']
```

让我们写a，b看看发生了什么。
```
a = {'a': 5, 'b': 4, 'c': 8}b = adel b['a']print(b)print(a)
```

输出：

{'b'：4，'c'：8} {'b'：4，'c'：8}

这里发生了什么？ 我们只是打算删除b的第一个元素，而不是a…
# 解决方案：默认可变对象

而不是将可变对象作为默认参数传递，而应传递None。 这个例子：
```
def add(x, y=None):    if y is None:        y = list()        y.append(x)    else:        y.append(x)    return yprint(add('halil'))print(add('yıldırım'))
```

输出：

['halil'] ['yıldırım']
# 问题：默认可变对象

嘿，等等-Python中的可变对象是什么？ 可变对象是可以更改的对象。 列表，集合和字典是可变对象的示例。

为了论证，我将定义一个非常简单且无用的函数。
```
def add(x, y=[]):    y.append(x)    return y
```

在此add函数中，我们将y变量默认设置为列表（可变对象）。 让我们使用此功能。
```
def add(x, y=[]):    y.append(x)    return yprint(add('halil'))print(add('yıldırım'))
```

输出为：

['halil'] ['halil'，'yıldırım']

这里发生了什么？ 它会覆盖相同的列表。 当我们第一次调用add（'halil'）时，默认参数变为y = ['halil']并开始覆盖相同的列表。 让我们来看看：
```
def add(x, y=[]):    y.append(x)    return yadd('halil')print(add.__defaults__)add('yıldırım')print(add.__defaults__)
```

输出为：

（['halil']，）（[['halil'，'yıldırım']，）

如您所见，我们正在覆盖默认列表。
# 您想在Python中避免的3个常见错误
## 三个问题及其解决方案
![Photo by NeONBRAND on Unsplash](0*OOwsHdyxZq49PKXF)
> Photo by NeONBRAND on Unsplash


在本文中，我将讨论您不想做的三个常见错误！
```
(本文翻译自Halil Yıldırım的文章《3 Common Mistakes You’d Want to Avoid in Python》，参考：https://medium.com/better-programming/3-common-mistakes-youd-want-to-avoid-in-python-6210f4d56310)
```
