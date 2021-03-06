---
layout: post
title: "Python调试神器"
subtitle: '比log和print好用，还省心'
author: "叉叉敌"
header-style: text
tags:
  - python
  - pysnooper
---

今天就来一小点知识。首先是一个python的库，还有一个是自己最近遇到的一件小事。


## Pysnooper

slogan就是 `不要再使用打印机进行调试`。
>https://github.com/cool-RR/PySnooper

- Python 代码不能按预期运行时，`或者想检查程序是否正确运行时`，可以使用带有断点和监视器的成熟的调试器。但是在某些情况下，不能`马上`设置一个。

- 想知道哪些行在运行，`哪些行没有运行`，`以及局部变量的值`是什么。

可以让你做同样的事情，只不过你只需要的函数中添加一个修饰符行，而不是精心设计正确的打印行。将得到函数的实时日志，包括哪些行运行、何时运行以及局部变量何时更改的确切时间。


安装，使用 pip 安装 pysnoop `pip install pysnooper`

----
### 用法

跟踪所有的变量和行数`@pysnooper.snoop()`

```py
import pysnooper

@pysnooper.snoop()
def demo(lst):
    for i in lst:
        print(i+1)
        
demo([1,23,14])
```

![](https://gitee.com/chasays/mdPic/raw/master/uPic/810BBq.png)

还有只用在涉及到的块上`with pysnooper.snoop():`

```py
import pysnooper

def average(number):
    s = 0
    for i in range(1, number + 1):
        s += i
    with pysnooper.snoop():
        avg = s / number
        return avg

print(average(5))
```

![2](https://gitee.com/chasays/mdPic/raw/master/uPic/tKL6FH.png)


还可以和logging一样，重定向到一个文件里面`@pysnooper.snoop('file.log')`

也可以和logging一样设置debug、warn等 `@pysnooper.snoop(prefix='DEBUG ')`

使用 `pysnooper` 进行调试比使用多个 print 语句更容易。它显示了更多的细节，当然，节省了添加 print 语句的时间。但是，`如果正在使用带有断点和监视器的调试器的 IDE，还是使用带有断点和监视器的。`

----
## 思考

前几天去工商局办一点事情，去服务台问了3次，然后取号2次，去了好去办理窗口2次，`最后事情还是没有办好`。

后来在外面吃饭的时间，有人来散发小传单，说我这种情况交`几百块他们可以帮忙搞定`。

当时想的既然来了，就一定要办妥，不能束之高阁。琢磨者既然外面的串串儿都能办好，`我也是普通人，为什么就不能办好喃？`开始打当地工商局的热线，真的是热线，打了很久后，询问后这个事情是可以在网上办理的，`不需要来现场`。

在办事大厅的角落里，找到一台电脑开始在网上捣腾，在网上申请好了，(全国一体化，每个地方都可以用 http://gjzwfw.www.gov.cn/)，最后提示「需要到现场提交资料」。问了服务台和办事窗口都说需要到现场办理。再次电话和当地工商局确认，确实可以网上办理。矛盾点就是现场工作人员说必须要到现场，但是网上提交了，他们窗口就不能现场办理；电话确认又说可以全程网上办理。

无奈之举，焦心重重之下，拨打了市长热线`投诉`了。从此办事效率就高了，对方还主动电话联系你，怎么办理。

![](https://gitee.com/chasays/mdPic/raw/master/uPic/7P3QBj.png)


有很多时候，人需要一点`耐心`，一点`信心`。每个人总会轮到几次不公平的事情，而通常，`安心等待是最好的办法`。在我等待的时候，体会到这个行业服务人员是多么的艰辛，天天都会遇到这么`笨`的客户，但同时也提醒我自己，在这个阶段要改变态度，培养更大的`耐性及自己动手做的能力`。

>[github博客](https://chasays.github.io/)
>微信公众号：chasays， 欢迎关注一起吹牛逼，也可以加微信号「xxd_0225」互吹。
