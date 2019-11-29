# 结论

Typescript为我们提供了一种编写具有编译时类型安全性的JavaScript的方法，同时还支持JavaScript中不支持的枚举，访问说明符之类的构造。

参考：https://basarat.gitbooks.io/typescript/
# 班级

ES6类和打字稿类之间的唯一区别是，打字稿为我们提供了类型安全性和类变量的访问说明符。

访问说明符仅提供编译时安全性，因为编译的JavaScript不支持它们-与类型安全性相同。
```
class Animal {  private readonly name: string;  protected isPet: boolean;    constructor(name: string, isPet: boolean = false) {    this.name = name;    this.isPet = isPet;  }    public isPetAnimal() {    return this.isPet;  }    protected getName() {    return this.name;  }}class Snake extends Animal {  public getName() {    // return a.name; // error since name is private in parent class    return super.getName();  }}const animal = new Animal('tom', true);console.log(animal.isPetAnimal()); // true// animal.getName(); // error since its protectedconst snake = new Snake('kaa');console.log(snake.isPetAnimal()); // falseconsole.log(snake.getName()); // kaa
```
# 命名空间

命名空间可用于功能的逻辑分组，如下所示：
```
namespace Logger {  export function info(message: string) {    console.log(message);  }    export function error(message: string) {    console.error(message);  }}Logger.info('info text');Logger.error('error text');
```

此逻辑分组也可以通过基于文件的模块来实现，建议在命名空间上使用。
# 功能

我们可以定义参数和函数的返回类型，如下所示：
```
interface point {  lat: number,  long: number}function getPoint(lat: number, long: number): point {  return {    lat: lat,    long: long  }}
```

即使我们没有定义函数的返回类型，打字稿也足够聪明，可以自行推断出返回类型。 因此，以下内容也适用：
```
function getPoint(lat: number, long: number) {  return {    lat: lat,    long: long  }}
```

但是始终建议定义返回类型，以避免出现以下错误：
```
function getPoint(lat: number, long: number) {  return {    lat: lat,    lnog: long // no error since we left it to typescript to infer the return type  }}
```
## 可选参数

我们可以将参数定义为可选：
```
function foo(bar: string, baz?: number) {  // baz is optional}foo('str'); // okfoo('str', 1); // ok
```

另外，我们可以为参数设置默认值：
```
function foo(bar: string, baz: number = 1) {  console.log(bar, baz);}foo('str'); // str, 1foo('str', 100); // str, 100
```
## 函数重载

Typescript允许我们声明重载。 这对于文档和安全目的很有用。 但是由于JavaScript不支持函数重载，因此我们必须为所有重载实现单个通用函数。
```
function stringOrNumber(a: string): string;function stringOrNumber(a: number): number;function stringOrNumber(a: any) {  if (typeof a === 'string') {    // typescript knows 'a' is a string in this block    // let b = a * 2; // error        return a;  } else if (typeof a === 'number') {    // typescript knows 'a' is a number in this block    // let b = a.substr('') // error        return a * 2;  }}stringOrNumber('hello'); // hellostringOrNumber(100); // 200stringOrNumber(true); // error
```
## 宣告功能

有两种方法可以在没有实现的情况下声明函数。
```
type longHand = {  (a: number): number}type shortHand = (a: number) => number;
```

如果我们要声明函数重载，则速记和速记声明的唯一区别在于。 例如：
```
type longHand = {  (a: number): number,  (a: string): string,}
```
# 类型注释

所有的变量，函数参数和函数返回类型都是使用typescript中的类型注释定义的，如下所示：
```
const a: number = 124;const b: number = 56;function sum(a: number, b: number): number {  return a + b;}
```
## 原始类型

JavaScript基本类型（例如，数字，字符串，布尔值）都可以用作打字稿中的内置类型。
```
let a: number;a = 5;a = '5'; // errorlet b: string;b = '100';b = 100; // errorlet c: boolean;c = true;c = 'true'; // error
```
## 数组

如果我们想将变量定义为数组，则可以简单地将postfix []与任何有效的类型注释一起使用。 这使我们可以安全地对数组对象进行操作，而不必担心为数组成员分配错误的类型。 如下所示：
```
let numArray: number[] = [ 24, 57, 100 ];numArray[0] = 10; // oknumArray[1] = '10'; // error
```
## 接口/用户定义类型

我们可以借助类型或接口在JavaScript中定义架构复杂对象，如下所示：
```
type point = {  x: number;  y: number;}let a: point = {  x: 1,  y: 1};a.x = 0;a.y = '1'; // errora.z = 2; //errorinterface point2 {  x: number;  y: number;}let b: point2 = {  x: 1,  y: 1};b.x = 0;b.y = '1'; // errorb.z = 2; //error
```

类型和接口都可以用来定义类型。 它们都可以通过类扩展/实现。 界面和类型的详细区别可以在此处阅读。

可选属性

我们可以简单地后缀吗？ 我们知道的变量是可选的，如下所述：
```
type point = {  x: number;  y: number;  z?: number;}let a: point = { x: 1 }; // error missing property 'y'let b: point = { x: 1, y: 1 }; // ok since z is optional
```
## 内联注释

代替为每个对象创建新的类型或接口，我们可以内联定义其结构，如下所示：
```
let student: {  age: number;  name: string,};student = {  age: 15,  name: 'John doe'};function getAge(student: { age: number }) {  return student.age;}console.log(getAge(student)); // 15
```
## 特殊类型
+ 任何→我们可以将变量的类型定义为任何，表示可以为其分配任何内容。 一个人应该避免使用它，因为这违反了定义类型的目的。
+ null和undefined→除非ts编译器选项中的strictNullChecks标志为true，否则我们可以将null / undefined分配给任何其他类型。
+ ：void→当函数没有返回类型时使用。
## 泛型

某些功能/算法不取决于对象的实际类型。 例如，一个函数获取一个项目列表和一个谓词，以根据该谓词返回过滤后的列表。
```
type student = {  name: string,  age: number}const students: student[] = [  {    age: 17,    name: 'John doe'  },  {    age: 15,    name: 'Jane doe'  }];function filter<T>(list: T[], predicate): T[] {  return list.filter(predicate);}console.log(filter(students, (s: student) => s.age > 15));// [ { age: 17, name: 'John doe' } ]
```

这样，我们也可以在返回的列表中获得类型安全性。 实际上，由于JavaScript已经具有用于数组的过滤器功能，因此内部Typescript使用泛型来定义其结构。
## 联合类型

在某些情况下，我们希望变量为多种类型之一，例如字符串或数字。 我们可以像这样简单地定义它：
```
let a: number | string;a = 100; // oka = '100'; // ok
```
## 交叉点类型

在某些情况下，我们希望将两个对象的属性合并到一个新对象中。 交集类型允许我们以类型安全的方式执行此操作，如下所示：
```
function extend<T, U>(a: T, b: U): T & U {  return {    ...a,    ...b  };}const test = extend({ name: 'John' }, { age: 25 });console.log(test);//{ name: 'John', age: 25 }
```
## 元组类型

在JavaScript中，我们通常使用数组作为元组。 我们可以简单地在typescript中将该元组定义为：[typeOfElement1，typeOfElement2]。
```
let a: [string, number];a[0] = '100'; // oka[1] = 100; // oka[1] = '100'; //errora[0] = 100; // error
```
## 枚举

枚举是相关值的集合。 JavaScript不支持将enum作为数据类型。但是typescript支持。
```
enum WeekDay {  monday,  tuesday,  wednesday,  thursday,  friday,  saturday,  sunday}function isWorkingDay(day: WeekDay): boolean {  switch (day) {    case WeekDay.saturday:    case WeekDay.sunday:      return false;    default:      return true;  }}const mon = WeekDay.monday;const sat = WeekDay.saturday;console.log(isWorkingDay(mon)); // trueconsole.log(isWorkingDay(sat)); // falseenum Color {  RED = 'red',  GREEN = 'green',  BLUE = 'blue',}// string enums can be used for comparisonsif (someStringFromDb === Color.GREEN) {}
```
# TypeScript的基础
## 什么是TypeScript，为什么要尝试呢？
![Photo by Arnold Francisca on Unsplash](0*OYrHp_b84xKs_hgW)
> Photo by Arnold Francisca on Unsplash


Typescript是JavaScript的超集，可编译为纯JavaScript。 顾名思义，typescript为我们提供了一种编写类型安全的JavaScript的方法，就像使用其他强类型语言（如C＃或Java）一样。

JavaScript是一种有效的打字稿，其类型是可选的，因此可以轻松地将JavaScript项目迁移到打字稿，并逐步考虑类型安全。

它为我们提供了编译时类型的安全性，并在IDE中提供了更好的IntelliSense。 这可以帮助您及早发现错误并提高生产率。

与无模式对象说再见。 向自我记录的输入和输出对象打个招呼。
