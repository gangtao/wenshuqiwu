## 比较DynamoDB和MongoDB
### MongoDB的查询语言使开发人员能够构建可以查询和分析其数据的应用程序，这些数据可以多种...
## Amazon DynamoDB的好处
### 为了处理IT世界中的数据存储需求，您需要依赖数据库管理系统（DBMS）…
## 什么是PostgreSQL
### 简介：在本教程中，您将学习PostgreSQL及其使PostgreSQL与众不同的功能。
## JAMstack WTF
### 以下技巧将帮助您充分利用堆栈中的最佳内容。 内容交付网络自所有标记和…
# 我的意见

“容器赢得了战斗，但战争将输给了无服务器的人。”

— HackerNoon引用西蒙·沃德利（Simon Wardley）

JAM Stack是当今最酷的技术之一。 它非常快捷，可访问且对SEO友好，而且可以免费在AWS上托管静态文件。

但是，对于那些能够拥有构建步骤并重新编译所有更改的应用程序，JAM Stack是唯一正确的选择。

如果您问我，我会争辩说，即使是非常大的网站也可以通过计划的编译（例如每小时）在JAM Stack上构建。 JAM Stack是rad。

它可能不适用于新闻网站，但是许多动态网站并不需要更新的频率更高，而静态网站当然不需要。
## SQL与NoSQL

如果需要一个编译步骤是项目的重中之重，那么它取决于SQL与NoSQL：PostgreSQL或DynamoDB。

PostgreSQL不必托管在Amazon上，尽管可以托管在Amazon RDS上。 DynamoDB由Amazon开发并且是Amazon专有的。

SQL数据库本质上更强大，但也更复杂。 他们的优势在于业务分析和搜索。

NoSQL数据库更易于设置并且足以用于许多项目。 这就是为什么《卫报》考虑DynamoDB撰写230万篇文章的原因。

最后，他们选择了PostgreSQL，因为DynamoDB在2017年没有提供静态加密，但是如果他们今天考虑从MongoDB迁移，他们可能会做出不同的决定。
# 包起来

JAM Stack（无服务器体系结构）是一个不错的选择，特别是对于大多数静态站点而言，也是一种值得注意的出色技术。

PostgreSQL具有庞大的社区，并以可靠，功能丰富的开源软件包提供了SQL的所有强大功能，并具有出色的性能。

DynamoDB是MongoDB的直接替代品，可为您提供规模，安全性和速度，而无需维护任何基础架构。
## 额外资源
+ 理解JAM Stack的一种好方法是WTF网站是JAMstack吗？：
## JAMstack WTF
### 以下技巧将帮助您充分利用堆栈中的最佳内容。 内容交付网络自所有标记和…
+ PostgreSQL Tutorial网站介绍了什么使“ PostgreSQL在其他数据库管理系统中脱颖而出”：
## 什么是PostgreSQL
### 简介：在本教程中，您将学习PostgreSQL及其使PostgreSQL与众不同的功能。
+ CMARIX TechnoLabs博客介绍了DynamoDB的优点：
## Amazon DynamoDB的好处
### 为了处理IT世界中的数据存储需求，您需要依赖数据库管理系统（DBMS）…
+ 如果您问Mongo的人，MongoDB比DynamoDB更好：
## 比较DynamoDB和MongoDB
### MongoDB的查询语言使开发人员能够构建可以查询和分析其数据的应用程序，这些数据可以多种...
# MongoDB替代方案3：DynamoDB

DynamoDB是Amazon Web Services（AWS）的NoSQL产品。 MongoDB和DynamoDB都使用任意模式存储类似JSON的数据。

DynamoDB最近添加了一个称为“静态加密”的功能，现在它在仍然是NoSQL数据库的同时，与MongoDB相比具有很高的竞争力。

这意味着从MongoDB迁移到DynamoDB确实非常容易。
## DynamoDB的优点

DynamoDB是AWS上的旗舰NoSQL数据库，因此其固有的优势是AWS平台的成本，速度和可靠性。

作为AWS产品，它可以轻松地与AWS Lambda和API Gateway集成。

DynamoDB对于当前使用Mongo的任何人的最大优势是，用户可以直接从MongoDB进行实时迁移到DynamoDB。

最好的部分是没有可管理的基础架构-Amazon负责管理。
## DynamoDB的缺点

如果我认为NoSQL丢失记录的可能性太大，那么DynamoDB对我来说不是一个好选择。

DynamoDB可能会遇到可伸缩性问题，例如与所谓的“热键”相关的问题，这些记录的评估频率要比其他记录高得多。

此外，与MongoDB相比，DynamoDB支持较少复杂的数据类型，并且是AWS专有的产品。
# MongoDB替代方案2：PostgreSQL

提倡使用SQL的人引用了SQL体系结构的持续流行以及对SQL数据库执行操作分析的卓越能力：

传统数据库已发展。 他们可以满足现代应用程序所需的可伸缩性，可靠性和可用性要求，几乎可以处理所有工作负载。

— memSQL博客上的Rick Negrin

换句话说，如果SQL数据库可以扩展，那么它比NoSQL更可取。

PostgreSQL（也称为Postgres）是一种流行的免费SQL数据库，在其网站上称自己为“世界上最先进的开源数据库”。
## PostgreSQL的优点

PostgreSQL是功能强大的软件，已经连续开发了30多年。 很多人使用它，并且它有一个充满活力的社区。

它与平台无关。 对于使用AWS的用户，可以使用Amazon Relational Database Service（RDS）上的Amazon Aurora托管它。

另外，PostgreSQL正在迅速发展。 它的性能优于MySQL，MySQL已经比MongoDB快得多。
## PostgreSQL的缺点

使用SQL本质上增加了任何项目的复杂性。 它是团队每天使用的全新编程语言。

从NoSQL迁移到SQL可能很困难。 从根本上说，它们是一种不同类型的数据库结构。 NoSQL是具有键值对的文档存储，而SQL由表和行组成。

一个选项以及Guardian在其迁移中使用的选项是PostgreSQL中的JSONb列类型。 但是，使用JSON Blob有点像黑客，就像将NoSQL数据库转换为SQL格式一样。
# MongoDB替代方案1：JAM堆栈

JAM Stack是JavaScript，API和预渲染的标记的缩写，它是一种无服务器架构，可以完全避免使用数据库。

只要数据可以移动到用Markdown编写的大量JSON文件中，JAM Stack甚至可以替换文档数据库。

使用JAM Stack时，通常使用Gatsby之类的工具来编译（或构建）整个应用程序。

不幸的是，这意味着任何更改都需要重建站点。

另一方面，如果通过API访问动态内容，则动态内容可以实时更改，例如通过Disqus处理的注释。
## JAM Stack的优势

闪电般快速的内容交付是JAM Stack的最大优势，因为它没有服务器，整个应用程序都在客户端运行。

同时，还具有最大的SEO-因为该应用程序已经过预编译，因此被当作静态页面使用，而不是按需生成。

JAM Stack的另一个优势是最小的托管成本。 例如，静态页面基本上可以免费托管在AWS上。
## JAM Stack的缺点

每个更改都必须重新构建。 这意味着需要重新编译应用程序，然后该更改才能在线上可用。

并且，网站越大，构建时间越长。 每次。

因此，对于需要频繁发布，大量数据或实时编辑数据记录的应用程序，通常认为JAM Stack不适合。
# MongoDB的三种选择

当许多人继续使用Mongo时，软件开发人员和数据库工程师可以使用许多替代方法，例如：
+ JAM Stack：无需网络服务器即可提供快速，安全和动态的网站。
+ PostgreSQL：SQL数据库，以其可靠性，功能和性能而闻名。
+ DynamoDB：Amazon Web Services（AWS）创建的NoSQL数据库

这三个选项是当前MongoDB的最佳替代方案。 我们将在下一节中详细介绍每种选择的利弊。
## 为什么监护人从MongoDB切换到PostgreSQL
### 他们为何转换，如何迁移以及今天为什么不这样做
## 再见Mongo，您好Postgres | 数字博客
### 在《卫报》上，大部分内容（包括文章，实时博客，画廊和视频内容）都是在…制作的。
# 著名的监护人离开了MongoDB

在线出版物和英国报纸《卫报》在其2018年11月关于离开MongoDB的文章中获得了100,000多次意见：
## 再见Mongo，您好Postgres | 数字博客
### 在《卫报》上，大部分内容（包括文章，实时博客，画廊和视频内容）都是在…制作的。

在其中，进行切换的开发人员表明，他们的团队在使用OpsManager（Mongo的数据库管理软件）时遇到了问题，并且在两次停机期间，Mongo的支持代理并没有太大帮助。

我深入探讨了该出版物选择“更好的编程”从MongoDB迁移到PostgreSQL的原因：
## 为什么监护人从MongoDB切换到PostgreSQL
### 他们为何转换，如何迁移以及今天为什么不这样做
# 人们为什么要离开MongoDB

通常，NoSQL与以前的数据库体系结构有显着差异，可能会导致记录丢失和性能下降：

NoSQL放弃了数据库的一些核心功能，这些功能使它们具有高性能且易于使用。

— memSQL博客上的Rick Negrin

作为回应，许多开发人员正在考虑从MongoDB和NoSQL转向其他替代方案，例如JAM Stack，PostgreSQL或DynamoDB。
# 2019年MongoDB的前三名替代品
## JAM Stack，PostgreSQL和Amazon的DynamoDB都是MongoDB的竞争替代品
![Photo by Marlene Prusik on Unsplash](1*LaNSw_oIifj42PjW8KoXLw.png)
> Photo by Marlene Prusik on Unsplash


NoSQL是用于描述任何与SQL关系模型不对应的数据库类型的名称。

NoSQL数据库起源于2009年，当时MySpace等网站规模不断扩大：

之所以出现NoSQL，是因为当时的数据库无法满足所需的规模。

— memSQL博客上的Rick Negrin

MongoDB是最著名的NoSQL数据库。 它经常被JavaScript开发人员使用，特别是那些使用MERN Stack或MEAN Stack（将Mongo与Express，Angular或React和Node结合使用）的开发人员。
