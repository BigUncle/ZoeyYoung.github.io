Title: [设计模式] 策略模式
Date: 2013-10-15
Tags: 读书,Book
Slug: design-patten-strategy
Author: Zoey Young
Summary: Adapter

STRATEGY(策略) —— 对象行为型模式

### 意图

定义一系列的算法, 把它们一个个封装起来, 且使它们可相互替换. 本模式使得算法可独
立于使用它的客户而变化.

### 别名

政策(Policy)

### 适用性

当存在以下情况时使用Strategy模式

* 许多相关的类仅仅是行为有异. "策略"提供了一种用多个行为中的一个行为来配置一个类的方法.
* 需要使用一个算法的不同变体. 例如, 你可能会定义一些反映不同的空间/时间权衡的
算法. 当这些变体实现为一个算法的类层次时, 可以使用策略模式.
* 算法使用客户不应该知道的数据. 可使用策略模式以避免暴露复杂的、与算法相关的数
据结构.
* 一个类定义了多种行为, 并且这些行为在这个类的操作中以多个条件语句的形式出现. 将相关的条件分支移入它们各自的Strategy类中以代替这些条件语句.

### 结构

![策略模式结构图](/static/images/design-patten-strategy.png)

### 参与者

* Strategy(策略)
    - 定义所有支持的算法的公共接口. Context使用这个接口来调用某ConcreteStrategy定义的算法.【使用组合】
* ConcreteStrategy(具体策略)
    - 以Strategy接口实现某具体算法.
* Context(上下文)
    - 用一个ConcreteStrategy对象来配置.【setStrategy(Strategy concreteStrategy)】
    - 维护一个对Strategy对象的引用.
    - 可定义一个接口来让Strategy访问它的数据.

### 协作

* Strategy和Context相互作用以实现选定的算法. 当算法被调用时, Context可以将该算法所需要的所有数据都传递给该Strategy. 或者, Context可以将自身作为一个参数传递给Strategy操作. 这就让Strategy在需要时可以回调Context.
• Context将它的客户的请求转发给它的Strategy. 客户通常创建并传递一个ConcreteStrategy对象给该Context; 这样, 客户仅与Context交互. 通常有一系列的ConcreteStrategy类可供
客户从中选择.

### 效果

优:

1. 相关算法系列
2. 一个替代继承的方法
3. 消除了一些条件语句
4. 实现的选择

缺:

1. 客户必须了解不同的 Strategy
2. Strategy和Context之间的通信开销
3. 增加了对象的数目【使用Flyweight】

### 实现

1. 定义Strategy和Context接口
2. 将Strategy作为模板参数【C++】
3. 使Strategy对象成为可选的【常见, 在无Strategy时使用默认实现】

### JDK

recognizeable by behavioral methods in an abstract/interface type which invokes a method in an implementation of a different abstract/interface type which has been passed-in as method argument into the strategy implementation

[java.util.Comparator#compare()](http://docs.oracle.com/javase/7/docs/api/java/util/Comparator.html#compare%28T,%20T%29), executed by among others Collections#sort().

[javax.servlet.http.HttpServlet](http://docs.oracle.com/javaee/7/api/javax/servlet/http/HttpServlet.html), the `service()` and all `doXXX()` methods take `HttpServletRequest` and `HttpServletResponse` and the implementor has to process them (and not to get hold of them as instance variables!).

[javax.servlet.Filter#doFilter()](http://docs.oracle.com/javaee/7/api/javax/servlet/Filter.html#doFilter%28javax.servlet.ServletRequest,%20javax.servlet.ServletResponse,%20javax.servlet.FilterChain%29)

[java.io.File#list()](http://docs.oracle.com/javase/7/docs/api/java/io/File.html#list(java.io.FilenameFilter)) FilenameFilter作为Strategy, 其它带FilenameFilter参数的方法也是.

