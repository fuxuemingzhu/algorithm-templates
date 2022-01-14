# Python 快速入门

本文讲解刷题时会用到的 Python 语法，包括基本数据类型、循环、常用函数。

**适合人群**：

- 零基础、想快速学习 Python 的同学。

更详细的讲解建议看[廖雪峰官方网站的 Python教程](https://www.liaoxuefeng.com/wiki/1016959663602400)，只用看到「高级特性」即可，后面的函数式编程、网络、正则等可以不看。

本文也是在廖雪峰 Python 教程的基础上，做了总结、精炼写出的，更适合刷题入门。

## 基本数据类型

### 字符串 str

#### Tips

- 算法题中的字符串基本都是英文字符、数字、标点，因此不会涉及中文与编码问题；

- 与 C++/Java 不同，Python 中没有「字符 char」类型；
- 用`''`或者`""`表示。

#### 长度

```python
>>> len('ABC')
3
```

#### 下标

下标是从 0 开始的。

```python
>>> a = 'ABC'
>>> a[1]
'B'
```

下标可以是负数，表示倒数第几个字符。

```python
>>> a = 'ABC'
>>> a[-1]
'C'
```

#### 切片

切片是用来取一个字符串中的部分元素。

切片表示的区间是是左闭右开，即`[x, y)`。

`a[1:3]`含义是取 `a`的第 1 个元素（包含）到第 3 个元素（不包含），即 `a[1]`, `a[2]`共两个元素。

```python
>>> a = "abcdef"
>>> a[1:3]
'bc'
```

当不写切片的起始位置，表示从第 `0`个元素开始。

```python
>>> a = "abcdef"
>>> a[:3]
'abc'
```

如果不写切片的结束位置，表示读取到最后一个元素。

```python
>>> a = "abcdef"
>>> a[3:]
'def'
```

#### 拼接

```python
>>> a = "abcdef"
>>> b = "xyz"
>>> a + b
'abcdefxyz'
```

#### 修改

python 的字符串是不可变对象，不支持修改。

```python
>>> a = "abcdef"
>>> a[1] = "g"
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
```

#### 字符与 ASCII 码相互转换

使用场景：

- 假如定义了一个大小为 26 的数组，每个位置保存一个小写英文字符出现的个数。
  - 则 `ord('x') - ord('a')` 就是字符 `x` 在数组中的下标。
  - 则 `chr(ord('a') + 1)` 表示数组下标 1 对应的字符，即 `'b'`。

```python
>>> ord('A')
65
>>> chr(66)
'B'
```

### 列表 list

#### Tips

- Python 中的列表 list 是一种**有序列表**，底层用数组实现的，相当于 Java 的 ArrayList 或者 C++ 的 vector；
- 在刷题中**非常常用**，既可以当做普通数组，也可以当做可变长度的数组，还可以当做栈；
- 注意：一般不把列表 list 当做队列使用，因为弹出其开头元素的时间复杂度是 $O(N)$ 。
- 用中括号 `[]` 表示；

#### 长度、下标、切片、拼接

均与字符串的操作相同。

```python
>>> a = [1, 2, 3]
>>> len(a)
3
>>> a[1]
2
>>> a[-1]
3
>>> a[:2]
[1, 2]
>>> b = [4, 5]
>>> a + b
[1, 2, 3, 4, 5]
```

#### 修改

列表是可变对象，可以修改。

```python
>>> a = [1, 2, 3]
>>> a[0] = 100
>>> a
[100, 2, 3]
```

#### 添加

在末尾增加元素，使用 `append(x)` 方法。

**注意**：`append(x)` 是原地操作，没有返回值！

```python
>>> a = [1, 2, 3]
>>> a.append(4)
>>> a
[1, 2, 3, 4]
```

#### 删除

弹出末尾的元素，使用 `pop()`方法。

**注意**：`pop()`是原地操作，其返回值是弹出的值！

```python
>>> a = [1, 2, 3]
>>> a.pop()
3
>>> a
[1, 2]
```

### 元组 tuple

#### Tips

- Python 中的元组 tuple 也是一种有序列表，与列表 list 十分类似，唯一不同是元组 tuple 初始化之后就不能再修改；

- 用小括号 `()` 表示

#### 长度、下标、切片、拼接

与字符串、列表相同。

```python
>>> a = (1, 2, 3)
>>> len(a)
3
>>> a[1]
2
>>> a[-1]
3
>>> a[:2]
(1, 2)
>>> b = (4, 5)
>>> a + b
(1, 2, 3, 4, 5)
```

#### 修改

不支持修改

```python
>>> a[0] = 4
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```

#### 适用场景

- 元组 tuple 由于有不可变特性，因此可以用作字典的 key。（而列表 list 不行）

### 字典 dict

#### Tips

- Python 中的字典 dict 就是哈希表，相当于 Java 中的 HashMap 或者 C++ 中的 unordered_map；

- 用大括号 `{}`表示，每个键值用冒号 `:` 分隔。

#### 元素个数

```python
>>> a = {"a" : 1, "b" : 3, "c" :9}
>>> len(a)
3
```

#### 添加/覆盖

如果字典中已经有这个 key，那么会覆盖；否则是新增。

```python
>>> a = {"a" : 1, "b" : 3, "c" :9}
>>> a["d"] = 100
>>> a["b"] = 666
>>> a
{'a': 1, 'c': 9, 'b': 666, 'd': 100}
```

#### 删除

可以使用 `pop()`方法或者 `del`关键字，看个人习惯。

```python
>>> a = {"a" : 1, "b" : 3, "c" :9}
>>> a.pop("c")
9
>>> a
{'a': 1, 'b': 3}
>>> del a["b"]
>>> a
{'a': 1}
```

#### 获取所有的键/值

可以通过 `keys()` 方法获取字典中存储的所有的键。

可以通过 `values()` 方法获取字典中存储的所有的值。

```python
>>> a = {"a" : 1, "b" : 3, "c" :9}
>>> a.keys()
['a', 'c', 'b']
>>> a.values()
[1, 9, 3]
>>> a.items()
[('a', 1), ('c', 9), ('b', 3)]
```

### 集合 set

#### Tips

- Python 中的集合 set 就是哈希集合，相当于 Java 中的 HashSet 或者 C++ 中的 unordered_set；
- 用大括号 `{}`表示。
- 初始化的时候不能用`{}`，因为 `{}`表示空的字典。

#### 元素个数

```python
>>> a = {1, 2, 3}
>>> len(a)
3
```

#### 添加

集合会自动去重。

**注意**：`remove` 是原地操作，没有返回值！

```python
>>> a = {1, 2, 3}
>>> a.add(4)
>>> a
set([1, 2, 3, 4])
>>> a.add(3)
>>> a
set([1, 2, 3, 4])
```

#### 删除

可以使用 `remove()`方法。

**注意**：`remove` 是原地操作，没有返回值！

```python
>>> a = {1, 2, 3}
>>> a.remove(3)
>>> a
set([1, 2])
```

## 循环

### for

for 循环基本有两个作用：

- 让一段代码执行多次；
- 遍历某个数据结构。

#### 让一段代码执行多次

常见的使用场景：

- 杨辉三角；
- 动态规划；

```python
>>> for i in range(10):
...     print(i)
... 
0
1
2
3
4
5
6
7
8
9
```

#### 遍历某个数据结构

可以对列表 list、元组 tuple、字典 dict、集合 set 进行遍历。

列表 list /元组 tuple 的 for 遍历是按照下标的顺序的，下面的代码 `i` 是 `a`中的每个元素。

```python
>>> a = [1, 2, 3]
>>> for i in a:
...     print(i)
... 
1
2
3
```

字典 dict 的遍历是对其存储的 key 的遍历。遍历是无序的。

```python
>>> a = {"a" : 1, "b" : 3, "c" :9}
>>> for i in a:
...     print(i)
... 
a
c
b
```

集合 set 的遍历是无序的。

```python
>>> a = {"3", "4", "1", "2"}
>>> for i in a:
...     print(i)
... 
1
3
2
4
```

**注意**：不要在循环中修改正在遍历的数据结构！

**错误做法**：

```python
>>> a = {"3", "4", "1", "2"}
>>> for i in a:
...     if i == "1":
...         a.remove(i)
... 
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
RuntimeError: Set changed size during iteration
```

### while

相比于 for 循环，while 循环更常用于不确定循环次数的的情况：「满足某种条件」、「不满足某种条件」等场景。

比如广度优先遍历 BFS 中会使用 while 循环。

举例： [102. 二叉树的层序遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/) ，使用 BFS 解决，参考代码中同时用到了 while 和 for，可以体会下两者的使用场景。

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def levelOrder(self, root):
        queue = collections.deque()
        queue.append(root)
        res = []
        while queue:
            size = len(queue)
            level = []
            for _ in range(size):
                cur = queue.popleft()
                if not cur:
                    continue
                level.append(cur.val)
                queue.append(cur.left)
                queue.append(cur.right)
            if level:
                res.append(level)
        return res
```

上面的代码中使用了 `while queue` 这样的写法，相当于 `while len(queue) != 0`。

## 常用函数

### abs

`abs()` 函数用于求一个数值的绝对值。

```python
>>> abs(-100)
100
>>> abs(-66.6)
66.6
```

### min/max

`min()` / `max() `用于求一个列表 list、元组 tuple、集合 set 所有元素的最小值/最大值。

```python
>>> a = [1, 2, 3]
>>> min(a)
1
>>> a = {3, 4, 1, 2}
>>> max(a)
4
```

### sum

`sum()` 函数用于求一个列表 list、元组 tuple、集合 set 所有元素的和。

```python
>>> a = [1, 2, 3]
>>> sum(a)
6
>>> a = {3, 4, 1, 2}
>>> sum(a)
10
```

### int/float/str

`int()` / `float()` / `str()` 用于数据类型转换。

`int()` 函数可以将字符串、浮点数转成整型。

```python
>>> int("123")
123
>>> int("-123")
-123
>>> int(23.4)
23
>>> int(-23.4)
-23
```

`float()` 函数可以将字符串、整型转成浮点数。

```python
>>> float("123.4")
123.4
>>> float(123)
123.0
```

`str()` 函数可以将整型、浮点数转成字符串。

```python
>>> str(123)
'123'
>>> str("123.4")
'123.4'
```

有些题目中，将数据类型转换之后做起来更简单。比如[7. 整数反转](https://leetcode-cn.com/problems/reverse-integer/)，可以写出下面这种非常狗🐶的写法：

```python
class Solution(object):
    def reverse(self, x):
        if x == 0: return 0
        flag = 1
        if x < 0:
            flag = -1
            x = -x
        r = int(str(x)[::-1]) # 先转成字符串，翻转字符串，然后再转成整数
        if flag == 1 and r <= 2147483647:
            return r
        elif flag == -1 and -r >= -2147483648:
            return -r
        return 0
```

但是不建议这么做，因为有点类似于作弊。

### bin

`bin()` 是获取整数的二进制，用字符串表示。

注意：`bin()`函数结果的前两位永远是 `0b`，真正的二进制需要把前两位去掉。

```python
>>> bin(10)
'0b1010'
```

二进制转十进制怎么转呢？使用 `int`函数，第二个参数填 2，表示是要把二进制转十进制。

```python
>>> int("1010", 2)
10
```

## 高级函数

下面的几个高级函数你可能在算法题解中遇到，但并不是刷题必会的，你完全可以用 for 循环实现它们。

这些函数存在的意义是简化代码。

### map

`map()`函数接收两个参数，第一个参数是函数，第二个参数是可迭代对象。

`map()`函数自动把函数作用到可迭代对象的每个元素上；返回值的元素个数和输入的可迭代对象个数相等。

注意：Python2 和 Python3 的 `map()`函数返回值类型不同。

- Python2 的 `map()` 函数返回的是个列表 list；
- Python3 的 `map()` 函数返回的是个可迭代对象，想要变成 list 需要把结果传入 `list()`函数。

下面是个求平方的例子，注意返回值 `r` 的类型。

Python2：

```python
>>> def f(x):
...     return x * x
...
>>> r = map(f, {1, 2, 3, 4, 5, 6, 7, 8, 9})
>>> r
[1, 4, 9, 16, 25, 36, 49, 64, 81]
```

Python3：

```python
>>> def f(x):
...     return x * x
...
>>> r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> r
<map object at 0x7fb83803ca30>
>>> list(r)
[1, 4, 9, 16, 25, 36, 49, 64, 81]
```

### reduce

`reduce()` 函数接收两个参数，第一个参数是函数，第二个参数是可迭代对象。

与 `map()` 函数不同的是，`reduce()` 的第一个函数需要接收两个参数。

`reduce()`的作用是把可迭代对象的前两个元素作为函数的输入，计算得到的结果 与 序列的下一个元素当做函数的两个输入进行计算……依次递推，直至全部元素都处理完。

`reduce()`函数的返回值是一个值。

其效果就是：

```python
reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)
```

使用`reduce()`进行求和的例子：

```python
>>> def add(x, y):
...     return x + y
...
>>> reduce(add, [1, 3, 5, 7, 9])
25
```



看到这里，你已经基本上掌握了 Python 的常见语法。

Python 的语法非常简单，尤其擅长字符串处理，容易快速上手。

本文没有讲解 Python 中与算法有关的函数——将在第二章「Python 刷题手册」中讲解。



参考资料：

1. [廖雪峰官方网站的 Python教程](https://www.liaoxuefeng.com/wiki/1016959663602400)
