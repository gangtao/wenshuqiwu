# 喜欢学习吗？

在Twitter上关注我，在其中发布有关最新，最出色的AI，技术和科学的所有信息！ 也在LinkedIn上与我联系！
# Python类的所有基础知识
## 您需要了解的有关Python类的所有知识！
![](1*ICBT-jxfLVgpCO80d897fw.jpeg)

Python编程语言的核心是一种高级的面向对象的语言。 它的设计专门用于帮助程序员为任何规模的项目编写清晰，逻辑的代码。

Python简单，清晰，易于理解，但功能强大。 这些设计原理真正展现出来的功能是Python类。
# Python类

Python中的几乎所有东西都是对象。 当然，每个对象都具有自己的特征，属性和功能。

我们可以将类视为创建对象的“蓝图”。 具体来说，就是我们自己针对对象定制设计的蓝图。 由于我们是定制它的人，因此我们可以为其提供所需的任何功能，特性和功能！

让我们从一个简单的例子开始。 我们将创建一个具有“ x”属性的类，其中x = 10。 这是我们的班级定义：
```python
class my_class:
  x = 10
```

而已！ 我们创建了第一个Python类my_class，该类具有名为x的属性，其值为10。要实际使用该类，我们可以“调用”函数，然后可以分别访问该类的任何属性。
```python
class my_class:
  x = 10

c_1 = my_class()
print(c_1.x)
```

上面的代码打印出数字10。容易！

我们还可以修改该变量，只需将其分配给新值即可。 让我们使其不等于10，而应使其等于字符串“ Bob”。
```python
class my_class:
  x = 10

c_1 = my_class()
c_1.x = "Bob"
print(c_1.x)
```
# __init __（）函数

所有类都有一个可以随时修改的函数，称为__init __（）。 当从此类创建对象时，总是执行__init __（）函数，该函数可用于初始化某些类变量。 因此，当我们希望Python类始终以某些属性开始时，__init __（）变得非常有用。

让我们以下面的代码为例。
```python
class Person:
  def __init__(self, name, gender):
    self.name = name
    self.gender = gender
    self.country = "USA"

person_1 = Person("Bob", "Male")
person_2 = Person("Kate", "Female")

print(person_1.name)
print(person_1.gender)
print(person_1.country)

print(person_2.name)
print(person_2.gender)
print(person_2.country)
```

在上面的代码中，我们使用名为Bob和Kate的“人员”类创建了2个人。 在这两种情况下，都将执行__init __（），以初始化人员的姓名，性别和所在国家/地区的类变量。

对于名称和性别，我们将自己的变量传递给__init __（）接受的类。 对于“国家/地区”变量，它是在创建对象时也在__init __（）中初始化的。 唯一的区别是，由于它不是__init __（）的函数变量，因此无法从外部进行分配-即所有人将拥有“美国”国家/地区！

该代码的打印输出为：
```
BobMaleUSAKateFemaleUSA
```
# 类功能

就像任何对象一样，Python类可以包含函数！ 这些函数的作用和执行与类之外的完全相同。 唯一真正的区别是类函数能够直接访问类变量，而不必将其作为参数。
```python
class Person:
  def __init__(self, name, gender, age):
    self.name = name
    self.gender = gender
    self.age = age
    
    self.country = "USA"
    
  def print_info(self):
    print("Name: {}".format(self.name))
    print("Gender: {}".format(self.gender))
    print("Age: {}".format(self.age))
    print("Country: {}".format(self.country))
    
  def grow_person(self, years_of_growth):
    self.age = self.age + years_of_growth
    
    
def grow_person(current_age, years_of_growth):
  return current_age + years_of_growth


# Initialise the person
person_1 = Person("Bob", "Male", 30)

# Print all information about Bob by grabbing each variable
print("Name: {}".format(person_1.name))
print("Gender: {}".format(person_1.gender))
print("Age: {}".format(person_1.age))
print("Country: {}".format(person_1.country))

# Print all information about Bob using the class function
person_1.print_info()

# Use the external function
person_1.age = grow_person(person_1.age, years_of_growth=5)

# Use the class function
person_1.grow_person(years_of_growth=5)
```

一流的函数在第9行称为print_info（），它打印有关我们的Person对象的所有可用信息。 请注意，由于我们将类变量与self一起使用，因此我们可以从班级中的任何地方访问Bob的信息！ 由于可以直接获得所有数据，因此在将函数应用于Python对象时非常方便。

另一方面，请注意，我们需要在外部使用Python print（）打印出Bob的信息，需要多少额外的代码。 具有专门针对要在该类中定义的特定类类型而设计的功能的地方，也更加井井有条。

我们编写的第二个函数称为grow_person（），它将用户的年龄增加用户指定的年限。 自然地，将此作为类函数更有意义，因为它主要与我们的Person类有关。 该代码还最终看起来更加易于阅读和清晰！
```
this document is translated from article 《All the basics of Python classes》 written by George Seif, refer to https://levelup.gitconnected.com/all-the-basics-of-python-classes-8b07046d2a52
```
