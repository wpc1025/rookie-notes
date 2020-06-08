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

