# Math

## 常量	           描述

math.e		返回欧拉数 (2.7182...)
math.inf	返回正无穷大浮点数
math.nan	返回一个浮点值 NaN (not a number)
math.pi	π 一般指圆周率。 圆周率 PI (3.1415...)
math.tau	数学常数 τ = 6.283185...，精确到可用精度。Tau 是一个圆周常数，等于 2π，圆的周长与半径之比。

## 常用函数              描述

math.ceil(x)		将 x 向上舍入到最接近的整数
math.degrees(x)		将角度 x 从弧度转换为度数。
math.exp(x)			返回 e 的 x 次幂，Ex， 其中 e = 2.718281... 是自然对数的基数。
math.fabs(x)		返回 x 的绝对值。
math.factorial(x)	返回 x 的阶乘。 如果 x 不是整数或为负数时则将引发 ValueError。
math.floor()		将数字向下舍入到最接近的整数
math.fmod(x, y)		返回 x/y 的余数
math.gcd()			返回给定的整数参数的最大公约数。
math.isnan()		判断数字是否为 NaN，如果 x 是 NaN（不是数字），则返回 True ，否则返回 False 。
math.isqrt()		将平方根数向下舍入到最接近的整数
math.pow(x, y)		将返回 x 的 y 次幂。

## 三角函数：

math.sin(x)			返回 x 弧度的正弦值。
math.sinh(x)		返回 x 的双曲正弦值。
math.sqrt(x)		返回 x 的平方根。
math.tan(x)			返回 x 弧度的正切值。
math.acos(x)		返回 x 的反余弦，结果范围在 0 到 pi 之间。
math.asin(x)		返回 x 的反正弦值，结果范围在 -pi/2 到 pi/2 之间。
math.atan(x)		返回 x 的反正切值，结果范围在 -pi/2 到 pi/2 之间。
math.cos()			返回 x 弧度的余弦值。

Collections

2.1 Counter 计数器
Counter是一个dict的子类，用于计数可哈希对象。它是一个集合，元素像字典键(key)一样存储，它们的计数存储为值。计数可以是任何整数值，包括0和负数，Counter类有点像其他语言中的bags或multisets。简单说，就是可以统计计数，来几个例子看看就清楚了，比如

用于计数，看作一个字典dict
可以直接对列表统计每个元素出现的次数

```python
#计算列表中单词的个数
from collections import Counter
a = ["apple", 'banana', 'cat', 'cat', 'cat', 'cat', 'dog']
b = Counter(a)
print("type_b = ",type(b))
print("b = ", b)
```



输出：

```
type_b =  <class 'collections.Counter'>
b =  Counter({'cat': 4, 'apple': 1, 'banana': 1, 'dog': 1})
进程已结束，退出代码 0
```

```
from collections import Counter

字符串计数
print(Counter('gallahad') )

字典计数
print(Counter({'red': 4, 'blue': 2}))  

是个啥玩意计数
print(Counter(cats=4, dogs=8))

print(Counter(['red', 'blue', 'red', 'green', 'blue', 'blue']))
```

输出：

```
Counter({'a': 3, 'l': 2, 'g': 1, 'h': 1, 'd': 1})
Counter({'red': 4, 'blue': 2})
Counter({'dogs': 8, 'cats': 4})
Counter({'blue': 3, 'red': 2, 'green': 1})

进程已结束，退出代码 0
```

- 常用函数：
- **most_common(k)**： 返回一个列表，其中包含n个最常见的元素及出现次数，按常见程度由高到低排序。 如果 n 被省略或为None，most_common() 将返回计数器中的所有元素，计数值相等的元素按首次出现的顺序排序，经常用来计算top词频的词语。
- **elements()**:返回一个迭代器，每个元素重复对应次数； 元素会按首次出现的顺序返回。如果一个元素的计数小于1，elements()将会忽略他
- **clear()**:清空，移除所有的元素，使长度为0
- 数学运算

```
例1：most_common(k)

# 返回一个列表
a = Counter('abracadabra').most_common(3)
print(a)
b =Counter('abracadabra').most_common(5)
print(b)
```

输出：

```
[('a', 5), ('b', 2), ('r', 2)]
[('a', 5), ('b', 2), ('r', 2), ('c', 1), ('d', 1)]

进程已结束，退出代码 0
```

```
例2：elements()

# 可以看到元素计数小于1的就不会被打印出来了
c = Counter(a=4, b=2, c=0, d=-2)
counter_c = list(c.elements())
print(counter_c)

sort_c = sorted(c.elements())
print(sort_c)

c = Counter(a=4, b=2, c=0, d=5)
lis_c = list(c.elements())
print(lis_c)
```

输出：

```
['a', 'a', 'a', 'a', 'b', 'b']
['a', 'a', 'a', 'a', 'b', 'b']
['a', 'a', 'a', 'a', 'b', 'b', 'd', 'd', 'd', 'd', 'd']

进程已结束，退出代码 0
```

- 数学运算

```
c = Counter(a=3, b=1)
d = Counter(a=1, b=2)
print(c + d)                       # add two counters together:  c[x] + d[x]
print(c - d)                      # subtract (keeping only positive counts)
print(c & d)                       # intersection:  min(c[x], d[x]) 
print(c | d)                       # union:  max(c[x], d[x])
```

输出：

```
Counter({'a': 4, 'b': 3})
Counter({'a': 2})
Counter({'a': 1, 'b': 1})
Counter({'a': 3, 'b': 2})
```

#### 2.2 deque： 双端队列

双端队列，可以快速的从另外一侧追加和推出对象,deque是一个双向链表，针对list连续的数据结构插入和删除进行优化。它提供了两端都可以操作的序列，这表示在序列的前后你都可以执行添加或删除操作。双向队列(deque)对象支持以下方法：

- 这一部分内容参考了： https://zhuanlan.zhihu.com/p/343747724；想要详细了解这部分内容的可以去看这份资料，比我整理的详细

```
1、append()：添加 x 到右端。
2、appendleft()：添加到左端
3、clear()：移除所有元素，使其长度为0.
4、copy()：创建一份浅拷贝。
5、count()：计算 deque 中元素等于 x 的个数。
6、extend()：扩展deque的右侧，通过添加iterable参数中的元素。
7、extendleft()：扩展deque的左侧，通过添加iterable参数中的元素。注意，左添加时，
在结果中iterable参数中的顺序将被反过来添加。
8、index()：返回 x 在 deque 中的位置（在索引 start 之后，索引 stop 之前）。 
返回第一个匹配项，如果未找到则引发 ValueError。
9、insert()：在位置 i 插入 x 。如果插入会导致一个限长 deque 超出长度 maxlen 的话，就引发一个 IndexError。
10、pop()：移去并且返回一个元素，deque 最右侧的那一个。 如果没有元素的话，就引发一个 IndexError。
11、popleft()：移去并且返回一个元素，deque 最左侧的那一个。 如果没有元素的话，就引发 IndexError。
12、remove(value)：移除找到的第一个 value。 如果没有的话就引发 ValueError。
13、reverse()：将deque逆序排列。返回 None 。
14、rotate(n=1)：向右循环移动 n 步。 如果 n 是负数，就向左循环。如果deque不是空的，
向右循环移动一步就等价于 d.appendleft(d.pop()) ， 向左循环一步就等价于 d.append(d.popleft()) 。
15、maxlen：Deque的最大尺寸，如果没有限定的话就是 None 。
```

### 3.heapq 库

- 堆： 完全二叉树，每个节点小于等于子节点（默认为最小堆）（数据结构内容，大家自行了解）
- 每个节点k都有两个子节点 2k+1 ， 2k+2
- 用法一： 将无序list转换成最小堆：

```
heapq.heapify(a)
```

- 用法二： 最小堆a中添加元素x：

```
heapq.heappush(a, x)
```

- 用法三：弹出并返回最小元素：

```
heapq.heappop(a)
```

- 用法四：弹出并返回最小元素，同时添加元素x

```
heapq.heapreplace(a,x)
```

- 掌握以上几种方法即可，在做堆排序的题目的时候，或构建最小堆等操作会事半功倍

### 4. functool 库

- Functool 模块应用于高阶函数，即参数或（和）返回值为其它函数的函数
- 蓝桥杯中，我们只需要了解 **偏函数:partial** 即可
- partial： “冻结” 某些函数的参数或者关键字参数，然后返回一个函数
  它的作用是部分应用一个函数，返回一个新的可调用对象，类似于原始函数，但其中的一些参数被固定。这能够更灵活地使用函数，适应不同的需求。
- 举一个例子为大家介绍：

```
from functools import partial
我们自己定义了一个Add函数
def Add(a,b,c):
    print("a = ",a)
    print("b = ",b)
    print("c = ",c)
    print("a + b + c = ",a + b + c)

Add(1,2,3)
print("=" * 20)


这里调用了 partial函数，创建了两个新的函数 add_fix_c  和 add_fix_a ，他们分别固定了参数c=10 和 参数 a=5
这样，通过调用新的函数时，只需要传递剩余的参数

add_fix_c = partial(Add, c = 10)
add_fix_c(1, 2)
print("=" * 20)

add_fix_a = partial(Add, 5)
add_fix_a(2, 3)
```

这里调用了 partial函数，创建了两个新的函数 add_fix_c 和 add_fix_a ，他们分别固定了参数c=10 和 参数 a=5
这样，通过调用新的函数时，只需要传递剩余的参数

- 可以去解决一些定制排序的问题，我找到合适的例题以后会回来更新进来

### 5. itertools 库

- 创建迭代器的模块
- 无限迭代器
- 有限迭代器
- 排列组合迭代器

#### 5.1 无限迭代器

- 生成长度为无限的迭代器
- **count(start = 0, step = 1)** : 创建一个迭代器，它从 start 值开始，返回均匀间隔的值
- **cycle(iterable)** : 创建一个迭代器，循环遍历 iterable 中所有的元素
- **repeat(object [, times ])** : 创建一个迭代器，如果没有指定 times 则无限循环遍历 object ，否则遍历指定次数

#### 5.2 有限迭代器

- **accumulate(iterable[, func])** :创建一个迭代器，返回累积汇总值或其它双目运算的累积结果值
- (1) **accumulate([1,2,3,4,5])** ——> 1 3 6 10 15
- (2) **accumulate([1,2,3,4,5], max)** ——> 1 2 3 4 5
- (3) **accumulate([1,2,3,4,5], operator.mul)** ——> 1 2 6 24 120
- **chain(\*iterables)**: 合并多个迭代器
- (1) chain(‘ABC’, ‘DEF’) ——> A B C D E F

#### 5.3 排列组合迭代器

- product(*iterables, repeat = 1): 可迭代对象的笛卡尔积
- *iterables： 表示这些可迭代序列重复的次数
- repeat：表示这些可迭代序列重复的次数

```
product([1,2,3],[4,5,6])
product('ab', repeat = 2)
product('ab','cd')
```

- permutations(iterable, r = None): 由 iterable 元素生成长度为 r 的排列，如果 r 未指定或为 None，r 默认设置为iterable 的长度

```
permutations('ABCD', 2)
permutations([1,2,3,4])
```

- combinations(iterable, r): 返回值由输入 iterable 中元素组成长度为 r 的子序列

```python
combinations('ABCD', 2)			
#OUTPUT: ————> AB AC AD BC BD CD
combinations([1,2,3,4,5], 3)

例程：
from itertools import  combinations

print(list(combinations('ABCD', 2)))
print(list(combinations([1,2,3,4,5], 3)))
```

输出：

```python
[('A', 'B'), ('A', 'C'), ('A', 'D'), ('B', 'C'), ('B', 'D'), ('C', 'D')]
[(1, 2, 3), (1, 2, 4), (1, 2, 5), (1, 3, 4), (1, 3, 5), (1, 4, 5), (2, 3, 4), (2, 3, 5), (2, 4, 5), (3, 4, 5)]

进程已结束，退出代码 0
```