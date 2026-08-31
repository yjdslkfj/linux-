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

