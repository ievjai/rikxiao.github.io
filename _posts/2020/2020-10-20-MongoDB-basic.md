---
layout: post
title: "MongoDB 入门学习"
subtitle: '从入门到放弃'
author: "叉叉敌"
header-style: text
tags:
  - 数据库
  - MongoDB
---

>MongoDB 是一个基于`分布式文件存储`的数据库。由 C++ 语言编写。旨在为 WEB 应用提供可扩展的高性能数据存储解决方案。
MongoDB 是一个介于关系数据库和非关系数据库之间的产品，是非关系数据库当中功能最丰富，最像`关系数据库`的。

![dHnpnj](https://gitee.com/chasays/mdPic/raw/master/uPic/dHnpnj.png)

## 分布式计算的优点


- 可靠性（容错） ：

分布式计算系统中的一个重要的优点是可靠性。一台服务器的系统崩溃并不影响到其余的服务器。

- 可扩展性：

在分布式计算系统可以根据需要增加更多的机器。

- 资源共享：

共享数据是必不可少的应用，如银行，预订系统。

- 灵活性：

由于该系统是非常灵活的，它很容易安装，实施和调试新的服务。

- 更快的速度：

分布式计算系统可以有多台计算机的计算能力，使得它比其他系统有更快的处理速度。

- 开放系统：

由于它是开放的系统，本地或者远程都可以访问到该服务。

- 更高的性能：

相较于集中式计算机网络集群可以提供更高的性能（及更好的性价比）

## 分布式计算的缺点
- 故障排除：

故障排除和诊断问题。

- 软件：

更少的软件支持是分布式计算系统的主要缺点。

- 网络：

网络基础设施的问题，包括：传输问题，高负载，信息丢失等。

- 安全性：

开放系统的特性让分布式计算系统存在着数据的安全性和共享的风险等问题


## 安装

```sh
brew tap mongodb/brew
# 安装完了执行即可看到版本， 如果没有，添加到环境变量里面即可
(base) ➜   mongo --version
MongoDB shell version v4.0.9
git version: fc525e2d9b0e4bceff5c2201457e564362909765
allocator: system
modules: none
build environment:
    distarch: x86_64
    target_arch: x86_64

```

主要还有一些配置文件
- 配置文件 (/usr/local/etc/mongod.conf)

- 日志目录路径 (/usr/local/var/log/mongodb)

- 数据目录路径 (/usr/local/var/mongodb) 数据库文件都存在这里

安装好了，还要在后台启动该程序
```sh
mongod --dbpath /usr/local/var/mongodb --logpath /usr/local/var/log/mongodb/mongo.log --fork

## 注释
--dbpath 设置数据存放目录
--logpath 设置日志存放目录
--fork 在后台运行

```
![zpctwH](https://gitee.com/chasays/mdPic/raw/master/uPic/zpctwH.png)


## 连接



配置了环境变量，直接输入`mongo`就可以启动了。
![bkwPs0](https://gitee.com/chasays/mdPic/raw/master/uPic/bkwPs0.png)

为了方便记忆，和SQL对于起来看下哪有那些专业名词。
>https://www.runoob.com/mongodb/mongodb-databases-documents-collections.html

SQL术语/概念	|MongoDB术语/概念|	解释/说明
---|----|---
database|	database	|数据库
table	|collection|	数据库表/集合
row	|document	|数据记录行/文档
column	|field	|数据字段/域
index	|index	|索引
table joins|	 	|表连接,MongoDB不支持
primary key	|primary key	|主键,MongoDB自动将_id字段设置为主键



- `show dbs` 就是查看所有的数据列表

![PTb46k](https://gitee.com/chasays/mdPic/raw/master/uPic/PTb46k.png)


- `db`是查看当前的连接数据库， `use`是切换数据库

![SHd08a](https://gitee.com/chasays/mdPic/raw/master/uPic/SHd08a.png)

- `db.xx.insert` 就是插入数据

![oQs4RU](https://gitee.com/chasays/mdPic/raw/master/uPic/oQs4RU.png)

插入数据有常见的几种，数据内容格式为Json格式。
- 一条文档数据

```
db.collection.insertOne({"test":22})
```
![2JEPT1](https://gitee.com/chasays/mdPic/raw/master/uPic/2JEPT1.png)

- 多条数据

```
document = [
  {"test":22}, {"test11":221}
]
db.collection.insertMany(document)
```

![dKSeh6](https://gitee.com/chasays/mdPic/raw/master/uPic/dKSeh6.png)

- 还有放到for循环 然后，直接把数组insert到集合中

```
var lst = []
for (var i =1;i<1000;i++) {
  lst.push({num:i});
}
db.numbers.insert(lst)
```

![MHBWJe](https://gitee.com/chasays/mdPic/raw/master/uPic/MHBWJe.png)


- remove 这个是删除集合， `但是不会真正的释放空间，需要用repairDatabase`， 还有deleteMany 和deleteOne方法

```
db.inventory.deleteMany({})
db.inventory.deleteMany({ status : "A" })

db.repairDatabase()

```

比如刚刚插入的999条记录，就可以删除了

![FxlxPb](https://gitee.com/chasays/mdPic/raw/master/uPic/FxlxPb.png)


- find 查看类似于sql的 select语句。
里面的条件符号和linux下面的类似
```
(>) 大于 - $gt
(<) 小于 - $lt
(>=) 大于等于 - $gte
(<= ) 小于等于 - $lte
```

还有模糊查询

```
db.col.find({title:/叉叉敌/}) #包含
db.col.find({title:/^叉叉敌/}) # 开头
db.col.find({title:/叉叉敌$/}) # 结尾

```


## 进阶
 

 ## Read more
 https://awesomedataengineering.com/

>[github博客](https://chasays.github.io/)
>微信公众号：chasays， 欢迎关注一起吹牛逼，也可以加微信号「xxd_0225」互吹。
