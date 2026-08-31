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


# Python 网络自动化笔记

> 来源：WOLF 实验室《Python 网络自动化》系列教程（第 11 ~ 20 课）
> 内容涵盖：函数、模块、正则表达式、SMTP 发邮件、Telnet 登录网络设备与自动化综合实战。

---

## 目录

1. [函数及其参数](#1-函数及其参数)
2. [函数的返回值与作用域](#2-函数的返回值与作用域)
3. [函数嵌套、高阶函数、递归](#3-函数嵌套高阶函数递归)
4. [内置模块](#4-内置模块)
5. [正则表达式 re 模块](#5-正则表达式-re-模块)
6. [模块的导入与调用](#6-模块的导入与调用)
7. [SMTP 发送邮件](#7-smtp-发送邮件)
8. [Telnet 登录网络设备](#8-telnet-登录网络设备)
9. [综合实战：备份设备配置并发到指定邮箱](#9-综合实战备份设备配置并发到指定邮箱)

---

## 1. 函数及其参数

### 1.1 为什么需要函数？

**场景**：老板让你写一个监控程序，24 小时全年无休地监控公司网络设备的系统状况。当 CPU 使用率超过 90%、内存大于 80%、硬盘使用空间大于 90% 时，都要自动发送邮件报警。

如果不用函数，代码会写成这样：

```python
while True:  # 死循环，全年无休监控
    if cpu_usage > 90:
        # 连接邮箱服务器
        # 发送邮件
        # 关闭连接
        pass
    if disk_usage > 90:
        # 连接邮箱服务器
        # 发送邮件
        # 关闭连接
        pass
    if memory_usage > 80:
        # 连接邮箱服务器
        # 发送邮件
        # 关闭连接
        pass
```

这种写法存在 **两大问题**：

1. **重复代码太多**：每一次报警都要重写一遍发邮件代码，只能不停地复制粘贴，不符合可扩展性与可维护性。
2. **修改困难**：如果日后要加入"群发"功能，所有用到这段发邮件代码的地方都要逐一修改。

**解决思路**：把重复的代码提取出来，放在一个公共的地方，起个名字，谁想用就直接调用。

```python
def send_mail():
    """发送邮件报警的函数"""
    # 连接邮箱服务器
    # 发送邮件
    # 关闭连接
    pass

while True:
    if cpu_usage > 90:
        send_mail()      # 直接调用
    if disk_usage > 90:
        send_mail()
    if memory_usage > 80:
        send_mail()
```

这样既减少了重复代码量，又使程序变得**可扩展、可维护**——增加功能时只需要修改 `send_mail` 这一处，所有调用点会自动生效。

### 1.2 函数的概念

- 函数（function）这个名字来源于数学，但编程中的函数与数学中的函数有很大不同。
- 在不同语言中函数有不同的叫法：Basic 里叫过程/子程序，C 语言叫 function，Java 叫 method，Python 里就叫**函数**。
- **函数**：将一组语句的集合通过一个名字（函数名）封装起来。想要执行这段代码，只需要调用函数名即可。

函数的三大特性：
1. **减少重复代码**
2. **使程序变得可扩展**
3. **使程序变得可维护**

### 1.3 定义和调用函数

语法：使用 `def`（define 的缩写，"定义"的意思）关键字，函数名后加括号，以冒号结尾，函数体缩进。

```python
def say_hi():
    print("hello, welcome to WOLF lab")

# 调用函数
say_hi()
say_hi()   # 可以多次调用
```

> 定义好函数后，在编辑器里输入函数名前几个字母就能 Tab 自动补全，就像敲命令行一样。

### 1.4 带参数的函数

如果代码写死（如固定计算 `2 ** 6`），算 2 的 7 次方、3 的 10 次方都得重新写。用函数加参数就灵活多了：

```python
def calc(x, y):
    result = x ** y   # x 的 y 次方
    return result

c = calc(2, 6)        # 2 的 6 次方 = 64
print(c)              # 64

print(calc(2, 10))    # 1024
print(calc(2, 32))    # 4294967296
print(calc(3, 10))    # 59049
```

调用时把实际值（实参）传给函数定义中的形参，即可灵活计算任意底数和指数。

### 1.5 形参与实参

- **形参（形式参数）**：函数定义时括号里的变量，如上例中的 `x`、`y`。
- **实参（实际参数）**：函数调用时实际传入的值，如上例中的 `2` 和 `8`。

```python
def calc(x, y):     # x、y 是形参
    return x ** y

result = calc(2, 8)  # 2、8 是实参，2 传给 x，8 传给 y
print(result)        # 256
```

要点：
- 实参可以是常量、变量、表达式，甚至是函数。
- 无论实参是什么类型，调用函数时都必须有**确定的值**，才能把这些值传给形参。
- 因此调用前需要预先给实参赋值。

### 1.6 默认参数

对于大多数情况都相同的参数，可以给它一个默认值，这样调用时就不用每次都传。

```python
def student_register(name, age, country, course):
    print("WOLF lab 学员信息")
    print("姓名:", name)
    print("年龄:", age)
    print("国籍:", country)
    print("课程:", course)

# 每次都要传 4 个参数
student_register("张三", 22, "CN", "HCIE")
student_register("李四", 21, "CN", "HCIE")
student_register("王五", 23, "CN", "HCIP")
```

国籍这一栏几乎都是中国（CN），可以用默认参数简化：

```python
def student_register(name, age, course, country="CN"):
    print("姓名:", name, "年龄:", age, "课程:", course, "国籍:", country)

student_register("张三", 22, "HCIE")      # country 默认为 CN
student_register("李四", 21, "HCIE")
student_register("王五", 23, "HCIP")
```

**规则：默认参数必须写在参数列表的最后。**（如果前面写默认参数、后面写必选参数，会语法报错。）

### 1.7 关键参数（关键字参数）

正常情况下传参要按顺序。如果不想按顺序，可以用**关键参数**——直接指定参数名。

```python
def student_register(name, age, course, country="CN"):
    print(name, age, course, country)

# 用关键参数，可以不按顺序
student_register(course="HCIA", age=35, name="赵六")
```

**规则**：
- 指定了参数名的参数就是关键参数。
- **关键参数必须放在位置参数之后**（位置参数优先于关键参数）。
- 如果默认参数被明确指定了值，以指定的值为准。

```python
# 错误：位置参数写在关键参数之后会报错
# student_register(course="HCIA", 35)   # SyntaxError
```

### 1.8 非固定参数 `*args`

当不确定用户会传入多少个参数时，用 `*args` 接收，多余的参数会被打包成一个**元组**。

```python
def student_register(name, age, *args):
    print("姓名:", name, "年龄:", age)
    print("其他信息(元组):", args)

student_register("张三", 22)                    # args = ()
student_register("张三", 22, "CCIE")            # args = ('CCIE',)
student_register("李四", 25, "日本", "CCNA", "CCNP", "CCIE")
# args = ('日本', 'CCNA', 'CCNP', 'CCIE')
```

> `*args` 里的 args 是 arguments（参数）的缩写，传入的额外参数会以**元组**形式存放。

### 1.9 非固定参数 `**kwargs`

`**kwargs` 接收**带名字**的多余参数（形如 `key=value`），打包成一个**字典**。

```python
def student_register(name, age, *args, **kwargs):
    print("姓名:", name, "年龄:", age)
    print("args(元组):", args)
    print("kwargs(字典):", kwargs)

# 只有 name、age 时，元组和字典都是空的
student_register("张三", 22)
# args: ()  kwargs: {}

# 传位置参数进元组，传 key=value 进字典
student_register("李四", 23, "CN", "上海", gender="男", course="CCIE")
# args: ('CN', '上海')
# kwargs: {'gender': '男', 'course': 'CCIE'}
```

**总结对比**：

| 参数类型 | 写法 | 存储形式 | 特点 |
|---------|------|---------|------|
| 位置参数 | `name` | 单个值 | 按顺序传 |
| 默认参数 | `country="CN"` | 单个值 | 写在参数最后 |
| 关键参数 | `course="HCIE"` | 单个值 | 指定参数名传 |
| 非固定位置参数 | `*args` | 元组 | 多余的位置参数 |
| 非固定关键字参数 | `**kwargs` | 字典 | 多余的 key=value 参数 |

---

## 2. 函数的返回值与作用域

### 2.1 return 返回值

一个函数执行完成后，只要遇到 `return` 语句，就**立即停止执行并返回结果**。

- `return` 代表函数结束。
- 遇到 `return`，函数中后续代码不会被执行。
- 如果函数中没有 `return`，函数返回空（`None`）。
- 可以返回**任意类型**的数据，也可以返回**多个值**。

### 2.2 返回布尔值（True/False）

结合前面学员注册的例子，加一个年龄判断，返回注册是否成功：

```python
def register(name, age, country, course):
    if age > 18:
        return True      # 满 18 岁，注册成功
    else:
        return False     # 未满 18 岁，注册失败

# 接收返回值
status = register("张三", 32, "CN", "CCIE")
if status:
    print("注册成功")
else:
    print("未满18岁，注册失败")

# 输出：注册成功
print(register("李四", 12, "CN", "CCNP"))
# False -> "未满18岁，注册失败"
```

调用函数会得到一个结果，通过返回值可以把这个结果拿到外面继续使用。

### 2.3 实战：判断 IP 地址是否合法

编写函数判断一个 IPv4 地址是否合法（点分十进制，范围 0.0.0.0 ~ 255.255.255.255，共四段）。

```python
def is_valid_ip(ip_address):
    # 1. 用 split 去掉点，分成长度为 4 的列表
    ip = ip_address.split('.')
    # 2. 长度必须是 4，否则一定不是合法 IP
    if len(ip) == 4:
        for i in range(4):
            # 每一段必须是数字，且 0 <= 值 <= 255
            if not ip[i].isdigit() or int(ip[i]) > 255 or int(ip[i]) < 0:
                print(ip_address, "不是合法的 IP 地址")
                return
        print(ip_address, "是合法的 IP 地址")
    else:
        print(ip_address, "不是合法的 IP 地址")

is_valid_ip(input("请输入 IP 地址: "))
```

**逻辑讲解**（以 `192.168.1.1` 为例）：
1. `split('.')` 把 `192.168.1.1` 拆成列表 `['192', '168', '1', '1']`。
2. 判断长度为 4 才继续，否则直接判定非法。
3. `for i in range(4)` 循环 4 次，逐段检查：是不是数字（`isdigit()`）、是否大于 255、是否小于 0。
4. 只要有一段不满足，就打印非法并 `return`（提前结束）。
5. 4 段全部合法才判定为合法 IP。

测试：
- `192.168.1.1` → 合法
- `192.168.1.1.2` → 五段，非法
- `300.300.1.1` → 超范围，非法
- `1.300.1.1` → 超范围，非法

### 2.4 变量作用域：全局变量与局部变量

```python
name = "WOLF"                 # 全局变量（程序一开始就定义）

def change_name():
    name = "WOLF CCIE/HCIE 行业领导者"   # 函数内部的局部变量
    print("after change:", name)

change_name()
print("外面看:", name)
```

输出：
```
after change: WOLF CCIE/HCIE 行业领导者
外面看: WOLF
```

**结论**：
- **局部变量**：在函数体中定义的变量，只在定义它的那个函数内有效。
- **全局变量**：程序一开始（函数外）定义的变量，作用域是整个程序。
- **变量的查找顺序**：局部变量优先于全局变量。
- 当全局变量与局部变量同名时，在定义局部变量的函数内，局部变量起作用；其他地方全局变量起作用。
- **在函数内部不能直接修改全局变量**（这就是为什么外面打印的 name 没变）。

### 2.5 global 关键字

如果想在函数内部修改全局变量，需要先用 `global` 声明。

```python
name = "WOLF"

def change_name():
    global name       # 声明 name 是全局变量
    name = "WOLF CCIE/HCIE 行业领导者"

change_name()
print("外面看:", name)
# 输出：外面看: WOLF CCIE/HCIE 行业领导者
```

加上 `global name` 声明后，函数内部对 `name` 的修改就会作用到全局变量上。

---

## 3. 函数嵌套、高阶函数、递归

### 3.1 函数的嵌套

函数里面套函数，就是函数嵌套。内层函数和外层函数的变量互相独立，变量查找顺序从当前层依次向上找。

```python
name = "WOLF"

def change_name():
    name = "WOLF lab CCIE/HCIE 认证培训基地"

    def change_name2():                    # 嵌套的内层函数
        name = "WOLF lab CCIE/HCIE 认证培训基地，不要钱"
        print("第3层打印:", name)

    change_name2()                          # 调用内层函数
    print("第2层打印:", name)

change_name()
print("最外层打印:", name)
```

输出：
```
第3层打印: WOLF lab CCIE/HCIE 认证培训基地，不要钱
第2层打印: WOLF lab CCIE/HCIE 认证培训基地
最外层打印: WOLF
```

**要点**：每个函数里的变量互相独立；变量查找顺序从当前层次依次往上找（第 3 层找不到就到第 2 层，再到最外层）。

### 3.2 高阶函数

变量可以指向函数，函数的参数可以接收变量，因此函数可以接收**另一个函数作为参数**。这种函数就是高阶函数。

```python
# 求绝对值函数
def get_abs(n):
    if n < 0:
        return -n
    return n

# 求两数绝对值之和（高阶函数：把 get_abs 作为参数传入）
def add_abs(fx, fy, x, y):
    return fx(x) + fy(y)

print(add_abs(get_abs, get_abs, 3, -6))
# get_abs(3) + get_abs(-6) = 3 + 6 = 9
```

这里 `add_abs` 接收了函数 `get_abs` 作为参数，这就是**高阶函数**。

### 3.3 递归函数

在函数内部不断调用自身，就是递归函数。

**需求**：把 100 不断除以 2 取整，直到商为 0，打印每次的商。

用循环实现：

```python
n = 100
while n > 0:
    n = int(n / 2)   # 除以 2 并取整
    print(n)
# 输出：50 25 12 6 3 1
```

用递归函数实现：

```python
def calc(n):
    n = n // 2
    print(n)
    if n > 0:          # 结束条件
        calc(n)        # 调用自己，递归

calc(100)
# 输出：50 25 12 6 3 1 0
```

### 3.4 递归的注意事项

1. **必须有明确的结束条件**：如上例的 `n > 0`。如果没有结束条件，会陷入无限递归，最终报错。
2. **每次递归问题规模要有所减少**：如上例中 `n` 每次除以 2。
3. **递归效率不高**：层次过多（超过约 1000 层）会导致**栈溢出**。

原理：计算机中函数调用通过**栈**实现，每进入一次函数调用，栈就增加一层帧；每次函数返回，栈就减少一层帧。栈的大小是有限的，所以递归调用次数过多会栈溢出。

```python
# 错误示范：没有结束条件，会导致递归黑洞、栈溢出
def calc(n):
    n = n // 2
    print(n)
    calc(n)     # 缺少结束条件！

calc(100)  # 会一直递归下去，最终 RecursionError
```

---

## 4. 内置模块

### 4.1 什么是模块？

程序越写越多，一个 .py 文件里几万行代码很难维护。为了可维护性，通常把代码分组，分别放在不同的文件里，每个文件完成一定功能。

- **模块**：一个 `.py` 文件就是一个模块，文件名（不含 `.py` 后缀）即为模块名。
- 模块可以理解为"工具包"。
- 通过 `import` 语句导入模块。

**使用模块的好处**：
1. 大大提高代码可维护性，不必从零开始维护。
2. 避免函数名和变量名的冲突（每个模块有独立的命名空间）。
3. 方便多人协作（每个人完成一个模块）。

**Python 模块分三种**：

| 类型 | 说明 | 例子 |
|------|------|------|
| 内置标准模块 | Python 自带，300 多个 | `os`、`time`、`re` |
| 第三方开源模块 | 需联网安装 | `paramiko`、`netmiko` |
| 自定义模块 | 自己创建的 .py 文件 | 自己写的模块 |

### 4.2 OS 模块

`os` 模块用于访问操作系统功能，提供程序和操作系统交互的能力（获取平台信息、目录操作等）。

```python
import os

print(os.name)          # 返回当前工作平台，Windows 显示 nt，Linux 显示 posix
print(os.getcwd())      # 返回当前工作目录（当前脚本所在路径）
print(os.listdir())     # 返回当前目录下所有文件和目录名（列表形式）
os.remove("test2.py")   # 删除指定文件
```

运行示例：
```
nt
C:\python2023
['day1.py', 'day2.py', 'day3.py', ...]
```

#### os.system 执行系统命令

`os.system()` 可以执行系统命令（如 ping），返回值 0 表示成功，非 0 表示失败。

```python
import os

hostname = "www.wolf-lab.com"
response = os.system("ping " + hostname)

if response == 0:
    print(hostname, "is reachable")     # 可达
else:
    print(hostname, "is not reachable") # 不可达
```

> `os.system` 的返回值：0 表示命令成功执行（可达），非 0 表示失败（不可达）。

### 4.3 time 模块

在代码中需要跟时间打交道时使用，如记录日志（日志必须有时间戳才有意义）、时间转换、时间运算。

#### Python 中表示时间的几种方式

1. **时间戳**：从 1970 年 1 月 1 日 0 时 0 分 0 秒开始，按秒计算的偏移量，一直在递增，方便做运算。
2. **格式化字符串**：如 `2023-07-14 20:33:25`。
3. **结构化时间（元组）**：9 个元素——年、月、日、时、分、秒、周几、一年中第几天、是否为夏令时。

```python
import time

print(time.time())            # 返回时间戳（1970-01-01 至今的秒数）
print(time.localtime())       # 返回当前时间的元组（结构化时间）
print(time.localtime(3600))   # 时间戳转元组：1970-01-01 09:00:00（东八区）
# time.struct_time(tm_year=1970, tm_mon=1, tm_mday=1, tm_hour=9, tm_min=0, tm_sec=0, tm_wday=3, tm_yday=1, tm_isdst=0)

# 格式化输出时间
print(time.strftime("%Y-%m-%d %H:%M:%S"))   # 2023-07-14 20:33:25
print(time.strftime("%Y/%m/%d %H:%M:%S"))   # 2023/07/14 20:33:25
print(time.asctime())                        # Fri Jul 14 20:34:31 2023
```

#### 时间格式化符号

| 符号 | 含义 |
|------|------|
| `%Y` | 年（四位） |
| `%m` | 月（小写） |
| `%d` | 日 |
| `%H` | 时（24 小时制） |
| `%M` | 分（大写 M，注意区分） |
| `%S` | 秒 |

> 注意大小写：`%m` 是月，`%M` 是分钟。

#### time.sleep 延时

让程序在运行过程中暂停（休息）一段时间。

```python
import time

print("开始")
time.sleep(10)      # 暂停 10 秒
print("10 秒后才会打印")

# 配合 for 循环，每次打印后休息 2 秒
for i in range(4):
    print(i)
    time.sleep(2)
```

在后续登录网络设备刷配置时，因为脚本执行速度远快于设备响应速度，需要用 `time.sleep` 让程序"缓一缓"，否则会丢配置。

### 4.4 datetime 模块

`datetime` 模块接口更直观、更容易调用。

```python
import datetime

now = datetime.datetime.now()      # 当前时间
print(now)                          # 2023-07-14 20:39:43.xxxxx
print(now.strftime("%Y-%m-%d %H:%M"))        # 2023-07-14 20:40
print(now.strftime("%Y-%m-%d %H:%M:%S"))     # 2023-07-14 20:40:58
print(now.strftime("%Y/%m/%d %H:%M:%S"))     # 2023/07/14 20:41:21
```

#### 时间运算（timedelta）

```python
import datetime

# 30 天以后
day = datetime.date.today() + datetime.timedelta(30)
print(day)   # 2023-08-13

# 100 天以后
print(datetime.date.today() + datetime.timedelta(100))   # 2023-10-22

# 180 天之前
print(datetime.date.today() - datetime.timedelta(180))   # 2023-01-15
```

### 4.5 ipaddress 模块

用于 IP 地址的扫描、计算、判断。

```python
import ipaddress

# 计算 192.168.1.0/27 网段内的所有 IP 地址
net = ipaddress.ip_network("192.168.1.0/27")
for ip in net:
    print(ip)
# 192.168.1.0 ... 192.168.1.31

# 统计网段内 IP 地址数量（含网络号和广播地址）
net = ipaddress.ip_network("192.168.1.0/26")
print(net.num_addresses)   # 64

# 打印网络号和广播地址
print(net[0])              # 192.168.1.0  （主机位全 0，网络号）
print(net[-1])             # 192.168.1.63 （主机位全 1，广播地址）

# 判断某个 IP 是否属于该网络
a = ipaddress.ip_address("192.168.1.50")
print(a in net)            # True

b = ipaddress.ip_address("192.168.1.150")
print(b in net)            # False
```

> 以 /26 为例，前 26 位是网络位，后 6 位是主机位，2 的 6 次方 = 64 个地址，第一个是网络号，最后一个是广播地址。

### 4.6 random 模块

网络中很多地方需要随机数，如登录网站的随机验证码。

```python
import random

print(random.randint(1, 100))    # 生成 1~100 的随机整数（含两端）
print(random.randrange(0, 100, 2))  # 生成 0~100 的随机偶数（步长为 2）
print(random.random())           # 生成 0~1 的随机浮点数

# 从给定字符中随机返回一个
print(random.choice("abcdef123456"))

# 从给定字符中随机返回 3 个
print(random.sample("abcdef123456", 3))
```

#### 生成随机验证码

配合 `string` 模块生成数字和大小写字母，再从中随机取 5 个组成验证码：

```python
import random
import string

print(string.digits)          # 0123456789
print(string.ascii_lowercase) # abcdefghijklmnopqrstuvwxyz
print(string.ascii_uppercase) # ABCDEFGHIJKLMNOPQRSTUVWXYZ

# 所有数字 + 小写字母 + 大写字母
chars = string.digits + string.ascii_lowercase + string.ascii_uppercase

# 随机取 5 个（返回列表），用 join 拼成字符串
code = "".join(random.sample(chars, 5))
print(code)   # 每次都不一样，如 'a8B3k'
```

> `"".join(列表)` 把列表拼接成字符串。

### 4.7 sys 模块

用于获取脚本参数、处理模块搜索路径、查找内建模块等（网络工程师用得不多）。

```python
import sys

print(sys.platform)      # 当前操作系统平台，如 win32
print(sys.version)       # 当前 Python 解释器版本，如 3.10.5
print(sys.modules)       # 当前系统加载的模块

# 判断某个模块是否被加载
import random
print('random' in sys.modules)   # True
```

---

## 5. 正则表达式 re 模块

### 5.1 正则表达式概念

正则表达式（Regular Expression，RE）是对字符串（包括普通字符和特殊字符）操作的一种逻辑公式。用事先定义好的特殊字符及其组合，组成一个"规则字符串"，用来表达对字符串的过滤逻辑。

**场景**：设备上 `show running-config`、`show mac address-table` 的过滤，或者从几十万条日志中快速筛选出想要的信息（如某个 IP 地址是否出现、OSPF/BGP 邻居是否翻动），正则表达式非常高效。

> 注意：Python 中的正则表达式与 BGP 中的正则表达式（匹配 AS-Path）语法不同，不要混淆。

### 5.2 re 模块常用方法

| 方法 | 说明 |
|------|------|
| `re.match()` | 从头开始匹配，要求第一个字符就要符合规则，用得不多 |
| `re.search()` | 匹配包含，只要找到一个就不再往下找，用得较多 |
| `re.findall()` | 把所有匹配到的字符存放在列表中返回，用得较多 |
| `re.sub()` | 匹配到字符并做替换（类似 Word 的一键替换） |

### 5.3 示例：从文本中找 IP 地址

```python
import re

text = "服务器的 IP 是 10.10.5.5，网关是 10.10.5.1。"

data_list = re.findall("10.10.5.5", text)
print(data_list)          # ['10.10.5.5']

r = re.search("10.10.5.5", text)
print(r)                  # <re.Match object; ...>
print(r.group())          # 10.10.5.5
```

### 5.4 从文件中匹配 IP 地址

匹配形如 `x.x.x.x` 的结构。IP 地址每段是 1~3 位数字，用 `\d{1,3}` 表示。

```python
import re

f = open(r"D:\test\log.txt", mode="r")   # 读文件
result = f.read()                         # 先把文件内容读出来
f.close()

# 匹配 x.x.x.x 结构的 IP 地址
ip_pattern = r"\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}"
ips = re.findall(ip_pattern, result)
print(ips)
```

> 踩坑提示：要先 `f.read()` 把内容读取出来保存到变量，再对变量做正则匹配；边读边筛选容易出错。

### 5.5 常用元字符

| 元字符 | 说明 |
|--------|------|
| `.` | 匹配除换行符以外的任意字符 |
| `[...]` | 字符集合，匹配方括号内任意一个字符，如 `[0-9]`、`[a-z]` |
| `[^...]` | 匹配不在方括号内的任意一个字符（`^` 表示非） |
| `\d` | 匹配任意一个数字字符，等价 `[0-9]` |
| `\D` | 匹配任意一个非数字字符 |
| `\w` | 匹配字母、下划线、数字中任意一个字符 |
| `\W` | 匹配不在字母、下划线、数字中的任意一个字符 |
| `\s` | 匹配空白字符（空格、制表符、换行等） |
| `\S` | 匹配非空白字符 |
| `^` | 行首匹配（字符串必须以 ^ 后的内容开始） |
| `$` | 行尾匹配 |

```python
import re
print(re.findall(r"[0-9]", "abc123"))       # ['1', '2', '3']
print(re.findall(r"[a-z]", "AbC"))          # ['b']
print(re.findall(r"[^0-9]", "a1b2c3"))      # ['a', 'b', 'c']
print(re.findall(r"\d", "a1b2c3"))          # ['1', '2', '3']
print(re.findall(r"\D", "a1b2c3"))          # ['a', 'b', 'c']
```

### 5.6 限定符

限定符指定某个组件的出现次数。

| 限定符 | 说明 |
|--------|------|
| `*` | 匹配前面的子表达式零次或多次 |
| `+` | 匹配前面的子表达式一次或多次 |
| `?` | 匹配前面的子表达式零次或一次 |
| `{n}` | 匹配确定的 n 次 |
| `{n,m}` | 至少 n 次，最多 m 次 |
| `{n,}` | 至少 n 次 |

示例：

```python
import re
print(re.findall(r"1*", "111a1"))     # 匹配零次或多个 1
print(re.findall(r"x+", "xxxy"))      # 匹配至少一个 x
print(re.findall(r"x?", "xy"))        # 匹配零个或一个 x
print(re.findall(r"\d{1,3}", "192.168.1.1"))
# ['192', '168', '1', '1']  ：每个数字至少 1 次、最多 3 次
```

### 5.7 实战：从日志中搜索关键信息

假设日志文件中可能有 OSPF/BGP 邻居变化的信息（几十万条），快速定位：

```python
import re

f = open(r"D:\test\log.txt", mode="r")
result = f.read()
f.close()

# 查找 OSPF 邻居变化
r1 = re.search(r"OSPF.*change", result)
print(r1)

# 查找 BGP 邻居变化
r2 = re.search(r"BGP.*change", result)
print(r2)
```

- `search` 只要找到一个就不再往下找；`findall` 找到所有。
- `.` 匹配任意字符，`*` 表示零次或多次，`OSPF.*change` 可匹配 "OSPF邻居关系 change"。

---

## 6. 模块的导入与调用

### 6.1 自定义模块

自己创建一个 Python 文件，就相当于创建了一个自定义模块。

例如创建 `test.py`：

```python
# test.py  —— 自定义模块，包含两个函数
def say_hi():
    print("welcome to WOLF lab")

def wolf():
    print("CCIE and HCIE training professional")
```

### 6.2 导入模块的几种方式

#### 方式一：`import 模块名` —— 导入整个模块

```python
import test

test.say_hi()   # welcome to WOLF lab
test.wolf()     # CCIE and HCIE training professional
```

导入整个模块，模块中的所有函数都可使用。

#### 方式二：`from 模块 import 函数` —— 导入指定函数

```python
from test import say_hi

say_hi()   # welcome to WOLF lab
# wolf()   # 报错：NameError，因为没有导入 wolf

from test import wolf
wolf()     # CCIE and HCIE training professional
```

只导入指定的函数，其他函数不可用（因为没导入）。

#### 方式三：`from 模块 import 函数 as 别名` —— 导入并重命名

```python
from test import say_hi as say_hello

say_hello()   # welcome to WOLF lab
```

把 `say_hi` 重命名为 `say_hello` 再使用。

#### 方式四：`from 模块 import *` —— 导入所有函数

```python
from test import *

say_hi()   # welcome to WOLF lab
wolf()     # CCIE and HCIE training professional
```

> 注意：模块文件名不能以纯数字开头（如 `123.py` 不能直接 `import 123`），文件名中可以有数字，但不能以数字开头。

### 6.3 `if __name__ == "__main__":` 的作用

这句话设计的目的是：**既能被其他程序导入，又能独立运行，互相不干扰**。

先创建 `test2.py`：

```python
# test2.py
def calc(a, b):
    return a ** b

if __name__ == "__main__":
    # 只有自己独立运行时才执行
    print(calc(2, 12))   # 4096
```

在另一个文件里导入 `test2`：

```python
# day7.py
from test2 import *

print(calc(2, 10))   # 1024
```

**解释**：
- `test2.py` 自己独立运行时，`__name__` 等于 `"__main__"`，所以会执行 `calc(2, 12)`，打印 4096。
- 被其他文件 `import` 时，那段 `if __name__ == "__main__"` 里的代码**不会执行**，所以不会打印 4096，只执行导入文件里的 `calc(2, 10)` 打印 1024。

即：作为模块被导入时，`__name__ == "__main__"` 内部的代码不会被触发，从而保证"被调用"和"自己运行"互不干扰。

---

## 7. SMTP 发送邮件

### 7.1 SMTP 协议

- SMTP：Simple Mail Transfer Protocol（简单邮件传输协议），用于控制邮件的中转方式。
- **SMTP 只负责发邮件，不负责收邮件**（收邮件用 IMAP/POP3）。
- 默认端口 25；使用 SSL 加密时端口为 465 或 587。
- 发邮件流程：发送方先登录邮件服务器 → 构建符合协议规则的邮件内容 → 发送；对端通过 IMAP 收取。

### 7.2 Python 发邮件用到两个内置模块

| 模块 | 作用 |
|------|------|
| `smtplib` | 负责发送邮件，对 SMTP 协议简单封装 |
| `email` | 负责构建邮件内容（正文、头部、附件） |

### 7.3 发送纯文本邮件

```python
import smtplib
from email.mime.text import MIMEText      # 构建邮件正文
from email.header import Header           # 构建邮件头部

# 1. 登录邮件服务器（以 QQ 邮箱为例，使用 SSL 加密）
smtp_obj = smtplib.SMTP_SSL("smtp.qq.com", 465)
smtp_obj.login("757984305@qq.com", "授权码")   # 授权码不是邮箱密码
smtp_obj.set_debuglevel(1)                  # 开启调试信息

# 2. 构建邮件正文
msg = MIMEText("欢迎加入 WOLF lab 网络技术实验室", "plain", "utf-8")

# 3. 设置邮件头部：发件人、收件人、主题
msg["From"] = Header("WOLF 班主任", "utf-8")
msg["To"] = Header("CCIE/HCIE VIP 学员", "utf-8")
msg["Subject"] = Header("WOLF lab CCIE/HCIE 直通车课程", "utf-8")

# 4. 发送邮件
smtp_obj.sendmail("757984305@qq.com", "接收者@qq.com", msg.as_string())
```

**要点**：
- QQ 邮箱发送服务器是 `smtp.qq.com`，使用 SSL 时端口 465（或 587）。
- 登录用的**授权码**不是 QQ 密码，需在 QQ 邮箱「设置 → 账号 → SMTP 服务 → 生成授权码」中获取。
- `From`/`To`/`Subject` 通过 `Header` 构建，编码格式 `utf-8`。

### 7.4 发送 HTML 格式邮件

把正文换成 HTML，让邮件支持超链接、排版：

```python
mail_body = """
<h5>hello 小哥哥</h5>
<p>WOLF lab 实验室 CCIE/HCIE 直通车，从零基础开始培训</p>
<p><a href="https://www.wolf-lab.com">点击进入 WOLF lab 官网</a></p>
"""

msg = MIMEText(mail_body, "html", "utf-8")   # 注意第二个参数是 html
msg["From"] = Header("WOLF 班主任", "utf-8")
msg["To"] = Header("CCIE/HCIE VIP 学员", "utf-8")
msg["Subject"] = Header("WOLF lab CCIE/HCIE 直通车课程", "utf-8")

smtp_obj.sendmail("757984305@qq.com", "接收者@qq.com", msg.as_string())
```

关键是 `MIMEText` 的第二个参数传 `"html"`，正文里的 `<a>` 标签就会变成可点击的超链接。

### 7.5 发送带附件的邮件

带附件需要导入 `email.mime.multipart` 和 `email.mime.base`：

```python
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart   # 多部件（正文 + 附件）
from email.mime.base import MIMEBase             # 附件对象
from email.header import Header

smtp_obj = smtplib.SMTP_SSL("smtp.qq.com", 465)
smtp_obj.login("757984305@qq.com", "授权码")

# 邮件正文（HTML）
mail_body = "<h5>hello 小哥哥</h5><p>点击进入 WOLF lab 官网</p>"

# 1. 用 MIMEMultipart 标识邮件由多个部分（正文 + 附件）构成
message = MIMEMultipart()

# 2. 添加正文部分
att1 = MIMEText(mail_body, "html", "utf-8")
message.attach(att1)

# 3. 构建附件：定义附件内容类型为二进制流
att2 = MIMEBase("application", "octet-stream")   # 二进制流读文件
fi = open("wolf.txt", "rb")
att2.set_payload(fi.read())
fi.close()

# 4. 激活下载对话框，让用户可下载附件
att2.add_header("Content-Disposition", "attachment", filename=Header("wolf.txt", "utf-8").encode())
message.attach(att2)

# 5. 设置头部并发送
message["From"] = Header("757984305@qq.com", "utf-8")
message["To"] = Header("接收者@qq.com", "utf-8")
message["Subject"] = Header("带附件的邮件", "utf-8")
smtp_obj.sendmail("757984305@qq.com", "接收者@qq.com", message.as_string())
```

**要点**：
- `MIMEMultipart` 表示邮件由多个部分构成（正文 + 附件）。
- `MIMEBase("application", "octet-stream")` 定义附件内容类型，用二进制流编码读取文件。
- `add_header("Content-Disposition", "attachment", ...)` 激活下载对话框，设置附件文件名。
- 把每个部分（正文、附件）用 `attach()` 挂到 message 上。

---

## 8. Telnet 登录网络设备

### 8.1 telnetlib 模块

`telnetlib` 是 Python 内置模块，支持远程登录网络设备（另还有 paramiko 等支持 SSH）。适合批量对多台设备做统一操作（如临时开会创建用户、会后统一删除用户）。

> 注意：Telnet 是明文传输，实际生产中使用不多；Python 3.13 起内置的 `telnetlib` 已被移除，生产环境建议改用 `paramiko`/`netmiko` 走 SSH。本教程仍以 telnetlib 演示基础流程。

### 8.2 基础：登录单台设备并执行命令

以思科设备为例（IP `192.168.7.250`，用户名 `admin`，密码 `wolf`）：

```python
import telnetlib
import time

# 1. 定义三个变量：目标主机、用户名、密码
host = "192.168.7.250"
username = "admin"
password = "wolf"

# 2. 调用 telnetlib.Telnet() 登录设备
tn = telnetlib.Telnet(host)

# 3. 输入用户名和密码（固定格式）
tn.read_until(b"Username: ")
tn.write(username.encode("ascii") + b"\n")

tn.read_until(b"Password: ")
tn.write(password.encode("ascii") + b"\n")

# 4. 输入配置命令
tn.write(b"enable\n")                          # 进入特权模式
tn.write(b"config terminal\n")                 # 进入全局模式
tn.write(b"username user001 password 123456\n") # 创建用户
tn.write(b"end\n")                             # 退出到用户视图

# 5. 延时，等设备响应（脚本速度远快于设备，需等一等）
time.sleep(1)

# 6. 输出结果并关闭连接
print(tn.read_very_eager().decode("ascii"))
tn.close()
```

**要点**：
- `.encode()` 把字符串转成字节（用户名/密码是英文字符，用 `ascii` 编码）。
- `b"\n"` 表示回车（换行）。
- `read_until(b"Username: ")` 等待设备提示符再输入。
- `time.sleep()` 延时很关键，否则脚本会跑在设备响应之前而丢配置。

### 8.3 用函数封装，提高可扩展性

把上一段代码写死的话，只能操作一台设备。封装成函数后传参即可对任意设备操作：

```python
import telnetlib
import time

def run_telnet(host, username, password):
    tn = telnetlib.Telnet(host, port=23, timeout=10)  # 端口默认 23
    tn.read_until(b"Username: ")
    tn.write(username.encode("ascii") + b"\n")
    tn.read_until(b"Password: ")
    tn.write(password.encode("ascii") + b"\n")

    # 登录后要执行的命令
    tn.write(b"config terminal\n")
    time.sleep(0.2)
    tn.write(b"username user001 privilege 15 password 123456\n")
    time.sleep(0.2)
    tn.write(b"end\n")
    time.sleep(0.2)

    print(tn.read_very_eager().decode("ascii"))
    tn.close()

if __name__ == "__main__":
    # 对多台设备执行同样操作
    run_telnet("10.10.1.1", "admin", "wolf")
    run_telnet("10.10.2.2", "admin", "wolf")
    run_telnet("10.10.3.3", "admin", "wolf")
    run_telnet("10.10.4.4", "admin", "wolf")
    run_telnet("10.10.5.5", "admin", "wolf")
```

**要点**：
- 用 `if __name__ == "__main__":` 保护，使该函数既能被导入、又能独立运行。
- 用函数传参（host、username、password），避免硬编码，程序更灵活、可扩展。
- 几百台设备也只需循环调用即可，比逐台手工登录高效得多。

### 8.4 删除用户（处理二次确认）

删除用户时设备会要求二次确认，需要额外补一个回车：

```python
# 删除用户
tn.write(b"config terminal\n")
tn.write(b"no username user001\n")
time.sleep(0.2)
tn.write(b"\n")          # 关键：设备要求二次确认时再敲一个回车
time.sleep(0.2)
tn.write(b"end\n")
```

> 经验：命令敲完后单独 `tn.write(b"\n")` 送一个回车，处理设备的二次确认提示。

---

## 9. 综合实战：备份设备配置并发到指定邮箱

**需求**：登录网络中的多台设备（R1~R5），抓取它们的配置，保存到一个带时间戳的文件，再把该文件作为附件发送到指定邮箱备份。

### 9.1 完整代码

```python
import telnetlib
import time
import datetime
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.mime.base import MIMEBase
from email.header import Header

# ========== 第一部分：备份配置到文件 ==========
print("程序正在备份设备配置，请耐心等待……")
name = input("谁做的备份：")                       # 记录操作者

# 生成带时间戳的文件名
date = datetime.datetime.now().strftime("%Y年%m月%d日_%H时%M分%S秒")
file_name = "WOLF综合实验_" + name + "_" + date + ".txt"

def run_telnet(host, username, password, commands):
    tn = telnetlib.Telnet(host, port=23, timeout=10)
    tn.read_until(b"Username: ")
    tn.write(username.encode("ascii") + b"\n")
    tn.read_until(b"Password: ")
    tn.write(password.encode("ascii") + b"\n")

    # 循环执行命令列表
    for command in commands:
        tn.write(command.encode("ascii") + b"\n")
        time.sleep(4)

    # 读取回显（配置内容）
    output = tn.read_very_eager().decode("ascii")
    print(output)

    # 把回显追加写入文件
    f = open(file_name, mode="a")   # a 追加模式
    f.write(output)
    f.close()

    tn.close()

if __name__ == "__main__":
    commands = ["terminal length 0", "show running-config"]
    run_telnet("10.10.1.1", "admin", "wolf", commands)
    run_telnet("10.10.2.2", "admin", "wolf", commands)
    run_telnet("10.10.3.3", "admin", "wolf", commands)
    run_telnet("10.10.4.4", "admin", "wolf", commands)
    run_telnet("10.10.5.5", "admin", "wolf", commands)

# ========== 第二部分：发送带附件的邮件 ==========
# 1. 登录邮件服务器
smtp_obj = smtplib.SMTP_SSL("smtp.qq.com", 465)
smtp_obj.login("757984305@qq.com", "授权码")

# 2. 构建邮件正文（HTML）
mail_body = """
<h5>hello</h5>
<p>WOLF lab 网络技术实验室 CCIE/HCIE 培训与认证，包含 Python 网络自动化部分内容</p>
<p><a href="https://www.wolf-lab.com">点击进入 WOLF lab 实验室官网</a></p>
"""

# 3. 多部件邮件：正文 + 附件
email = MIMEMultipart()

# 3.1 正文
att1 = MIMEText(mail_body, "html", "utf-8")
email.attach(att1)

# 3.2 附件（就是前面备份的配置文件）
att2 = MIMEBase("application", "octet-stream")
f = open(file_name, mode="rb")
att2.set_payload(f.read())
f.close()
att2.add_header("Content-Disposition", "attachment",
                filename=Header(file_name, "utf-8").encode())
email.attach(att2)

# 4. 邮件头部：发件人、收件人、主题
email["From"] = Header("757984305@qq.com", "utf-8")
email["To"] = Header("CCIE/HCIE 学员", "utf-8")
email["Subject"] = Header("WOLF lab CCIE/HCIE 直通车，零基础开始", "utf-8")

# 5. 发送
smtp_obj.sendmail("757984305@qq.com", "接收者@qq.com", email.as_string())
```

### 9.2 代码要点解析

1. **备份文件名带时间戳**：用 `datetime.datetime.now().strftime(...)` 取当前时间并格式化，因为"什么时候备份的配置"很重要，没有时间的配置备份没有价值。

2. **`terminal length 0`**：进入设备后先关闭分页，让 `show running-config` 一次性完整输出，否则配置会分页显示（中间出现 "--More--" 提示）。

3. **用命令行列表 + 循环**：把要执行的命令放进 `commands` 列表，函数内 `for command in commands` 逐个执行，比写死在函数里更灵活（不同设备可传不同命令）。

4. **追加写文件 mode="a"**：多台设备的配置依次追加到同一个文件；读附件时用 `mode="rb"`（二进制读）。

5. **两次打开文件模式不同**：备份写入用 `"a"`（追加），发附件读取用 `"rb"`（二进制读）。

### 9.3 常见坑与注意事项

- **文件名/附件名不要含中文或过长**：中文名可能导致附件的下载文件名乱码，建议附件名用全英文。
- **授权码不是邮箱密码**：要用 QQ 邮箱生成的 SMTP 授权码；授权码写错会导致登录失败。
- **收发地址别写错**：发件人邮箱账号、收件人邮箱都要准确，否则报错或收不到。
- **标点符号用英文**：构建 Header/正文时文件名、主题中的冒号、斜杠等符号要用英文符号。
- **telnetlib 仅支持 Telnet**：明文传输，生产环境中用得不多，后续可学习 `paramiko`/`netmiko` 走 SSH 更安全。

---

## 附：本教程知识点速查

| 章节 | 核心知识点 |
|------|-----------|
| 函数及参数 | `def`、形参/实参、默认参数、关键参数、`*args`、`**kwargs` |
| 返回值与作用域 | `return`、全局变量/局部变量、`global`、判断合法 IP |
| 嵌套/高阶/递归 | 函数嵌套、函数作参数、递归、结束条件、栈溢出 |
| 内置模块 | `os`、`time`、`datetime`、`ipaddress`、`random`、`string`、`sys` |
| 正则表达式 | `re` 模块、`search/findall/match/sub`、元字符、限定符 |
| 模块导入 | `import`、`from...import`、`as` 重命名、`import *`、`__name__=="__main__"` |
| SMTP 发邮件 | `smtplib`、`email`、授权码、HTML 邮件、附件 |
| Telnet 登录 | `telnetlib`、`read_until`、`write`、`encode`、`time.sleep`、函数封装 |
| 综合实战 | 备份配置 + 时间戳文件名 + 列表循环刷命令 + 附件邮件 |

> 备注：本文档所有代码示例均由教程字幕整理、归纳并规范化，可直接复制运行验证（其中邮箱授权码、账号、IP 地址等需替换为你自己的实际信息）。



# Python 网络自动化学习笔记

> 来源：WOLF 实验室《Python 网络自动化》课程第 21–28 课字幕整理。
> 主题：使用 Python 登录网络设备（华为 / 思科）并实现配置备份、批量操作、周期任务与可执行文件打包。
> 涉及模块：`telnetlib`、`schedule`、`paramiko`、`netmiko`、`datetime`、`time`、`PyInstaller`。

***

## 目录

- [1. 基础知识与环境准备](#1-基础知识与环境准备)

- [2. telnetlib 模块：明文登录设备](#2-telnetlib-模块明文登录设备)

- [3. schedule 模块：定时任务](#3-schedule-模块定时任务)

- [4. paramiko 模块：SSH 登录](#4-paramiko-模块ssh-登录)

- [5. 配置备份的几种方式](#5-配置备份的几种方式)

- [6. 周期性自动化备份](#6-周期性自动化备份)

- [7. 脚本参数化（交互输入）](#7-脚本参数化交互输入)

- [8. netmiko 模块：更简洁的多厂商工具](#8-netmiko-模块更简洁的多厂商工具)

- [9. 生成可执行文件（PyInstaller）](#9-生成可执行文件pyinstaller)

- [10. 网络设备侧配置速查](#10-网络设备侧配置速查)

- [11. 常见问题与优化建议](#11-常见问题与优化建议)

***

## 1. 基础知识与环境准备

### 知识点 1.1 三种模块类型

Python 中可以把模块（module）分为三大类：

| 类型      | 说明                | 示例                                                         |
| ------- | ----------------- | ---------------------------------------------------------- |
| 内置标准模块  | Python 自带的模块，无需安装 | `time`、`datetime`、`telnetlib`                              |
| 第三方开源模块 | 社区开发、开源，需安装后使用    | `paramiko`、`netmiko`、`schedule`、`pythonping`、`pyinstaller` |
| 自定义模块   | 自己编写的 `.py` 文件    | 把你写的备份脚本封装成函数，供其它脚本 `import`                               |

**详细介绍：** 区分这三类模块的意义在于"是否要先安装"。内置模块开箱即用；第三方模块往往正是 Python 生态强大的原因——大量常用功能已经有人写好并开源，我们可以直接"拿来用"，而不必从零造轮子。

```python
import time       # 内置模块：让程序暂停
import datetime   # 内置模块：获取、格式化时间
import telnetlib  # 内置模块：明文 telnet 登录（Python 3.13 起已移除，建议改用 paramiko/netmiko）
import schedule   # 第三方模块：定时任务（需先安装）
import paramiko   # 第三方模块：SSH 登录（需先安装）
```

### 知识点 1.2 第三方模块的三种安装方式

**详细介绍：** 第三方模块使用前必须安装。课程演示了三种常用方式，掌握其中任意一种即可。

**方式一：在线安装（命令行）**

```bash
pip install paramiko
pip install schedule
pip install netmiko
pip install pyinstaller
```

**方式二：源码下载安装**

从开源社区下载源码包，解压进入目录后执行：

```bash
python setup.py install
```

**方式三：PyCharm 图形界面安装**

`File → Settings → Project → Python Interpreter → 点「+」→ 搜索模块名 → Install Package`。

**注意：** 安装时若网络较慢（尤其无代理/VPN），可用国内镜像加速：

```bash
pip install paramiko -i https://pypi.tuna.tsinghua.edu.cn/simple
```

***

## 2. telnetlib 模块：明文登录设备

### 知识点 2.1 telnetlib 介绍

**详细介绍：** `telnetlib` 是 Python 内置模块，用于通过 Telnet 协议（默认 23 端口）远程登录设备。它的特点是**明文传输**（用户名、密码、配置都不加密），安全性差，生产环境更推荐使用支持 SSH 加密的 paramiko / netmiko。`telnetlib` 从 Python 3.11 起被标记为弃用，Python 3.13 已移除；但作为理解"交互式登录设备"的第一课，它非常适合入门。

### 知识点 2.2 建立 Telnet 连接

**详细介绍：** 使用 `telnetlib.Telnet(host, port, timeout)` 建立到设备的连接。`host` 是设备的管理 IP，`port` 默认 23，`timeout` 是连接超时时间（秒）。

```python
import telnetlib

host = "10.10.1.1"
tn = telnetlib.Telnet(host, port=23, timeout=10)  # 连接设备，10 秒超时
tn.set_debuglevel(0)  # 0 关闭调试输出；1 打印收发过程，便于排错
```

### 知识点 2.3 交互式登录（发送用户名 / 密码）

**详细介绍：** Telnet 登录是交互式的：连接后设备提示 `Username:`、`Password:`，需要"等待提示符出现 → 再发送内容"。核心方法：

- `read_until(expected)`：读取数据，直到出现 `expected` 指定的字节串为止。

- `write(data)`：向设备写入命令，命令后必须手动加换行符 `\n` 表示回车。

- 发送的字符串要用 `.encode()` 转成字节，或用 `b"..."` 前缀。

```python
tn.read_until(b"Username:")                 # 等待用户名提示
tn.write(username.encode() + b"\n")         # 输入用户名并回车

tn.read_until(b"Password:")                 # 等待密码提示
tn.write(password.encode() + b"\n")         # 输入密码并回车
```

### 知识点 2.4 解决"分屏"问题（screen-length 0）

**详细介绍：** 设备默认一屏只显示 24 行，`display current-configuration` 这类长输出会显示到一半停下，出现在 `---- More ----` 处等待翻页（回车翻一行、空格翻一屏）。脚本无法像人一样"按空格"，所以必须先关闭分屏，让所有配置一次性输出。

- **华为设备**：进入 VTY 视图，执行 `screen-length 0`（0 表示单屏显示全部）。

```python
tn.write(b"system-view\n")               # 华为设备：进入系统视图
tn.write(b"user-interface vty 0 4\n")    # 进入 VTY 线程
tn.write(b"screen-length 0\n")           # 关闭分屏
tn.write(b"quit\n")                      # 逐级退回
```

### 知识点 2.5 导出配置并读取回显

**详细介绍：** 发送 `display current-configuration`（华为）命令后，**网络设备的响应速度远慢于 Python 脚本**，需要 `time.sleep()` 等待设备把内容完整回显出来，再用读取方法拿到回显并解码。

- `read_very_eager()`：立即读取当前缓冲区中已有的全部内容（配合 sleep 使用较稳妥）。

- `.decode("utf-8")`：把字节流转成字符串。

```python
import time

tn.write(b"display current-configuration\n")
time.sleep(3)                              # 等设备把配置完整回显出来

output = tn.read_very_eager().decode("utf-8")  # 读取回显并解码
print(output)
```

### 知识点 2.6 把配置写入文件（含时间戳文件名）

**详细介绍：** 备份的文件名最好带上"什么时候备份的"，否则单看文件无法判断是否最新。利用 `datetime.datetime.now()` 取当前时间，`strftime()` 格式化为字符串，再用 `open()` 写入文件。

`datetime` 常用格式化字符：

| 格式符  | 含义     | 格式符  | 含义         |
| ---- | ------ | ---- | ---------- |
| `%Y` | 四位年份   | `%H` | 小时（24 小时制） |
| `%m` | 月份（补零） | `%M` | 分钟         |
| `%d` | 日期（补零） | `%S` | 秒          |

```python
import datetime

now = datetime.datetime.now().strftime("%Y%m%d_%H%M%S")
filename = f"wolf_{host}_{now}.txt"        # 例如：wolf_10.10.1.1_20230729_220130.txt

with open(filename, "w", encoding="utf-8") as f:
    f.write(output)                        # 把配置内容写入文件

tn.close()                                 # 关闭 Telnet 会话
```

### 知识点 2.7 封装成函数 + 主程序入口

**详细介绍：** 把"对一台设备做备份"的逻辑封装成函数，传入 `host / username / password` 三个参数，即可复用；`if __name__ == "__main__":` 保证脚本被直接运行时才调用，被其它脚本 `import` 时不会自动执行。

```python
import telnetlib
import time
import datetime

def run_telnet(host, username, password):
    tn = telnetlib.Telnet(host, port=23, timeout=10)

    tn.read_until(b"Username:")
    tn.write(username.encode() + b"\n")
    tn.read_until(b"Password:")
    tn.write(password.encode() + b"\n")
    time.sleep(1)

    tn.write(b"system-view\n")
    tn.write(b"user-interface vty 0 4\n")
    tn.write(b"screen-length 0\n")
    tn.write(b"quit\n")
    time.sleep(1)

    tn.write(b"display current-configuration\n")
    time.sleep(3)

    output = tn.read_very_eager().decode("utf-8")

    now = datetime.datetime.now().strftime("%Y%m%d_%H%M%S")
    filename = f"wolf_{host}_{now}.txt"
    with open(filename, "w", encoding="utf-8") as f:
        f.write(output)

    tn.close()

if __name__ == "__main__":
    run_telnet("10.10.1.1", "admin", "wolf")   # 备份 R1
    run_telnet("10.10.2.2", "admin", "wolf")   # 备份 R2
```

> **易错点：** 华为设备需在 **VTY 线程**（而非 console 口）下配置 `screen-length 0`，否则通过 telnet/SSH 登录后分屏依然存在，导致配置没拉全。若配置没拉全，优先延长 `sleep` 时间。

***

## 3. schedule 模块：定时任务

### 知识点 3.1 schedule 介绍

**详细介绍：** `schedule` 是一个轻量的第三方定时任务模块，语法简单、可读性强，适合"每隔一段时间 / 每周某天某时刻"自动执行函数。相比 Windows 任务计划或 Linux crontab，它无需额外的系统运维知识，直接写在 Python 里即可。**它不是**系统级调度器——程序（`while True` 循环）必须一直运行，定时才会生效。

### 知识点 3.2 基本用法（三要素）

**详细介绍：** 使用 schedule 只需拼装三部分：

1. `schedule.every(间隔).时间单位.do(函数)` —— 注册任务；
2. `schedule.run_pending()` —— 执行所有到期的 pending 任务；
3. `while True: ... time.sleep(1)` —— 持续循环，让调度器一直工作。

```python
import schedule
import time
from datetime import datetime

def wolf():
    now = datetime.now().strftime("%H:%M:%S")
    print("现在时间是:", now)

schedule.every(3).seconds.do(wolf)   # 每隔 3 秒执行一次 wolf

while True:
    schedule.run_pending()           # 执行到期任务
    time.sleep(1)
```

运行效果（每 3 秒打印一次）：

```
现在时间是: 22:15:17
现在时间是: 22:15:20
现在时间是: 22:15:23
```

### 知识点 3.3 常用定时时间单位

**详细介绍：** 时间单位有 `seconds / minutes / hours / days / weeks`，以及按星期 `monday`\~`sunday` 和精确时刻 `.at("HH:MM")`。

```python
schedule.every(5).seconds.do(task)             # 每 5 秒
schedule.every().minute.do(task)               # 每分钟（间隔默认 1）
schedule.every(2).minutes.do(task)             # 每 2 分钟
schedule.every().hour.do(task)                 # 每小时
schedule.every().day.at("10:00").do(task)      # 每天 10:00
schedule.every().monday.do(task)               # 每周一
schedule.every().friday.at("22:00").do(task)   # 每周五 22:00
```

> **注意：** `do(函数)` 里传的是**函数对象本身**，不要加括号——`do(wolf)` 正确，`do(wolf())` 错误（后者会立刻执行一次并传入其返回值）。

### 知识点 3.4 实战：周期性 Ping 监控

**详细介绍：** 借助第三方模块 `pythonping`，可以周期性地 Ping 某个主机/网站，判断是否可达，实现简单监控。

```python
import schedule
import time
from pythonping import ping

host = "www.wolf-lab.com"

def ping_wolf():
    result = ping(host)
    if result.success():                # 所有包都有回包即视为可达
        print(f"{host} 可达")
    else:
        print(f"{host} 不可达")

schedule.every(3).seconds.do(ping_wolf)   # 每 3 秒 Ping 一次

while True:
    schedule.run_pending()
    time.sleep(1)
```

***

## 4. paramiko 模块：SSH 登录

### 知识点 4.1 paramiko 介绍

**详细介绍：** `paramiko` 是 Python 中实现 SSH2 协议的经典开源库，支持**加密远程登录**、执行命令、上传/下载文件。相比明文 Telnet，SSH 更安全，是生产环境的主流选择。课程后续的备份、周期任务、可执行文件基本都基于它。

### 知识点 4.2 基本连接流程（固定四步）

**详细介绍：** 用 paramiko 登录设备有固定的四步套路，牢记即可套用：

1. 创建客户端：`paramiko.SSHClient()`
2. 信任主机公钥：`set_missing_host_key_policy(paramiko.AutoAddPolicy())`
3. 连接：`connect(hostname=..., username=..., password=...)`
4. 关闭：`close()`

```python
import paramiko

ip = "10.10.1.1"
username = "admin"
password = "wolf"

# 1. 创建 SSH 客户端
ssh_client = paramiko.SSHClient()

# 2. 默认拒绝未知公钥；AutoAddPolicy 表示自动接受并信任服务器公钥
ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())

# 3. 连接设备
ssh_client.connect(hostname=ip, username=username, password=password)
print(f"Successfully connect to {ip}")

# ... 后续操作 ...

# 4. 关闭会话
ssh_client.close()
```

### 知识点 4.3 唤醒 shell、发送命令、接收回显

**详细介绍：** `connect()` 只是建立了 SSH 通道。要与设备**交互式**下发一批命令（例如进系统视图、创建用户、保存），需要先 `invoke_shell()` 唤醒一个交互式 shell，再逐个 `send()` 命令，最后 `recv()` 收取出显。

- `invoke_shell()`：唤醒交互式会话，返回一个 channel 对象。

- `send(cmd)`：发送一条命令，命令末尾要手动加 `\n` 回车。

- `recv(max_bytes)`：接收回显，`65535` 表示取最大字节数，再用 `.decode()` 解码。

```python
command = ssh_client.invoke_shell()        # 唤醒 shell

command.send("config t\n")                 # 思科：进入全局配置模式
command.send("username user001 privilege 15 password 123456\n")  # 创建临时用户
command.send("end\n")
command.send("write\n")                    # 保存
time.sleep(2)

output = command.recv(65535).decode("utf-8")   # 接收回显
print(output)

ssh_client.close()
```

### 知识点 4.4 发送命令配合 sleep 延时

**详细介绍：** 与 telnet 一样，Python 执行速度远快于设备，批量下发配置时须在关键节点 `time.sleep()`，否则可能丢配置或回显不完整。`show running-config` / `display current-configuration` 这类长输出尤其要多等几秒。

```python
import time

command.send("terminal length 0\n")       # 思科：关闭分屏
time.sleep(0.5)
command.send("show running-config\n")
time.sleep(3)                              # 等待配置完整回显
```

***

## 5. 配置备份的几种方式

### 知识点 5.1 方式一：通过 TFTP 备份

**详细介绍：** 借助 TFTP 服务器，把设备上的配置文件"推"到本机。思科用 `copy running-config tftp`，华为用 `tftp <本地IP> put <文件名>`。前提是**本机开启 TFTP 服务**，且指定了根目录（备份的文件会落在该目录下）。

**思科示例：**

```python
import paramiko
import time

ssh_client = paramiko.SSHClient()
ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
ssh_client.connect(hostname="192.168.183.250", username="admin", password="wolf")

command = ssh_client.invoke_shell()

command.send("copy running-config tftp\n")   # 开始 TFTP 备份
time.sleep(1)
command.send("192.168.183.1\n")              # 输入 TFTP 服务器（本机）地址
command.send("\n")                           # 文件名保持默认，直接回车
time.sleep(2)

output = command.recv(65535).decode("utf-8")
print(output)

ssh_client.close()
```

**华为示例（保存后推送到 TFTP）：**

```python
command.send("tftp 192.168.183.1 put flash:/vrpcfg.zip\n")
command.send("y\n")                        # 若提示确认则输入 y
time.sleep(2)
```

### 知识点 5.2 方式二：show / display 输出 + 写入本地文件

**详细介绍：** 不依赖 TFTP，直接把 `show running-config`（思科）或 `display current-configuration`（华为）的**回显内容**写到本地文本文件。前提同样是先关闭分屏。

```python
import paramiko
import time

ssh_client = paramiko.SSHClient()
ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
ssh_client.connect(hostname="10.10.1.1", username="admin", password="wolf")

command = ssh_client.invoke_shell()

command.send("terminal length 0\n")          # 思科关闭分屏（华为用 screen-length 0）
time.sleep(0.5)
command.send("show running-config\n")        # 华为用 display current-configuration
time.sleep(3)

output = command.recv(65535).decode("utf-8")
print(output)

ssh_client.close()
```

### 知识点 5.3 备份文件名加时间戳

**详细介绍：** 备份文件应能一眼看出"对哪台设备、什么时间"做的备份，否则没有归档价值。用 `format()` 或 f-string 拼接 IP 与时间。

```python
import datetime

date = datetime.datetime.now().strftime("%Y-%m-%d_%H%M%S")
filename = f"{ip}_{date}.txt"   # 例如：10.10.1.1_2023-07-29_150512.txt

with open(filename, "w", encoding="utf-8") as f:
    f.write(output)
```

> **温习** **`open()`** **参数：**
>
> - `"w"`：写入模式，**若文件已存在会清空覆盖**；
>
> - `"a"`：追加模式，在原有内容末尾继续写；
>
> - 用带时间戳的文件名可避免每次覆盖旧备份（每次都是新文件）。

***

## 6. 周期性自动化备份

### 知识点 6.1 把备份逻辑封装成函数

**详细介绍：** 把"SSH 登录 + 导出配置 + 写文件"整段封装成 `run_ssh(host, username, password)`，这样一台设备和多台设备都能复用，也为定时调用打下基础。

```python
import paramiko
import time
import datetime

def run_ssh(host, username, password):
    ssh_client = paramiko.SSHClient()
    ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
    ssh_client.connect(hostname=host, username=username, password=password)
    print(f"Successfully connect to {host}")

    command = ssh_client.invoke_shell()
    command.send("terminal length 0\n")
    time.sleep(0.5)
    command.send("show running-config\n")
    time.sleep(3)

    output = command.recv(65535).decode("utf-8")

    date = datetime.datetime.now().strftime("%Y-%m-%d_%H%M%S")
    filename = f"{host}_{date}.txt"
    with open(filename, "w", encoding="utf-8") as f:
        f.write(output)

    ssh_client.close()
```

### 知识点 6.2 schedule + paramiko 实现周期备份

**详细介绍：** 把 `schedule` 与 `run_ssh` 结合即可定时备份。示例中先用"每 2 分钟"观察现象，实际生产可改为"每周五 22:00"。

```python
import schedule
import time

schedule.every(2).minutes.do(run_ssh, "192.168.183.250", "admin", "wolf")

# 生产环境示例：每周五 22:00 备份
# schedule.every().friday.at("22:00").do(run_ssh, "192.168.183.250", "admin", "wolf")

while True:
    schedule.run_pending()
    time.sleep(1)
```

> **说明：** `do(函数, 参数1, 参数2, ...)` 会把后面的参数依次传给被调用的函数，非常方便。

***

## 7. 脚本参数化（交互输入）

### 知识点 7.1 input() 交互输入

**详细介绍：** 把写死在代码里的 IP / 用户名 / 密码改为运行时由用户输入，脚本即可"一次编写、处处可复用"，对不同设备执行。核心是 `input()` 函数，它接收键盘输入并返回字符串。

```python
name = input("请输入你的名字: ")                 # 备份人
ip = input("请输入要备份的网络设备IP地址: ")
username = input("请输入设备的登录用户名: ")
password = input("请输入设备的登录密码: ")

print(f"{name} 正在备份 {ip} ...")
```

### 知识点 7.2 参数化完整示例

**详细介绍：** 把 `input()` 收集的变量传给连接与文件命名逻辑，生成形如 `老杨_10.10.1.1_2023-07-29_150512.txt` 的备份文件，一眼看清"谁、哪台设备、什么时间"。

```python
import paramiko
import time
import datetime

name = input("请输入你的名字: ")
ip = input("请输入要备份的网络设备IP地址: ")
username = input("请输入设备的登录用户名: ")
password = input("请输入设备的登录密码: ")

ssh_client = paramiko.SSHClient()
ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
ssh_client.connect(hostname=ip, username=username, password=password)
print(f"Successfully connect to {ip}")

command = ssh_client.invoke_shell()
command.send("terminal length 0\n")
time.sleep(0.5)
command.send("show running-config\n")
time.sleep(3)

output = command.recv(65535).decode("utf-8")

date = datetime.datetime.now().strftime("%Y-%m-%d_%H%M%S")
filename = f"{name}_{ip}_{date}.txt"
with open(filename, "w", encoding="utf-8") as f:
    f.write(output)

ssh_client.close()
```

***

## 8. netmiko 模块：更简洁的多厂商工具

### 知识点 8.1 netmiko 介绍

**详细介绍：** `netmiko` 是 2015 年发布的开源库，基于 paramiko 二次封装，目标是简化多厂商网络设备的 CLI 连接（支持 SSH 和 Telnet）。如果说 paramiko 是"手动挡"，netmiko 就是"自动挡"——它自动处理回车、进入配置模式（`config t` / `system-view`）与退出（`end` / `return`），代码更简洁。它通过 `device_type` 指定厂商（思科、华为、惠普、Juniper、Palo Alto 等），适配不同设备的命令差异。

安装：

```bash
pip install netmiko
```

### 知识点 8.2 连接设备（ConnectHandler + 字典）

**详细介绍：** 用 `from netmiko import ConnectHandler` 导入连接函数，用一个字典描述设备信息（`device_type`、`ip`、`username`、`password`），再传入 `ConnectHandler(**device)` 建立连接。

```python
from netmiko import ConnectHandler

device = {
    "device_type": "cisco_ios",   # 思科 IOS；华为常用 huawei
    "ip": "10.10.1.1",
    "username": "admin",
    "password": "wolf",
}

with ConnectHandler(**device) as conn:   # with 语句自动管理连接的关闭
    print(f"Successfully connect to {device['ip']}")
```

> 使用 `with` 语句，退出代码块时会自动断开连接，无需手写 `close()`。

### 知识点 8.3 send\_command：发送单条查询命令

**详细介绍：** `send_command()` 用于发送**单条**查询命令（如 `show` / `display` / 保存类命令），**不需要**手动加回车。它会一直等待，直到收到完整的回显。

```python
with ConnectHandler(**device) as conn:
    output = conn.send_command("show ip interface brief")
    print(output)
```

### 知识点 8.4 send\_config\_set：批量推送配置命令

**详细介绍：** `send_config_set()` 用于推送**配置类**命令，可用**列表**一次性下发多条。它会自动在命令前加"进入配置模式"，命令后加"退出配置模式"，因此**不需要**自己写 `config t` / `end`。

```python
with ConnectHandler(**device) as conn:
    config_commands = [
        "username user005 privilege 15 password 123456",   # 创建用户
        "line vty 0 4",
        "transport input ssh",                              # 允许 SSH
    ]
    output = conn.send_config_set(config_commands)
    print(output)
```

> **注意：** `send_config_set` 自动进入配置模式后，如果想执行 `show` 这类查询命令，需在前面加 `do`（思科），例如 `"do show ip interface brief"`，否则会因处于配置模式下而报"Invalid input"。

### 知识点 8.5 send\_config\_from\_file：从文件读取配置

**详细介绍：** 当要刷的配置很多时，把命令写进列表会让代码过长、不易阅读，还可能在部分厂商设备上引起超时。此时可把配置写到一个文本文件里（每行一条命令），用 `send_config_from_file()` 读取并执行。它同样会自动补上"进入/退出配置模式"，所以**文件中不要写** `config t` / `end`。

`commands.txt` 文件内容：

```
username user006 password 666666
username user007 password 123456
username user008 password 123456
```

```python
with ConnectHandler(**device) as conn:
    output = conn.send_config_from_file("commands.txt")
    print(output)
```

### 知识点 8.6 备份配置 + 封装成函数

**详细介绍：** 用 `send_command` 依次下发"关闭分屏"和"导出配置"两条命令（因 `send_command` 只接受单条命令，须分开调用），再把回显写入文件、带上时间戳；最后把整段封装成可复用函数。

```python
import datetime
from netmiko import ConnectHandler

def run_ssh(device):
    with ConnectHandler(**device) as conn:
        print(f"Successfully connect to {device['ip']}")
        conn.send_command("terminal length 0")      # 思科关闭分屏
        output = conn.send_command("show running-config")

    date = datetime.datetime.now().strftime("%Y%m%d")
    filename = f"wolf_{date}.txt"
    with open(filename, "w", encoding="utf-8") as f:
        f.write(output)

if __name__ == "__main__":
    device = {
        "device_type": "cisco_ios",
        "ip": "10.10.2.2",
        "username": "admin",
        "password": "wolf",
    }
    run_ssh(device)
```

***

## 9. 生成可执行文件（PyInstaller）

### 知识点 9.1 PyInstaller 介绍

**详细介绍：** `PyInstaller` 是第三方模块，能把 `.py` 脚本打包成独立的 `.exe` 可执行文件，打包后**无需安装 Python 环境**即可在目标机器上直接运行，便于交付给不会写代码的同事使用。

安装：

```bash
pip install pyinstaller
```

### 知识点 9.2 打包命令与常用参数

**详细介绍：** 先在命令行 `cd` 到 `.py` 文件所在目录，再执行 `pyinstaller` 命令。常用参数：

| 参数            | 作用                                              |
| ------------- | ----------------------------------------------- |
| `-F`          | 生成**单个** exe 文件（否则默认生成一堆依赖文件）                   |
| `-w`          | 去除控制台窗口（GUI 程序用；**需要交互输入的脚本千万不要加**，否则看不到提示也输不了） |
| `-i icon.ico` | 给 exe 指定图标                                      |

```bash
cd C:\Users\jingl\PycharmProjects\python2023
pyinstaller -F backup.py            # 推荐：单个文件 + 保留控制台（便于交互）
pyinstaller -F -w gui.py            # 去控制台的 GUI 程序
pyinstaller -F -i icon.ico backup.py  # 自定义图标
```

打包成功后，可执行文件位于同目录下的 **`dist`** 文件夹中，如 `dist\backup.exe`。

### 知识点 9.3 运行打包后的程序

**详细介绍：** 双击 `dist` 目录下的 exe，或在命令行运行，即可按脚本中的 `input()` 进行交互。

```
请输入你的名字: laoyang
请输入要备份的网络设备IP地址: 10.10.3.3
请输入设备的登录用户名: admin
请输入设备的登录密码: wolf
Successfully connect to 10.10.3.3
```

***

## 10. 网络设备侧配置速查

> 脚本能登录的前提是设备侧已开启相应服务并配置好账号。此处汇总思科与华为两套命令。

### 10.1 华为设备：Telnet 登录

```
<Huawei> system-view
[Huawei] telnet server enable                     # 开启 Telnet 服务
[Huawei] aaa
[Huawei-aaa] local-user admin password cipher wolf
[Huawei-aaa] local-user admin privilege level 15
[Huawei-aaa] local-user admin service-type telnet
[Huawei-aaa] quit
[Huawei] user-interface vty 0 4
[Huawei-ui-vty0-4] authentication-mode aaa        # 认证方式用 AAA
[Huawei-ui-vty0-4] protocol inbound telnet        # 允许 Telnet 登录
```

### 10.2 华为设备：SSH 登录

```
<Huawei> system-view
[Huawei] stelnet server enable                     # 开启 SSH（STelnet）服务
[Huawei] aaa
[Huawei-aaa] local-user admin password cipher wolf
[Huawei-aaa] local-user admin privilege level 15
[Huawei-aaa] local-user admin service-type ssh      # 该用户用于 SSH 登录
[Huawei-aaa] quit
[Huawei] user-interface vty 0 4
[Huawei-ui-vty0-4] authentication-mode aaa
[Huawei-ui-vty0-4] protocol inbound ssh             # 允许 SSH 登录
```

### 10.3 思科设备：SSH 登录

```
Router> enable
Router# configure terminal
Router(config)# hostname R1
Router(config)# ip domain-name wolf.com            # 生成密钥前必须先有域名
Router(config)# crypto key generate rsa            # 生成 RSA 密钥（如 1024 位）
Router(config)# username admin privilege 15 password wolf
Router(config)# line vty 0 4
Router(config-line)# transport input ssh           # 允许 SSH
Router(config-line)# login local                   # 本地认证
```

### 10.4 本机静态路由（模拟环境桥接时）

**详细介绍：** 在 eNSP / EVE-NG 模拟环境中，设备通过"云"桥接到本机网卡，`192.168.183.x` 是直连网段可通过；但访问设备的管理地址 `10.10.x.x` 时本机没有路由，会走默认网关（互联网）而不可达。此时需要在**本机**加一条指向设备的静态路由。

```powershell
route add 10.10.0.0 mask 255.255.0.0 192.168.183.250
```

删除该路由：

```powershell
route delete 10.10.0.0 mask 255.255.0.0 192.168.183.250
```

> 工作环境中，管理 PC 到设备本身就可达，此步仅模拟环境需要。

***

## 11. 常见问题与优化建议

### 11.1 配置"没拉全"

**原因：** 分屏未关闭，或 `sleep` 时间太短，设备还没把配置完整回显。

**解决：**

1. 确认已在正确的视图（telnet/SSH 走 **VTY**，consle 直连才用 console 口）下关闭分屏：

   - 思科：`terminal length 0`

   - 华为：`screen-length 0`
2. 导出配置后把 `time.sleep()` 延长到 3～4 秒。

### 11.2 SSH 连接被拒（unable to connect to port 22）

**常见原因：**

- 设备未开启 SSH 服务；

- VTY 下未配置 `transport input ssh`（思科）或 `protocol inbound ssh`（华为）；

- 本地没有到设备管理 IP 的路由（模拟环境漏配静态路由）。

**排查：** 先在命令行手工 `ssh` 或 `telnet` 验证能否登录，再排查脚本。

### 11.3 密码提示 / 密钥信任问题

- 首次 SSH 登录，paramiko 默认拒绝未知公钥，务必加 `set_missing_host_key_policy(paramiko.AutoAddPolicy())`。

- 用户名 / 密码发错会得到认证失败，确认设备侧账号的 `service-type` 与权限级别（`privilege level 15`）正确。

### 11.4 Telnet 明文无加密

- Telnet 用户名、密码、配置均明文传输，生产环境应优先使用 **SSH**（paramiko / netmiko）。

- `telnetlib` 已弃用（Python 3.13 移除），新项目建议直接用 paramiko 或 netmiko。

### 11.5 编码问题（写入文件报"必须是字符串而非字节"）

- `recv()` 返回的是字节流 `bytes`，写入文本文件前要 `.decode("utf-8")` 转成字符串。

- 写入文件时建议显式指定 `encoding="utf-8"`，避免中文乱码。

### 11.6 优化方向（课程提及，可自行扩展）

1. **设备清单化**：把要备份的多台设备（IP、用户名、密码）写进一个 `devices.txt` 或 `Excel`，脚本循环读取，批量执行，而不是逐个手写调用。
2. **日志与异常处理**：对登录失败、超时做 `try/except` 捕获并记录日志，避免单台故障导致整体中断。
3. **结果回执**：备份完成后自动发送邮件给管理员（课程前半部分思路）。

***

## 附：一句话总结每个模块

| 模块            | 定位           | 一句话总结                                          |
| ------------- | ------------ | ---------------------------------------------- |
| `telnetlib`   | 明文 Telnet    | 入门用，需手动处理提示符、回车、分屏与等待                          |
| `schedule`    | 定时调度         | 用 `every().时间单位.do()` + `run_pending()` 实现周期任务 |
| `paramiko`    | SSH 客户端      | 四步连接 + `invoke_shell`/`send`/`recv` 交互操作       |
| `netmiko`     | paramiko 的封装 | 自动挡，靠 `device_type` 适配多厂商，命令更简洁                |
| `datetime`    | 时间处理         | `now()` + `strftime()` 生成带时间戳的文件名              |
| `PyInstaller` | 打包           | `pyinstaller -F` 把脚本打成独立 exe 交付                |

