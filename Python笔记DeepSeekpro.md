# Python 网络自动化笔记

> 本笔记整理自《WOLF实验室 Python网络自动化》系列课程，覆盖 Python 基础语法、数据类型、运算符、流程控制、字符串操作、元组/字典/集合、哈希原理、字符编码与文件操作，共十个章节。
> 授课老师：杨广成（CCIE / HCIE）

---

## 目录

1. [Python 简介与开发环境](#1-python-简介与开发环境)
2. [变量与注释](#2-变量与注释)
3. [数据类型（数字、字符串、布尔、列表）](#3-数据类型数字字符串布尔列表)
4. [运算符](#4-运算符)
5. [用户输入与格式化输出](#5-用户输入与格式化输出)
6. [流程控制（if / elif / else）](#6-流程控制if--elif--else)
7. [流程控制（while / for 循环）](#7-流程控制while--for-循环)
8. [流程控制综合举例](#8-流程控制综合举例)
9. [字符串常用操作](#9-字符串常用操作)
10. [元组、字典、集合](#10-元组字典集合)
11. [哈希：为何字典查询快](#11-哈希为何字典查询快)
12. [字符编码](#12-字符编码)
13. [文件操作](#13-文件操作)

---

## 1. Python 简介与开发环境

### 1.1 什么是编程

**详细介绍：** 编程即"编写程序"的中文简称，本质是让计算机去解决某个问题——针对某个计算体系规定一定的运算方式，让计算机按照这种方式执行，最终获取结果。计算机底层只能识别二进制（0 和 1），最早期人类确实直接输入 0/1 代码，但这种方式开发速度极慢。于是人们发明了更高级的"指令"，把想表达的事情通过指令书写，再由计算机把这些指令翻译成二进制去执行。

**举例：** 想让主机播放一首歌，只需输入 `open 某首歌.mp3`、`play` 这类指令即可，CPU 收到指令后会将其转换为自身可执行的二进制代码，再调用硬盘上的歌曲通过音箱播放。

### 1.2 编程语言的三个层级

**详细介绍：** 编程语言从低到高分为三层：

| 类型 | 特点 | 缺点 |
|------|------|------|
| 机器语言 | 最底层、速度最快 | 最复杂、开发效率最低、依赖具体硬件 |
| 汇编语言 | 使用易于理解的助记符，直接操作硬件 | 仍难理解、难记忆、难应用 |
| 高级语言 | 对底层硬件指令做了封装，省略大量细节 | 需转换后才能被计算机识别 |

**举例：** 用汇编打印一句 hello world 需要很长一串助记符代码；而用高级语言只需 `print("hello world")` 一行。

### 1.3 编译型语言与解释型语言

**详细介绍：** 高级语言编写的程序不能被计算机直接识别，必须经过转换。按转换方式分两类：

- **编译型**：源代码执行前，一次性全部翻译成目标语言（机器语言），再执行。代表：C、C++、Delphi。
  - 优点：执行速度快，可脱离语言环境独立执行（生成可执行文件）。
  - 缺点：跨平台性差，因为直接与操作系统接口打交道。
- **解释型**：类似"同声传译"，边翻译边执行。代表：Python、Java、PHP、Ruby。
  - 优点：跨平台好（解释器封装了与操作系统交互的接口，一份代码处处运行）。
  - 缺点：执行速度慢，且不能生成独立可执行文件，运行必须依赖解释器。

**举例：** 编译型就像先把整本中文书翻译成英文再读；解释型就像同声传译，说一句翻一句。Python 属于解释型语言。

### 1.4 Python 的发展历史与应用领域

**详细介绍：** Python 由荷兰人 **吉多·范罗苏姆（Guido van Rossum）** 于 1989 年开始编写编译器，名字来源于他挚爱的电视剧《Monty Python's Flying Circus》。他希望创造一种"基于 C 与 shell 之间、功能全面、易学易用、可扩展"的语言，崇尚优美、清晰、简单。

几个关键时间节点：

- 2005 年加入 Google，Python 逐渐出现在大众视野；
- 2012 年云计算兴起（OpenStack 架构基于 Python 开发）；
- 2014 年 AI 人工智能、数据分析兴起；
- 2016—2017 年 Python 走入大众，2019 年后"全民编程"。

主要应用领域：

- Web 开发（如 Django 框架）；
- 网络编程（高并发网络架构）；
- 爬虫（Python 几乎处于霸主地位，但须合规使用）；
- 云计算（OpenStack）；
- 人工智能与数据分析（必备语言）；
- 自动化运维（本课程核心目标）；
- 金融分析（量化交易、高频交易）。

### 1.5 Python 2 与 Python 3

**详细介绍：** 2008 年是分水岭。2008 年前是 Python 2.0 时代，2008 年后进入 Python 3.0 时代。由于 Python 3.0 不兼容 2.0，很多公司老项目仍基于 2.0，因此 2010 年推出了 2.7 这个"过渡版本"。**现在学习与开发都应使用 Python 3**，Python 3 中默认编码改为 unicode，文件存储编码改为 UTF-8。

### 1.6 环境安装

**详细介绍：** 主流操作系统 Linux/Unix 自带 Python 环境。Windows 安装很简单，关键一步是在安装向导中勾选"Add Python to PATH"（把 python.exe 加入环境变量），这样在任何目录下都能调用 `python` 命令，无需手动配置环境变量。

### 1.7 第一个 Python 程序

**详细介绍：** 按照编程惯例，第一程序输出 hello world。新建文本文件 `hello.py`，写入代码，用 `python hello.py` 运行。

**举例：**

```python
print("hello world")
```

运行方式：在 CMD 中执行 `python hello.py`（或把文件拖进命令行）。这种"交互模式"（直接输入 `python` 进入）适合测试、调试代码功能；真正编写程序应使用 IDE（如 PyCharm，专业版功能最全）。

---

## 2. 变量与注释

### 2.1 什么是变量

**详细介绍：** 变量是**内存中存放数据的一个容器**。计算机最核心的功能是计算，计算需要数据源，数据源就存在内存里。我们给变量起个名字并赋值，后面程序就可以直接调用这个变量名。

**举例：**

```python
name = "小明"      # 姓名
age = 22           # 年龄
height = 1.8       # 身高（米）

print(name)     # 小明
print(age)      # 22
print(height)   # 1.8
```

### 2.2 变量必须先定义后调用

**详细介绍：** 程序是**从上往下依次执行**的，所以变量必须先定义、后调用，否则会报 `NameError: name 'xxx' is not defined`。

**举例（错误示范）：**

```python
print(address)   # 报错：address 未定义
address = "徐汇区漕宝路82号"
```

**正确写法：**

```python
address = "徐汇区漕宝路82号"
print(address)
```

### 2.3 变量命名规则

**详细介绍：**

- 变量名只能由**字母、数字、下划线**任意组合；
- 第一个字符**不能是数字**；
- 不能使用 Python 的**关键字**（如 `and`、`as`、`for`、`break`、`class`、`continue` 等）；
- 命名风格推荐两类：
  - **驼峰体**：每个单词首字母大写，如 `numberOfStudents`；
  - **下划线式**：单词间用下划线连接，如 `number_of_students`（课程推荐）。
- 不建议用中文/拼音作变量名，变量名应"见名知意"，不要过长或词不达意。

**举例：**

```python
number_of_students = 51   # 推荐
numberOfStudents = 51     # 驼峰体，也行
# 1st = 10                # 错误：不能以数字开头
# class = "python"        # 错误：关键字不能作变量名
```

### 2.4 变量的创建过程

**详细介绍：** 执行 `name = "andy"` 时，实际是：① 在内存中开辟一块空间存放 `"andy"`；② 让变量名 `name` 指向该内存地址。可通过 `id(name)` 查看该变量在内存中的地址。

**举例：**

```python
name = "andy"
print(id(name))   # 输出内存地址，如 140231234567890
```

### 2.5 变量的修改（重新指向）

**详细介绍：** 修改变量**不是**用新值覆盖旧值，而是：① 再申请一块新内存空间存放新值；② 断开原来指向旧值的链接；③ 让变量名指向新值。所以修改前后 `id()` 会不同。

**举例：**

```python
name = "andy"
print(id(name))     # 地址A
name = "jack"
print(id(name))     # 地址B，和地址A不同
```

### 2.6 变量的指向关系

**详细介绍：** 多个变量可以指向同一内存地址。修改其中一个变量，只是断开它与旧值的连接并指向新值，不影响其它变量。

**举例：**

```python
name1 = "andy"
name2 = name1     # name2 也指向 "andy"
print(name1, name2)   # andy andy

name1 = "jack"    # name1 重新指向 "jack"
print(name1, name2)   # jack andy  （name2 仍指向 andy）
```

### 2.7 垃圾回收机制

**详细介绍：** Python 解释器有**自动垃圾回收机制**，会周期性地将**没有与任何变量名关联**的内存数据删除，程序员无需手动释放内存。

### 2.8 常量

**详细介绍：** 常量即运行过程中不变的量（如 π）。Python **没有专门定义常量的语法**，程序员约定俗成用**全大写**表示常量。C 语言则用 `const` 定义、修改会报错。

**举例：**

```python
PI = 3.141592653   # 约定：全大写表示常量
GENDER = "男"
```

### 2.9 注释

**详细介绍：** 注释是代码中不执行的部分，用于增加代码可读性（给自己和协作的人看）。分为：

- **单行注释**：以 `#` 开头（快捷键 Ctrl + /）；
- **多行注释**：用三对双引号 `""" ... """` 或三对单引号 `''' ... '''` 包裹。

注释可用中文或英文，但**不要用拼音**；只在重要或不好理解的地方注释即可。

**举例：**

```python
# 这是单行注释
name = "andy"   # 注释也可以跟在代码后面

"""
这是多行注释
可以写多行内容
不会被程序执行
"""
```

---

## 3. 数据类型（数字、字符串、布尔、列表）

**详细介绍：** 计算机分不清"1"和"汉字"，因此每种编程语言都有"数据类型"，对常用的各种数据进行明确划分，方便计算机正确处理（数字运算传数字、文字处理传字符串）。Python 常用数据类型：数字、字符串、布尔、列表、集合、字典、字节。

### 3.1 数字（int 和 float）

**详细介绍：**

- **整型 int**：整数。64 位系统上整数位数为 64。
- **长整型**：Python 与 C 不同，长整型不指定位宽、不限制大小（受机器内存限制）。Python 2.2 起整数溢出会自动转为长整型，Python 3 中已没有 long，统一用 `int`。
- **浮点型 float**：即小数。

可用 `type()` 查看数据的类型。

**举例：**

```python
age = 22
print(type(age))     # <class 'int'>

height = 1.8
print(type(height))  # <class 'float'>
```

### 3.2 字符串 str

**详细介绍：** 字符串是**有序的字符集合**，用于存储和表示基本的文本信息。用单引号 `'...'`、双引号 `"..."` 或三引号 `'''...'''` 包裹的内容都是字符串。**下标从 0 开始**，从左到右顺序访问。

- 单引号、双引号、三引号**没有本质区别**；
- 当字符串内部本身含有引号时，需要单双引号**配合使用**；
- 多行文本用**三引号**。

**举例：**

```python
name = "老杨"
hometown = '山东'

# 字符串内有单引号，用双引号包裹
message = "my name is old yang, I'm 18 year old"

# 多行字符串用三引号
poem = '''床前明月光，
疑是地上霜。'''

print(type(name))   # <class 'str'>
```

**字符串的运算（拼接）：**

**详细介绍：** 字符串只能做**相加（拼接）**和**相乘（重复）**，不能相减，也不能与数字等其他类型拼接。

**举例：**

```python
a = "我本将心向明月"
b = "奈何明月照沟渠"
print(a + b)     # 我本将心向明月奈何明月照沟渠
print("哈哈" * 3)  # 哈哈哈哈哈
# print("数字" + 1)   # 错误：字符串不能和数字拼接
```

### 3.3 布尔类型 bool

**详细介绍：** 布尔类型只有两个值：`True`（真）和 `False`（假），主要用于逻辑判断。当需要让计算机描述"A 大于 B"是否成立时，就通过布尔类型表达。常与流程控制（if/else）结合。

**举例：**

```python
a = 3
b = 5
print(a > b)   # False
print(a < b)   # True

score = 690
if score > 680:
    print("恭喜你，可以上清华北大")
else:
    print("欢迎你，蓝翔技校")
```

### 3.4 列表 list

**详细介绍：** 列表用**方括号**括起来，元素之间用逗号分隔，用于存放多个值。用字符串记录全班人名不灵活（想把单独的"andy"取出来很麻烦），而用列表则非常方便。

列表特点：

- 可存放多个值；
- 从左到右依次定义元素，**下标从 0 开始**，顺序访问、有序；
- **可变**，可修改指定索引的值，可增删改查。

**举例：**

```python
names = ["老王", "老杨", "andy", "rachel", "mike"]
print(names)        # ['老王', '老杨', 'andy', 'rachel', 'mike']
print(names[2])     # andy  （下标从0开始：0老王 1老杨 2andy）
```

#### 3.4.1 列表增加（insert / append）

**详细介绍：** 增加元素有两种方式：

- **insert(位置, 元素)**：可在任意位置插入；
- **append(元素)**：只能追加到列表末尾。

**举例：**

```python
names = ["老王", "老杨", "andy", "rachel", "mike"]
names.insert(3, "小明")   # 在索引3处（andy后面）插入小明
names.append("小王")       # 末尾追加小王
print(names)   # ['老王', '老杨', 'andy', '小明', 'rachel', 'mike', '小王']
```

#### 3.4.2 列表查询（index）

**详细介绍：** 用 `index(元素)` 查询某元素在列表中的位置（索引）。

**举例：**

```python
names = ["老王", "老杨", "andy", "小明", "rachel", "mike", "小王"]
print(names.index("小明"))   # 3
print(names[3])              # 小明
```

#### 3.4.3 列表修改

**详细介绍：** 根据下标找到元素位置，重新赋值即可修改。

**举例：**

```python
names[0] = "老王(中文)"
print(names)   # ['老王(中文)', '老杨', ...]
```

#### 3.4.4 列表删除（remove / del / pop）

**详细介绍：** 删除元素有多种方法：

- `remove(元素)`：删除从左开始的第一个匹配元素；
- `del 列表[索引]`：按索引删除；
- `pop()`：删除并返回最后一个元素；
- `pop(索引)`：删除指定索引的元素。

**举例：**

```python
names = ["老王", "老杨", "andy", "rachel", "mike", "小王"]
names.remove("rachel")   # 删除第一个 rachel
del names[4]             # 删除索引4的元素（小王）
names.pop()              # 删除最后一个元素
names.pop(1)             # 删除索引1的元素（老杨）
```

#### 3.4.5 列表清空（clear）

**举例：**

```python
names.clear()
print(names)   # []
```

#### 3.4.6 列表切片

**详细介绍：** 切片可一次取出多个元素，格式 `列表[起始:结束]`，**顾头不顾尾**（包含起始下标元素、不包含结束下标元素）。也可用负下标反向切片。

**举例：**

```python
names = ["老王", "老杨", "andy", "rachel", "mike"]
a = names[1:5]
print(a)    # ['老杨', 'andy', 'rachel', 'mike']  （不含索引5）

a2 = names[-5:-1]
print(a2)   # 从后往前的反向切片，同样顾头不顾尾
```

#### 3.4.7 列表反转（reverse / 切片）

**举例：**

```python
names = ["老王", "老杨", "andy", "rachel", "mike"]
names.reverse()
print(names)          # 原地反转
print(names[::-1])    # 用切片实现反转
```

#### 3.4.8 列表排序（sort）

**详细介绍：** `sort()` 针对列表做排序。数字按从小到大；字符串按字符编码顺序排序。

**举例：**

```python
a = [3, 55, 89, 100, 67, 88]
a.sort()
print(a)   # [3, 55, 67, 88, 89, 100]

names.sort()
print(names)   # 按字符编码排序
```

#### 3.4.9 循环列表

**详细介绍：** 用 `for` 循环遍历列表元素。

**举例：**

```python
names = ["老王", "老杨", "andy", "小明", "rachel", "mike"]
for i in names:
    print(i)
```

---

## 4. 运算符

### 4.1 算术运算符

**详细介绍：** 加减乘除之外，重点是：

- `%` **取模**：返回除法余数（常用于判断奇偶）；
- `**` **幂**：如 `2**10` 表示 2 的 10 次方；
- `//` **取整（整除）**：舍去小数部分。

**举例：**

```python
print(5 % 2)    # 1 （5除以2余1）
print(2 ** 10)  # 1024
print(7 // 2)   # 3 （不要小数点后面）

# 用取模判断 1~100 的奇数
for i in range(1, 101):
    if i % 2 == 1:
        print(i)   # 1 3 5 7 9 ...
```

### 4.2 比较运算符

**详细介绍：**

- `==` 等于（**两个**等号才是"等于"）；
- `!=` 不等于；
- `>`、`<`、`>=`、`<=` 大于、小于、大于等于、小于等于。

注意：**一个等号 `=` 是赋值，两个等号 `==` 才是比较是否相等**。

**举例：**

```python
a = 10
b = 20
print(a == b)   # False
print(a != b)   # True
print(a < b)    # True
```

### 4.3 赋值运算符

**详细介绍：** 复合赋值：`+=`、`-=`、`*=`、`/=`。`b += a` 等价于 `b = b + a`。其中 **`i += 1`（自增）在后面循环里用得很多**，等价于 `i = i + 1`。

**举例：**

```python
b = 20
b += 10
print(b)   # 30

i = 0
i += 1   # 相当于 i = i + 1
print(i)   # 1
```

**注意：** 循环（while/for/if）语句结尾必须有**冒号 `:`**，这是 Python 的语法规则，缺少会报错。

### 4.4 逻辑运算符

**详细介绍：**

- `and` **与**：多个条件**都**为真时返回真；
- `or` **或**：任一条件为真即返回真；
- `not` **非**：取反。

**举例：**

```python
a = 10
b = 20
print(a > 10 and b > 10)   # False （a>10 不成立）
print(a > 5 or b > 10)     # True  （b>10 成立）
print(not a == b)          # True  （a==b 为 False，取反为 True）
```

---

## 5. 用户输入与格式化输出

### 5.1 input 读取用户指令

**详细介绍：** 程序执行时若需要用户输入（如登录哪台设备、输入用户名密码），用 `input(提示语)`。**关键点：input 接收到的所有输入默认都是字符串（str）**，即使输入的是"22"，也是字符串。要与数字比较或运算，必须先用 `int()` 转换。

**举例：**

```python
name = input("what's your name? ")
print("hello " + name)   # 输入老杨 → hello 老杨

# 问卷调查
name = input("姓名: ")
age = input("年龄: ")
job = input("工作: ")
print(name, age, job)
```

### 5.2 格式化输出（占位符 %）

**详细介绍：** 拼接字符串做格式化输出"很不智能"，更推荐**占位符**方式：预先定义好格式模板，用占位符表示待填充位置，最后用 `%` 把前面字符串与后面括号里的变量按顺序关联起来。

占位符类型：

- `%s` 字符串占位符；
- `%d` 数字占位符；
- `%f` 浮点数占位符。

**举例：**

```python
name = "小甜甜"
age = 22
job = "teacher"
question = "yes"

info = '''%s 的信息如下：
姓名：%s
年龄：%d
职业：%s
你喜欢我吗：%s''' % (name, name, age, job, question)

print(info)
```

输出：

```
小甜甜 的信息如下：
姓名：小甜甜
年龄：22
职业：teacher
你喜欢我吗：yes
```

---

## 6. 流程控制（if / elif / else）

**详细介绍：** 流程控制让程序在满足某个条件时执行对应代码。之前写的程序都是一条直线走到底，而现实中会遇到分岔路，需要判断后决定往哪走。"满足条件 → 执行某段代码；不满足 → 执行其它代码"。

### 6.1 单分支（if）

**举例：**

```python
age = int(input("how old are you? "))   # 先转成int，否则字符串无法和18比较
if age >= 18:
    print("你可以进来，玩得开心")
```

**重要：** input 获取的是字符串，`age >= 18` 会报 `TypeError: '>=' not supported between instances of 'str' and 'int'`，所以要先 `int(input(...))` 转成数字。

### 6.2 双分支（if / else）

**举例：**

```python
age = int(input("how old are you? "))
if age >= 18:
    print("玩得开心")
else:
    print("好好学习，天天向上")
```

### 6.3 多分支（if / elif / else）

**详细介绍：** 多个条件时用 `elif`（相当于"else if"）。多个分支是**自上而下匹配**，一旦某条件满足，执行对应代码后**不再往下执行**。

**举例（猜年龄）：**

```python
age = 38
guess = int(input("猜猜我多大了: "))
if guess > age:
    print("猜大了，往小了试试")
elif guess < age:
    print("猜小了，往大了试试")
else:
    print("恭喜你，猜对了")
```

**举例（CPU 使用率分级报警）：**

```python
cpu = int(input("请输入CPU使用率: "))
if cpu > 100:
    print("着火了，问题严重")
elif cpu >= 90:
    print("A级报警")     # 90~100
elif cpu >= 80:
    print("B级报警")     # 80~89
elif cpu >= 60:
    print("C级报警")     # 60~79
elif cpu >= 40:
    print("D级报警")     # 40~59
else:
    print("E级报警")     # 0~39
```

> 注意：因为自上而下匹配，`elif cpu >= 90` 前面已经排除了 `>100` 的情况，所以不必再写 `and cpu <= 100`。

### 6.4 缩进（Python 的一大特色）

**详细介绍：** Python 通过**强制缩进**来区分代码块，而非其他语言（C/Java/JavaScript）的大括号。

- 顶级代码（不依赖任何条件）必须**顶格写**；
- 同一级别的代码**缩进必须一致**；
- 每个条件（if/elif/else/while/for）下面一行缩进（官方建议 **4 个空格**，2 个或 8 个也行，但须统一）。

缩进的目的是让程序知道每段代码依附于哪个条件。

**举例：**

```python
if age >= 18:
    print("玩得开心")    # 缩进4格，属于 if
else:
    print("好好学习")    # 缩进4格，属于 else
```

---

## 7. 流程控制（while / for 循环）

### 7.1 while 循环

**详细介绍：** `while 条件:` 当条件成立时，循环执行下面缩进的代码；条件不成立则跳出循环。理解方式：**"当……时，就……"**。

**举例（打印 0~100）：**

```python
count = 0
while count <= 100:
    print(count)
    count += 1   # 每循环一次加1，否则是死循环
```

> 务必有 `count += 1` 这类改变条件的语句，否则 count 永远 ≤100，变成死循环。

**举例（猜年龄给5次机会）：**

```python
age = 38
count = 1
while count <= 5:
    guess = int(input("猜猜年龄: "))
    if guess > age:
        print("猜大了，往小了试试")
    elif guess < age:
        print("猜小了，往大了试试")
    else:
        print("恭喜猜对了")
    count += 1
```

### 7.2 死循环（while True）

**详细介绍：** 当 while 后面的条件**永远成立**时，形成死循环（如 `while True:`）。这在需要 24 小时不断监控的场景有用。**注意 `True` 首字母必须大写**，小写会被当成变量名而报错。

**举例：**

```python
count = 0
while True:
    print("wolf lab")
    count += 1
```

程序会以极快速度重复执行。

### 7.3 break 与 continue

**详细介绍：**

- **break**：完全结束循环，跳出循环体，执行循环后面的语句；
- **continue**：只终止**本次**循环，继续执行下一轮循环。

**举例（break）：**

```python
count = 0
while count <= 100:
    print(count)        # 输出 0 1 2 3 4 5
    if count == 5:
        break           # 到5就完全跳出循环
    count += 1
print("已经跳出循环体")
```

**举例（continue）：**

```python
count = 0
while count <= 100:
    count += 1
    if count > 5 and count < 90:
        continue        # 跳过本次，继续下一轮
    print(count)        # 输出 1 2 3 4 5 90 91 ... 101
```

### 7.4 while / else

**详细介绍：** 在 Python 中 else 不只与 if 搭配，还可与 while 搭配。`while ... else` 表示：当 while 循环**正常执行完**（中间没有被 break 终止）时，执行 else 后面的语句；若中间被 break 打断，则 else 不执行。

**举例：**

```python
count = 0
while count <= 10:
    print(count)
    count += 1
else:
    print("循环正常执行完了")   # 会执行
```

```python
count = 0
while count <= 10:
    print(count)
    if count == 7:
        break                # 被break打断
    count += 1
else:
    print("循环正常执行完了")   # 不会执行
```

### 7.5 for 循环

**详细介绍：** for 循环也是一种循环，用于遍历序列（字符串、列表、元组、字典、集合）。`for i in xxx:` 会把 xxx 中的每个元素依次赋值给临时变量 `i`。

**举例（遍历字符串/列表）：**

```python
for i in "wolf lab":
    print(i)

names = ["andy", "lois", "jack", "ccie"]
for i in names:
    print(i)
```

### 7.6 range 函数

**详细介绍：** `range(n)` 生成 0 到 n-1 的整数序列；`range(start, end)` 生成 start 到 end-1（顾头不顾尾）。常配合 for 循环。

**举例：**

```python
for i in range(10):
    print(i)      # 0 1 2 ... 9

for i in range(1, 101):
    if i % 2 == 0:
        print(i)  # 0~100 内的偶数（02468...100）
    if i % 2 == 1:
        print(i)  # 奇数（13579...）
```

### 7.7 import 与随机数模块

**详细介绍：** `import random` 可导入系统现成的模块，`random.random()` 或相关函数产生随机数，可用来写猜数字小游戏。

**举例：**

```python
import random
n = random.randint(1, 100)   # 产生 1~100 之间的随机整数
print(n)
```

---

## 8. 流程控制综合举例

### 8.1 复利计算（存多少年翻倍）

**详细介绍：** 用 while 循环实现：10 万本金，年利率 0.0325，复利（每年本息 = 上一年本息 × (1+利率)），计算多少年本息能达到 20 万。

**举例：**

```python
base = 100000        # 本金
interest = 0.0325    # 年利率
year = 0

while base <= 200000:
    year += 1
    base = base + base * interest   # 复利：本息 = 本金 + 本金*利率

print(year, base)    # 22 2002106...
```

### 8.2 猴子吃桃

**详细介绍：** 猴子每天吃桃子总数的一半多一个，第 11 天只剩 1 个桃子。反向推：前一天的桃子数 = (当天数 + 1) × 2。用 while 循环从第 11 天倒推。

**举例：**

```python
n = 1        # 第11天剩1个
day = 11

while day > 1:
    n = (n + 1) * 2   # 前一天 = (当天+1)*2
    day -= 1
    print(day, n)     # 第10天4个 第9天10个 第8天22个...

print("一共", n, "个桃子")   # 第一天 3070 个
```

---

## 9. 字符串常用操作

**详细介绍：** 字符串是**有序、不可变**的，不能像列表那样直接修改其中某个元素；对字符串的任何"修改"实际是重新生成一份新数据。Python 自带大量字符串操作方法，可直接调用。

### 9.1 常用方法一览

**举例：**

```python
name = "wolf lab"
print(name.capitalize())   # "Wolf lab"  首字母大写
print(name.lower())        # "wolf lab"  全部小写
print(name.upper())        # "WOLF LAB"  全部大写
print(name.center(50, "-"))  # 字符串居中，总宽50，两端用-填充
```

**count 统计字符数量：**

```python
s = "welcome to wolf lab"
print(s.count("o"))    # 3  统计 o 的数量
print(s.count("e"))    # 2
```

**endswith 判断结尾（返回布尔值）：**

```python
name = "wolf lab!"
print(name.endswith("lab"))    # False（以感叹号结尾）
print(name.endswith("lab!"))   # True
```

**find 找索引（找不到返回 -1）：**

```python
name = "wolf lab"
print(name.find("t"))    # 8
print(name.find("x"))    # -1（不存在）
```

**format 引用外部变量：**

**详细介绍：** 字符串里的 `{}` 是占位符，用 `.format()` 填入外部变量的值；也可以用命名参数 `{name}` 配合 `format(name=...)`。

```python
s = "welcome {who} to wolf lab, you are number {num}"
print(s.format("老杨", "999"))   # welcome 老杨 to wolf lab, you are number 999

s2 = "welcome {user} to wolf lab, you are number {number} user"
print(s2.format(user="andy", number=1000))
```

**is 系列判断（返回布尔值）：**

```python
info = "wolf lab"
print(info.islower())   # 是否全小写
print(info.isupper())   # 是否全大写
print("wolf".isalpha())   # 是否全为字母
print("123".isdigit())    # 是否全为数字
print(" ".isspace())      # 是否为空格
```

**strip 去空格：**

```python
info = "  wolf lab  "
print(info.lstrip())   # 去左边空格
print(info.rstrip())   # 去右边空格
print(info.strip())    # 去两边空格
```

**split 字符串转列表：**

**详细介绍：** `split(分隔符)` 默认按空格切分，返回列表。常用于把"192.168.1.1,192.168.1.3"这类字符串按逗号切分成列表。

```python
ip = "192.168.1.1,192.168.1.3,192.168.1.4"
print(ip.split(","))   # ['192.168.1.1', '192.168.1.3', '192.168.1.4']
```

**join 列表拼接成字符串：**

```python
ip_list = ["192.168.1.1", "192.168.1.2", "192.168.1.3"]
print(",".join(ip_list))   # 192.168.1.1,192.168.1.2,192.168.1.3
```

**index 与 replace：**

```python
ip = "192.168.1.3"
print(ip.index("3"))   # 找索引

info = "wolf lab"
print(info.replace("wolf", "WOLF"))   # "WOLF lab" 替换
```

### 9.2 综合练习：统计字符、数字、空格、特殊字符个数

**详细介绍：** 综合运用 `isalpha`、`isdigit`、`isspace`、for 循环、格式化输出，统计输入字符串中各类型字符的数量。

**举例：**

```python
msg = input("请输入字符串: ").strip()
str_count = 0      # 字母数
int_count = 0      # 数字数
space_count = 0    # 空格数
special_count = 0  # 特殊字符数

for i in msg:
    if i.isalpha():
        str_count += 1
    elif i.isdigit():
        int_count += 1
    elif i.isspace():
        space_count += 1
    else:
        special_count += 1

print(f"字母数量: {str_count}, 数字数量: {int_count}, 空格数量: {space_count}, 特殊字符数量: {special_count}")
```

### 9.3 综合练习：双色球选购

**详细介绍：** 双色球规则：红球 33 选 6（不重复），蓝球 16 选 1。综合运用输入校验、int 转换、循环、continue、append。

**举例：**

```python
red_balls = []   # 红球列表
blue_ball = []   # 蓝球列表

count = 0
while count < 6:
    choice = input("请输入第%d个红球: " % (count + 1)).strip()
    if not choice.isdigit():          # 不是数字则不合法
        print("输入不合法，请重新输入")
        continue
    choice = int(choice)
    if 0 < choice <= 33 and choice not in red_balls:   # 在1~33且不重复
        red_balls.append(choice)
        count += 1  # 合法才计数+1
    else:
        print("输入不合法，请重新输入")

count = 0
while count < 1:
    choice = input("请输入第1个蓝球: ").strip()
    if not choice.isdigit():
        print("输入不合法，请重新输入")
        continue
    choice = int(choice)
    if 0 < choice <= 16 and choice not in blue_ball:
        blue_ball.append(choice)
        count += 1
    else:
        print("输入不合法，请重新输入")

print("红球:", red_balls)
print("蓝球:", blue_ball)
```

---

## 10. 元组、字典、集合

### 10.1 元组 tuple

**详细介绍：** 元组就是把列表的方括号 `[]` 改成圆括号 `()`，又称**"只读列表"**。特点：

- 可存放多个值；
- **不可变**（元组本身内容不能改）；
- 下标从 0 开始，有序。

**举例：**

```python
scores = (580, 320, 490, 600, 650, 550)
print(scores[0])    # 580
print(scores[2])    # 490

for i in scores:    # 循环
    print(i)

print(len(scores))  # 6  长度
print(700 in scores)   # False  是否包含
print(650 in scores)   # True
```

**元组内元素修改（特殊情况）：** 元组本身不可改，但若元组内嵌套了**列表**（可变类型），则该列表内容可以修改。

```python
scores = (250, 320, 490, [101, 102])   # 元组里套了列表
scores[3][1] = 680    # 修改列表中的元素，可以
print(scores)   # (250, 320, 490, [101, 680])
```

### 10.2 字典 dict

**详细介绍：** 字典是 Python **唯一的映射类型**，格式为**键值对 key: value**。用**花括号** `{}` 括起来，键和值之间用冒号 `:`，项与项之间用逗号 `,`。

字典特点：

- 键值对结构；
- **键（key）必须是不可变数据类型，且必须唯一**；
- 可存放多个任意 value，value 可重复；
- **无序**；
- **查询速度快，且不受字典大小影响**（与哈希相关，见第 11 章）。

**为什么用字典？** 若把公司员工信息存成列表，查某一个人的工资必须从头到尾遍历整个列表，几十万条数据就要遍历几十万次，列表越大越慢，不可取。用字典按 key 查询则极快。

**举例（用列表存员工信息 vs 用字典存）：**

```python
# 用列表（不推荐，查询慢）
message = [
    ["andy", 37, "讲师", 2300],
    ["jack", 34, "研发", 2400],
    ["lois", 26, "前台", 8000],
    ["eda", 18, "公关", 28000],
]
# 查 eda 的工资，需要 for 遍历 + break

# 用字典（推荐）
info = {
    "name": "wolf lab",
    "业务": "网工培训的集散地",
    "评价": "IE认证的黄埔军校",
    "website": "www.wolf-lab.com"
}
print(info)
```

#### 10.2.1 创建字典

```python
message = {
    "andy": [37, "讲师", 2300],
    "jack": [34, "研发", 2400],
}
```

#### 10.2.2 增加

```python
message["eda"] = [20, "公关", 28000]
```

#### 10.2.3 删除

```python
message.pop("andy")     # 删除指定key
message.popitem()       # 随机删除一个key
del message["jack"]     # 删除指定key
message.clear()         # 清空字典
```

#### 10.2.4 修改 / 合并

```python
message["andy"] = [37, "高级讲师", 2500]   # 修改

message2 = {"nova": "实习生"}
message.update(message2)   # 把message2的键值合并进message
```

#### 10.2.5 查询

```python
print(message["eda"])        # 直接查，key不存在会报错
print(message.get("eda"))    # 用get查，更安全
print("eda" in message)      # 判断key是否存在，返回True/False
print(message.keys())        # 所有key
print(message.values())      # 所有value
print(message.items())       # 所有键值对（元组列表）
```

#### 10.2.6 循环字典

```python
for k in message.keys():     # 循环key
    print(k)

for k, v in message.items(): # 循环key和value
    print(k, v)
```

#### 10.2.7 求字典长度

```python
print(len(message))   # 字典项数
```

### 10.3 集合 set

**详细介绍：** 集合也是一种可存一堆数据的数据类型，与列表类似，但有独特特点：

- 集合中的元素**不可变**（不能存列表、字典，但字符串、数字、元组等不可变类型可以）；
- **天生去重**（不能存重复元素）；
- **无序**（无索引，元素无先后之分，集合 {3,4,5} 与 {5,3,4} 是同一个集合）。

基于以上特性，集合主要做两件事：**去重**、**关系运算**。

**举例（去重）：**

```python
lst = [2, 3, "andy", "jack", "andy", 1024]   # andy 出现两次
s = set(lst)          # 转成集合，自动去重
print(s)              # 只有一个 andy
result = list(s)      # 再转回列表
print(result)
```

#### 10.3.1 集合的增删查

```python
info = {1, 2, 3, "andy", "jack", 1024}
info.add(567)            # 增加
info.discard(2)          # 删除存在的值
info.remove("andy")      # 删除
info.pop()               # 随机删除
print("lois" in info)    # 判断是否在集合中
```

#### 10.3.2 集合的关系运算

**详细介绍：** 集合的关系运算包括**交集、并集、差集、对称差集（对等差集）**，以及判断相交/子集/超集关系。

```python
hcip = {"小明", "灰姑娘", "老王2", "andy"}
hcie = {"灰姑娘", "老王2", "jack"}

print(hcip & hcie)      # 交集：既报HCIP又报HCIE → {'灰姑娘','老王2'}
print(hcip | hcie)      # 并集：报了任一课程的所有人
print(hcip - hcie)      # 差集：只报了HCIP的
print(hcip ^ hcie)      # 对称差集：只报了一门课的人
```

**判断集合关系：**

```python
ccna = {"小明", "老王"}
ccnp = {"小明", "老王", "老杨"}
ccie = {"老杨", "小李"}

print(ccnp.isdisjoint(ccie))   # 是否不相交
print(ccna.issubset(ccnp))     # ccna 是否是 ccnp 的子集 → True
print(ccnp.issuperset(ccna))   # ccnp 是否是 ccna 的超集(父集) → True
```

---

## 11. 哈希：为何字典查询快

### 11.1 什么是哈希

**详细介绍：** 哈希（Hash）又称"散列""杂凑"，把**任意长度的输入**通过散列函数算法转换成**固定长度的输出**，该输出值叫散列值/哈希值。

### 11.2 哈希的三大特点

**详细介绍：**

1. **不可逆**：单向过程，不能从哈希值反推原始数据（如 MD5 得到 128 比特字符串，不是加密，无法解密）。
2. **雪崩效应**：原始数据哪怕只有一点点不同，哈希后的结果也毫无相似性。可用于完整性校验。
3. **定长**：无论输入多大（10G 电影 vs 5K 文本），复杂度相同、计算量极小，都能在极短时间内得到结果。

### 11.3 哈希的用途

**详细介绍：**

- **密码存储**：网站数据库不存明文密码，而是存密码的哈希值。登录时把输入的密码做哈希再与库里比对（原始数据相同则哈希结果相同）。
- **完整性校验**：发送文件前先对文件做哈希得到 A，把文件连同 A 发给对端；对端收到后再做哈希得到 B，比较 A 与 B 是否一致，判断文件是否被篡改。
- **数字签名**：结合非对称加密（公钥/私钥），发送方用自己的私钥加密哈希值，接收方用发送方公钥解密，能验证"文件一定是发送方发出的，而非他人冒充"（实现来源认证）。

### 11.4 基于哈希的数据类型：字典与集合

**详细介绍：** Python 中基于哈希的数据类型有两个：**字典**和**集合**。

**举例（用 hash() 查看哈希值）：**

```python
print(hash("wolf lab"))     # 某哈希值
print(hash("wolf lab2"))    # 完全不同的哈希值
```

### 11.5 为什么字典查询速度快？

**详细介绍：** 字典会对每一个 key 先做哈希，生成**固定长度的哈希值**，再针对这些哈希值**按大小排序**，放进一个有序列表里。因为列表是有序的，查询时先对目标 key 做哈希，再用**二分法**查找，每次排除一半，所以极快，且基本不受字典大小影响。

**举例（二分法直觉）：** 0~100 里查一个数，有序时第一次取 50 排除一半，第二次 25 再排除一半…… 2 的 7 次方是 128，最多 7 次必定查出。14 亿人的身份证号做哈希排序后，用二分法最多 31 次就可查出，而不需要从头遍历 14 亿次。

### 11.6 为什么集合天生去重？

**详细介绍：** 集合中每存入一个值都会先做哈希，算出它该存放的位置；存之前检查该位置上是否已有相同哈希值，若相同则不再存储（即去重），不相同才存进去。

---

## 12. 字符编码

**详细介绍：** 计算机显示各种文字符号的基石是编码表。早期美国发明计算机，先把英文字符编入编码表。

### 12.1 ASCII 码

**详细介绍：** ASCII（American Standard Code for Information Interchange，美国信息交换标准代码）基于拉丁字母的电脑编码系统，是最通用的单字节编码系统，用**1 个字节（8 比特位）**编码一个字符。最早 127 个字符，后扩展为 256 个。

**举例：**

```python
print(ord("A"))    # 65   大写A的ASCII码
print(ord("a"))    # 97   小写a的ASCII码
print(ord("!"))    # 33   感叹号
```

> 每 8 个比特位表示一个字符，"断句"很重要——否则无法分清哪 8 位是一个字符。

### 12.2 GB2312 / GBK（中文编码）

**详细介绍：**

- ASCII 只能存 255 个字符，而常用汉字有几千个，无法支持中文，于是中国设计了 **GB2312**（1980 年发布，存 6763 个汉字，用 2 个字节表示字符，兼容 ASCII）。
- 随着电脑普及，生僻字打不出来，1995 年升级扩展出 **GBK**（GB2312 扩展字符集），加进了藏语、维吾尔语、日语、韩语等，支持 2 万多个汉字，用 2 个字节表示字符。Windows 中文版至今默认 GBK。

### 12.3 Unicode（万国码）

**详细介绍：** 全世界语言几百种，各国各用各的编码会导致乱码。为此推出 **Unicode（万国码）**：把所有语言统一到一套编码里。特点：

- 支持全球所有语言，收录 113 万+ 字符（还在扩张）；
- 用 2~4 个字节表示字符；
- 可与各种语言自由转换（如 GBK ↔ unicode），因为是"一统天下"的对应关系。

**问题：** 若所有文本都用 unicode，纯英文文本比 ASCII 多至少一倍存储空间（2~4 字节 vs 1 字节），存储和网络传输会翻倍，无法容忍（内存里做运算无所谓，但写硬盘、传网络就成问题）。

### 12.4 UTF-8（可变长编码）

**详细介绍：** 为解决 unicode 存储/传输浪费空间的问题，出现了 **UTF（Unicode Transformation Format，即对 unicode 字符进行转换）**，在存储/网络传输时节省空间。

- UTF-8：变长编码，用 1~4 个字节表示字符，优先 1 字节。英文 1 字节、欧洲语系 2 字节、东亚（含中文）3 字节、其他 4 字节。**这是我们最常用的编码**。
- UTF-16：用 2 或 4 字节，优先 2 字节。
- UTF-32：固定 4 字节表示所有字符。

UTF-8 的额外好处：ASCII 编码可看作 UTF-8 的一部分（英文仍 1 字节）。

### 12.5 现代计算机的字符编码工作方式

**详细介绍：** 总结编码体系：

| 年代 | 编码 | 说明 |
|------|------|------|
| 1967 | ASCII | 1字节/8比特，支持英语和西欧语言 |
| 1980 | GB2312 | 兼容ASCII，2字节表示字符，6763汉字 |
| 1991 | Unicode | 国际标准，统一字符编码（万国码） |
| — | GBK | GB2312扩展，支持繁体字 |
| — | UTF-8 | 不定长编码，1~3字节（英文1、欧洲2、中文3） |

**核心规则：** 计算机**内存中统一使用 unicode** 编码做运算；当需要保存到硬盘或网络传输时，转换为 **UTF-8** 编码以节省空间。

Python 2.7 之前默认用 ASCII（只支持英文，其他语言需单独配置）；**Python 3 默认编码改为 unicode，文件存储编码为 UTF-8**，无需任何声明即可写出各种语言。

---

## 13. 文件操作

**详细介绍：** 文件操作用于创建、打开、读写文件。在后续自动化运维中（如把设备配置备份成 txt 文件）会用到。

### 13.1 打开文件的模式

**详细介绍：** `open(路径, mode="模式")` 的常用模式参数：

| 模式 | 含义 | 注意 |
|------|------|------|
| `r` | 只读 | 只能读文件内容 |
| `w` | 创建/写入 | **危险**：若文件已存在，会先清空再写内容 |
| `x` | 创建 | 只创建新文件，若文件已存在则报错 |
| `a` | 追加 | 在文件已有内容末尾追加 |
| `b` | 二进制模式 | 处理语音、视频等非文本文件 |
| `t` | 文本模式 | 默认模式 |
| `r+` 等 | 读写 | 加号表示同时读写 |

`encoding` 参数一般可不写，默认 UTF-8。

### 13.2 创建并写文件（w）

**举例：**

```python
f = open("D:/wolf-lab/wolf.txt", mode="w")   # w模式创建文件
f.write("老王 CCIE 13800 IT manager\n")
f.write("老崔 HCIE 16800 network\n")
f.write("老杨 CCIE 19800 SIT\n")   # \n 是转义符，表示回车换行
f.close()
```

> `\n` 是转义字符，表示换行，不是普通的字母 n。

### 13.3 追加文件（a）

**举例：**

```python
f = open("D:/wolf-lab/wolf.txt", mode="a")   # a 追加模式
f.write("\n老李 CCNP 14800 software\n")
f.close()
```

### 13.4 读取文件（r）

**详细介绍：** 三种读法：

- `readline()`：从光标所在位置读取**一行**；
- `read()`：读取**整个文件**所有内容；
- `readlines()`：读取全部内容并存到**列表**里（每行一个元素）。

**举例：**

```python
f = open("D:/wolf-lab/wolf.txt", mode="r")
print(f.readline())     # 读取一行
print(f.read())         # 读取全部内容
print(f.readlines())    # 读取为列表，每行一个元素
f.close()
```

### 13.5 循环文件

**详细介绍：** 用 `for line in f:` 逐行遍历文件，也可把每行 split 转成列表。

**举例：**

```python
f = open("D:/wolf-lab/wolf.txt", mode="r")
for line in f:
    print(line)              # 逐行打印
f.close()

# 每行转成列表
f = open("D:/wolf-lab/wolf.txt", mode="r")
for line in f:
    line_list = line.split()
    print(line_list)   # ['老王', 'CCIE', '13800', 'IT', 'manager'] ...
f.close()
```

### 13.6 按条件筛选文件内容

**详细介绍：** 结合循环与条件，从文件中筛选想要的数据。注意从文件读出的是**字符串**，与数字比较前要用 `int()` 转换。

**举例（筛选工资大于 16000 的人）：**

```python
f = open("D:/wolf-lab/wolf.txt", mode="r")
for line in f:
    line_list = line.split()     # 转成列表，如 ['老王','CCIE','13800','IT']
    salary = int(line_list[2])   # 第3项是工资，转成int
    if salary > 16000:
        print(line, end="")
f.close()
```

输出工资超过 16000 的行（如老王 19800）。

---

## 课程总结

本课程是"网络工程师的 Python 之路"系列基础部分，核心主线：

1. 理解编程的**本质**（让机器按指令执行）与 Python 作为**解释型高级语言**的定位；
2. 掌握**变量、数据类型**（数字/字符串/布尔/列表/元组/字典/集合）及常用操作；
3. 掌握**运算符**与**格式化输出**、`input` 用户输入；
4. 掌握**流程控制**（if 分支 + while/for 循环 + break/continue + 缩进语法）；
5. 理解**哈希**原理（字典为什么快、集合为什么天生去重）；
6. 理解**字符编码**演进（ASCII → GB2312/GBK → Unicode → UTF-8）；
7. 掌握**文件操作**（读写/追加/循环/筛选）。

后续将进入**网络自动化运维实战**：使用 Python 登录到网络设备（Telnet/SSH）、执行配置操作、对海量设备做周期性备份。