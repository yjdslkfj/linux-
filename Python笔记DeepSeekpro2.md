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