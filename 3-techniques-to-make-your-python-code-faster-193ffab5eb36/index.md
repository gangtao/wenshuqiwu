# 3种使Python代码更快的技术
## 你甚至都不会流汗
![](1*62EZF_HlqzT9-YIRkJXGvg.jpeg)

在这篇文章中，我将分享您在日常脚本编写中可能会使用的3种Python效率技术，以及如何衡量两种解决方案之间的性能提升。 让我们开始吧！
# 我们如何比较两个候选解决方案的性能？

性能可能是指解决方案中的许多不同因素（例如执行时间，CPU使用率，内存使用率等）。 不过，在这篇文章中，我们将专注于执行时间。

新解决方案执行时间的缩短可以像进行除法一样简单地计算出来。 也就是说，我们将旧的（或未优化的）解决方案的执行时间除以新的（或优化的）解决方案：Told / Tnew。 此度量标准通常称为加速。 例如，如果我们将加速因子设为2，则改进后的解决方案所花的时间将是原始解决方案的一半。

为了比较我们函数的性能，我们将创建一个函数，该函数同时接收它们，计算它们的执行时间并计算获得的加速比：
```
import timedef compute_speedup(slow_func, opt_func, func_name, tp=None):  x = range(int(1e5))  if tp: x = list(map(tp, x))  slow_start = time.time()  slow_func(x)  slow_end = time.time()  slow_time = slow_end - slow_start  opt_start = time.time()  opt_func(x)  opt_end = time.time()  opt_time = opt_end - opt_start  speedup = slow_time/opt_time  print('{} speedup: {}'.format(func_name, speedup))
```

为了获得明显的结果，我们将使用相对较大的数组（100.000个元素），并将其作为参数传递给两个函数。 然后，我们将使用时间模块来计算执行时间，并最终实现所获得的加速。

请注意，我们还传递了一个可选参数，该参数允许我们更改列表元素的类型。
# 1.避免使用+运算符连接字符串

您可能会发现一种常见的情况是必须形成一个包含多个子部分的字符串。 Python有一个方便的+运算符，可让我们通过以下方式轻松地连接字符串：
```
def slow_join(x):  s = ''  for n in x:    s += n
```

尽管对我们来说似乎是一种干净的方法，但Python的字符串被创建为不可变的，因此无法进行修改。 这意味着每次我们使用+运算符时，Python实际上都是在两个子字符串的基础上创建一个新字符串并返回新字符串。 考虑到在我们的情况下，此操作将执行100.000次。

这种方法显然是有成本的，并且我们可以使用join（）找到更便宜的解决方案，例如以下示例：
```
def opt_join(x):  s = ''.join(x)
```

此解决方案采用子字符串数组，并将其与空字符串分隔符连接在一起。 让我们检查一下性能提升：
```
compute_speedup(slow_join, opt_join, 'join', tp=str)
```

我得到的加速因子是7,25！ 考虑到实施此技术所需的少量工作，我认为还算不错。
# 2.使用地图功能

当我们需要对列表中的每个元素进行操作时，通常可以通过以下方式进行操作：我们使用列表推导对列表进行迭代并处理当前元素：
```
def slow_map(x):  l = [str(n) for n in x]
```

但是，在许多情况下，您可能更喜欢使用Python的内置映射功能，该功能将相同的操作应用于列表中的每个元素。 最好的是，它可以通过以下简单方式实现：
```
def opt_map(x):  l = map(str, x)  for n in l:    pass
```

现在该检查我们在执行时间方面有多少改进！ 运行我们的compute_speedup函数，如下所示：
```
compute_speedup(slow_map, opt_map, 'map')
```

我的加速比为1.49。 请记住，为了进行公平的比较，我们还必须模拟在地图对象上的遍历。
# 3.避免重新评估功能

每当您发现自己在循环块内的元素上重复使用相同的功能时，例如：
```
y = []for n in x:  y.append(n)  y.append(n**2)  y.append(n**3)
```

…或仅在循环块内一次但在一个较大的列表中使用该函数，例如在以下情况下：
```
def slow_loop(x):  y = []  for n in x:    y.append(n)
```

…您可以利用另一种优化技术。 此方案假定您不能使用map（如果可以，请使用map：加速会高得多）。

如果您以前将其保留为变量并在循环块中重用，则可以节省重新评估函数的成本。 以下代码段显示了此行为：
```
def opt_loop(x):  y = []  append = y.append  for n in x:    append(n)
```

请注意，如果您需要将当前元素追加到其他列表中，则必须为每个列表的append函数创建一个新变量。

让我们使用compute_speedup检查加速：
```
compute_speedup(slow_loop, opt_loop, 'loop')
```

在这种情况下，我获得了2,07的加速！ 同样，我们无需进行任何重大更改即可获得这种改进。
```
(本文翻译自Dhanesh Budhrani的文章《3 techniques to make your Python code faster》，参考：https://towardsdatascience.com/3-techniques-to-make-your-python-code-faster-193ffab5eb36)
```
