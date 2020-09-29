# 突击

## java

### java是值传递还是引用传递？

java中**只有值传递**，只不过传递的内容是对象的引用，更准确的说，是共享对象传递



### java基础类型

字符型：char

布尔类型：boolean

数值类型：byte、short、int、long、float、double

byte：1字节 -128 ~ 127

short：2字节 -2^15 ~ 2^15-1

int：4字节 -2^31 ~ 2^31-1

long: 8字节 -2^63 ~ 2^63-1

整型类型，每种类型都有一定的表示范围，若数据超过其范围，则会导致溢出。



#### 自动拆装箱

自动装箱是通过包装类的`valueOf()`方法来实现的，自动拆箱是通过包装类对象的`***Value()`来实现的

自动拆装箱常见场景：

- 将基本数据类型放入集合类——自动装箱
- 包装类型和基本类型的大小比较——自动拆箱
- 包装类型的运算——自动拆箱
- 三目运算符，当第二、三位操作数分别为基本类型和对象时，其中的对象就会进行自动拆箱操作



#### 自动拆装箱带来的问题

- 包装对象的数值比较，不能简单的使用 `==`，虽然 -128 到 127 之间的数字可以，但是这个范围之外还是需要使用 `equals` 比较。

- 前面提到，有些场景会进行自动拆装箱，同时也说过，由于自动拆箱，如果包装类对象为 null ，那么自动拆箱时就有可能抛出 NPE。

- 如果一个 for 循环中有大量拆装箱操作，会浪费很多资源。



#### Integer的缓存机制

Byte、Short、Long固定缓存范围：-128 ~ 127

Character固定缓存范围：0 ~ 127

Integer的缓存范围可通过`-XX:AutoBoxCacheMax=size`修改，或通过`java.lang.Integer.IntegerCache.high`设置最大值



### String







>java工程师成神之路
>https://github.com/hollischuang/toBeTopJavaer
>
>spring面试题
>https://github.com/Snailclimb/JavaGuide/blob/master/docs/system-design/framework/spring/SpringInterviewQuestions.md
>
>kafka面试题
>https://github.com/Snailclimb/JavaGuide/blob/master/docs/system-design/data-communication/kafka-inverview.md
>
>美团面试常见问题
>https://github.com/Snailclimb/JavaGuide/blob/master/docs/essential-content-for-interview/PreparingForInterview/%E7%BE%8E%E5%9B%A2%E9%9D%A2%E8%AF%95%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98%E6%80%BB%E7%BB%93.md





