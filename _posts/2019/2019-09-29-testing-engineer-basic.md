---
layout: post
title: "从基础开始"
subtitle: '不是科班出身，所有这方面还是要下功夫'
author: "叉叉敌"
header-style: text
tags:
  - 基础
  - 计算机
---

## http和https的区别

- 概念，区别（信息是否加密涉及到安全性，端口）
- 工作原理
![1](https://gitee.com/chasays/mdPic/raw/master/uPic/m310cl.png)

![2](https://gitee.com/chasays/mdPic/raw/master/uPic/mbIsT2.png)

- https的优点和缺点
优点就是安全
缺点就是安全的太复杂了，因此加载时间增加，数据开销大，要收费，不过有免费的有时间限制。

## cookie 和session 的区别
- 前者在本地， 后者在服务器
- cookie不安全，拿到这个可以欺骗服务器。比如说爬虫
- session保存在服务器，占用服务器的性能
- 较为重要的放在session， 不重要的用cookie

## http状态码
- 有1x是消息
- 2是响应正确 200
- 3 是重定向类 如单个页面、表单或者整个 Web 应用被迁移到新的 URL 下的时候，保持（原有）链接可用的技术。HTTP 协议提供了一种特殊形式的响应—— HTTP 重定向（HTTP redirects）来执行此类操作， 其实这种操作对用户来说是基本上没有感知的。
- 4 是错误码 一般是404 403 access denied
- 5 一般是服务器错误码，500， 503
http劫持， https可以避免这个问题，

## OSI七层协议和TCP/IP四层协议
[7层](https://blog.csdn.net/yaopeng_2005/article/details/7064869)
- 应用  http  
- 表示 格式转化和加密数据
- 会话 开始建立链接会话
- 传输 tcp udp（维护会话）
- 网络 ip地址 （这个主要是不同子网间的）
- 数据链路 比如arp （这个是同一个子网间的）
- 物理  就是硬件 （网卡网线等硬件类的）


4层
- 应用层  http
- 传输层 tcp or udp
- IP层 ip （第2层有可能是数据链路层）
- 网络接口 接口1
[OSI七层协议和TCP](https://www.cnblogs.com/aspirant/p/10813139.html)

![7](https://gitee.com/chasays/mdPic/raw/master/uPic/oNMEjl.jpg)

## TCP、IP
为什么不是2次握手

- 为了实现可靠数据传输， TCP 协议的通信双方， 都必须维护一个序列号， 以标识发送出去的数据包中， 哪些是已经被对方收到的。 三次握手的过程即是`通信双方相互告知序列号起始值`， 并`确认对方已经收到了序列号起始值`的必经步骤
- 如果只是两次握手， 至多只有连接发起方的起始序列号能被确认， 另一方选择的序列号则得不到确认

序号（sequence number）、确认号（acknowledgement number）、同步( SYNchronize )

#### 为什么不是4次握手
简单说来是 “先关读，后关写”，一共需要四个阶段。以客户机发起关闭连接为例：
- 1.服务器读通道关闭
- 2.客户机写通道关闭
- 3.客户机读通道关闭
- 4.服务器写通道关闭

关闭行为是在发起方数据发送完毕之后，给对方发出一个`FIN`（finish）数据段。直到接收到对方发送的 `FIN` ，且对方收到了`接收确认ACK`之后，双方的数据通信完全结束，过程中每次接收都需要返回确认数据段ACK。
详细过程：

- 第一阶段 客户机发送完数据之后，向服务器发送一个FIN数据段，序列号为i；

1.服务器收到FIN(i)后，返回确认段ACK，序列号为i+1，`关闭服务器读`通道；

2.客户机收到ACK(i+1)后，`关闭客户机写`通道；

（此时，客户机仍能通过读通道读取服务器的数据，服务器仍能通过写通道写数据）
- 第二阶段 服务器发送完数据之后，向客户机发送一个FIN数据段，序列号为j；

3.客户机收到FIN(j)后，返回确认段ACK，序列号为j+1，`关闭客户机读`通道；

4.服务器收到ACK(j+1)后，`关闭服务器写`通道。

[4次挥手](https://blog.csdn.net/smileiam/article/details/78226816)
第二次握手的时候，还发送了自己的SYN和

![wX3Fwc](https://gitee.com/chasays/mdPic/raw/master/uPic/wX3Fwc.png)

[为什么不是2次握手](https://blog.csdn.net/lengxiao1993/article/details/82771768)





## 冒泡

```python
# bubble
def bubble(list1):
    tmpLen = len(list1)
    for i in range(tmpLen-1):
        for j in range(tmpLen - i):
            if list1[j] < list1[j+1]:
                list1[j], list1[j+1] = list1[j+1], list1[j]
                print(i, j, list1)
    return list1


# 找出字符串中第一个不重复的字符
def findFirstAlpha(s):
    tmps = []
    for i in range(len(s)):
        print(tmps)
        if s[i] not in s[:i]:
            tmps.append(s[i])
        else:
            tmps.remove(s[i])
    ret = tmps[0] if len(tmps) else None
    print(ret)
    return ret
```
![2](https://gitee.com/chasays/mdPic/raw/master/uPic/rDlc82.png)

## python 深拷贝和钱拷贝
```python
# importing copy module 
import copy 
  
# initializing list 1  
li1 = [1, 2, [3,5], 4] 
  
  
# using copy for shallow copy   
li2 = copy.copy(li1)  
  
# using deepcopy for deepcopy   
li3 = copy.deepcopy(li1)  
```
- 都开辟一个新空间
- 对于浅拷贝来说，可变不可变都是引用之前的原始
- 深拷贝来说，只有不可变才是引用之前的。
- 对于赋值来说， 就只是引用，都不开辟空间

![gqj4aD](https://gitee.com/chasays/mdPic/raw/master/uPic/gqj4aD.png)

![ewJkRx](https://gitee.com/chasays/mdPic/raw/master/uPic/ewJkRx.png)


## python 装饰器
```python
import functools
import time

def printRunTime(func):
    @functools.wraps(func)
    def wrapper(*arg, **kw):
        print(time.time())
        func(*arg, **kw)
    return wrapper

@printRunTime
def testDeco(x):
    print(x)
    return x
testDeco(11)

```
staticmethod和classmethod
- 前者是静态，调用的时候需要实例化。
- 后者是类方法， 也不需要实例化，用cls来表示当前类

## python内存管理
- 引用计数， 没有引用就不用了就回收
- 垃圾回收
- [内存池机制](https://nodefe.com/implement-of-pymalloc-from-source/)


主要是为了提高效率， 比如申请小内存后，在运行的时候在用户态和核心态之间转化，影响效率。
`不用的内存，放到内存池`，而不是返回给系统。


- 内核态：cpu可以访问内存的所有数据，包括外围设备，例如硬盘，网卡，cpu也可以将自己从一个程序切换到另一个程序。

- 用户态：只能受限的访问内存，且不允许访问外围设备，占用cpu的能力被剥夺，cpu资源可以被其他程序获取。

最大的区别就是权限不同，在运行在用户态下的程序不能直接访问操作系统内核数据结构和程序。


Python中所有小于512kb的对象都使用pymalloc实现的分配器，而大的对象则使用系统的 malloc。`另外Python对象，如整数，浮点数和List，都有其独立的私有内存池`，对象间不共享他们的内存池。也就是说如果你分配又释放了大量的整数，用于缓存这些整数的内存就不能再分配给浮点数。

## python
- 生成器 yiled
- 迭代器  iter()


__new__:创建对象时调用，会返回当前对象的一个实例

__init__:创建完对象后调用，对当前对象的一些实例初始化，无返回值

调用顺序：先调用__new__生成一个实例再调用__init__方法对实例进行初始化，比如添加属性。



## 浏览器中输入一个URL后，按下回车后发生了什么
URL，统一资源定位符，l简单点就是网址=ip或域名 + 端口号 + 资源位置 + 参数 + 锚点

1．输入一个网址之后，首先浏览器通过查询DNS，查找这个URL的IP地址，（通过层层向上级DNS服务器查找直到找到对应URL的IP地址）

2．得到目标服务器的IP地址及端口号（http 80端口，https 443端口），会调用系统库函数socket，请求一个TCP流套接字。客户端向服务器发送HTTP请求报文

（1）应用层：客户端发送HTTP请求报文。

（2）传输层：（加入源端口、目的端口）建立连接。实际发送数据之前，三次握手客户端和服务器建立起一个TCP连接。

（3）网络层：（加入IP头）路由寻址。

（4）数据链路层：（加入frame头）传输数据。

（5）物理层：物理传输bit。

3．服务器端经过物理层→数据链路层→网络层→传输层→应用层，解析请求报文，发送HTTP响应报文。

4．关闭连接，TCP四次挥手。

5．客户端解析HTTP响应报文，浏览器开始显示HTML

- 网页卡顿原因
>有2个原因，一个是硬件，一个是软件

网速慢、带宽不足、硬件配置低、内存被占满。

JS脚本过大，阻塞了页面的加载。

网页资源过多、接受数据时间长、加载某个资源慢。

DNS解析速度。

- 一般怎么检查
硬件问题：检查网线或者无限网卡有没有插好，有没有连上路由器，就是底层是不是联通状态；

软件问题：查看是否有对应的驱动，服务器好不好，DNS对不对，或者可能是代理没关

- 当网页加载很慢的时候，应如何分析其原因并解决问题？
http请求次数太多

资源过大，资源过多

JS脚本过大

网速慢


## 测试知识
- 白盒 内部逻辑是否ok， 语句，条件，路径、判断，组合 不能验证需求
- 黑盒 按照需求规格说明书使用 等价，边界、因果、场景、错误推测，功能图。 覆盖低
- 单元 
- 性能测试  指标有哪些；  响应时间、单位时间的响应数、CPU利用率、内存、带宽、手机app还有耗电情况 （`不同场景，压力下、网络环境、硬件环境`）
- 压力测试 `并发`、和`保持同时最`大业务量


###  软件生命周期
计划阶段 - 需求分析 - 设计阶段 - 编码 - 测试 - 运行与维护

产品的生命周期
- 开发， 成长，成熟， 衰退


#### 测试生命周期
从测试`项目计划建立`到`BUG提交`的整个测试过程。

包括软件项目`测试计划，测试需求分析，测试用例设计，测试用例执行，BUG提交`五个阶段。 软件测试周期并行与软件生命周期，存在于软件生命周期的各个阶段。
- 测试用例的组成元素
用例编号、用例标题、功能模块名称、前置条件、输入数据、操作步骤、预期结果、优先级、执行结果、编写人、执行人、其他补充、

### 僵尸进程和孤儿进程
[孤儿进程与僵尸进程[总结](https://www.cnblogs.com/anker/p/3271773.html)
孤儿就是， 父进程挂了了。
僵尸就是, 子进程退出了， 父进程不知道，然还保存在系统中

## 高并发


- 响应时间、吞吐量、并发用户数…

- 测试多用户同时访问，访问量的缓慢增加/迅速增加…

- 大量相同类型访问，大量不同类型的访问

- 服务器角度，能够承受多大的压力（？），客户端角度，数据能否成功得到需要的信息，响应时间怎么样

- 实时地根据网络流量和各节点的连接、负载状况以及到用户的距离和响应时间等综合信息

- 一方面保证数据不丢失、一方面保证性能



#### Web和app测试的区别
1.     首先是web和app的区别：web是b/s架构的，基于浏览器；app是c/s架构的，必须要有客户端。Web测试中只要更新了服务器，客户端就会同步更新，保证每个用户用的客户端一样；app就不能保证完全一致，因为app客户端需要用户主动更新，如果app测试中修改了服务器，就意味着客户端用户使用的所有核心版本都要进行回归测试

2.     性能方面：web主要看响应速度；app还看电量、流量、CPU、内存…

3.     兼容方面：web基于浏览器，主要看电脑硬件、电脑系统；app依赖于手机或平板，关注的系统主要是安卓和ios，还要关心分辨率、屏幕尺寸

4. App比web测试多一些专项测试：弱网测试，安装、卸载、更新，界面操作、触摸手势等

## 测试例子
比如微信的搜索功能
- 基础功能   
输入内容，点击搜索是否调到对应页面
空内容点搜索
搜索长度，
不同语言
对应内容的连接和点击后是否正确
返回是否可用
没有结果是否有提示

- 性能测试
响应时间 符合？
弱网是否ok
在压力下，搜索正常？
不同硬件 带宽 内存等，是否正常
- 易用性测试
操作是否简单
有没有搜索建议
搜索结果是否高亮
保存最近记录？


- 兼容性
ios和安卓
不同屏幕分辨率
同步手机语言

- 安全性
有没有数据库sql注入
URL没有加sign标识

- UI
交互设计符合用户审美
图标是否显示
没有错别字

btw， 还有上传文件， 微信扫码点餐， 点赞，发图片，聊天

## 软件开发模型
- 瀑布模型
![fnZ4O1](https://gitee.com/chasays/mdPic/raw/master/uPic/fnZ4O1.png)
- 敏捷模型
![vP3hBV](https://gitee.com/chasays/mdPic/raw/master/uPic/vP3hBV.png)



- V模型：
把测试过程作为在需求分析、系统设计及编码之后的一个阶段，忽视了测试对需求分析，系统设计的验证，需求的满足情况一直到后期的验收测试才被验证。（应该比较多包括系统测试和验收测试）

- W模型：
测试的活动与软件开发同步进行，测试的对象不仅仅是程序，还包括需求和设计。因为在需求阶段测试就已经介入了，后面每一阶段的开发都需要经过测试，能够尽早发现软件的缺陷，降低debug的成本



## 多线程
- 线程与进程的区别


线程和进程
进程是操作系统进行资源分配和调度的最小单位，多个进程之间相互独立，如果一个进程崩溃，不会影响其他进程；

线程是CPU进行分配和调度的最小单位（或者说是进程的最小单位，进程的一部分），一个进程下可以有很多个线程共享该进程的所有资源，如果一个线程崩溃，整个进程就会崩溃。

进程和线程的区别
进程是操作系统进行资源分配和调度的最小单位，每个进程有自己的一部分独立的资源，如果一个进程崩溃，不会影响其他进程；线程是CPU进行分配和调度的最小单位，一个进程下可以有很多个线程共享该进程的所有资源，如果一个线程崩溃，整个进程就会崩溃。

线程一般是共享资源，在创建、或是进行调度的时候开销比进程小很多，通信同步也比较方便

通信方面进程间通讯需要同步或互斥手段的辅助，来保证数据的一致性，线程间可以直接读/写进程数据段（如全局变量）来进行通信。



`线程间通讯和进程间通讯的方法`

线程间：互斥锁、信号量、临界区…

- 互斥量（`全局变量`）：采用互斥对象机制，只有拥有互斥对象的线程才有访问公共资源的权限。因为互斥对象只有一个，所以`可以保证公共资源不会被多个线程同时访问`。

- 信号量：它允许同一时刻多个线程访问同一资源，但是需要控制`同一时刻访问此资源的最大线程数量`。

- 临界区：是一个访问共用资源的程序片段，而这些共用资源又无法同时被多个线程访问的特性。当有线程进入临界区段时，其他线程或是进程必须等待，有一些同步的机制必须在临界区段的进入点与离开点实现，以`确保这些共用资源是被互斥获得使用`。

进程间：共享内存、信号量、管道、消息队列…

共享内存就是映射一段能被其它进程访问的内存，这段共享内存由一个进程创建，但是多个进程可以访问。读写操作时需要用同步互斥的工具，保证在一个进程对这段内存进行访问的时候其他进程不能同时来

信号量是一个计数器，用来控制多个进程对资源的访问，它通常作为一种锁机制。

管道是一种半双工的通信方式，数据只能单项流动，并且只能在具有亲缘关系的进程间流动，进程的亲缘关系通常是父子进程。Pipe（管道），FIFO（有名管道）。调用管道，在内核里开辟一块缓冲区（一个共享文件）来进行进程间通信，有一个读端和一个写端（单向通信）

消息队列是消息的链表，存放在内核中并由消息队列标识符标识。


- 线程状态（5）
创建：new Thread(r)创建，有了相应的内存空间和其他资源，但还未开始执行
就绪：start()方法启动，进入线程队列排队，等待CPU服务
运行：获得处理器资源
阻塞：需要进行耗时的输入输出操作时，要等阻塞清除才能进入队列排队
终止：stop()、destory()或run()结束后，不在具有继续运行的能力

```python
import threading
import time
from queue import Queue
from queue import LifoQueue

lock = threading.Lock()
workQueue = LifoQueue(10)

def print_time(threadName, delay, counter):
    while counter:
        time.sleep(delay)
        print(f'{threadName}, {time.ctime(time.time())}')
        counter -= 1

class TestThread(threading.Thread):
    def __init__(self, threadID, name, q) -> None:
        threading.Thread.__init__(self)
        self.threadID = threadID
        self.name = name
        self.lock = lock
        self.q = q
    def run(self) -> None:
        print(f'starting {self.name}， {id(self.lock)}')
        process_data(self.name, self.q)
        print(f'exiting {self.name}')

def process_data(name, queue):
    lock.acquire()
    if not workQueue.empty():
        data = queue.get()
        print(f'{name}, {data}. {time.time()}')
        lock.release()
    else:
        lock.release()
    time.sleep(1)

if __name__=='__main__': 
    threadNames = ['thread_1', 'thread_2', 'thread_3', 'thread_4', 'thread_5']
    willData = ['_data:'+str(i+1)*4 for i in range(5)]
    # create
    threads = []

    lock.acquire()
    for data in willData:
        workQueue.put(data)
    lock.release()


    for i,v in enumerate(threadNames):
        thread = TestThread(i, v, workQueue)
        thread.start()
        threads.append(thread)
        
    # wait queue is empty
    # while not workQueue.empty():
    #     time.sleep(1)

    for t in threads:
        t.join()
    print("exiting main thread")

```

多进程， 通过使用子进程而非线程有效地绕过了 全局解释器锁。
```python
from multiprocessing import Pool, Process
from os import name
from queue import LifoQueue
import os, time, random

def process_test(name):
    start = time.time()
    print(f'{name}, {os.getpid()}')
    time.sleep(random.random()*3)
    print(f'engding: {time.time()-start} sec')

if __name__=='__main__':
    ## 多进程
    pro = Process(target=process_test, args=('Thread_1',))
    pro.start()
    pro.join()

    ## 大量的子进程
    p = Pool() # default is CPU core number
    for i in range(5):
        p.apply_async(process_test, (f'Process_{i+1}',))
    p.close()
    p.join()
    print('ending')
```

- 线程间通信方式
可以用多multiprocessing来规避GIL这个。
GIL 全局解释锁）能确保一次执行一个线程，线程轮流保存GIL并且在把他传给下一个线程之前执行一些操作，以达到多个进程在CPU上轮流运行，但是这个转换速度很快，让我们觉得他是并行的。
用Queue来实现，这个在multiprocessing和threading里面都有，或者是queue里面的Queue和LifoQueue。一个是FIFO，一个是LIFO
还可以用对应的threading.Lock, acquire和release来实现有序。

- 实现多线程的方式
- 这个需要用代码来实现


## 服务器出问题了，怎么排查
考察的是服务器错误码的分析。
- 500 internal server error就是程序内部错误，一般是出现空指针，或者数组访问越界等
- 501 not implemented这个就是 服务器不支持这个请求
- 502 bad gateway 网关错误，这个就有很多问题了， 有网络问题、请求人太多、带宽太小，服务器交互太大，优化协议
- 503 service unavailable  这个一般是暂时的，比如超载等
- 504 gateway timeout 这个就是比如服务器这个请求需要40s， 但是其他类似nginx的配置是30s超时，这个时候就会提示504

遇到问题怎么去解决
- 查看错误码
- 查看对应的log 或者 带宽和服务器负载问题
- 然后修复对于的问题，然后看看问题时候重现


## 内存溢出和内存泄漏
测试内存可以考虑的2个点，以及原理是什么。
溢出就是超出了， 申请的空间超出了。 空间不足
泄露，就是信息泄露给别人了，就是临时变量没有回收。使用空间过多，导致没有空间可以用。
- 对于android 可以用dumpsys meminfo packagename 来查看对于的views和activity
- 使用第三方工具来分析内存泄漏。比如LeakCanary

>内存溢出：简单地说内存溢出就是指程序运行过程中申请的内存大于系统能够提供的内存，导致无法申请到足够的内存，于是就发生了内存溢出。

内存泄漏：内存泄漏指程序运行过程中分配内存给临时变量，用完之后却没有被GC回收，始终占用着内存，既不能被使用也不能分配给其他程序，于是就发生了内存泄漏。

内存溢出 out of memory，是指程序在申请内存时，没有足够的内存空间供其使用，出现out of memory；

内存泄露 memory leak，是指程序在申请内存后，无法释放已申请的内存空间，一次内存泄露危害可以忽略，但内存泄露堆积后果很严重，无论多少内存，迟早会被占光。

memory leak会最终会导致out of memory！

内存泄露是指无用对象（不再使用的对象）持续占有内存或无用对象的内存得不到及时释放，从而造成的内存空间的浪费称为内存泄露。内存泄露有时不严重且不易察觉，这样开发者就不知道存在内存泄露，但有时也会很严重，会提示你Out of memory。


## linux里source、sh、bash、./有什么区别
考察对Linux的熟悉程度。
这里可以看一下GNU是什么。
source sh bash都是执行文件，后2个是在一个subshell里面执行的， 都不需要被执行文件有执行权限。
./就是需要文件有权限。
- source 不会建立一个subshell， 因此设置后的环境变量就会当前生效。用处就是设置环境变量，或者执行一个文件，里面有一些命令
- sh和bash都是在一个subshell里面执行，这个shell继承了父类的环境变量，但是执行完了后不会待会到父类。不影响父类，可以用于有些脚本的执行等。


## 7升水和11升水怎么倒出2升
以任一一个为参照物， 另一个为获得差值。然后把差值放入到参照物。然后差值继续转。。。

## SQL

sql语句，简单的，显示姓“王”和按年龄倒序输出
```sql
select * from user where firstName='王' order by age desc;

## and
SELECT * FROM Persons WHERE FirstName='Thomas' AND LastName='Carter'

## like 
SELECT * FROM Persons WHERE City LIKE 'N%';

# 顺序很重要
FROM > WHERE > GROUP BY > HAVING > SELECT 的字段 > DISTINCT > ORDER BY > LIMIT;
SELECT DISTINCT player_id, player_name, count(*) as num # 顺序 5
FROM player JOIN team ON player.team_id = team.team_id # 顺序 1
WHERE height > 1.80 # 顺序 2
GROUP BY player.team_id # 顺序 3
HAVING num > 2 # 顺序 4
ORDER BY num DESC # 顺序 6
LIMIT 2 # 顺序 7
```

## user age > 5 10 hubs 逆序

select * from user where age > 5 having sum(hub_number)>10 order by desc;


## 开放性题
为什么投测试
对测试开发的理解
为什么做测试而不是去做开发
如何处理矛盾
职业规划
你认为测试人员需要具备哪些素质
你的优点和缺点


app登录和网页登录的区别

估计美团外卖一天内的全国订单量

淘宝页面价格显示不出来，该怎么测

如果有一部分用户反馈APP的视频加载不出来，你会从哪里方面去定位问题

在一个产品的周期中，你会怎么安排测试工作


### [思维题](https://www.codenong.com/cs107020500/)


## 总结了一些面试过程中遇到的智力题及其解法

>两个水桶，一个水桶可以盛6L水，一个水桶可以盛5L水，盛出来3L水

- 5L水桶盛满，倒入6L空水桶中，6L水桶还余1L空间

- 5L水桶盛满，倒入6L水桶中，5L水桶剩下4L水

- 将6L水桶中的水倒掉，5L水桶中的水倒入6L水桶中，6L水桶还余2L空间

- 5L水桶盛满，2L倒入6L水桶中，则5L水桶剩下3L水

> 2、一个4分钟沙漏，一个7分钟沙漏，计算出9分钟

简单的方法（没有从头计时）：

- 4分钟沙漏和7分钟沙漏同时流，4分钟沙漏流完时，7分钟沙漏还有3分钟，将4分钟的沙漏翻转

- 7分钟沙漏流完时，4分钟沙漏还有1分钟，从此刻开始计时

- 当4分钟沙漏流完时，再次翻转两次4分钟的沙漏，即1+4+4=9分钟

从头计时的方法：

- 4分钟和7分钟的两个沙漏开始同时计时，4分钟后，4分钟的沙漏漏完了，7分钟沙漏还余3分钟

- 把4分钟的沙漏倒过来，继续计时，3分钟后，7分钟的沙漏也漏完了，4分钟沙漏还余1分钟

- 把7分钟的倒过来，当4分钟的沙漏又漏完时，这时正好过去8分钟，七分钟的沙漏这时计时正好过去1分钟

- 然后再次把7分钟的沙漏倒过来，当它漏完之后，刚好9分钟

> 3、八个球，其中有一个是其余球重量的1.5倍，只称两次，如何找出来

- 在这八个球中，随机抽取两组，每组的球的数量是3个，对这两组称重

- 如果天平平衡，则重的球在剩下的两个球中。将剩下的两个球放入天平的两端即可找出重的球

- 如果天平不平衡，在重的那一组的3个球中，再取出两个放到天平两端进行比较

- 如果天平平衡，则重的球是最后剩下的球，否则天平较低那一端的则为重的球

>  4、一圈蚊香烧完要用1个小时,用两圈蚊香识别45分钟

- 同时点燃第一圈的一头和第二圈的两头，第二圈烧完时过去了30分钟

- 立即点燃第一圈的另一头，第一圈烧完时又过去了15分钟，共计45分钟

> 5、10堆苹果，每堆10个，9堆里每个重50g，还有一堆每个重40g，只能称一次，找不一样的那一堆
给每堆苹果编号


- 第一堆里取一个苹果，第二堆里取两个苹果，第三堆里取三个苹果，…，以此类推

- 共取了55个苹果，如果每堆都是50g，应该共2750g

- 称一次，看差的斤数是10的多少倍，就知道是十堆苹果里第几堆斤数不够

> 6、现在有25匹马，赛马场每次只能让5匹马赛跑，没有计时仪器，只能看它们每次的排名顺序,用尽量少的次数选出前3匹

- 25匹马分成A、B、C、D、E五组进行比赛，得出每组第一名A1、B1、C1、D1、E1

- 让A1、B1、C1、D1、E1进行比赛，得出第一名，共比赛了6轮

- 假设名次按照A1、B1、C1、D1、E1这样排，那么第二名在A2，B1中产生，第三名在A2，A3，B1，B2，C1中产生

- 让A2，A3，B1，B2，C1进行比赛，得出第二名和第三名，共需7轮比赛

> 7、有1000瓶水，其中有1瓶水有毒，现有10只小白鼠，中毒反应在第七天显示出来，请问如何在第七天测试出哪一瓶水有毒

利用二进制的思想

- 我们将1000瓶液体编号1-1000，然后将编号转化为10位二进制，如1号就是0000000001

- 将十只小白鼠编号1-10

- 将液体的二进制编号上为1的位数给对应的小白鼠喝，如液体编号为 1111100000，那就是1-5号小白鼠不喝这瓶液体，6-10号小白鼠喝这瓶液体

- 一星期后观察小白鼠的死亡情况，如果1-5号小白鼠死亡，6-10号小白鼠存活，那么有毒的那瓶液体对应的二进制编码为 0000011111

- 将第四步得到的二进制编码转化为十进制，这里是31号，因此我们可以推断出编号为31的液体是被污染的

> 8、有10个石头，你和对手两人轮流拿，每人每次可以拿1-2个，最后一个拿的人算输，有什么必赢的方案
假设自己先拿，从只有1个石头的情况开始考虑：
```python
剩余硬币	（必）输赢	解释
1	输	必须拿走
2	赢	拿一个
3	赢	拿两个
4	输	我无论拿一个还是两个，都剩3个或2个，该对方拿，此时他必赢
5	赢	拿一个
6	赢	拿两个
7	输	我无论拿一个还是两个，都剩6个或5个，该对方拿，此时他必赢
8	赢	拿一个
9	赢	拿两个
10	输	我无论拿一个还是两个，都剩9个或8个，该对方拿，此时他必赢
```
结果：谁先拿，谁必输。所以想必赢，让对手先拿。

规律：硬币的数量，对3求余后余1时 3n+1，则此时谁先取，谁必输。



