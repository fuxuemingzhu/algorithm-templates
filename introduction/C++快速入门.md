# C++ 快速入门

本文讲解刷题时会用到的 C++ 语法，包括基本数据类型、循环、常用函数。

**适合人群**：

- 零基础、想快速学习 C++ 的同学。

本文参考了[菜鸟教程](https://www.runoob.com/cplusplus/cpp-tutorial.html)、《C++ Primer》，不讲解最基本变量类型与预算符等，旨在能快速学习与上手算法题。

# 基本数据类型

### 字符串 string

#### Tips

- 算法题中的字符串基本都是英文字符、数字、标点，因此不会涉及中文与编码问题；
- C++ 中有「字符串」和「字符」两种类型，分别用 `""` 和`''`表示。
- C++ 的 string 是可变长的，内容是可修改的。

#### 定义与初始化

string 的一些常见的初始化方式：

```C++
string s1; // 默认初始化，s1 是一个空字符串
string s2 = s1; // s2 是 s1 的副本
string s3 = "abcdef"; // s3 是字符串字面值的副本
string s4(10, 'c'); // s4 的内容是 cccccccccc
```

#### 长度

```C++
s4.size();
```

#### 取某下标的字符

下标是从 0 开始的，取值范围是 `[0, s.size() - 1]`，双闭区间。

```C++
string s3 = "abcdef";
std::cout << s3[1];

结果: b
```

string 的下标不可以是负数，也不可以大于 $s.size() - 1$。否则会报未定义行为的异常，也就是说可能什么也不发生，也可能机器冒烟。

```C++
string s = "abcdef";
std::cout << s[-1];

Char 9: runtime error: addition of unsigned offset to 0x7fff7f34f350 overflowed to 0x7fff7f34f34f (basic_string.h)
SUMMARY: UndefinedBehaviorSanitizer: undefined-behavior /usr/bin/../lib/gcc/x86_64-linux-gnu/9/../../../../include/c++/9/bits/basic_string.h:1070:9
```

#### 取子串

取某个 string 的子串的操作使用的函数 `substr(x, len)`。

- 其含义是从字符串的第 `x` 个下标开始，截取长度为 `len` 的子串，返回一个新构造的 string 。

- 所以实际上截取的子串范围是 `[x, x + len - 1]`，左闭右闭的区间。

- `a.substr(1,3) `含义是取 `a`的第 1 个元素（包含）到第 3 个元素（包含），即 `a[1]`, `a[2]`,`a[3]` 共 3 个元素。

- 如果截取的右边界超出了字符串，那么只到右边界。

- 如果 `substr(x)` 只有一个参数，表示从 `x` 下标开始截取到字符串的末尾。

```C++
string s = "abcdef";
cout << s.substr(1,3) << endl;
结果：bcd

string s = "abcdef";
cout << s.substr(2) << endl;
结果：cdef
```

#### 拼接

```C++
string a = "abcdef";
string b = "xyz";
string c = a + b;
cout << c << endl;

结果：abcdefxyz
```

#### 修改

C++ 的字符串可变，支持通过下标修改。

```
string a = "abcdef";
a[1] = 'g';
cout << a << endl;

结果：agcdef
```

#### 字符与 ASCII 码相互转换

使用场景：

- 假如定义了一个大小为 26 的数组，每个位置保存一个小写英文字符出现的个数。
  - 则 `'x' - 'a'` 就是字符 `x` 在数组中的下标。
  - 则 `char('a' + 1)` 表示数组下标 1 对应的字符，即 `'b'`。

```c++
cout << 'x' - 'a' << endl;
输出：23

cout << char('a' + 23) << endl;
输出：x
```

### 向量 vector

#### Tips

- C++ 中的向量 vector 是一种有序列表，底层用数组实现的，相当于 Java 的 ArrayList 或者 Python 的 list；
- 在刷题中**非常常用**，可以当做普通数组、可变长的数组；
- 虽然可以当做栈，但是一般使用 C++ 中的 stack 作为栈；不能作为队列使用。

#### 长度、下标

```C++
vector<int> a = {1, 2, 3, 4, 5, 6};
cout << a.size() << endl;
输出：6
cout << a[2] << endl;
输出：3
```

#### 修改

vector 是可变数组，可以修改。

```C++
vector<int> a = {1, 2, 3, 4, 5, 6};
cout << a[1] << endl;
输出：2
  
a[1] = 100;
cout << a[1] << endl;
输出：100
```

### 添加

在末尾增加元素，使用 `push_back(x)` 方法。

**注意**：`push_back(x)` 是原地操作，没有返回值！

```C++
vector<int> a = {1, 2, 3, 4, 5, 6};
for (int i : a) {
    cout << i << " ";
}
输出：1 2 3 4 5 6 
  
a.push_back(100);
for (int i : a) {
    cout << i << " ";
}
输出：1 2 3 4 5 6 100 
```

#### 删除

弹出末尾的元素，使用 `pop_back()`方法。

**注意**：`pop_back()`是原地操作，没有返回值！

```C++
vector<int> a = {1, 2, 3, 4, 5, 6};
for (int i : a) {
    cout << i << " ";
}
输出：1 2 3 4 5 6 

a.pop_back();
for (int i : a) {
    cout << i << " ";
}
输出：1 2 3 4 5 
```

### pair

#### Tips

- C++ 中的 pair 是将两个元素合成一组数据，两个元素可以有不同的数据类型；
- 例如，遍历 STL 中的 map 时， key 和 value 就是放在 pair 中的；
- 如果函数需要返回两个值的时候，可以用 pair 保存两个值一起返回；
- 可以把 pair 当做 map 的 key，比如保存某 `(x, y)` 位置的状态。

#### 创建与初始化

```c++
pair<string, int> word_count; // 创建一个空的 pair, 可用于统计字符串出现的次数
pair<string, int> name_age("Tom", 18); // 创建并初始化一个 pair
auto author = make_pair("fuxuemingzhu", "cpp"); // 使用 make_pair 构建一个 pair
```

#### 访问元素

```C++
pair<string, int> name_age("Tom", 18);
cout << name_age.first;
输出：Tom
  
cout << name_age.second;
输出：18
```

#### 修改

```c++
pair<string, int> name_age("Tom", 18);
name_age.first = "Alice";
cout << name_age.first;
输出：Alice

name_age.second = 25;
cout << name_age.second;
输出：25
```

### Map