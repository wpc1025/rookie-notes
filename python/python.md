# Python
## 一、数据类型
### 1.1 整数

### 1.2 浮点数

### 1.3 字符串

### 1.4 布尔值
  - `True`
  - `False`
### 1.5 空值：`None`

### 1.6 list

**特性**
- 有序集合，可随时添加和删除其中的二元素

```Python
# 定义一个数组
classMates = ["wpc", "hfg", "zhh", "zh"]
print(classMates)

# len()函数获取list的长度
print(len(classMates))

# 通过索引获取值
print(classMates[0], classMates[1], classMates[2], classMates[3])

# 负数做索引
print(classMates[-1], classMates[-2], classMates[-3], classMates[-4])

# 追加元素
classMates.append("wy")
print(classMates)

# 将元素插入到指定位置
classMates.insert(1,"brj")
print(classMates)

# 删除末尾元素或指定位置元素
classMates.pop()
print(classMates)
classMates.pop(0)
print(classMates)

# 替换某个索引位置的元素
classMates[0] = "wxx"
print(classMates)

# list嵌套
p = ["java","php",["go","node","vue"]]
print(p)
print(p[2][1])
```
### 1.7 tuple

**特性**
- 有序列表，一旦初始化就无法修改
- 当定义一个`tuple`时，`tuple`的元素就必须要确定下来

```Python
# 定义一个元组
classMates = ("rookie", "hfg", "wpc")

# 打印元素
print(classMates[0], classMates[1], classMates[2])
print(classMates[-1], classMates[-2], classMates[-3])

# tuple定义时，元素就必须要确定下来
t1 = (1, 2)
t2 = ()
t3 = (1,)
print(t1)
print(t2)
print(t3)

# 当tuple中包含一个list时，list的元素是可变的，但并不代表tuple可变
t4 = (1, 2, 3, [4, 5, 6])
print(t4)
t4[3][0] = 9
print(t4)
```
### 1.8 dict

**特性**
- 键值对存储，具有极快的查找速度
- 多次放入同一个`key`，不同的`value`，后面的`value`会把前面的冲掉
- 无序
- `key`必须是不可变对象

```Python
# 定义一个dict
d1 = {"rookie": 100, "hfg": 120, "zhh": 130}

# 打印某一个key的value
print(d1["rookie"])

# 赋值
d1["zh"] = 200
d1["rookie"] = 300
print(d1)

# 若key不存在，会报错
# print(d1["brj"])

# 如何避免key不存在的情况
print("brj" in d1)
print(d1.get("brj"))
print(d1.get("brj", -1))

# 删除一个key
d1.pop("rookie")
print(d1)
```
### 1.9 set

**特性**
- 元素集合，元素不重复
- 要创建一个`set`，需要提供一个`list`作为输入集合
- 无序
- 不可以添加可变对象到`set`中

```Python
# 定义set，需要一个list集合作为输入
# set 无序 不重复
s1 = set([1, 2, 3, 4, 1, 2, 3])
print(s1)

# 添加元素
s1.add(5)
s1.add(1)
s1.add(1)
print(s1)

# 删除元素
s1.remove(1)
s1.remove(2)
print(s1)

# set之间可以做并集和交集
s2 = set([8, 9, 10, 1, 2, 3])
print(s1 & s2)
print(s1 | s2)

```
## 二、控制语句

### 2.1 条件判断

```Python
age = int(input("请输入你的年龄"))
if age >= 100:
    print("你真是一个长寿的人")
elif age >= 80:
    print("扶我起来，我还能行")
else:
    print("年轻人，多奋斗，不要好吃懒做")

```

### 2.2 循环

#### 2.2.1 for ... in
```Python
# for ... in 的用法
l1 = [1, 2, 3, 4, 5, 6, 7, 8, 9]
sum = 0
for x in l1:
    sum += x
print(sum)

# range的用法
sum = 0
for x in list(range(50)):
    sum += x
print(sum)
```

#### 2.2.2 while
```Python
sum = 0
n = 99
while n >0:
    sum += n
    n = n -2
print(sum)
```

- `break`：提前结束循环
- `continue`：跳出当前循环



## 三、函数

```Python
import math


# 函数定义
def my_abs(x):
    # 进行类型检查
    if not isinstance(x, (int, float)):
        raise TypeError('bad operand type')
    if x >= 0:
        return x
    else:
        return -x


# 调用函数
print(my_abs(-10))


# 定义一个空函数
def nop():
    pass


# 函数可以返回多个值，其实只是一个tuple
def move(x, y, step, angle=0):
    nx = x + step * math.cos(angle)
    ny = y - step * math.cos(angle)
    return nx, ny


x, y = move(100, 100, 60, math.pi / 6)
print(x, y)
r = move(100, 100, 60, math.pi / 6)
print(r)
```

### 3.1 位置参数
```Python
def power(x):
    return x * x


print(power(2))


def power(x, n):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s


print(power(2, 4))
```

### 3.2 默认参数

- 必选参数在前，默认参数在后

```Python
# 定义一个默认函数，必选参数在前，默认参数在后
def enroll(name, gender, age=6, city='Beijing'):
    print("name：", name)
    print("gender：", gender)
    print("age：", age)
    print("city：", city)
    print("-------------------------------------")


# 默认参数函数调用时，可不传递默认参数，也可传递部分默认参数
enroll("rookie", "F")
enroll("wy", "M", 10)
enroll("wpc", "F", city="zhengzhou")


# 不能使用 L = [] 作为默认参数，因为L是一个默认参数，定义函数时已经计算出来了，如果后面改变了值，则下次调用时，默认参数的内容也就改变了
def add_end(L=None):
    if L is None:
        L = []
    L.append("END")
    return L


print(add_end())
print(add_end())
```

### 3.3 可变参数

- 可变参数，实际上接收的还是一个`tuple`
- 当调用可变参数函数时，可以传入`list`或`tuple`，只需要前面加一个`*`号即可

```Python
# 定义一个可变参数的函数
def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum


print(calc(1, 2))
print(calc())

l1 = [1, 2, 3]
print(calc(*l1))

s1 = (1, 2, 3)
print(calc(*s1))
```

### 3.4 关键字参数

- 关键字参数允许你传入0个或任意个含参数名的参数，自动组装成一个`dict`

```Python
# 定义一个关键字参数函数
def person(name, age, **kw):
    print("name:", name, "age:", age, "other:", kw)


# 调用关键字参数函数
person("rookie", 10)
person("wpc", 20, city='beijing', company='mrrookie')

# 传入一个dict
d1 = {"city": "beijing", "company": "mrrookie"}
person("hfg", 10, **d1)
```

### 3.5 命名关键字参数
- 如果要限制关键字参数名字，就可以使用命名关键字参数

```Python
# 定义一个命名关键字函数
def person(name, age, *, city, job):
    print(name, age, city, job)


person("Jack", 24, city="BeiJing", job="Engineer")


# 若不传入命名关键字参数会报错
# person("Jack", 24)

# 如果函数定义已经有一个可变参数，则后面跟着的命名关键字参数就不再需要一个特殊分隔符 * 了
def person(name, age, *args, city, job):
    print(name, age, args, city, job)

person("rookie", 10, 1, 2, 3, 4, city="BeiJing", job="engineer")
```

### 3.6 参数组合

- 以上所有类型参数可以组合使用，但参数顺序必须是：必选参数，默认参数，可变参数，命名关键字参数、关键字参数

```Python
def f1(a, b, c=0, *args, **kw):
    print('a =', a, 'b =', b, 'c =', c, 'args =', args, 'kw =', kw)

def f2(a, b, c=0, *, d, **kw):
    print('a =', a, 'b =', b, 'c =', c, 'd =', d, 'kw =', kw)
```

## 四、高级特性

### 4.1 切片
```Python
# 对于list、tuple、字符串都可以使用切片快速获取部分元素
l1 = list(range(10))
print(l1)
print(l1[0:3])
print(l1[:3])
print(l1[-2:-1])
print(l1[-2:])

t1 = tuple(range(10))
print(t1)
print(t1[:3])
print(t1[::2])

s1 = "hello mrrookie"
print(s1)
print(s1[0:3])
```

### 4.2 迭代
```Python
from collections.abc import Iterable

# 只要是可迭代的对象，都可以使用 for ... in 进行迭代，如list、tuple、dict、string等

# 对 dict 进行迭代
d1 = {'a': 1, 'b': 2, 'c': 3}
for key in d1:
    print(key)
for value in d1.values():
    print(value)
for k, v in d1.items():
    print(k, v)

# 对 字符串 进行迭代
for ch in 'ABC':
    print(ch)

# 如何判断一个对象是否是可遍历的
print(isinstance('abc', Iterable))
print(isinstance([1, 2, 3], Iterable))
print(isinstance(123, Iterable))

# 通过索引迭代list
for i, value in enumerate(['A', 'B', 'C']):
    print(i, value)
```

### 4.3 列表生成式

```Python
# 列表生成式，可以快速创建list
print([x * x for x in range(10)])

# 加上 if 判断，进行筛选
print([x * x for x in range(10) if x % 2 == 0])

# 使用两层循环
print([m + n for m in 'ABC' for n in 'XYZ'])

# 使用两个变量生成list
d1 = {'a': 1, 'b': 2, 'c': 3}
print([k + '=' + str(v) for k, v in d1.items()])

# 不能再筛选条件中增加else
# 表达式前用了 if 必须有 else
# print([x for x in range(10) if x % 2 == 0 else x])
print([x if x % 2 == 0 else -x for x in range(10)])
```

### 4.4 生成器
```Python
# 一边循环一边计算的机制，称为生成器：generator
g = (x * x for x in range(10))
print(g)
print(next(g))

# 使用 for ... in 迭代生成器，而不是使用next函数
for x in g:
    print(x)


# 定义 generator 的另一种方式，就是将函数变成生成器
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a + b
        n = n + 1
    return 'done'


for x in fib(6):
    print(x)

# 想要拿到 generator 的 return 返回值，就必须捕获 StopIteration 错误，返回值包含在 StopIteration 的 value 中
g = fib(6)
while True:
    try:
        x = next(g)
        print('g:', x)
    except StopIteration as e:
        print("Generator return value:", e.value)
        break
```

### 4.5 迭代器
- 可作用于`for`循环的数据类型有以下几种：
	- 集合数据类型，如`list`、`tuple`、`dict`、`set`、`str`等
	- `generator`，包括生成器和带`yield`的`generator`
- 凡是可作用与`for`循环的对象都是`Iterable`类型
- 凡是可作用于`next()`函数的对象都是`Iterator`类型，表示一个惰性计算的序列
- 集合数据类型是`Iterable`但不是`Iterator`，但可通过`iter()`函数获得一个`Iterator`对象
- 可使用`isInstance()`判断一个对象是否是`Iterator`或`Iterable`对象

## 五、函数式编程



## 六、面向对象
### 6.1 类的定义与实例创建
```Python
# 类的定义
class Student(object):
    def __init__(self, name, score):
        self.name = name
        self.score = score

    def print_score(self):
        print("%s : %s" % (self.name, self.score))


bart = Student('wpc', 100)
bart.print_score()
```

### 6.2 访问限制
- 属性名前增加`__`即可阻止外部访问

```Python
class Student(object):
    def __init__(self, name, score):
        self.__name = name
        self.__score = score

    def print_score(self):
        print("%s : %s" % (self.__name, self.__score))


bart = Student('wpc', 100)
bart.print_score()
# print(bart.__name)
# print(bart._Student__name)
```

### 6.3 继承和多态
```Python
# 继承与多态

class Animal(object):
    def run(self):
        print("Animal is running...")


class Dog(Animal):
    def run(self):
        print("Dog is running...")

    def eat(self):
        print("Eating meat...")


class Cat(Animal):
    def run(self):
        print("Cat is running...")


dog = Dog()
dog.run()
cat = Cat()
cat.run()

# 一个子类对象既是子类类型，也是父类类型
print(isinstance(cat, Animal))
print(isinstance(cat, Cat))


def run_twice(animal):
    animal.run()
    animal.run()


run_twice(dog)
run_twice(cat)


# 对于Python来说，run_twice 方法不一定需要传入 Animal 类型，只需要保证传入的对象有一个 run() 方法即可
class Timer(object):
    def run(self):
        print("Start...")


run_twice(Timer())
```
### 6.4 获取对象信息
- 获取对象类型，可以使用`type()`或`isinstance()`
```Python
class Animal(object):
    pass


class Dog(Animal):
    pass


# 判断对象类型，可以使用 type 函数
print(type(123))
print(type('str'))
print(type(None))
print(type(abs))
print(type(Animal()))
print(type(123) == type(456))
print(type(123) == int)

# 使用 isinstance
print(isinstance(Dog(), Animal))
print(isinstance(Animal(), (Animal, Dog)))
```
- 获取对象的属性和方法，可以使用`dir()`函数
- 可以通过`hasattr()`、`setattr()`、`getattr()`函数，操作对象的属性和方法
```Python
# 使用 dir 函数，可以获得一个对象的所有属性和方法
print(dir('ABC'))

# len() 函数其实是调用对象的 __len__() 方法
print(len('ABC'))
print('ABC'.__len__())


# 自己的类也可以实现 len() 方法，只需要自己写一个 __len__() 方法
class MyDog(object):
    def __len__(self):
        return 100


print(len(MyDog()))


# 配合 getattr()、setattr()、hasattr()，可以直接操作一个对象的状态
class MyObject(object):
    def __init__(self):
        self.x = 9

    def power(self):
        return self.x * self.x


myObject = MyObject()
print(hasattr(myObject, 'x'))
print(getattr(myObject, 'x'))
print(hasattr(myObject, 'y'))
print(setattr(myObject, 'y', 19))
print(hasattr(myObject, 'y'))
print(getattr(myObject, 'z', 404))
```
### 6.5 实例属性和类属性
- 给实例绑定属性的方法是通过实例变量，或者通过`self`变量
- 直接在`class`中定义属性，这种属性是类属性
```Python
class Student(object):
    name = 'Student'


s = Student()
print(s.name)  # 类属性
print(Student.name)  # 类属性
s.name = 'rookie'  # 实例属性赋值
print(s.name)  # 实例属性
print(Student.name)  # 类属性
del s.name  # 删除实例属性
print(s.name)  # 类属性
```
## 七、面向对象高级编程
### 7.1 __slots__
- `__slots__`变量，限制该`class`实例能添加的属性
- `__slots__`变量，对子类不起作用
```Python
class Student(object):
    __slots__ = ('name', 'age')


class GraduateStudent(Student):
    pass


s = Student()
s.name = 'rookie'
s.age = 10
# s.score = 100 # 会报错
print(s.name, s.age)

g = GraduateStudent()
g.score = 100
print(g.score)
```
### 7.2 @property
- `@property`装饰器负责把一个方法变成属性进行调用
- 还可以定义只读属性，只需要不定义`setter`方法即可
```Python
class Student(object):
    @property
    def birth(self):
        return self._birth

    @birth.setter
    def birth(self, value):
        self._birth = value

    @property
    def age(self):
        return 2020 - self._birth

s = Student()
s.birth = 1993
print(s.age)
```
### 7.3 多重继承



### 7.4 定制类
#### 7.4.1 __str__ 和 __repr__
- `__str__`返回用户看到的字符串
- `__repr__`返回程序开发者看到的字符串
```Python
class Student(object):
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return 'Student object (name=%s)' % self.name

    __repr__ = __str__


s = Student('rookie')
print(s)
```
#### 7.4.2 __iter__ 和 __next__
- 如果一个类想被用于`for ... in`循环，类似`list`或`tuple`那样，就必须实现一个`__iter__()`方法，该方法返回一个迭代对象，然后，Python的`for`循环就会不断调用该迭代对象的`__next__()`方法拿到循环的下一个值，直到遇到`StopIteration`错误时退出循环。
```Python
class Fib(object):
    def __init__(self):
        self.a, self.b = 0, 1

    def __iter__(self):
        return self

    def __next__(self):
        self.a, self.b = self.b, self.a + self.b
        if self.a > 1000:
            raise StopIteration()
        return self.a


for n in Fib():
    print(n)
```
#### 7.4.3 __getitem__
- 要表现得像list那样按照下标取出元素以及切片，需要实现`__getitem__()`方法
```Python
class Fib(object):
    def __init__(self):
        self.a, self.b = 0, 1

    def __iter__(self):
        return self

    def __next__(self):
        self.a, self.b = self.b, self.a + self.b
        if self.a > 1000:
            raise StopIteration()
        return self.a

    def __getitem__(self, n):
        if isinstance(n, int):
            for x in range(n):
                self.a, self.b = self.b, self.a + self.b
            return self.a
        if isinstance(n, slice):
            start = n.start
            stop = n.stop
            if start is None:
                start = 0
            self.a, self.b = 1, 1
            L = []
            for x in range(stop):
                if x >= start:
                    L.append(x)
                self.a, self.b = self.b, self.a + self.b
            return L


for n in Fib():
    print(n)

print(Fib()[5])

print(Fib()[0:5])

```
### 7.5 枚举类
```Python
from enum import Enum, unique

Month = Enum('Month', ('Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'))


@unique
class Weekday(Enum):
    Sun = 0
    Mon = 1
    Tue = 2
    Wed = 3
    Thu = 4
    Fri = 5
    Sat = 6


print(Weekday.Mon)
print(Weekday['Tue'])
print(Weekday.Tue.value)
print(Weekday(1))
for name, member in Weekday.__members__.items():
    print(name, '=>', member)
```

### 7.6 TODO使用元类

## 八、错误、调试和测试
### 8.1 错误处理
- 捕获异常的代码示例如下
```Python
try:
	doSomeThing()
except BaseException as e:
	logging.exception(e)
else:
	print('无异常发生')
finally:
	print('无论是否有异常都会执行')
```
- 通过`raise`语句可以抛出一个错误，如`raise ValueError('input error')`

```Python
import logging

try:
    print('try...')
    n = 0
    if n == 0:
        raise ZeroDivisionError()
    r = 10 / 2
    print('result', r)
except ZeroDivisionError as e:
    logging.exception(e)
    print('exception', e)
    raise ValueError('input error...')
else:
    print('no error...')
finally:
    print('finally...')
print('END')
```
## 九、IO编程
### 9.1 文件读写
```Python
# 读取文件
with open('C:\\Users\\rookie\\Desktop\\记录.txt', 'r', encoding='utf-8') as f:
    print(f.read())

# 按行读取文件
with open('C:\\Users\\rookie\\Desktop\\记录.txt', 'r', encoding='utf-8') as f:
    for line in f.readlines():
        print(line.strip('\n'))

# 读取二进制文件
with open('c:\\Users\\rookie\\Pictures\\车机拉取蓝牙钥匙时序图.jpg', 'rb') as f:
    print(f.read())

# 追加模式写文件
with open('C:\\Users\\rookie\\Desktop\\test.txt', 'a', encoding='utf-8') as f:
    f.write('rookie\n')
```
### 9.2 StringIO和BytesIO
