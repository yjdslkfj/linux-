# 服务器系统管理 · Linux 学习笔记

> 本笔记基于《IT 运维师》课程第 63～78 讲字幕整理而成，面向**网络初学者**。
> 内容没有按"一讲一讲"罗列，而是按知识体系重新组织：**认识 Linux → 安装系统 → 系统管理 → 初始化与远程运维**。
> 所有关键词首次出现时均标注英文全称，课程中语焉不详或缺失的知识点已补充（标注为"📖 补充"），文末附**关键词中英文对照总表**和**常用命令速查表**。

---

## 目录

1. [Linux 系统概述](#一linux-系统概述)
2. [安装 Linux 系统（U 盘安装与 PXE 批量安装）](#二安装-linux-系统)
3. [服务器硬件管理（在 Linux 中查看硬件）](#三服务器硬件管理)
4. [Linux 文件管理（目录结构 / 命令 / vim）](#四linux-文件管理)
5. [归档与压缩](#五归档与压缩)
6. [用户与用户组管理](#六用户与用户组管理)
7. [权限管理](#七权限管理)
8. [磁盘管理](#八磁盘管理)
9. [网络管理](#九网络管理)
10. [防火墙与 SELinux](#十防火墙与-selinux)
11. [root 管理员密码重置](#十一root-管理员密码重置)
12. [SSH 远程登录](#十二ssh-远程登录)
- [附录 A：关键词中英文对照总表](#附录-a关键词中英文对照总表)
- [附录 B：常用命令速查表](#附录-b常用命令速查表)
- [附录 C：学习路线建议](#附录-c学习路线建议)

---

## 一、Linux 系统概述

### 1.1 操作系统是干什么的？

一台服务器 = **硬件**（CPU、内存、硬盘、网卡……）+ **操作系统（OS，Operating System）** + **应用软件**。

- 硬件本身是"废铁"，操作系统负责管理和调度这些硬件，给上层软件提供运行环境。
- 服务器领域绝大多数使用 **Linux** 操作系统（网站、数据库、云计算平台背后几乎都是它）；个人电脑上常见的则是 Windows 和 macOS。

> 💡 角色视角（课程原话很有意思）：
> - 系统应用工程师：不懂 Linux 寸步难行；
> - 程序员：懂 Linux 相当于多一条腿走路；
> - 网络工程师：掌握 Linux 也是必备加分技能。

### 1.2 Linux 的诞生

| 项目 | 内容 |
|---|---|
| 作者 | 林纳斯·托瓦兹（**Linus Torvalds**），芬兰赫尔辛基大学学生 |
| 起因 | 他上大学时对当时的教学系统 Minix 不满意，"为了跟老师对着干"而自己写了一个内核 |
| 发布时间 | **1991 年 10 月 5 日**正式对外发布 |
| 吉祥物 | 一只企鹅，名字叫 **Tux**（为什么是企鹅官方从未解释，网友众说纷纭） |
| 许可 | 开源（源代码公开），遵循 **GPL（GNU General Public License，GNU 通用公共许可证）** |

📖 **补充**：Linux 这个名字来自 **Linus + Minix**，它**不是缩写**。Linux 只是"内核（Kernel）"——操作系统的核心部分；我们平时安装使用的其实是各大厂商在内核基础上"穿上衣服"（加入安装器、软件包、桌面环境等）做出来的**发行版（Distribution）**。

### 1.3 Linux 的主要特点（8 条）

1. **一切皆文件**：Linux 中所有东西（包括 CPU、内存、硬盘等硬件）都以文件形式存在，每个文件都有确定用途，所有操作都围绕文件进行。这是 Linux 最重要的哲学。
2. **内核完全免费、开源**：源代码全网公开，全世界的爱好者都可以参与修改。
3. **完全兼容 POSIX 1.0 标准**。POSIX（**Portable Operating System Interface，可移植操作系统接口**）：为一个 POSIX 兼容系统编写的程序，可以在其他 POSIX 系统上编译执行。
4. **多用户、多任务**：允许多个用户通过不同方式**同时**登录同一台主机，各自执行不同任务，互不干扰。
5. **支持多线程和多 CPU**。
6. **有良好的界面**：既有图形化操作，也支持命令行。运维工程师更喜欢"黑白界面"（命令行），干脆利落、省资源。
7. **支持多平台**：电脑、手机、服务器、游戏机、机床都能跑。
8. **严格区分大小写**：`Test.txt` 和 `test.txt` 是两个不同的文件；命令、文件名输入时必须注意大小写，这一点非常关键。

### 1.4 常见发行版

| 发行版 | 英文全称 | 说明 |
|---|---|---|
| Red Hat Enterprise Linux | **RHEL**（Red Hat Enterprise Linux，红帽企业版） | 商业发行版，收费，有官方技术支持 |
| CentOS | **CentOS**（Community ENTerprise Operating System，社区企业操作系统） | 基于 RHEL 源码重新编译的免费版本，互联网公司用得最多（"可以白嫖"） |
| openSUSE | — | 德国系发行版 |
| Ubuntu | — | 桌面体验好，云环境也常见 |
| Debian | — | 老牌社区发行版，Ubuntu 的上游 |
| 红旗 Linux | — | 国产发行版 |

📖 **补充（重要，避免初学者踩坑）**：
- 课程演示使用的是 **CentOS 7.5**，这也是国内机房存量最大的版本之一。
- CentOS 7 已于 **2020 年 6 月 30 日停止维护**、CentOS 8 于 2021 年底停止维护，官方后续转向 CentOS Stream。现在新装系统可考虑 **Rocky Linux**、**AlmaLinux**（均为 CentOS 的社区后继者）或 RHEL。但**学习阶段用 CentOS 7 完全没问题**，网上资料最多。
- 学习时没有物理服务器，可以在 Windows 电脑上装 **VMware Workstation** 或 **VirtualBox** 虚拟机练习（虚拟机装 CentOS 7 不会遇到下文 U 盘安装的标签问题）。

### 1.5 安装方式总览

| 方式 | 适用场景 | 特点 |
|---|---|---|
| **U 盘安装** | 一台或几台服务器 | 灵活，像用 U 盘给个人电脑装 Windows 一样 |
| **PXE 无人值守批量安装** | 数据中心一次上架几十上百台 | 全自动，装机人员只需把机器开机按一下键 |

---

## 二、安装 Linux 系统

### 2.1 需要准备的三样东西（U 盘安装）

1. **一个 U 盘**：容量必须大于 4GB，建议 **8GB**（Linux 镜像常规大小超过 4GB）。
2. **Linux 镜像文件**：即 ISO 文件（**ISO** 镜像格式源于光盘的 ISO 9660 标准）。
3. **刻录软件 UltraISO（软碟通）**：把普通 U 盘"摇身一变"做成 Linux 安装盘。

### 2.2 去哪里下载镜像？

- **官方渠道**：各发行版官网，如 CentOS 官网 `www.centos.org`。
- **开源镜像站**（国内下载速度快）：在搜索引擎搜"Linux 开源镜像站"即可。常见的有：
  - 网易（163）开源镜像站、搜狐开源镜像站；
  - 📖 补充：**清华大学 TUNA 镜像站**、**阿里云开源镜像站**（mirrors.aliyun.com）、**中科大 USTC 镜像站**。
- 注意：**不是每个镜像站都有你需要的版本**。例如网易镜像站上可能没有 CentOS 7.5（1804），而搜狐有。进入镜像站的 `isos/` 目录，再进 `x86_64/`（64 位）目录，后缀为 `.iso` 的就是镜像文件。

### 2.3 镜像的几种版本（以 CentOS 7 为例）

| 版本 | 说明 |
|---|---|
| **DVD** | 常规给服务器装系统用的版本，约 4GB+。**大多数情况下选它** |
| **Everything** | 相当于 DVD 版 + 更丰富的软件包，集成的软件非常多，8GB+ |
| **LiveGNOME** | GNOME（**GNU Network Object Model Environment**，一种桌面环境）桌面体验版，不装硬盘也能直接进桌面体验 |
| **LiveKDE** | KDE（**K Desktop Environment**，另一种桌面环境）桌面体验版 |
| **Minimal** | 最小化安装，**无图形界面**，装完是纯命令行黑框 |
| **NetInstall** | 网络安装版，安装时从网上下载软件包 |

### 2.4 制作安装盘（UltraISO 步骤）

1. 建议以**管理员身份运行** UltraISO（否则可能点不了"写入"）。
2. `文件 → 打开`，选择下载好的 ISO 镜像。
3. 插入 U 盘，菜单 `启动 → 写入硬盘映像`。
4. 确认"驱动器"选的是你的 U 盘（**千万别选错盘**——刻录过程会**格式化 U 盘**，重要资料提前备份）。
5. 写入方式等选项默认不动，点 **写入** → 提示"数据将全部丢失"→ 是。
6. 等待进度条走完，日志显示"刻录成功"，关闭软件、拔出 U 盘。

### 2.5 在服务器上安装（以华为 RH2288H V2 + CentOS 7.5 为例）

**总体流程**：制作好安装盘 → 插入服务器 USB 口 → 开机从 U 盘启动 → 按安装向导配置。

1. **选择启动设备**：开机时盯紧屏幕提示，按 **F11** 进入启动菜单（Boot Manager）。**每种机型按键不一样**，认准屏幕上带 **Boot** 关键字的提示。列表里选你的 U 盘回车。
2. **CentOS 7 安装菜单**有三个选项：
   - `Install CentOS 7`：直接安装（**一般选这个**）；
   - `Test this media & install CentOS 7`：先校验镜像完整性再装（下载时网络断续可能损坏镜像；测试过程漫长，一般跳过）；
   - `Troubleshooting`：排错/修复模式。
3. **经典报错与解决（初学者必看）**：选择第一项回车后，如果界面**一直卡住不动、不停弹出超时警告**，是因为服务器识别不了 U 盘的标签（CentOS 6 或虚拟机装 CentOS 7 不会遇到这个问题）。解决方法：
   - 在倒计时结束前按 **Tab** 键（有的机型是按 **e**，看屏幕提示）编辑启动参数；
   - 把参数行中 `hd:` 开头到末尾的内容删掉，改成 `hd:/dev/sda4`（即手动指定安装文件所在的 U 盘设备）；
   - 怎么知道 U 盘是哪个设备？进入 `dracut` 报错后的命令提示符，执行 `cd /dev` 后 `ls` 查看：`sd` 开头代表 SATA/SCSI 接口硬盘，`a` 是第 1 块、`b` 是第 2 块……；`sda4` 中末尾数字是分区号。**只有一个分区的那个就是 U 盘**（安装盘通常只有一个分区，所以可能是 `sda4`、`sdb4` 等，按实际情况填）。
   - 改完回车，即可正常进入安装界面。
4. **安装向导关键配置**：
   - 语言：选"中文"（这只是**安装过程**的语言；"语言支持"才是装完后的系统语言。生产环境习惯用英文）。
   - **软件选择**：默认"最小化安装"装完没有图形界面；想用桌面就选"带 GUI 的服务器"（GNOME 或 KDE）。
   - **安装位置（分区）**：勾选目标磁盘（别选成 U 盘；做了 RAID 的磁盘组会显示为一块盘）。可选"自动分区"，但**一般建议手动分区**，至少分两个区：
     - **swap（交换分区）**：虚拟内存空间。当物理内存不够用时，系统把闲置进程暂时换出到 swap，把内存腾给真正需要的程序，用完再换回来。大小一般为**物理内存的 1.5～2 倍**（课程演示：内存 8G 配 12G swap）。
     - **根分区 `/`**：除 swap 外的空间基本都给它（课程演示分了 100G）。
     - 文件系统类型：CentOS 7 默认 **XFS**（详见第八章磁盘管理）。
   - **Kdump**：内核崩溃转储机制（**Kernel Crash Dump**，系统崩溃时把内存 dump 下来供分析），默认保持不动。
   - **网络和主机名**：也可以装完系统后再配（见第九章）。
   - 设置 **root 密码**（密码太简单要点两次"完成"才生效）；可以顺便创建一个普通用户。
5. 开始安装 → 等待软件包安装完成 → **重启**。
6. 首次重启后的初始设置：接受许可证协议、选语言/键盘/时区、创建用户，之后进入系统（桌面版进 GNOME 界面，最小化安装进命令行）。

📖 **补充：更专业的分区方案**（生产环境常见，课程未展开）：

| 挂载点 | 建议大小 | 用途 |
|---|---|---|
| `/boot` | 1GB | 内核和引导文件，单独分区防止根分区写满导致无法启动 |
| `swap` | 内存的 1～2 倍 | 交换空间 |
| `/` | 50～100GB | 根分区 |
| `/data` | 剩余全部 | 业务数据单独存放，重装系统不丢数据 |

### 2.6 PXE 批量无人值守安装

**为什么需要**：数据中心一次上架几十上百台服务器，挨个插 U 盘装系统会"吐一口老血"，所以用 **PXE（Preboot eXecution Environment，预启动执行环境）** 网络批量安装。

**角色分工**（俗称）：
- **母机**：先用 U 盘装好系统的那一台，在上面搭建 PXE 服务（**DHCP 服务器 + TFTP 服务器** + HTTP/FTP/NFS 文件服务）；
- **小机**：其他所有需要装系统的服务器（PXE 客户端），全部连到同一台交换机上。

**PXE 工作流程**（初学者可先记大框架）：

1. 小机开机以 PXE 方式启动（一般按 **F12**，多数服务器通用；如果机器本来没有系统，开机会自动尝试 PXE，连键都不用按）；
2. 小机向母机发送 **DHCP（Dynamic Host Configuration Protocol，动态主机配置协议）** 请求 → 母机检测其合法性，返回 IP 地址，同时把启动文件 `pxelinux.0` 的位置信息一并下发；
3. 小机通过 **TFTP（Trivial File Transfer Protocol，简单文件传输协议）** 向母机请求 `pxelinux.0`（先协商大小，再正式传输）；
4. 小机执行 `pxelinux.0`，再向 TFTP 请求本机的配置文件（位于 TFTP 的 `pxelinux.cfg` 目录）；
5. 小机根据配置文件，向 TFTP 请求 **Linux 内核**文件并启动内核（启动参数已在配置文件中写好）；
6. 内核起来后，通过 **NFS（Network File System，网络文件系统）** 或 **HTTP（HyperText Transfer Protocol，超文本传输协议）/FTP** 下载完整镜像文件；
7. 读取 **Kickstart 自动化安装脚本（ks.cfg）**，实现全自动安装（分区、root 密码、IP、主机名等全部预置好，无需人工干预）。

**机房现场操作**：先用 U 盘给一台装系统 → 在母机上搭好 DHCP/TFTP/HTTP 等服务 → 其余小机逐台开机按 F12 → 自动获取 IP、下载安装文件、自动分区装包 → 全部装完后接显示器确认各台都到了登录界面即可。带外管理地址（如华为 iBMC，**intelligent Baseboard Management Controller**）也可以在 PXE 安装时一并指定。

**PXE 排错思路**（小机卡住时逐项检查）：可能是①防火墙没关、②SELinux 没关、③DHCP/TFTP/HTTP 服务没启动、④配置文件写错。母机自己搭的话要一项一项排查。

📖 **补充**：母机上的服务搭建（DHCP、TFTP、HTTP、Kickstart 配置）属于进阶内容，等学完本笔记的 basics 再回头看会轻松很多。

---

## 三、服务器硬件管理

系统装好后，运维中要**随时掌握服务器硬件状态**——内存爆了不能"若无其事"。好在 Linux"一切皆文件"，硬件信息都能用命令查出来。

### 3.1 查看整机与部件信息：dmidecode

`dmidecode` 从 SMBIOS/DMI 中读取硬件信息，可以查**厂商、型号、序列号、主板、BIOS、内存插槽**等（需要 root 权限）。典型用法是配合**管道符 `|`** 和 `grep` 过滤：

```bash
dmidecode -t system        # 查看服务器整体信息（型号、序列号、UUID 等）
dmidecode -t baseboard     # 查看主板信息
dmidecode -t bios          # 查看 BIOS（Basic Input/Output System，基本输入输出系统）信息
dmidecode -t memory        # 查看内存信息（共多少插槽、每根多大、有没有空槽）
dmidecode -t slot          # 查看 PCI（Peripheral Component Interconnect，外设部件互连标准）插槽信息
dmidecode | grep "Product" # 管道 + grep 筛选出产品型号等关键行
```

> 💡 管道符 `|` 的作用：把前一个命令的输出交给后一个命令处理；`grep` 是"过滤包含关键字的那几行"。这是 Linux 极高频的组合。

### 3.2 查看 CPU 信息

CPU 的详细信息存放在文件 **`/proc/cpuinfo`** 中（`/proc` 是内存中的虚拟目录，"一切皆文件"的典型体现），可以直接 `cat /proc/cpuinfo` 查看，也可用命令：

```bash
lscpu                 # CPU 概况：型号、架构、主频、核数等（最方便）
grep "model name" /proc/cpuinfo   # CPU 型号（如 Intel Xeon E5-2620）
grep "physical id" /proc/cpuinfo | sort -u | wc -l   # 物理CPU颗数
grep "cpu cores" /proc/cpuinfo | uniq               # 每颗CPU的物理核心数
grep "processor" /proc/cpuinfo | wc -l              # 逻辑CPU数（含超线程）
```

> 💡 注意 CPU 编号从 0 开始：显示到 cpu15 就是 16 核。课程演示机器是 Intel 至强（Xeon）E5-2620，2.2GHz，16 逻辑核。

### 3.3 查看内存信息

```bash
free -h                # 内存使用情况（-h 人类可读：G/M 单位）。Mem 行看总/已用/可用，Swap 行看交换分区
dmidecode -t memory    # 内存硬件信息：插槽数量、单条容量（"No Module Installed" 表示空槽）
grep MemTotal /proc/meminfo   # 内存总量
```

### 3.4 查看硬盘信息

```bash
lsblk                  # 列出块设备：有几块盘、几个分区、挂载在哪（最直观）
fdisk -l               # 硬盘和分区的详细信息（容量、分区表）
df -hT                 # 已挂载分区的使用情况：总量/已用/可用/挂载点（-T 显示文件系统类型）
```

课程演示：`lsblk` 看到一块盘 `sda`（实际是两块物理盘做的 RAID 组，系统识别为一块）下有 sda1（swap 12G）和 sda2（根分区 100G）；`df -hT` 显示 sda2 挂载在 `/`，总 100G 已用 12G。

📖 **补充**：
- 云主机/虚拟机上很多硬件查询命令结果不全或不可用（虚拟化对硬件指令做了限制），这是正常现象。
- 实时性能监控可用 `top`（看 CPU/内存/进程占用）和 `uptime`（看负载），是硬件管理章节的自然延伸。
- 硬盘的分区、格式化、挂载等**操作**类知识在第八章磁盘管理详细展开。

---

## 四、Linux 文件管理

### 4.1 目录结构：单根树 vs Windows 盘符

- Windows：磁盘分 C 盘、D 盘、E 盘，每个盘符是一棵独立的树。
- Linux：**整个系统只有一棵树**，树根就是 **`/`（根目录，root）**，所有文件和目录都从 `/` 出发。安装时的 swap、根等分区，本质是**把某个分区"挂载"到树上的某个目录**，从结构上看仍然统一在根之下。

Linux 的目录结构遵循 **FHS（Filesystem Hierarchy Standard，文件系统层次结构标准）**。

```
/                ← 根目录（一切的起点）
├── boot         ← 内核与引导文件
├── dev          ← 设备文件
├── etc          ← 配置文件
├── home         ← 普通用户家目录
├── root         ← root 的家目录
├── tmp          ← 临时文件
├── usr          ← 系统软件资源
├── var          ← 经常变化的数据（日志等）
└── ...
```

### 4.2 重要的二级目录及用途

| 目录 | 用途 | 记忆点 |
|---|---|---|
| `/boot` | 存放 Linux 内核、引导配置文件 | 相当于 Windows 的 C 盘核心区；**文件丢了系统就启动不了** |
| `/dev` | 设备文件目录（一切皆文件的体现） | 硬盘 `/dev/sda`、U 盘等都以文件形式在这里 |
| `/etc` | **各种服务的配置文件** | 想让软件实现什么功能，就改这里对应的配置文件（运维最常打交道的目录） |
| `/home` | 普通用户的家目录 | 每建一个普通用户，这里就多一个同名目录 |
| `/root` | 超级管理员 root 的家目录 | 注意它不在 /home 下 |
| `/tmp` | 临时文件 | 练习操作的"试验田"，丢了也无所谓 |
| `/bin` | 📖 补充：基本用户命令（binary 二进制可执行文件） | ls、cp、cat 等命令本体 |
| `/sbin` | 📖 补充：系统管理命令（system binary） | root 用的管理命令 |
| `/lib` | 📖 补充：库文件（library）和内核模块 | 命令运行依赖的共享库 |
| `/usr` | 📖 补充：Unix Software Resource，系统软件资源 | 安装的软件、文档大多在这里 |
| `/var` | 📖 补充：variable，经常变化的数据 | **日志 `/var/log/messages`**、邮件 `/var/spool/mail` |
| `/proc` | 📖 补充：内存中的虚拟文件系统 | 内核与进程信息，如 `/proc/cpuinfo` |
| `/mnt` | 📖 补充：临时挂载点 | 手动挂载 U 盘、新分区常用 |
| `/opt` | 📖 补充：第三方软件安装目录 | |

### 4.3 文件命名规则（7 条）

1. 除**斜杠 `/`** 以外的所有字符都合法（`/` 代表根、代表路径分隔）；
2. 特殊字符（如空格、`$`、`&` 等）**最好不用**；
3. 避免用 `.` 点作为文件名第一个字符——**以点开头的是隐藏文件**；
4. **严格区分大小写**（`Test` ≠ `test`）；
5. 文件后缀名**没有任何实际意义**（不像 Windows 靠后缀识别类型），但为了方便人识别，习惯上还是定义 `.txt`、`.conf` 等后缀；
6. 三个特殊目录符号：**`.` 当前目录**、**`..` 上一级目录**、**`/` 根目录**；
7. 同一目录下文件和目录**不能重名**（目录本身也是文件——一切皆文件）。

### 4.4 文件类型（终端颜色区分）

| 颜色 | 类型 | `ls -l` 首字符 |
|---|---|---|
| 黑色（白色） | 普通文件 | `-` |
| 蓝色 | 目录 | `d` |
| 绿色 | 可执行文件 | `-`（带 x 权限） |
| 红色 | 压缩文件 | `-` |
| 黄色 | 设备文件 | `b`/`c`（📖 补充：块设备/字符设备） |
| 浅蓝色 | 链接文件（快捷方式） | `l` |

📖 补充：`ls -l` 输出第一个字符完整含义：`-` 普通文件、`d` 目录、`l` 软链接、`b` 块设备（硬盘）、`c` 字符设备（终端、串口）、`s` 套接字、`p` 管道文件。

### 4.5 绝对路径与相对路径（初学者必须分清）

- **绝对路径**：从根 `/` 开始写全，如 `/tmp/hubei/wuhan`。任何位置都能用。
- **相对路径**：从**当前所在目录**出发，如当前在 `/tmp`，则 `hubei/wuhan` 等价于 `/tmp/hubei/wuhan`。

### 4.6 目录操作命令

| 命令 | 全称 | 作用 |
|---|---|---|
| `ls` | list | 查看目录下的文件和目录 |
| `cd` | Change Directory | 切换目录 |
| `pwd` | Print Working Directory | 显示当前目录的绝对路径 |
| `mkdir` | Make Directory | 创建目录 |
| `rmdir` | Remove Directory | 删除**空**目录 |

常用选项与写法：

```bash
ls -a        # 查看所有内容，包括隐藏文件（点开头的）
ls -l        # 查看详细信息（等价简写：ll）
ls -ld /etc  # 查看目录本身的属性（而不是目录里面的内容）
cd /tmp      # 切换到 /tmp（绝对路径）
cd ..        # 切换到上一级目录
cd -         # 切换到"上一次所在的目录"（来回跳很方便）
cd ~         # 切换到当前用户的家目录（root 在 /root，普通用户在 /home/用户名）
mkdir hubei            # 创建目录 hubei
mkdir -p hubei/wuhan/shangpinzhicheng   # -p 递归创建：父目录不存在时一并创建
rmdir hubei           # 删除空目录；目录非空会报错
rm -rf hubei          # 删除非空目录（危险！-r 递归 -f 强制，直接整个删掉）
```

> 💡 提示符中 `~` 表示当前用户的家目录；root 登录时 `pwd` 显示 `/root`。练习建议都在 `/tmp` 里做，文件丢了无所谓。

### 4.7 文件操作命令

| 命令 | 全称 | 作用 |
|---|---|---|
| `touch` | — | 创建空文件；文件已存在则更新其时间属性（创建/修改时间） |
| `rm` | Remove | 删除文件；`-f` 强制（不提示）、`-r` 递归（删目录用） |
| `mv` | Move | 移动文件/目录，或**重命名** |
| `cp` | Copy | 复制 |
| `scp` | Secure Copy | 📖 远程复制（基于 SSH 加密传输，见第十二章） |

```bash
touch 1.txt 2.txt           # 同时创建两个空文件
rm 1.txt                    # 删除（会询问 y/n）
rm -f 2.txt                 # 强制删除，不提示
cp 3.txt 301.txt            # 复制并重命名
cp /etc/passwd .            # 把文件拷到当前目录（. 代表当前目录）
cp /var/log/messages mess111    # 拷贝的同时重命名
mv 3.ppt 3.pptx             # 重命名
mv 3.pptx /tmp              # 移动到别的目录
rm -rf *                    # 清空当前目录所有内容（危险操作，注意所在目录！）
```

📖 **补充：scp 的典型用法**（课程提到但没展开）：

```bash
scp /tmp/1.txt root@192.168.1.10:/tmp       # 把本地文件推到远程服务器
scp root@192.168.1.10:/tmp/1.txt /tmp       # 从远程服务器拉文件到本地
scp -r /tmp/hubei root@192.168.1.10:/tmp    # -r 复制整个目录
```

### 4.8 查看文件内容的 5 个命令

| 命令 | 特点 |
|---|---|
| `cat` | concatenate（连接）：把文件**全部内容**一次性打印到终端，适合小文件 |
| `more` | **一页一页**翻动查看，有进度百分比提示，看完自动退出 |
| `less` | 一页一页翻动，支持翻页、跳转、查找，**按 `q` 手动退出**（比 more 好用） |
| `head` | 查看文件**前几行**，默认前 10 行；`head -3 文件` 看前 3 行 |
| `tail` | 查看文件**后几行**，默认后 10 行；`tail -4 文件` 看后 4 行 |

📖 **补充（运维高频）**：`tail -f /var/log/messages` 可以**实时跟踪**文件新增内容（如看日志滚动）；配合 `grep 关键字 文件` 可以过滤出关心的行。例如：

```bash
tail -f /var/log/secure              # 实时看登录日志
grep "Failed" /var/log/secure        # 找出登录失败的记录
```

### 4.9 vim 编辑器

Linux 中软件的很多功能是靠**修改配置文件**实现的，改文件内容是运维常规操作，必须掌握 **vim**（**Vi IMproved**，vi 的升级版；老系统没有 vim 就直接用 vi）。

**三种模式及切换**（核心中的核心）：

```
                按 i / a / o / I / A / O
   命令模式  ────────────────────────────▶  输入模式（编辑模式）
   （默认）  ◀────────────────────────────        │
                按 ESC                        │
        │  按 : （冒号）                       │ 按 ESC
        ▼                                     │
   末行模式  ◀────────────────────────────────┘
```

- 打开文件：`vim 文件名` → 进入**命令模式**；
- 命令模式按 `i/a/o` 等进入**输入模式**（真正打字编辑），按 **ESC** 回到命令模式；
- 命令模式按 **`:`** 冒号进入**末行模式**（保存、退出、替换等），按 ESC 回命令模式。

**命令模式常用按键**（先按 ESC 确保在命令模式）：

| 按键 | 作用 |
|---|---|
| `i` | 在**光标前**插入 |
| `a` | 在**光标后**插入 |
| `o` | 在**下一行**插入新行 |
| `I`（大写 i） | 跳到**行首**插入 |
| `A`（大写） | 跳到**行尾**插入 |
| `O`（大写） | 在**上一行**插入新行 |
| `yy` | 复制光标所在行（`nyy` 复制 n 行，如 `10yy`） |
| `dd` | 删除光标所在行；**也是剪切**——后面按 `p` 粘贴回来就是剪切，不粘贴就是删除 |
| `ndd` | 删除从光标起的 n 行（如 `10dd`） |
| `p` | 粘贴 |
| `u` | **撤销**上一步操作 |
| `gg` | 跳到文件**第一行行首** |
| `G`（大写） | 跳到文件**最后一行行首** |
| 📖 `x` | 删除光标所在字符 |
| 📖 `nG` / `:n` | 跳到第 n 行 |
| 📖 `/关键字` 回车 | 查找关键字，`n` 跳到下一个匹配 |

**末行模式常用命令**（先按 `:`）：

| 命令 | 作用 |
|---|---|
| `:w` | 保存（write） |
| `:q` | 退出（quit） |
| `:q!` | **不保存强制退出**（改乱了想放弃时用） |
| `:wq` | 保存并退出（最常用） |
| `:wq!` | 强制保存并退出 |
| `:set nu` | 显示行号（number） |
| `:set nonu` | 📖 取消行号 |
| 📖 `:s/old/new/g` | 替换当前行所有 old 为 new |
| 📖 `:%s/old/new/g` | 全文替换 |

命令模式下连按两次大写 **`ZZ`** 也可以直接保存退出。

> 💡 常见坑（📖 补充）：vim 异常退出（断电、误关终端）后再打开会提示 `.swp` 交换文件，按提示恢复（`R`）或删除交换文件即可。

---

## 五、归档与压缩

运维中经常要**打包备份**日志和数据。先分清两个概念：

- **归档（打包）**：把多个文件**合并成一个**文件（不减小体积），用 `tar` 命令；
- **压缩**：用算法减小体积。`tar` 可以通过选项直接调用压缩工具，一步完成"归档+压缩"。

### 5.1 四种压缩格式对比

| 格式 | 工具 | 特点 |
|---|---|---|
| `.gz` | gzip（**GNU zip**） | 速度快，压缩率一般 |
| `.bz2` | bzip2 | 压缩率比 gzip 高，速度慢些 |
| `.xz` | xz | **压缩率最高**，速度最慢 |
| `.zip` | zip | 📖 **保留原文件**、可直接压缩目录、Windows 也通用（跨平台首选） |

> gzip / bzip2 / xz 单独使用时默认**不保留原文件**（压缩后原文件消失，解压后恢复）；zip 默认保留。

### 5.2 tar 命令（重点）

`tar`（**Tape Archive**，磁带归档）常用选项：

| 选项 | 含义 |
|---|---|
| `-c` | **创建**归档（create） |
| `-x` | **展开**归档（extract） |
| `-v` | 在终端**显示过程**（verbose） |
| `-f` | **指定归档文件名**（file，必须放选项最后，后面紧跟文件名） |
| `-z` | 调用 **gzip** 压缩/解压 |
| `-j` | 调用 **bzip2** |
| `-J`（大写） | 调用 **xz** |
| 📖 `-t` | 不解压，查看包内容列表 |
| 📖 `-C 目录` | 解压到指定目录 |

**常用组合**（记住这三组就够了）：

```bash
# 归档 + gzip 压缩（.tar.gz 最常用）
tar -zcf 20211230.tar.gz messages passwd
# 解压 .tar.gz
tar -zxvf 20211230.tar.gz

# 归档 + bzip2（.tar.bz2）
tar -jcf 20211230.tar.bz2 messages passwd
tar -jxf 20211230.tar.bz2          # 解压

# 归档 + xz（.tar.xz）
tar -Jcf 20211230.tar.xz messages passwd
tar -Jxf 20211230.tar.xz           # 解压

# 📖 解压到指定目录
tar -zxvf 20211230.tar.gz -C /tmp
```

口诀：**压 c 解 x，过程看 v，名字跟 f；gz 用小 z、bz2 用小 j、xz 用大 J**。

📖 **补充**：
- 文件名 `xxx.tar.gz` 的意思是"先用 tar 归档、再用 gzip 压缩"的结果，也常写成 `xxx.tgz`。
- zip 的用法：`zip -r bak.zip 目录/`（-r 递归压目录），解压用 `unzip bak.zip`。
- 其他快捷键：终端里 **Ctrl + L** 清屏（等于 `clear`）；**Tab 键**自动补全命令和文件名（强烈建议养成习惯，又快又不易敲错）。
- 更多选项随时用 `命令 --help` 或 `man 命令`（manual，手册）查看。

---

## 六、用户与用户组管理

### 6.1 为什么要管用户？

Linux 是**多用户、多任务的分时操作系统**：任何人想使用系统资源，都必须先向管理员申请**账号**，以该账号身份进入系统。

关键认知：
- Linux **不认识用户名**，只认识用户名对应的 **ID 号**；
- **UID**（User Identifier，用户 ID）标识用户，**GID**（Group Identifier，组 ID）标识用户组；
- 用户管理的各种命令，本质上都是在**修改系统文件**（又是"一切皆文件"）。

### 6.2 三类用户与 UID 范围

| 用户类型 | 说明 | CentOS 6 UID | CentOS 7 UID |
|---|---|---|---|
| 超级用户 root | 至高无上的管理员 | 0 | 0 |
| 程序用户（系统用户） | 给系统服务/守护进程用的账号，一般**不允许登录** | 1～499 | 1～1000 |
| 普通用户 | 日常使用的账号 | 500～60000 | 1001～60000 |

> 💡 从 root 切换到任何用户都不需要密码（root 是密码的发放者）；从普通用户切回 root 需要输 root 密码。

### 6.3 用户管理命令

| 命令 | 作用 | 常用选项 |
|---|---|---|
| `useradd` | 添加新用户 | `-c` 描述信息；`-d` 指定家目录；`-g` 指定主组；`-G` 指定附加组；`-s` 指定登录 Shell；`-u` 指定 UID |
| `userdel` | 删除用户 | `-r` 连家目录、邮件文件一起删（"不仅把人干掉，还把家拆了"） |
| `usermod` | 修改用户属性 | 选项与 useradd 相同 |
| `passwd` | 设置/修改密码 | 不跟用户名默认改 root 的；跟用户名则改对应用户 |
| `su` | Switch User（切换用户） | `su - 用户名` 连**登录环境**一起切换（推荐）；直接 `su 用户名` 只切身份不完全切环境 |
| `id 用户名` | 查看用户的 UID、GID 等信息 | 也常用来**判断用户是否存在** |
| `whoami` | 查看当前登录的用户名 | — |

```bash
whoami                    # root
id kai                    # 查 kai 是否存在（不存在会提示 no such user）
useradd kai               # 创建用户 kai（CentOS 7 第一个普通用户默认 UID 从 1001 开始）
useradd -c "boss" -u 1003 -g kai dianwei   # 创建时直接指定描述、UID、主组
userdel -r dianwei        # 删除用户并删掉其家目录和邮件文件
usermod -u 1314 kai       # 修改 kai 的 UID
passwd kai                # 给 kai 设密码（输入时不显示，"无效的密码"提示可忽略，继续输第二遍）
passwd                    # 不带参数 = 重置 root 密码
su - kai                  # 切换到 kai（连环境一起切）
su kai                    # 只切身份
exit                      # 退回原来的用户
```

### 6.4 用户组管理命令

用 `useradd` 创建新用户时，**默认会自动创建一个与用户同名的组**（主组）。也可以单独管理组：

| 命令 | 作用 |
|---|---|
| `groupadd` | 添加用户组（`-g` 指定 GID） |
| `groupdel` | 删除用户组 |
| `groupmod` | 修改组属性（如 `-g 1011` 改 GID） |
| `gpasswd` | 管理组成员：`-A` 指定组管理员；`-a` 把用户**加入**组；`-d` 把用户从组**移除** |

```bash
groupadd -g 1010 game     # 创建组 game，GID 1010
gpasswd -a dianwei game   # 把用户 dianwei 加入 game 组
gpasswd -d dianwei game   # 把 dianwei 从 game 组删除
groupdel game2            # 删除组 game2
```

### 6.5 用户与组相关的配置文件（重点理解）

一切用户操作的背后，都是改动这几个文件；每创建一个新用户，这些文件的末尾都会追加一行该用户的信息，同时 `/home` 下新增同名家目录、`/var/spool/mail` 下新增该用户的邮件文件（`userdel -r` 删的就是后两者）。

**① /etc/passwd —— 用户配置文件**（每行一个用户，7 个字段，冒号分隔）：

```
root:x:0:0:root:/root:/bin/bash
 │  │ │ │  │    │       └─ 登录 Shell
 │  │ │ │  │    └─ 家目录
 │  │ │ │  └─ 描述信息（全名/备注）
 │  │ │ └─ GID（主组 ID）
 │  │ └─ UID
 │  └─ 密码占位符（x 表示真密码在 /etc/shadow 里）
 └─ 用户名
```

登录 Shell 两种常见取值：`/bin/bash` = **可以登录**；`/sbin/nologin` = **不允许登录**（程序用户都是它）。

**② /etc/shadow —— 影子密码文件**（存放**加密后**的密码，只有 root 可读写）：

字段依次为：登录名、加密口令、最后一次修改时间、**最小时间间隔**（多少天内不能改密码）、**最大时间间隔**（多少天必须改密码）、**警告时间**（到期前几天开始警告）、不活跃时间、失效时间、保留字段。

**③ /etc/group —— 组配置文件**：组名、组密码、GID、组内用户列表（附加组成员）。

**④ /etc/gshadow** —— 组的影子密码文件：组名、加密口令、组管理员、组成员列表。

📖 **补充**：
- 新用户家目录里的初始配置文件来自模板目录 `/etc/skel/`（如 `.bashrc`），这就是为什么新用户一登录就有提示符环境。
- 日常运维中**不建议直接用 root 干活**，普通用户需要临时提权时用 `sudo 命令`（**SuperUser Do**，以管理员身份执行单条命令），需事先在 `/etc/sudoers` 中授权。

---

## 七、权限管理

### 7.1 从 `ls -l` 说起：一行输出逐段拆解

用 `ls -ld /etc` 或 `ll` 查看文件/目录详细信息，输出各段含义如下：

```
drwxr-xr-x.  3   root  root    12288  Oct 14 10:00  .
│└─┬─┘└─┬─┘   │    │      │        │            └─ 文件名
│  │   └─ 第3组：其他用户(other)的权限       │            └─ 修改时间
│  └─ 第2组：所属组(group)的权限              └─ 文件大小（字节）
└─ 第1组：所有者(user)的权限        └─ 所属组
                              └─ 硬链接次数
└─ 文件类型：d 目录 / - 普通文件
```

**9 个权限字符，3 个一组**：第 1 组是**所有者（属主）**的权限，第 2 组是**所属组（属组）**的权限，第 3 组是**其他用户**的权限。

### 7.2 三类身份

| 代号 | 身份 | 说明（手机比喻） |
|---|---|---|
| `u`（user/owner） | 所有者 | 我买的手机，我说的算 |
| `g`（group） | 所属组 | 手机给公司用，公司同事对它有一定使用权 |
| `o`（others） | 其他用户 | 路人，可能什么权限都没有 |
| `a`（all） | 所有用户 | u + g + o 的总和 |

> 💡 手机"送给翠花"后，所有者就变成了翠花——所有者是可以改的（见 chown）。

### 7.3 三种权限：r、w、x

| 权限 | 字母 | 数字 | 对**文件**的含义 | 对**目录**的含义 |
|---|---|---|---|---|
| 读 | r（read） | 4 | 查看文件**内容** | 查看目录**内的内容**（ls） |
| 写 | w（write） | 2 | **修改**文件内容 | 修改目录内的内容（新建/删除/改名里面的文件） |
| 执行 | x（eXecute） | 1 | **执行**这个文件（脚本、程序） | 能否 `cd` 进入该目录 |
| 无权限 | `-` | 0 | 占位符 | 占位符 |

**数字表示法**：把三类权限的数字相加。例如 rwx = 4+2+1 = **7**；r-x = 4+0+1 = **5**；rw- = 4+2+0 = **6**。

- 一个文件"所有人都有全部权限"= `rwxrwxrwx` = **777**；
- **文件默认权限 644**（rw-r--r--）：所有者读写，其他人只读；
- **目录默认权限 755**（rwxr-xr-x）：所有者全权，其他人能进能看不能改。

三位数各代表谁：第 1 位所有者、第 2 位所属组、第 3 位其他用户。

### 7.4 权限管理三命令

**① chmod（Change Mode，修改权限）**——最重要：

```bash
# 字母表达法：[u/g/o/a] [+/-/=] [r/w/x]
chmod u-x 1.txt        # 取消所有者的执行权限（u 减 x）
chmod a+x 1.txt        # 给所有用户加执行权限（文件会变绿色）
chmod g+w 1.txt        # 给所属组加写权限

# 数字表达法：三位数字直接指定
chmod 600 1.txt        # rw-------，仅所有者可读写
chmod 755 aaa          # 目录常用
chmod 000 aaa          # 撤掉所有权限（root 仍然可以进入，root 不受权限限制！）
```

**② chown（Change Owner，更改所有者，也可以顺带改所属组）**——只有管理员能用：

```bash
chown kai 1.txt            # 只改所有者为 kai（所属组不变）
chown kai:kai 1.txt        # 同时改所有者和所属组（冒号分隔）
chown :root 1.txt          # 只改所属组为 root（冒号前留空）
```

**③ chgrp（Change Group，只更改所属组）**：

```bash
chgrp kai 1.txt        # 把 1.txt 的所属组改为 kai 组
chgrp kai aaa          # 目录同理
```

📖 **补充**：
- **root 用户不受普通权限约束**（000 权限的目录 root 照样进），权限体系主要约束普通用户。
- 默认权限 644/755 是由 **umask** 值决定的：文件 666 - umask(022) = 644，目录 777 - 022 = 755。用 `umask` 可查看。
- 进阶：特殊权限位 SUID（4）、SGID（2）、Sticky Bit（1），如 `/usr/bin/passwd` 的 `-rwsr-xr-x`、`/tmp` 的 `drwxrwxrwt`，初学阶段了解即可。

---

## 八、磁盘管理

### 8.1 硬盘的物理位置与槽位

服务器面板上有多个硬盘槽位，**从 0 开始编号**：0 号槽位是**第一块**硬盘，1 号槽位是第二块……（Linux/硬件世界普遍从 0 开始计数，如 CPU0、sda）。系统报硬盘故障时会显示槽位号，看到"0 号槽位"要知道说的是第一块盘。

### 8.2 硬盘在 Linux 中的设备名

一切皆文件——每块硬盘在 **`/dev`** 目录下对应一个文件：

| 设备名 | 含义 |
|---|---|
| `/dev/sda` | 第 1 块硬盘（a=第 1 块，b=第 2 块，c=第 3 块……以此类推，`/dev/sdo` 是第 15 块） |
| `/dev/sda1` | 第 1 块硬盘的第 1 个**主分区** |
| `/dev/sda2` | 第 1 块硬盘的第 2 个主分区 |
| `/dev/sda3` | 第 3 个主分区（**MBR 下最多 4 个主分区**） |
| `/dev/sda4` | 第 1 块硬盘的**扩展分区**（占掉一个主分区名额） |
| `/dev/sda5` | 第 1 个**逻辑分区**（逻辑分区编号固定从 5 开始，sda6 是第 2 个……） |

> `sd` 表示接口类型为 SATA（**Serial ATA**，串行 ATA）或 SCSI（**Small Computer System Interface**，小型计算机系统接口），SAS（**Serial Attached SCSI**，串行连接 SCSI）、USB 盘也是 sd 开头。
> 📖 补充：老式 IDE（**Integrated Drive Electronics**）硬盘是 `hd` 开头（hda、hdb）；NVMe 固态盘是 `/dev/nvme0n1`。

**分区逻辑**（MBR 分区表体系）：一块盘最多 4 个主分区；想分更多区，就把其中一个主分区做成**扩展分区**，在扩展分区内再切**逻辑分区**。做了 RAID 的多块物理盘会被系统识别为一块盘。

📖 **补充**：MBR（**Master Boot Record**，主引导记录）分区表最大支持 2TB 磁盘；超过 2TB 或需要更多分区时用 GPT（**GUID Partition Table**，全局唯一标识分区表），配合 `parted` 或 `gdisk` 分区。

### 8.3 文件系统类型（格式化用的"格式"）

Windows 的 C 盘 D 盘通常是 NTFS（**New Technology File System**）；Linux 有自己的一套：

| 文件系统 | 全称/含义 | 特点 | 默认采用版本 |
|---|---|---|---|
| ext2 | second extended file system | Linux 第一个商业级文件系统，**已淘汰** | — |
| ext3 | third extended FS | ext2 + **日志**功能；支持 16TB 文件系统、单个 2TB 文件 | RHEL 5 / CentOS 5 |
| ext4 | fourth extended FS | 兼容 ext3；支持 1EB 文件系统、16TB 单文件、无限量子目录、快速 fsck（**File System Check**，文件系统检查）、日志校验、在线碎片整理 | RHEL 6 / CentOS 6 |
| **XFS** | X File System（SGI 公司开发） | **能迅速恢复磁盘文件内容**、有日志；支持 8EB-1 字节单文件、在线碎片整理、在线调整尺寸、快照、高 IO 吞吐 | **RHEL 7 / CentOS 7** |
| swap | 交换空间 | **不用于存数据**的特殊类型：物理内存不够时与它交换（虚拟内存） | — |

> 1EB（Exabyte）= 1024PB = 1024×1024TB。现在主流使用 **ext4 和 XFS**。

### 8.4 磁盘操作四步曲：分区 → 刷新 → 格式化 → 挂载

因为"一切皆文件"，分完区**必须把分区挂载（mount）到某个目录**下才能使用——访问那个目录就等于访问这个分区。

**第 1 步：fdisk 分区**

```bash
fdisk -l                # 先查看当前有几块硬盘、分区情况（也可用 lsblk / df -hT）
fdisk /dev/sdb          # 对第 2 块硬盘进行分区（进入交互界面）
```

fdisk 交互界面的常用单字母命令：

| 按键 | 含义 |
|---|---|
| `m` | 帮助（help） |
| `p` | 打印当前分区情况 |
| `n` | 新建分区（new）——先问主分区 `p` 还是扩展分区 `e`，再给分区号（默认 1～4）、起始扇区（默认 2048 即可）、大小 |
| `e` | 扩展分区 |
| `d` | 删除分区 |
| `t` | 改分区类型 ID（如 8e 为 LVM） |
| `w` | **写入并保存**（write，不按 w 一切都不会生效！） |
| `q` | **不保存退出** |

指定分区大小的两种写法：直接给扇区数（不好算），或用 `+大小`，如 `+5G`、`+500M`。主分区分满 4 个名额后，第 4 个默认选 `e` 做扩展分区（把剩余空间全部给它），之后在扩展分区内建逻辑分区（编号自动从 5 开始，不再询问 p/e）。

**第 2 步：刷新分区表**

```bash
partprobe /dev/sdb      # 让内核重新读取新分区表
```

**第 3 步：格式化（创建文件系统）**

```bash
mkfs -t xfs /dev/sdb1       # 也可以写 mkfs.xfs /dev/sdb1
mkfs.ext4 /dev/sdb2         # 格式化为 ext4
# mkfs 后连按两次 Tab 可列出系统支持的所有文件系统类型
```

**第 4 步：挂载**

```bash
mkdir /dianwei /kai                 # 建目录当挂载点（有几个分区建几个）
mount /dev/sdb1 /dianwei            # 把 sdb1 挂到 /dianwei
mount /dev/sdb2 /kai                # 把 sdb2 挂到 /kai
df -hT                              # 查看挂载结果（能分别看到 xfs 和 ext4 类型）
```

挂载后，往 `/kai` 里放文件就等于放进了 `/dev/sdb2` 分区。

**卸载**：

```bash
umount /kai      # 注意：当前正"站在" /kai 目录里时无法卸载，先 cd 出去再 umount
```

### 8.5 永久挂载：/etc/fstab

`mount` 命令挂载只是**临时**的，重启失效。要**开机自动挂载**，需写入 **`/etc/fstab`（File System Table，文件系统表）**，每行 6 个字段：

```
/dev/sdb1   /dianwei   xfs     defaults    0 0
/dev/sdb2   /kai       ext4    defaults    0 0
│            │          │       │          │ │
│            │          │       │          │ └─ fsck 检查顺序（0 不检查）
│            │          │       │          └─ 是否备份（0 不备份）
│            │          │       └─ 挂载选项（defaults 默认即可）
│            │          └─ 文件系统类型（必须写对！）
│            └─ 挂载点目录（目录必须已存在）
└─ 设备（分区）
```

```bash
mount -a     # 重新读取 /etc/fstab 并挂载（用于测试刚写的配置；开机时系统也会自动读取它）
```

> ⚠️ **fstab 千万不能写错**（设备名、挂载点、类型任何一个错误），否则**开不了机**。生产环境推荐用分区的 UUID（**Universally Unique Identifier**，通用唯一标识符，`blkid` 命令可查）代替 `/dev/sdb1` 这种设备名，避免盘符漂移问题。

### 8.6 磁盘查看命令小结

```bash
df -hT       # 已挂载分区的容量使用情况（最常用）
fdisk -l     # 硬盘和分区详细信息
lsblk        # 块设备一览（树形，直观）
```

> ⚠️ **数据无价，谨慎操作**——分区、格式化、删除都是破坏性操作，执行前先确认目标设备没错。

---

## 九、网络管理

### 9.1 服务器网卡与基础网络参数

服务器网卡一般有**光口**（插光纤、带宽大）和**电口**（RJ45）两种接口。和 PC 一样，要访问网络必须配置四样东西：

| 参数 | 含义 |
|---|---|
| **IP 地址** | Internet Protocol 地址，主机的网络门牌号 |
| **子网掩码**（netmask） | 划定 IP 中哪些位是网络位，如 255.255.255.0（/24） |
| **网关**（gateway） | 跨网段通信的出口（如 192.168.1.1） |
| **DNS** | Domain Name System，域名系统：把 `baidu.com` 解析成 IP |

### 9.2 网卡配置文件（永久生效的方法）

网卡配置文件统一放在 **`/etc/sysconfig/network-scripts/`** 目录下，文件名形如 `ifcfg-eth0`（CentOS 6 惯例）或 `ifcfg-ens33`、`ifcfg-eno1`（CentOS 7 起的一致性命名）。`eth0` 是第 1 块网卡，`eth1` 是第 2 块……`lo` 是**回环网卡**（loopback，127.0.0.1，本机自环测试用）。

```bash
vim /etc/sysconfig/network-scripts/ifcfg-eth0
```

**DHCP 自动获取（最简改法）**：把最后一行 `ONBOOT=no` 改成 `yes`（开机启动网卡），保存退出，重启网卡即可。

**静态 IP 配置（服务器标准做法）**：

```ini
TYPE=Ethernet                # 网卡类型：以太网
BOOTPROTO=static             # 由 dhcp 改为 static（静态）；DHCP=Dynamic Host Configuration Protocol 动态获取
NAME=eth0                    # 网卡名称
UUID=xxxx-xxxx               # 通用唯一标识符（不用动）
ONBOOT=yes                   # 开机是否启动网卡服务：yes
IPADDR=192.168.10.11         # IP 地址
NETMASK=255.255.255.0        # 子网掩码
GATEWAY=192.168.1.1          # 网关
DNS1=114.114.114.114         # 首选 DNS
DNS2=8.8.8.8                 # 备用 DNS（可选）
```

> 字段名必须**大写**；改完保存退出后必须**重启网卡**才生效。

### 9.3 临时配置与查看

```bash
# 临时配置（重启失效）
ifconfig eth1 192.168.10.10 netmask 255.255.255.0

# 查看
ifconfig                    # 查看所有网卡 IP（interface configuration）
ip a                        # ip addr，新命令，效果相同
```

### 9.4 域名解析相关文件

| 文件 | 作用 |
|---|---|
| `/etc/resolv.conf` | DNS 服务器配置文件。网卡配置文件里写的 DNS1 会同步显示在这里；也可以直接改这个文件 |
| `/etc/hosts` | **本地域名解析**文件，记录"主机名 ↔ IP"对应关系。服务器解析域名时**先查 hosts，再查 DNS**。例如把远程服务器的主机名和 IP 写进本地 hosts，就可以直接用主机名 SSH 登录 |

### 9.5 网卡服务管理

```bash
ifconfig eth0 down          # 关闭第一块网卡
ifconfig eth0 up            # 激活第一块网卡

# CentOS 7 (systemctl 管理服务)：
systemctl restart network   # 重启所有网卡（改完配置文件后必做）
systemctl stop network      # 关闭所有网卡（IP 会消失，只剩 MAC 地址）
systemctl start network     # 启动所有网卡
systemctl enable network    # 设置下次开机自启网卡服务

# RHEL/CentOS 5、6 的老命令（7 里也兼容）：
service network restart
```

📖 **补充**：CentOS 8 起改为 NetworkManager 管理，用 `nmcli connection reload` + `nmcli connection up 网卡名` 或 `systemctl restart NetworkManager` 重启网络。

### 9.6 网络测试命令

```bash
# ping：检测网络连通性（Packet Internet Groper），可以 ping IP 也可以 ping 域名
ping 192.168.3.1            # ping 网关
ping baidu.com              # 能通说明 DNS 正常且能出外网
# ⚠️ Linux 下 ping 不会自动结束，按 Ctrl + C 终止（Windows 默认 4 次自动停）

# netstat：查看端口监听情况（Network Statistics）
netstat -nultp              # 显示所有 TCP/UDP 处于 LISTEN（监听）状态的连接
#   -n 以数字显示地址端口  -u UDP  -t TCP  -l 只看监听  -p 显示进程
```

> 💡 服务器提供什么服务就要开对应端口，客户端才能访问。`netstat -nultp` 就是检查"服务到底开了没有"的利器。
> 📖 补充：新系统推荐用 `ss -nultp`（**Socket Statistics**，netstat 的现代替代品，速度更快）；测试某个远程端口通不通可用 `telnet IP 端口`。

---

## 十、防火墙与 SELinux

### 10.1 什么是防火墙？

公网环境比企业内网恶劣得多（服务器被攻击是常事），需要在公网与内网之间设置**保护屏障**，阻挡不明流量——这就是**防火墙（Firewall）**，好比家里的防盗门。

- 有**软件防火墙**和**硬件防火墙**之分，但主要功能相同：**依据策略对穿越防火墙的流量进行过滤**；
- 策略可以基于流量的**源地址、目的地址、端口号、协议、应用**等信息定制；
- 工作方式：用预先制定的策略规则监控出入流量——**匹配上规则就执行相应处理，匹配不上就丢弃**，从而保证只有合法流量在内外网之间流动；
- 著名的例子：国家级的"长城防火墙"（GFW，Great Firewall）就是为什么你访问不了 Google、Facebook 的原因。

### 10.2 Linux 中的防火墙工具体系（重点理解）

| 工具 | 默认采用版本 | 本质 |
|---|---|---|
| **iptables** | CentOS 5 / 6 | 防火墙**策略管理工具**（不是防火墙本身），把配置好的策略交给内核的 **netfilter**（网络过滤器）处理 |
| **firewalld**（**firewall daemon**，防火墙守护进程） | CentOS 7 / 8 | 同样只是策略管理工具，把策略交给内核的 **nftables** 包过滤框架处理 |

> 💡 核心认知：**iptables 和 firewalld 都不是真正的防火墙**，都只是"防火墙的管理工具/服务"——用户空间配置规则 → 交给内核空间的包过滤器（netfilter/nftables）执行流量处理。当前 Linux 上还有多种管理工具并存（iptables、firewalld、ebtables 等），**配置其中一个就够，其他的关闭掉**。

### 10.3 iptables 工作原理（报文之旅）

客户端访问服务器上的服务时，报文（packet）到达服务器网卡后进入**内核**（TCP/IP 协议栈属于内核），像过"关卡"一样经过各条链：

```
                       ┌──────────── 内核空间 ────────────┐
 报文进入 ─▶ PREROUTING ─┬─▶ INPUT ─▶ [本机服务] ─▶ OUTPUT ─▶ POSTROUTING ─▶ 回给客户端
   （路由前）  │         │（入站）      （用户空间）  （出站）    （路由后）
              │ 目标不是本机
              └─▶ FORWARD ─▶ POSTROUTING ─▶ 转发给其他主机
                 （转发）
```

- 目标是本机：`PREROUTING`（路由前）→ `INPUT`（入站）→ 用户空间的 服务 → `OUTPUT`（出站）→ `POSTROUTING`（路由后）→ 返回客户端；
- 目标不是本机（服务器做路由转发）：`PREROUTING` → `FORWARD`（转发）→ `POSTROUTING` → 转给其他主机。

这些"关卡"在 iptables 里称为**链（chain）**，每条链上挂着**多条规则**；报文经过每条链时，要把链上的规则**从头到尾匹配一遍**。规则 = 匹配条件（源/目的地址、传输协议、服务类型等）+ 动作。

**三种动作**：

| 动作 | 含义 | 📖 补充区别 |
|---|---|---|
| **ACCEPT** | 放行 | — |
| **REJECT** | 拒绝 | 会给客户端回应"拒绝"消息 |
| **DROP** | 丢弃 | 直接扔掉，**不给任何回应**（更隐蔽） |

📖 **补充**：完整的 iptables 还有"四表"（filter 过滤表、nat 地址转换表、mangle 修改表、raw 表）的概念，五链四表的详细配置属于进阶课程内容，这里先建立"报文过链、逐条匹配、动作处理"的模型即可。CentOS 7 下常用操作：

```bash
systemctl stop firewalld        # 停止防火墙（学习环境常用）
systemctl disable firewalld     # 开机不自启
firewall-cmd --state            # 查看防火墙状态
# 永久放行某端口（--permanent 后要 reload）：
firewall-cmd --permanent --add-port=80/tcp && firewall-cmd --reload
```

### 10.4 SELinux

**SELinux（Security-Enhanced Linux，安全增强型 Linux）**：一个采用了安全框架的系统模块，定义了每个进程对系统资源、应用和文件的访问权限，用安全策略**强制执行**策略所允许的访问。

**三种工作模式**：

| 模式 | 含义 | 特点 |
|---|---|---|
| `enforcing` | **强制模式** | 严格按策略执行，动不动就报错——运维中一般很少用 |
| `permissive` | **宽容（警告）模式** | 策略生效但只警告不拦截，不严格 |
| `disabled` | **关闭** | 完全不启用 SELinux |

**查看与修改**：

```bash
getenforce                        # 查看当前模式（Enforcing/Permissive/Disabled）
setenforce 0                      # 临时切换为宽容模式
setenforce 1                      # 临时切换为强制模式
```

永久修改：编辑 **`/etc/selinux/config`**，把 `SELINUX=` 参数改为对应模式（如 `SELINUX=permissive`），保存退出即可（重启后生效）。**一般机房习惯配成宽容模式**。

> 💡 经验：很多"服务明明起来了、端口开了、就是访问不通"的诡异问题，最后查出来是**防火墙没关或 SELinux 在强制模式**——排错时记得先想到它们（PXE 装机排错也是这两条）。

---

## 十一、root 管理员密码重置

数据中心常有旧服务器**忘记 root 密码**的情况，重置 root 密码是运维工程师的常规操作。

### 11.1 前置知识：Linux 的 7 种运行级别（Runlevel）

| 级别 | 含义 | 说明 |
|---|---|---|
| 0 | 关机 | `init 0` 即关机命令 |
| **1** | **单用户模式** | **无网络连接、不运行守护进程、不允许非 root 登录**——重置密码就在这个级别（类似 Windows 的安全模式） |
| 2 | 多用户模式 | 无网络连接、不运行守护进程 |
| **3** | **多用户字符界面** | 服务器最小化安装后默认进入的级别（纯命令行） |
| 4 | 保留级别 | 没有意义 |
| **5** | **多用户图形界面** | 装了桌面（GNOME）的服务器启动后进入的级别 |
| 6 | 重启 | `init 6` 即重启命令 |

级别之间可互相切换：图形界面终端里执行 `init 3` 进入纯字符界面，`init 5` 回图形，`init 0` 关机，`init 6` 重启。

📖 补充：CentOS 7 改用 systemd 管理，运行级别对应"target"：`multi-user.target` ≈ 级别 3，`graphical.target` ≈ 级别 5，可用 `systemctl get-default` / `systemctl set-default` 查看/设置。

### 11.2 CentOS 7 重置 root 密码的完整步骤

服务器开机进不了系统时，**进入单用户模式**改密码：

1. **重启服务器**，出现 **GRUB（GRand Unified Bootloader，大一统引导加载器）** 内核选择界面时，倒计时结束前按**任意键**停留（否则会自动进入默认系统）；
2. 按 **`e`** 键进入启动参数编辑模式；
3. 找到以 **`linux16`** 开头的那一行，把行中的 `rhgb quiet` 改成 **`rd.break`**；
   - 📖 `rhgb`（Red Hat Graphical Boot，图形化启动画面）和 `quiet`（安静模式，隐藏启动信息）本来是为了让开机画面干净，现在要去掉它们并打断启动；
4. 按 **Ctrl + X** 启动，进入**单用户（紧急救援）模式**；
5. 以读写方式重新挂载系统：

```bash
mount -o remount,rw /sysroot     # 把 /sysroot 重新挂载为读写
chroot /sysroot                  # 切换到真正的系统环境（change root）
```

6. 修改密码：

```bash
passwd          # 或 passwd root；输入两遍新密码（如 123123）
```

7. 如果原系统 **SELinux 是开启的**，还必须创建隐藏文件（否则重启后密码不生效）：

```bash
touch /.autorelabel    # 让系统下次重启时自动重新打 SELinux 标签
```

8. 连续两次 `exit` 退出（第一次退出 chroot，第二次退出救援模式），系统自动重启；
9. 用新密码登录 root 即可。

> ⚠️ `/.autorelabel` 文件名千万不能写错。CentOS 6 进入单用户的方式与 7 不同（在 GRUB 界面按 a 或 e 在行尾加 `1` 或 `single`），需要时再查资料。
> 💡 安全视角（📖 补充）：能物理接触服务器的人就能重置 root 密码——所以机房物理安全和 GRUB 加密（设置 GRUB 密码）也是安全课题。

---

## 十二、SSH 远程登录

### 12.1 为什么需要 SSH？

服务器放在机房，虽然可以通过**带外管理**（远程管理卡，如 iBMC/KVM over IP）在浏览器里拉取服务器画面来操作，但非常麻烦。运维的日常是**直接远程连进服务器的命令行**——这就是 **SSH（Secure Shell，安全外壳协议）** 的舞台：通过服务器的 IP 地址远程登录 Linux 服务器，且通信全程加密。**公司里的服务器基本都是通过 SSH 远程管理的。**

### 12.2 SSH 要点

| 项目 | 内容 |
|---|---|
| 协议/端口 | SSH 协议，默认 **TCP 22 号端口** |
| 认证方式 | ① 用户名 + 密码；② **密钥对免密登录** |
| 服务端要求 | 服务器已配置 IP、**sshd 服务（SSH Daemon，SSH 守护进程）已开启**（系统默认安装并开启）、防火墙放行 22 端口 |
| 客户端软件 | Windows：**SecureCRT**、**Xshell**；macOS/Linux：直接用终端 `ssh` 命令 |

### 12.3 密码登录

**前提**：客户端与服务器网络互通——先 `ping 服务器IP` 测试。

```bash
# macOS / Linux 终端：
ssh root@192.168.3.108        # ssh 用户名@服务器IP
# 首次连接会问 yes/no（记录主机指纹），然后输入密码即可登录
```

- Xshell/SecureCRT 中：新建会话 → 协议选 SSH → 主机填服务器 IP → 端口 22 → 确定后输入用户名（root）和密码登录；可以勾选"记住用户名/密码"方便下次直连。
- 登录后执行的 `ifconfig` 等命令，跑在远程服务器上。

### 12.4 密钥免密登录（推荐）

原理：**非对称加密**。客户端生成一对密钥——**私钥**留在客户端、**公钥**上传到服务器；登录时服务器用公钥验证客户端持有的私钥，通过即免密。

**密钥算法**：RSA（**Rivest–Shamir–Adleman**，三位发明者姓氏命名）或 DSA（**Digital Signature Algorithm**，数字签名算法）；密钥长度 1024 位（快、安全性略低）或 2048 位（慢些、更安全）。

**操作流程**：

1. 客户端生成密钥对：
   - SecureCRT：工具栏 → 创建公钥 → 选类型/长度 → 保存到本用户家目录的 `.ssh` 隐藏目录下（生成**私钥**和带 `.pub`（public，公开）后缀的**公钥**）；
   - Linux/macOS 终端：`ssh-keygen` 一路回车全默认即可，同样生成在 `~/.ssh/` 下（私钥 `id_rsa`、公钥 `id_rsa.pub`）。
2. 把**公钥**上传到服务器并追加进授权文件：
   - 最简单（Linux/macOS）：`ssh-copy-id -i ~/.ssh/id_rsa.pub root@192.168.3.108`——上传并**自动**把公钥写入服务器的 `~/.ssh/authorized_keys`（认证密钥文件）；
   - Windows：先用 Xftp 之类的工具把公钥文件上传到服务器（如 `/tmp`），再在服务器上手动追加：`cat id_rsa.pub >> /root/.ssh/authorized_keys`。
3. **权限要求**：密钥相关文件权限必须是 **600**（默认即是，但建议检查确认），否则无法登录。
4. 客户端登录软件（如 SecureCRT）会话属性里选择"公钥认证"、指定**私钥**文件，连接时输入用户名即可，不再需要密码。

> 💡 口诀：**公钥上服务器，私钥留客户端**——谁拿私钥谁能登。

📖 **补充：sshd 服务端常用管理**：

```bash
systemctl status sshd          # 查看 SSH 服务状态
systemctl restart sshd         # 重启服务
vim /etc/ssh/sshd_config       # 服务端主配置文件：
#   Port 22                    改端口
#   PermitRootLogin no         禁止 root 直接远程登录（安全加固）
#   PasswordAuthentication no  关闭密码登录，仅留密钥登录（更安全）
```

---

## 附录 A：关键词中英文对照总表

### A.1 系统与协议类

| 缩写/关键词 | 英文全称 | 中文含义 |
|---|---|---|
| OS | Operating System | 操作系统 |
| IDC | Internet Data Center | 互联网数据中心 |
| GPL | GNU General Public License | GNU 通用公共许可证 |
| GNU | GNU's Not Unix（递归缩写） | 自由软件计划 |
| POSIX | Portable Operating System Interface | 可移植操作系统接口 |
| RHEL | Red Hat Enterprise Linux | 红帽企业版 Linux |
| CentOS | Community ENTerprise Operating System | 社区企业操作系统 |
| RAID | Redundant Array of Independent Disks | 独立磁盘冗余阵列 |
| PXE | Preboot eXecution Environment | 预启动执行环境 |
| DHCP | Dynamic Host Configuration Protocol | 动态主机配置协议 |
| TFTP | Trivial File Transfer Protocol | 简单文件传输协议 |
| FTP | File Transfer Protocol | 文件传输协议 |
| NFS | Network File System | 网络文件系统 |
| HTTP | HyperText Transfer Protocol | 超文本传输协议 |
| TCP | Transmission Control Protocol | 传输控制协议 |
| UDP | User Datagram Protocol | 用户数据报协议 |
| IP | Internet Protocol | 互联网协议 |
| DNS | Domain Name System | 域名系统 |
| MAC | Media Access Control | 介质访问控制（地址） |
| SSH | Secure Shell | 安全外壳协议 |
| sshd | SSH daemon | SSH 服务守护进程 |
| RSA | Rivest–Shamir–Adleman | 非对称加密算法 |
| DSA | Digital Signature Algorithm | 数字签名算法 |
| KVM | Keyboard, Video, Mouse | 键盘/显示器/鼠标（带外管理/虚拟化） |

### A.2 硬件与分区类

| 缩写/关键词 | 英文全称 | 中文含义 |
|---|---|---|
| CPU | Central Processing Unit | 中央处理器 |
| BIOS | Basic Input/Output System | 基本输入输出系统 |
| UUID | Universally Unique Identifier | 通用唯一标识符 |
| PCI | Peripheral Component Interconnect | 外设部件互连标准 |
| USB | Universal Serial Bus | 通用串行总线 |
| SCSI | Small Computer System Interface | 小型计算机系统接口 |
| SAS | Serial Attached SCSI | 串行连接 SCSI |
| SATA | Serial Advanced Technology Attachment | 串行高级技术附件 |
| IDE | Integrated Drive Electronics | 集成驱动器电子（老式并口硬盘） |
| SSD | Solid State Drive | 固态硬盘 |
| MBR | Master Boot Record | 主引导记录（分区表） |
| GPT | GUID Partition Table | 全局唯一标识分区表 |
| GUID | Globally Unique Identifier | 全局唯一标识符 |
| iBMC | intelligent Baseboard Management Controller | 华为智能主板管理控制器（带外管理） |

### A.3 文件系统与软件类

| 缩写/关键词 | 英文全称 | 中文含义 |
|---|---|---|
| FHS | Filesystem Hierarchy Standard | 文件系统层次结构标准 |
| ISO | 源自 ISO 9660 光盘标准（International Organization for Standardization） | 光盘/镜像文件格式 |
| DVD | Digital Versatile Disc | 数字通用光盘 |
| ext2/3/4 | the 2nd/3rd/4th extended file system | 第 2/3/4 代扩展文件系统 |
| XFS | X File System（SGI 开发） | 高性能日志文件系统 |
| NTFS | New Technology File System | Windows 用的文件系统 |
| fsck | File System Check | 文件系统检查 |
| GNOME | GNU Network Object Model Environment | GNU 桌面环境 |
| KDE | K Desktop Environment | K 桌面环境 |
| vim | Vi IMproved | vi 编辑器增强版 |
| GRUB | GRand Unified Bootloader | 大一统引导加载程序 |
| Kdump | Kernel Crash Dump | 内核崩溃转储机制 |

### A.4 命令类

| 命令 | 英文全称 | 作用 |
|---|---|---|
| ls | list | 列出目录内容 |
| cd | Change Directory | 切换目录 |
| pwd | Print Working Directory | 显示当前路径 |
| mkdir | Make Directory | 创建目录 |
| rmdir | Remove Directory | 删除空目录 |
| rm | Remove | 删除 |
| cp | Copy | 复制 |
| mv | Move | 移动/重命名 |
| scp | Secure Copy | 安全复制（远程） |
| cat | concatenate | 串联/显示文件内容 |
| grep | Global Regular Expression Print | 按正则过滤文本 |
| tar | Tape Archive | 磁带归档（打包） |
| useradd/userdel/usermod | user add/delete/modify | 用户 增/删/改 |
| passwd | password | 密码 |
| su | Switch User（Substitute User） | 切换用户 |
| sudo | SuperUser Do | 以管理员身份执行 |
| id | Identifier | 查看用户 ID 信息 |
| whoami | Who am I | 当前用户名 |
| groupadd/groupdel/groupmod | group add/delete/modify | 组 增/删/改 |
| gpasswd | group password | 组成员管理 |
| chmod | Change Mode | 改权限 |
| chown | Change Owner | 改所有者 |
| chgrp | Change Group | 改所属组 |
| fdisk | fixed disk | 磁盘分区工具 |
| mkfs | Make File System | 格式化 |
| partprobe | partition probe | 重新探测分区表 |
| df | Disk Free | 查看分区使用情况 |
| du | Disk Usage | 查看目录/文件占用 |
| lsblk | List Block devices | 列出块设备 |
| mount / umount | mount / unmount | 挂载 / 卸载 |
| fstab | File System Table | 开机挂载配置文件 |
| ifconfig | interface configuration | 网卡配置/查看 |
| netstat | Network Statistics | 网络连接/端口统计 |
| ss | Socket Statistics | 套接字统计（netstat 替代） |
| ping | Packet Internet Groper | 连通性测试 |
| dmidecode | DMI decode（Desktop Management Interface） | 硬件信息解码查询 |
| init | initialization | 初始化（切换运行级别） |
| chroot | change root | 切换根目录环境 |
| hostnamectl | hostname control | 主机名管理 |

### A.5 安全与服务类

| 缩写/关键词 | 英文全称 | 中文含义 |
|---|---|---|
| SELinux | Security-Enhanced Linux | 安全增强型 Linux |
| enforcing / permissive / disabled | 强制 / 宽容 / 关闭 | SELinux 三种模式 |
| iptables | IP Tables | 防火墙策略管理工具（CentOS 5/6） |
| firewalld | Firewall Daemon | 防火墙守护进程（CentOS 7/8） |
| netfilter | — | 内核网络过滤器（真正的过滤框架） |
| nftables | — | 新一代内核包过滤框架 |
| ebtables | Ethernet Bridge Tables | 以太网桥防火墙工具 |
| ACCEPT / REJECT / DROP | 接受 / 拒绝 / 丢弃 | 防火墙三种动作 |
| runlevel | 运行级别 | 系统运行模式（0-6） |
| systemd | System Daemon | 系统与服务管理器（CentOS 7+） |
| authorized_keys | 授权密钥文件 | 存放公钥实现免密登录 |

---

## 附录 B：常用命令速查表

```bash
# ===== 硬件 =====
dmidecode -t system/bios/memory   # 整机/BIOS/内存硬件信息
lscpu | grep "model name"         # CPU 信息
free -h                           # 内存使用
lsblk / fdisk -l / df -hT         # 硬盘/分区/挂载情况

# ===== 文件 =====
ls -a / ls -l(ll) / ls -ld        # 查看（含隐藏/详细/目录本身）
cd /tmp | cd .. | cd - | cd ~     # 切目录
pwd                               # 当前路径
mkdir -p a/b/c                    # 递归建目录
touch / cp / mv / rm -rf          # 建/拷/移(改名)/强制删
cat / more / less / head -n / tail -n / tail -f   # 看内容/实时日志
grep "关键字" 文件                 # 过滤
vim 文件                           # 编辑（i 进编辑，ESC，:wq 保存退出）

# ===== 归档压缩 =====
tar -zcf x.tar.gz 文件...          # 打包+gzip 压缩
tar -zxvf x.tar.gz                 # 解压
tar -jcf / -Jcf                    # bzip2 / xz 同理
zip -r x.zip 目录 / unzip x.zip    # zip 格式

# ===== 用户与权限 =====
useradd -u -g -G -s 用户名         # 建用户
userdel -r 用户名                  # 删用户（含家目录）
passwd 用户名                      # 设密码
su - 用户名                        # 切换用户
id / whoami                        # 查用户
groupadd -g / gpasswd -a/-d        # 组管理
chmod 755 文件 | chmod u+x 文件    # 改权限
chown 用户:组 文件                  # 改属主属组
chgrp 组 文件                      # 改属组

# ===== 磁盘 =====
fdisk /dev/sdb                    # 分区（n 新建 p 打印 w 保存 q 退出）
partprobe /dev/sdb                # 刷新分区表
mkfs.xfs /dev/sdb1                # 格式化
mount /dev/sdb1 /mnt/xxx          # 挂载
umount /mnt/xxx                   # 卸载（先 cd 出该目录）
vim /etc/fstab → mount -a         # 永久挂载

# ===== 网络 =====
vim /etc/sysconfig/network-scripts/ifcfg-eth0   # 网卡配置
ifconfig / ip a                   # 查看 IP
systemctl restart network         # 重启网卡
cat /etc/resolv.conf / vim /etc/hosts            # DNS / 本地解析
ping IP 或域名（Ctrl+C 停）        # 连通性测试
netstat -nultp / ss -nultp        # 端口监听

# ===== 安全 =====
systemctl stop firewalld          # 停防火墙
getenforce / setenforce 0         # SELinux 查看/临时关闭
vim /etc/selinux/config           # SELinux 永久配置

# ===== 远程 =====
ssh root@192.168.3.108            # 远程登录
ssh-keygen                        # 生成密钥对
ssh-copy-id -i ~/.ssh/id_rsa.pub root@IP   # 上传公钥免密
scp 本地文件 root@IP:/路径         # 远程拷贝

# ===== 开关机 =====
init 0 / poweroff                 # 关机
init 6 / reboot                   # 重启
```

---

## 附录 C：学习路线建议

1. **先动手装系统**：用 VMware/VirtualBox 装一个 CentOS 7 虚拟机（最小化 + 带桌面各装一次，体会软件选择的区别）。
2. **每天练命令**：文件管理 → vim → 用户/权限 → 磁盘 → 网络，按本笔记章节顺序，在 `/tmp` 里反复练。
3. **打通远程**：配置好 IP，从自己电脑用 Xshell/SecureCRT SSH 上去操作，习惯"黑窗口"。
4. **敢于排错**：遇到"不通/起不来"，按顺序查——网络（ping/netstat）→ 防火墙（firewalld）→ SELinux → 服务状态（systemctl）→ 配置文件（/etc 下对应文件）。
5. **进阶方向**：服务搭建（DHCP/TFTP/HTTP/Kickstart，PXE 母机实战）、iptables 四表五链、Shell 脚本、RAID/LVM、云原生（学完本笔记的基础再学会顺畅很多）。

> 一句话总结本课程：**装好系统 → 认识"一切皆文件" → 会管文件/用户/权限/磁盘/网络 → 关掉拦路的防火墙和 SELinux → 用 SSH 远程随心所欲地"盘"服务器。**

---

*笔记完 · 基于《IT 运维师》课程第 63～78 讲字幕整理，错误之处欢迎指正*
