# Linux 学习笔记

> **资料来源**：GeekHour《30 分钟 Linux 入门教程》(BV1cq421w72c) 字幕整理
> **整理方式**：按教程章节顺序梳理知识点，并对教程**未涉及或讲得不够完整**的部分做系统补充（补充内容统一标注为「补充」）
> **适用人群**：Linux 零基础 / 需要一份可随时查阅的命令手册的开发者与运维人员
> **演示环境**：Ubuntu 22.04 LTS（命令同样适用于绝大多数发行版，包管理器部分略有差异）

---

## 目录

- [第一部分　Linux 基础概念](#第一部分-linux-基础概念)
- [第二部分　环境搭建](#第二部分-环境搭建)
- [第三部分　Vim 编辑器](#第三部分-vim-编辑器)
- [第四部分　文件系统与目录结构](#第四部分-文件系统与目录结构)
- [第五部分　文件与目录操作命令](#第五部分-文件与目录操作命令)
- [第六部分　文件权限管理](#第六部分-文件权限管理)
- [第七部分　硬链接与软链接](#第七部分-硬链接与软链接)
- [第八部分　重定向与管道](#第八部分-重定向与管道补充)
- [第九部分　文本查看与处理三剑客](#第九部分-文本查看与处理三剑客补充)
- [第十部分　文件查找与搜索](#第十部分-文件查找与搜索补充)
- [第十一部分　压缩与归档](#第十一部分-压缩与归档补充)
- [第十二部分　软件包管理](#第十二部分-软件包管理补充)
- [第十三部分　用户与组管理](#第十三部分-用户与组管理补充)
- [第十四部分　进程与作业管理](#第十四部分-进程与作业管理补充)
- [第十五部分　系统信息与资源监控](#第十五部分-系统信息与资源监控补充)
- [第十六部分　网络与远程连接](#第十六部分-网络与远程连接补充)
- [第十七部分　Shell 脚本编程](#第十七部分-shell-脚本编程补充)
- [第十八部分　服务管理与计划任务](#第十八部分-服务管理与计划任务补充)
- [附录 A　命令速查表](#附录-a-命令速查表)
- [附录 B　Vim 速查表](#附录-b-vim-速查表)
- [附录 C　终端快捷键与常见坑](#附录-c-终端快捷键与常见坑)

---

## 第一部分 Linux 基础概念

### 1.1 什么是 Linux

Linux 是一种**开源、免费使用的类 Unix 操作系统**。

- 内核由 **Linus Torvalds（林纳斯·托瓦兹）** 于 **1991 年**首次发布。
- Linux 这个名字就来自于作者的名字 **Linus**。
- Linus 同时也是 **Git** 分布式版本控制系统的作者（2005 年，因 BitKeeper 收回免费授权，他花两周写出 Git 原型）。

> **补充：严格来说 Linux 只是「内核」**
> 我们日常说的「Linux 系统」，准确叫法是 **GNU/Linux**：
> - **Linux 内核（kernel）**：Linus Torvalds 维护，负责管理硬件
> - **GNU 项目组件**（Richard Stallman 1983 年发起）：gcc 编译器、bash shell、coreutils（`ls`/`cp`/`cat` 等命令）、glibc 库等
>
> 内核 + GNU 工具 + 应用软件 = 一个可用的操作系统。所以自由软件基金会（FSF）一直倡导称之为 GNU/Linux。

### 1.2 GPL 协议与开源

只要遵循 **GNU 通用公共许可证（GPL，GNU General Public License）**：

- 任何人和机构都可以**自由使用** Linux 的全部底层源代码
- 可以**自由修改**
- 可以**自由再发布**

GPL 的核心特性叫 **Copyleft（著佐权）**：**基于 GPL 代码的衍生作品，发布时也必须同样以 GPL 开源**。这是它与 MIT / Apache / BSD 等「宽松许可证」最大的区别 —— 后者允许你把代码改一改就闭源商用。

| 许可证 | 能否闭源商用 | 是否要求衍生作品开源 | 典型项目 |
| --- | --- | --- | --- |
| **GPL / LGPL** | 可以商用 | **必须**以相同协议开源 | Linux 内核、Git、GCC |
| **MIT** | 可以 | 不要求，保留版权声明即可 | Vue、React、Node.js |
| **Apache 2.0** | 可以 | 不要求，但需声明修改与专利授权 | Android、Kubernetes、Hadoop |
| **BSD** | 可以 | 不要求 | FreeBSD、Nginx（早期） |

> Linux 是**开源软件发展史上最著名的例子**：它证明了全球数千名互不相识、分散在各大公司的开发者，仅凭互联网协作，就能做出比顶级商业公司更好的产品。

### 1.3 Linux 系统架构（四层结构）

Linux 是一个**多层次结构**，自下而上包含：

```
┌──────────────────────────────────────────────────┐
│              应用程序 (Applications)              │  ← 浏览器、编辑器、Nginx、MySQL…
├──────────────────────────────────────────────────┤
│                  Shell (外壳)                     │  ← bash / zsh / fish，命令解释器
├──────────────────────────────────────────────────┤
│              系统库 (System Libraries)            │  ← glibc(C 标准库)、openssl…
├──────────────────────────────────────────────────┤
│                 内核 (Kernel)                     │  ← 驱动、进程、内存、文件系统、网络协议栈
├──────────────────────────────────────────────────┤
│                  硬件 (Hardware)                  │  ← CPU、内存、磁盘、网卡
└──────────────────────────────────────────────────┘
```

| 层次 | 说明 | 关键职责 / 举例 |
| --- | --- | --- |
| **内核 Kernel** | 系统的核心与基础 | 设备驱动程序、进程管理、内存管理、文件系统、网络协议栈 |
| **系统库** | 支撑应用程序开发的软件库 | 提供常用函数与接口，如 C 语言标准库 `glibc` |
| **Shell** | 命令行解释器（「壳」） | 接收用户命令 → 传递给操作系统执行。是用户使用 Linux 的接口 |
| **应用程序** | 日常使用的软件 | 桌面：浏览器/编辑器/办公软件；服务器：Nginx、MySQL、Redis、Docker |

**Shell 名字的由来**：相对于「内核（kernel，内壳）」，Shell 就是套在内核外面的一层壳 —— 你摸不到内核，只能通过这层壳去跟它打交道。

> **补充：内核态与用户态**
> CPU 有两种运行级别：
> - **内核态（Kernel Mode / Ring 0）**：内核代码运行，可执行所有指令、访问所有硬件
> - **用户态（User Mode / Ring 3）**：应用程序运行，权限受限，不能直接操作硬件
>
> 应用程序想读写磁盘、发网络包，必须通过**系统调用（syscall，如 `open`/`read`/`write`/`fork`）** 陷入内核态由内核代劳。这也是为什么「内核崩溃 = 整机死机（kernel panic）」，而「某个应用崩溃」只是那一个程序退出。
>
> 常见 Shell：`sh`（Bourne Shell，最原始）、`bash`（Bourne Again Shell，**绝大多数 Linux 默认**）、`zsh`（macOS 默认，功能更强，配合 oh-my-zsh）、`fish`（对新手最友好）。
> 查看当前 Shell：`echo $SHELL`；查看系统可用 Shell：`cat /etc/shells`

### 1.4 Linux 发行版（Distribution）

**发行版 = Linux 内核 + 软件包 + 系统工具 + 库文件 + 安装程序**，构成一个开箱即用的完整操作系统。

每个发行版都有自己的**包管理器、桌面环境和特定工具**，选择取决于使用场景与偏好。

| 发行版 | 基础 | 包管理器 | 特点与适用场景 |
| --- | --- | --- | --- |
| **Ubuntu** | Debian | `apt` / `dpkg` | 最流行、资料最多、容易上手，**适合个人桌面与入门**（本教程使用） |
| **Debian** | — | `apt` / `dpkg` | 极致稳定、软件包偏保守，服务器常用 |
| **CentOS / Rocky / AlmaLinux** | RHEL | `yum` / `dnf` / `rpm` | 企业级服务器首选，主打长期稳定（CentOS 已转向 Stream 滚动版，生产可用 Rocky/Alma 替代） |
| **RHEL** | — | `dnf` | Red Hat 商业发行版，需付费订阅 |
| **Kali Linux** | Debian | `apt` | **网络安全与渗透测试**，预装数百款安全工具 |
| **Alpine** | — | `apk` | **体积极小**（基础镜像约 5MB），**容器化应用首选** |
| **Arch Linux** | — | `pacman` | 滚动更新、极简可定制、AUR 仓库丰富，适合进阶用户 |
| **openSUSE** | — | `zypper` | 欧洲企业常用，YaST 配置工具强大 |
| **Fedora** | — | `dnf` | Red Hat 上游试验田，新技术尝鲜 |

> **重点**：无论选择哪个发行版，它们**都基于同一个 Linux 内核**，所以**基础命令和操作完全一样**。学会一套，发行版之间切换几乎没有成本。

> **补充：如何选择？**
> - 想学 Linux、做开发/部署 → **Ubuntu / Debian**
> - 公司服务器、考 RHCE、追求稳定 → **Rocky Linux / AlmaLinux / RHEL**
> - 想深入原理、自己从零搭系统 → **Arch / Gentoo / LFS**
> - 做安全 / CTF → **Kali**
> - 做容器镜像 → **Alpine**（注意：Alpine 用 musl libc 而非 glibc，部分二进制程序可能不兼容）

---

## 第二部分 环境搭建

在本地电脑上使用 Linux，常见有 5 类方案：

| 方案 | 优点 | 缺点 | 推荐度 |
| --- | --- | --- | --- |
| **虚拟机**（VMware / VirtualBox / Multipass / Parallels / UTM） | 不影响现有系统、可随时开关、可快照回滚 | 占用资源、性能有损耗 | 强烈推荐 |
| **WSL**（Windows Subsystem for Linux） | 与 Windows 深度集成、启动秒级、文件互通 | 无图形界面（WSL2 可配）、部分内核功能受限 | Windows 用户推荐 |
| **Docker 容器** | 一条命令启动、秒级创建销毁、环境隔离 | 不是完整系统（无 systemd），不适合练系统管理 | 适合快速验证 |
| **云服务器**（阿里云 / 腾讯云 / 华为云等） | 系统预装好、有公网 IP、随时随地访问 | 需要付费 | 做真实项目部署推荐 |
| **双系统 / 直接安装** | 性能最好、原生体验 | 安装配置麻烦、**切换系统要重启** | 不推荐新手 |

### 2.1 虚拟机工具选型

| 平台 | 推荐工具 | 说明 |
| --- | --- | --- |
| Windows | **VMware Workstation / VirtualBox** | 成熟、流行、图形界面友好，新建虚拟机 → 选镜像 → 一路下一步即可 |
| Windows | **WSL / WSL2** | Windows 官方的 Linux 子系统，非常方便 |
| macOS | **Multipass** | 轻量、极快、**支持命令行操作**，可脚本化批量创建虚拟机（如一条脚本搭多节点 Kubernetes 集群）。缺点：默认只支持 Ubuntu 镜像 |
| macOS | **Parallels Desktop（PD）** | 收费软件，mac 上常用的虚拟机，最典型场景是**在 Mac 上安装 Windows**（过渡使用习惯，或运行 Windows 独占软件，如逆向工程工具 IDA） |
| macOS | **UTM** | 基于 QEMU，**可模拟多种 CPU 架构**（x86、ARM、MIPS…）。适合在 M 系列 Mac 上跑 CTF 二进制题目（几乎都是 x86 架构）。缺点：模拟架构性能损耗大 |

> **补充：为什么需要模拟不同 CPU 架构？**
> 不同架构的**指令集不同**，编译出来的二进制不能通用。最典型的就是苹果 M 系列芯片（ARM 架构）刚发布时，很多 x86 软件无法直接运行，需要厂商重新发布 ARM 版本（现在主流软件官网基本都同时提供 x86 与 Apple Silicon 两个版本）。
> 但仍有刚需场景：CTF 比赛的二进制漏洞挖掘题几乎都是 x86 架构 —— 主力机是 M 系列 Mac 时，UTM 就是最佳选择。
> 如果**没有跨架构需求**，老老实实用 VMware / VirtualBox / Multipass，性能损耗最小。

### 2.2 Multipass 快速上手（macOS / Windows）

官网 `https://multipass.run` → 点击 **Install Now** → 下载对应系统安装包 → 安装。

```bash
# 创建并启动一台 Ubuntu 虚拟机
multipass launch --name ubuntu --cpus 2 --memory 2G --disk 20G

# 查看虚拟机列表
multipass list

# 进入虚拟机（ubuntu 是虚拟机名）
multipass shell ubuntu

# 停止 / 启动 / 删除
multipass stop ubuntu
multipass start ubuntu
multipass delete ubuntu      # 标记删除
multipass purge              # 彻底清除已删除的虚拟机

# 在宿主机直接执行虚拟机内的命令（不进入交互 shell）
multipass exec ubuntu -- ls -l /home
```

参数说明：

| 参数 | 含义 |
| --- | --- |
| `--name` | 虚拟机名字 |
| `--cpus` | 分配的 CPU 核心数 |
| `--memory` | 内存大小（如 `2G`） |
| `--disk` | 磁盘大小（如 `20G`） |

### 2.3 手动安装（VMware + Ubuntu ISO）

1. 打开 Ubuntu 官网 `https://ubuntu.com` → 点击 **Get Ubuntu** → **Download**
2. 等待弹出保存对话框，下载 ISO 镜像文件
3. 打开 VMware → **新建虚拟机** → 选择「安装程序光盘映像文件(iso)」→ 选中刚下载的镜像
4. 一路「下一步」即可

> **补充：VMware 安装后的必要操作**
> - 安装 **open-vm-tools**，才能实现宿主机与虚拟机之间复制粘贴、拖放文件、自适应分辨率：
>   ```bash
>   sudo apt update && sudo apt install -y open-vm-tools open-vm-tools-desktop
>   ```
> - 网络模式建议选 **NAT**（虚拟机可上网，IP 稳定）；需要局域网其他机器访问时选**桥接模式**
> - 装完先做一次**快照（Snapshot）**，之后玩坏了可以一键回滚

> **补充：其他几条实用路径**
> - **WSL2 安装（Windows，管理员 PowerShell 一行搞定）**：
>   ```powershell
>   wsl --install                 # 默认装 Ubuntu
>   wsl --list --online           # 查看可安装的发行版
>   wsl --install -d Ubuntu-22.04
>   ```
> - **Docker 跑一个 Linux**：
>   ```bash
>   docker run -it --name myubuntu ubuntu:22.04 /bin/bash
>   ```
> - **云服务器**：阿里云 / 腾讯云 / 华为云的「轻量应用服务器」，学生机通常几十元一年，还带公网 IP，适合练手真实部署

---

## 第三部分 Vim 编辑器

### 3.1 为什么要学 Vim

VS Code 很方便，但在**服务器环境**中通常：

- 没有图形界面
- 没有 VS Code 这类图形化编辑器
- 只能通过命令行操作

典型场景：**线上服务出故障 → 需要立刻查看日志排查 → 定位到错误行 → 修改配置文件**。如果等把日志下载到本地再用 VS Code 打开，可能已经错过最佳抢救时机。

> 所以无论开发还是运维，**都强烈建议掌握 Vim**。

### 3.2 VI 与 VIM 的关系

| 名称 | 说明 |
| --- | --- |
| **VI** | Unix 系统下的经典文本编辑器（1976 年，Bill Joy） |
| **VIM** | **Vi IMproved**（VI 增强版），在 VI 基础上增加了语法高亮、多级撤销、多窗口、插件系统、可视模式等 |

- 使用方法**完全一样**
- Linux 系统上一般装的是 VIM，命令行输入 `vi` 通常也会直接启动 vim
- 输入 `vi` 或 `vim` 回车进入界面，可看到版本号与帮助信息
  - 输入 `:help` 查看帮助
  - 输入 `:q` 退出

```bash
vim              # 直接打开 vim
vim hello.txt    # 打开/新建 hello.txt（文件不存在则创建）
```

### 3.3 三种常用模式

Vim 的核心难点就是**模式**。常用三种（另有替换模式、可视模式等，见本节末尾补充）：

```
                    i / I / a / A / o / O
      ┌──── 命令模式 (Normal) ────────────► 插入模式 (Insert) ─┐
      │          ▲                                            │
      │          │  ESC                                       │
      │          └────────────────────────────────────────────┘
      │  :
      ▼
  尾行模式 / 末行模式 (Command-line)  ←  ESC 或执行命令后回到命令模式
```

| 模式 | 别名 | 进入方式 | 作用 |
| --- | --- | --- | --- |
| **命令模式** | Normal Mode | 打开文件后**默认进入**；任何其他模式下按 `ESC` 返回 | 浏览内容、复制粘贴、查找、删除、移动光标 |
| **插入模式** | Insert Mode | 命令模式下按 `i` `I` `a` `A` `o` `O` | 编辑 / 输入文本 |
| **尾行模式** | 末行模式 / 命令行模式 | 命令模式下输入 `:`（冒号是前缀） | 保存、退出、替换、设置（如 `:set number`） |

> **口诀**：想打命令，先按 `ESC`；想打字，按 `i`；想存盘退出，`:wq`。

#### 进入插入模式的 6 种方式

| 键 | 全称 | 效果 |
| --- | --- | --- |
| `i` | insert | 在**当前光标位置前**插入 |
| `I` | 大写 i | 在**当前行的行首**插入 |
| `a` | append | 在**当前光标位置后**插入 |
| `A` | 大写 a | 在**当前行的行尾**插入 |
| `o` | open | 在**当前行的下一行**插入新行 |
| `O` | 大写 o | 在**当前行的上一行**插入新行 |

> 记忆法：小写 = 光标局部（前/后/下）；大写 = 行级别（行首/行尾/上）。

#### 保存与退出

| 命令 | 作用 |
| --- | --- |
| `:w` | 保存（write） |
| `:w filename` | 另存为 filename |
| `:q` | 退出（quit，未修改时） |
| `:q!` | **强制退出，不保存修改** |
| `:wq` | 保存并退出 |
| `:x` | 保存并退出（等价 `:wq`，但文件未改动时不更新 mtime，更优） |
| `ZZ` | 命令模式下直接保存退出（等价 `:x`） |
| `:e!` | 放弃所有修改，重新载入文件 |

### 3.4 光标移动

| 键 | 效果 | 记忆 |
| --- | --- | --- |
| `h` | 左移一个字符 | 最左边 = 左 |
| `l` | 右移一个字符 | 最右边 = 右 |
| `j` | 下移一行 | 扑克牌 J < K，J = **下** |
| `k` | 上移一行 | K = **上** |

> `hjkl` 在键盘右手区相邻位置，手指不用离开主行区，熟练后比方向键快得多。
> 记不住也没关系，**方向键上下左右效果完全一样**。

**行内跳转**：

| 键 | 效果 |
| --- | --- |
| `^` | 跳到**行首**（第一个非空白字符） |
| `0`（数字零） | 跳到**行首第一列**（绝对行首） |
| `$` | 跳到**行尾** |

> `^` 和 `$` 在其他场景（正则表达式、查找替换）中也常用来表示**开头**和**结尾**。

**翻页**（想象你在看一本书）：

| 键 | 全称 | 效果 |
| --- | --- | --- |
| `Ctrl + f` | forward | 向前（往下）翻一整页 |
| `Ctrl + b` | backward | 向后（往上）翻一整页 |
| `Ctrl + d` | down | 向下翻半页 |
| `Ctrl + u` | up | 向上翻半页 |

**跳转指定行**：

| 键 | 效果 |
| --- | --- |
| `G`（大写） | 跳到**文件最后一行** |
| `gg`（两次小写 g） | 跳到**文件第一行** |
| `100G` | 跳到第 100 行 |
| `:50` + 回车 | 跳到第 50 行（效果同上） |
| `H` / `M` / `L` | 跳到当前屏幕的**顶部** / **中间** / **底部**（High / Middle / Low） |

### 3.5 复制、粘贴、删除

| 键 | 效果 | Windows 类比 |
| --- | --- | --- |
| `yy` | 复制当前行 | Ctrl + C |
| `p` | 粘贴到**光标所在行的下一行** | Ctrl + V |
| `P`（大写） | 粘贴到**光标所在行的上一行** | — |
| `dd` | 删除（剪切）当前行 | Ctrl + X |
| `x` | 删除光标所在字符 | Delete |
| `D` | 删除从光标到行尾的内容 | — |

> `dd` 删除的内容**同样可以用 `p` 粘贴回来** —— 它本质是「剪切」。
> 每按一次 `p` 就粘贴一次，所以 `3p` 会粘贴 3 次。

**数字前缀 = 重复次数**（Vim 的通用语法：**数字 + 命令**）：

```bash
2yy     # 复制 2 行（从当前行开始）
3p      # 把刚复制的内容粘贴 3 次
100p    # 粘贴 100 次
5dd     # 删除 5 行
10j     # 光标下移 10 行
```

> **补充：更精细的复制 / 删除对象**
>
> | 命令 | 效果 |
> | --- | --- |
> | `yw` | 复制一个单词（word） |
> | `y$` | 复制到行尾 |
> | `y0` | 复制到行首 |
> | `yG` | 复制到文件末尾 |
> | `ygg` | 复制到文件开头 |
> | `dw` | 删除一个单词 |
> | `d$`（即 `D`） | 删除到行尾 |
> | `dG` | 删除到文件末尾 |
> | `dgg` | 删除到文件开头 |
> | `diw` | 删除光标所在单词（不含空格） |
> | `di"` | 删除双引号内的内容（`(` `[` `{` 同理，改配置极方便） |
> | `ciw` / `ci"` | 同上，但删除后**直接进入插入模式**（c = change） |

### 3.6 行号与显示设置

```bash
:set number       # 显示行号
:set nonumber     # 关闭行号
:set nu           # 缩写，等价 :set number
:set nonu         # 缩写，等价 :set nonumber
```

> 内容全是一模一样的重复行时，**打开行号**才能看清光标位置和文件长度。

### 3.7 查找

```bash
/hello      # 从光标位置开始向【下】查找 hello
?hello      # 从光标位置开始向【上】查找 hello
n           # 继续查找【下一个】（next，方向 = 当前查找方向）
N           # 继续查找【上一个】（方向与 n 相反）
```

- `/` 向下查找时，按 `n` 继续向下，按 `N` 向上
- `?` 向上查找时，按 `n` 继续向上，按 `N` 向下

**大小写敏感**：默认**区分大小写**，查找小写 `hello` 匹配不到驼峰的 `Hello`。

```bash
/hello\c          # 在查找内容后加 \c，本次查找忽略大小写
:set ignorecase   # 全局忽略大小写（缩写 :set ic）
:set noignorecase # 恢复区分大小写（缩写 :set noic）
:set smartcase    # 智能大小写：全小写则忽略大小写，含大写则严格匹配（推荐）
:set hlsearch     # 高亮所有匹配项（缩写 :set hls）
:nohlsearch       # 临时取消高亮（缩写 :noh），下次查找时重新高亮
:set incsearch    # 输入时即时高亮（边打边跳，很爽）
```

> **补充：快速查找当前单词**
> - `*` ：向下查找光标所在的单词（自动加单词边界）
> - `#` ：向上查找光标所在的单词
>
> 改变量名、看某个函数在哪被调用时，比手打 `/xxx` 快得多。

### 3.8 替换

替换的**通用格式**：

```
:[范围]s/查找内容/替换内容/[g][c]
```

- 范围用逗号分隔的两个数字表示 `起始行,结束行`；**省略范围 = 只替换当前行**
- `s` = substitute（替换）
- `g` = global，**替换每一行中的所有匹配**；不加 `g` 则只替换每行的**第一个**匹配
- `c` = confirm，替换前逐个确认
- `$` = 最后一行，`%` = 全文（`1,$` 的简写）

```bash
:s/hello/world        # 当前行：第一个 hello → world
:s/hello/world/g      # 当前行：所有 hello → world
:1,5s/hello/world/g   # 第 1~5 行：所有 hello → world
:1,$s/hello/world/g   # 全文：所有 hello → world
:%s/hello/world/g     # 全文：所有 hello → world（最常用，% 等价 1,$）
:%s/hello/world/gc    # 全文替换，但每个都先问一次（y 确认 / n 跳过 / a 全部 / q 退出）
:%s/\/usr\/local/\/opt/g   # 路径含 / 时用 \ 转义
:%s#/usr/local#/opt#g      # 或者把分隔符换成 # 等其他字符，免去转义
```

### 3.9 撤销与重做

| 键 | 效果 | Windows 类比 |
| --- | --- | --- |
| `u` | **撤销**（undo） | Ctrl + Z |
| `Ctrl + r` | **重做**（redo，撤销的撤销） | Ctrl + Y |

> 教程只讲了 `u`，但 `Ctrl + r` 同样重要 —— 撤销过头了能撤回来。

### 3.10 `.vimrc` 配置文件

`~/.vimrc` 用于保存 Vim 的个性化配置（快捷键、配色、插件、显示设置等）。每次启动 Vim 会自动加载，不用每次手动 `:set`。

**一份新手友好的 `.vimrc` 配置**（可直接复制）：

```vim
" ===== 显示 =====
set number              " 显示行号
set relativenumber      " 相对行号（配合 set number，方便 10j / 5dd）
set cursorline          " 高亮当前行
set showcmd             " 右下角显示正在输入的命令
set showmode            " 左下角显示当前模式
set ruler               " 显示光标位置（行,列）
set wildmenu            " 命令行补全增强

" ===== 缩进 =====
set tabstop=4           " Tab 显示为 4 个空格宽
set shiftwidth=4        " 自动缩进 4 格
set softtabstop=4
set expandtab           " Tab 自动转成空格（写 Python 必备）
set autoindent          " 自动缩进
set smartindent

" ===== 搜索 =====
set ignorecase          " 搜索忽略大小写
set smartcase           " 含大写字母时严格匹配
set hlsearch            " 高亮搜索结果
set incsearch           " 输入即时搜索

" ===== 编辑体验 =====
syntax on               " 语法高亮
set encoding=utf-8      " 编码（避免中文乱码）
set fileencodings=utf-8,gbk,latin1
set nobackup            " 不生成 ~ 备份文件
set undofile            " 持久撤销：关闭文件后重开还能 u 撤销
set backspace=indent,eol,start   " 让退格键能正常删除缩进/换行/行首
set clipboard=unnamedplus        " 让 y/p 与系统剪贴板互通（需 vim-gtk）

" ===== 其他 =====
set mouse=a             " 启用鼠标（选中/滚动）
set laststatus=2        " 总是显示状态栏
```

> 改完 `.vimrc` 后：重启 Vim，或在命令模式执行 `:source ~/.vimrc` 立即生效。
> 若 `set clipboard` 无效，说明装的是精简版 vim，需 `sudo apt install vim-gtk3`。

> **补充：Vim 的其他模式（教程未讲但很实用）**
>
> | 模式 | 进入 | 作用 |
> | --- | --- | --- |
> | **可视模式** | `v` | 逐字符选中，再 `y`/`d` 复制 / 删除 |
> | **可视行模式** | `V`（大写） | 整行选中，批量移动、注释代码块神器 |
> | **可视块模式** | `Ctrl + v` | 选中矩形块，**批量注释**：`Ctrl+v` 选中行首 → `I` → 输入 `#` → `ESC` |
> | **替换模式** | `R`（大写） | 输入直接覆盖光标后内容（不是插入） |
>
> **补充：分屏与多文件**
>
> ```bash
> vim -O a.txt b.txt    # 垂直分屏打开两个文件（-o 为水平）
> :sp file              # 水平分屏打开新文件
> :vsp file             # 垂直分屏打开新文件
> Ctrl + w + h/j/k/l    # 在分屏间切换
> Ctrl + w + =          # 等分所有窗口
> :q                    # 关闭当前窗口
> ```
>
> **补充：其他高频技巧**
>
> | 操作 | 命令 |
> | --- | --- |
> | 全文自动缩进格式化 | `gg=G` |
> | 把外部命令输出读入当前文件 | `:r !ls -l` |
> | 不退出 Vim 执行 shell 命令 | `:!pwd` |
> | 删除所有行 | `ggdG` 或 `:%d` |
> | 全文复制 | `ggyG` |
> | 重复上一次操作 | `.`（点号，Vim 最强大的键之一） |
> | 光标处字符大小写翻转 | `~` |
>
> **补充：卡在 Vim 里出不来怎么办？**
> 「救命三连」：先按 `ESC` 若干次，再输入 `:q!` 回车。
> 终端彻底卡死：`Ctrl + c` 不行就 `Ctrl + \`，再不行关标签页重开。
> 长期方案：装 `nano`（`Ctrl + O` 保存、`Ctrl + X` 退出），对新手更友好。

---

## 第四部分 文件系统与目录结构

### 4.1 与 Windows 的根本区别

| 对比项 | Windows | Linux |
| --- | --- | --- |
| 起点 | **盘符**：`C:\` `D:\` `E:\` | **根目录 `/`**（单一树状结构） |
| 分隔符 | 反斜杠 `\` | **正斜杠 `/`** |
| 大小写 | 不敏感（`A.txt` = `a.txt`） | **敏感**（`A.txt` ≠ `a.txt`） |
| 隐藏文件 | 由文件属性控制 | **以 `.` 开头**即为隐藏 |
| 扩展名 | 决定文件类型 | 只是文件名的一部分，类型由内容与权限位决定 |

Linux 中**所有文件和目录都从根目录 `/` 开始**，是一棵**倒置的树**。即使有多个硬盘分区，也是「挂载（mount）」到这棵树的某个目录上，不存在 C 盘 D 盘的概念。

### 4.2 路径：绝对路径 vs 相对路径

| 类型 | 定义 | 例子 |
| --- | --- | --- |
| **绝对路径** | 从**根目录 `/`** 开始的完整路径 | `/home/user/hello.txt` |
| **相对路径** | 相对于**当前目录**的路径 | `hello.txt`、`./docs/`、`../etc/` |

**特殊路径符号**：

| 符号 | 含义 |
| --- | --- |
| `.` | 当前目录 |
| `..` | 上一级目录 |
| `~` | 当前用户的**家目录**（如 `/home/user`，root 用户为 `/root`） |
| `-` | **上一次所在的目录**（`cd -` 在两个目录间来回切） |
| `/` | 根目录 |

```bash
pwd                 # 显示当前所在目录（Print Working Directory）
cd /                # 切换到根目录
cd ~                # 回到家目录（直接 cd 回车也可以）
cd ..               # 上一级
cd ../..            # 上两级
cd -                # 回到上一次所在的目录（来回跳转神器）
cd /var/log/nginx   # 绝对路径
cd ./nginx          # 相对路径
```

### 4.3 根目录常见目录一览（FHS 标准）

| 目录 | 含义 | 作用 |
| --- | --- | --- |
| **`/`** | 根目录 | 一切的起点 |
| **`/bin`** | **binary** | 系统的**基本命令**二进制文件（`ls` `cat` `cp` 都在这），所有用户可用 |
| **`/sbin`** | system binary | **系统管理命令**（`ifconfig` `reboot` `fdisk`），通常只有 root 用 |
| **`/boot`** | — | 启动相关文件：内核 `vmlinuz`、initramfs、GRUB 引导程序 |
| **`/dev`** | device | **设备文件**。Linux「一切皆文件」，硬盘是 `/dev/sda`，终端是 `/dev/tty`，黑洞是 `/dev/null` |
| **`/etc`** | et cetera | **系统和软件的配置文件**。装完 Nginx/MySQL，配置文件在 `/etc/nginx`、`/etc/mysql` |
| **`/home`** | — | 普通用户的**家目录**，每个用户一个子目录（`/home/zhangsan`），登录后的默认位置 |
| **`/root`** | — | **root 用户的家目录**（注意不是 `/home/root`） |
| **`/lib` `/lib64`** | library | 系统与程序的**共享库**（`.so` 文件），相当于 Windows 的 `.dll` |
| **`/media`** | — | 可移动设备自动挂载点（U 盘、光盘） |
| **`/mnt`** | mount | **手动挂载**临时文件系统的地方 |
| **`/opt`** | optional | 第三方大型软件安装目录（如手动装的 JDK、IDEA） |
| **`/proc`** | processes | **虚拟文件系统**，内核与进程信息的映射（`/proc/cpuinfo` 看 CPU、`/proc/meminfo` 看内存）。不占磁盘，实时生成 |
| **`/run`** | — | 系统启动以来的运行时数据（PID 文件、socket） |
| **`/srv`** | service | 服务提供的数据（如网站数据） |
| **`/sys`** | system | **虚拟文件系统**，设备与内核参数的统一视图 |
| **`/tmp`** | temporary | **临时文件**，所有用户可写，重启通常清空 |
| **`/usr`** | Unix System Resources | 用户程序的主体：`/usr/bin`（大部分命令）、`/usr/lib`、`/usr/local`（手动编译安装的软件，推荐位置）、`/usr/share`（文档、man 页） |
| **`/var`** | variable | **经常变化的数据**：`/var/log`（日志，排查问题第一站）、`/var/www`（网站根目录）、`/var/lib`（数据库等状态数据） |
| **`/lost+found`** | — | 文件系统异常断电后，`fsck` 找回的碎片文件 |

> **速记口诀**：
> - 找**命令** → `/bin`、`/usr/bin`、`/sbin`
> - 找**配置** → `/etc`
> - 找**日志** → `/var/log`
> - 找**设备** → `/dev`
> - 找**进程信息** → `/proc`
> - 手动装软件 → `/usr/local` 或 `/opt`

---

## 第五部分 文件与目录操作命令

### 5.1 命令的通用格式

```bash
命令名 [选项/参数] [操作对象]
```

- Linux 命令基本都由**命令名 + 参数**组成
- 参数用来指定命令的具体行为
- **多个短选项可以合并**：`ls -l -t -r` 可写成 `ls -ltr`
- 选项有两种风格：
  - **短选项**：单个字母，前面一个 `-`，如 `ls -a`
  - **长选项**：完整单词，前面两个 `--`，如 `ls --all`
- 绝大多数命令支持 `-h`/`--help` 查看简要帮助，`man 命令` 查看完整手册

```bash
ls --help       # 简要帮助
man ls          # 完整手册（q 退出，/关键词 搜索）
whatis ls       # 一行说明
which ls        # 查看命令的可执行文件路径
type ls         # 判断是内置命令 / 外部命令 / 别名
```

### 5.2 `ls` —— 列出目录内容

```bash
ls              # 列出当前目录的文件和目录（不含隐藏文件）
ls /etc         # 列出指定目录
ls -l           # 长格式，显示详细信息（权限、所有者、大小、修改时间、名称）
ls -a           # 显示所有文件，【包括隐藏文件】（以 . 开头的）
ls -A           # 同 -a，但不显示 . 和 ..
ls -h           # human-readable，文件大小以 K/M/G 显示（配合 -l 使用）
ls -t           # 按修改时间排序（新的在前）
ls -r           # reverse，逆序显示
ls -R           # 递归列出子目录内容
ls -S           # 按文件大小排序
ls -i           # 显示 inode 号
ls -d           # 只显示目录本身，不展开内容（常配合 -l：ls -ld /etc）
ls -1           # 每行只显示一个文件名
ls -F           # 目录后加 /、可执行文件后加 *，便于区分
ls -ltr         # 组合：详细 + 按时间 + 逆序（找最近改过的文件很方便）
ls -lah         # 最常用组合：详细 + 全部 + 人类可读
```

**`ls -l` 输出逐列详解**：

```bash
$ ls -l
drwxr-xr-x  2  ubuntu  ubuntu  4096  Sep  1 00:49  folder
-rw-r--r--  1  ubuntu  ubuntu   128  Sep  1 00:49  hello.txt
lrwxrwxrwx  1  ubuntu  ubuntu     9  Sep  1 00:49  link.txt -> hello.txt
│└──┬────┘  │  └──┬──┘  └──┬──┘   │    └────┬────┘   └──────┬──────┘
│   │       │     │        │      │         │                │
│   │       │     │        │      │         │                └─ 文件名（-> 表示软链接指向）
│   │       │     │        │      │         └─ 最后修改时间
│   │       │     │        │      └─ 文件大小（字节，-h 后显示 4.0K）
│   │       │     │        └─ 所属组
│   │       │     └─ 所有者
│   │       └─ 硬链接数（目录则为子目录数）
│   └─ 权限位（9 个字符，见第六部分）
└─ 文件类型（第 1 个字符）
```

**第 1 个字符：文件类型**

| 字符 | 类型 | 说明 |
| --- | --- | --- |
| `-` | 普通文件 | 文本、二进制、图片等 |
| `d` | 目录 | directory |
| `l` | **软链接（符号链接）** | link，类似 Windows 快捷方式，`ls -l` 中用 `->` 指向目标 |
| `b` | 块设备文件 | 硬盘 `/dev/sda` |
| `c` | 字符设备文件 | 键盘、终端 `/dev/tty` |
| `p` | 管道文件 | 进程间通信 |
| `s` | 套接字文件 | socket，如 `/var/run/docker.sock` |

> **补充：常见文件颜色含义**（Ubuntu 默认配色）
> 蓝色 = 目录｜白色 = 普通文件｜绿色 = 可执行文件｜青色 = 软链接｜红色 = 压缩包 / **失效的软链接**｜黄色 = 设备文件

**Linux 中的隐藏文件**：以半角英文句点 `.` 开头即为隐藏，直接用 `ls` 看不到，必须加 `-a`。

| 常见隐藏文件 | 作用 |
| --- | --- |
| `~/.vimrc` | Vim 配置 |
| `~/.bashrc` | bash 的个性化配置（别名、环境变量） |
| `~/.profile` | 用户登录时加载的环境配置 |
| `~/.ssh/` | SSH 密钥与配置（`~/.ssh/id_rsa`、`~/.ssh/config`） |
| `~/.bash_history` | 命令历史记录 |

### 5.3 `cd` / `pwd`

```bash
pwd           # Print Working Directory，显示当前所在目录的绝对路径
cd 目录路径   # Change Directory，切换目录
cd            # 不带参数 = 回到家目录
cd ~          # 回到家目录
cd /          # 到根目录
cd ..         # 上一级
cd ../..      # 上两级
cd -          # 回到上一次所在目录
```

> **补充：Tab 补全（最重要的效率技巧）**
> 输入路径或命令的前几个字母后按 **Tab**：
> - 唯一匹配 → 自动补全
> - 多个匹配 → 再按一次 Tab 列出所有候选
>
> 能补全命令、文件名、目录名、甚至命令参数。**一定要养成按 Tab 的习惯**，既快又能避免手打错路径。

### 5.4 `mkdir` / `rmdir` —— 创建与删除目录

```bash
mkdir folder              # 创建目录 folder
mkdir -p a/b/c            # -p：递归创建多级目录（父目录不存在也不报错）
mkdir -p project/{src,doc,test}    # 花括号展开，一次创建多个同级目录
mkdir -m 755 newdir       # 创建时直接指定权限
mkdir -v dir              # 显示创建过程（verbose）

rmdir folder              # 删除【空目录】（非空则报错 Directory not empty）
rm -r folder              # -r：递归删除目录及其下所有内容
rm -rf folder             # -rf：递归 + 强制，不询问直接删（危险！）
```

### 5.5 `touch` —— 创建空文件 / 更新时间戳

`touch` 本意是**更新文件的访问与修改时间**，但如果文件不存在，就**自动创建一个空文件**。

```bash
touch file.txt        # 文件不存在 → 创建空文件（大小为 0）
touch hello.txt       # 文件已存在 → 把修改时间更新为当前时间（内容不变）
touch f1 f2 f3        # 一次创建多个
touch -d "2026-01-01 10:00" file.txt    # 把时间改成指定值
touch -a file.txt     # 只更新访问时间（atime）
touch -m file.txt     # 只更新修改时间（mtime）
```

> **技巧**：按**方向键 ↑** 可以找到之前输入过的命令，回车即可再次执行；`history` 查看全部历史，`Ctrl + r` 反向搜索历史命令。

### 5.6 `echo` 与重定向 —— 快速写文件

```bash
echo hello              # 在屏幕上输出 hello
echo $PATH              # 输出环境变量
echo -e "a\nb"          # -e：启用转义（\n 换行、\t 制表符）
echo "hello" > f.txt    # 覆盖写入文件（文件不存在则创建）
echo "world" >> f.txt   # 追加到文件末尾
```

> 用重定向创建文件是运维写脚本的常用手段，比 `touch` 更实用（能直接带内容）。

### 5.7 `cp` / `mv` / `rm` —— 复制、移动、删除

**复制 `cp`（copy）**

```bash
cp file1 file2              # 复制 file1 为 file2
cp file1 /tmp/              # 复制到 /tmp 目录下（保持同名）
cp file1 file2 /tmp/        # 复制多个文件到 /tmp
cp -r dir1 dir2             # -r：递归复制目录（复制目录必须加，否则报错）
cp -a dir1 dir2             # -a：归档复制，保留权限/时间/软链接等全部属性（备份首选）
cp -i file1 file2           # -i：覆盖前询问（interactive）
cp -v file1 file2           # -v：显示复制过程
cp -p file1 file2           # -p：保留原文件的权限、属主、时间戳
cp -u file1 file2           # -u：只在源文件比目标新时才复制（增量备份）
```

**移动 / 重命名 `mv`（move）**

```bash
mv file3 file4        # 重命名（同一目录下移动）
mv file1 /tmp/        # 移动到 /tmp
mv dir1 dir2          # 目录重命名；若 dir2 已存在则把 dir1 移入 dir2 内部
mv -i file /tmp/      # 覆盖前询问
mv -v file /tmp/      # 显示过程
```

**删除 `rm`（remove）**

```bash
rm file               # 删除文件
rm -f file            # -f：强制删除，不提示、不存在也不报错
rm -r dir             # -r：递归删除目录及内容
rm -rf dir            # 递归 + 强制（最危险的命令之一）
rm -i file            # 删除前逐个询问
rm -v file            # 显示删除过程
```

> ### 极其重要：`rm` 是危险的
> Linux 的删除操作**不可逆**，也**没有 Windows 那样的回收站机制**，删了就是真删了。
>
> **使用 `rm -rf` 前必须做的自查**：
> 1. 先 `pwd` 确认当前路径对不对
> 2. 先用 `ls` 确认要删的东西对不对
> 3. 路径**不要用「相对路径 + 通配符」**的模糊写法
> 4. **绝对不要**执行 `rm -rf /` 或 `rm -rf /*`
> 5. 小心 `rm -rf /home/user data` —— 路径和文件名之间**多了个空格**就会误删整个 home
> 6. 生产环境建议给 `rm` 加保护：
>    ```bash
>    # 写入 ~/.bashrc：把 rm 变成「移动到回收站」
>    mkdir -p ~/.trash
>    alias rm='mv -t ~/.trash/'      # 需先建好回收站目录
>    # 或至少让 rm 永远询问
>    alias rm='rm -i'
>    ```
> 7. 重要数据**一定先备份**：`cp -a src src.bak.$(date +%F)`

### 5.8 `du` / `tree` —— 查看目录结构与大小

```bash
du              # 显示当前目录下各文件/目录的磁盘占用（顺带能看清目录结构）
du -h           # 人类可读（K/M/G）
du -sh          # -s：只显示总计（summary），最常用
du -sh /var/*   # 看 /var 下每个子目录的大小 → 快速定位磁盘被谁吃了
du -ah          # 把文件也列出来
du -h --max-depth=1    # 只显示 1 层深度
du -sh * | sort -hr | head -10     # 当前目录占用最大的前 10 项

tree            # 以树状图显示目录结构（非系统自带，需安装）
tree -L 2       # 只显示 2 层
tree -d         # 只显示目录
tree -a         # 包含隐藏文件

sudo apt install tree    # Ubuntu/Debian 安装
sudo yum install tree    # CentOS/RHEL 安装
```

> **补充：`df` 看磁盘剩余空间**（与 `du` 是一对，教程未讲）
> ```bash
> df -h          # 各分区总容量/已用/可用/挂载点
> df -h /home    # 只看 /home 所在分区
> df -i          # 看 inode 使用情况（inode 耗尽也会导致「磁盘满」却写不进文件）
> ```

### 5.9 通配符（补充，教程未讲）

Shell 会先把通配符**展开成实际文件名**再交给命令，所以几乎所有命令都支持。

| 通配符 | 含义 | 示例 |
| --- | --- | --- |
| `*` | 匹配任意长度任意字符 | `ls *.txt`、`rm -f log-2026*` |
| `?` | 匹配**单个**任意字符 | `ls file?.txt` 匹配 `file1.txt` |
| `[abc]` | 匹配方括号内任一字符 | `ls file[123].txt` |
| `[a-z]` | 匹配指定范围 | `ls [a-z]*.log` |
| `[!abc]` / `[^abc]` | 匹配**不在**括号内的字符 | `ls file[!1].txt` |
| `{a,b,c}` | 花括号展开，多选一 | `mkdir -p dir/{a,b,c}`、`cp f{,.bak}`（等价 `cp f f.bak`） |

> 想让通配符**不被展开**传给命令（如 `grep` 的正则），要用引号包起来：`grep "*.log" file`。

---

## 第六部分 文件权限管理

### 6.1 权限位解读

`ls -l` 最左边的 **9 个字符**就是权限位，**每 3 个一组**：

```
  -    rwx   r-x   r--
  │    └┬┘   └┬┘   └┬┘
  │     │     │     └── other：其他用户权限
  │     │     └──────── group：文件所属组的权限
  │     └────────────── user：文件所有者的权限
  └──────────────────── 文件类型
```

| 分组 | 英文 | 含义 |
| --- | --- | --- |
| 第 1 组（2-4 位） | **u**ser | 文件**所有者**的权限 |
| 第 2 组（5-7 位） | **g**roup | 文件**所属组**的权限 |
| 第 3 组（8-10 位） | **o**ther | **其他用户**的权限 |

每组 3 个字符分别是：

| 字符 | 权限 | 对文件 | 对目录 |
| --- | --- | --- | --- |
| `r` | read，可读（4） | 能读文件内容 | 能列出目录内容（`ls`） |
| `w` | write，可写（2） | 能修改文件内容 | 能**在目录内新建/删除/重命名**文件 |
| `x` | execute，可执行（1） | 能当程序执行 | 能**进入**该目录（`cd`） |
| `-` | 无此权限（0） | 相应位置显示 `-` | — |

```bash
-rw-r--r--    # 所有者：读写；同组：只读；其他：只读（普通文件默认 644）
drwxr-xr-x   # 所有者：读写执行；同组：读执行；其他：读执行（目录默认 755）
```

> **重点理解目录的 `x`**：目录没有 `x` 权限 = 进不去（`cd` 报 Permission denied），哪怕有 `r` 也只能看到文件名列表而读不到内容。
> **重点理解目录的 `w`**：能否删除目录内的文件，取决于**目录的 w 权限**，而不是文件本身的权限 —— 所以一个你只读的文件，只要它所在目录你可写，你依然能删掉它。

### 6.2 `chmod` —— 修改权限（符号法）

```bash
chmod +x file          # 给所有用户（u/g/o）添加【执行】权限
chmod +r file          # 添加读权限
chmod +w file          # 添加写权限
chmod -x file          # 移除执行权限
chmod -w file          # 移除写权限

chmod u+x file         # 只给【所有者】加执行权限
chmod g+w file         # 只给【所属组】加写权限
chmod o-r file         # 只给【其他用户】去掉读权限
chmod ug+x file        # 给所有者 + 所属组加执行权限（可组合）
chmod ugo+x file       # 给三类用户都加执行权限（等价 chmod +x）
chmod a+x file         # a = all = ugo
chmod u=rwx,g=rx,o=r file    # 用 = 直接赋值（不管原来是什么）

chmod -R 755 dir       # -R：递归修改目录及其下所有文件的权限
```

| 符号 | 含义 |
| --- | --- |
| `u` / `g` / `o` / `a` | 所有者 / 所属组 / 其他 / 全部 |
| `+` | 添加权限 |
| `-` | 移除权限 |
| `=` | 直接赋值（覆盖原权限） |
| `r` / `w` / `x` | 读 / 写 / 执行 |

> 加了 `x` 权限后，文件在 `ls` 中**显示为绿色**，表示可执行文件。

### 6.3 `chmod` —— 修改权限（数字法，更常用）

把每组 3 个字符换算成数字后**相加**：

```
r = 4    w = 2    x = 1    - = 0

rwx = 4+2+1 = 7      rw- = 4+2+0 = 6
r-x = 4+0+1 = 5      r-- = 4+0+0 = 4      --- = 0
```

于是 9 位权限就变成**一个 3 位数**：

```bash
chmod 644 file      # rw-r--r--：所有者读写，其他人只读（普通文件默认）
chmod 755 file      # rwxr-xr-x：所有者全权，其他人读+执行（可执行文件/目录默认）
chmod 777 file      # rwxrwxrwx：所有人都有全部权限（不安全，慎用！）
chmod 600 file      # rw-------：只有自己能读写（SSH 私钥必须是这个！）
chmod 700 dir       # 只有自己能进
chmod 400 file      # r--------：只读，谁都改不了（重要文件防误删）
```

**最常用的数字组合**：

| 数字 | 权限 | 典型用途 |
| --- | --- | --- |
| `644` | `rw-r--r--` | 普通文件（默认） |
| `755` | `rwxr-xr-x` | 可执行程序、目录（默认） |
| `600` | `rw-------` | **SSH 私钥**、含密码的配置文件 |
| `700` | `rwx------` | 私人目录、`~/.ssh`（必须是 700） |
| `777` | `rwxrwxrwx` | **禁止在生产环境使用**（任何人可改可执行） |
| `664` | `rw-rw-r--` | 团队共享的可写文件 |
| `775` | `rwxrwxr-x` | 团队共享的可写目录 |

> 若 SSH 私钥权限不对，`ssh` 会直接拒绝使用并报 `Permissions 0644 for 'id_rsa' are too open`：
> ```bash
> chmod 600 ~/.ssh/id_rsa
> chmod 700 ~/.ssh
> ```

### 6.4 `chown` / `chgrp` —— 修改所有者与所属组（补充）

```bash
chown user file           # 把文件的所有者改为 user
chown user:group file     # 同时改所有者和所属组
chown :group file         # 只改所属组
chown -R user:group dir   # 递归修改目录及内容

chgrp group file          # 只修改所属组（change group）
chgrp -R www-data /var/www
```

> 只有 **root** 或**文件当前所有者**（且属于目标组）才能执行 `chown`。普通用户改别人的文件需要 `sudo`。

### 6.5 `sudo` —— 临时提权（补充）

```bash
sudo command          # 以 root 身份执行单条命令（需输入当前用户密码）
sudo -i               # 切换到 root 并加载 root 环境
sudo su -             # 同上
sudo -u www-data cmd  # 以指定用户身份执行
sudo !!               # 用 sudo 重跑上一条命令（忘记加 sudo 时的救命键）
```

> 教程全程没提 `sudo`，但这是 Ubuntu 下**最高频的前缀**：改系统配置、装软件、看别人的日志基本都要 `sudo`。
> 判断依据：命令报 `Permission denied` 就在前面加 `sudo` 重试。

### 6.6 特殊权限与 umask（补充）

**三种特殊权限**（`chmod` 用 4 位数字，最高位是特殊权限）：

| 名称 | 数字 | 符号 | 作用 |
| --- | --- | --- | --- |
| **SUID** | 4 | `u+s` | 执行该文件时，**临时以文件所有者的身份运行**。典型：`/usr/bin/passwd`（普通用户改自己密码，需临时拿到 root 权限写 `/etc/shadow`） |
| **SGID** | 2 | `g+s` | ① 对文件：以文件所属组身份运行；② **对目录：目录内新建的文件自动继承目录的所属组**（团队协作共享目录必备） |
| **Sticky Bit** | 1 | `o+t` | **粘滞位**。对目录设置后，目录内的文件**只有所有者（和 root）能删除**。典型：`/tmp`（`drwxrwxrwt`） |

```bash
chmod 4755 file     # 设置 SUID（显示为 -rwsr-xr-x，x 位变 s）
chmod 2755 dir      # 设置 SGID（显示为 drwxr-sr-x）
chmod 1777 /tmp     # 设置 Sticky（显示为 drwxrwxrwt，x 位变 t）
chmod u+s /usr/bin/passwd
chmod g+s /shared
chmod +t /tmp
```

> 若看到的是**大写 `S`**（如 `rwSr--r--`），说明该位置原本**没有 x 权限**，特殊权限实际无效。

**`umask` —— 决定新建文件/目录的默认权限**：

```bash
umask            # 查看当前 umask（常见 0022 或 0002）
umask 022        # 临时修改
```

计算规则：**默认权限 - umask**

- 文件最大权限 `666`，目录最大权限 `777`
- `umask 022` → 文件 `644`，目录 `755`（最常见）
- `umask 002` → 文件 `664`，目录 `775`（团队协作用）
- `umask 077` → 文件 `600`，目录 `700`（最严格，个人服务器推荐）

> 永久修改：把 `umask 022` 写入 `~/.bashrc` 或 `~/.profile`。

---

## 第七部分 硬链接与软链接

`ls -l` 中文件类型位为 `l` 的就是**链接文件**。Linux 的链接分两种：

### 7.1 软链接（符号链接，Symbolic Link）

```bash
ln -s 源文件 链接文件
ln -s hello.txt link.txt
ln -s /var/www/html www        # 指向目录
```

- 类似 **Windows 的快捷方式**
- 软链接文件**本身不存储内容**，只是一个指向目标路径的字符串，所以**体积很小**
- `ls -l` 中用 `->` 显示指向关系：`link.txt -> hello.txt`
- **可以指向文件或目录**，也可以跨文件系统
- **源文件删除后，软链接失效**（`ls` 中显示为**红色**，即断链）

**典型用途**：

```bash
ln -s /usr/local/node-v20/bin/node /usr/bin/node      # 命令放进 PATH
ln -s /data/logs /var/log/myapp                        # 日志目录映射到别处
ln -snf /etc/nginx/sites-available/a.conf /etc/nginx/sites-enabled/a.conf   # nginx 启用站点
```

> `ln -sf`：`-f` 强制覆盖已存在的同名链接。**修改软链接指向时务必用 `-snf`**，否则会在目标目录里再套一层链接（`-n` 让已存在的链接被当作普通文件处理）。
> 软链接**尽量用绝对路径**创建 —— 用相对路径时是相对于**链接文件所在目录**解析的，容易出错。

### 7.2 硬链接（Hard Link）

```bash
ln 源文件 链接文件
ln file1.txt file2.txt
```

- 本质是**指向文件系统中同一个 inode 的另一个名字（指针）**
- 与原始文件**共享相同的 inode**，也就共享完全相同的内容、权限、大小、时间戳
- 原文件和硬链接是**同一个文件的两个不同名字**，地位完全平等（删掉「源文件」后，另一个名字照样能访问）
- **只能指向文件，不能指向目录**
- **不能跨文件系统**（不同分区的 inode 编号会冲突）

### 7.3 inode 是什么

在 Linux 文件系统中，**每个文件或目录都有唯一的 inode（索引节点）**。

- inode 存储文件的**元数据**：权限、所有者、大小、修改时间、**数据块在磁盘上的位置**
- **系统通过 inode 识别文件，而不是文件名**
- 文件名只是「inode 的一个便于人类记忆的别名」，存放在目录项里
- 文件名 ↔ inode 的对应关系，就是**硬链接**

```bash
ls -i              # 查看文件的 inode 号
ls -li             # 详细信息 + inode 号
stat file.txt      # 查看文件的完整 inode 信息（含 atime/mtime/ctime）
df -i              # 查看各分区 inode 使用情况
```

> **补充：inode 耗尽的坑**
> 磁盘还有空间却报「No space left on device」？很可能是**小文件太多把 inode 用光了**。用 `df -i` 确认。
> 这也是为什么**日志文件要定期切割清理**（`/var/log` 最容易出问题）。

### 7.4 实操演示（还原教程）

```bash
echo "hello linux" > file1.txt       # 用重定向创建文件
ln file1.txt file2.txt               # 创建硬链接
ls -li                               # 加 -i 查看，两者 inode 号相同

echo "new content" >> file1.txt      # 修改源文件
cat file2.txt                        # 硬链接内容同步变化

ls -l                                # 第 2 列数字 = 硬链接数，此时为 2
ln file1.txt file3.txt
ls -l                                # 硬链接数变为 3

rm file1.txt                         # 删除源文件
cat file2.txt                        # 硬链接依然可正常访问（数据没丢）

# 对比软链接：
ln -s hello.txt link.txt
rm hello.txt
ls -l                                # link.txt 变红，成为失效链接
```

> **硬链接数归零 = 文件真正被删除**。这也是 `rm` 的本质：它只是**断开一个文件名与 inode 的链接**，当链接数降到 0 且没有进程打开该文件时，空间才会被回收。
> 所以：如果某个大日志文件被 `rm` 了但磁盘没释放，是因为**还有进程占着它**，可用 `lsof | grep deleted` 找到并重启该进程。

### 7.5 软链接 vs 硬链接 对照表

| 对比项 | 软链接（符号链接） | 硬链接 |
| --- | --- | --- |
| 创建命令 | `ln -s 源 链接` | `ln 源 链接` |
| 本质 | 存储目标路径的字符串（快捷方式） | 指向同一 inode 的另一个文件名 |
| inode | 与原文件**不同** | 与原文件**相同** |
| 文件大小 | 很小（路径字符串长度） | 与原文件相同 |
| 能否指向目录 | **可以** | **不可以** |
| 能否跨文件系统 | **可以** | **不可以** |
| 源文件删除后 | 链接**失效**（变红，broken link） | **无影响**，数据仍在 |
| 修改内容 | 双方同步（本就是同一份数据） | 双方同步（同一份数据） |
| `ls -l` 显示 | `lrwxrwxrwx`，带 `->` 指向 | 与普通文件无异（`-`） |

---

## 第八部分 重定向与管道（补充）

教程只用了 `>` 把 `echo` 的输出存进文件。这一节把 Linux「**组合命令完成复杂任务**」的核心机制补全 —— 这是 Shell 最强大的地方。

### 8.1 三种标准数据流

| 名称 | 文件描述符 | 默认来源/去向 | 说明 |
| --- | --- | --- | --- |
| **stdin** 标准输入 | `0` | 键盘 | 程序读取输入 |
| **stdout** 标准输出 | `1` | 屏幕（终端） | 程序正常输出 |
| **stderr** 标准错误 | `2` | 屏幕（终端） | 程序报错信息 |

### 8.2 输出重定向

```bash
command > file        # 标准输出【覆盖】写入文件（文件不存在则创建）
command >> file       # 标准输出【追加】到文件末尾
command 2> file       # 只把【错误信息】写入文件（2 是 stderr 的编号）
command 2>> file      # 错误信息追加
command &> file       # 正确输出和错误信息【都】写入同一个文件
command > file 2>&1   # 同上，标准写法，兼容性最好
command > out.txt 2> err.txt    # 正确和错误分开存
command > /dev/null   # 丢弃输出（/dev/null 是黑洞设备）
command > /dev/null 2>&1        # 彻底静默执行（脚本里常用）
```

> **常见坑**：`>` 会**先清空**目标文件再写入。所以读取并写回**同一个文件**时，原内容已被清空：
> ```bash
> cat a.txt | grep x > a.txt     # 错误：a.txt 会变空
> grep x a.txt > tmp && mv tmp a.txt   # 正确做法
> # 或用 sponge（moreutils 包）：grep x a.txt | sponge a.txt
> ```

### 8.3 输入重定向

```bash
command < file        # 从文件读取输入，而非键盘
wc -l < a.txt         # 统计行数
mysql -u root -p < dump.sql         # 导入 SQL

command << EOF        # Here Document：把后续内容当作输入，直到遇到 EOF
line 1
line 2
EOF

cat > config.conf << EOF      # 经典用法：脚本里生成配置文件
server {
    listen 80;
}
EOF
```

### 8.4 管道 `|`

**把前一个命令的输出，作为后一个命令的输入**，可以无限串联。

```bash
ls -l | grep txt                    # 只显示含 txt 的行
cat /var/log/syslog | grep error    # 过滤日志中的 error
ps aux | grep nginx                 # 查找 nginx 进程
history | awk '{print $2}' | sort | uniq -c | sort -rn | head -10   # 统计最常敲的 10 个命令
du -sh * | sort -hr | head -5       # 找占用空间最大的 5 项
cat access.log | awk '{print $1}' | sort | uniq -c | sort -rn | head -20   # 统计访问 IP TOP20
```

> 注意：`|` 只传递 **stdout**，**stderr 不会进入管道**。需要一起处理时用 `2>&1`：
> ```bash
> command 2>&1 | grep error
> ```

### 8.5 `tee` —— 一边看一边存（补充）

```bash
command | tee file          # 输出到屏幕的同时写入 file（覆盖）
command | tee -a file       # 追加
echo "x" | sudo tee -a /etc/hosts    # 用 tee 绕过「sudo echo > 没权限」的经典问题
```

> **经典场景**：`sudo echo "1.2.3.4 a.com" >> /etc/hosts` 会报权限不足 —— 因为**重定向是 shell 做的，权限属于当前用户而非 sudo**。改成 `echo "..." | sudo tee -a /etc/hosts` 即可。

### 8.6 命令连接符（补充）

| 符号 | 含义 | 示例 |
| --- | --- | --- |
| `;` | 顺序执行，不管前一个成功与否 | `cd /tmp; ls` |
| `&&` | **前一个成功**才执行后一个 | `mkdir d && cd d` |
| `\|\|` | **前一个失败**才执行后一个 | `ping -c1 x \|\| echo "不通"` |
| `&` | 放到后台执行 | `./server &` |
| `&& \|\|` | 三元表达式风格 | `[ -f a ] && echo yes \|\| echo no` |

---

## 第九部分 文本查看与处理三剑客（补充）

教程只讲了 `cat`。但服务器排查问题时，日志动辄几 GB，**绝不能 `cat` 一个大日志**（会刷屏卡死终端）。

### 9.1 文本查看

| 命令 | 用途 | 常用写法 |
| --- | --- | --- |
| `cat` | 一次性显示**全部**内容（**只适合小文件**） | `cat -n f`（显示行号）、`cat a b > c`（合并） |
| `tac` | 倒序显示（cat 反过来） | `tac f` |
| `more` | 分页显示，只能向下翻 | `more f`（空格翻页，q 退出） |
| **`less`** | **分页显示，可上下翻、可搜索（最常用）** | `less /var/log/syslog` |
| `head` | 看开头若干行（默认 10） | `head -20 f`、`head -c 100 f`（前 100 字节） |
| `tail` | 看结尾若干行（默认 10） | `tail -20 f`、`tail -n +5 f`（从第 5 行到末尾） |
| **`tail -f`** | **实时追踪文件新增内容（看日志必备）** | `tail -f app.log`、`tail -100f app.log` |
| `nl` | 显示行号输出 | `nl f` |
| `wc` | 统计行数/单词数/字节数 | `wc -l f`（行数）、`wc -l *.log` |

**`less` 内的操作**（与 Vim 几乎一致）：

```bash
less /var/log/syslog

空格 / Ctrl+f  → 向下一页
b / Ctrl+b     → 向上一页
j / k          → 下一行 / 上一行
g / G          → 跳到开头 / 结尾
/error         → 向下搜索 error
?error         → 向上搜索 error
n / N          → 下一个 / 上一个匹配
q              → 退出
F              → 进入实时追踪模式（等同 tail -f，按 Ctrl+c 退回）
```

### 9.2 三剑客之一：`grep` —— 文本搜索

```bash
grep "error" app.log            # 在文件中搜索含 error 的行
grep -i "error" app.log         # -i：忽略大小写
grep -n "error" app.log         # -n：显示行号
grep -v "debug" app.log         # -v：反向匹配（排除含 debug 的行）
grep -c "error" app.log         # -c：只统计匹配的行数
grep -r "TODO" ./src            # -r：递归搜索目录下所有文件
grep -rn "TODO" ./src           # -rn：递归 + 显示行号（最常用）
grep -rn "TODO" --include="*.py" .   # 只在 .py 文件里搜
grep -A 5 -B 5 "error" app.log  # 显示匹配行的【后 5 行】/【前 5 行】
grep -C 5 "error" app.log       # 前后各 5 行（Context）
grep -E "error|warn" app.log    # -E：扩展正则，匹配多个模式
grep "^root" /etc/passwd        # 以 root 开头的行（^ 表示行首）
grep "bash$" /etc/passwd        # 以 bash 结尾的行（$ 表示行尾）
grep -w "test" f                # -w：全词匹配（不匹配 testing）
ps aux | grep nginx | grep -v grep    # 排除 grep 自身
```

### 9.3 三剑客之二：`sed` —— 流编辑器（批量替换）

```bash
sed 's/old/new/' f           # 把每行【第一个】old 换成 new（只输出到屏幕，不改文件）
sed 's/old/new/g' f          # g：替换每行【所有】old
sed -n '5,10p' f             # 只打印第 5~10 行（-n + p）
sed -i 's/old/new/g' f       # -i：直接修改文件（in-place）
sed -i.bak 's/old/new/g' f   # -i.bak：修改前先备份为 f.bak（更安全）
sed -i 's/old/new/g' *.conf  # 批量替换多个文件
sed '/^#/d' f                # 删除以 # 开头的行（注释）
sed '/^$/d' f                # 删除空行
sed '2d' f                   # 删除第 2 行
sed -n '/error/,+5p' app.log # 打印含 error 的行及其后 5 行
sed 's/^/  /' f              # 每行行首加两个空格
```

> Vim 的 `:s` 替换语法就是从 `sed` 来的，这就是为什么两者长得一模一样。
> **改配置前一定要先不带 `-i` 跑一遍预览输出**，确认无误再加 `-i`。

### 9.4 三剑客之三：`awk` —— 按列处理文本

`awk` 把每行按分隔符切成若干**字段**，用 `$1` `$2`… 引用，`$0` 是整行。

```bash
awk '{print $1}' f                  # 打印第 1 列（默认以空白分隔）
awk '{print $1, $3}' f              # 打印第 1 和第 3 列
awk -F: '{print $1, $7}' /etc/passwd   # -F 指定分隔符为冒号
awk 'NR==5' f                       # 打印第 5 行（NR = 行号）
awk 'NR>=10 && NR<=20' f            # 打印 10~20 行
awk '{print $NF}' f                 # 打印最后一列（NF = 字段数）
awk 'length($0)>80' f               # 打印长度超过 80 的行
awk '{sum+=$1} END {print sum}' f   # 求第 1 列之和
awk '$3 > 100 {print $1, $3}' f     # 条件过滤：第 3 列大于 100 才打印

# 实战：统计日志中访问最多的 IP TOP10
awk '{print $1}' access.log | sort | uniq -c | sort -rn | head -10

# 实战：批量杀掉某进程
ps aux | grep 'python worker' | awk '{print $2}' | xargs kill -9
```

### 9.5 排序去重与 `xargs`（补充）

```bash
sort f                # 按字典序排序
sort -n f             # 按数值排序
sort -r f             # 逆序
sort -rn f            # 数值逆序（配合 uniq -c 统计排名）
sort -u f             # 排序并去重
sort -k2 f            # 按第 2 列排序

uniq f                # 去掉【相邻】重复行（所以必须先 sort）
uniq -c f             # 统计每行出现次数
uniq -d f             # 只显示重复的行

cut -d: -f1 /etc/passwd      # 按冒号切分，取第 1 列
cut -c1-10 f                 # 取每行的第 1~10 个字符

tr 'a-z' 'A-Z' < f           # 小写转大写
tr -d '\r' < f > f.new       # 删除 Windows 换行符 \r（处理脚本 ^M 报错）

xargs                        # 把管道输入转成命令的参数
find . -name "*.log" | xargs rm -f
echo "a b c" | xargs -n1 echo     # -n1：每次传一个参数
find . -name "*.log" -print0 | xargs -0 rm -f   # -print0/-0：安全处理含空格的文件名
```

---

## 第十部分 文件查找与搜索（补充）

### 10.1 `find` —— 实时全文/全盘查找（功能最强）

```bash
find . -name "*.log"                    # 按文件名查找（区分大小写）
find . -iname "*.LOG"                   # -iname：忽略大小写
find / -name "nginx.conf"               # 全盘查找
find . -type f -name "*.py"             # -type f：只找文件
find . -type d -name "node_modules"     # -type d：只找目录
find . -type l                          # -type l：只找软链接

find /var/log -mtime +7                 # 7 天前修改过的文件
find /var/log -mtime -1                 # 最近 1 天内修改过的
find . -size +100M                      # 大于 100MB 的文件
find . -size -10k                       # 小于 10KB 的文件
find . -empty                           # 空文件或空目录
find . -perm 777                        # 权限为 777 的文件（安全排查）
find . -user root                       # 属于 root 的文件

# -exec：对找到的每个文件执行后续命令（{} 是占位符，\; 是固定结尾）
find /var/log -name "*.log" -mtime +30 -exec rm -f {} \;
find . -name "*.txt" -exec chmod 644 {} \;
find . -name "*.py" -exec grep -l "import os" {} \;

# 等价但更高效的写法（用 + 代替 \;，一次传多个参数）
find /var/log -name "*.log" -mtime +30 -exec rm -f {} +

# 实战：清理 30 天前的日志（运维最常用的一条）
find /var/log -type f -name "*.log" -mtime +30 -delete
```

**`find` 常用条件速查**：

| 条件 | 含义 |
| --- | --- |
| `-name "*.log"` | 文件名匹配（大小写敏感） |
| `-iname` | 文件名匹配（忽略大小写） |
| `-type f/d/l` | 文件 / 目录 / 软链接 |
| `-mtime +n / -n` | n 天前 / n 天内修改过 |
| `-size +100M` | 大于 100MB（`k` `M` `G`） |
| `-user name` | 属于某用户 |
| `-perm 644` | 权限等于 644 |
| `-newer file` | 比 file 更新的文件 |
| `-maxdepth 2` | 最多搜索 2 层目录 |

### 10.2 `locate` —— 基于索引的极速查找（补充）

```bash
locate nginx.conf         # 秒出结果（查的是预先建好的索引库）
sudo updatedb             # 手动更新索引库（新建的文件要先更新才能被搜到）
```

> `locate` 快，但索引不是实时的（通常每天自动更新一次）；`find` 慢（实时遍历磁盘），但结果永远准确。
> 找不到结果时先 `sudo updatedb` 再搜。

### 10.3 查找命令本身（补充）

```bash
which python        # 查看命令的可执行文件路径
whereis python      # 查找二进制、源码、man 手册位置
type cd             # 判断是 shell 内置命令还是外部命令
whatis ls           # 一行说明
man ls              # 完整手册
apropos network     # 按关键字搜索相关命令（忘了命令名时用）
```

---

## 第十一部分 压缩与归档（补充）

### 11.1 `tar` —— 最通用的打包工具

Linux 上**最常见的归档格式**是 `.tar.gz`（先 tar 打包，再 gzip 压缩）。

```bash
# 打包压缩
tar -czvf archive.tar.gz dir/          # 把 dir 打包并用 gzip 压缩
tar -cjvf archive.tar.bz2 dir/         # 用 bzip2 压缩（压缩率更高，更慢）
tar -cJvf archive.tar.xz dir/          # 用 xz 压缩（压缩率最高，最慢）
tar -czvf backup.tar.gz --exclude="node_modules" --exclude="*.log" project/

# 解包
tar -xzvf archive.tar.gz               # 解压到当前目录
tar -xzvf archive.tar.gz -C /opt/      # 解压到指定目录
tar -xzvf archive.tar.gz file1.txt     # 只解压包里的某个文件

# 查看内容（不解包）
tar -tzvf archive.tar.gz               # 列出包内文件清单
tar -xzf archive.tar.gz -O file.txt    # 直接把包内某文件内容输出到屏幕
```

**参数记忆**：

| 参数 | 含义 |
| --- | --- |
| `-c` | **c**reate，创建归档 |
| `-x` | e**x**tract，解包 |
| `-t` | lis**t**，列出内容 |
| `-z` | gzip 压缩（`.tar.gz` / `.tgz`） |
| `-j` | bzip2 压缩（`.tar.bz2`） |
| `-J` | xz 压缩（`.tar.xz`） |
| `-v` | **v**erbose，显示过程 |
| `-f` | **f**ile，指定文件名（**必须放最后**，紧接文件名） |
| `-C` | 指定解压目标目录 |
| `-r` | 往已有归档里追加文件 |
| `-p` | 保留原权限（备份系统文件时建议加） |

> **老手写法**：`-f` 必须写在所有参数的最后面，因为 `-f` 后面紧跟的就是文件名。写成 `tar -zcf x.tar.gz dir` 会报错或产生名为 `zcf` 的怪文件。

### 11.2 `zip` / `unzip`（补充）

```bash
sudo apt install zip unzip     # Ubuntu 安装

zip -r archive.zip dir/        # 压缩（-r 递归目录）
zip -r archive.zip dir/ -x "*.git*"     # 排除某些文件
unzip archive.zip              # 解压到当前目录
unzip archive.zip -d /opt/     # 解压到指定目录
unzip -l archive.zip           # 只看内容不解压
unzip -O gbk win.zip           # 指定编码，解决 Windows 压缩包中文乱码
```

### 11.3 `gzip` / `bzip2`（补充）

```bash
gzip file          # 压缩成 file.gz（原文件消失）
gzip -k file       # -k：保留原文件
gzip -d file.gz    # 解压（等价 gunzip）
gunzip file.gz
zcat file.gz       # 不解压直接查看内容（看压缩日志必备）
zgrep "error" file.gz      # 不解压直接搜索（排查历史日志神器）
```

> **运维实战**：日志切割后是 `.gz`，排查旧日志时**不要解压**，直接 `zgrep "error" app.log.2.gz` 或 `zcat app.log.2.gz | grep error | head`。

---

## 第十二部分 软件包管理（补充）

不同发行版用不同的包管理器，这是一开始最容易混淆的地方。

| 发行版系列 | 包管理器 | 包格式 | 安装命令 |
| --- | --- | --- | --- |
| **Debian / Ubuntu** | `apt`（底层 `dpkg`） | `.deb` | `sudo apt install pkg` |
| **RHEL / CentOS / Rocky / Fedora** | `yum` / `dnf`（底层 `rpm`） | `.rpm` | `sudo yum install pkg` |
| **Alpine** | `apk` | `.apk` | `apk add pkg` |
| **Arch** | `pacman` | `.pkg.tar.zst` | `sudo pacman -S pkg` |
| **openSUSE** | `zypper` | `.rpm` | `sudo zypper install pkg` |

### 12.1 `apt` 常用命令（Ubuntu / Debian）

```bash
sudo apt update                 # 【必做第一步】更新软件源索引
sudo apt upgrade                # 升级所有已安装的软件
sudo apt full-upgrade           # 升级并处理依赖关系变化（可能卸载旧包）
sudo apt install nginx          # 安装软件
sudo apt install nginx=1.18.0-0ubuntu1   # 安装指定版本
sudo apt install -y nginx       # -y：自动回答 yes
sudo apt reinstall nginx        # 重新安装

sudo apt remove nginx           # 卸载软件（保留配置文件）
sudo apt purge nginx            # 卸载并清除配置文件（重装才干净）
sudo apt autoremove             # 自动清理不再需要的依赖包
sudo apt clean                  # 清理已下载的安装包缓存

apt search nginx                # 搜索软件
apt show nginx                  # 查看软件详情（版本、依赖、描述）
apt list --installed            # 列出已安装的软件
apt list --upgradable           # 列出可升级的软件
apt-cache depends nginx         # 查看依赖关系
```

### 12.2 `dpkg` —— 直接安装本地 `.deb` 包

```bash
sudo dpkg -i package.deb        # 安装本地 deb 包
sudo dpkg -i *.deb              # 批量安装
dpkg -l                         # 列出所有已安装的包
dpkg -l | grep nginx            # 查找某个包
dpkg -L nginx                   # 查看某包装了哪些文件到哪
dpkg -S /usr/sbin/nginx         # 反查某个文件属于哪个包
sudo dpkg -r nginx              # 卸载（保留配置）
sudo dpkg -P nginx              # 卸载并清除配置
```

> `dpkg -i` 不会自动解决依赖，报依赖错误时执行 `sudo apt -f install` 补装依赖。

### 12.3 软件源配置（补充）

```bash
cat /etc/apt/sources.list              # Ubuntu 传统源配置
ls /etc/apt/sources.list.d/            # 附加源（Docker、Node 等都在这）

# 国内用户建议换成镜像源，下载速度快很多（以阿里云为例）
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
sudo sed -i 's|archive.ubuntu.com|mirrors.aliyun.com|g' /etc/apt/sources.list
sudo sed -i 's|security.ubuntu.com|mirrors.aliyun.com|g' /etc/apt/sources.list
sudo apt update

# 添加 PPA（Ubuntu 个人软件包仓库）
sudo add-apt-repository ppa:xxx/yyy
sudo apt update
```

### 12.4 其他安装方式（补充）

| 方式 | 适用场景 | 安装位置 |
| --- | --- | --- |
| 包管理器 `apt` | **首选**，自动处理依赖与升级 | `/usr/bin`、`/etc` |
| `dpkg -i xxx.deb` | 官网下载的 deb 包（如 Chrome、VS Code） | `/usr/bin` |
| 二进制包解压即用 | Go/Java 类程序 | 推荐放 `/usr/local` 或 `/opt`，再软链到 `/usr/local/bin` |
| 源码编译 `./configure && make && make install` | 需要定制编译参数 | 默认 `/usr/local` |
| `snap` / `flatpak` / `AppImage` | 跨发行版桌面应用 | 沙箱目录 |

**源码编译安装的标准三步**：

```bash
./configure --prefix=/usr/local/nginx     # 检查环境、生成 Makefile、指定安装路径
make                                       # 编译（可加 -j$(nproc) 并行加速）
sudo make install                          # 安装到 --prefix 指定的目录
```

> **为什么推荐装到 `/usr/local`？** 因为 `/usr` 是包管理器管的地盘，手动装进去会和 apt 打架、升级时被覆盖。`/usr/local` 就是留给「手动安装的软件」的，卸载时直接删目录即可，干净利落。

---

## 第十三部分 用户与组管理（补充）

### 13.1 三个关键配置文件

| 文件 | 作用 | 备注 |
| --- | --- | --- |
| `/etc/passwd` | 用户账号信息 | 所有用户可读。格式：`用户名:密码占位x:UID:GID:描述:家目录:Shell` |
| `/etc/shadow` | 用户密码（加密后） | **只有 root 可读**，密码字段是 `!` 表示未设置/锁定 |
| `/etc/group` | 组信息 | 格式：`组名:组密码占位:GID:附加成员列表` |

```bash
cat /etc/passwd
# root:x:0:0:root:/root:/bin/bash
# ubuntu:x:1000:1000:Ubuntu:/home/ubuntu:/bin/bash
```

> **UID 的含义**：`0` = root 超级用户；`1~999` = 系统用户（如 www-data、mysql，用于运行服务）；`1000+` = 普通用户。
> 判断自己是不是管理员：`id -u` 输出 `0` 就是 root。

### 13.2 用户管理命令

```bash
# 创建用户
sudo useradd zhangsan                    # 创建用户（不建家目录，不设密码）
sudo useradd -m -s /bin/bash zhangsan    # 推荐：-m 创建家目录，-s 指定 shell
sudo adduser zhangsan                    # 交互式创建，会引导设置密码（新手推荐）

# 设置密码
sudo passwd zhangsan                     # 修改某用户密码
passwd                                   # 修改自己的密码

# 修改用户
sudo usermod -aG sudo zhangsan           # -aG：【追加】到 sudo 组（管理员权限）
sudo usermod -s /bin/zsh zhangsan        # 改默认 shell
sudo usermod -d /data/zhangsan -m zhangsan    # 改家目录并迁移文件
sudo usermod -L zhangsan                 # 锁定账号（Lock）
sudo usermod -U zhangsan                 # 解锁账号

# 删除用户
sudo userdel zhangsan                    # 删除用户（保留家目录）
sudo userdel -r zhangsan                 # 连家目录和邮件一起删

# 查询
id zhangsan                              # 查看用户的 UID/GID/所属组
groups zhangsan                          # 查看用户所属组
whoami                                   # 当前用户名
who                                      # 当前登录的所有用户
w                                        # 谁在登录 + 在干什么
last                                     # 登录历史（排查安全事件）
```

> **高危提醒**：`usermod -G` 会**覆盖**原有附加组，导致用户被踢出 sudo 组而失去管理员权限。**一定要用 `-aG`（append）**！

### 13.3 组管理命令

```bash
sudo groupadd dev                 # 创建组
sudo groupdel dev                 # 删除组
sudo gpasswd -a user dev          # 把用户加入组
sudo gpasswd -d user dev          # 把用户移出组
cat /etc/group                    # 查看所有组
newgrp dev                        # 切换当前用户的有效组（新建文件的属组随之改变）
```

> **团队协作共享目录的标准做法**：
> ```bash
> sudo mkdir /data/shared
> sudo chown root:dev /data/shared
> sudo chmod 2775 /data/shared     # 2 = SGID，让新建文件自动继承 dev 组
> sudo usermod -aG dev alice
> sudo usermod -aG dev bob
> ```

### 13.4 切换用户

```bash
su zhangsan          # 切换到 zhangsan（不加载其环境，仍在当前目录）
su - zhangsan        # 完整切换（加载其环境变量，回到家目录）推荐
su -                 # 切到 root
exit                 # 退回原用户
sudo -i              # 以 root 身份登录（推荐，不用知道 root 密码）
```

> Ubuntu 默认**禁用 root 直接登录**，一切通过 `sudo`。这也是 Ubuntu 比 CentOS 更安全的默认设计之一。

---

## 第十四部分 进程与作业管理（补充）

### 14.1 查看进程

```bash
ps                   # 只显示当前终端的进程
ps aux               # 【最常用】显示系统所有进程的详细信息（BSD 风格）
ps -ef               # 同上（System V 风格，多一列 PPID 父进程）
ps aux | grep nginx  # 查找特定进程
ps -u ubuntu         # 查看某用户的进程
ps aux --sort=-%mem | head -10    # 按内存占用排序取前 10
ps -p 1234           # 查看指定 PID
pstree               # 以树状显示进程父子关系
```

**`ps aux` 输出列含义**：

| 列 | 含义 |
| --- | --- |
| `USER` | 进程所有者 |
| `PID` | 进程 ID（唯一标识，杀进程要用） |
| `%CPU` / `%MEM` | CPU / 内存占用百分比 |
| `VSZ` / `RSS` | 虚拟内存 / 实际物理内存（KB） |
| `TTY` | 所属终端（`?` 表示守护进程） |
| `STAT` | 进程状态（见下表） |
| `START` | 启动时间 |
| `TIME` | 累计占用 CPU 时间 |
| `COMMAND` | 启动命令 |

**进程状态 STAT**：

| 状态 | 含义 |
| --- | --- |
| `R` | Running，正在运行或可运行 |
| `S` | Sleeping，可中断睡眠（等待事件） |
| `D` | 不可中断睡眠（通常在等 I/O，**杀不掉**，多是磁盘/网络存储有问题） |
| `T` | Stopped，已停止（`Ctrl+z` 后） |
| `Z` | **Zombie，僵尸进程**（父进程没回收，需杀父进程） |
| `<` | 高优先级 |
| `N` | 低优先级 |
| `s` | 会话领导者（含有子进程） |
| `+` | 前台进程组 |

### 14.2 实时监控

```bash
top                  # 实时动态查看进程与系统负载（q 退出）
htop                 # top 的增强版（彩色、支持鼠标、可直接 F9 杀进程，需安装）
sudo apt install htop

# top 界面内的交互键
P                    # 按 CPU 排序
M                    # 按内存排序
1                    # 展开显示每个 CPU 核心的使用率
k                    # 杀进程（输入 PID）
u                    # 只看某用户的进程
q                    # 退出
```

**`top` 头部信息解读**：

```
top - 00:49:21 up 10 days,  2:30,  2 users,  load average: 0.15, 0.10, 0.05
Tasks: 120 total,   1 running, 119 sleeping,   0 stopped,   0 zombie
%Cpu(s):  2.0 us,  1.0 sy,  0.0 ni, 96.0 id,  0.5 wa,  0.0 hi,  0.5 si
MiB Mem :   3936.0 total,   1024.0 free,   1500.0 used,   1412.0 buff/cache
```

- **load average**：1/5/15 分钟的系统平均负载。**单核 CPU 时 1.0 = 满载**，四核则 4.0 才是满载。持续超过 CPU 核数说明系统压力大
- **us**：用户态 CPU 占用；**sy**：内核态；**id**：空闲；**wa**：**等待 I/O（这个高说明磁盘/网络是瓶颈）**
- **buff/cache**：被用作缓存的内存（**这部分是可回收的，不算真正占用**）

### 14.3 终止进程

```bash
kill PID                  # 发送 SIGTERM(15)，温柔地请求退出（让程序自己清理）
kill -9 PID               # 发送 SIGKILL(9)，【强制】杀死，无法被忽略（最后手段）
kill -15 PID              # 同 kill（默认就是 15）
kill -1 PID               # SIGHUP，让进程重读配置（nginx 常用）
kill -STOP PID            # 暂停进程
kill -CONT PID            # 继续被暂停的进程

pkill -f "python worker"  # 按【进程名/命令行】杀（匹配完整命令行）
pkill -u ubuntu           # 杀掉某用户的所有进程
killall nginx             # 按进程名杀掉所有同名进程

kill -9 $(pgrep -f worker)        # pgrep 取 PID + kill 组合拳
ps aux | grep worker | awk '{print $2}' | xargs kill -9    # 经典三连
```

> **信号使用原则**：**先 `kill PID`（15），不行再 `kill -9 PID`**。
> 直接用 `-9` 会导致程序来不及做清理工作（关闭数据库连接、写完缓冲区、删除锁文件），可能造成数据损坏 —— 对数据库、消息队列这类有状态服务尤其危险。
>
> 杀不掉的进程（`D` 状态）多半是在等 I/O，只能等 I/O 恢复或重启机器。

### 14.4 前台 / 后台作业（补充）

```bash
command &              # 命令放到后台执行
Ctrl + z               # 暂停【前台】进程并转入后台
jobs                   # 查看当前会话的后台作业列表
fg %1                  # 把作业 1 拉回前台
bg %1                  # 让后台暂停的作业继续运行
kill %1                # 终止作业 1

nohup command &        # 【重点】退出终端后命令依然继续运行（no hang up）
nohup python app.py > app.log 2>&1 &
nohup ./server &> server.log &

disown -h %1           # 让已在后台的作业忽略 SIGHUP，退出终端也不死
```

> **为什么需要 `nohup`？** SSH 断开时，终端会给它启动的所有进程发 SIGHUP 信号，进程默认会退出。
> 想长期运行服务，正确姿势是**写成 systemd 服务**（见第十八部分），`nohup` 只是临时方案。
>
> 更优雅的临时方案：用 `screen` 或 `tmux` 开一个可断开重连的会话：
> ```bash
> screen -S work          # 创建会话
> # 在会话里跑命令，然后 Ctrl+a d 脱离（detach）
> screen -ls              # 列出会话
> screen -r work          # 重新连回会话
> ```

---

## 第十五部分 系统信息与资源监控（补充）

### 15.1 系统与内核信息

```bash
uname -a                 # 内核版本、主机名、架构等全部信息
uname -r                 # 只看内核版本
uname -m                 # CPU 架构（x86_64 / aarch64）

cat /etc/os-release      # 查看发行版信息（最通用，推荐）
lsb_release -a           # 查看发行版信息（Ubuntu/Debian）
cat /etc/redhat-release  # CentOS/RHEL
hostnamectl              # 主机名 + 系统信息（systemd 系统）

hostname                 # 主机名
uptime                   # 运行时长 + 负载
date                     # 当前时间
date "+%Y-%m-%d %H:%M:%S"    # 格式化时间（脚本里常用）
cal                      # 日历
whoami                   # 当前用户名
```

### 15.2 硬件信息

```bash
lscpu                    # CPU 信息（核数、型号、架构）
nproc                    # CPU 核心数（脚本里常用）
cat /proc/cpuinfo        # CPU 详细信息
free -h                  # 内存使用情况（-h 人类可读）
cat /proc/meminfo        # 内存详细信息
lsblk                    # 块设备（硬盘分区）列表
df -h                    # 磁盘分区使用情况
lspci                    # PCI 设备（显卡、网卡）
lsusb                    # USB 设备
dmidecode                # 硬件详情（需 root）
```

> **注意 `free` 的输出**：Linux 会拿空闲内存做磁盘缓存，所以 `free` 很小不是问题。真正可用内存看 `available` 列：
> ```bash
> $ free -h
>                total        used        free      shared  buff/cache   available
> Mem:           3.8Gi       1.5Gi       200Mi        50Mi       2.1Gi       2.0Gi
> ```
> `buff/cache` 2.1G 是可回收的，**内存压力要看 `available`**。

### 15.3 环境变量（补充）

```bash
echo $PATH               # 查看 PATH（命令搜索路径，冒号分隔）
echo $HOME               # 家目录
env                      # 查看所有环境变量
export PATH=$PATH:/usr/local/bin        # 临时追加 PATH
export MY_VAR="hello"    # 定义环境变量
unset MY_VAR             # 删除环境变量
```

**永久生效的配置文件**（从上到下，越往下越晚加载、优先级越高）：

| 文件 | 作用范围 | 加载时机 |
| --- | --- | --- |
| `/etc/profile` | 所有用户 | 登录时 |
| `/etc/bash.bashrc` | 所有用户 | 打开 bash 时 |
| `~/.bash_profile` / `~/.profile` | 单个用户 | 登录时 |
| **`~/.bashrc`** | 单个用户 | 打开 bash 时（**最常用**） |

```bash
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
source ~/.bashrc         # 立即生效（或重启终端）
```

> **`source` 与 `.` 等价**：`source ~/.bashrc` = `. ~/.bashrc`，表示「在当前 shell 中执行脚本」，所以脚本里 `export` 的变量能留下来。直接 `./script.sh` 是在子 shell 执行，变量不会带回当前终端。

### 15.4 命令别名 `alias`（补充）

```bash
alias                    # 查看所有别名
alias ll='ls -alhF'      # 定义别名（临时）
unalias ll               # 删除别名
```

**推荐加入 `~/.bashrc` 的实用别名**：

```bash
alias ll='ls -alhF --color=auto'
alias la='ls -A'
alias l='ls -CF'
alias ..='cd ..'
alias ...='cd ../..'
alias grep='grep --color=auto'
alias df='df -h'
alias du='du -h'
alias ports='ss -tulnp'
alias myip='curl -s ifconfig.me'
alias h='history'
alias rm='rm -i'         # 安全保护，删除前询问
```

---

## 第十六部分 网络与远程连接（补充）

### 16.1 网络配置查看

```bash
ip addr                  # 查看网卡与 IP（新命令，推荐）
ip a                     # 简写
ifconfig                 # 老命令（net-tools 包，新系统可能没装）
ip route                 # 查看路由表
ip neigh                 # 查看 ARP 表（局域网设备）
hostname -I              # 只显示本机 IP 地址（脚本常用）
cat /etc/resolv.conf     # DNS 配置
cat /etc/hosts           # 本地 hosts 映射
```

### 16.2 端口与连接

```bash
ss -tulnp                # 【推荐】查看所有监听端口及进程
netstat -tulnp           # 老命令，功能同上（net-tools 包）
ss -tulnp | grep :80     # 查谁占用了 80 端口
ss -an | grep ESTAB | wc -l    # 统计已建立的连接数
lsof -i:8080             # 查谁占用 8080 端口（非常直观）
lsof -i -P -n | grep LISTEN    # 列出所有监听端口
```

**`ss -tulnp` 参数含义**：`-t` TCP，`-u` UDP，`-l` 监听中，`-n` 不解析服务名（显示数字端口），`-p` 显示进程。

### 16.3 连通性测试

```bash
ping baidu.com                   # 测试连通性（Ctrl+c 停止）
ping -c 4 baidu.com              # 只发 4 个包
curl https://api.github.com      # 发起 HTTP 请求（返回响应体）
curl -I https://baidu.com        # 只看响应头
curl -o file.zip https://x/f.zip # 下载并保存为指定文件名
curl -O https://x/file.zip       # 下载并保持原名
curl -L url                      # 跟随重定向
curl -X POST -d 'a=1' url        # POST 请求
wget https://x/file.zip          # 下载文件
wget -c https://x/big.zip        # 断点续传
traceroute baidu.com             # 追踪路由路径
dig baidu.com                    # DNS 查询
nslookup baidu.com               # DNS 查询
telnet host 22                   # 测试某端口是否可达
nc -zv host 22                   # 测试端口连通性（更现代）
```

> **排查网络问题的标准流程**：
> `ping 127.0.0.1`（本机协议栈）→ `ping 网关`（局域网）→ `ping 8.8.8.8`（外网 IP）→ `ping baidu.com`（DNS）
> 哪一步断了，问题就定位在哪一层。

### 16.4 SSH 远程连接（最重要的运维技能）

```bash
ssh user@192.168.1.100           # 连接远程服务器
ssh -p 2222 user@host            # 指定端口
ssh -i ~/.ssh/mykey.pem ubuntu@host    # 使用指定私钥（云服务器常用）

# 免密登录配置（必学）
ssh-keygen -t ed25519 -C "your@email.com"      # 生成密钥对（一路回车）
# 或 ssh-keygen -t rsa -b 4096
ls ~/.ssh/                       # id_ed25519（私钥，绝不能外泄）、id_ed25519.pub（公钥）
ssh-copy-id user@host            # 把公钥传到服务器（之后免密登录）
ssh-add ~/.ssh/id_ed25519        # 把私钥加入 ssh-agent（私钥有密码时用）
```

**SSH 客户端配置 `~/.ssh/config`**（配置后可直接 `ssh myserver`）：

```
Host myserver
    HostName 192.168.1.100
    User ubuntu
    Port 22
    IdentityFile ~/.ssh/id_ed25519
    ServerAliveInterval 60        # 每 60 秒发心跳，防止断连

Host *
    ServerAliveInterval 30
```

```bash
chmod 600 ~/.ssh/config
chmod 700 ~/.ssh
```

**文件传输**：

```bash
scp file.txt user@host:/tmp/            # 上传单个文件
scp -r dir/ user@host:/tmp/             # 上传目录
scp user@host:/var/log/app.log ./       # 下载
scp -P 2222 file.txt user@host:/tmp/    # 指定端口（注意是大写 P）

# rsync：增量同步，断点续传，传输大文件/目录首选
rsync -avz ./src/ user@host:/data/src/  # -a 归档、-v 详细、-z 压缩
rsync -avz --delete ./dist/ user@host:/var/www/    # --delete 保持两端完全一致
rsync -avz -e "ssh -p 2222" ./src/ user@host:/data/
```

> `scp` 的 `-P` 是大写，`ssh` 的 `-p` 是小写 —— 这是经典易错点。
> 目录结尾的 `/` 有讲究：`rsync -avz src/ dest/` 表示「把 src **里面的内容**同步到 dest 里」，不带 `/` 则会在 dest 下创建一个 src 子目录。

---

## 第十七部分 Shell 脚本编程（补充）

教程的最后一课预告讲 Shell 脚本，这里把核心内容补全 —— **把零散命令串成可复用的自动化程序，才是 Linux 真正的威力所在**。

### 17.1 第一个脚本

```bash
#!/bin/bash
# 上面这行叫 shebang，必须用绝对路径，指定解释器。第一行必须是它

echo "Hello Linux"
```

```bash
chmod +x hello.sh        # 加执行权限
./hello.sh               # 执行（./ 表示当前目录）
bash hello.sh            # 或直接指定解释器执行（不需要 x 权限，也不需要 shebang）
sh hello.sh
bash -x hello.sh         # 调试模式：逐行打印执行过程（排查脚本 bug 神器）
bash -n hello.sh         # 只检查语法错误，不执行
```

> 必须先 `chmod +x` 才能 `./hello.sh`；直接写 `hello.sh` 会报 command not found —— 因为当前目录不在 `PATH` 里（安全设计）。

### 17.2 变量

```bash
name="Linux"             # 定义变量（= 两边【不能有空格】！）
echo $name               # 使用变量
echo ${name}             # 推荐写法，花括号能明确变量边界
echo "Hello ${name}!"    # 双引号内变量会被解析
echo 'Hello ${name}!'    # 【单引号内原样输出】，不解析变量

readonly PI=3.14         # 只读变量
unset name               # 删除变量

result=$(date)           # 【推荐】命令替换，把命令输出赋给变量
result=`date`            # 老式写法（反引号），不推荐
count=$(ls | wc -l)      # 命令可以嵌套管道

echo "文件数：$count"     # 双引号里可以直接写中文和变量
```

**三种引号的区别（必考知识点）**：

| 引号 | 变量解析 | 命令替换 | 转义符 | 典型用途 |
| --- | --- | --- | --- | --- |
| 双引号 `" "` | **是** | **是** | 部分生效 | 最常用，保留空格：`echo "$var"` |
| 单引号 `' '` | 否 | 否 | 否 | 原样输出：`echo '$PATH'` |
| 反引号 `` ` ` `` | 是 | **是** | — | 命令替换（已过时，用 `$()`） |
| 无引号 | 是 | 是 | — | 会被词分割和通配符展开，**危险** |

### 17.3 特殊变量

| 变量 | 含义 |
| --- | --- |
| `$0` | 脚本自身的名字 |
| `$1` ~ `$9` | 第 1~9 个参数 |
| `${10}` | 第 10 个及以后的参数（**必须加花括号**） |
| `$#` | 参数个数 |
| `$*` | 所有参数（作为一个整体字符串） |
| `$@` | 所有参数（各自独立，**遍历时用这个**） |
| `$?` | **上一条命令的退出状态码**（0 = 成功，非 0 = 失败） |
| `$$` | 当前脚本的 PID |
| `$!` | 最后一个后台进程的 PID |
| `$USER` | 当前用户名 |
| `$HOME` | 家目录 |
| `$PWD` | 当前目录 |

```bash
#!/bin/bash
echo "脚本名: $0"
echo "第一个参数: $1"
echo "参数个数: $#"
echo "所有参数: $@"

ls /nonexistent
echo "上一条命令的返回值: $?"      # 输出 2（失败）
```

> **`$?` 是脚本里做错误处理的基础**：
> ```bash
> if [ $? -eq 0 ]; then echo "成功"; else echo "失败"; fi
> # 或更简洁：
> command && echo "成功" || echo "失败"
> ```

### 17.4 输入输出与运算

```bash
read -p "请输入名字: " name     # 读取用户输入到变量
read -s -p "密码: " pwd         # -s：静默输入（不回显）
echo "你好, $name"

# 算术运算（三种写法，推荐第一种）
echo $((1 + 2))              # 推荐：双括号，变量不用加 $
echo $((a + b))
echo $[1+2]                  # 老写法
expr 1 + 2                   # 外部命令，运算符两边必须有空格
let "c = a + b"              # let 命令

# 支持的运算：+ - * / % （取模） ** （幂）
echo $((10 / 3))             # 3（整数除法，直接截断小数）
echo $((10 % 3))             # 1
echo $((RANDOM % 100))       # 0~99 的随机数
```

> **bash 只支持整数运算**。需要小数时用 `bc`：
> ```bash
> echo "scale=2; 10/3" | bc          # 3.33
> echo "$((1+2)) * 1.5" | bc
> ```

### 17.5 条件判断

**`test` / `[ ]` / `[[ ]]`**：

```bash
# 数值比较（-eq -ne -gt -ge -lt -le）
[ $a -eq $b ]        # 等于
[ $a -ne $b ]        # 不等于
[ $a -gt $b ]        # 大于
[ $a -ge $b ]        # 大于等于
[ $a -lt $b ]        # 小于
[ $a -le $b ]        # 小于等于

# 字符串比较（= != -z -n）
[ "$a" = "$b" ]      # 相等（注意：字符串比较用 = 或 ==，不是 -eq）
[ "$a" != "$b" ]     # 不等
[ -z "$a" ]          # 长度为 0（empty）
[ -n "$a" ]          # 长度不为 0
[[ "$a" == a* ]]     # 通配符匹配（[[ ]] 才支持）
[[ "$a" =~ ^[0-9]+$ ]]   # 正则匹配（[[ ]] 才支持）

# 文件测试（最常用的一组）
[ -e file ]          # 存在（exist）
[ -f file ]          # 存在且是普通文件
[ -d dir ]           # 存在且是目录
[ -r file ]          # 可读
[ -w file ]          # 可写
[ -x file ]          # 可执行
[ -s file ]          # 存在且非空（size > 0）
[ -L file ]          # 是软链接
[ f1 -nt f2 ]        # f1 比 f2 新（newer than）

# 逻辑运算
[ 条件1 ] && [ 条件2 ]        # 与
[ 条件1 ] || [ 条件2 ]        # 或
[ ! 条件 ]                    # 非
[ -f "$f" -a -r "$f" ]        # -a = and（在单个 [] 内）
```

> **重要**：`[` 后面和 `]` 前面**必须有空格**！写成 `[ -f a ]` 才对，`[-f a]` 会报错。
> **变量一定要加双引号**：`[ "$a" = "b" ]`，否则变量为空时语句变成 `[ = "b" ]` 直接语法错误。这是 Shell 脚本最常见的新手坑。

**`if` 语句**：

```bash
#!/bin/bash
if [ -f "/etc/passwd" ]; then
    echo "文件存在"
elif [ -d "/etc/passwd" ]; then
    echo "是目录"
else
    echo "不存在"
fi

# 判断命令是否执行成功（比判断文件更常用）
if grep -q "error" app.log; then
    echo "日志中发现错误"
fi

# 判断命令存在与否
if command -v docker &> /dev/null; then
    echo "docker 已安装"
fi

# 简洁写法
[ -f a.txt ] && echo "存在" || echo "不存在"
```

**`case` 语句**（多分支，比一长串 elif 清晰）：

```bash
#!/bin/bash
read -p "请输入 start|stop|restart: " op
case "$op" in
    start)
        echo "启动服务"
        ;;
    stop)
        echo "停止服务"
        ;;
    restart)
        echo "重启服务"
        ;;
    *)
        echo "用法: $0 {start|stop|restart}"
        exit 1
        ;;
esac
```

### 17.6 循环

```bash
# for：遍历列表
for i in 1 2 3 4 5; do
    echo "第 $i 次"
done

for name in alice bob carol; do echo "Hello $name"; done

# for：数字范围（两种写法）
for i in {1..10}; do echo $i; done
for ((i=1; i<=10; i++)); do echo $i; done
for i in $(seq 1 2 10); do echo $i; done     # 步长 2：1 3 5 7 9

# for：遍历文件（最常用）
for file in *.log; do
    echo "处理 $file"
    gzip "$file"
done

# for：遍历命令输出
for ip in $(cat ip_list.txt); do
    ping -c 1 "$ip" &> /dev/null && echo "$ip 在线" || echo "$ip 离线"
done

# while：条件循环
count=1
while [ $count -le 5 ]; do
    echo "count = $count"
    ((count++))
done

# while：逐行读取文件（处理文本的标准姿势）
while IFS= read -r line; do
    echo "行内容: $line"
done < file.txt

# while：只读日志
tail -f app.log | while read -r line; do
    echo "$line" | grep -q "ERROR" && echo "发现错误: $line"
done

# until：条件为假时循环（与 while 相反）
until [ $count -gt 5 ]; do
    echo $count
    ((count++))
done

# 循环控制
break        # 跳出整个循环
continue     # 跳过本次，进入下一轮
```

### 17.7 函数

```bash
#!/bin/bash

# 定义（function 关键字可省略）
function greet() {
    local name=$1        # local：局部变量，不污染全局（强烈推荐）
    echo "Hello, $name"
    return 0             # 返回值只能是 0~255，0 表示成功
}

greet "Linux"            # 调用（注意：传参不用括号！）

# 用 echo 返回字符串（这才是 Shell 里返回数据的正道）
get_time() {
    echo "$(date '+%Y-%m-%d %H:%M:%S')"
}
now=$(get_time)
echo "当前时间: $now"
```

> 函数参数也用 `$1` `$2` `$#`，和脚本参数一样（在函数内部它们指的是**函数的**参数）。

### 17.8 实战脚本：一键备份

把前面所有知识串起来：

```bash
#!/bin/bash
# backup.sh - 目录备份脚本
set -euo pipefail        # 严格模式：出错即退出、未定义变量报错、管道错误传递

SRC="/var/www/html"
DEST="/data/backup"
DATE=$(date +%Y%m%d_%H%M%S)
KEEP_DAYS=7

# 检查源目录
if [ ! -d "$SRC" ]; then
    echo "[ERROR] 源目录不存在: $SRC"
    exit 1
fi

# 创建目标目录
mkdir -p "$DEST"

# 打包备份
BACKUP_FILE="${DEST}/html_${DATE}.tar.gz"
echo "[INFO] 开始备份 $SRC -> $BACKUP_FILE"
tar -czf "$BACKUP_FILE" -C "$(dirname "$SRC")" "$(basename "$SRC")"

# 检查结果
if [ $? -eq 0 ]; then
    echo "[OK] 备份成功: $BACKUP_FILE ($(du -h "$BACKUP_FILE" | cut -f1))"
else
    echo "[ERROR] 备份失败"
    exit 1
fi

# 清理旧备份
echo "[INFO] 清理 ${KEEP_DAYS} 天前的备份..."
find "$DEST" -name "html_*.tar.gz" -mtime +${KEEP_DAYS} -delete
echo "[OK] 完成"
```

**`set -euo pipefail` 的含义**（写生产脚本的标配）：

| 选项 | 作用 |
| --- | --- |
| `set -e` | 任何命令返回非 0 就**立即退出脚本**（防止错误累积） |
| `set -u` | 使用未定义变量时报错（防止 `rm -rf $UNDEF/` 变成 `rm -rf /`） |
| `set -o pipefail` | 管道中任一环节失败就整体失败 |
| `set -x` | 打印每条执行的命令（调试用） |

---

## 第十八部分 服务管理与计划任务（补充）

### 18.1 systemd 服务管理

现代 Linux（Ubuntu 16.04+、CentOS 7+）统一用 **systemd** 管理服务。

```bash
systemctl start nginx           # 启动服务
systemctl stop nginx            # 停止服务
systemctl restart nginx         # 重启服务
systemctl reload nginx          # 重读配置（不中断连接，优先用这个）
systemctl status nginx          # 查看状态（含最近几行日志）
systemctl enable nginx          # 设置【开机自启】
systemctl disable nginx         # 取消开机自启
systemctl is-enabled nginx      # 查看是否开机自启
systemctl is-active nginx       # 查看是否正在运行

systemctl list-units --type=service          # 列出所有服务
systemctl list-units --type=service --state=running    # 只看运行中的
systemctl daemon-reload         # 【改完 service 文件后必须执行】重载配置
```

> **老命令对照**（有些老教程/老系统还在用）：
> ```bash
> service nginx start       # 等价 systemctl start nginx
> /etc/init.d/nginx start   # 更老的 SysVinit 方式
> chkconfig nginx on        # 等价 systemctl enable nginx
> ```

### 18.2 查看日志 `journalctl`

```bash
journalctl                          # 查看全部系统日志
journalctl -u nginx                 # 只看某个服务的日志
journalctl -u nginx -f              # 实时跟踪（-f = follow，等同 tail -f）
journalctl -u nginx --since "2026-09-01" --until "2026-09-02"
journalctl -u nginx --since "10 min ago"
journalctl -u nginx -n 100          # 只看最近 100 行
journalctl -p err                   # 只看错误级别及以上
journalctl -xe                      # 查看最近日志并给出解释（排错首选）
journalctl --disk-usage             # 查看日志占用空间
sudo journalctl --vacuum-size=500M  # 清理日志到 500M 以内
```

### 18.3 编写自己的 systemd 服务

把 `nohup` 跑的程序改成正规服务，就能开机自启、崩溃自动重启、统一日志管理。

```bash
sudo vim /etc/systemd/system/myapp.service
```

```ini
[Unit]
Description=My Python App
After=network.target

[Service]
Type=simple
User=ubuntu
WorkingDirectory=/opt/myapp
ExecStart=/usr/bin/python3 /opt/myapp/app.py
Restart=always              # 崩溃自动重启
RestartSec=5
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl daemon-reload           # 改完必须执行
sudo systemctl enable --now myapp      # 开机自启 + 立即启动
systemctl status myapp
journalctl -u myapp -f                 # 看日志
```

### 18.4 计划任务 `crontab`

```bash
crontab -e               # 编辑当前用户的定时任务
crontab -l               # 查看当前用户的定时任务
crontab -r               # 删除所有定时任务（慎用）
crontab -u root -e       # 编辑 root 的定时任务（需 sudo）
cat /etc/crontab         # 系统级任务文件
ls /etc/cron.d/          # 系统级任务目录
```

**时间格式（5 个字段）**：

```
┌───────────── 分钟 (0-59)
│ ┌─────────── 小时 (0-23)
│ │ ┌───────── 日 (1-31)
│ │ │ ┌─────── 月 (1-12)
│ │ │ │ ┌───── 星期 (0-7，0 和 7 都是周日)
│ │ │ │ │
* * * * *  要执行的命令
```

```bash
# 每天凌晨 2 点备份
0 2 * * * /opt/scripts/backup.sh >> /var/log/backup.log 2>&1

# 每 5 分钟执行一次
*/5 * * * * /usr/bin/python3 /opt/monitor.py

# 每小时的第 30 分钟
30 * * * * /opt/scripts/check.sh

# 每周一早上 8 点
0 8 * * 1 /opt/scripts/weekly_report.sh

# 每月 1 号凌晨 3 点
0 3 1 * * /opt/scripts/monthly.sh

# 每天 9:00 和 18:00
0 9,18 * * * /opt/scripts/sync.sh

# 工作日（周一到周五）每天 10 点
0 10 * * 1-5 /opt/scripts/work.sh

# 开机自启执行一次
@reboot /opt/scripts/startup.sh
```

**特殊时间串**：

| 写法 | 等价 | 含义 |
| --- | --- | --- |
| `@reboot` | — | 开机时执行一次 |
| `@daily` / `@midnight` | `0 0 * * *` | 每天 0 点 |
| `@hourly` | `0 * * * *` | 每小时 |
| `@weekly` | `0 0 * * 0` | 每周日 0 点 |
| `@monthly` | `0 0 1 * *` | 每月 1 号 0 点 |
| `@yearly` | `0 0 1 1 *` | 每年 1 月 1 号 |

> **crontab 的三大坑**：
> 1. **环境变量极少**（PATH 只有 `/usr/bin:/bin`），所以**命令一律写绝对路径**（用 `which python3` 查）
> 2. **不会加载 `~/.bashrc`**，需要的环境变量要在 crontab 顶部显式声明：`PATH=/usr/local/bin:/usr/bin:/bin`
> 3. **输出不会显示**，务必重定向到日志文件（`>> /tmp/x.log 2>&1`），否则出问题无从查起
>
> 调试技巧：`* * * * * date >> /tmp/cron_test.log` 先确认 cron 本身在跑；`grep CRON /var/log/syslog` 查看 cron 执行记录。

### 18.5 开机启动的其他方式（补充）

```bash
/etc/rc.local            # 传统方式（需 chmod +x，且 systemd 下要启用 rc-local.service）
~/.bashrc                # 用户登录时执行（不是开机，是登录）
/etc/profile.d/*.sh      # 所有用户登录时执行
crontab 的 @reboot       # 开机执行一次
systemd service          # 【推荐】管理长期运行的服务
```

### 18.6 关机与重启（补充）

```bash
sudo shutdown -h now     # 立即关机
sudo shutdown -r now     # 立即重启
sudo shutdown -h +10     # 10 分钟后关机
sudo shutdown -c         # 取消定时的关机
sudo reboot              # 重启
sudo halt                # 停机
sudo poweroff            # 关机
init 0                   # 关机（SysVinit 方式）
init 6                   # 重启
```

---

## 附录 A 命令速查表

### A.1 文件与目录

| 命令 | 作用 | 高频用法 |
| --- | --- | --- |
| `ls` | 列出目录内容 | `ls -lah`、`ls -ltr`、`ls -li` |
| `cd` | 切换目录 | `cd ~`、`cd -`、`cd ..` |
| `pwd` | 显示当前路径 | `pwd` |
| `mkdir` | 创建目录 | `mkdir -p a/b/c` |
| `rmdir` | 删除空目录 | `rmdir d` |
| `touch` | 创建空文件/更新时间 | `touch f.txt` |
| `cp` | 复制 | `cp -r src dst`、`cp -a src dst` |
| `mv` | 移动/重命名 | `mv old new` |
| `rm` | 删除 | `rm -rf dir`（慎用） |
| `ln` | 创建链接 | `ln -s src link`、`ln src hardlink` |
| `file` | 查看文件类型 | `file unknown` |
| `stat` | 查看文件详细属性 | `stat f` |
| `du` | 查看占用空间 | `du -sh *`、`du -h --max-depth=1` |
| `df` | 查看磁盘剩余 | `df -h`、`df -i` |
| `tree` | 树状显示目录 | `tree -L 2` |

### A.2 查看与编辑文本

| 命令 | 作用 | 高频用法 |
| --- | --- | --- |
| `cat` | 显示全部内容 | `cat -n f`（小文件） |
| `less` | 分页查看（可搜索） | `less /var/log/syslog` |
| `more` | 分页查看 | `more f` |
| `head` | 查看开头 | `head -20 f` |
| `tail` | 查看结尾 | `tail -20 f`、`tail -f app.log` |
| `wc` | 统计行数/词数 | `wc -l f` |
| `grep` | 文本搜索 | `grep -rn "x" ./`、`grep -v x f` |
| `sed` | 批量替换 | `sed -i 's/a/b/g' f` |
| `awk` | 按列处理 | `awk '{print $1}' f`、`awk -F: '{print $1}'` |
| `sort` | 排序 | `sort -rn`、`sort -u` |
| `uniq` | 去重（需先 sort） | `sort f \| uniq -c` |
| `cut` | 按列切分 | `cut -d: -f1` |
| `tr` | 字符转换 | `tr -d '\r'` |
| `diff` | 比较文件差异 | `diff -u a b` |
| `vim` / `nano` | 编辑器 | `vim f` |

### A.3 权限与所有权

| 命令 | 作用 | 高频用法 |
| --- | --- | --- |
| `chmod` | 修改权限 | `chmod 755 f`、`chmod +x f`、`chmod u+x f` |
| `chown` | 修改所有者 | `chown user:group f`、`chown -R www-data /var/www` |
| `chgrp` | 修改所属组 | `chgrp -R dev /data` |
| `umask` | 默认权限掩码 | `umask 022` |
| `sudo` | 临时提权 | `sudo !!` |
| `su` | 切换用户 | `su - user` |

### A.4 查找

| 命令 | 作用 | 高频用法 |
| --- | --- | --- |
| `find` | 实时查找文件 | `find / -name "*.conf"`、`find . -mtime +7 -delete` |
| `locate` | 索引查找（快） | `locate nginx.conf`（先 `updatedb`） |
| `which` | 查命令路径 | `which python3` |
| `whereis` | 查二进制/源码/手册 | `whereis nginx` |
| `type` | 判断命令类型 | `type cd` |
| `grep` | 按内容查找 | `grep -rn "TODO" ./src` |

### A.5 压缩归档

```bash
tar -czvf a.tar.gz dir/          # 打包压缩
tar -xzvf a.tar.gz -C /opt/      # 解压到 /opt
tar -tzvf a.tar.gz               # 查看内容
zip -r a.zip dir/                # zip 压缩
unzip a.zip -d /opt/             # zip 解压
gzip -k f / gunzip f.gz          # gzip 压缩/解压
zgrep "error" f.gz               # 不解压直接搜
```

### A.6 进程与系统

| 命令 | 作用 | 高频用法 |
| --- | --- | --- |
| `ps` | 查看进程 | `ps aux`、`ps -ef` |
| `top` / `htop` | 实时监控 | `top`（P 按 CPU，M 按内存） |
| `kill` | 终止进程 | `kill -9 PID`、`kill -15 PID` |
| `pkill` | 按名杀进程 | `pkill -f "python app"` |
| `killall` | 杀同名进程 | `killall nginx` |
| `jobs` / `fg` / `bg` | 作业控制 | `Ctrl+z` 挂起，`bg` 后台，`fg` 前台 |
| `nohup` | 脱离终端运行 | `nohup cmd &> log &` |
| `free` | 内存 | `free -h` |
| `df` / `du` | 磁盘 | `df -h`、`du -sh *` |
| `uptime` | 负载 | `uptime` |
| `uname` | 内核信息 | `uname -a` |
| `lscpu` / `lsblk` | CPU / 磁盘信息 | `lscpu`、`lsblk` |
| `systemctl` | 服务管理 | `systemctl restart nginx` |
| `journalctl` | 系统日志 | `journalctl -u nginx -f` |
| `crontab` | 定时任务 | `crontab -e` |

### A.7 网络

| 命令 | 作用 | 高频用法 |
| --- | --- | --- |
| `ip` | 网络配置 | `ip a`、`ip route` |
| `ss` | 端口连接 | `ss -tulnp` |
| `lsof` | 查端口占用 | `lsof -i:8080` |
| `ping` | 连通性 | `ping -c 4 host` |
| `curl` | HTTP 请求 | `curl -I url`、`curl -O url` |
| `wget` | 下载 | `wget -c url` |
| `ssh` | 远程登录 | `ssh -p 22 user@host` |
| `scp` | 远程复制 | `scp -r dir/ user@host:/tmp/` |
| `rsync` | 增量同步 | `rsync -avz src/ user@host:/dst/` |
| `dig` / `nslookup` | DNS 查询 | `dig baidu.com` |
| `traceroute` | 路由追踪 | `traceroute baidu.com` |

### A.8 用户与包管理

```bash
# 用户
sudo useradd -m -s /bin/bash user      # 创建用户
sudo passwd user                        # 设密码
sudo usermod -aG sudo user              # 给管理员权限
sudo userdel -r user                    # 删除用户
id / groups / whoami / who / w / last   # 查询

# 包管理（Ubuntu/Debian）
sudo apt update && sudo apt upgrade     # 更新
sudo apt install -y pkg                 # 安装
sudo apt remove pkg / purge pkg         # 卸载
apt search pkg / apt show pkg           # 搜索/详情
dpkg -i x.deb / dpkg -l / dpkg -S file # 本地包操作
```

---

## 附录 B Vim 速查表

### B.1 模式切换

| 操作 | 效果 |
| --- | --- |
| `vim file` | 打开文件（默认**命令模式**） |
| `i` / `I` | 光标前 / 行首 → **插入模式** |
| `a` / `A` | 光标后 / 行尾 → **插入模式** |
| `o` / `O` | 下一行 / 上一行 → **插入模式** |
| `ESC` | 回到**命令模式**（万能键） |
| `:` | 进入**尾行模式** |
| `v` / `V` / `Ctrl+v` | 可视 / 可视行 / 可视块 |
| `R` | 替换模式 |

### B.2 光标移动

| 键 | 效果 | 键 | 效果 |
| --- | --- | --- | --- |
| `h j k l` | 左 下 上 右 | `gg` | 文件首行 |
| `w` / `b` | 下一词首 / 上一词首 | `G` | 文件末行 |
| `e` | 词尾 | `nG` / `:n` | 跳到第 n 行 |
| `0` / `^` | 行首（绝对/首个非空字符） | `Ctrl+f` / `Ctrl+b` | 下翻页 / 上翻页 |
| `$` | 行尾 | `Ctrl+d` / `Ctrl+u` | 下半页 / 上半页 |
| `H` / `M` / `L` | 屏幕顶 / 中 / 底 | `{` / `}` | 上一段 / 下一段 |

### B.3 编辑操作

| 键 | 效果 | 键 | 效果 |
| --- | --- | --- | --- |
| `yy` / `nyy` | 复制 1 行 / n 行 | `dd` / `ndd` | 剪切 1 行 / n 行 |
| `yw` / `y$` / `yG` | 复制词 / 到行尾 / 到文末 | `dw` / `d$` / `dG` | 删除词 / 到行尾 / 到文末 |
| `p` / `P` | 粘贴到下 / 上一行 | `x` | 删除当前字符 |
| `u` | 撤销 | `Ctrl+r` | 重做 |
| `.` | 重复上次操作 | `~` | 大小写翻转 |
| `>>` / `<<` | 右缩进 / 左缩进 | `gg=G` | 全文格式化 |

### B.4 查找与替换

```bash
/keyword            向下查找
?keyword            向上查找
n / N               下一个 / 上一个
* / #               向下/向上查找光标所在单词
/keyword\c          忽略大小写查找
:set ic / :set noic 开启 / 关闭忽略大小写
:set hls / :noh     高亮匹配 / 临时取消高亮

:s/old/new          当前行第一个
:s/old/new/g        当前行所有
:1,10s/old/new/g    第 1~10 行
:%s/old/new/g       全文（最常用）
:%s/old/new/gc      全文并逐个确认
```

### B.5 保存退出与设置

```bash
:w                  保存
:w file             另存为
:q                  退出
:q!                 强制退出不保存
:wq  /  :x  /  ZZ  保存并退出
:e!                 放弃修改重新载入

:set nu / :set nonu         显示 / 隐藏行号
:set ic / :set noic         忽略 / 区分大小写
:set hls / :set nohls       高亮搜索 / 取消
:set paste / :set nopaste   粘贴模式（粘贴代码不变形）
:set autoindent             自动缩进
:syntax on                  语法高亮
:source ~/.vimrc            重新加载配置
```

### B.6 分屏

```bash
:sp file / :vsp file        水平 / 垂直分屏
vim -O a.txt b.txt          垂直分屏打开
Ctrl+w h/j/k/l              在窗口间移动
Ctrl+w =                    等分窗口
:q                          关闭当前窗口
```

---

## 附录 C 终端快捷键与常见坑

### C.1 必背终端快捷键

| 快捷键 | 作用 |
| --- | --- |
| **Tab** | **命令/路径自动补全（最高频，一定要用）** |
| **↑ / ↓** | 浏览历史命令 |
| **Ctrl + r** | **反向搜索历史命令**（输入关键词再按，超级实用） |
| **Ctrl + c** | **强制终止当前命令** |
| **Ctrl + d** | 退出当前 shell（等价 `exit`）；空行时也可用作 EOF |
| **Ctrl + l** | 清屏（等价 `clear`） |
| **Ctrl + a** | 光标跳到**行首** |
| **Ctrl + e** | 光标跳到**行尾** |
| **Ctrl + u** | 删除光标到**行首**的全部内容 |
| **Ctrl + k** | 删除光标到**行尾**的全部内容 |
| **Ctrl + w** | 删除光标前的一个单词 |
| **Ctrl + z** | 挂起当前进程到后台（`fg` 拉回） |
| **Ctrl + s** | 锁定终端（误按会「卡死」，按 `Ctrl + q` 解锁！） |
| **Ctrl + q** | 解锁终端 |
| **!!** | 重复上一条命令 |
| **!$** | 上一条命令的最后一个参数 |
| **Ctrl + Shift + C/V** | 终端复制粘贴（`Ctrl+C` 在终端是终止命令，不是复制） |

### C.2 新手最容易踩的 12 个坑

1. **`rm -rf` 删库跑路** —— 删除不可逆，重要数据先备份；路径前先 `pwd` + `ls` 确认。
2. **空格问题** —— `a = b` 在赋值时是错的（必须 `a=b`）；`rm -rf / home/user` 多了个空格就毁了。
3. **`Permission denied`** —— 缺权限，加 `sudo`；或对文件没 `x` 权限就 `./script.sh`。
4. **`command not found`** —— ① 命令没装；② 执行当前目录脚本忘了加 `./`；③ PATH 没配好。
5. **`No such file or directory`** —— 路径写错；Linux **大小写敏感**；Windows 传来的脚本有 `\r`（用 `tr -d '\r'` 或 `dos2unix`）。
6. **卡在 Vim 里出不来** —— `ESC` 然后 `:q!` 回车。
7. **忘了加 `sudo`** —— `sudo !!` 一键补上。
8. **`cat` 打开几 GB 的大日志** —— 终端被刷爆卡死。改用 `less` 或 `tail -n 100`。
9. **`rm` 了大文件但磁盘没释放** —— 还有进程占着，`lsof | grep deleted` 找到并重启该进程。
10. **改了配置文件不生效** —— 忘了 `source ~/.bashrc` 或 `systemctl daemon-reload` / `systemctl reload`。
11. **`chmod -R 777`** —— 图省事给全部权限，等于把服务器大门敞开。正确做法是精确设置 `644`/`755` + `chown`。
12. **crontab 不执行** —— 环境变量缺失，命令要写绝对路径，并重定向输出到日志。

### C.3 排查问题的通用思路

```
服务起不来？
  systemctl status <service>      看状态和最近日志
  journalctl -u <service> -n 50   看详细日志
  ss -tulnp | grep <port>        端口是否被占用
  tail -f /var/log/<app>.log     看应用自己的日志

磁盘满了？
  df -h                          哪个分区满了
  du -sh /* 2>/dev/null | sort -hr | head   哪个目录最大
  du -sh /var/log/*              通常是日志
  find / -size +1G               找大文件
  df -i                          inode 是否耗尽

机器很卡？
  uptime                         看负载
  top                            看 CPU/内存占用最高的进程（P / M 排序）
  free -h                        看内存（重点看 available）
  iostat / iotop                 看磁盘 I/O 是否瓶颈（wa 高）

网络不通？
  ping 127.0.0.1                 本机协议栈
  ping 网关                       局域网
  ping 8.8.8.8                    外网 IP
  ping baidu.com                  DNS 解析
  ss -tulnp                       服务是否在监听
  curl -I localhost:8080          本机能否访问
  防火墙：sudo ufw status / iptables -L
```

### C.4 推荐的学习路线

1. **把基础命令敲熟**（本笔记第一 ~ 八部分），做到不看手册也能操作
2. **Vim 练到肌肉记忆**（`hjkl` / `yy` `p` `dd` / `:%s` / `:wq`）
3. **搞懂权限** —— 这是 Linux 与 Windows 最大的思维差异，也是 90% 的 "Permission denied" 的根源
4. **掌握管道与三剑客** —— `grep` / `sed` / `awk` 是文本处理的核武器
5. **写 Shell 脚本** —— 把重复工作自动化，这是分水岭
6. **学会看日志** —— `/var/log` + `journalctl`，排查问题的能力比会多少命令更重要
7. 进阶：`systemd` → 网络（`iptables` / `tcpdump`）→ 性能调优 → 容器（Docker / K8s）

---

## 结语

本笔记覆盖了教程的全部知识点，并额外补充了**重定向与管道、文本三剑客、查找搜索、压缩归档、软件包管理、用户与组、进程管理、系统监控、网络与 SSH、Shell 脚本、systemd 与计划任务**等教程未涉及的必备内容，另附三张速查表。

> **最后再强调一次**：Linux 是**练**出来的，不是看出来的。建议边看边在虚拟机里逐条敲一遍 —— 遇到报错不要慌，**报错信息本身就是最好的老师**，把它复制去搜索，你会记得比任何笔记都牢。

