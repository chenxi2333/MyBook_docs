# SICP CS61A Lab

## Lab和HW

1. doctest方法

2. Python的for递减循环

3. a//b代表的是整除——自动会舍去余项的除法

4. Python允许同时两个赋值

5. HW2展示了更高级别的抽象，通过函数来实现一种“方法”的抽象。并且使用这种高级抽象去“降维”实现一般的方法。

   1. 抽象的概念投射到现实，就被称为实例。

6. Python中的比较句式和C有所不同

   ```python
   return lambda x,y: (x%y) if (x%y) else True
   ```

   另外逻辑运算也是用的`and `和`or`实现。

7. 一些有关程序调试（Debug）的知识：

   1. Traceback message:如何分析阅读报错文本？
      1. 错误类型、错误位置、报错信息最后一行返回



## Lab2：高级函数实验

1. and 和 or的运算规则：

   1. 在Python中，这个返回的值取决于编译器“看到了哪里”。and会看到第一个错误的值停止，or会看到第一个正确的值停止。返回的也是最后一个看到的值。
   2. 在Python中，组合逻辑运算优先返回数字，not运算返回逻辑解。
   3. 逻辑判断的语句等同于这个语句的返回值True or False。
   4. None是Python中空内容的符号，不是任何值，是”Nothing“。

2. Q2是一些关于lambda的概念性问题

   1. lambda最重要的是“无名”函数。

      1. increment = **lambda** x: x + 1

         这样的写法和一般的有名字函数的写法等效。

   2. ```python
      (lambda:3)()# 返回3，表示了调用一个无参数，返回值为3的无名函数。
      ```

   3. 高级函数的多重调用：洋葱，一层层剥开。higg(g)是给外层的lambda赋值。这种问题其实可以给内层lambda一个”名字“然后再去阅读，就会变成一个很熟悉的问题。

      ```python
      higg = lambda f: lambda x:f(x)
      g = lambda x: x*x
      higg(g)(2)
      ```

   4. 没有返回值的函数返回None。（好像是一句废话？）

3. Q3~6都是一些在函数中定义函数的例子，以及应用。

   1. 区分函数的调用和函数的使用，后者直接写函数名字，返回出来的是函数的内尺地址。
   2. Q5需要从一个数素数的函数中抽象并构建出一个“方法”——数出满足condtion函数的所有数。很有意思。
   3. Q6主要内容是学一下如何去画高级抽象的框图。

4. Q7~8是一些常规编程练习题
   1. Q8需要构建一个3重的嵌套函数，这种高级的抽象比较难去思考，比较好用的方法就是剥洋葱法，一层层拨开，可以使用框图的方式来表示函数层层嵌套的问题（Q6）。



## Project1：Hog



## Lab3：Review

1. 优秀的程序设计有时候能够”合并逻辑“，使得程序更加简洁。
2. 程序一开始都是不知道怎么写，可以快速写一个”大概“的想法出来，然后就可以快速调试和迭代，到达最后想要的效果，排除所有的测试中的错误。
3. 这道自我组合的题目太妙了——自我的”递归”本质上可以看作是自己和自己的一种组合。这个复杂问题如果拆成两个函数的话反而意外的变简单了？
   1. 如果不使用composer的话也有办法。这种方法不需要在每一个循环内定义新的函数。
4. 抽象就是搭积木。这个实验大概就是熟悉最为基础的积木拼接方法。
   1. 顺带一提，不得不说，程序阅读的多了一点之后，感觉很多定势的的地方就变得非常熟悉了（有点像是数独熟练了之后去解简单数独的感觉？）
5. Q6问题的lmbda方法差不多就是高级抽象的集大成的题目了。不禁让人思考到底是怎么想到这么去解的。
   1. 绘制程序框图或许能够一定程度上解决这个问题。
6. 绘图题目其实还是听复杂的……最复杂的大概就是这个题目的变量名起的巨奇怪。
   1. Environment Diagrams：就是考虑程序运行时候帧栈中的情况。
   2. 具体可以参考Dis2。

