Java

## 一、反射

> Java反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意方法和属性；这种动态获取信息以及动态调用对象方法的功能称为Java语言的反射机制。



[java基础之一反射](https://blog.csdn.net/qq_36226453/article/details/82790375)



## 二、注解

> 注解是一系列元数据，它提供数据用来解释程序代码，但是注解并非是所解释的代码本身的一部分。注解对于代码的运行效果没有直接影响。
>
> 注解有许多用处，主要如下：
>
> - 提供信息给编译器： 编译器可以利用注解来探测错误和警告信息
> - 编译阶段时的处理： 软件工具可以用来利用注解信息来生成代码、Html文档或者做其它相应处理。
> - 运行时的处理： 某些注解可以在程序运行的时候接受代码的提取
>   值得注意的是，注解不是代码本身的一部分。



[java注解-最通俗易懂的讲解](https://blog.csdn.net/qq1404510094/article/details/80577555)



## 三、枚举

> 枚举实例必须在`enum`关键字声明的类中显式的指定
>
> 除了在枚举类中指定枚举实例，没有任何方式（`new`、`clone`、反射、序列化）可以手动创建枚举实例
>
> 枚举类不可以被继承
>
> 枚举类是线程安全的
>
> 枚举类型是类型安全的
>
> 无法继承其他类（默认继承`Enum`）



[Java枚举（enum）全面解读](https://www.jianshu.com/p/0d69c36a723b)



## 四、IO

> 输入输出都是相对于程序来讲的
>
> Java中将数据的输入输出抽象为流，流是一组有顺序的、单向的、有起点和终点的数据集合
>
> 流的最小数据单元可以为字节或字符



[Java基础之详解Java IO](https://www.cnblogs.com/CQqf/p/10795656.html)

