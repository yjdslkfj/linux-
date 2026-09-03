# Shell 学习笔记

> 本笔记整理自《30 分钟 Shell 光速入门教程》（B 站 BV17m411U7cC）。
> 视频内容已全部收录；标注 **【补充】** 的部分是视频中未展开、但对完整掌握 Shell 必不可少的知识，均已补齐。

---

## 目录

1. [Shell 基础概念](#一shell-基础概念)
2. [第一个 Shell 脚本](#二第一个-shell-脚本)
3. [编辑器选择：vim / VS Code / nano](#三编辑器选择vim--vs-code--nano)
4. [变量](#四变量)
5. [环境变量与配置文件](#五环境变量与配置文件)
6. [用户交互：echo 与 read](#六用户交互echo-与-read)
7. [运算符](#七运算符)
8. [条件判断 if](#八条件判断-if)
9. [循环](#九循环)
10. [函数](#十函数)
11. [命令替换与随机数](#十一命令替换与随机数)
12. [实战案例](#十二实战案例)
13. [补充：教程未覆盖的重要内容](#十三补充教程未覆盖的重要内容)
14. [常见坑速查表](#十四常见坑速查表)
15. [常用命令速查表](#十五常用命令速查表)

---

## 一、Shell 基础概念

### 1.1 Shell 是什么

Shell 是一个**命令行解释器（Command Interpreter）**，它的工作流程：

```
用户输入命令 ──► Shell 解释命令 ──► 调用操作系统内核执行 ──► 把结果返回给用户
```

也就是说，Shell 是用户与操作系统内核之间的"翻译官"。我们在终端里输入的命令，并不是内核直接认识的，而是先交给 Shell 解释，再由 Shell 调用内核去执行，最后把执行结果显示出来。

### 1.2 常见的 Shell 种类

Shell 有很多种类，常见的有：

| Shell | 全称 / 说明 |
|-------|------------|
| **sh** | Bourne Shell，最早的 Unix Shell，是所有 Shell 的"祖先" |
| **bash** | Bourne-Again Shell，sh 的增强版，**Linux 系统默认安装的一般就是 bash** |
| **zsh** | Z Shell，功能最强大，macOS 新版系统的默认 Shell |
| **ksh** | Korn Shell，兼容 sh，商业 Unix 中常见 |
| **fish** | Friendly Interactive Shell，开箱即用的现代化 Shell（语法与 bash 不完全兼容） |
| **cmd / PowerShell** | Windows 系统上微软自己的命令提示符与 PowerShell |

要点：

- 不同 Shell 版本之间存在一些**微妙差异**，但大部分基础命令是**通用**的；
- 本教程（及本笔记）以 **bash** 为例。

### 1.3 不同操作系统如何使用 Shell

| 系统 | 使用方式 |
|------|---------|
| **Windows** | ① 使用自带的子系统 **WSL**（Windows Subsystem for Linux）安装一个 Linux；② 更简单的方式：安装 **Git 客户端**，它自带一个轻量的 **Git Bash**。安装后在鼠标右键菜单中会出现 "Git Bash Here" 选项，点击即打开一个 bash 环境，对简单命令行操作完全够用 |
| **macOS / Linux** | 直接打开"终端"（Terminal）即可；macOS 上还可以用 Alfred 之类的工具搜索并打开终端 |

### 1.4 查看系统中所有的 Shell：/etc/shells

`/etc/shells` 这个文件记录了当前系统中**所有可用的 Shell 版本**：

```bash
cat /etc/shells        # 查看系统中所有已安装的 Shell
```

典型输出（Ubuntu）：

```
/bin/sh
/bin/bash
/usr/bin/bash
/bin/dash
/bin/rbash
/usr/bin/tmux
```

### 1.5 通过环境变量查看当前默认 Shell

Linux 中有很多**环境变量**，用来存储系统的配置信息。常见的几个：

| 环境变量 | 含义 |
|---------|------|
| `$HOME` | 当前用户的**家目录**（home directory） |
| `$PATH` | 系统的**命令查找路径**——你输入一个命令时，系统就会在这些路径中依次查找该命令的可执行文件 |
| `$SHELL` | 当前系统**默认使用的 Shell 的路径** |

使用 `echo` 命令加上**美元符号 `$`** 和变量名即可查看：

```bash
echo $SHELL     # 输出如：/bin/bash，说明默认 Shell 是 bash
echo $HOME      # 输出如：/home/laoyang
echo $PATH      # 输出一串以冒号分隔的路径
```

#### `$SHELL` 与 `$0` 的区别（易混淆）

| 变量 | 性质 | 含义 |
|------|------|------|
| `$SHELL` | **系统环境变量** | 当前用户默认 Shell 的路径，**切换到其他 Shell 后它不会变化** |
| `$0` | 位置参数 | **当前正在执行的脚本 / 程序的名称**，切换 Shell 后会变成新 Shell 的名字 |

```bash
/bin/sh         # 临时切换到 sh
echo $SHELL     # 仍然是 /bin/bash（默认 Shell 没变）
echo $0         # 变成了 sh（当前正在执行的程序变了）
exit            # 退出当前 Shell，回到 bash
```

### 1.6 切换 Shell 与退出

直接在命令行输入某个 Shell 的**路径**即可切换；输入 `exit` 退出：

```bash
/bin/sh         # 切换到 sh
/bin/zsh        # 切换到 zsh（前提是已安装）
exit            # 退出当前 Shell
```

---

## 二、第一个 Shell 脚本

### 2.1 为什么需要 Shell 脚本

交互式地一条条输入命令，对于简单操作很方便；但如果要执行**复杂操作**或**重复执行**的命令（例如凌晨自动备份数据、定时清理日志文件——总不能每天半夜爬起来手动执行一遍），就很麻烦了。

解决思路：**把想要执行的命令写进一个文件，执行这个文件，就能一次性执行所有命令。** 这个文件就是 **Shell 脚本**。

Shell 脚本的典型应用场景：

- 软件安装部署
- 数据备份
- 系统运维巡检
- 自动化定时任务

### 2.2 编写 hello.sh

用任意文本编辑器（vim、VS Code 均可）新建一个文件，命名为 `hello.sh`：

```bash
#!/bin/bash          # Shebang 行：声明本脚本使用 bash 解释器执行
echo "hello shell"   # 打印一段文字
date                 # 显示当前的日期和时间
whoami               # 显示当前登录的用户名
```

**逐行解释：**

- **第 1 行 `#!/bin/bash`**：井号 + 感叹号开头，称为 **Shebang（释伴）**，用来声明脚本使用哪个解释器执行。系统执行该脚本时会自动调用 `/bin/bash` 来解释执行。
  - 如果想用其他解释器，替换路径即可，例如使用 zsh 就写成 `#!/bin/zsh`；
  - 这一行**必须是第一行**才会生效。
- **第 2~4 行**：普通的系统命令，脚本中的命令会**按书写顺序依次执行**。

**关于扩展名 `.sh`：**

- 脚本文件的扩展名一般以 `.sh` 结尾，但这只是**约定俗成的规范**；
- 脚本可以是任意扩展名，甚至没有扩展名都没问题；
- 不过仍建议使用 `.sh`，让其他人一眼就知道这是个 Shell 脚本文件。

### 2.3 执行脚本

```bash
chmod +x hello.sh    # 给脚本添加执行权限（Linux 中执行文件必须有执行权限）
./hello.sh           # 方式一：点号斜线 + 文件名，直接执行
bash hello.sh        # 方式二：显式指定用 bash 来执行
```

**两种执行方式的区别：**

| 方式 | 是否需要执行权限 | 解释器由谁决定 |
|------|----------------|---------------|
| `./hello.sh` | **需要**（先 `chmod +x`） | 由脚本第一行的 Shebang 决定 |
| `bash hello.sh` | 不需要 | 由命令中显式指定的解释器决定 |

**【补充】** 两种方式都是在**子 Shell 进程**中执行脚本，脚本内的变量、目录切换不会影响当前终端。若想让脚本在**当前 Shell** 中执行（比如脚本里 `cd` 换目录后希望保留），用 `source` 或 `.`：

```bash
source hello.sh      # 在当前 Shell 中执行
. hello.sh           # 与 source 等价，注意点号后面有空格
```

### 2.4 Shell 脚本能做什么

Shell 脚本功能非常强大，支持很多编程语言才有的特性：

- 分支（if / case）、循环（for / while）
- 变量与函数
- 调用系统命令及其他程序
- 文件读写操作

---

## 三、编辑器选择：vim / VS Code / nano

写脚本离不开编辑器，视频介绍了三种：

**① vim**（上一节课讲过，但对新手不太友好）

**② VS Code 的 Remote-SSH 远程连接扩展**

- 在 VS Code 扩展商店搜索 **Remote - SSH** 并安装；
- 安装后左侧多出一个"远程连接"图标，可以添加、配置 SSH 连接；
- 连上远程服务器后，可以直接编辑远程文件，还能打开终端直接在服务器上执行命令，非常方便。

**③ nano（最简单，推荐新手）**

```bash
nano game.sh         # nano + 文件名，直接打开编辑器
```

- 不需要记忆复杂的命令和快捷键；
- 编辑完成后按 **Ctrl + X**，提示是否保存，按 **Y** 确认，回车保存退出。

---

## 四、变量

### 4.1 变量的定义与使用

```bash
name="老杨"           # 定义变量：注意等号两边【不能有空格】！
echo $name            # 使用变量：前面要加美元符号 $
echo "你好，$name"     # 双引号字符串中 $name 会被正常解析
```

**【补充】变量命名的规则与细节：**

- 定义时**等号两边不能有空格**（`name = "老杨"` 会报错，这是 Shell 和其他语言最大的区别之一）；
- 变量名只能包含字母、数字、下划线，且不能以数字开头；
- 定义时不加 `$`，**使用时才加 `$`**；
- 变量默认都是**字符串类型**（详见后文算术运算一节）；
- 建议使用变量时写成 `$\{name\}` 花括号形式，在字符串拼接时能避免歧义：

```bash
echo "${name}你好"    # 若写成 $name你好，Shell 会把 name你好 当成变量名而出错
```

### 4.2 只读变量与删除变量【补充】

```bash
name="老杨"
readonly name         # 设为只读变量，之后再赋值会报错
name="张三"           # bash: name: readonly variable

unset name            # 删除变量，删除后为空
```

### 4.3 位置参数与特殊变量

给脚本传参数，在脚本内用 **`$` + 数字序号** 引用：

| 变量 | 含义 |
|------|------|
| `$0` | 当前正在执行的**脚本名称** |
| `$1`、`$2`、`$3`... | 传给脚本的**第 1、2、3 个参数**（第 10 个及以后要写成 `${10}`） |
| `$#` | 传递给脚本的**参数个数** |
| `$*` | 所有参数的**整体**（当成一个字符串） |
| `$@` | 所有参数的**列表**（每个参数相互独立） |
| `$?` | **上一个命令的返回值**（退出状态码）：0 表示成功，非 0 表示失败 |
| `$$` | 当前脚本的**进程 ID（PID）** |
| `$!` | 最近一个后台进程的 PID【补充】 |

**示例 param.sh：**

```bash
#!/bin/bash
# 演示位置参数与特殊变量
echo "脚本名称：$0"          # 第 0 个参数：脚本自身
echo "第一个参数：$1"        # 姓名
echo "第二个参数：$2"        # 频道名
echo "参数个数：$#"          # 一共传了几个参数
echo "所有参数：$@"          # 列出所有参数
```

执行：

```bash
chmod +x param.sh
./param.sh 老杨 老杨聊编程
# 输出：
# 脚本名称：./param.sh
# 第一个参数：老杨
# 第二个参数：老杨聊编程
# 参数个数：2
# 所有参数：老杨 老杨聊编程
```

`$?` 的典型用法——判断上一条命令是否成功：

```bash
ls /not_exist_dir
echo $?          # 非 0（如 2），说明上一条命令失败了
echo "hello"
echo $?          # 0，说明上一条命令成功了
```

### 4.4 普通变量 vs 环境变量（重要概念）

**问题现场：** 在命令行定义了变量，脚本里却取不到——

```bash
name="老杨"                # 在命令行定义普通变量
channel="老杨聊编程"
./game.sh                  # 脚本里 echo $name，结果是空的！
```

**原因：** 命令行中直接定义的只是**普通变量（局部变量）**，只对**当前 Shell 会话**有效。执行脚本时，系统会**新开一个子 Shell 进程**去运行它，子进程拿不到父进程的普通变量。

**解决办法：** 用 `export` 命令把变量**导出为环境变量**。环境变量会被子进程继承：

```bash
export name="老杨"          # 方式一：定义的同时导出
channel="老杨聊编程"
export channel              # 方式二：先定义，再导出（可一次导出多个）
./game.sh                   # 这次脚本里能取到 $name 和 $channel 了
```

**注意：** 用 `export` 定义的环境变量也**只在当前 Shell 会话中有效**——用 `exit` 退出再重新登录后，这些变量就失效了（变成空值）。想要永久生效，见下一节。

---

## 五、环境变量与配置文件

### 5.1 让环境变量永久生效

Shell 在**启动时会读取一些配置文件**，把环境变量的定义写进这些文件，就能永久生效。

**用户级配置文件（位于家目录下）：**

| 文件 | 执行时机 | 说明 |
|------|---------|------|
| `~/.bash_profile` | 用户**登录时**执行，且**只执行一次** | 常用于设置环境变量 |
| `~/.bashrc` | **每次打开新终端 / 新建 Shell 会话**时执行 | 最常改的文件 |

- 这两个文件是**隐藏文件**：Linux 中所有以**点号 `.` 开头**的文件都是隐藏文件，直接 `ls` 看不到，需要 `ls -a`（a = all）显示所有文件；
- **`~/.bash_profile` 中通常会去调用 `~/.bashrc`**，所以一般推荐把环境变量放到 `~/.bashrc` 中，这样每次新开终端都能获取到；
- **系统级配置文件**（对**所有用户**都有效）：`/etc/profile`、`/etc/bash.bashrc`（不同发行版命名略有差异）；
- 不同 Shell 的配置文件不同，但原理相同：**zsh → `~/.zshrc`；fish → `~/.config/fish/config.fish`**。

**操作示例（把变量永久写入配置）：**

```bash
nano ~/.bashrc            # 用 nano 打开配置文件，滚动到文件最后
```

在文件末尾追加：

```bash
export name="老杨"
export channel="老杨聊编程"
```

保存退出后，**必须让系统重新读取配置文件**才能生效（高频踩坑点）：

```bash
source ~/.bashrc          # 重新加载配置文件
. ~/.bashrc               # 用点号（source 的简写）也可以
# 或者：exit 退出当前 Shell 会话，重新登录
```

验证：

```bash
echo $name $channel       # 重新登录后不再为空
./game.sh                 # 脚本中也能正常使用
```

### 5.2 alias 别名

`~/.bashrc` 中除了存环境变量，还可以定义**别名（alias）**来简化命令。默认的 `.bashrc` 中就定义了 `ls` 命令的一些别名，如 `ll`、`la` 等。也可以自定义：

```bash
# 写在 ~/.bashrc 中，source 生效后即可使用
alias ll='ls -l'              # 列表形式显示详细信息
alias la='ls -a'              # 显示所有文件（含隐藏文件）
alias cls='clear'             # 仿 Windows 的清屏
alias gs='git status'         # 简化 git 命令
```

【补充】查看当前已定义的所有别名直接输入 `alias`；删除别名用 `unalias 别名名`。

---

## 六、用户交互：echo 与 read

### 6.1 echo 输出

```bash
echo "请输入您的姓名"        # 输出一段文字（默认末尾换行）
echo $name                   # 输出变量的值
```

**【补充】echo 的常用选项：**

```bash
echo -n "不换行"             # -n：结尾不换行
echo -e "第一行\n第二行"      # -e：解释转义字符（\n 换行、\t 制表符）
```

### 6.2 read 读取用户输入

`read` 命令读取用户输入的一行，并赋值给变量：

```bash
read name                    # 用户输入的内容存入 name
```

配合 echo 实现交互：

```bash
#!/bin/bash
echo "请输入您的姓名："       # 先提示
read name                    # 再读取输入
echo "你好，$name！"          # 使用输入的内容
```

**【补充】read 的常用选项（非常实用）：**

```bash
read -p "请输入姓名：" name   # -p：自带提示语，省去单独的 echo
read -t 5 answer             # -t 5：限时 5 秒，超时返回非 0
read -n 1 key                # -n 1：只读取 1 个字符（无需回车）
read -s password             # -s：静默模式，输入不回显（适合密码）
read a b c                   # 一行输入多个值，按空格分给 3 个变量
```

### 6.3 printf 格式化输出【补充】

比 echo 更强大的格式化输出（语法同 C 语言的 printf）：

```bash
printf "%-10s %5d\n" "姓名" 18
# %-10s：左对齐、占 10 个字符宽的字符串
# %5d：右对齐、占 5 个字符宽的整数
# \n：printf 默认不换行，需要手动加
```

---

## 七、运算符

### 7.1 算术运算：`$(( ))`

Shell 变量默认是**字符串**，直接写 `$a + $b` 不会进行计算。**必须用两个小括号把表达式括起来**，Shell 才会把括号里的内容当成一个整体来计算：

```bash
a=10
b=3
echo $((a + b))        # 13，加
echo $((a - b))        # 7，减
echo $((a * b))        # 30，乘
echo $((a / b))        # 3，除（整数除法，舍去小数）
echo $((a % b))        # 1，取模（取余数）
echo $((2 ** 10))      # 1024，幂运算【补充】
```

其他算术运算写法【补充】：

```bash
let "sum = 1 + 2"      # let 命令
sum=`expr 1 + 2`       # expr 命令（注意运算符两边必须有空格），老写法，不推荐
sum=$[1 + 2]           # $[ ] 写法，等价于 $(( ))
```

### 7.2 数值比较运算符（用在 `[ ]` 中）

这类运算符都是**两个字母的缩写**，用于整数比较：

| 运算符 | 英文 | 含义 |
|--------|------|------|
| `-eq` | **eq**ual | 等于 |
| `-ne` | **n**ot **eq**ual | 不等于【补充】 |
| `-lt` | **l**ess **t**han | 小于 |
| `-gt` | **g**reater **t**han | 大于 |
| `-le` | **l**ess or **e**qual | 小于等于 |
| `-ge` | **g**reater or **e**qual | 大于等于 |

```bash
[ $guess -eq $number ]     # guess 等于 number
[ $guess -lt $number ]     # guess 小于 number
[ $guess -gt $number ]     # guess 大于 number
```

### 7.3 字符串比较运算符【补充】

| 运算符 | 含义 |
|--------|------|
| `=` 或 `==` | 字符串相等 |
| `!=` | 字符串不相等 |
| `-z` | 字符串长度为 0（为空） |
| `-n` | 字符串长度非 0（非空） |

```bash
[ "$choice" = "y" ]        # 字符串相等用 =，而不是 -eq
[ -z "$name" ]             # name 为空字符串
[ "$a" != "$b" ]           # 不相等
```

> 注意：比较字符串用 `=`；`-eq` 只用于整数。判断一个变量"是数字还是字符串"没有类型之分，关键看你用什么运算符去比较。

### 7.4 文件测试运算符【补充】

运维脚本中非常常用，用来判断文件/目录的状态：

| 运算符 | 含义 |
|--------|------|
| `-e` | 文件/目录存在 |
| `-f` | 存在且为普通文件 |
| `-d` | 存在且为目录 |
| `-r` / `-w` / `-x` | 可读 / 可写 / 可执行 |
| `-s` | 存在且大小不为 0（非空文件） |

```bash
if [ -f /etc/passwd ]; then
    echo "这是一个存在的普通文件"
fi

if [ -d /tmp ]; then
    echo "/tmp 是一个目录"
fi
```

### 7.5 逻辑运算符

```bash
[ $a -lt 10 ] && [ $a -gt 0 ]          # 逻辑与：两个条件都成立
[ "$choice" = "y" ] || [ "$choice" = "Y" ]   # 逻辑或（两个竖线）：任一条件成立即可
[ ! -z "$name" ]                       # 逻辑非：条件取反
```

- **`&&`（与）**：两边都成立结果才成立；
- **`||`（或）**：只要有一个条件成立就成立——例如猜数字游戏中，用户输入 `y` **或** `Y` 都继续游戏；
- **`!`（非）**：条件取反。

**【补充】`&&` 和 `||` 还可以连接两条命令（短路执行）：**

```bash
mkdir /tmp/test && echo "创建成功"      # 前一条成功，才执行后一条
[ -f a.txt ] || touch a.txt             # a.txt 不存在时才创建它
```

---

## 八、条件判断 if

### 8.1 基本格式

```bash
if [ 条件 ]; then
    命令          # 条件成立时执行
fi
```

**⚠️ 语法要点（极其严格）：**

- **中括号 `[` 两边必须有空格**！写成 `[$guess -eq $number]` 会因为语法错误无法执行；
- `if` 后面是条件，条件用中括号括起来，后面加**分号 `;`** 和 **`then`**（分号的作用是把 then 拉到同一行，`then` 单独换行写时可以省略分号）；
- 以 **`fi`**（if 的倒写）结束整个 if 语句。

### 8.2 if - else

```bash
if [ $guess -eq $number ]; then
    echo "猜对了"
else
    echo "猜错了"
fi
```

### 8.3 if - elif - else（多分支）

在 `if` 和 `else` 分支之间加 `elif` 实现多分支判断：

```bash
if [ $guess -eq $number ]; then        # 先判断是否相等
    echo "恭喜你，猜对了！"
elif [ $guess -lt $number ]; then      # 小于随机数
    echo "猜小了！"
else                                   # 剩下的情况就是猜大了
    echo "猜大了！"
fi
```

### 8.4 case 多分支语句【补充】

当分支很多时，`case` 比 `elif` 更清晰，特别适合菜单、选项判断：

```bash
#!/bin/bash
read -p "请选择操作 (start/stop/restart): " action
case $action in
    start)
        echo "服务启动中..." ;;
    stop)
        echo "服务停止中..." ;;
    restart)
        echo "服务重启中..." ;;
    y|Y)                              # 多个模式可用竖线合并，如 y 或 Y
        echo "确认" ;;
    *)
        echo "无效的操作：$action" ;;   # * 类似 default，兜底分支
esac
```

- 每个分支以 `)` 结束，分支内的命令以 **双分号 `;;`** 结束；
- 整个语句以 `esac`（case 的倒写）结束。

### 8.5 `[ ]` 与 `[[ ]]` 的区别【补充】

视频提到"两个中括号"，实际 bash 中两者都存在：

```bash
[ $a -lt $b ]            # POSIX 标准写法，所有 Shell 通用
[[ $a < $b && $b < $c ]] # bash 扩展写法：支持 &&、||、<、>、=~ 正则匹配
```

| 对比项 | `[ ]`（test） | `[[ ]]` |
|--------|--------------|---------|
| 兼容性 | 所有 POSIX Shell | 仅 bash / zsh 等 |
| 逻辑组合 | 必须用 `-a`、`-o` 或分开写 | 可直接用 `&&`、`\|\|` |
| 变量不加引号 | 含空格时可能出错 | 不会分词，更安全 |

**建议**：写 bash 专用脚本用 `[[ ]]` 更省心；要兼顾 `sh` 执行就用 `[ ]`。无论用哪个，**中括号两边的空格都不能省**。

---

## 九、循环

Shell 脚本中有两种常用循环：**for 循环**和 **while 循环**。

- **for**：用来**遍历列表或数组**（遍历次数已知）；
- **while**：**只要条件成立就一直执行**（循环次数不确定）。

### 9.1 for 循环

**写法一：遍历列表（经典写法）**

```bash
for i in 1 2 3 4 5; do     # 依次取 1、2、3、4、5
    echo "第 $i 次循环"
done
```

**写法二：C 语言风格（用两个小括号把 3 个表达式括起来）**

这是 ChatGPT 生成素数脚本中用到的写法，和其他编程语言的 for 循环非常类似：

```bash
for (( i=2; i*i<=num; i++ )); do     # 初始化;条件;步进，格式与 C 语言一致
    echo $i
done
```

**【补充】常用变体：**

```bash
# 用 seq 生成数字序列：从 1 到 10
for i in $(seq 1 10); do echo $i; done

# 遍历某个目录下的所有 txt 文件（文件批量处理）
for f in *.txt; do
    echo "处理文件：$f"
done

# 遍历命令的输出结果（遍历当前目录的每一项）
for item in $(ls); do echo $item; done

# 遍历数组
fruits=("苹果" "香蕉" "橘子")
for f in "${fruits[@]}"; do
    echo $f
done
```

### 9.2 while 循环

```bash
while [ 条件 ]; do        # 条件成立时进入循环
    命令
done                      # done 表示循环体的结束
```

**示例：条件成立就一直循环（猜数字游戏的第一版）**

```bash
while [ $guess -ne $number ]; do    # 只要没猜对（guess 不等于 number）就循环
    echo "请输入一个 1 到 10 之间的数字："
    read guess
done
```

**无限循环：`while true`**

```bash
while true; do            # true 恒为真 → 无限循环
    ...
done
```

> ⚠️ 注意：**`true` 两边不需要加中括号**（true 本身是一条命令/关键字，不是 `[ ]` 里的判断表达式）。同理还有 `while :`（冒号是 true 的等价写法）【补充】。

### 9.3 until 循环【补充】

until 与 while 正好相反——**条件不成立时一直循环，条件成立才停止**：

```bash
until [ $guess -eq $number ]; do   # 直到猜对才结束
    read guess
done
```

### 9.4 break 与 continue

- **`break`**：立即**结束整个循环**；
- **`continue`**：**跳过当前这一次循环**，直接进入下一轮循环。

猜数字游戏中的用法：猜对后询问是否继续，选 y 就 `continue`（跳到下一轮，继续游戏），否则 `break`（结束游戏）：

```bash
while true; do
    # ...猜数字逻辑...
    if [ "$choice" = "y" ]; then
        continue      # 继续下一轮游戏
    else
        break         # 结束整个游戏
    fi
done
```

【补充】`break n` / `continue n` 可跳出/跳过第 n 层循环（默认 n=1）。

---

## 十、函数

### 10.1 函数的定义与调用

Shell 脚本支持函数，把一段逻辑封装起来反复调用：

```bash
# 方式一（function 关键字可以省略）
function greet() {
    echo "你好，$1"        # $1：函数的第一个参数
}

# 方式二
greet() {
    echo "你好，$1"
}

greet "老杨"               # 调用函数：函数名 + 参数（参数不加括号）
# 输出：你好，老杨
```

### 10.2 函数的参数

函数内同样使用 `$1`、`$2`…… 接收参数，`$#` 表示参数个数，`$?` 表示函数的返回状态。**注意：函数的 `$1` 与脚本自身的 `$1` 是两套体系，互不干扰。**

```bash
is_prime() {
    local num=$1          # 把函数的第一个参数保存到局部变量 num
    # ...判断逻辑...
}
```

### 10.3 local 局部变量（重要）

**Shell 脚本中的变量默认是全局的**——这一点和 C++、Java 等高级语言不一样：变量一旦定义，其作用域就是**从定义的地方开始，直到脚本结束**，即使在函数里定义的变量，函数外也能访问到。

想在函数中定义**局部变量**，需要在变量前加 **`local`** 关键字，这样它的作用域就只在函数内部有效：

```bash
myfunc() {
    local x=10        # 局部变量：只在函数内有效
    y=20              # 全局变量：函数执行完后依然存在
}
myfunc
echo $x               # 空的（函数外访问不到局部变量）
echo $y               # 20（全局变量可以在函数外访问）
```

### 10.4 函数的返回值【补充】

- `return` 只能返回 **0~255 的状态码**（`$?` 接收），通常 0 表示成功，非 0 表示失败——适合做"成功/失败"的判断；
- 若想把函数的**计算结果**传出来，标准做法是让函数 `echo` 结果，再用**命令替换**捕获：

```bash
add() {
    echo $(( $1 + $2 ))     # 把结果 echo 出来
}

sum=$(add 3 5)              # 命令替换捕获函数的输出
echo $sum                   # 8

# return 的正确用途：返回状态码
check_file() {
    [ -f "$1" ] && return 0 || return 1
}
check_file /etc/passwd
if [ $? -eq 0 ]; then echo "文件存在"; fi
```

---

## 十一、命令替换与随机数

### 11.1 命令替换：把命令的输出赋给变量

**问题现场：** 想把 `shuf` 生成随机数的结果赋给变量，直接写会报错"找不到 -i 这个命令"：

```bash
number=shuf -i 1-10 -n 1     # 错误！Shell 会把 shuf 之外的部分当成新命令
```

**原因与解法：** 当想把**一个命令的输出结果**赋给变量时，必须使用**命令替换**语法——用**反引号** `` ` `` 或 **`$( )`** 把命令括起来，Shell 才会把命令的输出结果当成一个整体来处理：

```bash
number=`shuf -i 1-10 -n 1`       # 反引号方式（老式写法）
number=$(shuf -i 1-10 -n 1)      # $() 方式（推荐）
echo $number
```

**建议尽量使用 `$( )` 这种更现代的方式**：可读性更好，而且支持嵌套，灵活性比反引号强：

```bash
# $() 可以嵌套，反引号嵌套需要转义、极易出错
echo "当前目录下有 $(ls | wc -l) 个文件"
today=$(date +%F)                 # 获取今天的日期，如 2026-09-04
```

### 11.2 生成随机数

**方法一：shuf 命令（专门生成随机数的命令）**

```bash
shuf -i 1-10 -n 1
# -i 1-10：指定生成范围是 1 到 10
# -n 1   ：只生成 1 个随机数
```

每次执行，输出的数字都会变。

**方法二：`$RANDOM` 系统变量**

`$RANDOM` 是 bash 内置的环境变量，**每次调用都会生成一个 0~32767 之间的随机整数**：

```bash
echo $RANDOM              # 例如 29174，每次都不同，范围 0~32767
```

想用 `$RANDOM` 生成 **1~10** 之间的随机数，需要配合**取模运算**（用 `$(( ))` 括起来才会整体计算）：

```bash
echo $((RANDOM % 10))     # 只取模得到的是 0~9（错误示范）
echo $((RANDOM % 10 + 1)) # 取模后 +1，才是 1~10 ✔
```

**通用公式【补充】：** 生成 `[a, b]` 范围的随机数：`$((RANDOM % (b-a+1) + a))`

---

## 十二、实战案例

### 12.1 交互式问候脚本（最简版）

```bash
#!/bin/bash
# game.sh —— 最简单的交互式脚本
echo "请输入您的姓名："     # 提示用户输入
read name                   # 读取输入并存入变量 name
echo "你好，$name！"         # 使用变量打印问候
```

执行：

```bash
chmod +x game.sh
./game.sh
# 请输入您的姓名：Kirk
# 你好，Kirk！
```

### 12.2 通过参数传值的版本

不能交互输入、或需要自动化执行时，用**位置参数**传值更合适：

```bash
#!/bin/bash
# game.sh —— 参数版
# read name                 # 注释掉交互读取（井号开头的行是注释）
name=$1                     # 第 1 个参数：姓名
channel=$2                  # 第 2 个参数：频道名
echo "你好，$name！欢迎来到 $channel 频道！"
```

执行：

```bash
./game.sh 老杨 老杨聊编程
# 你好，老杨！欢迎来到 老杨聊编程 频道！
```

### 12.3 素数判断脚本（ChatGPT 生成的教学示例）

这个脚本综合运用了**函数、局部变量、if 判断、C 风格 for 循环、read、算术运算**等知识点：

```bash
#!/bin/bash

# 判断一个数是否为素数的函数
is_prime() {
    local num=$1                  # local 定义局部变量，作用域仅限函数内
                                  # $1 是函数的第一个参数，即要检查的数字
    if [ $num -lt 2 ]; then       # -lt：小于。小于 2 的数（0、1、负数）都不是素数
        return 1                  # 返回 1 表示"不是素数"
    fi

    # C 风格 for 循环：i 从 2 遍历到 num 的平方根
    # 两个小括号把 3 个表达式括起来，格式严格
    # 只需检查到平方根，因为因子总是成对出现（如 12 = 2×6 = 3×4）
    for (( i=2; i*i <= num; i++ )); do
        if [ $((num % i)) -eq 0 ]; then   # num 能被 i 整除 → 不是素数
            return 1
        fi
    done
    return 0                      # 循环结束仍未被任何数整除 → 是素数
}

echo "请输入一个正整数："
read n                            # 读取用户输入

if is_prime $n; then              # 函数返回值（$?）为 0 即条件成立
    echo "$n 是一个素数"
else
    echo "$n 不是一个素数"
fi
```

执行效果：

```
bash prime.sh
请输入一个正整数：1
1 不是一个素数

bash prime.sh
请输入一个正整数：7
7 是一个素数
```

### 12.4 猜数字小游戏（完整最终版）

视频从头一步步搭建的完整案例，涵盖了本笔记的绝大部分知识点。完整代码与逐行注释：

```bash
#!/bin/bash
# ============ 猜数字小游戏 ============
# 随机生成 1~10 之间的一个数字，用户不断猜测；
# 猜错时提示"大了/小了"，猜对后可选择是否继续游戏

# 生成 1~10 的随机数：命令替换 $( ) 把 shuf 的输出赋给 number
number=$(shuf -i 1-10 -n 1)

while true; do                          # 无限循环（true 两边不加中括号）
    echo "请输入一个 1 到 10 之间的数字："
    read guess                          # 读取用户猜测的数字

    if [ $guess -eq $number ]; then     # -eq：等于 → 猜对了
        echo "恭喜你，猜对了！"
        echo "是否继续游戏？(y/n)"
        read choice                     # 读取用户的选择
        # 两个竖线 || 表示"或"：小写 y 或大写 Y 都继续游戏（处理大小写问题）
        if [ "$choice" = "y" ] || [ "$choice" = "Y" ]; then
            number=$((RANDOM % 10 + 1)) # 用 $RANDOM 重新生成随机数（取模+1 得 1~10）
            continue                    # 跳过本轮，开始新一局
        else
            break                       # 结束循环，退出游戏
        fi
    elif [ $guess -lt $number ]; then   # -lt：小于 → 猜小了
        echo "猜小了！"
    else                                # 剩下的情况 → 猜大了
        echo "猜大了！"
    fi
done

echo "游戏结束，再见！"
```

**搭建过程中的关键演进（学习思路）：**

1. **v1**：echo 提示 + read 读姓名 + echo 问候 —— 学会交互；
2. **v2**：改用 `$1`、`$2` 位置参数 —— 学会传参；
3. **v3**：`$(shuf ...)` 生成随机数 —— 学会命令替换（直接赋值会报错的原因与修复）；
4. **v4**：`if [ $guess -eq $number ]` 判断对错 —— 学会 if 与数值比较符；
5. **v5**：加 `elif -lt` / `else` 分支提示"大了/小了" —— 学会多分支；
6. **v6**：`while [ $guess -ne $number ]` 让用户一直猜 —— 学会 while；
7. **v7**：改成 `while true` + 猜对后询问 + `continue`/`break` —— 学会循环控制；
8. **v8**：`[ y ] || [ Y ]` 兼容大小写 —— 学会逻辑或；
9. **v9**：continue 前 `$((RANDOM % 10 + 1))` 重新生成随机数 —— 学会内置随机变量与算术运算。

---

## 十三、补充：教程未覆盖的重要内容

> 视频结尾提到 Shell 脚本还可以"配合 grep/awk/sed 做文本处理、使用函数和数组、进行系统管理和监控"，以下内容将这些缺口补全。

### 13.1 数组

bash 支持一维数组（下标从 0 开始）：

```bash
# 定义数组：用小括号，元素之间用空格分隔
fruits=("苹果" "香蕉" "橘子" "葡萄")

echo ${fruits[0]}            # 访问单个元素：苹果
echo ${fruits[@]}            # 访问所有元素
echo ${#fruits[@]}           # 数组长度（元素个数）：4
echo ${#fruits[0]}           # 单个元素的字符长度：2

fruits[1]="香蕉2"            # 修改元素
fruits[4]="西瓜"             # 追加元素
unset fruits[2]              # 删除元素

# 遍历数组
for f in "${fruits[@]}"; do
    echo "水果：$f"
done

# 【补充】关联数组（类似其他语言的字典/Map），bash 4.0+
declare -A score
score["数学"]=95
score["英语"]=88
echo ${score["数学"]}        # 95
for key in "${!score[@]}"; do       # ${!arr[@]} 取所有键
    echo "$key: ${score[$key]}"
done
```

### 13.2 字符串处理

Shell 内置了丰富的字符串操作（不用记全，用到时查）：

```bash
str="Hello Shell"

echo ${#str}                 # 字符串长度：11

echo ${str:6}                # 从下标 6 截取到结尾：Shell
echo ${str:0:5}              # 从下标 0 截取 5 个字符：Hello

echo ${str#Hello}            # 删除开头最短匹配 Hello → " Shell"
echo ${str##*o}              # 删除开头最长匹配 *o → " Shell"
echo ${str%Shell}            # 删除结尾最短匹配 Shell → "Hello "
echo ${str%%l*}              # 删除结尾最长匹配 l* → "He"

echo ${str/Shell/Bash}       # 替换第一个匹配：Hello Bash
echo ${str//l/L}             # 替换所有匹配：HeLLo SheLL

echo ${str,,}                # 全部转小写：hello shell【bash 4.0+】
echo ${str^^}                # 全部转大写：HELLO SHELL【bash 4.0+】
```

### 13.3 重定向与管道

**标准流：** 每个命令都有三个标准流——标准输入（stdin，0）、标准输出（stdout，1）、标准错误（stderr，2）。

**输出重定向：**

```bash
echo "hello" > out.txt       # > 覆盖写入文件（原内容清空）
echo "world" >> out.txt      # >> 追加写入文件（原内容保留）
ls /not_exist 2> err.log     # 2> 只把【错误输出】重定向到文件
ls /not_exist > all.log 2>&1 # 标准输出和错误输出都写入同一文件
ls /not_exist &> all.log     # 同上的简写【补充】
command > /dev/null 2>&1     # 丢弃所有输出（/dev/null 是"黑洞"设备）
```

**输入重定向：**

```bash
wc -l < /etc/passwd          # < 从文件读取标准输入
mysql -u root < init.sql     # 典型用法：把 SQL 脚本喂给 mysql
```

**Here Document（多行文本块）【补充】：**

```bash
cat << EOF
第一行
第二行
EOF
```

**管道 `|`：** 把前一个命令的**标准输出**作为后一个命令的**标准输入**，把多个简单命令组合成强大功能：

```bash
cat /etc/passwd | grep bash          # 找出使用 bash 的用户
ps aux | grep nginx                  # 查找 nginx 进程
history | tail -10                   # 最近 10 条历史命令
cat access.log | grep "404" | wc -l  # 统计日志中 404 出现次数
```

### 13.4 文本三剑客：grep / sed / awk

**grep —— 按行查找过滤：**

```bash
grep "root" /etc/passwd              # 在文件中查找包含 root 的行
grep -i "error" app.log              # -i 忽略大小写
grep -n "main" test.sh               # -n 显示行号
grep -r "TODO" ./src                 # -r 递归搜索目录
grep -v "^#" /etc/ssh/sshd_config    # -v 反选：排除以 # 开头的注释行
grep -E "^[0-9]+" data.txt           # -E 支持扩展正则表达式
ps aux | grep nginx                  # 配合管道过滤进程
```

**sed —— 流编辑器（替换、删除、插入）：**

```bash
sed 's/old/new/' file.txt            # 把每行第一个 old 替换为 new（只显示，不改文件）
sed 's/old/new/g' file.txt           # g：替换每行所有的 old
sed -i 's/old/new/g' file.txt        # -i：直接修改文件本身（谨慎使用）
sed -n '10p' file.txt                # 只打印第 10 行
sed '3d' file.txt                    # 删除第 3 行
sed '/^$/d' file.txt                 # 删除所有空行
```

**awk —— 按列处理文本（默认按空格分列，$1 第 1 列……）：**

```bash
awk '{print $1, $3}' file.txt        # 打印每行的第 1、3 列
awk -F: '{print $1}' /etc/passwd     # -F: 指定冒号为分隔符，打印用户名列
df -h | awk '{print $5}'             # 打印磁盘使用率列
ps aux | awk '{sum += $3} END {print sum}'   # 统计所有进程 CPU 之和
awk '$3 > 90 {print $1}' score.txt   # 条件过滤：第 3 列大于 90 时打印第 1 列
```

**三剑客联用示例——统计日志中访问量最高的 10 个 IP：**

```bash
awk '{print $1}' access.log | sort | uniq -c | sort -rn | head -10
# 提取第1列IP → 排序 → 去重并计数 → 按次数倒序 → 取前10
```

### 13.5 定时任务 crontab（呼应视频开头的"凌晨自动备份"）

视频开头说"凌晨自动备份数据、定时清理日志"是脚本的核心用途，但没讲怎么定时执行，补上 **crontab**：

```bash
crontab -e                 # 编辑当前用户的定时任务
crontab -l                 # 列出已有任务
```

任务格式（5 个时间字段 + 命令）：

```
分 时 日 月 周  要执行的命令
*  *  *  *  *
30 2  *  *  *  /home/user/backup.sh    # 每天凌晨 2:30 执行备份脚本
*/10 * * * *  /home/user/check.sh      # 每 10 分钟执行一次检查
0 8 * * 1-5   /home/user/report.sh     # 工作日每天早上 8 点执行
```

### 13.6 脚本调试与健壮性【补充】

**调试：**

```bash
bash -n script.sh          # 语法检查，不真正执行
bash -x script.sh          # 逐行打印实际执行的命令，排查逻辑问题
```

**让脚本更健壮（推荐加在脚本开头）：**

```bash
#!/bin/bash
set -e         # 遇到任何命令失败（非0退出码）立即终止脚本
set -u         # 使用未定义的变量时报错（而不是当成空字符串）
set -o pipefail # 管道中任何一个命令失败，整条管道算失败
# 三个一起用的简写：set -euo pipefail
```

**其他实用细节：**

```bash
# 严格模式下的参考写法
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'
```

### 13.7 实用小技巧集【补充】

```bash
basename /etc/passwd       # passwd —— 提取文件名
dirname /etc/passwd        # /etc —— 提取目录名
command -v git             # 查看命令的安装路径
type ll                    # 查看命令类型（别名/内建/文件）
date +%F                   # 2026-09-04，日期格式化
date +%s                   # 时间戳（秒）
sleep 5                    # 暂停 5 秒
seq 1 10                   # 生成 1~10 的序列
wc -l file.txt             # 统计行数
cut -d: -f1 /etc/passwd    # 按冒号分隔取第 1 列
sort / uniq -c / head -n   # 排序 / 去重计数 / 取前 n 行
tr 'a-z' 'A-Z' < file      # 小写转大写
find / -name "*.log"       # 按名称查找文件
xargs                      # 把输入转成命令参数：cat list.txt | xargs rm
```

**脚本开头通用模板（企业常用）：**

```bash
#!/bin/bash
# 描述：本脚本的用途
# 作者：xxx  日期：2026-09-04
set -euo pipefail

LOG_FILE="/var/log/myapp.log"       # 配置变量集中放前面

log() {                             # 简单的日志函数
    echo "[$(date '+%F %T')] $*" >> "$LOG_FILE"
}

main() {                            # 主逻辑封装成函数
    log "脚本开始执行"
    # ... 具体逻辑 ...
    log "脚本执行完成"
}

main "$@"                           # 调用主函数并透传所有参数
```

---

## 十四、常见坑速查表

| 坑 | 错误写法 | 正确写法 |
|----|---------|---------|
| 赋值等号两边加空格 | `name = "老杨"` | `name="老杨"` |
| if 中括号内没空格 | `[$a -eq $b]` | `[ $a -eq $b ]` |
| if 后忘记 then / fi | — | `if ...; then ... fi` |
| 比较数字用了 `=` | `[ $a = $b ]` | `[ $a -eq $b ]`（字符串才用 `=`） |
| 命令输出直接赋值 | `n=shuf -i 1-10 -n 1` | `n=$(shuf -i 1-10 -n 1)` |
| 算术不加双括号 | `echo $RANDOM % 10 + 1` | `echo $((RANDOM % 10 + 1))` |
| 修改 .bashrc 不生效 | 改完直接用 | `source ~/.bashrc` 或重新登录 |
| 命令行变量脚本里取不到 | `name=xx` | `export name=xx`（导出环境变量） |
| `./xx.sh` 提示 Permission denied | 直接执行 | `chmod +x xx.sh` 后再执行 |
| 字符串比较变量没加引号 | `[ $str = "a b" ]` | `[ "$str" = "a b" ]`（防变量含空格/为空时报错） |
| 无限循环写成了 `[ true ]` | `while [ true ]` | `while true`（true 两边不要中括号） |
| while 条件里变量未初始化就 `-ne` | — | 先给 guess 赋初值，或先 read 再进循环 |

---

## 十五、常用命令速查表

| 命令 | 作用 | 常用示例 |
|------|------|---------|
| `echo` | 打印输出 | `echo $SHELL` |
| `cat` | 查看文件内容 | `cat /etc/shells` |
| `ls` / `ls -a` | 列目录 / 含隐藏文件 | `ls -a ~` |
| `chmod` | 修改权限 | `chmod +x hello.sh` |
| `date` | 日期时间 | `date +%F` |
| `whoami` | 当前用户 | — |
| `read` | 读取输入 | `read -p "提示" name` |
| `export` | 导出环境变量 | `export name="老杨"` |
| `source` | 重新加载配置 | `source ~/.bashrc` |
| `alias` | 定义别名 | `alias ll='ls -l'` |
| `shuf` | 生成随机数 | `shuf -i 1-10 -n 1` |
| `$RANDOM` | 内置随机数变量 | `$((RANDOM % 10 + 1))` |
| `env` / `printenv` | 查看所有环境变量【补充】 | `env` |
| `grep` | 文本过滤 | `grep -n "main" a.sh` |
| `sed` | 文本替换 | `sed -i 's/a/b/g' f.txt` |
| `awk` | 按列处理 | `awk -F: '{print $1}' /etc/passwd` |
| `crontab` | 定时任务【补充】 | `crontab -e` |
| `bash -x` | 调试脚本【补充】 | `bash -x game.sh` |

---

## 附：核心知识点一句话总结

- **Shell** 是命令行解释器，是用户与内核之间的翻译官；
- 脚本第一行 **`#!/bin/bash`** 叫 Shebang，声明解释器；
- 执行脚本两条路：**`chmod +x` 后 `./xx.sh`**，或直接 **`bash xx.sh`**；
- **`$1 $2`** 收参数，**`$#`** 参数个数，**`$?`** 上条命令返回值，**`$0`** 脚本名；
- 普通变量只在当前 Shell 有效，**`export`** 后才能被子进程（脚本）继承，永久生效要写进 **`~/.bashrc`** 并 **`source`**；
- 数值比较用 **`-eq -ne -lt -gt -le -ge`**，文件判断用 **`-f -d -e`**，字符串用 **`= != -z -n`**；
- **if [ ... ]; then ... elif ... else ... fi**，中括号两边必须有空格；
- **for** 遍历列表，**while** 条件循环，**break** 跳出 **continue** 跳过；
- 函数内 **`local`** 定义局部变量，Shell 变量默认全局；
- 命令输出赋值用命令替换 **`$( )`**（优于反引号），算术运算用 **`$(( ))`**；
- 随机数：**`shuf -i 1-10 -n 1`** 或 **`$((RANDOM % 10 + 1))`**。

---

*笔记完 · 基于视频内容整理并系统化补充 · 2026-09-04*
