# 模运算符

如果整数除法运算符为我们提供了整体，那么我们还需要一种方法来找到该部分。

模数运算是数学课程中忽略的运算，但在编程和数据科学中可能会非常有用。 使用模数运算符％时，将返回除法的其余部分。
```
x = 10y = 4z = x % yprint(z) # 2
```

如果您在思考使用模数运算符的方式时遇到麻烦，我通常会使用它来检查奇数或偶数整数。
```
x = 11if x % 2:   print("odd number")else:   print("even number")
```

通过从2的除法返回余数，余数将为0（偶数）或1（奇数）。
# 整数除法运算符

您是否曾经需要通过删除其小数位来截断该值？ JavaScript具有Math.floor（）方法进行四舍五入； 但是，这在Python中是不必要的。

Python中的双正斜杠称为整数除法运算符。 本质上，它将左除以右，并且仅保留整数部分。
```
x = 8y = 3z = x // yprint(z) # 2
```
# 求幂运算符

求幂运算符**替代了旧式科学计算器中的传统插入符号^。

与其将变量相乘三次以求多维数据集，也不是使用JavaScript中的Math.pow（）这样的外部库，只需使用双星号将左操作数提高为右方的幂。
```
x = 5x_cubed = x ** 3x_to_the_eighth = x ** 8
```
# Python中较少见的算术运算符
## 超越加，减，乘和除
![Photo by Helloquence on Unsplash](1*5IwI3UFT8BmTwyY9k_vcbg.jpeg)
> Photo by Helloquence on Unsplash


undefined

这是您可能不知道的三个方便的算术（算术）运算符，但它们对您的编程过程有所帮助。
```
(本文翻译自Jonathan Hsu的文章《Lesser-Known Arithmetic Operators in Python》，参考：https://medium.com/better-programming/lesser-known-arithmetic-operators-in-python-a34670087b3a)
```
