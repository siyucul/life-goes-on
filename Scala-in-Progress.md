# WIP: Scala in Progress
终于还是打算给自己最近两个月学习Scala的经历写点总结，好过以前什么记录都不留下的好。过去对Scala有过一些误解和迷思，这里也可以澄清。写啊写啊发现自己变成了一个Java黑。


## 不只是纯粹的函数式编程

Scala自己的设计是同样面向对象也也是函数式的，意味着我们喜欢的封装继承多态可以很轻易在Scala里面实现，而且也可以原生地将函数作为一等公民而且没有副作用。作为Java 8的使用者，我开始并没有觉得Scala的函数式编程有多强大，毕竟Java 8的Stream，Collection还有lambda的使用已经足够覆盖平常函数式编程的需求了。然而Scala为了将函数式编程范式利用到最大程度，极大鼓励使用不可变（immutable）的值，默认的基本数据结构，比如Map之类的，第一次赋值都是不可变的，而Java只有String是这样，若要使用不可变的数据结构必须借助外部的库，比如Guava。

比如说要设计一个简单的Finite State Machine，Scala就会用case class或者case object来定义状态，然后用函数来定义每个状态的转换，以及用不可变的val来定义开始状态和停机状态，类似于写数学证明。Java会用内部可变的object来作为当前的状态，enum class来定义不同的状态，然后用不同的setter来定义每个状态的转换。如果模拟某个输入并且得到最终状态，用Scala来做就可以curry不同的函数然后得到一个确定的最终结果。同样的输入的话，用Java的纯粹的面向对象方法就是操作内部的object来得到一个结果，在多线程的条件下如果有多个writer，这个结果是不确定的。


## Generator

比起Java 8的for loop，Scala的for loop真的是好用太多。首先，Java 8需要借助lombok才能不对变量进行类型声明，Scala连val或者var都不需要放，多少节省了一些时间。更重要的是Scala的for loop是可以filter的，也就是说在Java的for loop内用if判断的语句都可以压缩到Scala里一行的for loop，于是又省了些空间。想想经典的深度搜索数小岛的面试问题，可以用Scala的两行解决遍历邻居的问题。我想面试官肯定觉得写Scala都算作弊吧。

    for (i, j <- getNeighbors; if m[i][j] == 1) dfs(i, j, m)
