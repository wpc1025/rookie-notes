# Redis
## 一、简单动态字符串
### 1.1 数据结构
```C
struct sdshdr {
	// 记录buf数组中已使用字节的数量
	// 等于SDS所保存字符串的长度
	int len;
	// 记录buf数组中未使用字节的数量
	int free;
	// 字节数组，用于保存字符串
	char buf[];
}
```
### 1.2 SDS与C字符串的区别
1. 常数复杂度获取字符串长度
2. 杜绝缓冲区溢出
3. 减少修改字符串时带来的内存重分配次数
	- 空间预分配
		- 修改后`len`属性小于1MB，则分配和len属性同样大小的未使用空间
		- 修改后`len`属性大于1MB，则分配1MB的未使用空间
    - 惰性空间释放
4. 二进制安全，SDS可以保存文本或二进制数据，C字符串只能保存文本
5. 兼容部分C字符串函数

## 二、链表
### 2.1 数据结构
#### 2.1.1 链表节点
```C
type struct listNode {
	// 前置节点
	struct listNode *prev;
	// 后置节点
	struct listNode *next;
	// 节点的值
	void *value;
}listNode;
```
#### 2.1.2 链表

```C
typedef struct list{
	// 表头节点
	listNode *head;
	// 表尾节点
	listNode *tail;
	// 链表所包含的节点数量
	unsigned long len;
	// 节点值复制函数
	void *(*dup) (void *ptr);
	// 节点值释放函数
	void (*free) (void *ptr);
	// 节点值对比函数
	int (*match)(void *ptr,void *key);
}list;
```
### 2.2 特性
1. **双端**：链表节点带有prev和next指针，获取某个节点的前置后置节点复杂度都是O(1)
2. **无环**：表头节点的prev和表尾节点的next指针都指向NULL，对链表的访问以NULL为终点
3. **带表头指针和表尾指针**：通过list结构的head指针和tail指针，程序获取链表的表头节点和表尾节点的复杂度为O(1)
4. **带链表长度计数器**：程序使用list结构的len属性来对list持有的链表节点进行计数，程序获取链表中节点数量的复杂度为O(1)
5. **多态**：链表节点使用void*指针来保存节点值，并且可以通过list结构的dup、free、match三个属性为节点值设置类型特定函数，所以链表可以用于保存不同类型的值

## 三、字典

### 3.1 数据结构

#### 3.1.1 哈希表节点
```C
typedef struct dictEntry{
	// 键
	void *key;
	
	// 值
	union{
		void *val;
		uint64_tu64;
		int64_ts64;
	} v;
	
	// 指向下个哈希表节点，形成链表
	struct dictEntry *next;
} dictEntry;
```

#### 3.1.2 哈希表
```C
typedef struct dictht{
	// 哈希表数组
	dictEntry **table;
	
	// 哈希表大小
	unsigned long size;
	
	// 哈希表大小掩码，用于计算索引值
	// 总是等于 size - 1
	unsigned long sizemask;
	
	// 该哈希表已有节点数量
	unsigned long used;
} dictht;
```

#### 3.1.3 字典
```C
typedef struct dict{
	// 类型特定函数
	dictType *type;
	
	// 私有数据
	void *privdata;
	
	// 哈希表
	dictht ht[2];
	
	// rehash索引
	// 当 rehash 不在进行时，值为-1
	int rehashidx;
}
```

### 3.2 hash算法
使用特定类型的`hash函数`对`key`求hash值，然后再用值与`dictht的掩码`做`位与`运算

### 3.3 键冲突
采用`链地址`，将新添加的与已有键值对冲突的放在链表的首部，因为没有指向链表尾部的指针，所以放在首部，时间复杂度为O(1)

### 3.4 哈希表扩展和收缩的时机
1. 扩展
	- 服务器未进行`BGSAVE`或`BGREWRITEAOF`时，负载因子大于等于1
	- 服务器进行`BGSAVE`或`BGREWRITEAOF`时，负载因子大于等于5
2. 收缩
	- 当负载因子小于0.1时，哈希表执行收缩操作

**负载因子公式：**`ht[0].used / ht[0].size`

### 3.5 渐进式rehash
- 避免`rehash`对服务器性能造成影响，服务器分多次、渐进式地将`ht[0]`里面的键值对慢慢地`rehash`到`ht[1]`
- 步骤
	1. 为ht[1]分配空间，让字典同时持有ht[0]和ht[1]两个哈希表
	2. 字典中维护索引计数器rehashindex，将其值设置为0，表示rehash开始
	3. rehash期间，每次对字典进行添加、删除、查找或更新，程序除执行指定操作，还会将ht[0]哈希表中rehashindex索引上的所有键值对rehash到ht[1]
	4. 在某个时间点，ht[0]的所有键值对都会被rehash到ht[1]，这时rehashindex置为-1，表示rehash结束

## 四、 跳跃表

### 4.1 数据结构
#### 4.1.1 跳跃表节点
```C
typedef struct zskiplistNode{
	// 层
	struct zskiplistLevel{
		// 前进指针
		struct zskiplistNode *forward;
		// 跨度
		unsigned int span;
	} level[];
	// 后退指针
	struct zskiplistNode *backward;
	// 分值
	double score;
	// 成员对象
	robj *obj;
}zskiplistNode;
```

#### 4.1.2 跳跃表
```C
typedef struct zskiplist{
	// 表头节点和表尾节点
	struct skiplistNode *header, *tail;
	// 表中节点的数量
	unsigned long length;
	// 表中层数最大的节点的层数
	int level;
}zskiplist;
```
### 4.2 特性
1. 有序数据结构，在每个节点中维持多个指向其他节点的指针，从而达到快速访问节点的目的。支持平均`O(logN)`、最坏`O(N)`复杂度的节点查找。有序集合键的底层实现之一。





