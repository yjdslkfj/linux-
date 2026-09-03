# CCNP 学习笔记（WOLF-LAB 课堂笔记 · 整理版 v2）

> **来源**：WOLF-LAB CCNP 课堂笔记（Day 1 ~ 57），OCR 识别文本经整理排版而成。
> **整理说明**：保留全部原始知识点内容，仅优化排版结构、修复 OCR 错误、统一命令格式。

## 📑 目录

- [一、EIGRP 专题](#一eigrp-专题)
  - [Day 1：EIGRP专题-CCNP第一课 NA路由知识回顾](#day-1：eigrp专题-ccnp第一课-na路由知识回顾)
  - [Day 2：EIGRP的邻居表 · 数据库表 · EIGRP数据包类型 · EIGRP建立邻居的过程](#day-2：eigrp的邻居表-·-数据库表-·-eigrp数据包类型-·-eigrp建立邻居的过程)
  - [Day 3：影响EIGRP建立邻居的条件,EIGRP的Metric计算方式,FD,AD](#day-3：影响eigrp建立邻居的条件eigrp的metric计算方式fdad)
  - [Day 4：EIGRP的DUAL算法参数 修改Metric的方式](#day-4：eigrp的dual算法参数-修改metric的方式)
  - [Day 5：EIGRP的汇总,EIGRP注入默认路由的方式](#day-5：eigrp的汇总eigrp注入默认路由的方式)
  - [Day 6：EIGRP的等价负载分担和非等价负载分担,负载分担的转发方式,EIGRP的路由条目过滤](#day-6：eigrp的等价负载分担和非等价负载分担负载分担的转发方式eigrp的路由条目过滤)
  - [Day 7：EIGRP的查询机制,Query,SIA-Query](#day-7：eigrp的查询机制querysia-query)
  - [Day 8：限制EIGRP的查询范围](#day-8：限制eigrp的查询范围)
  - [Day 9-11：EIGRP综合实验补充知识](#day-9-11：eigrp综合实验补充知识)
- [二、OSPF 专题](#二ospf-专题)
  - [Day 12：OSPF引入,OSPF运行方式,分区域设计,选举DR和BDR,Router-ID](#day-12：ospf引入ospf运行方式分区域设计选举dr和bdrrouter-id)
  - [Day 13：OSPF建邻居的过程,OSPF的DR&BDR选举方式,影响OSPF建立邻居的条件(上)](#day-13：ospf建邻居的过程ospf的drbdr选举方式影响ospf建立邻居的条件上)
  - [Day 14：OSPF建立邻居的条件,OSPF的网络类型](#day-14：ospf建立邻居的条件ospf的网络类型)
  - [Day 15-16：OSPF的LSA格式,LSA的比较,LSA的类型,LSA的作用详解](#day-15-16：ospf的lsa格式lsa的比较lsa的类型lsa的作用详解)
  - [Day 17：OSPF的汇总,OSPF LSA过滤](#day-17：ospf的汇总ospf-lsa过滤)
  - [Day 18-19：OSPF通告默认路由的方式,OSPF选路(上)(下),OSPF特殊区域](#day-18-19：ospf通告默认路由的方式ospf选路上下ospf特殊区域)
  - [Day 20：OSPF的FA地址规则,OSPF的ON路由选路方式](#day-20：ospf的fa地址规则ospf的on路由选路方式)
  - [Day 21-22：OSPF的FA地址规则,OSPF的ON路由选路方式](#day-21-22：ospf的fa地址规则ospf的on路由选路方式)
- [三、BGP 专题](#三bgp-专题)
  - [Day 23-24：BGP引入,BGP建立邻居的配置方式,BGP建立邻居的过程,包类型,BGP Router-ID](#day-23-24：bgp引入bgp建立邻居的配置方式bgp建立邻居的过程包类型bgp-router-id)
  - [Day 25：BGP发起TCP连接的顺序 · 路由宣告 · BGP防环机制 · 最优路由的行为 · 成为最优的条件](#day-25：bgp发起tcp连接的顺序-·-路由宣告-·-bgp防环机制-·-最优路由的行为-·-成为最优的条件)
  - [Day 26：联邦,路由反射器,BGP清理进程的方式](#day-26：联邦路由反射器bgp清理进程的方式)
  - [Day 27：BGP路由条目属性的分类,团体属性,Backdoor](#day-27：bgp路由条目属性的分类团体属性backdoor)
  - [Day 28-29：BGP的路由聚合,BGP的AS-Path属性,Local-Preference](#day-28-29：bgp的路由聚合bgp的as-path属性local-preference)
  - [Day 30：BGP的十三条选路原则(上)](#day-30：bgp的十三条选路原则上)
  - [Day 30-31：BGP的十三条选路原则](#day-30-31：bgp的十三条选路原则)
  - [Day 31-32：BGP综合实验中补充知识](#day-31-32：bgp综合实验中补充知识)
  - [Day 33：peer-group,listen range,address-family,BGP路由惩罚](#day-33：peer-grouplisten-rangeaddress-familybgp路由惩罚)
  - [Day 34：BGP的重分布专题](#day-34：bgp的重分布专题)
  - [Day 35：PBR(Policing-based Pouting)](#day-35：pbrpolicing-based-pouting)
- [四、组播与 IPv6 基础](#四组播与-ipv6-基础)
  - [Day 36-39：组播引入,组播地址规划,组播MAC地址,IGMP](#day-36-39：组播引入组播地址规划组播mac地址igmp)
  - [Day 40：PIM Sparse-mode中动态选举RP的方式(AutoRP,BSR)](#day-40：pim-sparse-mode中动态选举rp的方式autorpbsr)
  - [Day 41：IGMPV3&IGMP snooping](#day-41：igmpv3igmp-snooping)
  - [Day 42-43：IPv6的地址格式 · 地址空间划分 · IPv6单播地址范围 · EUI-64](#day-42-43：ipv6的地址格式-·-地址空间划分-·-ipv6单播地址范围-·-eui-64)
  - [Day 44：ICMPv6,NDP协议中NS,NA,RS,RA消息](#day-44：icmpv6ndp协议中nsnarsra消息)
- [五、IPv6 路由与过渡技术](#五ipv6-路由与过渡技术)
  - [Day 45-48：IPv6 SLAAC网关冗余,IPv6路由,IPv6静态路由写法,EIGRP,OSPF,BGP](#day-45-48：ipv6-slaac网关冗余ipv6路由ipv6静态路由写法eigrpospfbgp)
  - [Day 49：NAT64(network address translation)](#day-49：nat64network-address-translation)
- [六、园区网与交换机专题](#六园区网与交换机专题)
  - [Day 50：交换机知识复习,PVST,PVST+](#day-50：交换机知识复习pvstpvst)
  - [Day 51：RSTP(Rapid-PVST)](#day-51：rstprapid-pvst)
  - [Day 52：VLAN之间通讯](#day-52：vlan之间通讯)
  - [Day 53：交换机安全(port-security)](#day-53：交换机安全port-security)
  - [Day 54：VLAN安全(VACL,PVLAN)](#day-54：vlan安全vaclpvlan)
  - [Day 55-56：DHCP 安全（DHCP 欺骗攻击防范、DHCP 中继、DHCP Snooping、IP 源保护）](#day-55-56：dhcp-安全dhcp-欺骗攻击防范dhcp-中继dhcp-snoopingip-源保护)
  - [Day 57：DAI(Dynamic ARP Inspection),EtherChannel](#day-57：daidynamic-arp-inspectionetherchannel)

---

# 一、EIGRP 专题

> 增强型内部网关路由协议

## Day 1：EIGRP专题-CCNP第一课 NA路由知识回顾

上课方式，课程介绍：CCNP课程 每周一，三，五 晚上 19:00 - 21:30 风雨无阻法定节假日，老师“没了”上海市徐汇区斜土路 英雄大厦周期 2个半月- 3个月。CCIE课程 5月8号开班 每周二 周四 19:00 - 21:30 周六 下午13:30- 16:00老师是全职，手机一天24小时开机，微信永不断连 碰到问题可以直接微信单播留言，或者在群里如果老师没有回复消息 要么在睡觉 要么在上课 要么真的在忙

**考证：**

**学习旧学习 考证旧考证**

学习可以细究一些，仔细一些，但是不用钻牛角尖

考试是可以功利过去的

CCNA：可以在公司的网络项目组当中完成中小型网络的部署和运维。

一门笔试（选择题） 有题库 考试抽100题

CCNP：可以独自完成中小型公司网络的部署和运维。

两门笔试 有题库

一门核心笔试（350- 401）引入了操作题 虽然有趣库 但是还是建议学习完NP之后再去考笔试。678多道单选多选拖图题，操作题有55道 （考试时抽6道操作题 和50道单选多选拖图） 满分1080分 825通过。NP学习完了之后再考笔试 如果比较急可以在学习完园区网交换机技术之后再备考一门选考笔试（380- 418/380- 420） 两个选一个

CCIE：可以独自完成大型公司及分支站点的部署和运维。

**一门笔试+一门LAB考试**

一门核心笔试（350- 401）

LAB（实验）考试 有解法。 一旦开始备考，可以每天预约3个小时的机架

所有的笔试都可以随时随地预约。

所有的实验考试预约两个月后的位置

考完CCNP和CCIE之后将会有证书的有效期（3年）

**需要重认证：**

积分制：满120分则重认证成功。一门笔试60分 例如考两门笔试则重认证成功了。CCDE笔试 120分一门LAB 120分

**如何学习：**

理论配置操作练习

每节课有录播 有课堂的随堂笔记

**尽可能上直播课**

每个专题都会有综合实验需要完成，交作业。

使用模拟器来进行上课的实验和练习。

PNET 或 EVE。

安装过程中如果碰到虚拟化的安全性问题，联系老师解决。

**EIGRP引入**

**路由器依据路由表转发**

**路由的回顾：**

**直连路由**

> 流程图文字

路由

```
├── 直连路由
│ └── 主机路由
└── 非直连路由
├── 静态路由
└── 动态路由
├── 距离矢量动态路由协议 -> EIGRP
└── 链路状态动态路由协议
├── OSPF
└── IS-IS
```

**直连路由：**

当路由器的接口UP，链路的协议UP，接口配置了IPv4地址及掩码，将会产生接口地址对应网段的直连路由插入到路由表。

解决了路由器直连链路的互相访问代表了接口所连接的对应网段

**主机路由：**

当路由器的接口UP，链路的协议UP，接口配置了IPv4地址及掩码，将会产生接口地址对应/32位掩码的主机路由插入到路由表。

解决路由器自身IPv4地址的访问。

防止网络中地址冲突造成访问自身地址去往其它路由器的问题出现

不会被宣告进入任何的动态路由协议数据库

**静态路由：**

手工在路由器的路由表中插入路由条目。

```
R1(config)#ip route 192.168.23.0 255.255.255.0 G0/0
```

需要下一跳网关路由器接口开启代理ARP功能：

当路由器收到ARP请求时，查看ARP请求的目的IP地址并非自己接口的IP地址，如果开启了代理ARP功能，路由器将会查询路由表，如果自己有去往目的地址的路由条目，则发觉自身是本网段与目的地址所在网段的网关设备，主动回复自己接口的MAC地址作为ARPReply给予发送方。

Cisco路由器所有接口默认开启代理ARP。

华为华三路由器接口默认关闭代理ARP。

```
R1(config)#ip route 192.168.23.0 255.255.255.0 172.16.12.2 //静态路由跟下一跳地址的写法（最常用的。）
```

当路由器根据路由表转发数据包时，将会直接封装目的MAC地址为该路由条目下一跳地址对应的MAC地址，将数据包送到网关设备上。

**简单，高效，稳定**

中大型网路使用静态路由配置量非常大。

人工配置，容易产生次优路径和环路。

动态路由协议→EIGRP引入。

Cisco私有。

EIGRP是典型的距离矢量动态路由协议。

可以自动运算，计算出最优的路由条目提交到路由表。

**工作方式概述：**

将路由器接口的自身直连路由（静态路由也可以）存放进入动态路由协议的数据库，并将该数据库条目通告给其它的路由器。

谁给自己的数据库条目，下一跳指向谁

## Day 2：EIGRP的邻居表 · 数据库表 · EIGRP数据包类型 · EIGRP建立邻居的过程

**创建EIGRP进程**

EIGRP基于IPv4协议，协议号码88。

**EIGRP的运行方式**

**创建EIGRP进程**

```
R1(config)#router eigrp <process ID> //创建EIGRP进程仅有EIGRP的框架和数据库- 激活路由器的接口运行EIGRP. network命令适用于激活接口，存放进入数据库的是接口的路由条目，network在RIP，OSPF，EIGRP中与路由条目无关。network：使用network命令匹配IPv4的地址范围，被范围地址匹配的本路由器接口地址，则接口被激活运行动态路由协议。
```

被network命令后续网段匹配的接口地址，该地址对应的接口被激活运行EIGRP

被network命令后续网段匹配的接口地址，该地址对应接口的直连路由被存放进入动态路由协议的数据库。

例如需要激活172.16.12.1/24接口运行EIGRP。

正确方式激活：network 172.16.12.0 255.255.255.0 //哪怕使用正确方式激活也会自动转成反掩码。

反掩码方式激活：network 172.16.12.0 0.0.0.255

精确方式激活：network 172.16.12.1 0.0.0.0

老师个人最喜欢的方案。

以上都是方便理解的方法。

```
R1(config-router)# network <network number> <eigrp wildcard bits>
```

通配符：帮助匹配前缀地址，使得单台命令行可以同时匹配上多个条目参数。通配符用0来表示前缀地址的对应位置固定，用1表示前缀地址的对应位置可以发生变化。

**EIGRP引入的表示**

邻居表：记录了EIGRP的邻居状态信息。

在EIGRP当中需要先建立邻居关系再去互相之间传递数据库条目。

当路由器收到了对方的EIGRPHello包时则直接记录下对方的信息，与对方建立超邻居关系。

```
R1#show ip eigrp neighbors //查看EIGRP的邻居关系
```

数据库表：专用于存放EIGRP存入到数据库的路由条目信息。

```
R1#show ip eigrp topology
```

> 💡 用于查看EIGRP的数据库表项。

EIGRP引入的数据包类型

Hello：发现，建立，和维持EIGRP的邻居关系；用作ACK消息针对于EIGRP的Update数据包，Query数据包做出回复。

只要路由器的接口一旦被激活运行了EIGRP，则接口将会立刻加入到EIGRP的组播地址224.0.0.10，并且开始周期性（每隔5s）的向224.0.0.10发送

EIGRP的Hello包。

为什么使用组播？

因为路由器也不知道自己的邻居是谁，在跟邻居互相交换信息之前，谁都不认识谁。在不认识对方的情况下可以通过组播给对方发送消息。

```
R1#show ip int g0/0
```

> 💡 查看接口的网络信息可以查看到接口加入了哪些组播地址。

```
R1#show ip int g0/0 哪怕建立了EIGRP邻居关系，也会仍然每隔5s周期性互相之间发送Hello包。维持邻居关系。默认情况下，超过hold时间（15s）收不到对方的Hello则认为对方出现故障，重置&断开邻居关系。
```

Update数据包：用于可靠性确认。更新数据包，EIGRP将数据库条目更新通过update数据包发送给邻居；

EIGRP建立邻居的过程。

EIGRP作为网络层协议仍需确保通告的信息已被对方接收，双方可以稳定可靠的传输。

通过update数据包以及ACK确认消息来保证EIGRP的可靠性传输。

ACK：Hello包的特殊消息，用作确认。一旦收到了对方的update路由条目更新，或者query查询消息，都会用ACK做出回复。

> 拓扑图：R1(G0/0) <--- 172.16.12.0/24 ---> (G0/0)R2(G0/1) <--- 192.168.23.0/24 ---> (G0/1)R3

一旦建立好EIGRP的邻居关系，则会立刻向邻居单播发送一次EIGRP的Hello包。

例如，如图所示，R1收到了R2发送过来的EIGRPHello包，认为R2是自己的EIGRP邻居，存放进邻居表，但是，为了确保自己与R2之间可以稳定的传输，则向R2单播发送一次EIGRP的Update数据包，该数据包当中不通告路由条目更新，仅携带了Sequence号和Acknowledge号码（以下简称为序列号和ACK。）

update: Seq = 7 ACK = 0

R1- - - - - - - - - - - - - - - - - - - - - R2

update: Seq = 9 ACK = 7

R1<- - - - - - - - - - - - - - - - - - - - - R2

R1能够确定自己跟R2之间可以互相交互。

ACK: Seq = 0 ACK = 9

2能够确定自己跟R1之间可以互相交互。

> 拓扑图：R1(G0/0) <--- 172.16.12.0/24 ---> (G0/0)R2(G0/1) <--- 192.168.23.0/24 ---> (G0/1)R3

当可靠性确认完成，R1开始发送路由条目更新。

update: 10.10.1.0/24 seq = 8 ACK = 0 R1- - - - - - - - - - - - - - - - - - - - - 224.0.0.10

> 示意图

R1<---Hello(ACK) seq = 0 ACK = 8-------------------R2

update 192.168.23.0/24 10.10.2.0/24 seq = 10 ACK = 0

> 示意图

224.0.0.10<-------------------R2

Hello(ACK) seq = 0 ACK = 10

R1- - - - - - - - - - - - - - - - - - - - - R2

以上是双方互相之间交换各自的EIGRP数据库条目信息。

update: seq = 8 ACK = 10

R1- - - - - - - - - - - - - - - - - - - - - R2

表示由R1开始的本次双方建立邻居关系的数据库条目交换仪式到此结束。

> 示意图

Update 192.168.23.0/24 10.10.2.0/24 seq = 9 ACK = 0

R1------------------------------------->224.0.0.10

R1问R2你通告给我的是不是这些路由？

> 示意图

R1<---Hello(ACK) seq = 0 ACK = 9-------------------R2

R2告诉R1，是的没错。

update: 10.10.1.0/24 seq = 11 ACK = 0

224.0.0.10- - - - - - - - - - - - - - - - - - - - - R2

R2问R1，你给给我的是这些路由吗？

Hello(ACK) seq = 0 ACK = 11 R1- - - - - - - - - - - - - - - - - - - - - R2

R1跟R2说：是的没错。

SRTT (smooth round-trip time): 平均往返时间

当EIGRP邻居刚刚建立，需要使用update消息来进行可靠性确认（三个数据包），并且在可靠性确认过程中记录下发送update数据包到对方回复ACK消息的平均往返时间。

如果没有可靠性确认的update消息的交互，默认的SRTT时间1ms。

RTO(retransmission Time-out): 重传超时计时器。路由器通过SRTT自动计算RTO（算法Cisco保留了）

路由器针对于等待ACK消息的时间底线。如果超过了RTO时间还收不到对方发送给自己的ACK消息回复，则会立刻再次发送一个update消息。

如果没有可靠性确认的update消息的交互，默认的RTO时间500ms。5s收不到对方的ACK则重传update消息。

**十六次重传机制：**

一旦路由器超过RTO时间仍收不到对端发送的ACK消息回复则会立刻重新发送update消息。再一次超过RTO时间收不到ACK则再次发送update消息，如此往复，一共将会重传十六次update，如果十六次update都没有ACK的回复，则断开并重置与对方的EIGRP邻居关系。

```
R2#debug eigrp packets update
```

Queue count: 队列数量

对方是否有数据包还未处理，表示是否有数据包等待对方回复。 者单边邻居。

1: 表示对方还有消息并未给出答复。

## Day 3：影响EIGRP建立邻居的条件,EIGRP的Metric计算方式,FD,AD

CCNP day 3

EIGRP 建立邻居的条件

EIGRP的AS(进程)表明了自已的归属地,自己属于哪个AS。

AS如果不一样则不能够建立起EIGRP邻居关系。

单播对单播，组播对组播。

默认情况下，EIGRP选择使用组播的方式发送Hello包，用于发现邻居关系，建立邻居关系。

neighbor <x> <interface> //指定接口通过单播的方式与某一个IPv4地址建立EIGRP邻居关系。

代价——如果接口使用neighbor命令指定了单播邻居，则该接口不再接收任何EIGRP的组播数据包，仅接收EIGRP的单播数据包。

认证通过。

双方的接口之间可以互相Ping通才可以起邻居

当接口收到了EIGRP Hello包时,检查EIGRP Hello包的源IPv4地址在本接口上是否可以访问,可以则与对方建立EIGRP邻居关系。

当接口收到了EIGRP Hello包时,检查EIGRP Hello包的源IPv4地址在本接口上是否有直连路由可达,可以与对方建立EIGRP邻居关系★

**(扩展知识:辅助地址)**

主地址：一个设备的接口有且仅有一个IPv4主地址。 当设备主动从接口发送消息时,默认只会使用接口的主地址发送。

```
R2(config-if)#ip add 172.16.12.2 255.255.255.0 secondary //secondary将地址作为辅助地址配置在接口
```

辅助地址默认情况下不会主动发送消息,但是可以接收发送过来的消息。(主要用于重分布 在学习完EIGRP的RIP之后会有重分布专题)

EIGRP认证通过(暂略)

EIGRP的Metric一致

EIGRP计算Metric值时需要利用K值对应路由条目的传递链路当中的对应链路参数情况。

K值有6个

**K1 = 带宽**

K2 = 最大时延的可靠性

K3 = 延时之和

**K4 = 最小负载**

K5 = MTU

K6 = 电力损耗(运营商未使用)

K值相当于EIGRP对于路径的价值、判断最优路由条目的依据所在。

**默认情况下K值**

K1 = 1

K2 = 0

K3 = 1

K4 = 0

K5 = 0

K6 = 0 (还没被拿来做使用)

K值不相同,双方计算Metric值的方式不同,就起不了EIGRP邻居。

```
R1#show ip protocols //可以查看本设备上所有IPv4协议。
```

**EIGRP的邻居关系建立**

这是一个完美的相互过程。

双方在同一区域 (异域容易乱)

单对单 (直连对直连) 多对多 (组播活动)

**需要能直接沟通**

有类似接口信息来增加仪式感

最终还是需要的值相同的,...

Hello time和Hold time是否影响到EIGRP建立邻居关系?

Hello time和Hold time不影响EIGRP邻居关系的建立。

```
R1(config)#interface g0/0
R1(config-if)#ip hello-interval eigrp 100 XX //修改EIGRP接口的Hello time。
```

使用上一条命令改变了EIGRP接口自身发送Hello包的时间间隔。

```
R1(config-if)#ip hold-time eigrp 100 //修改EIGRP的Hold time
```

告诉邻居超过多长时间收不到我的Hello包则主动重置与自己的EIGRP邻居关系。

千万注意: Hold time一定不要小于Hello time。

路由的传递方向？数据流量的转发方向？

距离矢量动态路由协议当中，路由的传递方向与数据流量的方向正好相反。

Min.Bandwidth 

≡

≡ 路由条目传递方向上入方向接口的最小带宽（从源头开始） 单位kbps

Total Delay 

≡

≡ 路由条目传递方向上入方向接口的延时之和（从源头开始） 单位usec/10

路由器怎么知道路径上的最小带宽和延时之和

路由在通告EIGRP数据库条目出去时会携带上目前计算该数据库条目Metric值得当前链路各项参数。

**EIGRP的DUAL算法参数：**

EIGRP的DUAL算法参数：FD（Forward Distance）转发距离：本路由器去往目的网段的Metric值。

RD（Report Distance）/AD（Advertise Distance）通告距离：本路径的下一跳路由器去往目的网段的Metric值。

Successor路由：最优路由

Feasible Successor路由：次优路由

## Day 4：EIGRP的DUAL算法参数 修改Metric的方式

调整路由器条目传递方向入方向最小带宽（不推荐）下之下策

调整路由器条目传递方向入方向延时之和。

Offset-list（偏移列表） //距离矢量动态路由协议专用于调整Metric值的工具。可以将路由器条目的Metric进行添加。（不能减）

利用标准访问控制列表匹配路由器条目。

利用Offset-list针对于匹配的路由调整Metric。

access-list <0-99>/<1300-1999> //编号标识的标准访问控制列表

ip access-list standard //可以命名的标准访问控制列表

使用标准访问控制列表匹配路由，仅能够匹配路由条目的问题标识（前缀），不能匹配路由条目的问题。

```
R1(config)#access-list 1 permit 10.10.3.0 //匹配上10.10.3.0的路由
R1(config)#router eigrp 90 //当从G0/3接口收到EIGRP路由条目时，针对于匹配的路由+257由+257
```

Offset-list在一个方向上或者作用于接口的方向上只能够调用一个访问控制列表。

offset-list in //从所有接口收到了的EIGRP对应条目添加Metric。

offset-list in //从某一个接口收到了的EIGRP对应条目添加Metric。

offset-list out //从所有接口通告的EIGRP对应条目添加Metric

offset-list out //从某一个接口通告的EIGRP对应条目添加Metric。

## Day 5：EIGRP的汇总,EIGRP注入默认路由的方式

CCNP Day 5

**EIGRP的汇总**

减少路由当中连贯的、相同转发路径的路由条目数量，减少路由器转发数据包时查询路由条目的负载。

**自动汇总**

IOS版本 > 15.0 默认情况下EIGRP关闭了自动汇总。

```
R1(config)#router eigrp 90
R1(config-router)#auto-summary //开启自动汇总(慎用)
```

当路由器从接口通告出去明细路由时，要检查该明细路由的主类与出接口的主类是否相同，如果不相同，则将该明细路由汇总成主类路由通告出去，相反，则正常通告明细路由。

只有通告明细路由的发起路由器可以进行主类自动汇总、针对于学习到的EIGRP路由条目无法自动汇总。

自动汇总全部汇总成主类路由，无法自行调配。

主类汇总的范国过大，容易引起转发错误。

**手工汇总**

最常用的是手工汇总。

将明细路由汇总成路由条目时，最终汇总路由条目的掩码可以自行决定。

针对于自己学习到的路由条目也可以进行汇总。

符合条件的明细路由(被汇总路由包含的明细路由)可以被汇总，抑制明细路由，不通告明细，仅通告汇总路由。

明细路由可以被汇总多次。

```
R1(config)#interface g0/0
R1(config-if)#ip summary-address eigrp <AS_num> <network number> <mask> //在接口出配置EIGRP汇总。
```

必须被汇总路由存在至少一条才能够进行汇总。

汇总以后，将会自动产生汇总网段对应的指向Null0的防环路由。(discard port) ★★★

汇总掩码尽可能地精确。

EIGRP注入默认路由的方式

通过network命令默认宣告路由进入EIGRP的数据库，通过EIGRP的通告使得网络中的其它设备计算产生默认路由。

**Network命令用于宣告：**

被network匹配的接口能被地址，该地址对应的接口被激活运行EIGRP

被network匹配的接口地址，该地址对应的接口的直连路由被存放进入动态路由协议的数据库。

在EIGRP当中使用network命令可以用于宣告路由。但是需要满足以下条件：

仅有EIGRP和RIP可以使用network命令宣告路由。(以下条件仅适用于EIGRP，不包含RIP)

该路由条目必须是静态路由，非静态路由不可宣告进入EIGRP。

该静态路由必须指出接口，非下一跳地址的静态路由不可宣告进入EIGRP。

被network命令匹配的接口(指的是该路由条目)才可能被宣告进入EIGRP数据库。

出接口路由： ip route 0.0.0.0 0.0.0.0 <interface>

宣告该默认路由进入数据库： router eigrp <as> / network 0.0.0.0 0.0.0.0

通过重分布的方式将出接口的默认路由重分布引入到EIGRP的数据库，并将该数据库条目通告给其它路由器。

可以将路由进程中其它协议(例如Local主机路由)的路由条目以外部的形式引入到EIGRP当中。

route is Internal: 内部路由，在本EIGRP进程当中通过network命令加入的数据库条目都为内部路由。

route is External: 外部路由，在本EIGRP进程不是通过network引入的数据库条目，而是从别的协议导入到EIGRP数据库的条目。

出接口路由： ip route 0.0.0.0 0.0.0.0 <interface>

```
R3(config)#router eigrp 90
R3(config-router)#redistribute static
```

在EIGRP当中，内部路由条目的管理距离为 90 ， 外部路由的管理距离为 170

汇总产生默认路由，在出路由器连接内部网络的接口上进行汇总，通告EIGRP的默认路由。

```
R3(config-if)#ip summary-address eigrp <as> 0.0.0.0 0.0.0.0
```

## Day 6：EIGRP的等价负载分担和非等价负载分担,负载分担的转发方式,EIGRP的路由条目过滤

使用EIGRP协议路由协议，使用EIGRP协议路由协议，使用EIGRP协议路由协议，使用EIGR协议路由协议，使用EIGRP协议路由协议，使用EIGRP协议路由协议。

EIGRP等价负载分担和非等价负载分担。EIGRP过滤路由条目EIGRP查询机制。

路由器的路由表中仅能够存放一条最优路由。（默认）

路由器的路由表中仅能够存放一条最优路由。（默认）当出现相同网段标识，相同掩码的路由条目时，比较路由条目的管理距离和Metric来选择最优路由。优先比较管理距离，小的优先，管理距离相同则比较Metric，同样小的优先。仅有当管理距离与Metric都相同的路由条目时，才能够都提交到路由表。实现等价负载分担。

**EIGRP的非等价负载分担：**

EIGRP非等价负载分担：EIGRP非等价负载分担：EIGRP非等价负载分担：EIGRP协议路由协议，使用EIGRP协议路由协议，使用EIGRP协议路由协议，使用EIGRP协议的协议路由协议，使用EIGRP协议的协议路由协议，使用EIGRP协议的协议。

在EIGRP当中，允许Metric不相同的路由条目都可以提交到路由表实现负载分担。

仅有Feasible Successor路由可以与successor路由一同提交到路由表实现非等价负载分担。

Feasible Successor路由：次优路由，虽然不是FD第二小的路由条目，但是一定不会产生环路的次优路径。

Feasible Successor'AD<Successor路由'FD

会随同Successor路由一同存在EIGRP的数据库并中且，一旦检测到Successor路由故障，则立刻直接将其提交到路由表。

Successor'FD 

×

× VarianceValue（默认=1）>Feasible Successor'FD

最优路由的FD×variance大于Feasible Successor路由的FD，则该Feasible Successor路由可以一同提交到路由表。

```
R1(config)#router eigrp 90
```

```
R1(config-router)#variance XX //调整Variance的数字
```

如果实现了非等价负载分担，则Feasible Successor路由也可以提交到路由表中，如果Successor路由故障省去了从数据库提交到路由表的步骤，加快收敛。并且Feasible Successor路由也能够承担一部分转发的目的，但是排除以下情况：

```
R1(config)#router eigrp 90
```

```
R1(config-router)#traffic-share min across-interfaces //
```

> 💡 那怕非等价负载分担了，也仍然让数据流量走Metric小的

Successor路由。

虽然实现了非等价负载，但是除了Successor路由，Feasible Successor路由不负责转发数据流量，最终目的，省去了Successor路由故障将Feasible Successor路由从数据库提交到路由表的步骤，加快收敛。

针对于目的地址的负载分担（默认）

现如今Cisco路由器默认的执行方案。

访问相同目的地址的数据流量按照相同路径转发。

针对于数据包的负载分担

如果是等价负载分担，则每一个链路发送一个数据包之后切换到另一个链路转发。

```
R1(config)#no ip cef //关闭Cisco的快速转发
```

平均的分配每一个链路上的数据包。

如果是非等价负载分担，则按照链路的Metric比例来分配每一个链路上发送数据包的数量。

**EIGRP的路由过滤：**

工具：Distribute-list 分发列表 专用于距离矢量（链路状态其实也可以但是比较特殊）路由条目过滤使用的工具。

Distribute-list <ACL> in <cr>

//当从所有接口收到路由条目时调用ACL针对于路由做过滤

Distribute-list <ACL> in <interface>

//当从某个接口收到路由条目时调用ACL针对于路由做过滤

Distribute-list <ACL> out <cr>

//当从所有接口通告路由条目时调用ACL针对于路

**由做过滤**

Distribute-list <ACL> out <interface>

//当从某个接口通告路由条目时调用ACL针对于路由做过滤

利用ACL来设定是否通告路由条目或是禁止路由条目。

access-list 1 permit //放行路由

access-list 1 deny //禁止路由条目。

access-list <0-99>/<1300-1999> <deny/permit>

//编号标识的标准访问控制列表

ip access-list standard <deny/permit>

//可以命名的标准访问控制列表

使用标准访问控制列表匹配路由，仅能够匹配路由条目的网段标识（前缀），不能匹配路由条目的掩码。

当IGRP丢失了当前的Successor路由时，如果数据库当中不存在满足条件的Feasible Successor路由，则会通过IGRP查询机制尽可能找到去往目的网段的另一条路径，进行收敛。

如果IGRP数据库当中存在Feasible Successor路由，当Successor路由丢失时，则不需要查询，直接将Feasible Successor路由提交到路由表。

## Day 7：EIGRP的查询机制,Query,SIA-Query

当EIGRP丢失了当前的Successor路由时，如果数据库当中不存在满足条件的Feasible Successor路由，则会通过EIGRP查询机制尽可能找到去往目的网段的另一条路径，进行收敛。

如果EIGRP数据库当中存在Feasible Successor路由，当Successor路由丢失时，则不需要查询，直接将Feasible Successor路由提交到路由表。

**EIGRP查询机制的数据包：**

Query：查询数据包，当EIGRP路由器丢失了自身的successor路由之后，将会向自己的所有EIGRP邻居发送Query消息，询问一下对方是否知道该路由条目的相关信息（看看邻居有没有去往目的网段的路由）

ACK：回复消息，Hello包的特殊情况。

Reply：用于做出针对于Query消息所查询的路由条目进行回复。

**EIGRP查询机制：**

当EIGRP路由器丢失了最优路由之后，尝试找到另外一个去往目的网段的转发方向的机制。

情况一：当EIGRP的路由器丢失了最优路由，且其它路径的路由器也没有去往目的网段的路由的情况。

当EIGRP路由器丢失了Successor路由，且没有feasible Successor路由的情况下，将会立刻向所有的EIGRP邻居发送Query消息，表明自己该路由条目延迟无穷，带宽最大，无法计算路由，查询该路由条目的情况；当邻居收到了Query消息时，将会优先回复ACK（表示你发送的查询请求我收到了。），然后邻居路由器去查询自身关于该路由的情况，此时发现自身也没有该路由条目的信息，则直接回复Reply消息，并表示该路由条目延时是无穷，且没有任何该路由条目的信息，告诉发送查询的路由器，该路由6了；当路由器收到了Reply之后会优先回复ACK（表示针对于Reply消息的回复，Reply消息收到了。），最终将该路由条目从数据库当中删除。

情况二：当EIGRP路由器丢失了最优路由，且其它路由器有该路由条目并且下一跳不是自己。

当EIGRP路由器丢失了Successor路由，且没有feasible Successor路由的情况下，将会立刻向所有的EIGRP邻居发送Query消息，表明自己该路由条目延迟无穷，带宽最大，无法计算路由，查询该路由条目的情况；当邻居收到了Query消息时，将会优先回复ACK（表示你发送的查询请求我收到了。），然后邻居路由器去查询自身关于该路由的情况，邻居路由器发现自己有该路由条目的信息，并且下一跳不是发送该Query消息的路由器，将会把该路由条目通过Reply消息做出回应，告诉对方自己的该路由条目的信息；当路由器收到了Reply消息之后优先回复ACK消息，并且发现对方是一条可用路由，则通过其中的条目信息，计算该路由条目的Metric，最终将该条目提交到路由表，成功完成路径切换。

情况三：当EIGRP路由器丢失了最优路由，且其它路由器有该路由条目信息并且下一跳就是发送Query消息的路由器。

当EIGRP路由器丢失了Successor路由，且没有feasible Successor路由的情况下，将会立刻向所有的EIGRP邻居发送Query消息，表明自己该路由条目延迟无穷，带宽最大，无法计算路由，查询该路由条目的情况；

当邻居收到了Query消息时，将会优先回复ACK（表示你发送的查询请求我收到了。

），然后邻居路由器去查询自身关于该路由的情况，邻居路由器发现自己有该路由条目的信息，并且下一跳就是发送Query消息的路由器，此时此刻，被查询的路由器也意识到自己的Success路由条目也出现了故障，被查询的路由器将会向除了发送给自己Query消息的邻居以外的其它EIGRP邻居发送Query消息，并且在自己收到Reply消息之前不会向给自己发送Query的路由器回复Reply，如果再下一个路由器收到Query消息发现路由的下一跳还是指向发送Query消息的路由器，则继续向它的其它邻居发送Query查询，每一次查询都会经历以上的情况，情况二，情况三；

该查询将会一致持续到EIGRP网络的边界路由器上（除了发送给自己Query的EIGRP邻居以外没有其它的EIGRP邻居可以发送Query），如果Query查询到了网络的边界仍然没有其它去往目的网段的路径，则回复Reply，告知该路由条目不可使用，没有其它路径，最终路由器收到了Reply之后将数据库条目删除并继续向前发送Reply告知整个路径上的设备，该路由条目没有其它方向可转发，整个路径的设备都删除掉该数据库条目。

EIGRP当中通告路由条目不可用将会把延时设置为infinity

EIGRP的SIA-Query查询。

路由器发送了几个Query消息出去就需要收到了几个Query消息的回复。否则就不清楚针对于该数据库条目有没有其他路径？是否需要删除？。

当EIGRP发送了Query消息时，会在本地开启一个Query消息计时器，时间为3min（180s）。如果超过了180s还收不到该路径上的Reply消息，则直接重置与对方的EIGRP邻居关系。

由于上述方案可能会造成整个路径上的EIGRP邻居关系全部重置，所以引入了SIA-Query消息。做出确保。

当EIGRP发送了Query消息时，会在本地开启一个Query消息计时器，时间为3min（180s）。如果超过了1min30s（一分半/90s）收不到链路上的Reply消息，则主动发送一次SIA-Query消息，如果对方收到了SIA-Query则需要主动地回复SIA-Reply做出确认，从而让路由器得知并回响这一段链路的故障造成收不到Reply消息的问题，当Query的3min倒计时的结果则不会重置EIGRP邻居关系。

当发送了SIA-Query时收不到对方的SIA-Reply则会将对方该数据库条目置为SIA-Stuck（卡在了SIA-Query的状态），并等待对方的SIA-Reply，如果3mins时间一到，则重置与对方的EIGRP邻居关系。

## Day 8：限制EIGRP的查询范围

1 EIGRP限制查询范围的方式.

汇总

EIGRP路由器丢失了successor路由且没有feasible successor路由时，将会向所有的EIGRP邻居发送Query查询消息，查询该明细路由对应的路由条目信息。被查询的路由器必须在数据库当中判断是否存在与Query消息中一模一样的明细路由条目。但凡掩码不一样，或者网段标识不一样都认为自己没有这条路由。

**EIGRP的边界路由器.**

正常情况下，常说一台链接着终端设备的EIGRP路由器是EIGRP的边界路由器，其只有直连路由是自己的，其它路由器都是从上游的EIGRP路由器学习到的。该路由器对接终端，一般情况下很少会有该路由器有其它去往目的网段的途径。

在EIGRP当中，可以直接让一台 那怕是中游或中下游的，不是真正边界路由器，使其成为逻辑上的EIGRP边界路由器。

EIGRP的边界路由器（stub）特点：

如果路由器被配置为EIGRP的边界路由器，则该路由器不会成为查询的对象。（被配置的边界路由器将在Hello包当中告诉自己的邻居自己是边界路由器。）Stub路由器不会成为查询的对象，但是可以发送查询消息。默认情况下EIGRPStub路由器只通告自己数据库条目的直连路由和自己的汇总路由。学习到的EIGRP数据库条目都不会通告。

**[代码框内容]**

text

```
R2(config)#router eigrp 90
R2(config-router)#eigrp stub                            //使得路由器成为EIGRP的边界路由器。
R2(config-router)#eigrp stub connected summary          //默认情况下EIGRP的Stub路由器只通告自己的直连路由和自己的汇总路由
R2(config-router)#
R2(config-router)#eigrp stub ?
```

  connected      Do advertise connected routes

  leak-map       Allow dynamic prefixes based on the leak-map (包括学习到的)

  receive-only   Set receive only neighbor

  redistributed  Do advertise redistributed routes

  static         Do advertise static routes

  summary        Do advertise summary routes

  <cr>

**[代码框内容]**

text

```
R1#show ip eigrp neighbors detail              //在邻居路由器上查看该路由器的详细信息
```

## Day 9-11：EIGRP综合实验补充知识

清理路由表指令 RX#clear ip route * 表.

RIP的重分布路由条目Metric值计算.

默认情况下，针对于RIP的通过network命令正常宣告激活接口存放进入数据库的路由，默认的Metric 

0

=0 ，此后路由器通告该路由条目时自动将Metric 

1

+1 针对于重分布标识的RIP数据库条目，路由器将其通告出去时Metric不变。当路由器将带有重分布标识的数据库条目通告出去时不会携带其重分布的标识。

Route-map：路由策略工具.

可以利用route-map工具针对于匹配出的路由条目做出策略性的操作。

利用route-map工具针对于匹配的路由条目设定其Metric值。

route-map <word(name)> permit/deny <seq_num>

同一个命名的route-map当中可以存在多个不同序列号的语句，最终同样于访问控制列表相同，按照序列号的从小到大依次执行。如果不设置序列号，则默认序列号从10开始，间隔同样与ACL相同，也为10。

**[代码框内容]**

text

1 ip access-list standard deny_100.1.8.0

2 deny 100.1.8.0

3 permit any

4 ip access-list standard JISHU

5 permit 100.1.1.0 0.0.6.0

6 ip access-list standard OUSHU

7 permit 100.1.0.0 0.0.6.0

8 route-map Change_Metric permit 10

9 match ip address JISHU

10 set metric 5

11 route-map Change_Metric permit 20

12 match ip address OUSHU

13 set metric 7

14 route-map Change_Metric permit 30

15 router rip

16 redistribute connected route-map Change_Metric //当重分布直连路由引入RIP时，只有route-map当中对应的路由条目允许被引入

17 distribute-list deny_100.1.8.0 out GigabitEthernet0/0 //当通告路由的时候过滤掉100.1.8.0

**[代码框内容]**

text

1. R1(config)#ip access-list standard deny_100.1.8.0
2. R1(config-std-nacl)#deny 100.1.8.0
3. R1(config-std-nacl)#permit any
4. R1(config)#route-map Change_Metric permit 10

**5 许**

6. R1(config-route-map)#match ip address OUSHU
7. R1(config-route-map)#set metric 7
8. R1(config-route-map)#exit
9. R1(config)#route-map Change_Metric permit 20

10 许，表示其它的路由条目默认也允许通过

11. R1(config-route-map)#exit
12. R1(config)#router rip
13. R1(config-router)#redistribute connected metric 5 route-map Change_Metric //当重分布直连路由引入RIP时，其中偶数路由被指定了对方的Metric等于7，其它路由条目默认也允许被重分布且默认它们的Metric设定为5...
14. R1(config-router)#distribute-list deny_100.1.8.0 out GigabitEthernet0/0 //当通告路由的时候过滤掉100.1.8.0

**[代码框内容]**

text

1. R1(config)#ip access-list standard permit_100.1.8.0
2. R1(config-std-nacl)#permit 100.1.8.0
3. R1(config-std-nacl)#exit
4. R1(config)#route-map Change_Metric permit 10

**5 许**

6. R1(config-route-map)#match ip address OUSHU
7. R1(config-route-map)#set metric 7
8. R1(config-route-map)#exit
9. R1(config)#route-map Change_Metric permit 20

10 许，表示其它的路由条目默认也允许通过

11. R1(config-route-map)#match ip address permit_100.1.8.0
12. R1(config-route-map)#set metric 16
13. R1(config-route-map)#exit
14. R1(config)#route-map Change_Metric permit 30
15. R1(config-route-map)#exit
16. R1(config)#router rip
17. R1(config-router)#redistribute connected metric 5 route-map Change_Metric //当所有允许的路由条目都被引入到RIP时，默认的Metric都为5，其中针对于偶数路由允许被引入RIP且设置Metric=7，针对于100.1.8.0路由也允许被引入RIP，且设置Metric=16，其它路由也允许被引入RIP，并按照之前的默认Metric设定为5...

route-map工具如同访问控制列表一样，针对于未匹配的路由（数据），其默认的行为动作是deny。如果需要放行其它，需要添加一个permit <seq_num + 10> 的空节点

RIP的neighbor命令

```
R1(config)#router rip
```

```
R1(config-router)#neighbor 1.1.123.3
```

> 💡 在RIP中指定了单播邻居

RIP的neighbor命令行类似于“特别关照”，组播的RIP更新照样发，只是再一次单独地给neighbor指定的邻居地址再发一次RIP数据库条目更新。

指定了RIP的单播邻居，单独给邻居发送RIP的更新，组播照样发。

EIGRP的neighbor命令

EIGRP中使用neighbor命令指定了EIGRP的接口对端的单播邻居，则自己该接口只能通过单播的方式与对方交互EIGRP数据包，该接口不再接口EIGRP的任何组播数据包消息。

只要指定了接口单播邻居，则该接口不发也不受组播的EIGRP数据包。

RIP的Passive-interface

可以将RIP接口配置为“passive-interface（被动接口）”，路由器将不会再从该接口向外发送组播的RIP更新消息

接口不再能够发送RIP的组播更新消息，但是可以发送出去单播的RIP更新消息。但是还是可以接收其它RIP路由器的组播更新消息。

EIGRP的passive-interface

如果将EIGRP的接口指定为了被动接口，该接口将不再能够发送和接收任何EIGRP的组播数据包（也不收EIGRP的单播数据包。）

不再发送和接收EIGRP的组播数据包，不再接收EIGRP的单播数据包，但是可以发送EIGRP的单播数据包。

只要在EIGRP里面接口被置为了被动接口，则该接口将不再能够建立EIGRP邻居关系， 

⟶

⟶ 接口的路由可以存放进入数据库（因为被激活运行EIGRP），但是接口不向外发送也不收EIGRP的组播更新，接口不能够建立起来EIGRP邻居。

**水平分割**

距离矢量路由协议的防环措施，路由器从一个接口收到的数据库条目不会再从同一个接口通告出去。

```
R3(config)#interface g0/0 
R3(config-if)#no ip split-horizon
```

> 💡 关闭RIP的水平分割。

**第三方下一路：**

当路由器通告的路由条目下一跳与通告的设备地址网段能够互相访问时，将会优化该路由条目的下一跳地址，告知接收该路由条目的路由器选择指定的下一跳地址，不要选择自己作为下一跳。进行第三方下一跳优化。

Prefix-list：前缀列表

专用于匹配路由条目所使用的列表。

既能够匹配路由条目的前缀（网段标识），也能够匹配路由条目掩码。

使用标准的ACL来匹配路由：只能够匹配的路由条目的前缀（网段标识），不能够匹配路由条目的掩码

**例如：**

**路由表中存在四条明细路由：**

10.10.0.0/16 10.10.0.0/18 10.10.0.0/20 10.10.0.0/22

如果只能够使用标准的访问控制列表要求匹配上10.10.0.0/18明细路由。

access-list 1 permit

access-list 1 permit 10.10.0.0 

⇒

⇒ 10.10.0.0

以上的四条明细路由都会被匹配。

扩展的访问控制列表匹配路由：既能够匹配路由条目的前缀（网段标识），也能够匹配路由条目掩码。

access-list <100-199> <permit/deny> //扩展访问控制列表匹配数据流量

**例如：**

**路由表中存在四条明细路由：**

10.10.0.0/16

10.10.0.0/18

10.10.0.0/20

10.10.0.0/22

如果只能够使用扩展的访问控制列表要求匹配上10.10.0.0/18明细路由。

access-list 100 permit ip 10.10.0.0 0.0.0.0 255.255.192.0 0.0.0.0 一只匹配 10.10.0.0/18

如果希望能够匹配上以上10.10.0.0/18和10.10.0.0/20 掩码的两条明细路由。

access-list 100 permit ip 10.10.0.0 0.0.0.0 255.255.192.0 0.0.0.48.0

10.10.0.0 255.255.192.0 10.10.0.0/16

10.10.0.0 255.255.224.0 10.10.0.0/17

10.10.0.0 255.255.248.0 10.10.0.0/18

255.255.192.0

255.255.240.0

11111111.11111111.11000000.00000000

11111111.11111111.11110000.00000000

11111111.11111111.11110000.00000000

11111111.11111111.11110000.00000000 前级： 255.255.192.0

00000000.00000000.00110000.00000000 通配符： 0.0.48.0

11111111.11111111.11 00 0000.00000000 前级： 255.255.192.0

00000000.00000000.00110000.00000000 通配符： 0.0.48.0

11111111.11111111.11 00 0000.00000000 255.255.192.0

11111111.11111111.11 00 0000.00000000 255.255.192.0

11111111.11111111.11 00 0000.00000000 255.255.192.0

11111111.11111111.11 10 0000.00000000 255.255.224.0

11111111.11111111.11 11 0000.00000000 255.255.240.0

如果希望能够匹配上 10.10.0.0/18 和 10.10.1.0/18 和 10.10.2.0/18 和 10.10.3.0/18 四条明细路由。

access-list 100 permit ip 10.10.0.0 0.0.0.3.0 255.255.192.0 0.0.0.0.0.0.0.0.0.0.0

10.10.0.0 0.0.0.3.0

10.10.0.0 0.0.0.3.0

00001010.00001010.00000000.00000000

00000000.00000000.00000000 11.00000000

00001010.00001010.00000000.00000000 10.10.0.0/18

00001010.00001010.00000000 01.00000000 10.10.1.0/18

00001010.00001010.00000000 01.00000000 10.10.1.0/18

00001010.00001010.00000000 10.00000000 10.10.2.0/18

00001010.00001010.00000000 11.00000000 10.10.3.0/18

利用前缀列表匹配路由： 能够匹配路由条目的网段标识部分，还能够匹配路由条目的掩码部分。书写起来很方便，扩展起来也很方便。

ip prefix-list <name> <permit/deny> A.B.C.D./length ge X le Y

A.B.C.D: 网段标识的部分

length: 类似于通配符，/n 则表示网段标识的前面几个bits固定不便。

ge: 路由条目的掩码最小长度

le: 路由条目的掩码的最大长度

如果不写ge,le,则ge=le=length

```
R4#show ip prefix-list 检查前缀列表. 例: 路由表中存在四条明细路由:  10.10.0.0/24 10.10.1.0/24 10.10.2.0/24 10.10.3.0/24 如果只能够使用前缀列表要求匹配以上四条明细路由. ip prefix-list A permit 10.10.0.0/22 ge
```

如果不写ge,则ge = length 如果不写le,则le = 32. ge 不可以小于length 路由表中存在四条明细路由: 10.10.0.0/16 10.10.0.0/18 10.10.0.0/20 10.10.0.0/22 如果只能够使用扩展的访问控制列表要求匹配上10.10.0.0/18明细路由. ip prefix-list A permit 10.10.0.0/18 ip prefix-list A permit 0.0.0.0/1 ge

8 le 8 匹配了什么路由? 所有的A类主类路由. 0000000.0000000.0000000.0000000 0.0.0.0/8 - 1.0.0.0/8 - 127.0.0.0/8 ip prefix-list A permit 0.0.0.0/1 le 32 匹配了什么路由? 所有的A类路由 0000000.0000000.0000000.0000000 0.0.0.0/1 - 1.0.0.0/8 - 127.255.0.0/16 - 127.255.255.0/24 127.255.255.255/32 127.255.255.255/31 127.255.255.255/30 127.255.255.255/29 ip prefix-list A permit 0.0.0.0/8 le 32 匹配了什么路由? 所有的路由 0000000.0000000.0000000.0000000 0.0.0.0/9 - 255.255.255.255/32 ip prefix-list A permit 0.0.0.0/8 ge

1 le 32 匹配了什么路由? 除了默认路由以外的其它所有路由条目. 前缀列表也自带一句deny any. 默认最后会有一句ip prefix-list .deny 0.0.0.0/0 le 32 如果前缀列表需要放行其它路由,则需要补充一句ip prefix-list .permit 0.0.0.0/0 le 32 前缀列表同样按照每一个语句的序列号从小到大依次匹配调用.需要注意的是前缀列表每一个语句的序列号默认从5开始,每一个语句的序列号间隔为5. 

24 le

24 A.B.C.D: 网段标识的部分 Length: 类似于通配符,/n 则表示网段标识的前面几个bits固定不变. ge: 路由条目的掩码最小长度 le: 路由条目掩码的最大长度 如果不写ge,le,则ge=le=length 如果不写ge,则ge = length 如果不写le,则le = 32. 10.10.0.0 10.10.1.0 10.10.2.0 10.10.3.0 00001010.00001010.00000000.00000000 00001010.00001010.00000001.00000000 00001010.00001010.00000010.00000000 00001010.00001010.00000011.00000000 前缀,相同是几就是几,不同为9. ++ 00001010.00001010.00000000.00.++ 00000000

00001010.00001010.000000 00.++ 10.10.0.8/24 00001010.00001010.000000 01.++ 10.10.1.0/24 00001010.00001010.000000 10.++ 10.10.2.0/24 00001010.00001010.000000 11.++ 10.10.3.0/24

**重分布：**

当动态路由协议重分布本路由器的直连路由或静态路由进入数据库时不需要设置初始的Metric参数。

但当需要把其它动态路由协议的数据库条目引入到本动态路由协议时，需要讲究一个入乡随俗。

把其它动态路由协议的数据库条目引入本动态路由协议时需要给它设定一个初始的Metric，后续其在本协议当中传递时才能够继续计算Metric。

仅有提交到路由表的数据库条目才能够被重分布（有例外。）

分发列表基于协议的过滤（只有重分布的时候可以生效。）只能out方向。

ip access-list standard deny_100.1.1.0- 100.1.7.0

deny 100.1.0.0 0.0.7.0

permit any

router eigrp 100

EIGRP.

EIGRP时，调用ACL做过滤

**EIGRP的认证**

可以在EIGRP的路由器接口上开启认证，此后从该接口发送出去的EIGRP数据包都将携带接口的认证信息，并且从该接口收到的数据包必须携带认证信息，且认证信息通过才能够接收该EIGRP数据包。

**RIP的认证方式：**

**明文认证：**

设备发送动态路由协议的数据包时只发送接口所有Key当中KeyID最小的密钥，并且在发送时 不携带KeyID

**例如：**

接口当中存在key1 

= ccie key2 

= ccnp.

**在发送时仅发送：**

//由于明文认证，发送时直接发送明文。

接收方将对方Key值与自己密钥库的密钥进行一一比对，只要有一个对得上号则认证成功，可以接收对方的消息。

**MD5认证：**

设备发送动态路由协议的数据包时只发送接口所有的Key当中KeyID最小的密钥，并且在发送时 携带KeyID

例如

接口当中存在key1 

= ccie key2 

= ccnp.

在发送时仅发送： key1=ccie

//由于MD5加密认证，发送时会进行MD5加密

接收方将对方KeyID所对应的密钥与自己密钥库当中相同KeyID的密钥进行比对，如果密钥信息相同，则通过认证。

接收方将对方KeyID所对应的密钥与自己密钥库当中相同KeyID的密钥进行比对，如果密钥信息不同，则不通过认证，不接收消息。

如果对方的KeyID在自己的密钥库当中不存在，例如对方发送了Key1，自己没有Key1，则向上查找是否存在Key2?Key3?key4？，直接将对方的KeyID对应的密钥信息与自己密钥库当中比Key1大的KeyID进行比较，密钥信息相同则通过认证，密钥信息不同则不通过认证。

EIGRP仅支持MD5认证

**MD5认证：**

设备发送动态路由协议的数据包时只发送接口所有的Key当中KeyID最小的密钥，并且在发送时 携带KeyID

例如

接口当中存在key1 

= ccie key2 

= ccnp. 在发送时仅发送： key1=ccie //由于MD5加密认证，发送时会进行MD5加密

接收方将对方KeyID所对应的密钥与自己密钥库当中相同KeyID的密钥进行比对，如果密钥信息相同，则通过认证。

接收方将对方KeyID所对应的密钥与自己密钥库当中相同KeyID的密钥进行比对，如果密钥信息不同，则不通过认证，不接收消息。

接收方收到了对方的Key时，如果对方的KeyID在自己的密钥库当中不存在，则直接不比对，不接受对方的消息。

**开启EIGRP认证的方式：**

在路由器当中配置密钥库。

```
R2(config)#key chain EIGRP_Key_Store
```

1. 
R2(config-keychain)#key 1 //创建Key1 
R2(config-keychain-key)#key-string cisco //设定密钥为cisco 
R2#show key chain //展示密钥库，哪怕空格也能看出来。 - 路由器的接口下设定EIGRP认证的模式 
R2(config)#interface g0/1 
R2(config-if)#ip authentication mode eigrp 100 md5 //针对于EIGRP100进程开启MD5认证。 - 路由器的接口下设定EIGRP认证使用的密钥库。 
R2(config-if)#ip authentication key-chain eigrp 100 EIGRP_Key_Store //调用EIGRP密钥库。

**修改EIGRP路由条目管理距离的方式：**

使用命令：Distance

使用格式：Distance<管理距离>

使用条件：EIGRP仅能够针对于内部路由修改管理距离，无法针对于外部路由调整管理距离。（但是更改全局可以修改。）

**[代码框内容]**

text

1. R2(config)#ip access-list standard EIGRP_DISTANCE            //创建标准ACL
2. R2(config-std-nacl)#permit 10.10.3.0                        //匹配10.10.3.0的路由
3. R2(config-std-nacl)#exit
4. R2(config)#router eigrp 100
5. R2(config-router)#distance 121 1.1.24.4 0.0.0.0 EIGRP_DISTANCE //针对于1.1.24.4通告的ACL匹配的路由调整管理距离121.
6. R2(config-router)#distance eigrp <internal distance> <external distance> //可以直接修改整个EIGRP进程的内外部路由条目管理距离(非常危险)

**[代码框内容]**

text

1 ip route 0.0.0.0 0.0.0.0 null 0                   //写一条默认路由指向null 0

2 ip prefix-list DEF permit 0.0.0.0/0               //利用前缀列表匹配上默认路由

3 route-map LMAP permit 10                         //创建名为LMAP的route-map指定行为是允许

4 match ip address prefix-list DEF                  //匹配上DEF的前缀列表

5 router eigrp 99

6 redistribute static                              //将静态路由重分布引入到数据库。

7 eigrp stub static leak-map LMAP                  //配置为边界路由器并且仅通告自己的EIGRP数据库中的静态路由，且仅通告Leak-map所匹配允许的静态路由

```
R2#terminal length 0
```

```
R2#show running-config
```

---

# 二、OSPF 专题

> 开放最短路径优先

## Day 12：OSPF引入,OSPF运行方式,分区域设计,选举DR和BDR,Router-ID

链路状态动态路由协议。

距离矢量路由协议存放到数据库中的是路由条目。

链路状态路由协议存放到数据库中的是运行该协议的接口所对应的链路状态信息。（接口地址，链接在哪一个网段，Metric）

Router-ID：路由器的ID号码，类似于“人的姓名”，与IPv4地址格式相同，表现为点分十进制。例如：1.1.1.1 2.2.2.2 3.3.3.3

**自动选举：**

路由器当中没有loopback接口

将会自动选举最大的物理接口IP地址作为OSPF Router-ID

路由器当中有loopback接口

将会选举最大的loopback接口IP地址作为OSPF Router-ID。哪怕Loopback接口没有运行OSPF，依然会选择最大的Loopback接口IP地

址作为Router-ID...

**手动指定：**

```
R1(config)#router ospf 1 
R1(config-router)#router-id 1.1.1.1 router-id x.x.x.x clear ip ospf process
```

**OSPF进程**

OSPF邻居关系将会全部重置，重新建立OSPF邻居。

**OSPF的三张表：**

邻居表：记录了OSPF的邻接关系。以及对方OSPF邻居状态，Router-ID，接口地址，DR/BDR等情况。

```
R3#show ip ospf neighbor
```

数据库表：存放了OSPF路由器的自身以及学习到的所有链路状态信息。

```
R1#show ip ospf database
```

```
R1#show ip ospf database Router
```

**态息。）**

路由表：通过OSPF的数据库条目计算可以得到的路由条目将被提交到路由表中。

**OSPF的运行方式：**

router ospf <process ID>

//创建OSPF进程。

OSPF接口激活方式之集中式宣告

被network命令后续网段匹配的接口地址，该地址对应的接口被激活运行OSPF

被network命令后续网段匹配的接口地址，该地址对应接口的直连路由被存放进入动态路由协议的数据库。

例如：需要激活172.16.12.1/24接口运行OSPF。

正确方式激活： network 172.16.12.0 255.255.255.0 area 0 //哪怕使用正确方式激活也会自动转成反掩码。

反掩码方式激活： network 172.16.12.0 0.0.0.255 area 0

精确方式激活： network 172.16.12.1 0.0.0.0 area 0

//老师个人最喜欢的方案。

以上都是方便理解的方法。

```
R1(config-router)# network <network number> <OSPF wildcard bits> area <area_ID >
```

通配符：帮助匹配前缀地址，使得单句命令行可以同时匹配上多个条目参数。通配符用0来表示前缀地址的对应位置固定，用1表示前缀地址的对应位置可以发生变化。

OSPF接口激活方式之接口下宣告

interface g0/0

ip ospf 1 area 0

ip ospf <process id> area <area_ID>

//直接在接口下运行OSPF进程1，区域0。

//☆☆☆☆☆☆

如果进程中激活接口运行的OSPF区域与接口下激活运行的区域不同，接口下激活运行的区域优先。

**分区域设计**

如果同一区域运行链路状态动态路由协议

数据库太过于庞大，占用设备的大部分资源。

为了保证始终LSDB同步，但凡网络中有某个设备链路状态信息发生了变化，则会全网泛洪，大家一起抖动。

所有设备必须要有详细的链路状态信息才能够算路由，如何汇总减少路由条目呢？

**普通区域**

**非Area0**

Stub Totally Stub

**特殊区域**

NSSA Totally NSSA

每一个区域当中的设备仅与本区域的路由交换链路状态数据库条目信息,仅保证区域内部的设备进行LSDB同步。

可以通过本区域的LSDB同步完成本区域所有路段的路由计算。

引入了ABR(Area Border Router):区域边界路由器 → 至少有一个接口运行在区域0,至少有一个接口运行在非区域0。ABR可能会同时地存放两个及两个以上区域的详细的链路状态数据库条目信息。

ABR可以将非区域0的详细的链路状态信息汇总成摘要的链路状态信息通告到区域0当中去,也可以将区域0当中的详细的链路状态信息通告到非区域0。

引入了ABR之后,每一个区域的路由器仅需要存放本区域详细的链路状态数据库条目以及其它区域的摘要链路状态数据库条目信息。

区域与区域之间互相访问都需要经过ABR。 → 区域与区域之间互相访问都需要经过区域0

每一个区域当中的设备数量不要超过38个。

**OSPF的包类型:**

Hello包:发现,建立,以及维护OSPF邻居关系,只要接口被激活运行了动态路由协议OSPF,则接口将会立刻马上加入到组播地址224.0.0.5,224.0.0.6,所有的路由器都会使用224.0.0.5来发送OSPF的Hello包。

Database Description(简称为DBD包):数据库描述,相当于目录,包含了路由器自己的数据库条目的头部信息。(1)

Link-State Request(简称为LSR包):通过DBD包的交换使得路由器清楚了自己数据库当中所缺少的链路状态信息,则通过LSR向对方请求自己所缺失的数据库条目。

Link-State Update(简称为LSU包):通过LSU将路由器数据库当中的链路状态信息打包发送给邻居,进行数据库条目更新。

Link-State Acknowledgement(简称为LSACK):当收到了邻居的LSU消息数据库通告之后需要做出回应,发送LSACK。

**DR/DBR:**

在多接入(一个链路上多个设备)网络中运行OSPF,会自动选举DR/BDR路由器。

链路上的所有路由器都将只与DR与BDR建立OSPF邻居关系以及交换机链路状态数据库条目。BDR只负责收集全网的链路状态数据库,DR在收集好了链路状态数据库条目之后会负责进行下发,能够减少OSPF邻居关系的数量,加快链路上的LSDB同步的速度。如果DR挂了,可以BDR转为DR接管DR的工作。

DR是路由器接口链路上的角色,不是区域当中的角色。

当链路上所有的路由器都与DR和BDR建立邻居关系之后,其它路由器都为Dother。

## Day 13：OSPF建邻居的过程,OSPF的DR&BDR选举方式,影响OSPF建立邻居的条件(上)

OSPF的包类型：Hello包：发现，建立，以及维护OSPF邻居关系，只要接口被激活运行了动态路由协议OSPF，则接口将会立刻马上加入到组播地址224.0.0.5，224.0.0.6，所有的路由器都会使用224.0.0.5来发送OSPF的Hello包。

OSPFhello包周期时间默认每隔10s发送一次Hello包，如果超过dead时间40s收不到对方发送的Hello包则认为对方出现故障。

Hello包都发送在224.0.0.5interface XXXip ospf hello-interval //调整接口发送Hello包的周期时间如果调整了hello-interval，则dead-interval会自动变成hello-interval的四倍。

ip ospf dead-interval //调整接口dead-interval时间。

如果只调hold时间则hello时间不被影响（Database Description（简称为DBD包）：数据库描述，相当于目录，包含了路由器自己的数据库条目的头部信息。（可以用来选举主从关系。

）Link-State Request（简称为LSR包）：通过DBD包的交换使得路由器清楚了自己数据库当中所缺少的链路状态信息，则通过LSR向对方请求自己所缺失的数据库条目。

Link-State Update（简称为LSU包）：通过LSU将路由器数据库当中的链路状态信息打包发送给邻居，进行数据库条目更新。

Link-State Acknowledgement（简称为LSACK）：当收到了邻居的LSU消息数据库通告之后需要做出回应，发送LSACK。

OSPF建立邻居关系的过程

debug ip ospf adj

//通过该命令可以查看OSPF邻居关系的变化过程。

Down：没有运行OSPF，没有收到任何的OSPF数据包。

Init：当两个设备激活接口运行OSPF时开始发送第一个Hello包，此时互相之间不认识，当路由器收到了对方Hello包时，并且发现对方的Hello包当中没有active neighbor字段，没有自己的Router-ID，则认识了该新的邻居，后续通过在Active neighbor当中填写对方的Router-ID，表示想要与对方互相之间认识，只要路由器收到了第一个对方发送的包含active neighbor router-id为自己的Hello包时，则立刻向对方单播回复一个Hello包并在active neighbor当中填写对方的Router-ID，表示同意与对方互相结识，互相在active neighbor当中填写上对方的Router-ID。（只要双方的Hello包当中active neighbor字段都有对方的Router-ID）则正式转为Two-way状态。

Two-WAY：当路由器双方进入Two-way状态，路由器将会在链路当中开始选举DR/BDR。如果不需要选举DR/BDR则可以跳过Two-way状态。

EXSTART：双方交换第一个DBD消息，该DBD消息当中不包含数据库条目的头部信息，主要的目的是选举主（master）从（slave）关系[比较路由器的OSPF Router-ID，Router-ID大的路由器将会成为主，Router-ID小的将会成为从]，选举主从之后所有的slave路由器都将会与master路由器的序列号同步，以保证后续的数据同步准确

EXCHANGE：双方交换第二个DBD消息，该DBD消息正式地包含了数据库的头部信息，当双方的DBD消息当中的more bit = 0 表示双方的数据库头部交换完成，没有更多的DBD消息需要交换机，则双方转入loading状态。

LOADING：路由器发送LSR消息请求自己的数据库当中所缺少的对方的数据库条目详细信息，当路由器收到了LSR之后将会把数据库详细的链路状态信息存放到LSU消息发送给对方链路状态更新，双方互相之间交换各自的链路状态数据库条目，当收到了对方的LSU消息之后会发送LSACK消息进行回复，表示对方的LSU已经收到了。路由器把收到了链路状态信息加载到自己的数据库并计算路由。

FULL：邻居关系建立成功。

**DR/BRD:**

在多接入（一个链路上多个设备）网络中运行OSPF，会自动选举DR/BRD路由器。

链路上的所有路由器都将只与DR与BDR建立OSPF邻居关系以及交换机链路状态数据库条目。BDR只负责收集全网的链路状态数据库，DR在收集好了链路状态数据库条目之后会负责进行下发，能够减少OSPF邻居关系的数量，加快链路上的LSDB同步的速度。如果DR挂了，可以BDR转为DR接替DR的工作。

DR是路由器接口链路上的角色，不是区域当中的角色。

当链路上所有的路由器都与DR和BDR建立邻居关系之后，其它路由器都为Dother。

减少邻居关系数量，加快LSDB同步

**如何选举DR/BRD**

DR Priority:DR的优先级（默认是1级）

```
R5(config)#interface g0/1
R5(config-if)#ip ospf priority ?
```

优先级。

<0-255> Priority

如果优先级设置为0则表示本路由器接口不参与DR/BRD的选举。

优先级越大越优先。

Router-ID最大的路由器成为DR。

show ip ospf interface brief OSPF哪个接口以及角色。

show ip ospf interface 的详细情况。

情况。

在DSPF当中，DR和BDR的角色不可抢占，哪怕将路由器的优先级调再大也抢夺不了DR和BDR的角色，只有DR或BDR断开OSPF邻居主动卸任，才会空出DR和BDR的位置

如果DR出现故障则BDR直接转正成为新的DR

当路由器之间的邻居关系进入Two-way状态下时将会选举DR/ BDR。

此时路由器发送的Hello包当中DR和BDR的地址都为0.0.0.0。

此时所有的路由器都将会在网络当中等待DR和BDR发消息，等待的时间wait=dead-interval=40s，如果等待了wait时长没有DR和BDR发送Hello包。则认为该链路上没有DR和BDR，才会进入到DR和BDR的选举。如果路由器在wait时间当中收到了DR/BDR发送的hello包，发现网络中有DR/BDR，则直接跳过Two-way状态，直接跟DR和BDR建立邻居关系并交换数据库。

先选举BDR，让BDR转为DR。

再选举新的BDR。

所有的路由器与DR和BDR建立邻居。

DRother之间保持为Two-way状态

DRother发送LSU给组播地址224.0.0.6. 将链路状态数据库条目上传给DR/BDR。DR收到了DRother的LSU消息之后回复LSACK也发送给224.0.0.6。

（DRother与DR，BDR之间交换数据库条目使用组播地址224.0.0.6） DRother上传信息给DR使用224.0.0.6

DR发送收集好的链路状态数据库条目信息给DRother时使用组播地址224.0.0.5。

（DR发送LSU给Dother使用组播地址224.0.0.5） DR下发信息给BDR使用224.0.0.5

影响到OSPF建立邻居的条件

Router-ID要求全网唯一。

Hello-interval需要一致。

Dead-interval需要一致。 特殊情况：ip ospf dead-interval minimal hello-multiplier XX //将接口的dead时间设置为1s并且该时间hello时间的X倍

因为Hello包当中Hello-Interval字段以秒为单位，并且需要取整，当时间小于1s时直接设置为0。

## Day 14：OSPF建立邻居的条件,OSPF的网络类型

影响到OSPF建立邻居的条件

Router-1D要求全网唯一。

Hello-interval需要一致。

Dead-interval需要一致。 特殊情况:ip ospf dead-interval minimal hello-multiplier XX //将接口的dead时间设置为1s并且该时间hello时间的X倍

因为Hello包当中Hello-interval字段以秒为单位，并且需要取整，当时间小于1s时直接设置为0。

Area-ID需要保证一致。

OSPF的stub标识和nssa标识保证一致（特殊区域标识）

MTU需要保持一致（MTU不一致则双方会卡在Exstart状态）

在比较第一个DBD消息选举主从关系时会比较MTU大小。如果不一致则无法进入到exchange继续交换数据库头部。

MA网络环境（路由器接口的网络类型为Broadcast[广播]） ==> 需要选举R/BR的网络环境下要求掩码一致。

OSPF认证通过。

OSPF的版本号一致。

OSPF网络类型。

可以根据不同的链路类型来挑选和使用OSPF的网络类型。根据需求而选择使用自己所需要的OSPF网络类型，没有固定的组合。

默认情况下，OSPF将会根据路由器接口的数据链路层链路类型而自动选举对应的网络类型。

记住不同网络类型下OSPF工作的特点

show ip ospf interface

//查看OSPF接口的详细情况

RX(config)#interface xxx

RX(config-if)#ip ospf network ?

broadcast Specify OSPF broadcast multi-access network

non-broadcast Specify OSPF NBMA network

point-to-multipoint Specify OSPF point-to-multipoint network

point-to-point Specify OSPF point-to-point network

默认情况下，只要路由器的接口是FID（180Mbps），6口（180Mbps），等号以太网接口，默认情况下接口的OSPF网络类型为Broadcast

默认情况下，只要路由器的接口是S口，点到点的链路封装，OSPF网络类型默认是Point-to-Point

<table>OSPF网络类型二层链路类型Hello/DeadDR/DBR手动邻居/32路由POINT-TO-POINTHDLC、PPP、FR点对点子接口10/40NONONOBROADCAST以太网、令牌环网、FDDI10/40YesNONONBMA（单播）FR网络、FR多点子接口、X.25、ATM30/120YesYesNO点到多点（组播交互）没有默认二层的链路类型（工程中Hub-spoke）30/120NONOYes点到多点非广播（单播）CISCO私有（若工程中不支持组播）30/120NOYesYesLoopbackLoopbackTreat as host</table>

Point-to-Point：不用选举DR/BRD 默认Hello时间10s，dead时间40s 接口对端只能建立一个OSPF邻居，如果有多个邻居将会删动，使用组播建立邻居。

点到点网络类型说明路由器的接口对端只有一个设备，没有多台邻居，不需要选举DR/BRD减少邻居的数量并加快数据库同步。

Broadcast：需要选举DR/BRD 默认Hello时间10s，dead时间40s接口可以和多个设备建立邻居关系

广播的网络类型说明路由器的接口可能接入在一个多设备的网络，可能与多个设备建立邻居关系，默认接口需要选举DR/BRD，并跟DR/BRD建立邻居关系。

non-broadcast：接口不通过组播的方式建立OSPF邻居关系，通过单播的方式建立邻居，需要手动指定OSPF的邻居IP地址，hello时间30s，dead时间120s，会选择DR/BRD。可以跟多个设备起邻居 使用单播建立邻居。所有信息使用单播交互。

interface g0/0

ip ospf network non-broadcast

router ospf 1

neighbor 1.1.123.2

Point-to-multipoint：接口可以跟多个设备起邻居，但是可以不选举DR/BRD，Hello时间30s，dead时间120。但是会产生/32掩码的邻居地址路由条目。其它的路由不受影响，使用组播

Point-to-multipoint non-broadcast：接口可以跟多个设备其邻居，不用选举DR/BRD，Hello时间30s，dead时间120，需要手工指定单播邻居地址，通过单播与对方建立邻居关系单播

网络类型不影响OSPF邻居关系的建立，不同网络类型带来的Hello时间和dead时间不同才是影响到建立OSPF邻居关系的因素。

网络类型不同能够建立邻居，但是不同网络类型可能会影响到路由器条目计算。

p2p（不选DR/BDR）- broadcast（选DR/BDR） 没有路由p2p（不选DR/BDR）- p2mp（不选DR/BDR） 有路由nbma（选DR/BDR）- broadcast（选DR/BDR） 有路由nvma（选DR/BDR）- p2mp nbma（不选DR/BDR） 没有路由

都选举DR/BDR的网络类型路由器之间建立邻居关系可以计算路由器条目，都不选DR/BDR的网络类型路由器之间建立邻居关系可以计算路由器- 选举DR/BDR的网络类型和不选举DR/BDR的网络类型之间建立邻居关系则不能够计算路由器。

**链路状态信息当中LSA的链路类型：**

如果该接口没有建立OSPF邻居关系，则该接口的链路状态信息的链路类型为Stub network。

如果该接口建立了OSPF邻居关系，则该接口的链路状态信息的链路类型为Transit network。

## Day 15-16：OSPF的LSA格式,LSA的比较,LSA的类型,LSA的作用详解

1.1.1.1.1.1.1.1.1.1.1

LSA(Link-state advertisement):链路状态通告(路由器的链路状态信息。)

ABR(Area Border Router):区域边界路由器(路由器至少有一个接口运行在区域0,有一个接口运行在非区域0)

<table>LSA NumberLSA TypeLSA Link type1 Type LSA路由器的链路状态信息通告Router2 Type LSA由DR通告的LSANet3 Type LSA由ABR通告的LSA(区域之间的链路状态信息)Summary4 Type LSA由ABR通告的LSA(通告ASBR的位置)ASBR-Summary5 Type LSA由ASBR通告(外部路由的LSA)External7 Type LSA由NSSA/Totally NSSA特殊区域当中ASBR引入的LSA(特殊区域中外部路由的LSA)</table>

> 图片内容识别

LSA | Link-id | ADV-Router | Content | Area

1(P2P) | Route-id | Route-id | neighbor-id ; prefix/mask ; ip address ; metric | Intra-area

1(MA) | Route-id | Route-id | DR-address ; ip address ; metric no mask | Intra-area

2 | DR的地址 | DR-Route-id | mask ; attach neighbor | Intra-area

3 | 区域间路由 | ABR-Route-id | prefix/mask ; metric | Inter-area

4 | ASBR-Route-id | ABR-Route-id | metric | Intra-area

5 | 外部路由 | ASBR-Route-id | prefix/mask ; metric-type ; metric ; FA | All-area

show ip ospf database //查看OSPF数据库目录。

一类二类LSA能够计算得出本区域内部的路由条目,其产生的路由标识为0路由

三类LSA能够计算得出区域之间的路由条目

四类和五类LSA能够计算得出外部路由条目。

**其产生的路由标识为0路由**

Metric-type=1的五类LSA计算得出0E1路由;Metric-type=2的五类LSA计算得出0E2路由。

1- Type LSA.

show ip ospf database Router

//查看路由器的类LSA。

> 图片内容识别

LS age: 165 //寿命

(0-3600)

Options: (No TOS-capability, DC) //特性

LS Type: Router Links //标识

LSA link type

Link State ID: 1.1.1.1 //关于哪种类型的LSA。(由1.1.1.1通告关于router-id为1.1.1.1的路由器所对应的它的链路状态情况。)

Advertising Router: 1.1.1.1 //标识由谁通告的LSA。

LS Seq Number: 80000009 //LSA的序列号。(判断LSA的新旧,避免重复)

Checksum: 0x905F //校验位。

Length: 48 //LSA的长度

Number of Links: 2 //通告了几条链路的LSA。

Link connected to: a Stub Network

(Link ID) Network/subnet number: 10.18.1.1

(Link Data) Network Mask: 255.255.255.255

Number of MTID metrics: 0

TOS 0 Metrics: 1

Link connected to: a Transit Network

(Link ID) Designated Router address: 1.1.123.3 //该链路上DR的接口地址

(Link Data) Router Interface address: 1.1.123.1 //本路由器的1.1.123.1 接口地址链接在一条链路

Number of MTID metrics: 0 //Metric

TOS 0 Metrics: 1

19 (Link Data) Router Interface address: 1.1.123.1 //本路由器的1.1.123.1 接口地址链接在一条链路 20 Number of MTID metrics: 0 //Metri 21 TOS 0 Metrics: 1

**LSA的序列号：**

范围0x80000000 0x7FFFFFFF

**//LSA的范围.**

1000 0000 0000 0000 0000 0000 0000 0000 / 0111 1111 1111 1111 1111 1111 1111 1111

**1表示（- 号）**

**0表示（+号）**

//第一位不要看..雨管他.

**序列号越大约优异.**

路由器如何选举最优的LSA存放到数据库.

比较LSA的序列号，大的优先.

**比较校验位，大的优先.**

如果收到一条相同的LSA，且该LSA的老化时间为3600s，则选举它作为最优的LSA替换存放到数据库。（如果路由器收到了LSAage=3600s，则知道LSA已经不可用，需要老化，则直接将其作为最优的LSA存放到数据库。并最终将该数据库条目删除。）

如果两条相同内容的LSA其老化时间差距大于15分钟，则选举老化时间比较小的。

如果以上四条都比较不出，则认为两条LSA相同。

次.

OSPF既是触发更新，也是周期更新

EIGRP和BGP都是触发更新.

在OSPF的网络类型为Broadcast的情况下，必须使用一类和二类LSA才能够计算得出本区域当中的路由。

**LSA由谁通告**

**LSA通告的范围.**

**·如何算路由.**

一类LSA由路由器自己进行通告，通告关于自己的链路状态信息。

在本区域当中传递，本区域的所有路由器都能够看到全部区域设备的一类LSA。

**·LSA由谁通告**

**·LSA通告的范围.**

一类LSA由路由器自己进行通告，通告关于自己的链路状态信息。

在本区域当中传递，本区域的所有路由器都能够看到全部区域设备的一类LSA。

将会通告路由器链路的接口地址，链路上DR的地址，以及链路上的Metric.

没有链路的掩码

**二类LSA**

show ip ospf database network

**类LSA.**

//查看本区域的所有链路上DR通告的二

**类LSA.**

LSA age: 1090

Options: (No TOS-capability, DC)

LSA Type: Network Links

Link State ID: 1.1.123.3 (address of Designated Router)

对应链路上的情况.

Advertising Router: 3.3.3.3

LSA Seq Number: 80000002

Checksum: 6x2887

Length: 36

Network Mask: /27

Attached Router: 3.3.3.3

Attached Router: 1.1.1.1

Attached Router: 2.2.2.2

ID.

二类LSA是由本区域的DR进行通告，通告DR接口链路上的掩码以及链路上的成员Router-ID

在本区域当中传递，本区域的所有路由器都能够看到全部区域设备链路上的DR以及链路的掩码情况。

P2P网络类型的情况下，只需要一类LSA即可计算路由。

一类LSA由路由器自己通告，将会通告接口链路的地址，掩码，以及对端设备的Router-ID.

在本区域当中传递.

**三类LSA**

由ABR通告，直接通告区域之间的路由条目网络号+掩码，将路由条目在区域与区域之间通告。

·ABR可以将非区域0的一类、二类LSA，转化到区域0当中通告三类LSA.

通过以上两步可以解决区域0和非区域0之间互访的问题。

ABR可以将区域0的三类LSA通告的非区域0产生三类LSA。

ABR可以将区域0的三类LSA通告的非区域0产生三类LSA。

通过以上这一步可以解决非区域0与非区域0之间的互相访问。

ABR不会将非区域0的三类LSA再转换到区域0。（所有的非区域0的三类LSA都来自于区域0。）

ABR不会把非区域0已有一类二类LSA所对应的三类LSA条目再从区域0引入到非区域0。

**OSPF算路由：**

当路由器通过LSDB画出网络拓扑之后，将会计算每一个去往目的网段的Metric之和，最小的最优。

**Metric计算：**

计算本路由器去往目的网段的 出方向 链路Metric之和。 = 本路由器去往目的网段出方向的接口COST之和。

Metric = 接口的cost = OSPF的参考带宽（10bps = 100Mbps） + 路由器的接口带宽

参考带宽：auto-cost reference-bandwidth 100

**如何调整接口的COST：**

调整OSPF的参考带宽（很少用）

接口下直接使用“ip ospf cost <cost_value>” //使用该命令直接调整接口的COST

```
R1(config)#int g0/0
```

```
R1(config-if)#ip ospf cost 10000
```

**五类LSA**

**重分布：**

可以把其它协议的路由条目以外部路由的形式引入到本动态路由协议。

只有提交到路由表的数据库条目能够被重分布引入本动态路由协议

重分布需要讲究一个入向随俗。

router ospf 1

redistribute <type> subnets

//subnets必须添加。

```
R5#show ip ospf database external
```

OSPF Router with ID (5.5.5.5) (Process ID 1)

Type-5 AS External Link States

LS age: 219 Options: (No TOS-capability, DC, Upward) LS Type: AS External Link LS Link State ID: 100.1.1.0 (External Network Number) Advertising Router: 5.5.5.5 LS Seq Number: 80000001 Checksum: 0x2105 Length: 36 Network Mask: /24 Metric Type: 2 (Larger than any Link state path) MTID: 0 Metric: 20 Forward Address: 0.0.0.0 External Route Tag: 0

当重分布引入数据库条目进入OSPF时，OSPF默认会给这些外部路由条目种子Metric=20

OSPF引入的的五类LSA有两种Metric-Type，默认情况下OSPF会以Metric-type=2引入外部路由。

Metric-type=2，种子Metric默认为20，路由器针对于Metric-type=2的五类LSA计算得出的路由条目直接提交种子metric到路由表。

Metric-type=1，种子Metric默认为20，路由器针对于Metric-type=1的五类LSA计算得出的路由条目需要提交种子Metric+Forward-Metric

当五类LSA的Forward-address=0.0.0.0的情况是，Forward-Metric=本路由器去往ASBR的开销。

ASBR（自治系统边界路由器）：在OSPF里重分布引入五类LSA（外部路由）的路由器就是ASBR。

五类LSA由ASBR通告，可以在整个OSPF的网络传递，并且传递的过程当中ADV Router-ID不会发生变化，所有的路由器都将会知道该五类LSA是由谁引入的。

```
R5(config-router)#redistribute <type> subnets metric-type 1
```

> 💡 通过此命令可以将引入的五类LSA改为Metric-

由ABR通告，通告关于ASBR的位置，以及去往ASBR的Metric。

**解决非区域0未接壤区域0的方法：**

**方法一：魔道修法**

使用GRE隧道。

> 图片内容识别

**R2:**

interface Tunnel0

ip address 172.16.12.1 255.255.255.0 //指定隧道的IP地址。

tunnel source 1.1.24.2 //指定隧道源地址

tunnel destination 1.1.24.4 //指定隧道目的地址

ip ospf 1 area 0

**R4:**

interface Tunnel0

ip address 172.16.12.2 255.255.255.0

tunnel source 1.1.24.4

tunnel destination 1.1.24.2

ip ospf 1 area 0

R2 Tunnel口被激活运行OSPF,则将会

[(172.16.12.1 ---> 224.0.0.5 ospf Hello包。

1.1.24.2 ---> 1.1.24.4 )]

通过Tunnel建立起来的OSPF邻居关系默认是P2P网络类型,且Tunnel口的OSPF COST = 1000。

**方法二：正典 *******

**OSPF虚链路.**

> 图片内容识别

router ospf 1

area <area_ID> virtual-link <router-id>

跨越的区域 对方的Router-ID

本路由器需要跨过那一个区域与对方(router-id)建立起OSPF

路由器上会自动创建一个虚拟接口 OSPF_VL0接口,如果多个虚链

只能够跨越一个区域使用

不能够跨越特殊区域建立虚链路

**不能跨越区域0建立虚链路**

OSPF的路由条目过滤：邓典

使用工具：distribute-list

使用场景：仅限于入方向或本地重分布引入OSPF基于协议的过滤。

Distribute-list在距离矢量动态路由协议当中常常使用，主要用于过滤路由条目。

但是，OSPF通告的是LSA（链路状态信息）

Distribute-list在OSPF的入方向调用，意思是，当把数据库的条目计算得出路由，准备将路由提交到路由表时，进行过滤。

> 图片内容识别

router ospf 1

router-id 1.1.1.1

distribute-list 1 in

access-list 1 deny 10.10.5.0

access-list 1 permit any

当把LSA计算得出路由提交到路由表时,利用分发列表调用ACL做过滤,针对于10.10.5.0路由过滤掉,其它路由允许提交到路由表。

## Day 17：OSPF的汇总,OSPF LSA过滤

被汇总的类一类的LSA所在区域 汇总之后的类LSA的网络号和掩码

谁引入的LSA,让谁去做汇总。

**域间汇总:**

进行三类LSA的汇总。

当ABR将区域的一类二类LSA转换为三类LSA时才能够做汇总。.针对于三类LSA通告到其它区域时不能够进行汇总。

可以在ABR上做。

router ospf <process_ID>

area <area_ID> range <network number> <mask> //在ABR上做域间汇总

被汇总的一类二类LSA所在区域 汇总之后的类LSA的网络号和掩码

被汇总路由所包含的明细路由将会被抑制 一 抑制明细。只有至少存在一条明细路由,汇总才能够存在。路由器会自动产生一条指向null0的防环路由。

```
R2(config-router)#no discard-route internal
```

```
R1(config-router)#no discard-route external
```

**某种意义上的LSA过滤**

告,相当于过滤。

**域外汇总:**

进行五类LSA的汇总。

当ASBR将外部路由以五类LSA的方式引入到OSPF时才能够做汇总。

只能够在ASBR上做。

router ospf <process_ID>

summary-address <network number> <mask>

**某种意义上的LSA过滤**

summary-address <network number> <mask> not-advertise

当于过滤。

**OSPF的LSA过滤**

OSPF的三类LSA的过滤。

前缀列表: ip prefix-list permit/deny a.b.c.d/length ge X le Y

网络号/前面多少bit固定 掩码最小长度 掩码最大长度Y

如果不写ge,则ge=length

如果不写le,则le=32

如果不写ge,le,则ge=le=length。

ip prefix-list Test seq 5 deny 100.1.2.0/24

ip prefix-list Test seq 10 deny 100.1.3.0/24

ip prefix-list Test seq 15 permit 0.0.0.0/0 le 32

router ospf 1

area 2 filter-list prefix Test out

三类LSA时,调用前缀列表做过滤

ip prefix-list Test seq 5 deny 100.1.2.0/24

ip prefix-list Test seq 10 deny 100.1.3.0/24

ip prefix-list Test seq 15 permit 0.0.0.0/0 le 32

router ospf 1

area 0 filter-list prefix Test in

LSA时,调用前缀列表做过滤。

area <area_ID> filter-list prefix <word> out

过滤

area <area_ID> filter-list prefix <word> in

过滤。

//禁止100.1.2.0/24

//禁止100.1.3.0/24

//放行其它的全部所有路由

//将区域2的一类二类LSA通告到其它区域的

//禁止100.1.2.0/24

//禁止100.1.3.0/24

//放行其它的全部所有路由

//将其它区域的LSA引入到区域0产生三类

//将其它区域的LSA引入到区域0产生三类

帮我识别每个PDF中的文字。所有文字都要识别输出，不要省略。不要总结。按照day日期大小进行排序

## Day 18-19：OSPF通告默认路由的方式,OSPF选路(上)(下),OSPF特殊区域

OSPF通告默认路由。

OSPF下发的默认路由五类LSA会自带一个Tag值，Tag等于ASBR的OSPF进程ID。例如ASBR上使用的是router ospf 15，则下发的5类LSA会携带tag=15。路由器将会以五类LSA的方式向整个OSPF网络下发该默认路由。默认Metric-type 

2

=2 ，默认的种子Metric=1

有条件地注入默认路由

默认情况下，有条件注入默认路由的条件是：路由器路由表中需要有一条默认路由（任何协议的都可以）

```
R5(config)#router ospf 1
```

```
R5(config-router)#default-information originate
```

> 💡 有条件下发默认路由

```
R5(config-router)#default-information originate ? metric OSPF default metric metric-type OSPF metric type for default routes type,默认是2. route-map Route-map reference <cr>
```

**手工指定条件：**

路由器表中需要存在“某一条路由（自己指定）”，只要该路由存在，则可以下发默认路由

ip prefix-list DEF seq 5 permit 1.1.56.0/24 1.1.56.0/24 route-map DEF permit 10 行为是允许/匹配 match ip address prefix-list DEF router ospf 1 default-information originate route-map DEF 发默认路由。

//利用前缀列表匹配上 //创建名为DEF的route-map设定 //抓取出前缀列表匹配的路由 //当满足route-map的条件时下

**无条件地注入默认路由**

```
R5(config)#router ospf 1
```

```
R5(config-router)#default-information originate always
```

**OSPF的选路方式**

**0路由的选路**

通过相同区域的一类二类LSA计算得出相同的0路由。

先比较路由条目的Metric值，小的优先，如果Metric值相同，则等价负载。

通过不同区域的一类二类LSA计算得出的相同0路由

先比较路由条目的Metric值，小的优先，如果Metric值相同，则优选区域ID比较大的路由。

**0IA路由的选路**

0路由永远优先于0IA路由，不考虑Metric值大小。 0>0IA。

当通过不同区域的三类LSA计算得出相同的0IA路由时

当没有区域0的三类LSA时，先比较路由条目的Metric值，小的优先，Metric值相同，则等价负载。

**先。）**

当有区域0的三类LSA时，优先选择区域0的三类LSA，不考虑Metric。（所有非区域0的三类LSA都来自于区域0。区域0的三类LSA绝对优

**0E路由选路**

0IA路由永远优先于0E路由，不考虑Metric大小。 0IA 

>

> 0E

Metric-Type 

1

=1 >Metric 

2

=2 ，0E1 

>

> 0E2

**0E2路由的选路**

当存在两条5类LSA计算得出的相同0E2路由时，先比较种子Metric，小的优先。

种子Metric相同，则比较Forward-Metric，小的优先。Forward-metric相同，则等价负载。

当Forward-address 

0.0.0.0

=0.0.0.0 时，Forward-metric 

= 本路由器去往ASBR的Metric。

0E2路由只是提交5类LSA到路由表时直接提交种子Metric，但并不代表不计算。

**0E1路由的选路**

当存在两条五类LSA计算得出的相同0E1路由时，直接比较总Metric，总Metric小的优先，如果总Metric相同，则等价负载。

减少区域内部的LSA条目且不影响外部的访问。

Stub

Stub区域可以阻止其它区域的四类/五类LSA进入到stub特殊区域。ABR将会作为门神将其它区域四类/五类LSA隔离在外。

```
R1(config)#router ospf 1
```

```
R1(config-router)#area 2 stub
```

> 💡 将区域2配置为特殊区域stub。

设备会将运行在区域2当中的接口发送的Hello包当中external routing字段变为0，表示本区域不支持外部路由。

如果需要将一个区域配置为特殊区域，整个区域的所有设备都需要配置，否则邻居无法建立。

ABR在过滤四类五类LSA的同时会下发一条三类LSA的默认路由进入stub特殊区域以作代替，默认的初始Metric=1。

```
R2(config)#router ospf 1
```

```
R2(config-router)#area 2 default-cost 28
```

> 💡 调整ABR下发到stub的默认路由初始

Metric

stub区域不能够引入四类五类LSA，不可以存在ASBR。

area 8不能够成为stub特殊区域。

虚链路所在的区域也不可以成为stub特殊区域。

totally Stub

在原有stub特殊区域过滤四类/五类LSA的基础之上，再一次能够过滤掉三类LSA。其它区域的三类LSA也不能够进入到Totally Stub。

**只需要在ABR上做：**

```
R2(config)#router ospf 1
```

```
R2(config-router)#area 2 stub no-summary
```

> 💡 不要向区域2注入三类LSA。

同样，ABR会下发一条三类LSA的默认路由进入Totally stub特殊区域，默认初始Metric=1。

NSSA(not-so-stubby-area)

nssa特殊区域可以阻止其它区域的四类/五类LSA进入到nssa特殊区域。ABR将会作为门神将其它区域四类/五类LSA隔离在外。

但是NSSA区域中 可以存在ASBR，可以重分布 引入外部路由

```
R1(config)#router ospf 1
```

```
R1(config-router)#area 2 nssa
```

> 💡 将区域2配置为特殊区域nssa。

设备会将运行在区域2当中的所有接口发送的hello包当中NSSA字段置为1，表示本区域是nssa特殊区域。

如果需要将一个区域配置为特殊区域，整个区域的所有设备都需要配置，否则邻居无法建立。

NSSA特殊区域，ABR不会自动向区域当中注入默认路由。如果需要注入默认路由，可以在ABR上做：

```
R2(config)#router ospf 1
```

```
R2(config-router)#area 2 nssa default-information-originate
```

引入的7类LSA与五类LSA相同，种子metric=20，默认Metric-type=2。

```
R2(config-router)#area 2 nssa default-information-originate ?
```

metric OSPF default metric

metric-type OSPF metric type for default routes

Metric-type

```
R2#show ip ospf database nssa-external
```

Metric-type=1 的7类LSA计算得出的为0N1路由。

Metric-type=2 的7类LSA计算得出的为0N2路由。

只有NSSA特殊区域中才能够存在7类LSA。

当NSSA特殊区域的7类LSA需要向普通区域传递时，ABR将会把7类LSA转换成为五类LSA通告到普通区域。ABR将会成为普通区域中的ASBR，因为它引入了五类

LSA.

ABR在七转五的时候，LSA当中的参数都不会更改。

如果有多个ABR，则只有Router-id较大的路由器会做7转5。

Totally NSSA

在原有NSSA特殊区域过滤四类/五类LSA的基础之上，再一次能够过滤掉三类LSA。其它区域的三类LSA也不能够进入到Totally NSSA。

Totally NSSA也可以存在ASBR。引入的外部路由以7类LSA存在。

**只需要在ABR上做：**

```
R2(config)#router ospf 1
```

```
R2(config-router)#area 2 nssa no-summary
```

> 💡 ABR不向区域2注入三类LSA。

Totally NSSA区域中，ABR可以自动注入默认路由，以三类LSA的方式进行，默认的初始Metric=1。

```
R2(config)#router ospf 1
```

## Day 20：OSPF的FA地址规则,OSPF的ON路由选路方式

当Forward-address = 0.0.0.0时,Forward-Metric = 本路由器去往ASBR Router-ID的Metric。当Forward-address 不为0时,Forward-metric = 本路由器去往Forward-address的Metric。Forward-address真正指明引入外部路由的路由器是谁。

**ON路由的选路方式**

**ON2路由的选路**

与OE2路由的比较相同，先比较种子Metric，小的优先，种子metric相同，则比较Forward-metric，小的优先，如果Forward-metric相同，则等价负载。

**ON1路由的选路**

与OE1路由比较相同，直接比较总Metric，总metric小的优先，如果总Metric相同，则等价负载。

OE1路由VS ON1路由 小心bug V10S≤16.2 100%触发。

比较总Metric值，小的优先，如果总Metric相同，OE1>ON1

OE2路由VS ON2路由 小心bug

先比较种子Metric值，小的优先，种子Metric相同则比较Forward-metric，小的优先，如果Forward-metric相同，则OE2>ON2。

OE1路由 VS ON2路由

优选OE1路由，Metric-type=1的LSA永远优先于Metric-type=2的LSA，不考虑种子Metric和Forward-metric

OE2路由VS ON1路由

优选ON1路由，Metric-type=1的LSA永远优先于Metric-type=2的LSA，不考虑种子Metric和Forward-metric

整个OSPF的选路可以总结为 

0

>

0

0>0 IA>OE>ON，但是OE和ON有特殊情况，Metric-type=1>Metric-type=2

Forward-address 地址的规则。

在NSSA特殊区域重分布直连路由进入OSPF：

当路由器有Loopback接口运行OSPF

最早运行OSPF的Loopback接口地址将会成为Forward-address。

show ip ospf interface brief

//loopback接口会按照运行顺序从旧到新排列。

当路由器没有Loopback接口运行OSPF

最新运行OSPF的物理接口地址将会成为Forward-address。

show ip ospf interface brief

//物理接口会按照运行顺序从新到旧排列。

在NSSA特殊区域重分布其它协议路由进入OSPF：

如果运行其它协议的路由器接口并没有运行OSPF

结果与上方一致

如果运行其它协议的路由器接口也运行了OSPF

Forward-address = 被重分布协议的路由条目下一跳地址。

在普通区域重分布数据库条目进入OSPF时

重分布的直连路由，另一个协议的路由进入到OSPF并且运行其它协议的接口没有运行OSPF时

Forward-address = 0.0.0.0

重分布其它协议路由条目进入OSPF，并且运行该其它协议的接口同样运行了OSPF。

Forward-address = 被重分布协议的路由条目下一跳地址。

如果一台路由器既运行在普通区域也运行在NSSA特殊区域，则按照普通区域看待

## Day 21-22：OSPF的FA地址规则,OSPF的ON路由选路方式

利用tag值针对于路由条目做过滤

summary-address 100.1.0.0 255.255.252.0 tag 2

route-map killtag2 deny 10

**句并指定行为deny.**

match tag 2

route-map killtag2 permit 20

放行其它所有路由

router ospf 1

distribute-list route-map killtag2 in

**OSPF的认证:**

**明文认证**

路由器之间的认证信息使用明文交互

**接口下开启OSPF认证**

在路由器的接口下配置明文密钥,接口下开启认证.

```
R4(config)#interface g0/1
```

```
R4(config-if)#ip ospf authentication-key cisco123
```

```
R4(config-if)#ip ospf authentication
```

```
R4(config)#router ospf 1
```

```
R4(config-router)#area 1 virtual-link 10.10.2.2 authentication-key cisco123 //虚链路接口配置认证密钥
```

```
R4(config-router)#area 1 virtual-link 10.10.2.2 authentication
```

**OSPF区域认证**

在路由器的接口下配置明文密钥,在进程下针对于区域开启认证.

```
R4(config)#interface g0/1
```

```
R4(config-if)#ip ospf authentication-key cisco123
```

```
R4(config)#router ospf 1
```

```
R4(config-router)#area 1 virtual-link 10.10.2.2 authentication-key cisco123 //虚链路接口配置认证密钥
```

```
R4(config-router)#area 0 authentication
```

本路由器所有运行在区域0的接口都会自动开启明文认证.

**加密认证**

路由器之间的认证信息使用加密交互

**MD5加密.**

**接口下开启OSPF认证**

在路由器的接口下配置MD5密钥,接口下开启认证.

```
R4(config)#interface g0/1
```

```
R4(config-if)#ip ospf message-digest-key 1 md5 cisco123
```

```
R4(config-if)#ip ospf authentication message-digest
```

```
R4(config)#router ospf 1
```

```
R4(config-router)#area 1 virtual-link 10.10.2.2 message-digest-key 1 md5 cisco123 //虚链路接口配置MD5加
```

密钥

```
R4(config-router)#area 1 virtual-link 10.10.2.2 authentication message-digest
```

**密认证.**

接口下使用非原生的MD5加密认证

```
R4(config)#key chain OSPF_AUTHER_N_STORE
```

```
R4(config-keychain)#key 1
```

```
R4(config-keychain-key)#key-string cci3
```

```
R4(config-keychain-key)#cryptographic-algorithm hmac-sha-384
```

```
R4(config)#interface g0/1
```

```
R4(config-if)#ip ospf authentication key-chain OSPF_AUTHER_N_STORE
```

**开启认证.**

**OSPF区域认证**

在路由器的接口下配置MD5密钥,在进程下针对于区域开启认证.

```
R4(config)#interface g0/1
```

```
R4(config-if)#ip ospf message-digest-key 1 md5 cisco123
```

```
R4(config)#router ospf 1
```

```
R4(config-router)#area 1 virtual-link 10.10.2.2 message-digest-key 1 md5 cisco123 //虚链路接口配置MD5加
```

密钥

启MD5认证。

**空认证**

路由器之间开启认证但是不需要交换认证信息路由器接口下没有配置任何的密钥但是开启了认证。

OSPF的冷门过滤LSA的命令。

```
R5(config)#int g0/0 
R5(config-if)#ip ospf database-filter all out LSA. 但收。
```

> 💡 该接口哪怕有邻居不向对方推送任何

OSPF忽略MTU检测。

```
R5(config)#int g0/1 
R5(config-if)#ip ospf mtu-ignore MTU检测。
```

> 💡 接口在建立邻居关系时忽略

WOLF-LAB 网络技术实验室

---

# 三、BGP 专题

> 边界网关协议

## Day 23-24：BGP引入,BGP建立邻居的配置方式,BGP建立邻居的过程,包类型,BGP Router-ID

用AS号来区分和标识每一个自治系统

<1-65535> 早期16bitsAS号的范围。<1-64511> 公有的AS号<64512-65535> 私有的AS号最后的1824个AS号是私有AS号。<1-4294967295> 现如今AS号已经可以使用32bits来表示。当然显示的时候，AS号可以写成 例如： AS号为65536可以写成1.1

BGP(Border Gateway protocol)边界网关路由协议：

路径矢量路由协议，或称之为高级的距离矢量动态路由协议。

BGP基于TCP传输协议用于建立邻居关系，只能够使用单播建立BGP邻居关系，对应的TCP传输协议端口号179号端口。

**BGP引I入了的表项：**

邻居表：BGP邻居（neighbor）关系也被称之为BGP的对等体（peers）关系。

**数据库表（BGP表）：**

BGP有两种邻居关系

**EBGP邻居：**

不同AS之间的路由器建立起来的BGP邻居关系就是EBGP邻居关系。

**IBGP邻居：**

相同AS的路由器建立起来的BGP邻居关系就是IBGP邻居关系。

BGP的运行方式（建立邻居方式）

**BGP的源检测**

BGP中neighbor命令行的作用

本路由器将会主动向neighbor命令指定的地址发送TCP链接请求。

本路由器只接收neighbor命令指定的地址向自己发送的TCP链接请求。

**EBGP邻居建立邻居的运行方式：**

**通过直连建立EBGP邻居的运行方式：**

```
R1(config)#router bgp 100 
R1(config-router)#neighbor 1.1.12.2 remote-as 200 
R2(config)#router bgp 200 
R2(config-router)#neighbor 1.1.12.1 remote-as 100
```

**通过非直连建立EBGP邻居的运行方式：**

```
R1(config)#router bgp 100
R1(config-router)#neighbor 10.10.2.2 remote-as 200
R1(config-router)#neighbor 10.10.2.2 update-source loopback0
R1(config-router)#neighbor 10.10.2.2 ebgp-multihop 2/disable-connected-check //关注直连检测。
R2(config)#router bgp 200
R2(config-router)#neighbor 10.10.1.1 remote-as 100
R2(config-router)#neighbor 10.10.1.1 update-source loopback0
R2(config-router)#neighbor 10.10.1.1 ebgp-multihop 2/disable-connected-check //关注直连检测。
```

**EBGP邻居的直连检测**

EBGP建立邻居关系默认TTL=1. //默认情况下EBGP建立邻居需要直连建立，默认的TTL设定为1。

当需要建立EBGP邻居，BGP检测到neighbor所指向的目的IP地址不是本路由器的直连路由对应的目的地址，路由器不知道TTL=1是否可以将该BGP的TCP链接请求发送给对方，因此“开援”，既然发送这个TCP的链接请求不一定能够发给对面，那就不发了。

**关闭直连检测方式：**

直接关闭直连检测。 （TTL=1但是路由器可以发送TCP）

更改EBGP建立邻居时的TTL跳数。（TTL 

≥

2

≥2 既能够关闭直连检测。）R1(config-router)#neighbor 10.10.1.2.2 ebgp-multihop 2如果不设置TTL直接回车，则TTL=255。

**IBGP邻居建立邻居的运行方式：**

IBGP建立邻居关系默认TTL=255。

**通过直连建立IBGP邻居的运行方式：**

```
R1(config)#router bgp 100 //创建BGP进程。
R1(config-router)#neighbor 1.1.12.2 remote-as 100 //指定单播的BGP邻居关系以及对方AS号
R2(config)#router bgp 100 //创建BGP进程。
R2(config-router)#neighbor 1.1.12.1 remote-as 100 //指定单播的BGP邻居关系以及对方AS号
```

**通过非直连建立IBGP邻居的运行方式：**

```
R1(config)#router bgp 100 //创建BGP进程。
R1(config-router)#neighbor 10.10.2.2 remote-as 100 //指定单播的BGP邻居关系以及对方AS号
R1(config-router)#neighbor 10.10.2.2 update-source loopback0 //指定向对方发送TCP链接的源地址（更新源）
R2(config)#router bgp 100 //创建BGP进程。
R2(config-router)#neighbor 10.10.1.1 remote-as 100 //指定单播的BGP邻居关系以及对方AS号
R2(config-router)#neighbor 10.10.1.1 update-source loopback0 //指定向对方发送TCP链接的源地址（更新源）
R1#show ip bgp neighbors //查看BGP邻居关系（不常用）（详细）
R1#show ip bgp summary //查看BGP邻居关系（★★★★★）
```

```
R1#show ip bgp neighbors
```

```
R1#show ip bgp summary
```

```
R1#show ip bgp summary
```

text[[125, - 420, 476, 430]]

BGP router identifier 10.10.1.1, local AS number 100

BGP table version is 1, main routing table version 1

Neighbor

10.10.2.2
7 7 7 7 7

I0LE:指定了BGPneighbor地址，但是没有去往neighbor的路由，发送不了TCP链接请求，或者发送了TCP链接但是为得到相应。

Connect：路由器尝试向对方发送TCP链接请求，希望建立BGP邻居关系。

Active：TCP链接建立失败，将会处于Active状态。之后又会回到IDLE，然后尝试再次进入connect，再一次发送TCP希望建立邻居，如果又失败又会回到Active。

OpenSent：互相之间交换Open消息，对比消息当中的内容判断双方是否可以建立BGP邻居关系。

OpenConfirm：双方交换完成Open消息并确保Open消息中的内容无误，即可进入OpenConfirm。开始互相之间交换各自的第一个Keepalive。

Established：当双方互相之间交换确认了keepalive消息之后，开始发送Update消息，交换BGP的数据库条目。交换完成之后则正式建立成功BGP邻居。

**BGP包类型**

Open：包含了BGP路由器的AS号，Router-ID，Hold时间以及自身BGP的能力，通过对比Open消息判断是否能够建立邻居关系。

KeepAlive：保活消息，BGP建立邻居之后会每隔60s发送一次keepalive，来维持BGP的邻居关系。

update：包含了BGP的路由条目更新。

notification：当BGP的邻居状态故障或异常会发送警告消息。

BGP没有ACK消息，但是也有确认方式，发送的任何BGP数据包都会有TCP传输协议的ACK做出确认。

BGP的Router-id与OSPF相同：

**自动选举：**

如果没有loopback接口则选择最大的物理接口地址作为BGProuter-ID

如果有loopback接口则选择最大的loopback接口地址作为BGPRouter-ID

**手工指定：**

手工指定BGP的Router-ID。 手工指定>自动选举

```
R1(config)#router bgp 100
```

```
R1(config-router)#bgp router-id 1.1.1.1
```

> 💡 手工指定BGP的Router-ID。

## Day 25：BGP发起TCP连接的顺序 · 路由宣告 · BGP防环机制 · 最优路由的行为 · 成为最优的条件

当BGP的邻居关系进入IDLE状态时，路由器将会主动开启一个“Open active delayed”，（≤35000S），并开始倒计时，倒计时结束即可进入Connect状态并发起TCP连接。

Active Delay小的一方优先结束倒计时，优先发送TCP连接请求。

默认路由不能够作为BGP发送连接请求使用的路由条目。如果需要非直连建立BGP邻居关系，则路由表中能够使用明细路由

默认路由不能够作为主动发送TCP连接的那一方，可以回复TCP连接请求。

**BGP的路由宣告：**

我们不生产路由，我们只是路由条目的搬运工——BGP（摘自农夫山泉）

BGP可以直接将路由表中存在的（直连路由/EIGRP路由/OSPF路由/其它BGP的路由/...）路由表里有的路由（主机路由除外），宣告进入到BGP的数据库当没有开启自动汇总时，宣告路由进入BGP数据库：

使用Network命令匹配路由表中路由条目的网络号及掩码完全一致，即可将路由条目宣告进入到BGP的数据库。

Router BGP XX

Network <Network number> mask <Mask>

```
R1#show ip bgp
```

> 💡 查看BGP表（BGP数据库）

可以使用重分布，能够将路由表中当前明细的路由条目都重分布进入BGP数据库

Router bgp XX

redistribute <protocol>

如果开启了自动汇总，宣告路由进入BGP数据库：

使用Network命令匹配路由表中路由条目的网络号及掩码完全一致，即可将路由条目宣告进入到BGP的数据库。

使用network命令匹配路由表中路由条目中的主类路由网络号及掩码完全一致，则可以宣告路由条目中的主类路由进入数据库。

可以使用重分布将明细路由的主类路由重分布引入BGP数据库

**BGP针对于最优路由的行为：**

只有最优的BGP路由条目可以提交到路由表

只会通告数据库当中的最优路由给自己的BGP邻居。

**BGP最优路由的条件：**

BGP的入向策略允许的BGP路由。

下一跳可达的路由。

BGP的十三条选路原则选择出的路由。

如果开启了BGP同步，则满足同步条件的路由可以成为最优路由（特殊的BGP最优路由选举方式）

**BGP的路由条目传递：**

EBGP之间传递路由条目下一跳改变

**BGP路由管理距离20**

IBGP之间传递路由条目下一跳不变（...）

IBGP路由管理距离280.

router bgp XX

neighbor a.b.c.d next-hop-self

//向邻居通告路由条目时将路由的下一跳改成自己

只需要在边界路由器上敲。

**解决路由黑洞的方式：**

拉物理线路，（可以，但仅限于对接的AS熟练少可以使用。）

重分布（可以使得路由黑洞有路由，但是会导致BGP路由丢失属性）

IBGP全互联。

以上三个可以用，不是最好的方式。

联邦

**绕开IBGP水平分割**

**路由反射器**

**关闭IBGP水平分割**

MPLS(MPLS VPN)

不走水平分割。

当路由器从IBGP邻居收到的路由条目不会再通告给自己的其它IBGP邻居

**AS-Path属性**

当BGP路由条目离开当前AS时，将会在BGP路由条目当中添加AS-Path属性增添当前离开的AS号码。

当路由器收到了BGP路由条目时，一旦当前路由条目的AS-Path属性中包含了自己的AS号，则不接受该路由条目。

## Day 26：联邦,路由反射器,BGP清理进程的方式

**搞定IBGP水平分割**

联邦

绕开了IBGP的水平分割

IBGP水平分割：从IBGP邻居收到的路由不会再传递给IBGP邻居。

在同一个AS内部建立EBGP邻居关系。

router bgp xxx

bgp confederation identifier XXX

//指定本路由器属于的联邦的AS。

当联邦当中的路由器需要建立EBGP邻居关系时，使用大范围的AS去建立EBGP邻居关系。

当联邦当中的路由器需要建立IBGP邻居关系时，使用小范围的AS去建立IBGP邻居关系。

router bgp xxx

bgp confederation peers 64523

//指定本联邦当中的EBGP邻居AS号。

当需要与联邦内部指定的小的AS建立EBGP邻居关系时将会使用小范围的AS去建立。

联邦当中小范围的AS的路由器数量≤2。

**路由反射器**

关闭了IBGP水平分割

可以使得一台运行了BGP的路由器成为BGP的路由反射器。

路由反射器将会关闭自己的IBGP水平分割

虽然关闭了水平分割，但是路由反射器的BGP路由器还是存在BGP路由条目传递的激励机制。

一台路由反射器至少有一台客户端（将路由器配置为路由反射器时必须为其指定至少一个客户端。）

非非不能传：从非客户端的IBGP邻居收到的BGP路由条目不能够传递给其它的非客户端的IBGP邻居。

```
R3(config)#router bgp 234
```

```
R3(config-router)#neighbor 10.10.2.2 router-reflector-client
```

经过BGP路由反射器反射过的BGP路由条目，路由反射器将会在路由条目的属性当中自动插入originator字段和cluster list字段

Originator：表示该BGP路由条目经过路由反射器反射之前，该IBGP路由条目通告路由器的BGP Router-ID。

当BGP路由器收到的BGP路由条目的属性当中Originator字段出现了自己的BGP Router-id，表示该路由是自己传递出去的路由，将会丢弃该路由

Cluster list：当路由器反射器反射了该BGP路由条目时，将会在该路由条目的属性当中插入自己的BGP Router-ID进入Cluster-list ID字段，表示该

BGP路由经过自己反射过了。

当BGP路由器收到的BGP路由条目属性当观众Cluster list字段包含了自己的BGP Router-ID，则丢弃该路由，不接受。

**BGP 清理进程的方式**

硬清

直接断开邻居关系，重新建立邻居，重新交换路由。

clear ip bgp x

clear ip bgp 10.10.3.3

//清理所有的BGP邻居关系（慎用）

//重置某一个邻居关系。

软清

BGP是触发更新，只要BGP的路由条目没有发生过变更或故障，就不会发送update消息进行路由条目更新。

路由器针对于路由条目实施策略之后没有路由条目更新会导致策略没有生效。

```
R2(config)#access-list 1 deny 1.1.1.0
```

```
R2(config)#access-list 1 permit any
```

```
R2(config)#router bgp 234
```

```
R2(config-router)#neighbor 10.10.3.3 distribute-list 1 out
```

通告的BGP路由做过滤。

```
R2(config-router)#
```

clear ip bgp * soft out

**//出方向软清**

路由器会发送一个路由刷新通告，之后会专门发送BGP的Update消息更新通告自己的BGP数据库条目。

clear ip bgp * soft in

**//入方向软清**

路由器会发送一个路由刷新请求消息，收到该消息的邻居将会回复路由条目刷新通告，并且回复Update通告BGP的数据库条目。

clear ip bgp * soft

//双方向软清=in+out。

## Day 27：BGP路由条目属性的分类,团体属性,Backdoor

公认强制属性：AS-Path Next-hop Origin Code （通告BGP路由条目时一定会携带在路由条目当中的属性。） 公认自宽属性：Local Preference（EBGP之间传递路由不携带该属性，IBGP之间传递路由携带该属性。） 可选可传递属性：团体属性（Community） 可选非传递属性：MED

**团体属性：**

使得BGP路由器可以控制BGP路由条目的传递范围。

公有团体属性：（使用设备已经预定好的团体属性进行设置，按照系统的设定规定了路由条目的传递范围）

Internet：BGP路由没有任何的传递范围限制。

no-export：该BGP路由条目不会传递出路由器所在的AS。（如果存在联邦的环境，该BGP路由不会传递出大的AS）

no-advertise：该BGP路由条目不会传递给任何的BGP邻居

local-as：该BGP路由条目不会传递出路由器所在的AS。（如果存在联邦的环境，该BGP路由不会传递出小的AS）

> 图片内容：配置命令

```
R1(config)#ip prefix-list 100 permit 100.1.1.0/24
R1(config)#ip prefix-list 101 permit 100.1.1.0/24
R1(config)#ip prefix-list 102 permit 100.1.2.0/24
R1(config)#ip prefix-list 103 permit 100.1.3.0/24 //使用前缀列表匹配上需要设置团体属性的路由。
R1(config)#route-map COM permit 10
R1(config-route-map)#match ip address prefix-list 100
R1(config-route-map)#set community internet
R1(config-route-map)#exit
R1(config)#route-map COM permit 20
R1(config-route-map)#match ip address prefix-list 101
R1(config-route-map)#set community no-export
R1(config-route-map)#exit
R1(config)#route-map COM permit 30
R1(config-route-map)#match ip address prefix-list 102
R1(config-route-map)#set community no-advertise
R1(config-route-map)#exit
R1(config)#route-map COM permit 40
R1(config-route-map)#match ip address prefix-list 103
R1(config-route-map)#set community local-as
R1(config-route-map)#exit
R1(config)#router bgp 100
R1(config-router)#neighbor 192.168.12.2 route-map COM out //针对于匹配的路由设定团体属性。
```

> 💡 向外通告路由条目时调用route-map

路由器在向外通告BGP路由条目时默认不会携带团体属性，哪怕设置了团体属性也无用。

```
R1(config-router)#neighbor 192.168.12.2 send-community
```

> 💡 使得路由器向外通告路由条目时允许携带团体属性通告。

私有的团体属性：（可以人为给予路由条目特定的团体属性并利用该团体属性进行过滤。）

类似于EIGRP，OSPF当中的Tag值。

BGP当中没有Tag值这个属性，取而代之的是私有团体属性。

如果需要针对于私有团体属性过滤路由，需要使用团体属性列表匹配私有团体属性并用于调用。

```
R4(config)#ip community-list 1 permit 100 条目。
```

```
R4(config)#route-map R3- R4 deny 10 deny
```

```
R4(config-route-map)#match community 1
```

```
R4(config)# route-map R3- R4 permit 20
```

```
R4(config-route-map)#exit
```

```
R4(config)#router bgp 64544
```

```
R4(config-router)#neighbor 18.10.3.3 route-map R3- R4 in 调用route-map.
```

```
R4(config)#ip community-list 1 permit 100 200 能匹配。
```

```
R4(config)#ip community-list 1 permit 100
```

上.

backdoor

当通过非直连建立EBGP邻居关系时，千万不要将建立邻居所使用的接口对应的路由条目宣告进入BGP，容易造成递归成环以及邻居联动问题。

Network a.b.c.d mask x.x.x.x backdoor //network宣告路由表中的EBGP路由条目可以将其管理距离设置为IBGP路由的管理距离200。（受害者上敲。）

> 图片内容：WOLF-LAB 网络技术实验室 网络工程师培训系列课程 

## Day 28-29：BGP的路由聚合,BGP的AS-Path属性,Local-Preference

1 R2: 2 ip prefix-list 10.6 seq 5 permit 10.10.6.0/24 //使用前缀列表匹配路由 3 route-map R2- R1 permit 10 //创建Route-map工具 4 match ip address prefix-list 10.6 //匹配上对应的路由 5 set as-path prepend 123 456 //设置添加的AS-Path属性的AS号 6 router bgp 23 //进入BGP进程 7 neighbor 1.1.12.1 route-map R2- R1 out //针对于邻居给自己的路由调用route-map工具 做路由策略

当在BGP的出行方向调整AS-Path属性，添加AS号时，将会在原有最后一个经过的AS号码的右侧添加AS号。

```
R1#show ip bgp
```

\*> 10.10.6.0/24 1.1.12.2

812345623（最后一个经过的AS）123456680i

> 图片内容：配置命令

**R2:**

access-list 1 permit 10.10.2.0

access-list 2 permit 6.6.6.0

route-map R2-R1 permit 10

match ip address 1

set as-path prepend 456

route-map R2-R1 permit 20

match ip address 2

set as-path prepend last-as 5 //将该路由条目AS-path属性中最右侧的AS号复制5次。

route-map R2-R1 permit 30

router bgp 23

neighbor 1.1.12.1 route-map R2-R1 out

默认情况下，当把BGP路由重分布引入到IGP协议时，会将BGP路由最左侧的AS-Path属性号码作为Tag写入到重分布以后的IGP路由数据库条目当中。

> 图片内容：配置命令

route-map AS-PATH permit 10

set as-path tag //将IGP路由条目的tag作为BGP的AS-Path属性

router bgp 145

redistribute eigrp 145 route-map AS-PATH //将IGP路由引入到BGP时，将IGP路由的tag作为BGP的AS-Path属性。

Local-Preference（本地优先级）

公认自觉属性。（EBGP之间传递路由不携带本地优先级属性。IBGP之间传递路由携带本地优先级属性）

当路由器宣告路由条目进入BGP表时，默认BGP路由条目的本地优先级为100。（选择路由器设定的本地优先级数值默认100）

当路由器收到BGP路由条目时，发现该路由没有本地优先级属性，则默认设置该BGP路由条目的本地优先级为100。（选择路由器设定的本地优先级数值默认100）

告知本AS内部的设备访问目的网段对应的出行路径。（告知本AS的所有设备从哪个方向离开去访问目的网段。）

当需要通过本地优先级选举最优的BGP路由条目时，优选本地优先级属性值更大的路由条目作为最优。

```
R1(config)#router bgp 145
```

```
R1(config-router)#bgp default local-preference xx
```

> 💡 通过该命令可以修改路由器默认的本地优先级数值（默认=100）

该参数针对于所有的EBGP路由条目以及本路由器宣告的路由条目全部生效，作用范围很大。

可以使用route-map工具针对于路由条目调整本地优先级。

不可以在EBGP的出行方向使用route-map调整路由条目的本地优先级，设置了本地优先级值是向EBGP邻居通告根本不携带本地优先级属性。

> 图片内容：配置命令

access-list 1 permit 10.10.2.0

route-map R2-R1 permit 10

match ip address 1

set local-preference 200

route-map R2-R1 permit 20

router bgp 145

neighbor 1.1.12.2 route-map R2-R1 in

可以在EBGP邻居关系的入方向以及IBGP的邻居的入方向和出方向都能够调用修改路由条目的本地优先级。

## Day 30：BGP的十三条选路原则(上)

默认情况下，针对某一个BGP路由，路由器会先认为其第一个转发路径的路由条目为最优路由，之后将会使得该路径的BGP路由与下一条路径的路由条目进行比较，胜出者继续与之后的路径路由条目进行比较，最终选择出最优路由。

默认情况下，BGP针对某一个路由条目，从不同路径收到该路由时，将会按照其接收的顺序来先后排列，按照从新到旧来排列。

1、优选Weight值最大的BGP路由条目

Weight值仅本地有效 不会向任何BGP邻居通告weight值属性。 不可以在BGP的出口内挂载route-map修改weight值属性。 当从BGP邻居收到的BGP路由没有weight属性时，默认其weight 

0

=0 。 当宣告路由条目进入自己的BGP表时，默认BGP的Weight=32768。 始终选择自己宣告的路由条目作为最优。 是最快修改本地路由器针对于最优路由选举的方式。 只能够在EBGP的入方向或IBGP的入方向设定BGP路由条目的Weight。

> 图片内容：配置命令

```
R4(config)#access-list 1 permit 101.1.1.0
R4(config)#route-map R5-R4 permit 10
R4(config-route-map)#match ip address 1
R4(config-route-map)#set weight 666
R4(config-route-map)#exit
R4(config)#route-map R5-R4 permit 20
R4(config-route-map)#exit
R4(config)#router bgp 234
R4(config-router)#neighbor 10.10.5.5 route-map R5-R4 in //可以在入方向挂载route-map调整weight值属性。
R4(config-router)#end
```

2、优选本地优先级最大的路由条目

公认自宽属性。（EBGP之间传递路由不携带本地优先级属性，IBGP之间传递路由携带本地优先级属性）

当路由器宣告路由条目进入BGP表时，默认BGP路由条目的本地优先级为100。（选择路由器设定的本地优先级数值默认100）

当路由器收到BGP路由条目时，发现该路由没有本地优先级属性，则默认设置该BGP路由条目的本地优先级为100。（选择路由器设定的本地优先级数值默认100）告知本AS内部的设备访问目的网段对应的出方向路径。（告知本AS的所有设备从哪个方向离开去访问目的网段。）

当需要通过本地优先级选举最优的BGP路由条目时，优选本地优先级属性值更大的路由条目作为最优。

```
R1(config)#router bgp 145 
R1(config-router)#bgp default local-preference xx //通过该命令可以修改路由器默认的本地优先级数值（默认=100）该参数针对于所有的EBGP路由条目以及本路由器宣告的路由条目全部生效，作用范围很大。可以使用route-map工具针对于路由条目调整本地优先级。
```

可以使用route-map工具针对于路由条目调整本地优先级。

不可以在EBGP的出口内使用route-map调整路由条目的本地优先级，设置了本地优先级但是向EBGP邻居通告根本不携带本地优先级属性。

> 图片内容：配置命令

access-list 1 permit 10.10.2.0

route-map R2-R1 permit 10

match ip address 1

set local-preference 200

route-map R2-R1 permit 20

router bgp 145

neighbor 1.1.12.2 route-map R2-R1 in

可以在EBGP邻居关系的入方向以及IBGP的邻居的入方向和出方向都能够调用修改路由条目的本地优先级。

BGP的十三条选路原则，只有以上两条选路原则是越大越优先，其余的路选原则都是小的或者短的优先。

3、优选本地起源的BGP路由条目 （自己宣告的路由优先于从其它人那学习到的路由。）

自己宣告的BGP路由优先于从邻居学习到的BGP路由

自己network引入的BGP路由

自己重分布引入的BGP路由

**自己聚合产生的BGP路由**

Network > redistribute > aggregate

4、优选AS-Path属性长度最短的路由

AS-Path属性是EBGP之间的防环机制

当路由条目离开本AS时，将会在AS-Path属性当中插入自己的AS号进入属性当中。

当收到BGP路由条目时，如果AS-Path属性中包含了自己的AS号，则拒绝该路由条目进入自己的BGP表。

当路由聚合不同AS的BGP路由条目时，如果只聚合正常的AS号，不考虑联邦，将会产生（的AS-Path属性，称之为as-set当路由聚合不同AS的BGP路由条目时，如果聚合联邦的AS号，则会产生（的AS-Path属性。

BGP会优选AS-Path当中属性长度最短的路由（最短=AS-Path属性中AS号码的数量最少的路由条目）由BGP路由聚合产生的（AS-SET的AS-Path属性，不论（中有多少个AS号，整个AS-SET统计数量为1由联邦以及联邦聚合产生的（AS-path属性，不论（中有多少个AS号，都不计数，统计为0AS-Path的属性，当添加AS号时，默认情况下将会在原有AS号的左侧添加，可以通过该顺序得出接口，路由条目AS-Path属性的最右侧AS号是BGP路由条目源头所在的AS，路由条目AS-Path属性最左侧的AS号是BGP路由条目所经过的最后一个AS。

可以利用Route-map工具调整BGP路由条目的AS-Path属性。只能够在EBGP邻居关系之间调整AS-Path属性号码。IBGP之间不能够调整AS-Path属性。一般情况下添加AS-Path属性号码时，添加自己的AS号。

只能够添加BGP路由条目的AS号，不能减去AS号码。

> 图片内容：配置命令

**R1:**

ip prefix-list 10.6 seq 5 permit 10.10.6.0/24 //使用前缀列表匹配路由

route-map R2-R1 permit 10 //创建Route-map工具

match ip address prefix-list 10.6 //匹配上对应的路由

set as-path prepend 123 456 //设置添加的AS-Path属性的AS号

router bgp 145 //进入BGP进程

neighbor 1.1.12.2 route-map R2-R1 in //针对于邻居给自己的路由调用route-map工具做路由策略

当在BGP的入方向调整AS-Path属性，添加AS号时，将会在原有最后一个经过的AS号码的左侧添加AS号。

> 图片内容：R1#show ip bgp

*> 10.10.6.0/24 1.1.12.2 0 123 456 23(最后一个经过的AS) 600 i

> 图片内容：配置命令

**R2:**

ip prefix-list 10.6 seq 5 permit 10.10.6.0/24 //使用前缀列表匹配路由

route-map R2-R1 permit 10 //创建Route-map工具

match ip address prefix-list 10.6 //匹配上对应的路由

set as-path prepend 123 456 //设置添加的AS-Path属性的AS号

router bgp 23 //进入BGP进程

neighbor 1.1.12.1 route-map R2-R1 out //针对于邻居给自己的路由调用route-map工具做路由策略

**> 图片内容：**

当在BGP的出方向调整AS-Path属性，添加AS号时，将会在原有最后一个经过的AS号码的右侧添加AS号...

```
R1#show ip bgp
```

*> 10.10.6.0/24 1.1.12.2 0 123 456 23(最后一个经过的AS) 123 456 600 i

> 图片内容：配置命令

**R2:**

access-list 1 permit 10.10.2.0

access-list 2 permit 6.6.6.0

route-map R2-R1 permit 10

match ip address 1

set as-path prepend 456

route-map R2-R1 permit 20

match ip address 2

set as-path prepend last-as 5次. //将该路由条目AS-path属性中最右侧的AS号复制5次。

route-map R2-R1 permit 30

router bgp 23

neighbor 1.1.12.1 route-map R2-R1 out

默认情况下，当把BGP路由重分布引入到IGP协议时，会将BGP路由最左侧的AS-Path属性号码作为Tag写入到重分布以后的IGP路由数据库条目当中。

> 图片内容：配置命令

route-map AS-PATH permit 10

set as-path tag //将IGP路由条目的tag作为BGP的AS-Path属性

router bgp 145

redistribute eigrp 145 route-map AS-PATH //将IGP路由引入到BGP时，将IGP路由的tag作为BGP的AS-Path属性。

neighbor xxxx allows-in <num> //打破 AS-Path的防环机制，可以允许自己的AS号在BGP路由当中出现N次

bgp bestpath as-path ignore //可以使用该命令跳过AS-Path属性的比较。

5、优选起源类型最小的路由条目

IGP //表明该BGP路由条目是通过Network命令引入的BGP路由。

incomplete //表明该BGP路由条目是通过重分布引入的BGP路由

EGP //表明该BGP路由条目是BGP的前身EGP路由协议引入的路由。（已被淘汰，可以不用在意）

```
R3(config)#route-map RED permit 10 2
R3(config-route-map)#match interface Loopback0 3
R3(config-route-map)#set origin igp 4
R3(config-route-map)#exit 5
R3(config-route-map)#exit 6
R3(config-route)#redistribute connected route-map RED 7
R2(config)#route-map ORI permit 10 8
R2(config-route-map)#set origin incomplete 9
R2(config-route-map)#exit 10
R2(config)#router bgp 23 11
R2(config-route-map)#network 10.10.2.0 mask 255.255.255.0 route-map ORI 12
R1(config)#access-list 1 permit 10.10.2.0 13
R1(config)#route-map R2- R1 permit 10 14
R1(config-route-map)#match ip address 1 15
R1(config-route-map)#set origin incomplete 16
R1(config-route-map)#exit 17
R1(config)#router bgp 145 18
R1(config-route-map)#neighbor 1.1.12.2 route-map R2- R1 in 19 6 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71 72 73 74 75 76 77 78 79 80 81 82 83 84 85 86 87 88 89 90 91 92 93 94 95 96 97 98 99 100 101 102 103 104 105 106 107 108 109 110 111 112 113 114 115 116 117 118 119 120 121 122 123 124 125 126 127 128 129 130 131 132 133 134 135 136 137 138 139 140 141 142 143 144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 160 161 162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179 180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197 198 199 200 201 202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 217 218 219 220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 235 236 237 238 239 240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255 256 257 258 259 260 261 262 263 264 265 266 267 268 269 270 271 272 273 274 275 276 277 278 279 280 281 282 283 284 285 286 287 288 289 290 291 292 293 294 295 296 297 298 299 300 301 302 303 304 305 306 307 308 309 310 311 312 313 314 315 316 317 318 319 320 321 322 323 324 325 326 327 328 329 330 331 332 333 334 335 336 337 338 339 340 341 342 343 344 345 346 347 348 349 350 351 352 353 354 355 356 357 358 359 360 361 362 363 364 365 366 367 368 369 370 371 372 373 374 375 376 377 378 379 380 381 382 383 384 385 386 387 388 389 390 391 392 393 394 395 396 397 398 399 400 401 402 403 404 405 406 407 408 409 410 411 412 413 414 415 416 417 418 419 420 421 422 423 424 425 426 427 428 429 430 431 432 433 434 435 436 437 438 439 440 441 442 443 444 445 446 447 448 449 450 451 452 453 454 455 456 457 458 459 460 461 462 463 464 465 466 467 468 469 470 471 472 473 474 475 476 477 478 479 480 481 482 483 484 485 486 487 488 489 490 491 492 493 494 495 496 497 498 499 500 501 502 503 504 505 506 507 508 509 510 511 512 513 514 515 516 517 518 519 520 521 522 523 524 525 526 527 528 529 530 531 532 533 534 535 536 537 538 539 540 541 542 543 544 545 546 547 548 549 550 551 552 553 554 555 556 557 558 559 560 561 562 563 564 565 566 567 568 569 570 571 572 573 574 575 576 577 578 579 580 581 582 583 584 585 586 587 588 589 590 591 592 593 594 595 596 597 598 599 600 601 602 603 604 605 606 607 608 609 610 611 612 613 614 615 616 617 618 619 620 621 622 623 624 625 626 627 628 629 630 631 632 633 634 635 636 637 638 639 640 641 642 643 644 645 646 647 648 649 650 651 652 653 654 655 656 657 658 659 660 661 662 663 664 665 666 667 668 669 670 671 672 673 674 675 676 677 678 679 680 681 682 683 684 685 686 687 688 689 690 691 692 693 694 695 696 697 698 699 700 701 702 703 704 705 706 707 708 709 710 711 712 713 714 715 716 717 718 719 720 721 722 723 724 725 726 727 728 729 730 731 732 733 734 735 736 737 738 739 740 741 742 743 744 745 746 747 748 749 750 751 752 753 754 755 756 757 758 759 760 761 762 763 764 765 766 767 768 769 770 771 772 773 774 775 776 777 778 779 780 781 782 783 784 785 786 787 788 789 790 791 792 793 794 795 796 797 798 799 800 801 802 803 804 805 806 807 808 809 810 811 812 813 814 815 816 817 818 819 820 821 822 823 824 825 826 827 828 829 830 831 832 833 834 835 836 837 838 839 840 841 842 843 844 845 846 847 848 849 850 851 852 853 854 855 856 857 858 859 860 861 862 863 864 865 866 867 868 869 870 871 872 873 874 875 876 877 878 879 880 881 882 883 884 885 886 887 888 889 890 891 892 893 894 895 896 897 898 899 900 901 902 903 904 905 906 907 908 909 910 911 912 913 914 915 916 917 918 919 920 921 922 923 924 925 926 927 928 929 930 931 932 933 934 935 936 937 938 939 940 941 942 943 944 945 946 947 948 949 950 951 952 953 954 955 956 957 958 959 960 961 962 963 964 965 966 967 968 969 970 971 972 973 974 975 976 977 978 979 980 981 982 983 984 985 986 987 988 989 990 991 992 993 994 995 996 997 998 999 1000 1001 1002 1003 1004 1005 1006 1007 1008 1009 1010 1011 1012 1013 1014 1015 1016 1017 1018 1019 1020 1021 1022 1023 1024 1025 1026 1027 1028 1029 1030 1031 1032 1033 1034 1035 1036 1037 1038 1039 1040 1041 1042 1043 1044 1045 1046 1047 1048 1049 1050 1051 1052 1053 1054 1055 1056 1057 1058 1059 1060 1061 1062 1063 1064 1065 1066 1067 1068 1069 1070 1071 1072 1073 1074 1075 1076 1077 1078 1079 1080 1081 1082 1083 1084 1085 1086 1087 1088 1089 1090 1091 1092 1093 1094 1095 1096 1097 1098 1099 1100 1101 1102 1103 1104 1105 1106 1107 1108 1109 1110 1111 1112 1113 1114 1115 1116 1117 1118 1119 1120 1121 1122 1123 1124 1125 1126 1127 1128 1129 1130 1131 1132 1133 1134 1135 1136 1137 1138 1139 1140 1141 1142 1143 1144 1145 1146 1147 1148 1149 1150 1151 1152 1153 1154 1155 1156 1157 1158 1159 1160 1161 1162 1163 1164 1165 1166 1167 1168 1169 1170 1171 1172 1173 1174 1175 1176 1177 1178 1179 1180 1181 1182 1183 1184 1185 1186 1187 1188 1189 1190 1191 1192 1193 1194 1195 1196 1197 1198 1199 1200 1201 1202 1203 1204 1205 1206 1207 1208 1209 1210 1211 1212 1213 1214 1215 1216 1217 1218 1219 1220 1221 1222 1223 1224 1225 1226 1227 1228 1229 1230 1231 1232 1233 1234 1235 1236 1237 1238 1239 1240 1241 1242 1243 1244 1245 1246 1247 1248 1249 1250 1251 1252 1253 1254 1255 1256 1257 1258 1259 1260 1261 1262 1263 1264 1265 1266 1267 1268 1269 1270 1271 1272 1273 1274 1275 1276
```

1 

## Day 30-31：BGP的十三条选路原则

默认情况下，针对于某一个BGP路由，路由器会先认为其第一个转发路径的路由条目为最优路由，之后将会使得该路径的BGP路由与下一条路径的路由条目进行比较，胜出者继续与之后的路径路由条目进行比较，最终选择出最优路由。（BGP deterministic-med除外）

默认情况下，BGP针对于某一个路由条目，从不同路径收到该路由时，将会按照其接收的顺序来先后排列，按照从新到旧来排列。（BGP deterministic-med除外）

1、优选Weight值最大的BGP路由条目

Weight值仅本地有效 不会向任何BGP邻居通告weight值属性。不可在BGP的出行由挂载route-map修改weight值属性。当从BGP邻居收到的BGP路由没有weight属性时，默认其weight=0。当宣告路由条目进入自己的BGP表时，默认BGP的Weight=32768。始终选择自己宣告的路由条目作为最优。是最快修改本地路由器针对于最优路由选举的方式。只能够在EBGP的入方向或IBGP的入方向设定BGP路由条目的Weight。

> 图片内容：配置命令

```
R4(config)#access-list 1 permit 101.1.1.0
R4(config)#route-map R5-R4 permit 10
R4(config-route-map)#match ip address 1
R4(config-route-map)#set weight 666
R4(config-route-map)#exit
R4(config)#route-map R5-R4 permit 20
R4(config-route-map)#exit
R4(config)#router bgp 234
R4(config-router)#neighbor 10.10.5.5 route-map R5-R4 in //可以在入方向挂载route-map调整weight值属性。
R4(config-router)#end
```

2、优选本地优先级最大的路由条目

公认自宽属性。（EBGP之间传递路由不携带本地优先级属性。IBGP之间传递路由携带本地优先级属性）

当路由器宣告路由条目进入BGP表时，默认BGP路由条目的本地优先级为100。（选择路由器设定的本地优先级数值默认100）

当路由器收到BGP路由条目时，发现该路由没有本地优先级属性，则默认设置该BGP路由条目的本地优先级为180。（选择路由器设定的本地优先级数值默认180）

告知本AS内部的设备访问目的网段对应的出方向路径。（告知本AS的所有设备从哪个方向离开去访问目的网段。）

当需要通过本地优先级选举最优的BGP路由条目时，优选本地优先级属性值更大的路由条目作为最优。

```
R1(config)#router bgp 145
```

```
R1(config-router)#bgp default local-preference xx
```

> 💡 通过该命令可以修改路由器默认的本地优先级数值（默认=100）

该参数针对于所有的EBGP路由条目以及本路由器宣告的路由条目全部生效，作用范围很大。

可以使用route-map工具针对于路由条目调整本地优先级。

不可以在EBGP的出行向使用route-map调整路由条目的本地优先级，设置了本地优先级但是向EBGP邻居通告根本不携带本地优先级属性。

> 图片内容：配置命令

access-list 1 permit 10.10.2.0

route-map R2-R1 permit 10

match ip address 1

set local-preference 200

route-map R2-R1 permit 20

router bgp 145

neighbor 1.1.12.2 route-map R2-R1 in

可以在EBGP邻居关系的入方向以及IBGP的邻居的入方向和出方向都能够调用修改路由条目的本地优先级。

BGP的十三条选路原则，只有以上两条选路原则是越大越优先，其余的路选原则都是小的或者短的优先。

3、优选本地起源的BGP路由条目 （自己宣告的路由优先于从其它人那学习到的路由。）

自己宣告的BGP路由优先于从邻居学习到的BGP路由

自己network引入的BGP路由

自己重分布引入的BGP路由

**自己聚合产生的BGP路由**

Network > redistribute > aggregate

4、优选AS-Path属性长度最短的路由

AS-Path属性是EBGP之间的防环机制

当路由条目离开本AS时，将会在AS-Path属性当中插入自己的AS号进入属性当中。

当收到BGP路由条目时，如果AS-Path属性中包含了自己的AS号，则拒绝该路由条目进入自己的BGP表。

当路由聚合不同AS的BGP路由条目时，如果只聚合正常的AS号，不考虑联邦，将会产生（的AS-Path属性，称之为as-set当路由聚合不同AS的BGP路由条目时，如果聚合联邦的AS号，则会产生[]的AS-Path属性。

BGP会优选AS-Path当中属性长度最短的路由（最短=AS-Path属性中AS号码的数量最少的路由条目）由BGP路由聚合产生的（AS-SET的AS-Path属性，不论（中有多少个AS号，整个AS-SET统计数量为1由联邦以及联邦聚合产生的（[]AS-path属性，不论（[]中有多少个AS号，都不计数，统计为0AS-Path的属性，当添加AS号时，默认情况下将会在原有AS号的左侧添加，可以通过该顺序得出接口，路由条目AS-Path属性的最右侧AS号是BGP路由条目源头所在的AS，路由条目AS-Path属性最左侧的AS号是BGP路由条目所经过的最后一个AS。

可以利用Route-map工具调整BGP路由条目的AS-Path属性。只能够在EBGP邻居关系之间调整AS-Path属性号码。IBGP之间不能够调整AS-Path属性。一般情况下添加AS-Path属性号码时，添加自己的AS号。

只能够添加BGP路由条目的AS号，不能减去AS号码。

> 图片内容：配置命令

**R1:**

ip prefix-list 10.6 seq 5 permit 10.10.6.0/24 //使用前缀列表匹配路由

route-map R2-R1 permit 10 //创建Route-map工具

match ip address prefix-list 10.6 //匹配上对应的路由

set as-path prepend 123 456 //设置添加的AS-Path属性的AS号

router bgp 145 //进入BGP进程

neighbor 1.1.12.2 route-map R2-R1 in //针对于邻居给自己的路由中调用route-map工具做路由策略

当在BGP的入方向调整AS-Path属性，添加AS号时，将会在原有最后一个经过的AS号码的左侧添加AS号。

> 图片内容：R1#show ip bgp

*> 10.10.6.0/24 1.1.12.2 0 123 456 23(最后一个经过的AS) 600 i

> 图片内容：配置命令

**R2:**

ip prefix-list 10.6 seq 5 permit 10.10.6.0/24 //使用前缀列表匹配路由

route-map R2-R1 permit 10 //创建Route-map工具

match ip address prefix-list 10.6 //匹配上对应的路由

set as-path prepend 123 456 //设置添加的AS-Path属性的AS号

router bgp 23 //进入BGP进程

neighbor 1.1.12.1 route-map R2-R1 out 做路由策略

> 图片内容：R1#show ip bgp

*> 10.10.6.0/24 1.1.12.2 0 123 456 23(最后一个经过的AS) 123 456 600 i

> 图片内容：配置命令

**R2:**

access-list 1 permit 10.10.2.0

access-list 2 permit 6.6.6.0

route-map R2-R1 permit 10

match ip address 1

set as-path prepend 456

route-map R2-R1 permit 20

match ip address 2

set as-path prepend last-as 5 //将该路由条目AS-path属性中最右侧的AS号复制5次。

route-map R2-R1 permit 30

router bgp 23

neighbor 1.1.12.1 route-map R2-R1 out

默认情况下，当把BGP路由重分布引入到IGP协议时，会将BGP路由最左侧的AS-Path属性号码作为Tag写入到重分布以后的IGP路由数据库条目当中。

> 图片内容：配置命令

route-map AS-PATH permit 10

set as-path tag //将IGP路由条目的tag作为BGP的AS-Path属性

router bgp 145

redistribute eigrp 145 route-map AS-PATH //将IGP路由引入到BGP时，将IGP路由的tag作为BGP的AS-Path属性。

中出现N次bgp bestpath as-path ignore //可以使用该命令就过AS-Path属性的比较。

5、优选起源类型最小的路由条目

IGP //表明该BGP路由条目是通过Network命令引入的BGP路由。incomplete //表明该BGP路由条目是通过重分布引入的BGP路由EGP //表明该BGP路由条目是BGP的前身EGP路由协议引入的路由。（已被淘汰，可以不用在意）

```
R3(config)#route-map RED permit 10 2
R3(config-route-map)#match interface Loopback0 3
R3(config-route-map)#set origin igp 4
R3(config-route-map)#exit 5
R3(config)#router bgp 23 6
R3(config-router)#redistribute connected route-map RED 7
R2(config)#route-map ORI permit 10 8
R2(config-route-map)#set origin incomplete 9
R2(config-route-map)#exit 10
R2(config)#router bgp 23 11
R2(config-route-map)#network 10.10.2.0 mask 255.255.255.0 route-map ORI 12
R1(config)#access-list 1 permit 10.10.2.0 13
R1(config)#route-map R2- R1 permit 10 14
R1(config-route-map)#match ip address 1 15
R1(config-route-map)#set origin incomplete 16
R1(config-route-map)#exit 17
R1(config)#router bgp 145 18
R1(config-router)#neighbor 1.1.12.2 route-map R2- R1 in 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71 72 73 74 75 76 77 78 79 80 81 82 83 84 85 86 87 88 89 90 91 92 93 94 95 96 97 98 99 100 101 102 103 104 105 106 107 108 109 110 111 112 113 114 115 116 117 118 119 120 121 122 123 124 125 126 127 128 129 130 131 132 133 134 135 136 137 138 139 140 141 142 143 144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 160 161 162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179 180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197 198 199 200 201 202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 217 218 219 220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 235 236 237 238 239 240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255 256 257 258 259 260 261 262 263 264 265 266 267 268 269 270 271 272 273 274 275 276 277 278 279 280 281 282 283 284 285 286 287 288 289 290 291 292 293 294 295 296 297 298 299 300 301 302 303 304 305 306 307 308 309 310 311 312 313 314 315 316 317 318 319 320 321 322 323 324 325 326 327 328 329 330 331 332 333 334 335 336 337 338 339 340 341 342 343 344 345 346 347 348 349 350 351 352 353 354 355 356 357 358 359 360 361 362 363 364 365 366 367 368 369 370 371 372 373 374 375 376 377 378 379 380 381 382 383 384 385 386 387 388 389 390 391 392 393 394 395 396 397 398 399 400 401 402 403 404 405 406 407 408 409 410 411 412 413 414 415 416 417 418 419 420 421 422 423 424 425 426 427 428 429 430 431 432 433 434 435 436 437 438 439 440 441 442 443 444 445 446 447 448 449 450 451 452 453 454 455 456 457 458 459 460 461 462 463 464 465 466 467 468 469 470 471 472 473 474 475 476 477 478 479 480 481 482 483 484 485 486 487 488 489 490 491 492 493 494 495 496 497 498 499 500 501 502 503 504 505 506 507 508 509 510 511 512 513 514 515 516 517 518 519 520 521 522 523 524 525 526 527 528 529 530 531 532 533 534 535 536 537 538 539 540 541 542 543 544 545 546 547 548 549 550 551 552 553 554 555 556 557 558 559 560 561 562 563 564 565 566 567 568 569 570 571 572 573 574 575 576 577 578 579 580 581 582 583 584 585 586 587 588 589 590 591 592 593 594 595 596 597 598 599 600 601 602 603 604 605 606 607 608 609 610 611 612 613 614 615 616 617 618 619 620 621 622 623 624 625 626 627 628 629 630 631 632 633 634 635 636 637 638 639 640 641 642 643 644 645 646 647 648 649 650 651 652 653 654 655 656 657 658 659 660 661 662 663 664 665 666 667 668 669 670 671 672 673 674 675 676 677 678 679 680 681 682 683 684 685 686 687 688 689 690 691 692 693 694 695 696 697 698 699 700 701 702 703 704 705 706 707 708 709 710 711 712 713 714 715 716 717 718 719 720 721 722 723 724 725 726 727 728 729 730 731 732 733 734 735 736 737 738 739 740 741 742 743 744 745 746 747 748 749 750 751 752 753 754 755 756 757 758 759 760 761 762 763 764 765 766 767 768 769 770 771 772 773 774 775 776 777 778 779 780 781 782 783 784 785 786 787 788 789 790 791 792 793 794 795 796 797 798 799 800 801 802 803 804 805 806 807 808 809 810 811 812 813 814 815 816 817 818 819 820 821 822 823 824 825 826 827 828 829 830 831 832 833 834 835 836 837 838 839 840 841 842 843 844 845 846 847 848 849 850 851 852 853 854 855 856 857 858 859 860 861 862 863 864 865 866 867 868 869 870 871 872 873 874 875 876 877 878 879 880 881 882 883 884 885 886 887 888 889 890 891 892 893 894 895 896 897 898 899 900 901 902 903 904 905 906 907 908 909 910 911 912 913 914 915 916 917 918 919 920 921 922 923 924 925 926 927 928 929 930 931 932 933 934 935 936 937 938 939 940 941 942 943 944 945 946 947 948 949 950 951 952 953 954 955 956 957 958 959 960 961 962 963 964 965 966 967 968 969 970 971 972 973 974 975 976 977 978 979 980 981 982 983 984 985 986 987 988 989 990 991 992 993 994 995 996 997 998 999 1000 1001 1002 1003 1004 1005 1006 1007 1008 1009 1010 1011 1012 1013 1014 1015 1016 1017 1018 1019 1020 1021 1022 1023 1024 1025 1026 1027 1028 1029 1030 1031 1032 1033 1034 1035 1036 1037 1038 1039 1040 1041 1042 1043 1044 1045 1046 1047 1048 1049 1050 1051 1052 1053 1054 1055 1056 1057 1058 1059 1060 1061 1062 1063 1064 1065 1066 1067 1068 1069 1070 1071 1072 1073 1074 1075 1076 1077 1078 1079 1080 1081 1082 1083 1084 1085 1086 1087 1088 1089 1090 1091 1092 1093 1094 1095 1096 1097 1098 1099 1100 1101 1102 1103 1104 1105 1106 1107 1108 1109 1110 1111 1112 1113 1114 1115 1116 1117 1118 1119 1120 1121 1122 1123 1124 1125 1126 1127 1128 1129 1130 1131 1132 1133 1134 1135 1136 1137 1138 1139 1140 1141 1142 1143 1144 1145 1146 1147 1148 1149 1150 1151 1152 1153 1154 1155 1156 1157 1158 1159 1160 1161 1162 1163 1164 1165 1166 1167 1168 1169 1170 1171 1172 1173 1174 1175 1176 1177 1178 1179 1180 1181 1182 1183 1184 1185 1186 1187 1188 1189 1190 1191 1192 1193 1194 1195 1196 1197 1198 1199 1200 1201 1202 1203 1204 1205 1206 1207 1208 1209 1210 1211 1212 1213 1214 1215 1216 1217 1218 1219 1220 1221 1222 1223 1224 1225 1226 1227 1228 1229 1230 1231 1232 1233 1234 1235 1236 1237 1238 1239 1240 1241 1242 1243 1244 1245 1246 1247 1248 1249 1250 1251 1252 1253 1254 1255 1256 1257 1258 1259 1260 1261 1262 1263 1264 1265 1266 1267 1268 1269 1270 1271 1272 1273 1274 1275 1276 1277
```

1 

9、负载分担（可选项，当前8条选路原则仍然选不出最优路由，则此时可以选择将这些几乎相同的路由条目一起提交到路由表，实现等价负载。）

负载分担是路由表中负载分担，可以把前8条选路原则相同的路由提交到路由表，但是数据库当中仍然只会选择唯一的一条最优路由，也只会向邻居通告一条最优路由。

```
R1(config-router)#maxium-paths ?
```

<1-32> Number of paths

eibgp Both eBGP and IBGP paths as multipath

**条目数量..**

1bgp IBGP-multipath

//选择可以负载分担的BGP条目数量，//可以实现EBGP负载分担路由条目的数量//可以同时设置EBGP和IBGP负载分担的路由//可以设置实现IBGP负载分担的路由条目数目

10、针对于EBGP路由条目，越老越优。

哪怕由于11，12，13条选路原则应当选举最新收到的数据库条目，但是不会这么做，依然选择BGP表中尽可能靠下的稳定的路由条目。

**第十条选路原则在以下条件下不会生效：**

针对于IBGP邻居以及联邦中EBGP邻居不会生效。

针对于散了clearipbgp\*的路由器不会生效（大家都是重置BGP邻居最新学到的数据库条目，不能判断谁更稳定。）

针对于散了bgp deterministic-ned命令的路由器不会生效（散了该命令BGP表不再按照数据库条目接收顺序从新到旧排列了，而是按照最左侧的AS号分组排列，无法判断谁更老谁更新。）

使用了BGP Best-path compare-routerid的路由器（强制要求去比较第十一条选路原则，不考虑越老越优）

11、优选BGP Router-ID最小的路由条目

如果BGP路由经过了路由反射器反射，则进行比较时使用originator-ID代替Router-ID进行比较。

12、优选Cluster-ID长度短的路由条目。

13、优选Neighbor所指向的邻居地址最小的路由条目。

## Day 31-32：BGP综合实验中补充知识

可以直接修改与对方建立BGP邻居关系时Open消息中自身的AS号。

```
R5(config-router)#neighbor xxxx local-as 64513
```

定的AS号去建立。

既然假冒了AS就需要对别人负责，收到了EBGP路由条目时就会自动添加进去自己假冒的AS号。

```
R5(config-router)#neighbor xxxx local-as 64513 no-prepend
```

> 💡 收到路由时不添加假的AS号。

同步（Synchronization）

BGP当中的同步用于鼓励用户重分布或使用IGP协议的方式解决路由黑洞的方案。

默认关闭，一旦开启BGP同步，则最优路由的选举条件也将会发生变化，针对于BGP路由条目不受影响，只针对于IBGP路由条目有效。

当路由国收到了IBGP路由条目时，要求路由器的路由表中需要存在与当前IBGP路由条目完全一致的IGP协议路由，如果路由表中不存在该IBGP路由的IGP路由，则该IBGP路由永远不会成为最优路由，如果路由表中存在该IBGP路由的IGP路由，则只要满足以下条件，可以成为最优路由：

该IGP路由为OSPF协议的路径条目

该OSPF路由条目的Router-IO与接收到了IBGP路由条目的Router-IO一致，则该IBGP路由条目可以成为最优路由该OSPF路由条目的Router-IO与接收到的IBGP路由条目的Router-IO不一致，则该IBGP路由条目可以成为最优路由。

该IGP路由不是OSPF路由条目

如果IBGP路由条目的管理距离大于该IGP协议的路由条目管理距离，则该IBGP路由条目可以成为最优路由

如果IBGP路由条目的管理距离小于该IGP协议的路由条目管理距离，则该IBGP路由条目不可以成为最优路由。

OSPF使用Distance指令修改路由条目的管理距离：

```
R2(config)#access-list 1 permit 105.1.1.0 
R2(config)#router ospf 1 
R2(config-router)#distance 241 <Router-IO> <wildcardbits> <ACL> 
R2(config-router)#distance 241 5.5.5.5 0.0.0.0 1 路由修改管理距离241.
```

> 💡 匹配路由 //链路状态路由协议使用Router-ID //针对于Router-IO5.5.5.5通告的LSA计算得出的ACL1匹配的路

BGP使用Distance指令修改路由条目管理距离：

```
R2(config)#access-list 1 permit 105.1.1.0 
R2(config)#router bgp 235 
R2(config-router)#distance 241 <neighbor address> <wildcardbits> <ACL> 
R2(config-router)#distance 241 10.10.5.5 0.0.0.0 1 理距离241.
```

**BGP通告默认路由的方式：**

default-originate

```
R4(config)#router bgp 64512
```

```
R4(config-router)#neighbor 10.10.5.5 default-originate
```

**network宣告**

直接把路由表中的默认路由宣告进入到BGP。

```
R5(config-router)#network 0.0.0.0 mask 0.0.0.0
```

Redistribute

直接把路由表中默认路由重分布引入到BGP。

默认情况下，BGP不会允许将默认路由重分布引入到BGP。如果需要重分布引入默认路由进入BGP，需要多敲一句指令。

```
R5(config-router)#default-information originate
```

> 💡 开关，允许将IGP的默认路由重分布引入BGP.

**扩展访问控制列表匹配路由：**

access-list 100 permit ip

移除BGP路由条目中私有的AS-Path属性号码

```
R2(config-router)#neighbor x.x.x.x remove-private-as
```

**利用前缀列表过滤路由：**

```
R5(config)#ip prefix-list no-def permit 0.0.0.0/0 ge 1 le 32 
R5(config)#router bgp 235 
R5(config-router)#neighbor 10.10.2.2 prefix-list no-def out 
R5(config-router)#neighbor 10.10.3.3 prefix-list no-def out 
R5(config-router)#end
```

> 💡 利用前缀列表过滤掉默认路由。

**EBGP之间传递路由下一跳不变的方式：**

```
R5(config-router)#neighbor x.x.x.x next-hop-unchanged要求EBGP之间的邻居关系TTL≥2.
```

> 💡 向EBGP邻居通告路由时下一跳不变。

重分布BGP路由引入到IGP

默认情况下只能够重分布EBGP路由条目进入到IGP协议（OSPF，EIGRP）

```
R5(config)#router bgp 235
```

```
R5(config-router)#bgp redistribute-internal
```

> 💡 可以将IBGP路由重分布进入IGP协议。

WOLF-LAB 网络技术实验室

帮我识别每个PDF中的文字。所有文字都要识别输出，不要省略。不要总结。按照day日期大小进行排序

## Day 33：peer-group,listen range,address-family,BGP路由惩罚

针对多个BGP邻居采用相同的对等体配置时可以选择使用该技术。

```
R5(config)#router bgp 235
```

```
R5(config-router)#neighbor PEER peer-group
```

```
R5(config-router)#neighbor PEER remote-as 235
```

**于AS235**

```
R5(config-router)#neighbor PEER update-source Loopback0 loopback0作为更新源
```

```
R5(config-router)#neighbor PEER next-hop-self的路由下一跳变成自己。
```

```
R5(config-router)#neighbor 10.10.2.2 peer-group PEER与它建邻居将会使用其中命令
```

Listen range

正常情况下，路由器路由表中存在去往目标的明细路由，即可主动向对方发送BGP的连接请求。

当需要与多个BGP邻居建立关系时，且这些邻居所使用的配置也一致，即可使用listen range，listen range使用必须配置peer-group

```
R5(config)#router bgp 235
```

```
R5(config-router)#neighbor PEER peer-group
```

```
R5(config-router)#neighbor PEER remote-as 235于AS235
```

```
R5(config-router)#neighbor PEER update-source loopback0 loopback0作为更新源
```

```
R5(config-router)#neighbor PEER next-hop-self的路由下一跳变成自己。
```

```
R5(config-router)#bgp listen range 10.10.0.0/16 peer-group PEER的地址向自身发送的BGP邻居关系请求，并且默认此类地址都属于PEER-group PEER对等体组的邻居，采用对等体组当中的命令行。
```

不会主动发送BGP邻居关系请求，只能够被动收到邻居请求做出回复。

Address-family（地址簇） 多进程的BGP。

全局BGP：no address-family情况下的BGP。

router bgp 235neighbor 10.10.5.5 remote-as 235neighbor 10.10.5.5 update-source Loopback0neighbor 10.10.5.5 next-hop-self

address-family情况下的BGP。

router bgp 235neighbor 10.10.5.5 remote-as 235neighbor 10.10.5.5 update-source Loopback0

address-family IPv4中，调整IPv4的BGP邻居关系属性neighbor 10.10.5.5 activate（默认自动激活IPv4的BGP邻居）

关闭自动激活IPv4的BGP邻居）

neighbor 10.10.5.5 next-hop-self

BGP 路由惩罚机制（Dampening）

BGP的路由在AS与AS之间传递，如果一条BGP路由不断翻动，所影响到的不知自身一个AS，而是全局下的多个AS的BGP路由。

仅针对于EBGP的路由条目有效，IBGP的路由条目无法启用BGP路由惩罚机制。

惩罚值：当一条BGP路由每翻动一次，则路由条目的惩罚值+1000。惩罚值不能够被改变

半衰期：路由条目每隔一段时间没有再次翻动，则惩罚值自动降低一半。默认15分钟

抑制门限：当BGP的路由条目惩罚值到达抑制门限时，则该BGP路由条目将会被置为抑制状态，不会被提交到路由表，也不会传递给邻居。默认2000

重门限：当被抑制的BGP路由条目惩罚值降低到低于重门限时，该BGP路由条目将重新被使用，可以提交到路由表，可以传递给BGP邻居。750

最大抑制时长：相当于惩罚值的上限，如果惩罚值始终无上限，则一条不断翻动的BGP路由稳定之后要等待特别长的时间才能重新投入使用，因此设计最大抑制时长，一条BGP路由默认的最大惩罚值（12000），默认最大抑制时长为60分钟

```
R5(config)#router bgp 5
```

一旦一条路由条目超时了一次，则立刻将次路由条目置为h（history），认为该数据库条目不稳定，不会将其提交到路由表，但是数据库条目照样保留，同时也没有立刻向邻居发送update通告该路由条目不可用。

一旦一条路由条目惩罚值超过了抑制门限，则立刻将该BGP路由置为d（damped）状态，不将其提交到路由，不将其传递给BGP邻居，且只有惩罚值低于了重门限才会重新使用。

```
R5#show ip bgp dampening dampened-paths
```

```
R5#show ip bgp dampening flap-statistics
```

```
R5#clear ip bgp dampening
```

> 💡 查看所有被BGP惩罚机制抑制的路由

//查看BGP路由惩罚路由条目的翻动情况。

//清空所有抑制的BGP路由，并且惩罚值归零。

针对于单一路由开启BGP dampening并且设置其独特的惩罚参数

> 图片内容：配置命令

ip prefix-list A seq 5 permit 104.1.1.0/24 //匹配上需要路由惩罚的路由。

route-map DAM permit 10

match ip address prefix-list A

set dampening 10 750 2000 40 //设置其惩罚参数。

router bgp 5

bgp dampening route-map DAM //在BGP当中开启路由惩罚并调用route-map。

针对于单一路由设置特殊的BGP dampening参数，其它路由也开启BGP dampening

> 图片内容：配置命令

ip prefix-list A seq 5 permit 104.1.1.0/24 //匹配上需要路由惩罚的路由。

route-map DAM permit 10

match ip address prefix-list A

set dampening 10 750 2000 40 //设置其惩罚参数。

route-map DAM permit 20 //其它路由也开启BGP dampening

router bgp 5

bgp dampening route-map DAM //在BGP当中开启路由惩罚并调用route-map。

其它路由某一种BGP dampening参数，某一个单一路由特定的BGP dampening参数

> 图片内容：配置命令

ip prefix-list A seq 5 permit 104.1.1.0/24 //匹配上需要路由惩罚的路由。

route-map DAM permit 10

match ip address prefix-list A

set dampening 10 750 2000 40 //设置其惩罚参数。

route-map DAM permit 20 //其它路由也开启BGP dampening

set dampening 15 750 2000 50

router bgp 5

bgp dampening route-map DAM //针对于route-map匹配的路由开启BGP dampening，未设置参数的路由按照全局惩罚机制参数(15 750 2000 50),route-map中设定特殊参数的路由则(10 750 2000 40)。

## Day 34：BGP的重分布专题

**重分布定义：**

把某一个路由协议的数据库条目以 外部路由 的形式导入到另一个动态路由协议的数据库中，称之为重分布。

入多随信：当把某一个协议的数据库条目重分布引入到另一个协议时，需要对其设置初始的Metric值。因为不同协议计算路由条目Metric值的方式是不一致的。

只有提交到路由表的数据库条目才会被重分布（当A协议重分布引入到B协议时，被A协议的network命令所包括但未被B协议的network命令包括的直连路由的数据库条目也会被重分布。）

在哪一台路由器上做重分布就看哪一台路由器的路由表。

总结双点双向重分布次优路径的出现规律。

RIP < - - - > EIGRP 没有次优路由 EIGRP < - - - > OSPF 没有次优路由 RIP < - - - > OSPF 有次优路由

当进行双点双向或多点多向重分布时，如果将管理距离大的数据库对应路由条目引入到管理距离小的动态路由协议当中时，容易产生次优路径。

**解决双点双向的次优路径**

**·过滤（利用tag值。）**

> 图片内容：配置命令

```
R1(config)#router ospf 1
R1(config-router)#redistribute eigrp 90 subnets tag 100 //一重分布时可以设置tag标签。
R3(config)#route-map deny_tag deny 10 //创建route-map命名为deny_tag，行为deny,序列号为10的语句
R3(config-route-map)#match tag 100 //匹配上tag100的路由
R3(config-route-map)#exit
R3(config)#route-map deny_tag permit 20 //针对于其它路由放行，书写序列号为20的空节点
R3(config-route-map)#exit
R3(config)#router ospf 1
R3(config-router)#distribute-list route-map deny_tag in //在OSPF中调用route-map工具进行路由过滤
```

·改管理距离。（不能使用tag...只能用ACL一个个匹配需要调整的路由条目。）（比过滤的方法多了一点冗余性。）

> 图片内容：配置命令

```
R1(config)#access-list 1 permit 10.10.2.0 //利用acl匹配上需要修改管理距离的路由
R1(config)#router ospf 1
R1(config-router)#distance 171 3.3.3.3 0.0.0.0 1 //针对于3.3.3.3通告的该路由条目修改管理距离171。
```

## Day 35：PBR(Policing-based Pouting)

利用策略路由工具，调整 数据流量 的转发方向，优先于路由表转发， 是一种非常有效的引流工具，可以将特定的数据流量设定特定的转发途径， 两种工具： ACL：访问控制列表 标准的ACL：匹配某一个用户发送出去的所有协议所有目的地址的数据流量 扩展的ACL：匹配某一个用户访问某一个地址特定协议的数据流量， route-map工具：针对于数据流量做操作= PBR， 使用route-map设定数据流量的下一跳时，不可以指定非直连的下一跳地址 如果PBR指定的下一跳对应的直连路由丢失，则默认该PBR失效，正常按照路由表转发，

> 图片内容：配置命令

access-list 1 permit 10.10.5.5 //利用acl1匹配上10.10.5.5发送给任何目的地址的所有数据流量

route-map PBR permit 10 //创建route-map命名为PBR并指定行为动作是放行,序列号10的语句

match ip address 1 //针对于ACL1匹配的数据流量

set ip next-hop 1.1.34.3 //设置这些数据流量的下一跳方向是1.1.34.3。

interface g0/2

ip policy route-map PBR //在收到数据流量的接口上调用PBR，优先于路由表进行策略转发

> 图片内容：配置命令

```
R4(config)#access-list 100 permit ip host 10.10.5.5 host 10.10.2.2
R4(config)#route-map PBR permit 10
R4(config-route-map)#match ip address 100
R4(config-route-map)#set ip next-hop 1.1.34.3
R4(config-route-map)#exit
R4(config)#interface g0/2
R4(config-if)#ip policy route-map PBR
R4(config-if)#end
```

> 图片内容：配置命令

access-list 100 permit ip host 10.10.5.5 host 10.10.2.2

route-map PBR permit 10

match ip address 100

set ip next-hop 1.1.34.3

set ip next-hop verify-availability //开启Cisco内部的下一跳可达性校验。

使用Cisco的CDP(cisco discovery protocol)协议。

默认Cisco设备运行CDP协议，一旦接口开启则会每隔60s向外发送自身的个人信息。超过180s收不到邻居的消息则认为邻居故障。

show cdp neighbors //查看Cisco的CDP邻居表。

> 图片内容：配置命令

```
R4(config)#ip sla 1 //创建1号探针
R4(config-ip-sla)#icmp-echo 1.1.34.3 source-interface g0/0 //选择使用ICMP协议周期性探测1.1.34.3的可达性。
R4(config-ip-sla-echo)#frequency 10 //修改探针的探测间隔时间，此处为10s
R4(config-ip-sla-echo)#threshold 400 //超过多少时间收不到回复认为探测失败，此处为400毫秒。
R4(config-ip-sla-echo)#timeout 500 //设定整个探测的总时长限制。
R4(config)#ip sla schedule 1 start-time now life forever //设定探针现在开始工作并且永远工作下去。
R4(config)#track 1 ip sla 1 reachability //创建一号跟踪项目跟踪探针的最终结果。
R4(config)#access-list 100 permit ip host 10.10.5.5 host 10.10.2.2
R4(config)#route-map PBR permit 10
R4(config-route-map)#match ip address 100
R4(config-route-map)#set ip next-hop verify-availability 1.1.34.3 1(第一个下一跳) track 1(跟踪的Track项目编号) //设定数据流量的第一个下一跳为1.1.34.3,并且启用track工具,当Track工具跟踪的内容为up,则认为该下一跳可以使用,当Track工具跟踪的内容为down,则认为该下一跳不可使用。
```

默认情况下SLA的探测周期为60s，意思是每隔60s发送一次探测。

1. 
R2(config)#access-list 100 permit ip host 10.10.2.2 host 10.10.5.5 2 
R2(config)#route-map PBR permit 10 3 
R2(config-route-map)#set ip next-hop 1.1.23.3 4 
R2(config-route-map)#match ip address 100 5 
R2(config-route-map)#exit 6 
R2(config)#ip local policy route-map PBR 量做PBR.

**路由器的转发机制：**

当路由器从接口收到数据包，拆开数据链路层查看网络层2. 根据目的IP地址查询路由表3. 依据最长匹配，递归查询的原则找到对应的路由4. 将数据包重新封装5. 将封装好的数据包从路由对应的出接口转发出去。

WOLF-LAB 网络技术实验室

---

# 四、组播与 IPv6 基础

> 组播协议与 IPv6 地址体系

## Day 36-39：组播引入,组播地址规划,组播MAC地址,IGMP

**组播专题-day1.**

**组播的优势：**

发送同一个消息给多个接收方时可以使用组播。- 优化了带宽的使用- 减少主机和路由器的进程- 不需要知道接收方的IP地址。- 尽可能使得接收方同时收到数据消息。

**缺点：**

尽可能传输- 没有流控- 容易收到重复的数据包- 不像TCP可以按照顺序传输。（无序传输）

**组播的模型：**

源段：从组播源到第一跳路由器之间的部分称之为源段。（在服务器或主机上运行的应用程序发送组播的数据流量到路由器上的距离。）不需要学

组播分发树：组播的数据流量传递的途径。

运行组播的动态路由协议来使得路由器知晓组播数据流量的转发方向。（IP）

接收段：最后一跳路由器与组播客户端（负责加入组播组接收数据流量的设备）之间的部分。

将会运行组播接收段的特殊协议（IGMP），使得最后一跳路由器管理组成员的加组和离组情况。

**组播的地址规划：**

组播的地址范围是：224.0.0.0→239.255.255.255

224.0.0.0/24 - Link-local Multicast→224.0.0.0→224.0.0.255 链路上需要用到组播的协议保留使用了。

链路上所有的节点 224.0.0.1

链路上所有的路由器 224.0.0.2

RIP 224.0.0.9

EIGRP 224.0.0.10

OSPF 224.0.0.5/224.0.0.6

224.0.1.0/24 - 224.0.1.0→224.0.1.255→专用于某些特殊协议使用的组播地址范围（例如NTP）

232.0.0.0/8 - 232.0.0.0→232.255.255.255→专用于特定源组播使用的IPv4组播地址范围。

233.0.0.0/8 - 233.0.0.0→233.255.255.255→买AS号赠送的公有组播IPv4地址。

AS号：16个bits表示AS范围1- 65535

例如，公司的AS号是24。 00000000000110000

0 24

公司因为AS号是24，所以可以被分配到233.0.24.X→233.0.24.0→233.0.24.255都是给你这个AS使用的组播地址范围。

239.0.0.0/8 - 239.0.0.0→239.255.255.255→私有组播地址范围。企业内部随便用。

https://www.iana.org/assignments/multicast-addresses/multicast-addresses.xhtml#multicast-addresses-3

如果需要了解其它点击上列网址。

**组播MAC地址运算方式**

口决 01005E 0 01005E0

**十六进制 二进制**

例如：有组播地址 239.1.1.1。

MAC地址：共48个bits，12个十六进制数。

前6个十六进制数写成 01:00:5E

后6个十六进制数写成【（二进制数8开头） 

  （组播IPv4地址的最后23个bits）】 

⟹

⟹ 转换成为6个十六进制数。

11101111.0 0000001.00000001.00000001 239.1.1.1

00000001.00000001.00000001

00000001 00000001 00000001

因此，组播IPv4地址239.1.1.1的组播MAC地址为 01:00:5E:01:01:01

使得最后一路路由器了解到所连接的主机成员加组情况以及离组情况，以判断是否需要向组播组成员下发组播的数据流量。

对于最后一跳路由器来说，只需要在于是否有成员加入了组播组，组播组当中究竟有多少个组成员没有任何的参考必要，只有两种情况

组播组当中有成员，那么最后一跳路由器如果收到了该组播组的数据流量，则需要下发

组播组当中没有组成员，那么最后一跳路由器如果收到了该组播的数据流量，则直接丢弃。

IGMP协议就是最后一跳路由器用来判断自己所接入的链路上是否有成员加入组播，是否需要组播数据流量的过程。

IGMPv1

**包含的消息类型：**

Report消息：当成员加入组播组时，将会立刻连续发送两次Report消息，目的IP地址将会是自己所加入的组播IPv4地址，目的MAC地址也是组播的IPv4地址对应的组播MAC地址。发送IGMPv1的报告消息表明自己加入了该组播组。希望接收到该组播组的数据流量。

当组成员收到Query消息时，将会立刻开启一个以秒为单位的10秒钟以内的倒计时，倒计时优先结束的路由器将会优先发送Report，其它该组的组成员设备将不会再回复Report消息，因为已经有组成员回复Report了。回复Report消息的设备将会连续发送两次Report消息进行回复，告知最后一跳路由器自己还在组里

Query消息：当最后一跳路由器知晓自己所连接的链路上有组播组以及组播组成员时，将会开始每隔60s下发一次Query消息，目的IP地址224.0.0.1（发送给链路上的所有节点，包括路由器，PC，服务器，AP...）目的MAC地址为224.0.0.1对应的MAC地址，进行组播组查询。查询组播组当中是否还有组成员，自己是否还需要继续下发该组播组的数据流量。

成员离组时将会选择悄味味离开小组，不会告诉最后一跳路由器自己离组了，最后一跳路由器发送Query消息查询成员情况时收不到回应，需要连续三次Query都没有成员发送Report才会认为该组播组当中没有任何成员，不再需要下发数据流量。

```
R1(config)#interface g0/0
```

```
R1(config-if)#ip igmp version 1
```

```
R1#show ip igmp groups
```

> 💡 让路由器连接主机的接口运行IGMPv1。

**//查看组播组成员情况**

表中当只记录下组播组当中最后一个发送Report消息的设备IPv4地址。路由器只需要知道该组播组当中至少有一个组播组成员即可。

```
R2(config)#interface g0/0
```

```
R2(config-if)#ip igmp version 1
```

```
R2(config-if)#ip igmp join-group 224.1.1.1
```

> 💡 运行IGMPv1

//成员加入组播组224.1.1.1

IGMPv2

Report消息：当成员加入组播组时，将会立刻连续发送两次Report消息，目的IP地址将会是自己所加入的组播IPv4地址，目的MAC地址也是组播的IPv4地址对应的组播MAC地址。发送IGMPv2的报告消息表明自己加入了该组播组。希望接收到该组播组的数据流量。

当组成员收到Query消息时，将会立刻开启一个以8.1秒为单位的10秒钟以内的倒计时，倒计时优先结束的路由器将会优先发送Report，其它该组的组成员设备将不会再回复Report消息，因为已经有组成员回复Report了。回复Report消息的设备将会连续发送两次Report消息进行回复，告知最后一跳路由器自己还在组里面。

Query消息：当最后一跳路由器知晓自己所连接的链路上有组播组以及组播组成员时，将会开始每隔60s下发一次Query消息，目的IP地址224.0.0.1（发送给链路上的所有节点，包括路由器，PC，服务器，AP...）目的MAC地址为224.0.0.1对应的MAC地址，进行组播组查询。查询组播组当中是否还有组成员，自己是否还需要继续下发该组播组的数据流量。

**提升：**

收到Query消息后主机回复Report不再开启以秒为单位的倒计时，而是以0.1秒为单位。

引入了查询者选举，当出现了两个及以上最后一跳路由器时，不会让所有最后一跳路由器都去进行Query消息的发送，它们将会比较选举出查询者来负责发送Query消息进行查询，其它路由器则只负责倾听Report。

查询者选举机制： 比较最后一跳路由器在接收段链路上的接口IP地址，最小的将会成为查询者路由器。

```
R2#show ip igmp interface g0/0
```

> 💡 可以查看到IGMPv2的接口

**链路情况（包括查询者）**

如果连续三次（188s）收不到当前查询者所发送的Query消息，则认为当前查询者挂了，则重新选举新的查询者。

DR是可以抢占的，不像OSPF中的DR那么重要。

IGMPv1中其实也有查询者，当存在多个最后一跳路由器只有一台路由器（查询者）负责发送查询消息，只不过IGMPv1的查询者不是通过IGMP协议选举的，而是通过PIM协议选举的，PIM协议中所选举的DR的角色将会作为IGMPv1的查询者来负责Query。

3.Leave Message（离组消息）：新增消息

在IGMPv1中成员离组将会悄悄地离开，查询者路由器不清楚组播组当中是否还有成员，需要连续三次Query没有回复才会讲组播组删除，才会停止发送组播的数据流量。

在IGMPv2中，成员一旦离开组播组（最后一个发送Report消息的组成员），将会立刻向224.0.0.2发送Leave Message，告知最后一跳路由器自己离组了。

Group-Specific Query（特定组查询消息）：新增消息。

当查询者收到了成员的Leave Message时，将会立刻发送连续两次的特定组查询消息，目标IP地址则是所接收到的离组消息的成员所离开的组播组地址，询问该组播组当中是否还存在组播组成员，以此来判断后续是否需要继续发送该组播组的数据流量。

> 图片内容：组播分发树图

**组播分发树：**

**树模型：**

源树（最短路径树） ---> Dense mode

共享树 ---> sparse mode

**源树（最短路径树）**

被称之为（Push）模型。

在源树模型中，路由器一旦收到了组播源发送给组播组的数据流量时将会产生组播的路由条目，路由器会认为该组播数据流量对应的组播路由条目所有除了收到数据流量的接口之外其它的接口都会弹出接口，将组播数据从这些接口都转发出去。

组播的数据流量将会发到全网。

从最后一跳路由器开始，当最后一跳路由器发现不需要组播数据流量时，将会直接向上游发送 Prune（修剪）消息，希望不要再向自己发送组播数据流量。上游收到该修剪消息时，将会回复ACK消息，之后将会收到该修剪的接口修剪掉，不再将该接口发送出去组播的数据流量。

最终被修剪之后的组播数据流量的传送途径将是单向的最短转发途径。

当已经搭建完成源树之后，最后一跳路由器一旦接收到新的成员加组信息（report），则会立刻向上游发送 Graft（嫁接）消息，希望上游可以向上自己下发该组播组的数据流量。

· 如果网络较为庞大，则流量浪费严重，安全性问题较为严重。

· 路由器一旦接收到组播数据流量就会立刻产生组播的路由条目（S，G）表项，该表项的老化时间为180s。

· 为了保证源树是绝对最优，组播数据流量会每隔180s一次泛洪，则路由器的（S，G）表项，最新修剪出最优路径。

· 如果有多个组播源，则比较占用设备的资源，安全性更严重。

**RPF校验：**

防止路由器收到重复的组播数据包使用的方式。

路由器收到组播数据包时必须要先确认从哪里接受组播所使用的接口，如果不是从唯一接口接收数据包。

当路由器收到组播数据包，查看到数据包的IP源地址，根据源IP地址查找到自己的路由表，自己去往组播源对应的出接口是谁，判断自己去往组播源使用的接口是否是收到组播数据流量的接口，是则接收数据流量，不是则丢弃数据流量。

RPF校验每5分钟自动检测一次，确保RPF的接口结果是正确的。

如果出现丢去往组播源的路由条目动荡的情况，则有可能会以IGRP包，从而造成本设备的IP地址更改，重新校验出新的接口IP地址。大多的情况

**共享树模型：**

称之为PULL（拉）模型。

从接收段出发寻找到共享树，建立共享树模型组播数据流量的转发路径。

引入了RP（Rendezvous Point）结合点，共享树模型中，组播的数据流量先发送到RP，再由RP将组播的数据流量下发到接收段。

**RP的选举方式：**

· 手工指定RP（但是冗余性比较低。）

· Auto-RP（Cisco私有的动态选举RP的技术 224.0.1.39 224.0.1.40）

· BSR（PIM中自动选举RP的方式，公有）

在共享树模型当中，所有的路由器都必须知道RP的IP地址，（大家都要知道在哪里集合。）

最后一跳路由器一旦知道RP信息就会产生（，G）的表项，此时路由器会查询RP的信息的端口将会成为出接口，意思是往后一旦收到该组播组的数据流量直接收到report消息的接口发出。

最后一跳路由器一旦产生（，G）的表项，则立刻开始RPF校验指向RP集合点，找到去往RP的出接口，去往RP的方向发送 Join 消息，告知沿途的路由器（直到RP），往后去往该组播组的数据流量应当往自己这个方向转发。

第一跳路由器收到了组播源发送的组播数据包时，将会产生（S，G）的组播路由表项，但是组播数据包不会直接发送，路由器会将该组播数据包封装在单播数据包当中，通过单播的方式将数据包发送给RP集合点。这个包含组播数据包的组播数据包称之为（register）注册消息。

RP集合点收到了第一跳路由器由转发过来发送的组播数据包，将会做两件事：

RP因为之前已经收到了（，G）的表项，知道组播数据流量的转发方向，如今收到了组播数据包直接将数据包按照（，G）表项的出接口直接发送。

RP由于知道了组播源的IP地址，则直接RPF校验向组播源，直接去往组播源的出接口，去往组播源的路由上发送 Join 消息，告知沿途的路由器，往后接收到该组播源去往该组播组的数据流量，直接往RP的方向转发。

当第一跳路由器在接收到来自于第一跳路由器的 Join消息之前，收到组播数据包都会采用封装到单播数据包当中转发给RP的方式（不知道组播数据包的发送路径）。[第一跳路由器接收到来自于第一跳路由器发来的Join消息，则RP会接收组播数据包来发送，此时第一跳路由器会将组播数据包封装到单播数据包，以及直接发送组播数据包，两种的方式同时进行。

当RP能够通过组播的方式连接到来自于第一跳路由器发送来的组播数据包，而不是通过单播数据包，则RP将会给第一跳路由器发送（register-stop）消息，一旦第一跳路由器收到了 register-stop 消息，则会停止使用组播封装到单播数据包发送的方式，而是始终使用组播路由表直接发送消息。

路由器由组播信息时，RPF校验指向RP，知道了组播源的地址时，RPF校验指向组播源。

PIM(protocol independent Multicast):

Hello包：发现、建立、维护PIM邻居关系。一旦激活接口运行了组播，则路由器将会默认每30s发送一次PIM的Hello包，建立PIM邻居关系，如果超过3.5*30（105s）没有收到邻居的Hello包，则认为邻居出故障，断开PIM的邻居关系。

只运行PIM协议，则路由器的端口链路上就需要选举DR的角色在Dense-mode中，DR将不具备任何作用在Sparse-mode中，只有DR所在的路由器可以发送组播数据流量，可以发送Join等消息。

Dense-mode（源树模型）

Rx(config)#ip multicast-routingRx(config)#interface range g0/0,g0/1Rx(config-if-range)#ip pim dense-modeRx#show ip mroute

//开启路由器的组播路由功能

//使得设备的端口运行组播动态路由协议PIM//查看组播的路由表。

一旦产生（S，G）表项，只要组播的数据流量始终在发送，哪怕所有端口已被prune，没有任何出接口，但是每隔180s，就会把所有的prune端口打开再一次全网泛洪数据流量重新修剪。

（1.1.56.6，239.1.1.1），00:04:21（该组播条目一共存在的时间）/00:02:28（该组播路由条目生存时间）[默认倒计时3分钟]，flags：1Incoming interface: GigabitEthernet0/2, RPF nbr 0.0.0.0Outgoing interface list: GigabitEthernet0/1, Forward/Dense, 00:01:21（上一次该端口泛洪修剪过后的计时时间）/stopped（目前组播数据流量暂停，也可以是记录下次泛洪的倒计时）

（S，G）的表项始终都会存在一个倒计时（不记数据流量是否发送或停止）默认180s（三分钟），只要180s倒计时结束则该组播的（S，G）表项将会自动老化，但是如果组播数据流量仍在发送，则该时间将会被重置，如果组播数据流量早已停止，则该（S，G）表项直接老化删除。

当路由器收到组播数据流量产生（S，G）表项的同时也会产生（\*，G）的表项，但是该表项在Dense-mode中没有什么作用。

表示本路由器有哪些端口可以转发该组播组的数据流量。

便于切换到Sparse-mode。

当该组播组的（S，G）表项老化之后，再等待180s，则该行生物（\*，G）的表项将会删除。

**前转者选举**

当同时存在多个最后一跳路由器时，由于所有的最后一跳路由器都能够收到成员的Report消息，都认为需要下发组播的数据流量，当所有最后一跳路由器都发送时将产生重复的数据包，因此，在PIM的Dense-mode中，最后一跳路由器当中将会选举前转者路由器（在接收段的链路上通过ASeret消息），只有成为前转者的最后一跳路由器可以负责下发组播的数据流量，其它最后一跳路由器将会发送修剪，不去下发组播的数据流量。

比较去往组播器的路由条目管理距离（小的优先）

比较去往组播器的路由条目Metric值（小的优先）

比较接收段链路上设备的接口IP地址（大的优先）

比较去往组播器的路由条目管理距离（小的优先）2. 比较去往组播器的路由条目Metric值（小的优先）3. 比较接收段链路上设备的接口IP地址（大的优先）

clear ip mroute \*

//清除组播的路由表。

Sparse-mode（共享树模型）

引入了RP（RendezvousPoint）集结点，共享树模型当中，组播的数据流量先发送到RP，再由RP将组播的数据流量下发到接收段。

**RP的选举方式：**

手工指定RP（但是冗余性比较低。）Auto-RP（Cisco私有的动态选举RP的技术224.0.1.39 224.0.1.40）BSR（PIM中自动选举RP的方式，公有）

在共享树模型当中，所有的路由器都必须知道RP的IP地址，（大家都要知道在哪里集合。）

```
R2(config)#ip multicast-routing
```

```
R2(config)#interface range g0/0,g0/1
```

```
R2(config-if-range)#ip pim sparse-mode
```

> 💡 运行组播路由功能。

//接口运行PIM的Sparse-mode。

手工指定RP。

每一个运行组播的路由器都需要配上静态RP的命令行，手工告知路由器RP是谁，

一般情况下选择loopback口作为RP集结点，并且loopback接口需要运行组播。

RX(config)#ip pim rp-address 10.10.4.4

RX#show ip pim rp mapping

```
R2#show ip pim neighbor
```

> 💡 告知路由器RP的地址为10.10.4.4。

//查看本路由器所绑定的RP表项。

//检查PIM组播路由器协议邻居关系。

1 手工指定RP的负载分担 2 
R2(config)#access-list 1 permit 239.1.1.1 3 
R2(config)#access-list 2 permit 239.2.2.2 4 
R2(config)#ip pim rp-address 10.10.2.2 1 5 
R2(config)#ip pim rp-address 10.10.3.3 2 6 
R2#show ip pim rp mapping 7 PIM Group-to-RP Mappings 8 Ac1: 1, Static 9 RP: 10.10.2.2 (?) 10 Ac1: 2, Static 11 RP: 10.10.3.3 (?) 12 
R2# 的RP, 10.10.3.3成为ACL2的RP.

**共享树切换到源树：**

默认开启，从最后一跳路由器出发，当最后一跳路由器得知了组播源之后，RPF校验指向组播源，向组播源对应的方向发送Join消息，使得组播的转发途径从共享树切换到源树。

（之前房东与租客之间需要房产中介，当租客和房东认识后，则租客直接找房东交谈。）

> 图片内容：配置命令

```
R3(config)#ip pim spt-threshold ?
```

0 Always switch to source-tree //开启共享树切换到源树

infinity Never switch to source-tree //始终使用共享树

如果关闭了切换，则路由器将不会产生组播的（S，6）路由表项。

（\*，6）的表项将会删除"J：JoinSPT"

**查询者：**

接收段。IGMPv2，v3协议。

当出现多个最后一跳路由器，只有查询者会负责向客户端发送Query消息（6s），定期查探下方成员是否还在组播组。

**选举方法：**

接收段链路上IP地址小的路由器成为查询者路由器

如果是IGMPv1协议不会自动选举查询者，由PIM协议中选举出的DR来担任接收段的查询者

**前转者：**

仅在PIM Dense-mode中有效。Sparse-mode中无效

当接收段出现多个最后一跳路由器只能有一个设备下发组播数据流量，在接收段上需要选举前转者，只有前转者下发Dense-mode中的组播数据流量。

**选举方法：**

比较去往组播源的路由条目管理距离（小的优先）

比较去往组播源的路由条目Metric值（小的优先）

比较接收段链路上设备的接口IP地址（大的优先。）

**DR:**

show ip pim interface g0/0

//检查接口链路上的DR是谁。

当接收段存在多个最后一跳路由器时，都产生了（\*，6）的表项，此时只有DR所在的路由器会向RP发送Join消息告知RP组播组的数据流量对应的转发途径。只有DR路由器能够下发组播的数据流量。

**选举方式：**

DR Priority：DR的优先级（默认是1级）

优先级越大越优先。

```
R2(config)#interface g0/0
```

```
R2(config-if)#ip pim dr-priority 100
```

> 💡 修改接口上的DR优先级。

接口地址最大的路由器成为DR。

**RP:**

集合点，仅在PIM Sparse-mode中有用。

在Sparse-mode中，组播数据流量发送到RP，再有RP下发到接收段。

## Day 40：PIM Sparse-mode中动态选举RP的方式(AutoRP,BSR)

**新角色**

C-RP:RP候选者 （班长候选人）

MA(Mapping-Agent):映射代理路由器。 （班主任（小学））

**如何选举C-RP/MA**

C-RP和MA由路由器的管理器，管理员可以随意指定任意设备的接口地址成为C-RP或MA。

C-RP将会提交自己的参选信息给MA

C-RP将会把自己的个人信息发送给224.0.1.39组播地址（周期性：60s）

一旦指定一台路由器成为MA，其所有运行组播的接口将会自动加入组播组地址224.0.1.39能够接收到C-RP发送的参选信息。

需要选举RP - - - - - - - - - - - - - - - - - - - - C-RP将组播数据流量发送给224.0.1.39 - - - - - - - - - - - - - - - - - - - - 如果C-RP没有跟MA直连，需要经过路由器转发，而Sparse-mode中路由器如果需要转发组播的数据包，需要先将其发送给RP - - - - - - - - - - - - - - - - - - - - 但是现在没有RP。

因此，如果需要运行auto-rp自动选举RP协议必须再多运行一些命令来进行补充

**方法一：**

全网不再运行PIM Sparse-mode，而全部修改为Sparse-dense-mode。

先通过dense-mode选举出RP，再运行有RP的Sparse-mode。

所有的路由器一旦收到了C-RP发送给224.0.1.39的组播数据流量都会优先洗，肯定能够泛红到MA上，使得C-RP的

参选信息能够发送到MA，最终选举好了RP之后再切换会Sparse-mode。

不使用的原因： 其有了dense-mode的缺点。 泛洪（不安全，占用资源等等）；被第二种方式代替

**方法二：**

不需要更改Sparse-mode的运行方式，而是所有的路由器都缺一命令行：

ip pin autorp listener 所有的路由器针对于C-RP发送的224.0.1.39以及MA发送的224.0.1.40数据流量都默认采用Dense-mode的工作方式，其它的组播数据流量照常使用Sparse-mode

MA将选举的RP结果下发到整个网络的所有路由器，告诉大家RP基础

MA将会把选举结果发送到224.0.1.40组播组地址。（只要运行组播的路由器默认都会加入到该组播组地址- - - - - - - - - - - - - - - - - - - - - 仅限Cisco路由器。ip

pinautorp)

MA会选择C-RP中IP地址最大的路由器成为RP。

MA会每隔60s时间将RP的选举结果从所有运行组播协议的端口发送出去。

MA如果间隔180s都收不到当前RP发送的参选信息，则认为当前的RP故障，则重新从C-RP中选举一个新的RP进行通告

播

TTL=10.

ip pin send-rp-discovery loopback 0 scope 10

ip pin send-rp-discovery loopback 0 scope 10

ip pin send-rp-discovery loopback 0 scope 10

MA可以存在多个，但是不冲突，因为MA选举的结果是一致的，但是因为都在工作，缺乏主从关系

```
R2(config)#access-list 1 permit 239.1.1.1
```

组播组的C-RP。

默认情况下Cisco的设备动态RP的选举优先于静态的RP选举

```
R2(config)#access-list 1 permit 239.1.1.1
```

```
R2(config)#ip pin rp-address 10.10.3.3 1 override
```

用动态RP。

BSR(bootstrapp Router):自选路由器

**引入两个角色：**

C-RP: RP候选者 （班长候选人）

C-BSR: BSR候选者 （班主任（大学））

从C-BSR中可以选择出Active BSR（主班主任）其它的C-BSR作为备份

Active BSR的选举方式

比较各个C-BSR的优先级，大的成为Active BSR。（默认优先级都为0）

比较各个C-BSR的IP地址大小，大的成为Active BSR

所有的C-BSR将会把自己的参选信息发送给224.0.0.13PIMv2的组播地址（每60s）。

Active BSR将会每隔60s项所有的运行组播的端口发送自己的角色声明。

```
R5(config)#ip pim bsr-candidate loopback 0 32 //指定路由器的loopback0地址作为C-BSR
R4(config)#ip pim bsr-candidate loopback 0 32 160 //修改BSR的优先级。Hash掩码：控制了BSR针对于组播组选举RP负载分担的严格/稀松情况。
R2(config)#ip pim rp-candidate loopback 0 //使得路由器的loopback0地址成为C-RP。C-RP将会周期性地向Active BSR单播发送参选信息(60s)，hold时间(150s)，Active BSR一旦超过150s收不到C-RP的参选信息则认为其故障。1. 比较C-RP的优先级，小的成为组播组地址的RP（默认情况下所有C-RP的优先级都为0）ip pim rp-candidate loopback 0 priority? //调整C-RP的优先级。
R2(config)#ip pim rp-candidate loopback 0 interval? //调整C-RP发送消息的周期时间。hold时间默认2. 比较HASH值大小，大的优先。HASH(Group-address组播组地址，HASH MASK,C-RP Address候选者RP的IP地址)，HASH值大的成为组播地址的RP。show ip pim rp-hash a.b.c.d //查看不同组播组的HASH结果。BSR可以自带组播地址RP的负载分担，不同的组播地址可能会选择不同的RP。
```

默认情况下如果超过 150s 没有收到当前Active BSR的信息，则认为当前Active BSR故障，重新选举新的Active BSR。C-RP通过单播的方式将参选信息发送给Active BSR，BSR将会收集所有C-RP的参选信息，它不会做出RP选举，而是将所有C-RP的信息打包，并发送给所有的其它路由器所有的其它路由器将会自动来决定某一个组播组选择哪一个C-RP成为真正的RP。

## Day 41：IGMPV3&IGMP snooping

```
R1(config)#interface g0/0
R1(config-if)#ip igmp version 3//运行IGMPv3。使用组播组地址224.0.0.22Report:在IGMPv3当中,组播组成员发送加组消息时将会把Report消息发送到224.0.0.22组播组地址,其中包含了自己的加组以及特定源情况。IGMPv3中不再存在一个组播组中只能有一个设备回复Report消息的情况。不再有抑制一 如令IGMPv3中虽然组播组成员都在同一个组播组,但是可能需要不同组播源的数据主要两个模式:INCLUDE:主机在加入组播组时可以只接收特定组播源发送的组播数据流量EXCLUDE:主机在加入组播组时可以拒绝某一些组播源发送的组播组数据流量。
R1(config)#interface g0/0
R1(config-if)#ip igmp join-group 239.1.1.1 source 1.1.56.6//使得设备仅接收特定源发送的组播数据流量。SSM:特定源组播分发树模式,默认情况下路由器关闭该模式。也就是说路由器默认不支持特定源组播。
R3(config)#ip pim ssm default//需要在所有路由器上开启,针对于232.0.0.0/8开启特定源组播
R3(config)#access-list 1 permit 239.1.1.1
R3(config)#ip pim ssm range 1//针对于ac1匹配的组播组地址开启SSM特定源组播。
```

IGMPv3IGMPv1:Query:由最后一跳路由器发送,如果有多个最后一跳路由器则由PIM协议当中的DR路由器来选举作为查询者。

目标组播IP地址是:224.0.0.1(发给所有设备)Report:由终端设备发送,设备一旦加入到组播组或者收到Query消息(则会开启10s之内的随机倒计时,倒计时结束的路由器将会发送Report消息),目标的组播IP地址是:加入的组播组地址,例如:终端设备加入了239.1.1.1,则会向239.1.1.1发送Report消息。

没有离组消息,成员离组之后,需要Query路由器连续发送三次Query都收不到Report,才会认为组播组当中再无组成员,删除条目。

IGMPv2:Leave message:当组成员(最后一个回复Report消息的组成员)离组时,将会向最后一跳路由器发送离组消息目标组播IP地址:224.0.0.2Specific-Query:当最后一跳路由器收到了最后一个回复Report消息的终端设备发送的Leave message,将会向该组播组地址发送特定组查询消息,判断该组播组当中是否还有组成员目标组播IP地址是:对方离开的组播组地址。

IGMPv1&IGMPv2.成员收到Query需要回复Report消息时,一个主机的Report消息会抑制其它主机的Report(一个组播组当中只需要有一个组成员回复Report即可)IGMPv3:特定源!!!

CMP(Cisco私有):但是已被淘汰。

在交换机与路由器之间开启。

路由器收到了主机的Report消息会将主机的MAC地址以及主机所加入组播的MAC地址都通过CMP协议告知交换机。使得交换机知晓组播MAC地址中所加入的主机MAC地址是什么。

当交换机转发组播数据流量时可以查看到处于组播MAC地址中的对应主机MAC地址,将组播数据流量从对应端口转发。

缺点:交换机需要借助于最后一跳路由器来实现二层组播。

**IGMP Snooping:**

直接使得交换机能够识别到主机和路由器的IGMP协议消息。直接阅读主机的Report,Leave message,路由器的Query以及特定组查询。

```
Switch(config)#ip igmp snooping
```

口关联信息。

```
Switch#show ip igmp snooping querier
```

> 💡 针对于VLAN1启用IGMP

//查看IGMPSnooping组播组的表项以及端

//看看谁是cha'xun'zhe

## Day 42-43：IPv6的地址格式 · 地址空间划分 · IPv6单播地址范围 · EUI-64

共32个bits,分四组,每一组8个bits,表现为点分十进制。
2 32 2 32

  个IPv4地址 大约43亿个。

0.0.0.0 1.1.1.1

为了缓解IPv4地址紧缺使用NAT地址转换协议。

192.168.1.1:80

**缺点:**

头部比较复杂 部署起来复杂

重分布不便(一个节点只能够使用一个IPv4主地址)

广域网路由表太大(早期IPv4地址分配草率,IPv4分配地址不连续,不便于汇总)

**IPv6地址**

共128个bits,分8组,每一组16个bits,表现为十六进制数,用冒号隔开,冒号分十六进制数
2128 2 128

÷
2 32 2 96 2 128

 ÷2 
32 =2 96

**(倍)**

**43亿**

×
2 96

I

P

v

6

×2 

96

**=IPv6 地址空间**

0000000000000000000000000000000000000000000000000000000000000 000000000000000000000000000000000000000000000000000000000

0x0000:0000:0000:0000:0000:0000:0000:000

0xFFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF

**优点:**

**超大地址空间**

这一次认真地分配地址空间,可以很方便于汇总路由

**无状态自动化配置**

**更加简约的头部**

没有了广播,使用组播替代了广播的功能。

**扩展头部**

便于IPv4迁移到IPv6

**缺点:**

**书写不便**

2001:db8:4:14::1/64

路由器协议做出妥协。

**IPv6书写的格式要求:**

在IPv6地址当中连续的几组":0"可以被缩写为:: (一个IPv6地址当中只能够出现一次.)

2001:DB8:0000:0000:FFFF:0000:0000:000C

2001:DB8:0:0:FFFF:0:0:D0C

2001:DB8::FFFF:0:0:D0C

2001:DB8::FFFF:0:0:D0C

址

1 2 3 4 5 6

2001:DB8:0:0:FFFF:0:D0C

址

9

2001:DB8::FFFF:0:D0C

11

2001:DB8:0:0:0:FFFF:0:D0C

2001:DB8:0:0:0:FFFF:0:D0C

2001:DB8:0:0:0:FFFF:0:D0C

**//源地址**

**//简化**

//缩写,可以得知::省略了两组:0,可以还原出源地

//缩写,可以得知::省略了两组:0,可以还原出源地

//两组::,无法还原出唯一的源IPv6地址

//可以有三种情况

2001:db8:4:14::1 2001:1:100::1 6&2001:1:101::1

**特殊的IPv6地址**

:: 

= 0:0:0:0:0:0:0:0 类似于 ipv4的地址 0.0.0.0(未指定地址)书写默认路由::1 

= 0:0:0:0:0:0:0:1 类似于 ipv4的地址 127.0.0.1(本地回环地址)

**特殊写法：**

在URL中访问某一个IPv6主机的特殊端口时，IPv6地址需要用[ ]框起来例如：访问2001::1主机的TCP443端口需要写成：https://[2001::1]:443

IPv6地址的网络位主机位写法

192.168.1.1/24 192.168.1.1前24bits区分网络位，表明该地址属于192.168.1.0/24网段。主机位为1。

**IPv6地址**

≡

**≡ 前缀+接口标识组成**

前缀 

≡

**≡ 网络位**

**接口标识**

≡

**≡ 主机位**

2001:0:0:0:123:123:123:1/64

123:123:123:1

**IPv6的地址类型：**

单播：一对一发送消息

组播：一对多发送

任意播：一对最近。（多个设备公用同一个IPv6地址用户访问该目的IPv6地址时将会访问到距离自己最近的设备上。）

IPv6单播地址：（类似IPv4从1-223开头的地址）

目前已被分配的IPv6单播地址：2000::/3 001 + 124个0

可聚合的全球单播地址（公有IPv6地址）

2001::1/16 

⟶

⟶ 看到2001开头，就是公有的IPv6地址空间

2002::1/16 

⟶

⟶ 6to4tunnel的IPv6地址空间，用来将IPv4与IPv6兼容共同运行可以使用的方案。

本地链路地址（Link-Local）：仅在一条链路上有效

只要路由器的接口运行IPv6或者配置了一个IPv6的全球单播地址，那么路由器就会自动地通过接口的MAC地址自动运算计算出接口唯一的Link-Local地址。

FE80::/10 

⟶

⟶ 看到FE80开头，就是Link-local地址

书写静态路由、接口运行动态路由协议需要发送Hello包时、发送NS消息，RA消息，RA消息等都使用Link-local地址去发送。

**地址。）**

ULA(unique local address)地址：私有的IPv6地址（类似于10.0.0.0/8172.16.0.0/12192.168.0.0/16）

FC00::/7 

⟶

⟶ 看到FC开头或者FD开头的地址就是ULA地址。

**特殊的IPv6地址：**

IPv4的 0.0.0.0::1 IPv4的 127.0.0.1

**可以兼容IPv4的IPv6地址：**

：XXXX:XXXX/96 后面32个bits就是IPv4地址的32bits

例如：：192.168.1.1 

⟶

⟶ ：11000000010101000000000000000000000000000000000000000000000000000000000000000

：1111:XXXX:XXXX/96前面80位中64位固定位0，第65- 第80位固定为1111，最后的32个bits是IPv4地址。

```
R1(config-if)#ipv6 address ?
```

X:X:X:X:X:X/X<0-128> IPv6 prefix

```
R1#show ipv6 interface brief
```

址摘要情况。

```
R1#show ipv6 interface g0/0
```

息。

**Link-Local地址的计算方式：**

只要路由器的接口运行IPv6或者配置了一个IPv6的全球单播地址，那么路由器就会自动地通过接口的MAC地址自动运算计算出接口唯一的Link-local地址。

Link-Local 

= FE80::/10（前64bits固定为FE80） 

  EUI-64（特殊的IPv6地址格式64bits）

通过设备的MAC地址（48bits）扩充到64位数的IPv6地址格式

**确定设备的源MAC地址**

（例如：5000.0001.0000）

将源MAC地址拆开，分为前24个bits（6个十六进制数0UI）和后24bits（六个十六进制数EUI）

（例如：5000 00 / 01 0000）

在源MAC地址中间插入FFFE（4个十六进制数，16bits）

（例如：5000 00FFFE01 0000）

将插入了FFFE之后的地址第7个bits翻转，取反（0 

⇒

⇒ 1 1 

⇒

⇒ 0）

（例如：5000 00FFFE01 0000）

0101 00 0 0000 0000 

⇒

⇒ 0101 00 1 0 0000 0000 

⇒

⇒ 5200

MAC地址中第7位二进制数 0表示MAC地址全球有效 1表示MAC地址仅本地有效

EUI-64地址中第7位二进制数 0表示EUI-64地址本地有效 1表示EUI-64地址全球有效

**最终结果**

（例如：5200 00FFFE01 0000）

因此，源MAC地址为5000.0001.0000的接口最终自动运算产生的Link-Local地址

FE80::5200:00FF:FE01:0000

**替代ARP：**

不知道对方的MAC地址，只知道对方的IPv6地址，如果发送消息给对方（不能通过单播发送给对方请求对方的MAC地址）

使用组播的方式给对方发送请求消息，请求对方的MAC地址

对方加入的组播IPv6地址如何确定？

如何确定对方一定会加入该组播IPv6地址？

**IPv6的组播地址：**

看到FF开头的地址就是IPv6的组播地址

<table>组播地址作用FF02::1发给接口所在链路上的所有设备FF02::2发给接口所在链路上的所有路由器FF02::9发给接口所在链路上所有运行RIP的路由器FF02::A发给接口所在链路上所有运行EIGRP的路由器</table>

被请求节点组播组地址！！！被请求节点组播组地址！！！被请求节点组播组地址！！！被请求节点报组地址！！！被请求节点组播组地址！！！

设备只要有一个IPv6地址（不论是全球单播地址，还是UIA地址，还是Link-Local地址）就会自动加入到自己IPv6地址所对应的被请求节点组播组地址

**被请求节点组播组地址格式：**

FF02::1:FFXX:XXXX/104

通过IPv6地址计算对应被请求节点组播组地址的方式：

找到需要计算的IPv6地址

（例如：2001:123::1）

记下IPv6地址的最后6个十六进制数（24bits）

（例如：2001:0123:0000:0000:0000:0000:0000:0000:0000:00:0000:0000:0000:0000:0000:0000:0

将记下的6个十六进制数作为FF02::1:FFXX:XXXX/104的最后6个十六进制数

（例如：FF02::1:FF00:0001）

IPv6中主机发送组播数据包时，目的组播MAC地址的计算方式：

通过被请求节点组播组地址计算组播MAC地址的方式：

确定需要计算的被请求节点组播组地址

（例如：FF02::1:FF00:2）

记下被请求节点组播组地址的最后6个十六进制数（32bits）

（例如：FF02:0000:0000:0000:0000:0001:FF00:0002）

在组播MAC地址3333之后添加记下的8个十六进制数。

3333 FF00 0002

## Day 44：ICMPv6,NDP协议中NS,NA,RS,RA消息

使用ICMPv6当中NS以及NA消息替代了IPv4的ARP消息的作用。

Neighbor solicitation(NS消息)：邻居发现消息

替代了ARP Request

当主机需要请求目标IPv6地址的MAC地址时，将会封装NS消息数据包：

源IPv6地址是自己，目的IPv6地址是对方的被请求节点组播地址

源MAC地址是自己，目的MAC地址是对方被请求组播地址的组播MAC地址

NS消息头部当中将会包含自己的MAC地址以及自己需要请求MAC地址的目标IPv6地址。

Neighbor Advertisement(NA消息)：邻居发现消息

替代了ARP Reply

当主机收到了NS消息请求自己IPv6地址的MAC地址时：

源IPv6地址是自己被请求的IPv6地址，目的IPv6地址是发送方的IPv6地址

源MAC地址是自己，目的MAC地址是发送方的MAC地址

NA消息头部当中将会包含自己被请求的IPv6地址以及自己对应的MAC地址

邻居发现的作用：可以利用NS以及NA消息获取到双方的Link-Local地址。

```
R1#show ipv6 neighbors
```

> 💡 IPv6的邻居表（记录下IPv6地址以及对应MAC地址）

替代ARP的DAD(Duplicate Address Detection)重复地址检测

当主机配置上IPv6地址并即将使用之前将会发送NS消息进行重复地址检测：

源IPv6地址将会使用全为0的未指定地址为源（：），目的IPv6地址是自己即将使用的IPv6地址所对应的被请求节点组播组地址。

源MAC地址是自己，目的MAC地址是自己即将使用的IPv6地址所对应被请求节点组播组地址的MAC地址。

NS消息头部当中包含自己请求即将使用的目标IPv6地址以及自己的MAC地址。

当主机收到未指定地址发送给自己的NS请求（DAD检测消息）时，将会回复NA消息：

源IPv6地址是自己被请求的IPv6地址，目标IPv6地址将会是组播地址FF02：1（所有设备，因为发送方没有IPv6地址），因此告诉所有人地址自己

经使用。

源MAC地址是自己，目的MAC地址是FF02：1的MAC地址（3333：0080：0081）

NA消息头部当中包含自己的IPv6地址以及自己MAC地址（告诉本链路上的所有人该IPv6地址已经被自己这个MAC地址的设备使用了）

**无状态自动化配置**

Router Advertisement(RA消息)：路由器的前缀公告。

当路由器接口配置上了IPv6的全球单播地址，该路由器将会立刻开始向自己的端口对端周期性发送RA前缀公告消息，周期性地通告自己的IPv6地址前缀。

当主机收到了路由器通告的IPv6地址前缀，即可通过该地址前缀+自身MAC地址扩展的EUI-64地址格式自动产生一个IPv6的全球单播地址。

```
R1(config)#ipv6 unicast-routing //开启IPv6的单播路由功能，路由器才能够真正成为IPv6的路由器，支持转发IPv6的数据包。
```

源IPv6地址为路由器的Link-Local地址，目标IPv6地址是链路上所有设备都加入的（FF02：1）组播地址

源MAC地址是路由器自己的MAC地址，目的MAC地址是FF02：1对应的3333：0080：0081组播MAC地址。

RA消息当中包含了路由器接口的MAC地址，MTU，以及接口的IPv6地址前缀。（默认的周期时间为200s）

```
R1(config-if)#ipv6 nda interval 20
```

> 💡 修改前缀公告的周期时间

```
R3(config)#interface g0/0 
R3(config-if)#ipv6 address autoconfig
```

> 💡 启动无状态自动化配置。

Router solicitation(RS消息)

当主机或路由器支持无状态自动化配置产生IPv6地址时，将会发送RS请求消息希望路由器给自己下发前缀公告：

源IPv6地址是自己的Link-Local地址，目标IPv6地址是所有路由器所在的FF02：2组播地址

源MAC地址是自己，目的MAC地址是FF02：2对应的3333：0080：0082组播MAC地址

RS消息头部当中包含了自己的MAC地址。

只有/64掩码的IPv6全球单播地址或ULA地址前缀公告的前缀可以由主机或路由器无状态自动化配置产生IPv6地址。

首选生存时间(preferred lifetime)：默认7天，604800s，当通过前缀公告生成的IPv6地址首选生存时间0，则该IPv6地址不再能够主动的发送消息，但是仍然可以使用该IPv6地址，如果该地址被访问时可以做出回复。

可用生存时间(Valid Lifetime)：默认30天，2592000s，当通过前缀公告生成的IPv6地址可用生存时间0，则该IPv6地址将不再能够使用，设备将会把地址置为不可用状态，将该IPv6地址删除

路由器或主机每收到一次RA前缀公告消息，则首选生存时间和可用生存时间将会自动刷新。

1. R1(config-if)#ipv6 nd prefix 2001:123::/64 ? 2 <0-4294967295> Valid Lifetime (secs) //设置该前缀通告的可用生存时间 和首选生存时间 3 at Expire prefix at a specific time/date //设置该前缀的具体到期时间。 4 infinite Infinite Valid Lifetime //设置该前缀无限期 5 no-advertise Do not advertise prefix //不通告该前缀。 6 <cr>

Windows主机通过无状态自动化配置产生IPv6地址时会自动产生临时的IPv6地址和主要的IPv6地址，使用以下指令可以关闭临时的IPv6地址。（CMD中输入，需要管理员启动）

netsh interface ipv6 set privacy state=disabled

Windows主机生成EUI-64时为保证安全不会使用MAC地址生成EUI-64，而是使用私有协议产生IID（Interface Identifier），使用以下指令可以关闭CMD中输入，需要管理员启动）

Netsh interface ipv6 set global randomizeidentifiers=disabled

---

# 五、IPv6 路由与过渡技术

> IPv6 路由协议与 NAT64

## Day 45-48：IPv6 SLAAC网关冗余,IPv6路由,IPv6静态路由写法,EIGRP,OSPF,BGP

同一链路上有两个或多个路由器进行前缀公告，并且通告的是相同的地址前缀：例如：R1 & R2 都在通告 2001:123::/64的地址前缀。PC将会通过该地址前缀生成IPv6地址但是网关指向何处？设备将会选举第一个收到的前缀公告对应的设备作为自己的默认网关，下一跳指向对方的Link-Local

```
R1(config-if)#ipv6 nd router-preference ?
```

High High default router preference Low Low default router preference Medium Medium default router preference

设备会优先选择高优先级的路由器作为IPv6的默认网关路由器，下一跳指向对方的Link-Local地址

Life Time：生存时间，由路由器提供，在RA消息进行前缀公告时附带，告知通过自己的前缀生成IPv6地址的设备，超过多长时间收不到自己的RA前缀公告则认为自己出现故障，切换网关设备。（默认1800s）

```
R2(config)#interface g0/0
```

```
R2(config-if)#ipv6 nd ra lifetime 3
```

> 💡 接口中调整生存时间，生存实现需要大于通告时间。

**IPv6路由：**

**直连路由：**

只要路由器的接口UP，链路的协议UP，且路由器的端口上配置了IPv6地址及前缀，则将会产生接口对应网段的直连路由进入到路由表。

```
R1#show ipv6 interface brief
```

> 💡 查看IPv6的接口地址摘要情况。

```
R1#show ipv6 route
```

> 💡 查看IPv6路由表

**主机路由：**

只要路由器的端口up，链路的协议up，且路由器的端口配置上了IPv6地址及前缀，则将会产生接口ipv6地址对应/128位的主机路由进入到路由表。

**静态路由：**

**直接跟对方的下一跳IPv6地址：**

```
R1(config)#ipv6 unicast-routing //开启IPv6的路由功能。
```

```
R1(config)#ipv6 route 2001:23::/64 2001:12::2 //跟下一跳的IPv6地址写法
```

**跟下一跳的Link-Local地址：**

```
R1#show ipv6 neighbors
```

```
R1#show cdp neighbors detail
```

```
R1(config)#ipv6 route 2001:23::/64 g0/0 FE80::5200:FF:FE06:0 //跟对方的Link-Local地址。
```

Ip routing

//支持IPv4路由功能。

一旦被关闭，则路由器上所有的IPv4路由协议的配置全部会被铲掉，所以千万别乱删。

IPv6 RIP ===> RIPng

RIPng协议对应的组播地址是FF02::9（ipv4的224.0.0.9），一旦接口被激活运行RIPng，则开始周期性地（30s）向该组播地址发送RIPng更新消息并且端口自动加入到RIPng的组播组当中。

RIPng的通信消息由运行RIPng接口的Link-Local地址为源向FF02::9发送。

RIPng基于UDP传输协议521端口（IPv4的RIP基于UDP520端口）

**创建动态路由协议的进程**

```
R1(config)#ipv6 unicast-routing
```

```
R1(config)#ipv6 router rip A
```

> 💡 创建RIPNG的进程。

激活接口运行动态路由协议RIPng。

```
R1(config)#interface g0/0
```

```
R1(config-if)#ipv6 rip A enable
```

> 💡 激活端口运行RIP。

```
R1#show ipv6 rip database //查看RIPng的数据库
```

数据库条目进入数据库时默认的初始Metric 

1

=1 。通告出去时直接通告该数据库条目的Metric。

当其它路由器收到该数据库条目更新时，自动将Metric+1。

IPv6的RIP条目收敛时间与IPv4一致：

当超过188s收不到对方通告该数据库条目的更新，则将其对应的路由从路由表删除，认为其不可达。当超过248s收不到对方通告该数据库条目的更新，则将其从数据库当中彻底删除。

IPv6 EIGRP ===> EIGRP

IPv6的EIGRP基于组播地址FF02::A（ipv4的224.0.0.10）

一旦激活接口运行EIGRP，则接口会加入组播组FF02::A，并开始周期性（5s/15s）向该组播地址发送EIGRP的Hello

**创建进程**

```
R1(config)#ipv6 router eigrp 100
```

```
R1(config-rtr)#eigrp router-id 1.1.1.1
```

> 💡 需要配置EIGRP Router-ID（如果没有IPv4）

**激活接口运行EIGRP**

```
R1(config)#interface g0/0
```

```
R1(config-if)#ipv6 eigrp 100
```

> 💡 激活接口运行EIGRP

IPv6中动态路由协议依然需要Router-ID（虽然EIGRP中不是特别重要），格式与IPv4相同，点十分进制，32位。

Router-ID：路由器的标识。运行动态路由协议需要有Router-ID

没有Loopback接口选择最大的物理接口的IPv4地址作为Router-ID。

有Loopback接口选择最大的Loopback接口地址作为Router-ID。

可以手工指定，手工指定最优。

```
R1#show ipv6 eigrp topology
```

> 💡 查看IPv6的EIGRP数据库

以上第一种运行IPv6的EIGRP的方式。

多协议的EIGRP（可以同时支持IPv4和IPv6）

**创建进程**

```
R1(config)#router eigrp ccie
```

进入IPv6的EIGRP配置地址

```
R1(config-router)#address-family ipv6 autonomous-system 65001
```

```
R1(config-router-af)#eigrp router-id 1.1.1.1
```

激活接口运行EIGRP。

**//创建命名的EIGRP**

**//创建命名的EIGRP**

//进入IPv6地址族，配置IPv6的EIGRP

//指定IPv6 EIGRP的Router-ID

激活接口运行EIGRP。

af-interface default

指令。

no shutdown

**行ipv6 EIGRP**

no passive-interface

是被动端口。

```
R1(config-router-af)#af-interface default
```

```
R1(config-router-af-interface)#shutdown
```

```
R1(config-router-af-interface)#passive-interface
```

```
R1(config-router-af)#af-interface g0/0
```

界面，可以配置该端口

```
R1(config-router-af-interface)#no shutdown
```

```
R1(config-router-af-interface)#no passive-interface
```

```
R1#show ipv6 eigrp topology
```

```
R1(config-router-af)#topology base
```

> 💡 所有本路由器有IPv6地址的端口默认的

//所有本路由器上有IPv6地址的端口都运

//所有本路由器上有IPv6地址的端口都不

//所有本路由器上有IPv6地址的端口都不

text [[638, 624, 860, 635]]

//使得本路由器所有的IPv6接口不运行EIGRP

//使得本路由器所有的IPv6接口不建立EIGRP邻居

//进入Address-family ipv6 EIGRP端口的配置

//针对于该端口允许运行EIGRP

//该端口允许发送和接收EIGRP数据包可以建邻居。

//查看IPv6 EIGRP的数据库

//路由的高级操作被放到了Topology base配置界面下。

router eigrp ccie

address-family ipv4 unicast autonomous-system 65001

eigrp router-id 1.1.1.1

network 172.16.12.1 0.0.0.0

无需使用AF进行控制。

```
R1(config)#ipv6 router ospf 1 //创建OSPF进程。 2 Router-ID: 路由器的标识, 运行动态路由协议需要有Router-ID 3 没有loopback接口选择最大的物理接口的IPv4地址作为Router-ID。 4 有loopback接口选择最大的loopback接口地址作为Router-ID。 5 可以手工指定, 手工指定最优。 6
R1(config-rtr)#router-id 1.1.1.1 7 8
R1(config)#interface g0/0 9
R1(config-if)#ipv6 ospf 1 area 0 //直接指定Router-ID。 10
R1(config)#interface g0/0 11
R1(config-if)#ipv6 ospf 1 area 0 //激活端口运行OSPF。 12
R2(config)#router ospfv3 1 //创建进程 13
R2(config-router)#router-id 2.2.2.2 //设定OSPF Router-ID。 14
R2(config)#interface g0/0 15
R2(config-if)#ospfv3 1 ipv6 area 0 //运行IPv6的OSPF。 16
R1(config-if)#ospfv3 1 ipv4 area 0 //激活接口运行IPv4的OSPFv3。 17
R2(config-if)#ipv6 ospf 1 area 0 //与上方激活接口运行IPv6 OSPF方式一样 18 不要用ip ospf 1 area xx //使用的是OSPFv2版本的IPv4 ospf。 19
R3#show ipv6 ospf database //查看OSPFv3的IPv6数据库 20
R3#show ospfv3 database //同时查看OSPFv3的IPv4和IPv6的数据库 21 Type Command 22 Router 23 network 24 inter-area prefix 25 inter-area router 26 external 27 nssa-external 28 link 29 prefix 30 1类R2和2类LSA相较于IPv4的变化并不是很大,但是缺少了路由器链路上的接口地址以及链路的掩码。使用了接口的编号来替代了原先地址的表示方式。 31 OSPFv3当中通过1类,2类,8类,9类LSA计算得出本区域内部的路由条目。 32 OSPFv3当中3类LSA计算得出区域之间的路由 33 OSPFv3当中4类5类LSA计算得出外部路由 34 OSPFv3当中7类LSA计算得出NSSA特殊区域当中的外部路由 285 1.
```

1 

1 LS age: 1045 2 Options: (V6- Bit, E-Bit, R-Bit, DC-Bit)

3 LS Type: Network Links

4 Link State ID: 2 (Interface ID of Designated Router)

5 Advertising Router: 1.1.1.1 6 LS Seq Number: 80000001 7 Checksum: 0x45B1 8 Length: 32 9 Attached Router: 1.1.1.1 10 Attached Router: 2.2.2.2 11 少了掩码。 12 //告知链路上哪些设备接在同一个链路，分别是 13 //查看8类LSA。 14 //由链路上的路由器自己通告，通告自己连接在一条链路上的接口ID以及Link-Local地址和接口前缀。 15 只通告到本链路上，不会通告到本区域的其它链

16 LS age: 1469 17 Options: (V6- Bit, E-Bit, R-Bit, DC-Bit)

18 LS Type: Link-LSA (Interface: GigabitEthernet0/0)

19 Link State ID: 2 (Interface ID)

20 Advertising Router: 1.1.1.1 21 LS Seq Number: 80000001 22 Checksum: 0xEBCD

23 Length: 56 24 Router Priority: 1 25 Link Local Address: FE80::5200:FF:FE05:0 26 Number of Prefixes: 1 27 Prefix Address: 2001:12::

28 Prefix Length: 64, Options: None 29 //9类LSA，通告了本区域路由器自己的前缀有 30 有本区域的路由器自己通告，告知区域当中的设备自身有哪些前缀地址的路由可以计算，该LSA将会通告本区域内部，不会通告到其它区域。

31 LS age: 1336 32 LS Type: Intra-Area-Prefix-LSA

33 Link State ID: 0 34 Advertising Router: 1.1.1.1 35 LS Seq Number: 80000001 36 Checksum: 0x60CF

37 Length: 52 38 Referenced LSA Type: 2001 39 Referenced Link State ID: 0 40 Referenced Advertising Router: 1.1.1.1 41 Number of Prefixes: 1 42 Prefix Address: 2001:1111::1 43 Prefix Length: 128, Options: LA, Metric: 0 44 //有个地址2001:1111::1 45 //掩码为128。

 46 //告知链路上哪些设备接在同一个链路，分别是 47 //查看8类LSA。 48 //由链路上的路由器自己通告，通告自己连接在一条链路上的接口ID以及Link-Local地址和接口前缀。

 49 有本区域的路由器自己通告，告知区域当中的设备自身有哪些前缀地址的路由可以计算，该LSA将会通告本区域内部，不会通告到其它区域。

50 LS age: 1336 51 LS Type: Intra-Area-Prefix-LSA

52 Link State ID: 0 53 Advertising Router: 1.1.1.1 54 Prefix Address: 2001:1111::1 55 Prefix Length: 128, Options: LA, Metric: 0 56 //9类LSA，通告了本区域路由器自己的前缀有 57 有本区域的路由器自己通告，告知区域当中的设备自身有哪些前缀地址的路由可以计算，该LSA将会通告本区域内部，不会通告到其它区域。

58 LS age: 1336 59 LS Type: Intra-Area-Prefix-LSA

60 Link State ID: 0 61 Advertising Router: 1.1.1.1 62 Prefix Address: 2001:1111::1 63 Prefix Length: 128, Options: LA, Metric: 0 64 //有个地址2001:1111::1 65 //掩码为128。 66 //告知链路上哪些设备接在同一个链路，分别是 67 //查看8类LSA。 68 //由链路上的路由器自己通告，通告自己连接在一条链路上的接口ID以及Link-Local地址和接口前缀。 69 有本区域的路由器自己通告，告知区域当中的设备自身有哪些前缀地址的路由可以计算，该LSA将会通告本区域内部，不会通告到其它区域。

70 LS age: 1336 71 LS Type: Intra-Area-Prefix-LSA

72 Link State ID: 0 73 Advertising Router: 1.1.1.1 74 Prefix Address: 2001:1111::1 75 Prefix Length: 128, Options: LA, Metric: 0 76 //9类LSA，通告了本区域路由器自己的前缀有 77 有本区域的路由器自己通告，告知区域当中的设备自身有哪些前缀地址的路由可以计算，该LSA将会通告本区域内部，不会通告到其它区域。

78 LS age: 1336 79 LS Type: Intra-Area-Prefix-LSA

80 Link State ID: 0 81 Advertising Router: 1.1.1.1 82 Prefix Address: 2001:1111::1 83 Prefix Length: 128, Options: LA, Metric: 0 84 //有个地址2001:1111::1 85 //掩码为128。 86 //告知链路上哪些设备接在同一个链路，分别是 87 //查看8类LSA。 88 //由链路上的路由器自己通告，通告自己连接在一条链路上的接口ID以及Link-Local地址和接口前缀。 89 有本区域的路由器自己通告，告知区域当中的设备自身有哪些前缀地址的路由可以计算，该LSA将会通告本区域内部，不会通告到其它区域。

90 LS age: 1336 91 LS Type: Intra-Area-Prefix-LSA

92 Link State ID: 0 93 Advertising Router: 1.1.1.1 94 Prefix Address: 2001:1111::1 95 Prefix Length: 128, Options: LA, Metric: 0 96 //9类LSA，通告了本区域路由器自己的前缀有 97 有本区域的路由器自己通告，告知区域当中的设备自身有哪些前缀地址的路由可以计算，该LSA将会通告本区域内部，不会通告到其它区域。

98 LS age: 1336 99 LS Type: Intra-Area-Prefix-LSA

100 Link State ID: 0 101 Advertising Router: 1.1.1.1 102 Prefix Address: 2001:1111::1 103 Prefix Length: 128, Options: LA, Metric: 0 104 //有个地址2001:1111::1 105 //掩码为128。 106 //告知链路上哪些设备接在同一个链路，分别是 107 //查看8类LSA。 108 //由链路上的路由器自己通告，通告自己连接在一条链路上的接口ID以及Link-Local地址和接口前缀。 109 有本区域的路由器自己通告，告知区域当中的设备自身有哪些前缀地址的路由可以计算，该LSA将会通告本区域内部，不会通告到其它区域。

110 LS age: 1336 111 LS Type: Intra-Area-Prefix-LSA

112 Link State ID: 0 113 Advertising Router: 1.1.1.1 114 Prefix Address: 2001:1111::1 115 Prefix Length: 128, Options: LA, Metric: 0 116 //9类LSA，通告了本区域路由器自己的前缀有 117 有本区域的路由器自己通告，告知区域当中的设备自身有哪些前缀地址的路由可以计算，该LSA将会通告本区域内部，不会通告到其它区域。

118 LS age: 1336 119 LS Type: Intra-Area-Prefix-LSA

120 Link State ID: 0 121 Advertising Router: 1.1.1.1 122 Prefix Address: 2001:1111::1 123 Prefix Length: 128, Options: LA, Metric: 0 124 //有个地址2001:1111::1 125 //掩码为128。 126 //告知链路上哪些设备接在同一个链路，分别是 127 //查看8类LSA。 128 //由链路上的路由器自己通告，通告自己连接在一条链路上的接口ID以及Link-Local地址和接口前缀。 129 有本区域的路由器自己通告，告知区域当中的设备自身有哪些前缀地址的路由可以计算，该LSA将会通告本区域内部，不会通告到其它区域。

130 LS age: 1336 131 LS Type: Intra-Area-Prefix-LSA

132 Link State ID: 0 133 Advertising Router: 1.1.1.1 134 Prefix Address: 2001:1111::1 135 Prefix Length: 128, Options: LA, Metric: 0 136 //9类LSA，通告了本区域路由器自己的前缀有 137 有本区域的路由器自己通告，告知区域当中的设备自身有哪些前缀地址的路由可以计算，该LSA将会通告本区域内部，不会通告到其它区域。

138 LS age: 1336 139 LS Type: Intra-Area-Prefix-LSA

140 Link State ID: 0 141 Advertising Router: 1.1.1.1 142 Prefix Address: 2001:1111::1 143 Prefix Length: 128, Options: LA, Metric: 0 144 //有个地址2001:1111::1 145 //掩码为128。 146 //告知链路上哪些设备接在同一个链路，分别是 147 //查看8类LSA。 148 //由链路上的路由器自己通告，通告自己连接在一条链路上的接口ID以及Link-Local地址和接口前缀。 149 有本区域的路由器自己通告，告知区域当中的设备自身有哪些前缀地址的路由可以计算，该LSA将会通告本区域内部，不会通告到其它区域。

150 LS age: 1336 151 LS Type: Intra-Area-Prefix-LSA

152 Link State ID: 0 153 Advertising Router: 1.1.1.1 154 Prefix Address: 2001:1111::1 155 Prefix Length: 128, Options: LA, Metric: 0 156 //9类LSA，通告了本区域路由器自己的前缀有 157 有本区域的路由器自己通告，告知区域当中的设备自身有哪些前缀地址的路由可以计算，该LSA将会通告本区域内部，不会通告到其它区域。

158 LS age: 1336 159 LS Type: Intra-Area-Prefix-LSA

160 Link State ID: 0 161 Advertising Router: 1.1.1.1 162 Prefix Address: 2001:1111::1 163 Prefix Length: 128, Options: LA, Metric: 0 164 //有个地址2001:1111::1 165 //掩码为128。 166 //告知链路上哪些设备接在同一个链路，分别是 167 //查看8类LSA。 168 //由链路上的路由器自己通告，通告自己连接在一条链路上的接口ID以及Link-Local地址和接口前缀。 169 有本区域的路由器自己通告，告知区域当中的设备自身有哪些前缀地址的路由可以计算，该LSA将会通告本区域内部，不会通告到其它区域。

170 LS age: 1336 171 LS Type: Intra-Area-Prefix-LSA

172 Link State ID: 0 173 Advertising Router: 1.1.1.1 174 Prefix Address: 2001:1111::1 175 Prefix Length: 128, Options: LA, Metric: 0 176 //9类LSA，通告了本区域路由器自己的前缀有 177 有本区域的路由器自己通告，告知区域当中的设备自身有哪些前缀地址的路由可以计算，该LSA将会通告本区域内部，不会通告到其它区域。

178 LS age: 1336 179 LS Type: Intra-Area-Prefix-LSA

180 Link State ID: 0 181 Advertising Router: 1.1.1.1 182 Prefix Address: 2001:1111::1 183 Prefix Length: 128, Options: LA, Metric: 0 184 //有个地址2001:1111::1 185 //掩码为128。 186 //告知链路上哪些设备接在同一个链路，分别是 187 //查看8类LSA。 188 //由链路上的路由器自己通告，通告自己连接在一条链路上的接口ID以及Link-Local地址和接口前缀。 189 有本区域的路由器自己通告，告知区域当中的设备自身有哪些前缀地址的路由可以计算，该LSA将会通告本区域内部，不会通告到其它区域。

190 LS age: 1336 191 LS Type: Intra-Area-Prefix-LSA

192 Link State ID: 0 193 Advertising Router: 1.1.1.1 194 Prefix Address: 2001:1111::1 195 Prefix Length: 128, Options: LA, Metric: 0 196 //9类LSA，通告了本区域路由器自己的前缀有 197 有本区域的路由器自己通告，告知区域当中的设备自身有哪些前缀地址的路由可以计算，该LSA将会通告本区域内部，不会通告到其它区域。

198 LS age: 1336 199 LS Type: Intra-Area-Prefix-LSA

200 Link State ID: 0 201 Advertising Router: 1.1.1.1 202 Prefix Address: 2001:1111::1 203 Prefix Length: 128, Options: LA, Metric: 0 204 //有个地址2001:1111::1 205 //掩码为128。 206 //告知链路上哪些设备接在同一个链路，分别是 207 //查看8类LSA。 208 //由链路上的

**宣告路由**

```
R1(config-router-af)# network 2001:1111::/64
```

> 💡 宣告路由表当中的路由条目进入BGP的数据库

```
R1#show ip bgp ipv6 unicast summary
```

```
R1#show bgp ipv6 unicast summary
```

```
R1#show bgp ipv6 unicast
```

> 💡 建议下面这个.

//查看BGP的IPv6数据库.（建议用这个）

1 router bgp 1

2 bgp router-id 1.1.1.1

3 bgp log-neighbor-changes

4 neighbor 100.3.11.2 remote-as 2

!

address-family ipv6

neighbor 100.3.11.2 activate

由.

如果通过IPv4的BGP邻居学习到了IPv6的路由条目，则路由条目的下一跳自动更改为可靠IPv4的IPv6地址

**例如：**

从100.3.11.1邻居学到的IPv6路由，则下一跳为

::FFFF:100.3.11.1

必须要手工更改为可以访问的下一跳IPv6地址才能够将数据信息条目提交到路由表.

1 route-map R1- R2 permit 10

2 set ipv6 next-hop 2001:2710:311::1

3 router bgp 2

4 bgp router-id 2.2.2.2

5 neighbor 100.3.11.1 remote-as 1

6 address-family ipv6

7 neighbor 100.3.11.1 activate

8 neighbor 100.3.11.1 route-map R1- R2 in

**一跳做出修改**

//通过IPv4建立IPv6的BGP邻居并传递IPv6路

//所有路由允许通过并且设置下一跳.

//针对于对方给自己的所有IPv6路由下

//针对于对方给自己的所有IPv6路由下

利用6to4Tunnel解决IPv6站点跨越IPv4网络实现互相通讯的问题.

各个IPv6站点必须使用6to4tunnel地址范围进行部署.

站点内部的IPv6地址网段必须通过6to4地址网段2002::/16进行部署

具体网段的分配按照设备所具备的公有IPv4地址进行计算.

将公有IPv4地址的32个bits插入到6to4tunnel地址网段2002::之后的第17位至48位.

例如：设备的公有地址为172.16.12.1. 10101108.00010000.00001100.00000001 

⇒

⇒ AC10 0C01

则站点需要使用的地址范围是：2002：172.16.12.1： 

≡

≡

≡

≡≡≡ 2002:AC10:0C01::

**1 R1:**

2 interface Loopback0 3 ipv6 address 2002:AC10:C01::1/64 4 interface Tunnel0 5 no ip address

6 no ip redirects

7 ipv6 enable

8 tunnel source GigabitEthernet0/0 9 tunnel mode ipv6ip 6to4 10 ipv6 route 2002::/16 Tunnel0 静态路由

**1 R3:**

2 interface Loopback0 3 ipv6 address 2002:C0A8:1703::3/64 4 interface Tunnel0 5 no ip address

6 no ip redirects

7 ipv6 enable

8 tunnel source GigabitEthernet0/1 9 tunnel mode ipv6ip 6to4 10 ipv6 route 2002::/16 Tunnel0 静态路由

//Loopback6配置测试地址.

//模式更改为6to4 tunnel. //书写去往6to4 tunnel目标地址网段

//Loopback6配置测试地址.

//模式更改为6to4 tunnel.

//书写去往6to4 tunnel目标地址网段

**网络技术实验室**

## Day 49：NAT64(network address translation)

在IPv4和IPv6网络的接口上运行NAT64。
R2(config)#interface range g0/0,g0/1
R2(config-if-range)#nat64 enable2. 将IPv6地址映射到公网当中的IPv4地址。
R2(config)#nat64 v6v4 static 2001:23::3 172.16.12.3
R2#show nat64 translations
R2#show nat64 prefix stateful global IPv6地址前缀默认的NAT64 Prefix是：64:FF9B::/96例如：IPv4地址172.16.12.1经过NAT64映射之后的IPv6地址为64:FF9B::172.16.12.1 

⇒

⇒ 64:FF9B::10101100.00010000.00001100.00000001 

⇒

```
R2(config)#nat64 prefix stateful 2001:23::/96 //通过该命令可以调整IPv4地址进入IPv6之后的地址前缀。只能够一对一转换。
R2(config)#nat64 v6v4 static tcp 2001:23::3 23 172.16.12.3 12345 //进行IPv4与IPv6地址的端口映射。
R2(config)#nat64 v6v4 static 172.16.12.1 2001:123::1 //配置IPv4地址进入IPv6地址空间时的映射IPv6地址。IPv4- Embedded IPv6 Address FormatPL 0 - 31 32- 39 40- 47 48- 55 56- 63 64- 71 72- 79 80- 87 88- 95 96- 103 104- 12732 prefix v4(32) u suffix40 prefix v4(24) u v4(8) suffix48 prefix v4(16) u v4(16) suffix56 prefix v4(8) u v4(24) suffix64 prefix u v4(32) suffix96 prefix (tipo:64:ff9b:/96) v4(32)
```

⇒ 64:FF9B::AC10:8C01

Examples of algorithmic mapping

<table>IPv6 PrefixIPv4IPv4- Embedded IPv6 Address2001:db8::/32192.168.2.332001:db8:000:221::2001:db8:100::/40192.168.2.332001:db8:1c0:2:21::2001:db8:122::/48192.168.2.332001:db8:122:c000:2:2100::2001:db8:122:300::/56192.168.2.332001:db8:122:3c0:0:221::2001:db8:122:344::/64192.168.2.332001:db8:122:344:c0:2:2100::2001:db8:db8:122:344::/96192.168.2.332001:db8:122:344::192.0.2.33</table>

动态的多对一转换

在IPv4和IPv6网络的接口上运行NAT64。

```
R2(config)#interface range g0/0,g0/1
```

```
R2(config-if-range)#nat64 enable
```

使用IPv6的ACL匹配上感兴趣流（哪些数据流量需要经过NAT转换。）

```
R2(config)#ipv6 access-list Network:23
```

```
R2(config-ipv6- acl)#permit ipv6 2001:23::/64 any
```

> 💡 创建IPv6的ACL匹配所有2001:23::/64访问

将感兴趣流与公网地址池做管理+overload. R2(config)#nat64 v6v4 list Network:23 pool A overload

动态多对少转换

在IPv4和IPv6网络的接口上运行NAT64.

```
R2(config)#interface range g0/0,g0/1 
R2(config-if-range)#nat64 enable
```

使用IPv6的ACL匹配上感兴趣流（哪些数据流量需要经过NAT转换.）

```
R2(config)#ipv6 access-list Network:23
```

```
R2(config-ipv6- acl)#permit ipv6 2001:23::/64 any
```

**任何目的地址的数据流量**

使用NAT64的地址池匹配上可以转换的IPv4地址范围

```
R2(config)#nat64 v4 pool A 172.16.12.3 172.16.12.5
```

将感兴趣流与公网地址池做管理+overload.

```
R2(config)#nat64 v6v4 list Network:23 pool A overload
```

> 💡 该地址池当中仅有一个公有IPv4地址可以使用.

//创建IPv6的ACL匹配所有2801:23::/64访问

WOLF-LAB

**网络技术实验室**

帮我识别每个PDF中的文字。所有文字都要识别输出，不要省略。不要总结。按照day日期大小进行排序

好的，根据您的要求，我识别了所有PDF文件中的文字，并按照Day日期从小到大进行了排序，未做任何省略和总结。

---

# 六、园区网与交换机专题

> STP/VLAN/安全/DAI/EtherChannel

## Day 50：交换机知识复习,PVST,PVST+

```
SW1#show mac address-table //查看交换机的MAC地址表。一、学习MAC地址，形成MAC地址表项。
SW1#show vlan brief //查看交换机的VLAN情况可以在交换机当中创建和划分出其它VLAN，将交换机的端口划分进入其它的VLAN。不同VLAN的交换机端口在数据链路层上不能够互相访问。VLAN标签协议：IEEE 802.1Q协议：（IEEE：国际的电子电器工程师协会）（802委员会：专门颁布网络当中的协议标准）802.1Q VLAN标签协议：可以在数据链路层的头部当中插入4个bytes的VLAN标签头部，表示数据流量属于哪一个VLAN。可以利用VLAN标签进行数据流量所属VLAN的识别功能。
SW1(config)#vlan 10 //创建VLAN10，直接使用VLAN+ VLANID
SW1(config)#vlan 20,30,40 //可以同时创建VLAN20,30,40三个VLAN，用‘，隔开
SW1(config)#vlan 50-60 //创建VLAN50,51...60连续的11个VLAN需要交换机的端口工作在特定的模式下，来针对子VLAN标签进行插入，识别，剥离。
SW1(config)#interface g1/1
SW1(config-if)#switchport mode access
SW1(config-if)#switchport access vlan 10VLAN//将交换机接口设置为Access模式并且划分进入Trunk接口模式：交换机之间会使用到的接口模式，Trunk模式。Trunk接口可以允许多个VLAN的数据流量通过。一、识别标签当交换机从Trunk接口收到带有VLAN标签的数据帧时，检查其VLAN标签的VLANID是否在本Trunk接口允许通过的VLAN列表当中，允许，则接收，不允许，则丢弃。二、保留标签当交换机从Trunk接口发送出去带有VLAN标签的数据帧时，其可以保留其VLAN标签转发（不是Native VLAN。）三、打上剥离标签
```

**交换机的基本工作原理：**

只要交换机从端口收到了数据流量，将会立刻查看其源MAC地址：如果交换机的MAC地址表中没有该MAC地址的关联表项，交换机将会把该MAC地址关联到端口上形成MAC地址表项。

如果交换机的MAC地址表中已经学习过该MAC地址：如果该MAC地址所关联的端口就是此次收到数据流量的端口，则直接转发数据。

如果该MAC地址所关联的端口不是此次收到数据流量的端口，重新反旧，老化掉旧的MAC地址关联表项，并将其关联到最新的端口二、根据目的MAC地址转发。（按照MAC地址表转发。

）当目的MAC地址在MAC地址表中没有对应的关联端口表项，交换机将会把该消息从所有的其它端口转发出去（泛洪）泛洪广播，组播，未知单播。当目的MAC地址在MAC地址表中有的对应的关联表项，则交换机直接将消息从关联的接口转发出去。

交换机的VLAN技术主要用于隔离广播。默认情况下交换机的所有端口都属于同一个VLAN：VLAN1

Access接口模式：一、打标签当交换机从Access接口收到没有标签的数据帧时，直接打上接口的VLANID作为VLAN标签插入到数据帧当中。

**二、识别标签当交换机从Access接口收到打上标签的数据帧时，查看其VLAN标签的VLANID是否与本接口的VLANID相同，相同则接收，不同则丢弃。三、剥离标签当交换机从Access接口发送出去数据帧时，将会剥离掉VLAN标签转发出去。**

Access接口一个端口只能够属于一个VLANAccess接口常用来对接终端设备（PC，路由器）VLAN标签，是交换机内部实现VLAN之间隔离，识别VLAN的方式，它不会影响到终端设备的使用。

当数据帧进入交换机的Access接口之前长什么样，离开交换机的Access接口之后还是什么样。

每一个Trunk接口都会有一个Native VLAN默认 

= VLAN1，Trunk接口针对于native VLAN采用Access接口的工作方式。交换机从Trunk接口收到没有VLAN标签的数据帧时可以打上Trunk接口native VLAN的ID作为VLAN标签插入到数据帧交换机从Trunk接口发送出去带有native VLAN的VLAN标签数据帧时，可以剥离掉其VLAN标签转发。

STP生成树协议（协议的工作方式和选路方式）

保证网络冗余性的前提条件下，确保没有环路问题。

**一、在一个网络当中选举根桥交换机**

拥有最小的bridge-ID的交换机就是根桥交换机

比较交换机的优先级，最小的成为根桥交换机；如果交换机的优先级相同，则MAC地址最小的交换机成为根桥交换机。

Bridge-ID 

**= 交换机的优先级**

**交换机的MAC地址组成**

**交换机的优先级默认**

32768

=32768

```
SW1(config)#spanning-tree vlan 1 priority ? <8-61440> bridge priority in increments of 4096 级，且必须为4096的倍数。
```

**二、在每一个非根桥交换机上选举一个根端口RP**

**三、在每一个链路上选举一个指定端口DP**

**四、非根端口，非指定端口被置为阻塞端口。**

BPDU消息：全名叫做（bridge protocol data unit）桥协议数据单元，主要用于STP生成树协议当中的选路。

Root-ID：当前交换机所认为的根桥的优先级 

**根桥的MAC地址**

RPC（Root Path Cost）简称COST值：交换机从根端口去往根桥的开销值。

COST 

= 交换机从根端口去往根桥出方向接口的开销值之和。

Bridge-ID：交换机的优先级 

  交换机的MAC地址组成（准发送的BPDU消息，Bridge-ID就是准。）

Port-ID：交换机接口的优先级 

  接口的标识（接口是交换机上的第几个口，标识就是多少）

**接口的优先级默认**

128 =128

```
SW2(config)#interface g0/1 
SW2(config-if)#spanning-tree port-priority ? <8-240> port-priority in increments of 16 调整则必须设定为16的倍数。
```

```
SW1#show spanning-tree
```

> 💡 可用于查看生成树。

**收敛速度：**

38 s

**38s 一**

>
58 s

>58s

**PVST的端口角色：**

<table>role功能是否转发数据流量根端口负责接收来自根桥的BPDU消息，以及拓扑发生变化时告知根桥。能够指定端口负责向链路对端发送BPDU消息能够</table>

**PVST的端口状态：**

```
SW1#debug spanning-tree events
```

状态 作用 disabled 端口被关闭，不能够发送和接收BPDU消息，不能够发送和接收数据流量，不能够学习MAC地址形成MAC地址表项 block 不能够发送BPDU消息，可以接收BPDU消息，不能够发送和接收数据流量，不能够学习MAC地址形成MAC地址表项 listening 端口可以发送和接收BPDU消息，确定端口的角色，不能够发送和接收数据流量，不能够学习MAC地址形成MAC地址表项 15s learning 端口可以发送和接收BPDU消息，可以接收数据流量，可以学习MAC地址形成MAC地址表项 15s forwarding 端口可以发送和接收BPDU消息，可以发送和接收数据流量。

Forward Delay: 转发延时，默认15s，意味着在Listening和Learning状态下持续的时间。

PVST+

down ---> Designed port ---> 30s ---> Portfast ---> 0s Block ---> Root Port ---> 30s ---> uplinkfast ---> 0s Block ---> Designed Port ---> 50s ---> backbonefast ---> 30s

收敛速度：0s ---> 30s

**Portfast:**

交换机端口一旦设定了Portfast特定，则端口up时，将会跳过listening，跳过learning，直接进入到Forwarding状态（DP指定端口）

```
SW1(config)#interface g1/1
```

```
SW1(config-if)#spanning-tree portfast
```

> 💡 配置单一端口开启Portfast特定

```
SW1(config)#spanning-tree portfast edge default
```

**Portfast特性**

注意：当开启了Portfast特定的端口一旦收到了BPDU消息（对面有交换机），则会立刻自动删除自身的Portfast特性，变成普通的交换机端口。

**uplinkfast:**

根据口的快速切换。

**Forwarding状态**

```
SW1(config)#spanning-tree uplinkfast
```

```
SW1#show spanning-tree uplinkfast
```

**backbonefast:**

```
SW3(config)#spanning-tree backbonefast
```

```
SW3(config)#spanning-tree backbonefast
```

使得交换机在收到了非根桥发送的次级BPDU消息时，立刻向根桥发送根桥链路检测消息，确定根桥是否存活，一旦收到了根桥的ACK回复，则直接响应非根桥的次级BPDU消息而不再等待其老化，加快收敛速度。

## Day 51：RSTP(Rapid-PVST)

1.1.1.1.1.1.1.1.1.1.1

**PVST的端口角色：**

<table>role功能是否转发数据流量根端口负责接收来自根桥的BPDU消息，以及拓扑发生变化时告知根桥。能够指定端口负责向链路对端发送BPDU消息能够</table>

**PVST的端口状态：**

```
SW1#debug spanning-tree events //检测生成树端口状态变化的情况。
```

<table>states作用disabled端口被关闭，不能够发送和接收BPDU消息，不能够发送和接收数据流量，不能够学习MAC地址形成MAC地址表项block不能够发送BPDU消息，可以接收BPDU消息，不能够发送和接收数据流量，不能够学习MAC地址形成MAC地址表项listening端口可以发送和接收BPDU消息，确定端口的角色，不能够发送和接收数据流量，不能够学习MAC地址形成MAC地址表项learning端口可以发送和接收BPDU消息，可以接收数据流量，可以学习MAC地址形成MAC地址表项forwarding端口可以发送和接收BPDU消息，可以发送和接收数据流量。</table>

Forward Delay：转发延时，默认15s，意味着在Listening和Learning状态下持续的时间。

**RSTP的端口状态：**

<table>States作用Discarding(丢弃)端口可以发送和接收BPDU消息，确定端口的角色，不能够发送和接收数据流量，不能够学习MAC地址形成MAC地址表项Learning端口可以发送和接收BPDU消息，可以接收数据流量，可以学习MAC地址形成MAC地址表项Forwarding端口可以发送和接收BPDU消息，可以发送和接收数据流量。</table>

**RSTP的端口角色**

<table>role功能是否转发数据流量根端口(root Port)负责接收来自根桥的BPDU消息，以及拓扑发生变化时告知根桥。能够指定端口(Designated Port)负责向链路对端发送BPDU消息能够Alternate(替代端口)收到第二优异BPDU消息的阻塞端口，作为根端口的备份端口，只要根端口故障，则直接成为新的根端口并立刻 Forwarding。不能够Backup(备份端口)链路上发送第二优异BPDU消息的阻塞端口，作为指定端口的备份端口，如果指定端口故障，则可以立刻成为新的DP并进入Forwarding不能够</table>

**PVST的收敛方式：**

A topology change is generated on point T. 1st step: A TCN is going up to the root.

2nd step: the root advertises the TC for max-age+ forward delay.

当交换机检测到本交换机的拓扑发生了变化（端口进入forwarding或端口进入disabled），则会立刻从交换机的根端口向根桥方向发送一个TCN(topology change notification)消息

当上游交换机收到了TCN消息时，将会立刻从收到TCN消息的端口发送一个BPDU消息并将TCA(topology change acknowledgment)字段置为1表示针对于该TCN消息的回复。

该交换机将会继续将TCN消息从根端口向根桥方向发送，直到该TCN抵达根桥。

根桥收到了TCN消息之后同样需要回复TCA消息，只不过，根桥在回复TCA的同时根桥交换机将会把BPDU消息中的TC（topology change）字段置为1从自己的所有指定端口向外发送。

所有收到TC-1的交换机将会知道网络拓扑发生了变化并开始重新确定端口的角色和状态。

根桥是标准生成树的绝对权力核心，由它来负责管理，维护以及生成树的收敛。

**RSTP的收敛方式：**

The originator of the TC directly floods this information through the network

RSTP当中交换机发现拓扑发生了变化，将会从自己的所有非阻塞端口向外发送TC-1的BPDU消息

其它交换机收到了TC-1的BPDU消息过后，将会立刻回复TCA-1的BPDU消息。回复TCA之后将会继续向其它的非阻塞端口发送TC-1的BPDU消息

**TC While计时器**

交换机发送了TC-1的BPDU消息之后将会立刻开启TCWhile计时器，需要在E2次BPDU和HeLLo时间（4s）以内收到TCA的回复消息，如果两次都未收到TCA的回复则认为交换机之间的链路出现故障。（边缘端口不会开启TCWhile计时器）

**老化MAC地址**

交换机如果从端口收到了TC-1的拓扑发生变化的消息，则会老化掉本接口上关联的MAC地址表项。

RSTP发送TC-1的拓扑发生变化BPDU的条件

RSTP中只有非边缘端口进入到Forwarding状态，才会发送TC-1的BPDU消息。

0 1 2 3 4 5 6 7

第1和第6位表示proposal和agreement，是RSTP中的P/A机制，实现RSTP的快速协商收敛。

第2和第3位表示交换机端口自己的角色

第4和第5位表示端口的状态。

**新的BPDU消息交换的方式：**

**PVST:**

只有根桥会主动地从指定端口向外发送BPDU消息，其它非根桥交换机在从根端口收到根桥的BPDU消息之后从自己的指定端口中继转发BPDU消息出去。RSTP:

哪怕不是根桥交换机也会主动从指定端口每隔2s（默认）向外发送BPDU消息。超过三次端口未正常收到对方的BPDU消息，则认为链路损坏。

**继承了PVST+中的特性：**

继承了uplinkfast，可实现根端口的快速切换

继承了backbonefast，加快了骨干链路损坏出现次级BPDU消息的响应与收敛速度。

**引入了边缘端口（edge port）：**

PVST+当中的portfast特性。

针对于开启了portfast特性的，可以跳过forwarding time，直接进入forwarding状态的端口称之为边缘端口。

RSTP的Link-type

P2P(point-to-point)：如果RSTP端口的Link-type为p2p，则可以通过RSTP的P/A机制等收敛方式实现快速收敛进入到Forwarding。

如果交换机的端口链路的工作模式为全双工，则Link-type=p2p

Shared：如果RSTP端口的Link-type为shared，则哪怕是RSTP，也依然需要经过discarding 15s，learning 15s才可以使用端口进入到forwarding。

如果交换机的端口链路的工作模式为半双工，则Link-type=Shared

SWI(config)#int g8/8 SWI(config-if)#spanning-tree Link-type ? point-to-point Consider the interface as point-to-point shared Consider the interface as shared

agreement, p1 forwarding p1 p2 p3 p4 p5 p6 p7 p8 p9 p10 p11 p12 p13 p14 p15 p16 p17 p18 p19 p20 p21 p22 p23 p24 p25 p26 p27 p28 p29 p30 p31 p32 p33 p34 p35 p36 p37 p38 p39 p40 p41 p42 p43 p44 p45 p46 p47 p48 p49 p50 p51 p52 p53 p54 p55 p56 p57 p58 p59 p60 p61 p62 p63 p64 p65 p66 p67 p68 p69 p70 p71 p72 p73 p74 p75 p76 p77 p78 p79 p80 p81 p82 p83 p84 p85 p86 p87 p88 p89 p90 p91 p92 p93 p94 p95 p96 p97 p98 p99 p100 p101 p102 p103 p104 p105 p106 p107 p108 p109 p110 p111 p112 p113 p114 p115 p116 p117 p118 p119 p120 p121 p122 p123 p124 p125 p126 p127 p128 p129 p130 p131 p132 p133 p134 p135 p136 p137 p138 p139 p140 p141 p142 p143 p144 p145 p146 p147 p148 p149 p150 p151 p152 p153 p154 p155 p156 p157 p158 p159 p160 p161 p162 p163 p164 p165 p166 p167 p168 p169 p170 p171 p172 p173 p174 p175 p176 p177 p178 p179 p180 p181 p182 p183 p184 p185 p186 p187 p188 p189 p190 p191 p192 p193 p194 p195 p196 p197 p198 p199 p200 p201 p202 p203 p204 p205 p206 p207 p208 p209 p210 p211 p212 p213 p214 p215 p216 p217 p218 p219 p220 p221 p222 p223 p224 p225 p226 p227 p228 p229 p230 p231 p232 p233 p234 p235 p236 p237 p238 p239 p240 p241 p242 p243 p244 p245 p246 p247 p248 p249 p250 p251 p252 p253 p254 p255 p256 p257 p258 p259 p260 p261 p262 p263 p264 p265 p266 p267 p268 p269 p270 p271 p272 p273 p274 p275 p276 p277 p278 p279 p280 p281 p282 p283 p284 p285 p286 p287 p288 p289 p290 p291 p292 p293 p294 p295 p296 p297 p298 p299 p300 p301 p302 p303 p304 p305 p306 p307 p308 p309 p310 p311 p312 p313 p314 p315 p316 p317 p318 p319 p320 p321 p322 p323 p324 p325 p326 p327 p328 p329 p330 p331 p332 p333 p334 p335 p336 p337 p338 p339 p340 p341 p342 p343 p344 p345 p346 p347 p348 p349 p350 p351 p352 p353 p354 p355 p356 p357 p358 p359 p360 p361 p362 p363 p364 p365 p366 p367 p368 p369 p370 p371 p372 p373 p374 p375 p376 p377 p378 p379 p380 p381 p382 p383 p384 p385 p386 p387 p388 p389 p390 p391 p392 p393 p394 p395 p396 p397 p398 p399 p400 p401 p402 p403 p404 p405 p406 p407 p408 p409 p410 p411 p412 p413 p414 p415 p416 p417 p418 p419 p420 p421 p422 p423 p424 p425 p426 p427 p428 p429 p430 p431 p432 p433 p434 p435 p436 p437 p438 p439 p440 p441 p442 p443 p444 p445 p446 p447 p448 p449 p450 p451 p452 p453 p454 p455 p456 p457 p458 p459 p460 p461 p462 p463 p464 p465 p466 p467 p468 p469 p470 p471 p472 p473 p474 p475 p476 p477 p478 p479 p480 p481 p482 p483 p484 p485 p486 p487 p488 p489 p490 p491 p492 p493 p494 p495 p496 p497 p498 p499 p500 p501 p502 p503 p504 p505 p506 p507 p508 p509 p510 p511 p512 p513 p514 p515 p516 p517 p518 p519 p520 p521 p522 p523 p524 p525 p526 p527 p528 p529 p530 p531 p532 p533 p534 p535 p536 p537 p538 p539 p540 p541 p542 p543 p544 p545 p546 p547 p548 p549 p550 p551 p552 p553 p554 p555 p556 p557 p558 p559 p560 p561 p562 p563 p564 p565 p566 p567 p568 p569 p570 p571 p572 p573 p574 p575 p576 p577 p578 p579 p580 p581 p582 p583 p584 p585 p586 p587 p588 p589 p590 p591 p592 p593 p594 p595 p596 p597 p598 p599 p600 p601 p602 p603 p604 p605 p606 p607 p608 p609 p610 p611 p612 p613 p614 p615 p616 p617 p618 p619 p620 p621 p622 p623 p624 p625 p626 p627 p628 p629 p630 p631 p632 p633 p634 p635 p636 p637 p638 p639 p640 p641 p642 p643 p644 p645 p646 p647 p648 p649 p650 p651 p652 p653 p654 p655 p656 p657 p658 p659 p660 p661 p662 p663 p664 p665 p666 p667 p668 p669 p670 p671 p672 p673 p674 p675 p676 p677 p678 p679 p680 p681 p682 p683 p684 p685 p686 p687 p688 p689 p690 p691 p692 p693 p694 p695 p696 p697 p698 p699 p700 p701 p702 p703 p704 p705 p706 p707 p708 p709 p710 p711 p712 p713 p714 p715 p716 p717 p718 p719 p720 p721 p722 p723 p724 p725 p726 p727 p728 p729 p730 p731 p732 p733 p734 p735 p736 p737 p738 p739 p740 p741 p742 p743 p744 p745 p746 p747 p748 p749 p750 p751 p752 p753 p754 p755 p756 p757 p758 p759 p760 p761 p762 p763 p764 p765 p766 p767 p768 p769 p770 p771 p772 p773 p774 p775 p776 p777 p778 p779 p780 p781 p782 p783 p784 p785 p786 p787 p788 p789 p790 p791 p792 p793 p794 p795 p796 p797 p798 p799 p800 p801 p802 p803 p804 p805 p806 p807 p808 p809 p810 p811 p812 p813 p814 p815 p816 p817 p818 p819 p820 p821 p822 p823 p824 p825 p826 p827 p828 p829 p830 p831 p832 p833 p834 p835 p836 p837 p838 p839 p840 p841 p842 p843 p844 p845 p846 p847 p848 p849 p850 p851 p852 p853 p854 p855 p856 p857 p858 p859 p860 p861 p862 p863 p864 p865 p866 p867 p868 p869 p870 p871 p872 p873 p874 p875 p876 p877 p878 p879 p880 p881 p882 p883 p884 p885 p886 p887 p888 p889 p890 p891 p892 p893 p894 p895 p896 p897 p898 p899 p900 p901 p902 p903 p904 p905 p906 p907 p908 p909 p910 p911 p912 p913 p914 p915 p916 p917 p918 p919 p920 p921 p922 p923 p924 p925 p926 p927 p928 p929 p930 p931 p932 p933 p934 p935 p936 p937 p938 p939 p940 p941 p942 p943 p944 p945 p946 p947 p948 p949 p950 p951 p952 p953 p954 p955 p956 p957 p958 p959 p960 p961 p962 p963 p964 p965 p966 p967 p968 p969 p970 p971 p972 p973 p974 p975 p976 p977 p978 p979 p980 p981 p982 p983 p984 p985 p986 p987 p988 p989 p990 p991 p992 p993 p994 p995 p996 p997 p998 p999 p1000 p1001 p1002 p1003 p1004 p1005 p1006 p1007 p1008 p1009 p1010 p1011 p1012 p1013 p1014 p1015 p1016 p1017 p1018 p1019 p1020 p1021 p1022 p1023 p1024 p1025 p1026 p1027 p1028 p1029 p1030 p1031 p1032 p1033 p1034 p1035 p1036 p1037 p1038 p1039 p1040 p1041 p1042 p1043 p1044 p1045 p1046 p1047 p1048 p1049 p1050 p1051 p1052 p1053 p1054 p1055 p1056 p1057 p1058 p1059 p1060 p1061 p1062 p1063 p1064 p1065 p1066 p1067 p1068 p1069 p1070 p1071 p1072 p1073 p1074 p1075 p1076 p1077 p1078 p1079 p1080 p1081 p1082 p1083 p1084 p1085 p1086 p1087 p1088 p1089 p1090 p1091 p1092 p1093 p1094 p1095 p1096 p1097 p1098 p1099 p1100 p1101 p1102 p1103 p1104 p1105 p1106 p1107 p1108 p1109 p1110 p1111 p1112 p1113 p1114 p1115 p1116 p1117 p1118 p1119 p1120 p1121 p1122 p1123 p1124 p1125 p1126 p1127 p1128 p1129 p1130 p1131 p1132 p1133 p1134 p1135 p1136 p1137 p1138 p1139 p1140 p1141 p1142 p1143 p1144 p1145 p1146 p1147 p1148 p1149 p1150 p1151 p1152 p1153 p1154 p1155 p1156 p1157 p1158 p1159 p1160 p1161 p1162 p1163 p1164 p1165 p1166 p1167 p1168 p1169 p1170 p1171 p1172 p1173 p1174 p1175 p1176 p1177 p1178 p1179 p1180 p1181 p1182 p1183 p1184 p1185 p1186 p1187 p1188 p1189 p1190 p1191 p1192 p1193 p1194 p1195 p1196 p1197 p1198 p1199 p1200 p1201 p1202 p1203 p1204 p1205 p1206 p1207 p1208 p1209 p1210 p1211 p1212 p1213 p1214 p1215 p1216 p1217 p1218 p1219 p1220 p1221 p1222 p1223 p1224 p1225 p1226 p1227 p1228 p1229 p1230 p1231 p1232 p1233 p1234 p1235 p1236 p1237 p1238 p1239 p1240 p1241 p1242 p1243 p1244 p1245 p1246 p1247 p1248 p1249 p1250 p1251 p1252 p1253 p1254 p1255 p1256 p1257 p1258 p1259 p1260 p1261 p1262 p1263 p1264 p1265 p1266 p1267 p1268 p1269 p1270 p1271 p1272 p1273 p1274 p1275 p1276 p1277 p1278 p1279 p1280 p1281 p1282 p1283 p1284 p1285 p1286 p1287 p1288 p1289 p1290 p1291 p1292 p1293 p1294 p1295 p1296 p1297 p1298 p1299 p1300 p1301 p1302 p1303 p1304 p1305 p1306 p1307 p1308 p1309 p1310 p1311 p1312 p1313 p1314 p1315 p1316 p1317 p1318 p1319 p1320 p1321 p1322 p1323 p1324 p1325 p1326 p1327 p1328 p1329 p1330 p1331 p1332 p1333 p1334 p1335 p1336 p1337 p1338 p1339 p1340 p1341 p1342 p1343 p1344 p1345 p1346 p1347 p1348 p1349 p1350 p1351 p1352 p1353 p1354 p135

## Day 52：VLAN之间通讯

需要在保证不同VLAN隔离广播域的前提条件之下VLAN之间单播通讯。

多臂路由实现VLAN之间通讯。

缺点：浪费接口扩展性非常差灵活性差

有扩展性，而且较为灵活。

“单臂”一旦出现故障，则全挂了。

**SW1:**

G0/0: Trunk Allow: 10 20G0/1: VLAN10G0/2: VLAN20PC1: 192.168.1.1/24 GW: 192.168.1.254PC2: 192.168.2.1/24 GW: 192.168.2.254

**R1:**

G0/0.10 192.168.1.254/24G0/0.20 192.168.2.254/24

4 SWI(config-vlan)#exit

5 SWI(config)#vlan 20 6 SWI(config-vlan)#name VLAN20 7 SWI(config-vlan)#exit

8 SWI(config)#interface g0/1 9 SWI(config-if)#switchport mode access

10 SWI(config-if)#switchport access vlan 10 11 SWI(config-if)#exit

12 SWI(config)#interface g0/2 13 SWI(config-if)#switchport mode access

14 SWI(config-if)#switchport access vlan 20 15 SWI(config-if)#exit

16 SWI(config)#interface g0/0 17 SWI(config-if)#switchport trunk encapsulation dot1q

18 SWI(config-if)#switchport mode trunk

19 SWI(config-if)#switchport trunk allow vlan 10,20 20 SWI#show vlan brief

22 SWI#show interface trunk

SWI:(Switch Virtual/VLAN Interface)

SWI(config)#int g0/0 SWI(config-if)#no switchport

**创建，并使用SVI接口需要满足的条件：**

创建对应的VLAN。

本交换机上至少有一个端口（Access，Trunk）允许该VLAN的数据流量通过。

默认情况下，交换机从二层接口收到数据流量时，默认按照数据链路层的MAC地址表转发。

如果数据包根据目的MAC地址将数据包送到了交换机三层接口上，则交换机将会按照路由表配合ARP表做三层转发。

路由器（客车）可以按照路由表转发数据包（载人，载客），交换机（拖拉机）也可以按照路由表转发数据包（载人载客），但是交换机（拖拉机）不能够完全顶替路由器（客车）

## Day 53：交换机安全(port-security)

**园区网交换技术**

**园区网交换安全技术**

MAC地址安全Port-securityVLAN安全PVLAN(Private VLAN)DHCP安全DHCP DHCP Snooping防止欺骗攻击（地址欺骗，ARP欺骗）IP Source BindingDAT(Dynamic ARP Inspection)

**Port-security:**

限制交换机端口对端只能够使用指定的设备。只有特定的指定设备可以使用网络，

可以限制交换机端口对端能够学习到的MAC地址数量。

```
SW1#show port-security interface g1/1
```

```
SW1#show port-security
```

数是如何的）

Port-security只有Access模式的交换机的端口可以开启（对面是终端）

```
SW1(config)#interface g1/1
```

```
SW1(config-if)#switchport mode access
```

```
SW1(config-if)#switchport port-security
```

默认情况下端口最多学习到一个MAC地址。一旦端口上学习到MAC地址超出上限，则端口直接被视为err-disabled状态并直接shutdown，不允许对方发送数据流量。

被置为Err-disabled状态的端口不会自动恢复为up状态。默认情况下只有管理员手动将端口shutdown，再no shutdown之后端口才会重新进入UP状态。

为了err-disabled。

```
SW1#show errdisable recovery
```

可以自动恢复

```
SW1(config)#erdisable recovery cause psecure-violation
```

口能够自动恢复

```
SW1(config)#erdisable recovery interval 120
```

**120s（默认300s）**

```
SW1(config-if)#switchport port-security maximum 3
```

址。

```
SW1#show port-security interface g1/1 address
```

地址是哪些。

```
SW1(config-if)#switchport port-security mac-address 5000.0004.0000
```

```
SW1(config)#int g1/1
```

```
SW1(config-if)#switchport port-security violation ?
```

protect Security violation protect mode

流量将会被过滤。（特殊味道）

restrict Security violation restrict mode

流量将会被过滤。（会产生日志）

shutdown Security violation shutdown mode

```
SW1(config)#int g1/1
```

```
SW1(config-if)#switchport port-security aging time 1
```

0min，与MAC地址表一样（5min）

//超出MAC地址上限非端口学习到的MAC地址

//超出MAC地址上限非端口学习到的MAC地址

text [[698, 807, 890, 818]]

//超出MAC地址上限非端口学习到的MAC地址

//修改惩罚的方式，默认为shutdown

1. 
SW1(config-if)#switchport port-security aging type ? 2 absolute Absolute aging (default) //绝对老化,端口上只要学习到MAC地址则开 始老化倒计时 3 inactivity Aging based on inactivity time period //相对老化,端口对端的流量停止时开始倒计 时老化. 
SW1(config-if)#switchport port-security aging static //手工绑定到端口上的MAC地址也允许其老化. 
SW1(config-if)#switchport port-security mac-address sticky //将当前端口上学习到的MAC地址自动静态绑定到端口上.

## Day 54：VLAN安全(VACL,PVLAN)

能够实现交换机当中相同VLAN之间的流量 过滤

需要交换机是三层交换机（或该交换机能够识别到数据包的网络层头部）

如果是二层交换机

方法一：在交换机端口里面敲ip device tracking（交换机端口可以识别IP和MAC的关联。）

方法二：MAC access-list

**一、使用Access-list 匹配上需要进行VACL过滤或放行的数据流量。**

1 ip access-list extended R1- ALL 2 permit ip host 192.168.1.1 192.168.1.0 0.0.0.255

**二、使用VLAN Access-map 调用ACL匹配的数据流量并指定行为动作为禁止或允许转发**

vlan access-map Deny_R1_to_ALL 10

**的配置语句界面**

match ip address R1- ALL action drop

为的数据流量默认 action drop

vlan access-map Deny_R1_to_ALL 20

**三、使用VLAN Filter调用VLAN Access-map中指定的行为动作并正式实行。**

```
SW1(config)#vlan filter Deny_R1_to_ALL vlan-list 10 map进行过滤。
```

```
SW1(config)#ip access-list extended R1- R3
```

```
SW1(config-ext-nacl)#permit ip host 192.168.1.1 host 192.168.2.3
```

```
SW1(config-ext-nacl)#exit
```

```
SW1(config)#vlan access-map Deny_R1- R3
```

```
SW1(config-access-map)#match ip address R1- R3
SW1(config-access-map)#
```

```
SW1(config-access-map)#action drop
```

```
SW1(config-access-map)#action drop
```

```
SW1(config-access-map)#exit
```

```
SW1(config-access-map)#exit
```

```
SW1(config)#vlan filter Deny_R1- R3 vlan-list all
```

使用MAC Access-list针对于数据流量做VACL过滤

mac access-list extended R1

permit host 5000.0002.0000 any

vlan access-map DenyR1 10

match mac address R1

action drop

vlan access-map DenyR1 20

action forward

vlan filter DenyR1 vlan-list all

过滤只能够过滤ARP（广播消息）

过滤只能够过滤ARP（广播消息）

Private VLAN(PVLAN)

可以在主VLAN旗下创建并管理子VLAN。

**隔离子VLAN:**

一个主VLAN旗下只能够有唯一的一个隔离子VLAN。

处于相同隔离子VLAN的端口之间相互隔离。

处于隔离子VLAN的端口不能够访问其它主VLAN,不能够访问其它子VLAN,也不能够访问自己相同的隔离子VLAN,可以离开混杂端口

**联盟子VLAN:**

一个主VLAN旗下可以有多个联盟子VLAN。

处于联盟子VLAN的端口只能够访问相同联盟子VLAN的端口。

处于联盟子VLAN的端口不能够访问其它主VLAN,不能够访问其它子VLAN,可以访问自己相同的联盟子VLAN。可以离开混杂端口

混杂端口:可以允许某个主VLAN旗下的任何子VLAN(包括隔离子VLAN和联盟子VLAN)

```
SW1(config)#vtp mode transparent
```

不会同步。

```
SW1(config)#vlan 10
```

> 💡 VTP透明模式或关闭VTP使得VLAN信息

//创建VLAN10。

## Day 55-56：DHCP 安全（DHCP 欺骗攻击防范、DHCP 中继、DHCP Snooping、IP 源保护）

> 注：原始 PDF 文件名缺失，此标题按笔记内容补拟。

```
SW1(config-vlan)#private-vlan primary //将VLAN10配置为PVLAN的主VLAN。 4
SW1(config)#vlan 100 //创建VLAN100 5
SW1(config-vlan)#private-vlan isolated //设置为隔离子VLAN 6
SW1(config)#vlan 101 //创建VLAN101 7
SW1(config-vlan)#private-vlan community //设置为联盟子VLAN 8
SW1(config)#vlan 10 //进入VLAN10 9
SW1(config-vlan)#private-vlan association 100,101 //将子VLAN与主VLAN进行关联 10
SW1#show vlan private-vlan //检查PVLAN的情况 11
SW1(config)#interface range g1/0-2 //进入端口 12
SW1(config-if-range)#switchport mode private-vlan host //将端口设置为PVLAN的HOST（终端）。 13
SW1(config-if-range)#switchport private-vlan host-association 10 100 //将端口划分进入主VLAN10的隔离子 VLAN100。 14
SW1(config)#interface range g1/2-3 //将端口划分进入主VLAN10的联盟子 VLAN101。 15
SW1(config-if-range)#switchport mode private-vlan host-association 10 101 //将端口划分进入主VLAN10的联盟子 VLAN101。 16
SW1(config-if-range)#switchport private-vlan host-association 10 101 //检查PVLAN的划分情况。 17
SW1#show vlan private-vlan //检查PVLAN的划分情况。 18
SW1(config)#interface g0/0 //配置端口为混杂模式。 19
SW1(config-if)#switchport mode private-vlan promiscuous //配置允许哪些主VLAN及其子VLAN通过。 20
SW1(config-if)#switchport private-vlan mapping 10 100,101 //配置允许哪些主VLAN及其子VLAN通过。
```

3 

PVLAN交换机不能够利用单臂路由实现VLAN之间通讯，只能够使用SV接口。

如果本次交换机当中主VLAN被用作PVLAN使用，则该主VLAN在本次交换机上不再能够被Access口使用。只要该VLAN运行了PVLAN，则该VLAN在本次交换机上不再能够作为Access口使用，哪怕划分了也不能够发送数据和使用。

```
R1(config)#ip dhcp pool A //创建地址池
R1(dhcp-config)#network 192.168.1.0 255.255.255.0 //设定该地址池可以分配的地址空间
R1(dhcp-config)#default-router 192.168.1.254 //设定分配的网关IP地址
R1(dhcp-config)#dns-server 8.8.8.8 114.114.114.114 //设定分配的DNS服务器地址DHCP保留地址（某些IPv4地址不需要分配）（路由器和交换机配置相同）在Cisco系统的全局模式下使用命令：
R1(config)#ip dhcp excluded-address 192.168.1.1 192.168.1.180 //排除掉192.168.1.1-192.168.1.180 180个连续地址不分配
R1(config)#ip dhcp excluded-address 192.168.1.188 //如果只需要排除一个地址则直接写上即可。
```

欺骗攻击之DHCP欺骗攻击防范。DHCP协议的工作方式手工配置IP地址将会出现以下问题：1. 配置量比较大。2. 容易产生IPv4地址冲突3. 灵活性比较差DHCP是一种用于集中对用户IP地址进行动态管理和配置的协议效率高灵活性强易于管理。

DHCP是一种C(Client)/S(Server)模型Client：可以使用DHCP协议希望自动得到分配IP地址的设备。

Server：可以提供DHCP服务，为Client分配地址的服务设备（Windows Server, Linux Server, 路由器, 交换机）房东DHCP基于UDP传输协议，DHCP Server使用UDP 67号端口；

DHCP Client使用UDP的68号端口DHCP的工作方式：一、发现阶段 - Discover（发现消息） DHCP客户端寻找DHCP服务器（租客找房东租房子）消息类型： DHCP Discover谁负责发送消息： DHCP Client数据包头部封装： 源IP： 0.0.0.0（未指定地址） 目的IP： 255.255.255.255（广播地址）数据帧头部封装： 源MAC： DHCP Client 目的MAC：广播MAC地址二、提供阶段 - Offer（提供消息） DHCP服务器告知DHCP Client可以分配给对方的地址（房东邀请租客看房）消息类型： DHCP Offer谁负责发送消息： DHCP Server数据包头部封装： 源IP： DHCP Server地址 目的IP：即将分配的IPv4地址数据帧头部封装： 源MAC： DHCP Server地址 目的MAC： DHCP Client的MAC地址三、选择阶段 - Request（请求消息） DHCP Client选择对应的HCP Server（租客看房子选房东准备签合同）DHCP Client会选择第一个收到的Offer消息作为DHCP Server消息类型： DHCP Request谁负责发送消息： DHCP Client数据包头部封装： 源IP： 0.0.0.0（未指定地址） 目的IP： 255.255.255.255（广播地址）数据帧头部封装： 源MAC： DHCP Client 目的MAC： DHCP Server的MAC地址四、确认阶段 - ACK（确认消息） DHCP Server确定开始租借地址（房东签好合同）消息类型： DHCP Offer谁负责发送消息： DHCP Server数据包头部封装： 源IP： DHCP Server地址 目的IP：即将分配的IPv4地址数据帧头部封装： 源MAC： DHCP Server地址 目的MAC： DHCP Client的MAC地址DHCP Server地址池的配置（路由器和交换机配置相同）

**路由器的绑定地址方式**

（选择使用Client-ID还是MAC地址绑定地址取决于设备使用的是Client-ID还是MAC地址。）

注意，Cisco默认的Client-ID比较特殊 

= Cisco 

  MAC 

  interface

```
Client2(config)#interface g0/0
```

```
Client2(config-if)#ip address dhcp client-id gigabitEthernet 0/0 //是的Cisco设备使用正常的Client-ID来获
```

取地址。

正常情况下，一台设备获取IP地址时，其Client-ID 

= 01 

  MAC地址。

```
R1#show ip dhcp binding
```

**的绑定表项**

利用Client-ID给设备绑定地址

```
R1(config)#ip dhcp pool CLIENT1
```

```
R1(dhcp-config)#host 192.168.1.150 255.255.255.0
```

```
R1(dhcp-config)#client-identifier 0063.6973.636f.2d35.3030.302e.3030.3066.2e30.3030.302d.4769.302f.30 //设置
```

**设备的Client-ID**

```
R1(dhcp-config)#default-router 192.168.1.254
```

```
R1(dhcp-config)#dns-server 8.8.8.8 114.114.114.114
```

利用MAC地址给设备绑定地址

```
R1(config)#ip dhcp pool CLIENT1
```

```
R1(dhcp-config)#host 192.168.1.150 255.255.255.0
```

```
R1(dhcp-config)#hardware-address 0050.5686.4860
```

```
R1(dhcp-config)#default-router 192.168.1.254
```

```
R1(dhcp-config)#dns-server 8.8.8.8 114.114.114.114
```

交换机作为DHCP Server给设备绑定地址。

```
Switch(config)#ip dhcp pool A
```

```
Switch(dhcp-config)#network 192.168.1.0 255.255.255.0
```

```
Switch(dhcp-config)#default-router 192.168.1.254
```

```
Switch(dhcp-config)#dns-server 8.8.8.8 114.114.114.114
```

```
Switch(dhcp-config)#address 192.168.1.150 client-identifier
```

0063.6973.636f.2d35.3030.302e.3030.3066.2e30.3030.302d.4769.502f.30

```
Switch(dhcp-config)#address 192.168.1.150 client-identifier 0150.0000.1000.00 //交换机可以直接在地址池当中绑定设备
```

的IPv4地址。

```
Switch(dhcp-config)#address 192.168.1.151 hardware-address 0050.5686.4860 //MAC地址也可以。
```

**DHCP中继：**

DHCP 的消息大多是广播消息，其将会被路由器进行隔离，无法跨越网络传输。

因此，在没有DHCP中继的环境之下，只能够在与DHCP Client直连的链路上配置DHCP Server...对于DHCP的灵活性和管理上效率极差。

DHCP中继 = 寻找一个用户中（中继设备）为 租客（DHCP Client）和 房东（DHCP Server）之间单独转接。

DHCP客户端所在的网络与DHCP Server的IP地址之间需要能够互相通讯

与DHCP客户端直连的DHCP中继设备需要配置DHCP中继服务。

DHCP中继设备需要在连接终端设备链路的端口上配置IP helper-address...

ip helper-address <DHCP Server IP>

DHCP中继设备从端口收到DHCP Client的消息时，将会用 收到该消息的接口地址为源 向DHCP Server转交该DHCP消息。

DHCP Server收到中继的DHCP消息时，将会把回复的DHCP Offer或DHCP ACK消息单独转发给DHCP中继设备的地址。

DHCP Server收到中继的DHCP Discover消息时，将会从DHCP中继地址相同网段的地址池当中挑选IPv4地址回复Offer消息

当DHCP Server收到DHCP中继的DHCP Discover消息时，DHCP中继的地址可以匹配上本路由器当中多个地址池，按照掩码更长的地址池进行匹配。（哪个地址池当中地址更少）

**DHCP Snooping:**

**包含的端口角色**

Trust（信任端口）：接口可以向外发送DHCP Discover消息和DHCP Request消息，可以接收DHCP Offer消息和DHCP ACK消息。

Untrust（不信任端口）：接口不向外发送DHCP Discover消息和DHCP Request消息，不接收DHCP Offer消息和DHCP ACK消息。

交换机一旦开启DHCP Snooping，则交换机上的所有端口都将会变成 不信任端口。

交换机之间互联的Trunk接口需要开启信任接口。2. 连接合法DHCP Server的接口需要配置为信任端口。

1. 
SW2(config)#ip dhcp snooping //总开关2 
SW2(config)#ip dhcp snooping vlan 1 //针对于哪一个VLAN启用DHCP Snooping3 
SW1(config)#interface g1/1 //将某一个端口配置为DHCP4 
SW1(config-if)#ip dhcp snooping trust //将某一个端口配置为DHCP Snooping的信任端口。

开启DHCP Snooping的交换机针对于DHCP Client发送的Discover以及Request消息默认都会插入DHCP Snooping的Option 82消息

**Option 82中消息类型的含义：**

Agent Circuit ID: 00（消息类型）04（本字段的长度）0001（VLAN_ID）01（接口号码）收到的DHCP Discover消息对应的VLAN和交换机的接口号码

**Agent Remote ID:**

00（消息类型）06（本字段的长度）5000 0002 0000（设备的MAC地址）包含了收到该DHCP Discover消息的交换机MAC地址。

告诉DHCP Server这是哪一个交换机上哪一个VLAN的哪一个接口对端的主机所发送的DHCP Discover。

```
SW2(config)#no ip dhcp relay information option //使用该命令可以使得交换机不插入Option82（一般不用）
```

DHCP Snooping Untrust接口的另一个特点：

默认情况下不信任untrust端口收到的带有Option82的DHCP消息。

默认交换机都有以下指令

**82消息**

ip dhcp snooping information option allow-untrusted

收。

interface g0/1

收。

DHCP Relay information(option 82)在DHCP Server上的操作。

默认情况下DHCP Server收到了带有Option82消息的DHCP消息时，认为不安全，不信任其DHCP消息。

**方法一：**

```
R1(config)#interface g0/0
```

```
R1(config-if)#ip dhcp relay information trusted
```

**方法二：**

```
R1(config)#ip dhcp relay information trust-all
```

DHCP消息。

DHCP Snooping表

```
SW2#show ip dhcp snooping binding
```

MacAddress IpAddress Lease(sec) Type

50:00:00:06:00:00 192.168.1.105 86364

50:00:00:07:00:00 192.168.1.104 86348

Total number of bindings: 2

哪个主机对应DHCP获取的地址。

哪个主机对应DHCP获取的地址。

**IP源保护**

使得交换机对端的设备必须使用指定的IPv4地址才能够上网。对方只要私自更改了自己的IPv4地址就不允许上网。

```
SW2(config)#interface f0/1
```

```
SW2(config-if)#ip verify source
```

```
SW2#show ip verify source
```

> 💡 开启IP源保护

**//查看IP源保护表**

只要开启了IP源保护，则交换机当中将会立刻产生IP源保护表。只有IP源保护表当中存在对应接口条目以及IP地址信息，才能够访问网络。只要在源保护表项当中没有对应的信息，则禁止对方的数据流量。

默认情况下IP源保护需要与DHCP Snooping联用IP源保护表将会从DHCP Snooping binding表当中抽取接口对端的地址，VLAN，以及相关信息存进IP源保护表

```
SW2(config)#interface range f0/1- 2
```

```
SW2(config-if-range)#ip verify source port-security //开启IP源保护同时联合Port-security，同时保护IP地址和MAC地址。
```

IP源保护可以手工静态的绑定交换机对端设备的IP和MAC地址

```
SW2(config)#ip source binding 081b.5482.f2f6 vlan 1 192.168.1.188 interface f0/1 //绑定交换机端口对端VLAN，MAC地址以及IP地址。
```

```
SW2#show ip source binding
```

> 💡 查看IP源绑定表项。

IP源绑定表项当中包含了从DHCP Snooping中提取的表项内容和手工绑定的表项内容。

帮我识别每个PDF中的文字。所有文字都要识别输出，不要省略。不要总结。按照day日期大小进行排序

## Day 57：DAI(Dynamic ARP Inspection),EtherChannel

对于主机而言，其ARP缓存也存在 新庆旧（针对于同一个IPv4地址，将会关联上最后收到的ARP回复消息对应的MAC地址。）

仅适用于ARP消息头部的检测。

DAI技术将会作用在交换机上，使得交换机针对于端口对端的设备IPv4地址进行识别，如果对端的设备发送了与其IPv4地址不相符的ARP回复消息，则直接过滤，禁止。可以借用DHCP Snooping的绑定表项联动实现DAI检测功能。

```
SW2(config)#ip arp inspection vlan 1
```

> 💡 在全局下开启DAI。

一旦交换机开启DAI，则交换机的所有端口都会变成 untrust 接口，针对于untrust接口收到的ARP消息，将会检查其ARP头部当中关于源IP地址和MAC地址的对应关系是否与DHCP Snooping绑定表中该接口对端的IP和MAC地址对应关系一致，如果一致，则允许接收该ARP消息，如果不一致则直接丢弃。

可以将交换机的接口配置为 Trust，针对于信任端口则不进行ARP检查。

**静态的DAI检测配置方式**

```
SW2(config)#ip arp inspection vlan 1
```

```
SW2(config)#arp access-list DAI
```

list

```
SW2(config-arp-nacl)#permit ip host 192.168.1.100 mac host 001b.5482. f2f
```

送ARP。

```
SW2(config)#ip arp inspection filter DAI vlan 1
```

> 💡 当网关关闭时，//当前接口上包的数量超过了上述设

需要注意的是ARP的Access-list由自带一句deny any，未在ARP的Access-list当中放行的设备同样自动deny，禁止其发送ARP消息。

交换机之间的Trunk接口一般也被配置为DAI的信任端口

```
SW2(config-if)#storm-control ? <pps:packet Per seconds 每秒数据包（百分比）>
```

broadcast Broadcast address storm control

multicast Multicast address storm control

unicast Unicast address storm control

```
SW2(config-if)#storm-control action ?
```

置的限额设置惩罚方式。

shutdown Shutdown this interface if a storm occurs

trap Send SNMP trap if a storm occurs

**EtherChannel:**

将交换机的多个接口（链路）聚合绑定成为一个逻辑接口，形成一条逻辑链路，做到（防环，冗余，高带宽）

带宽（如果是Cisco设备，接口带宽>10M），带宽需要一致才能聚合。

双工模式必须一致。

VLAN（Access所属的VLAN需要相同，Trunk native vlan，allow vlan需要相同。）

二层/三层接口需要相同。

除开上述以外的条件以外都不是硬性条件，但是，理论上来说还是全部一样为妙。

**Static:**

不协商，强制性使得交换机的端口进行聚合。

```
SW1(config)#interface f0/11
```

```
SW1(config-if)#channel-group 1 mode on //使得F0/11接口输入channel-group组1号小组，该组是静态EtherChannel，生成Port-channel1逻辑接口
```

```
SW1(config)#interface f0/12
```

```
SW1(config-if)#channel-group 1 mode on //使得F0/12接口输入channel-group组1号小组，该组是静态EtherChannel，生成Port-channel1逻辑接口
```

```
SW1#show etherchannel summary //检查ethernchannel的情况。
```

```
SW1#show interface port-channel 1 //查看该接口的参数情况
```

```
SW1#show etherchannel summary
```

Flags: D - down P - bundled in port-channel

I - stand-alone s - suspended

H - Hot-standby (LACP only)

R - Layer3 S - Layer2

U - in use f - failed to allocate aggregator

M - not in use, minimum links not met

u - unsuitable for bundling

w - waiting to be aggregated

d - default port
12 13

常用子双方是不同厂商设备，且LACP协商无用的时侯可以使用静态的EtherChannel。

最多支持8条链路进行聚合，多余8个接口以外的接口将作为备份接口使用。

Desirable:主动协商

**Auto:被动协商**

```
SW1(config)#interface range f0/11- 12
```

```
SW1(config-if-range)#channel-group 2 mode desirable
```

EtherChannel.

**LACP:**

能用LACP就用LACP.不能用LACP才用静态。

**Active:主动协商**

**passive:被动协商**

```
SW1(config)#interface range f0/11- 12
```

```
SW1(config-if-range)#channel-group 2 mode active
```

EtherChannel.

//可以同时对多个接口做操作加入端口组形成

**第一页内容**

FHRP(First hop redundancy protocol) 网关冗余协议

没有网关冗余的网络

主机对于网关是否存活没有探测机制

网关一旦断开，则失去上网的能力。

没有冗余，网关一旦断开没有切换到备份路径的能力。

**ICMP重定向**

路由接收到数据包时，发现数据包的源IP地址与数据包转发的下一跳IP地址处于同网段，则将会进行路径的优化(ICMP重定向)

将会向数据包的源IP发送ICMP的重定向消息告知对方访问目标IP地址的正确下一跳地址。

**FHRP协议**

HSRP(Hot Standby Router Protocol):热备份路由协议 Cisco私有的，普遍运用多

VRRP(Virtual Router Redundancy Protocol):虚拟路由冗余协议 公有 普遍运用多

GLBP(Gateway Load-Balance Protocol):网关负载分担协议 Cisco私有 最厉害

**HSRP:**

在网关设备连接终端主机的三層接口上运行HSRP网关冗余协议：

一旦激活接口运行HSRP则将会立刻开始发送Hello包(3s/10s)进行HSRP角色的选举

Active: Active路由器

Standby: 备份路由器

Listener: 既不是Active，也不是Standby。

Standby 是 Active的备份；Listener是Standby的备份

运行HSRP时，网关设备需要指定HSRP的Group组以及虚拟的IPv4地址。每一个虚拟的IPv4地址都会拥有相同的虚拟MAC地址。

HSRP当中虚拟IPv4地址的MAC地址为：0000.0c07.acXX XX=HSRP虚拟IP地址中的group号码

谁是Active路由器，谁就拥有IP地址的拥有者，只有Active路由器可以回复ARP Reply

一旦standby设备成为了新的Active后会马上发送声明的ARP，更换交换机的MAC地址表项，实现网关的切换。

**运行HSRP的条件：**

• 虚拟IPv4地址的group号码相同

• 虚拟的IPv4地址要相同

• 虚拟的IPv4地址需要做接口地址处于同一网段。

**HSRP选举Master的方式：**

• 优先比较网关设备的HSRP Priority(优先级)，默认100，越大越优先

• 优先级相同则比较接口的IP地址，越大越优先

text

```
R2(config)#interface g0/0
R2(config-if)#standby 1 ip 1.1.1.254 254                                //接口中指定接口的虚拟Group号
```

> 💡 和虚拟IPv4地址。

```
R2(config-if)#standby 1 priority 110                                   //通过此命令调整HSRP的Group
```

> 💡 优先级大小。

```
R2(config-if)#standby 1 preempt                                        //开启抢占功能。
R2(config-if)#standby 1 timers 1 5                                    //调整HSRP的timers
R2(config-if)#standby 1 name v50                                      //可以修改Group的名称。
R2(config-if)#standby 1 preempt delay minimum 2                       //发现自己优先级更大不要急着抢
```

> 💡 占，等待2秒后再抢

```
R2#show standby                                                       //查看HSRP的详细信息。
R2#show standby brief                                                 //查看HSRP的简要信息
```

HSRPv1的虚拟IPv4地址为224.0.0.2(路由设备)

HSRP默认关闭了抢占功能，哪怕本路由器的优先级比当前的Active或Standby更加优异，也不会主动抢夺对手的角色。

HSRP会关闭ICMP重定向。

**第二页内容**

text

```
R3(config)#track 1 interface g0/3 line-protocol                       //创建跟踪项目，跟踪接口的链路情况。
R3(config)#interface g0/0
R3(config-if)#standby 1 track 1 decrement 30                         //HSRP发现Track down了之后自动降低30优先级。
R3(config-if)#standby 1 track 1 shutdown                             //HSRP发现Track down了之后直接丢弃所有角色，
```

> 💡 成为HSRP的Init状态

```
R3(config)#ip sla 1
R3(config-ip-sla)#icmp-echo 1.1.1.1 source-interface g0/3           //创建探针，周期性的默认每隔6s向对方发送ICMP
```

> 💡 探测请求。

```
R3(config-ip-sla)#ip sla schedule 1 start-time now life forever       //探针开始工作
R3(config)#track 2 ip sla 1 reachability                              //使用track跟踪探针的探测结果。
R3(config)#interface g0/0
R3(config-if)#standby 1 track 2 shutdown                             //HSRP发现Track down了之后直接丢弃所有角色，
```

> 💡 成为HSRP的Init状态

HSRPv2

text

```
R2(config)#interface g0/0
R2(config-if)#standby version 2                                      //接口运行HSRPv2
```

HSRPv1只支持256个group组，HSRPv2支持4096个group组

HSRPv1使用组播地址224.0.0.2，HSRPv2使用的组播地址为224.0.0.102

VRRP

一旦激活接口运行VRRP，接口将会开始发送VRRP的Hello包(1s/3s)，目标组播地址为224.0.0.18。

**选举角色：**

**Master: 主设备**

backup: 从设备

默认只有Master设备会每隔周期时间发送Hello包，backup设备只侦听，一旦超过hold时间收不到Master的Hello包，则重新选举新的Master。

VRRP group组的MAC地址为： 0000.5e00.01YY YY即为VRRP Group组的号码。

谁是Master，谁就是该虚拟IP地址以及虚拟MAC地址的拥有者

只有Master设备可以回复ARP请求。

**VRRP选举Master设备的方式：**

• 优先比较网关设备的VRRP Priority(优先级)，默认100，越大越优先

• 优先级相同则比较接口的IP地址，越大越优先

text

```
R2(config)#interface g0/0
R2(config-if)#vrrp 1 ip 1.1.1.1.234.254                               //接口运行VRRP Group-1,虚拟IP地
```

> 💡 址1.1.1.1.234.254

```
R2(config-if)#vrrp 1 priority 105                                    //通过此命令可以调整VRRP的优先级大
```

> 💡 小。

```
R2(config-if)#vrrp 1 timers advertise 20                              //调整VRRP的Hello包周期时间
R2#show vrrp                                                         //查看VRRP的详细参数信息。
R2#show vrrp brief                                                   //查看VRRP的简要信息
```

VRRP默认开启了抢占功能。

VRRP中优先级25较特殊，无法通过手动的方式修改Group的优先级为255，当设备指定自己的物理接口地址作为VRRP虚拟地址时，固定其优先级为255。

VRRP可以直接使用物理IP地址来作为虚拟的IPv4地址使用。

text

```
R3(config)#track 1 interface g0/3 line-protocol
R3(config)#interface g0/0
R3(config-if)#vrrp 1 track 1 decrement 20
```

> 💡 当Track down了时自动减低优先级

                                                                       //20

FHRP 配合DHCP中继

text

```
R2(config)#int g0/0
R2(config-if)#ip helper-address 1.1.1.1 redundancy hsrp-G1/0-1       //部署DHCP中继，且当自己是FHRP的
```

> 💡 Active设备时才会做中继。

**第三页内容**

GLBP(Gateway Load-balance protocol)

AVF: 活动的虚拟转发者 只要处于同一个group组当中，运行相同虚拟IP地址的GLBP路由器都是该Group组当中的AVF路由器。

一个group里最多存在4个AVF。

每一个AVF有自己对应的虚拟MAC地址。

MAC地址格式为 0007.b400.xxYY XX = group 号码 YY = AVF的号码

举个例子 group 1 当中的 AVF1路由器，其虚拟MAC地址为 0007.b400.0101

每一个AVF都可以知道其它AVF设备的信息，每一个AVF都是自己AVF的Active路由器。针对于每一个AVF也会选举Listener(类似HSRP。)

谁是AVF的Active路由器，谁就是该AVF MAC地址的拥有者。

AVG: 活动的虚拟网关：一个group组中只能有一台路由器成为Active AVG，其它路由器可以选举成为standby AVG，或listener AVG(类似HSRP)

只有Active AVG 可以回复ARP的请求消息。

AVG在回复ARP的Reply的时候将会采用轮询的方式进行ARP的回复，轮询地回复 AVF1,AVF2,AVF3....AVF1,AVF2,AVF3....AVF1 的MAC地址

text

```
R2(config)#interface g0/0
R2(config-if)#glbp 1 ip 1.1.1.1.234.254                              //接口运行Glbp Group-1,虚拟IP地
```

> 💡 址1.1.1.1.234.254

```
R2(config-if)#glbp 1 priority 110                                    //调整GLBP的优先级大小。
R2(config-if)#glbp 1 preempt                                         //开启GLBP的抢占功能
R2(config-if)#glbp 1 forwarder preempt delay xx                      //默认AVF开启抢占且抢占延时为
```

> 💡 30s。

AVG的选举.（与HSRP相同）

• 优先比较网关设备的GLBP Priority(优先级)，默认100，越大越优先

• 优先级相同则比较接口的IP地址，越大越优先

GLBP中 AVG默认关闭抢占功能。

**AVF的选举**

在GLBP当中 AVF不可抢占，可以让责。当自己的Active AVF挂了之后，其它AVF检测到当前AVF出现故障，可以针对于该AVF重新选举Active AVF；或当开启了Track跟踪功能，当AVF的weight值小于AVF自己设定的区间范围时，则可以出让AVF的角色，使得其它路由器来选举本AVF的Active

**AVF的抢占默认开启的**

AVF的weight值默认为100。

text

```
R2(config)#track 1 interface g0/2 line-protocol                       //创建Track 1跟踪上行链路的状态。
R2(config)#interface g0/0
R2(config-if)#glbp 1 weighting 100 lower 90                          //当weight低于90，则会舍弃自己AVF的
```

> 💡 active 角色。

```
R2(config-if)#glbp 1 weighting track 1 decrement 20
```

Day 60 & 61 & 62 & 63 - SPAN, QOS专题

**端口镜像技术**

可以针对于交换机端口收到或发送出去的数据包镜像复制一份转发到另一个接口。

**本地端口镜像**

```
Switch(config)#monitor session 1 source interface gigabitEthernet 0/1 rx //针对于G0/1接口收到的数据作为源。
Switch(config)#monitor session 1 destination interface g0/2 //针对于源所打包好的数据镜像转发到G0/2端口。
```

```
Switch(config)#monitor session 1 source vlan 1 //针对于所有VLAN1"both"的数据
Switch(config)#monitor session 1 destination interface g0/2 //镜像转发到G0/2接口
```

monitor session source 要么只能够source 接口的数据或只能source VLAN的数据，同一个session当中不能同时的source interface和VLAN。

RSPAN(Remote SPAN)

```
Switch(config)#vlan 500 //创建
```

VLAN500

```
Switch(config-vlan)#remote-span //设定为RSPAN对应的VLAN。
Switch(config)#monitor session 1 source interface g0/1 both //指定monitor session的源
Switch(config)#monitor session 1 destination remote vlan 500 //通过RSPAN的VLAN500将数据发送到其它交换机。
```

**对端交换机:**

```
Switch(config)#vlan 500 //创建
```

VLAN500

```
Switch(config-vlan)#remote-span //设定为RSPAN对应的VLAN。
Switch(config)#monitor session 1 source remote vlan 500 //将RSPAN的VLAN500的数据作为源。
Switch(config)#monitor session 1 destination interface g1/0 //将RSPAN收到的VLAN500的数据给到G1/0
```

QOS(Quality of Service) 服务质量

在带宽优先的情况下使得某些数据流量能够更加稳定，高效，或低延时地进行转发。

**QOS中重要的组件：**

可用带宽- - - - - - - - - - - - - - - - - - - - - 整段路径上链路的最小带宽。

延时 - - - - - - - - - - - - - - - - - - - - 传输延时（电信号在传输介质上传递需要的时间）+进程延时（设备处理数据包所需损耗的时间）+队列延时（数据包送到出接口排队所需要的时间）

丢包 - - - - - - - - - - - - - - - - - - - - 队列（出方向有硬件队列和软件队列用于数据包出方向转发进行排队）如果队列排满，后续的数据包将不允许再进入队列，执行丢包措施

**QOS的三种服务模型：**

尽力而为模型 （不做QoS）- 统一集成式服务模型 （仅运营商使用）RSVP（资源预留协议）- 区分服务模型 （使用最广泛，最常用的服务模型）上下游独立。

Flow：相同五元组的数据流量称之为一个Flow。相同源IP地址，相同目的IP地址，相同源端口号，相同目的端口号，相同协议号。

Inbound traffic stream → Classifier → (Meter) → Marker → Conditioner → Queuing (Scheduling Dropping)

分类：ACL：访问控制列表一般常用扩展的访问控制列表（标准ACL可以根据实际情况使用）：正好可以匹配源自IP地址，源自端口号以及协议号。

```
R2(config)#ip access-list extended R1- R6 
R2(config-ext-nacl)#permit ip host 1.1.1.1 host 6.6.6.6 
R2(config-ext-nacl)#exit 配出数据流量（分类）
```

**打标记：**

TOS字段所默认使用的表示优先级的协议为：DSCP

DSCP（区分服务代码点）

DSCP共6bits。最后三个bit如果等于0，则表示IPprecedence，只要最后三位不是0，则表示使用默认DSCP协议表示优先级。

前三个bits称之为PHB（per hop behavior）字段

[DSCP 6 bits diagram]

000 = Default

001,010,011,or100 = AF

101 = EF

000 = Class Selector

PHB	Type	表示含义

000	默认行为数据流量	尽可能传输

001	AF1	加速转发等级一，大多数网络当中不是特别必要的数据流量

010	AF2	加速转发等级二，大多数网络当中点播的视频流量

011	AF3	加速转发等级三，大多数网络当中的直播数据流量

100	AF4	加速转发等级四，企业中的语音节点或会议视频节点数据流量

101	EF	低延时转发，最快最猛地转发效率，最快速度最优先转发数据流量。

[DSCP bits diagram: 1 0 1 1 1 0]

最后三个bit可以表示该数据包的丢弃概率，最后一个bits始终固定为0，用倒数第二和第三bit表示丢弃概率

<table> Drop probability bits 丢弃概率 01 低概率被丢弃 10 中等概率被丢弃 11 有很大概率被丢弃 </table>

0 0 1 0 1 0 DSCP = AF11 325P-007

<table> Class <td colspan="2">Value AF1 001dd AF2 010dd AF3 011dd AF4 100dd </table><table> Drop Probability (dd)Value AF Value Low 01 AF11 Medium 10 AF12 High 11 AF13 </table>

IP precedence（可以立即为DSCP当中的特殊情况。）

用三个bits来区分优先级大小，共8种等级，分为8- 7级。

**越大越优先**

PBR工具用于打标标记 仅能够设置IP precedence优先级的表示方式。

```
R2(config)#ip access-list extended R1-R6
R2(config-ext-nacl)#permit ip host 1.1.1.1 host 6.6.6.6
R2(config-ext-nacl)#exit
R2(config)#route-map PBR permit 10
R2(config-route-map)#match ip address R1-R6
R2(config-route-map)#set ip precedence ?
```

<0-7>

Precedence value

critical Set critical precedence (5)

flash Set flash precedence (3)

flash-override Set flash override precedence (4)

immediate Set immediate precedence (2)

internet Set internetwork control precedence (6)

network Set network control precedence (7)

priority Set priority precedence (1)

routine Set routine precedence (0)

```
R2(config-route-map)#set ip precedence 7
R2(config-route-map)#exit
R2(config)#interface f0/0
R2(config-if)#ip policy route-map PBR //在收到流量的入方向调用。
```

MQC（模块儿化的QOS命令行）一专门设计为QOS使用，用于分类，标记，保障带宽，限速，拥塞避免...

Class-map 分类 Policy-map 标记，保障带宽，限速，拥塞避免... Service-Policy 调用Policy-map.

```
R2(config)#class-map ?
```

WORD class-map name

match-all Logical-AND all matching statements under this classmap

match-any Logical-OR all matching statements under this classmap

```
R2(config)#class-map ACL
R2(config-cmap)#match access-group name R1-R6
```

class-map调用ACL匹配需要QoS的数据流量

```
R2(config-cmap)#exit
R2(config)#policy-map PMAP
```

Policy-map

8. R2(config-pmap)#class ACL //调用 Class-map ACL分类的数据
9. R2(config-pmap-c)#set dscp ?

10 <0-63> Differentiated services codepoint value

11 af11 Match packets with AF11 dscp (001010)

12 af12 Match packets with AF12 dscp (001100)

13 af13 Match packets with AF13 dscp (001110)

14 af21 Match packets with AF21 dscp (010010)

15 af22 Match packets with AF22 dscp (010100)

16 af23 Match packets with AF23 dscp (010110)

17 af31 Match packets with AF31 dscp (011010)

18 af32 Match packets with AF32 dscp (011100)

19 af33 Match packets with AF33 dscp (011110)

20 af41 Match packets with AF41 dscp (100010)

21 af42 Match packets with AF42 dscp (100100)

22 af43 Match packets with AF43 dscp (100110)

23 cs1 Match packets with CS1(precedence 1) dscp (001000)

24 cs2 Match packets with CS2(precedence 2) dscp (010000)

25 cs3 Match packets with CS3(precedence 3) dscp (011000)

26 cs4 Match packets with CS4(precedence 4) dscp (100000)

27 cs5 Match packets with CS5(precedence 5) dscp (101000)

28 cs6 Match packets with CS6(precedence 6) dscp (110000)

29 cs7 Match packets with CS7(precedence 7) dscp (111000)

30 default Match packets with default dscp (000000)

31 ef Match packets with EF dscp (101110)

32

33. R2(config-pmap-c)#set dscp AF41 //设置DSCP AF41优先级
34. R2(config-)#interface f0/0 //接口下入方
35. R2(config-)#service-policy input PMAP

36 ---

37. R2(config-)#interface f0/1 //也可以选择
38. R2(config-)#service-policy output PMAP 出方向。

队列： 每一个设备在接口的出方向都会预留一块缓存，用于存放来不及处理转发的数据包。

存放数据包的方式将会采用队列来进行存放。

队列 - - - - - > 软件队列 + 硬件队列（出接口）

设备将数据包送到软件队列，经过软件队列的筛选器送到硬件队列，最终离开硬件队列即可从端口转发出去。

如果硬件队列和软件队列都已排满，则后续进入到缓存的数据包将会被直接丢弃，称之为丢包

可以调整设备的软件队列，调整数据包的队列机制，调度机制 ===> 重要的数据包优先得到调度，优先转发，不重要的数据包不会被优先转发，可能会有丢包。

如何分类？ 如何排队？如何调度？

FIFO（First in First out）：先入先出队列

**如何分类——视同仁**

如何排队——只有一支队伍排队，按照进入队列的顺序来排队。

如何调度——最先进入到队列的数据包得到优先转发，按照顺序依次转发。

硬件队列默认都是FIFO并且不可调整。

默认情况下只要设备的接口带宽 ≥ 2Mbps，则默认软件队列也为FIFO。

默认情况下FIFO的队列深度为40（最多40个数据包排队。）

PQ（priority queue）：优先级队列

如何分类——默认数据流量的优先级都是Normal，可以认为抓取出数据流量并且设定其流量的优先级。

如何排队——每一个优先级都有自己的队列（一共四个优先级，四个队列），数据流量按照优先级去对应的队列当中排队。

如何调度——按照优先级的大小，从高到低进行调度。

每一次调度都会从高优先级队列开始查看，只要高优先级队列有数据包则优先转发，高优先级队列如果没有数据包，则查看中等优先级队列，如果有数据包则优先转发，

转发完成之后再一次从高优先级队列开始查看。

只要优先级高的队列有数据包则永远得到优先转发。

[PQ调度流程图: Packet in HIGH queue? → Yes → Dispatch packet and start checking the HIGH queue again → No → Packet in MEDIUM queue? → Yes → Dispatch ... → No → Packet in NORMAL queue? → Yes → Dispatch ... → No → Packet in LOW queue? → Yes → Dispatch ... → No → Hardware Q]

```
R2(config)#access-list 100 permit ip host 1.1.1.1 host 6.6.6.6
R2(config)#access-list 101 permit ip host 1.1.1.1 host 5.5.5.5
R2(config)#access-list 102 permit ip host 1.1.1.1 any
R2(config)#priority-list 1 protocol ip high list 100 //ACL100的数据流量高优先级队列
R2(config)#priority-list 1 protocol ip medium list 101 //ACL101的数据流量中等优先级队列
R2(config)#priority-list 1 protocol ip low list 102 //ACL102的数据流量低优先级队列
R2(config)#priority-list 1 default normal //其它数据默认普通优先级队列。
R2(config)#interface s1/0
R2(config-if)#priority-group 1 //接口下调用PQ。
R2#debug priority //查看PQ的日志。
```

**PQ的队列深度默认：**

High: 20

Medium: 40

Normal: 60

Low: 80

```
R2(config)#priority-list 1 queue-limit 10 10 60 60
```

> 💡 该命令可以调整队列的深度。

CQ(Custom Queueing): 公平队列(自定义队列)

如何分类 → 可以人为的匹配和控制数据流量。

如何排队 → 有十六个队列可以进行排队, 可以人为的控制数据流量去对应的队列当中进行排队。

如何调度 → 采用轮询的调度方式, 逐个按照顺序每一个队列发送一定的数据。

太公平了。

容易造成延时不平均而产生抖动问题。

引入了0号队列(第17个队列), 0号队列和其它16个队列之间的关系是PQ关系。只要0号队列当中有数据包先发送0号队列的数据, 0号队列没有数据时, 其它队列轮询公平队列。

```
R2(config)#access-list 100 permit ip host 1.1.1.1 host 6.6.6.6
R2(config)#access-list 101 permit ip host 1.1.1.1 host 5.5.5.5
R2(config)#access-list 102 permit ip host 1.1.1.1 any
R2(config)#queue-list 1 protocol ip 1 list 100 //ACL100的数据流量1号队列
R2(config)#queue-list 1 protocol ip 2 list 101 //ACL101的数据流量2号队列
R2(config)#queue-list 1 protocol ip 16 list 102 //ACL102的数据流量16号队列
R2(config)#queue-list 1 default 3 //其它数据默认3号队列。
R2(config)#interface s1/0
R2(config-if)#custom-queue-list 1 //接口下调用CQ。
R2#debug custom-queue //显示CQ的日志。
```

如何解决 → 自动进行分类，人无法干预，默认基于五元组

如何排队 → 根据五元组自行排队，自行排队。

CDT：早期丢弃门限，其会优先地丢弃掉队列当中最具有侵略性的数据流量，当软件队列中包的数量达到早期丢弃门限，则目前软件队列中队列最长的五元组数据流量禁止其数据流量再进入队列排队

HQ0：队列中可以容纳数据包的上限，软件队列当中可以存放数据包的数量上限，当队列中的数据包达到上限的时候，如果有非侵略性的数据流量需要进入队列排队，则可以丢弃目前队列中最具侵略性的数据流量，给非侵略性的数据流量腾位置。

如何调度 → 根据数据包的FT（FinishTime）从小到大进行调度。

FT（FinishTime）：V（t） + 包长或 PreFT + 包长

每一个队列的第一个数据包FT = V（t） + 包长

每一个队列的其它数据包FT = PreFT + 包长

V（t）：数据包所在队列的虚拟时间

PreFT：前一个数据包的FT（FinishTime）

包长 = 数据包的真实长度 + 优先级

优先级越大，包长越小，包长越小计算出的FT越小，FT越小越优先转发。

```
R2(config-if)#fair-queue
```

> 💡 接口下运行WFQ。

通过WFQ带来的拥塞管理机制，可以做到保障带宽。

哪怕拥塞产生了，可以调整对应优先级的数据流量依然优先转发。

CBWFQ：基于MQC模块儿化的命令行。

```
R3(config)#ip access-list extended R1-R6
R3(config-ext-nacl)#permit ip host 1.1.1.1 host 6.6.6.6
R3(config-ext-nacl)#exit
R3(config)#class-map match-all CMAP
R3(config-cmap)#match access-group name R1-R6 //利用CMAP调用ACL匹配上需要做CBWFQ的数据
R3(config-cmap)#exit
R3(config)#policy-map PMAP
R3(config-pmap)#class CMAP
R3(config-pmap-c)#bandwidth 2000 //哪怕拥塞产生也可以保障2Mbps带宽
R3(config-pmap-c)#exit
R3(config-pmap)#class class-default
R3(config-pmap-c)#fair-queue //默认接口都是FIFO,需要修改改为WFQ。
R3(config)#interface f0/0
R3(config-if)#service-policy output PMAP //调用PMAP。
R3#show policy-map interface f0/0 //检查接口的QoS配置。
```

CBLLQ：低延时保障带宽

```
R4(config)#ip access-list extended R1-R5
R4(config-ext-nacl)#permit ip host 1.1.1.1 host 5.5.5.5
R4(config-ext-nacl)#exit
R4(config)#class-map match-all CMAP
R4(config-cmap)#match access-group name R1-R5 //利用CMAP调用ACL分类数据
R4(config-cmap)#exit
R4(config)#policy-map PMAP
R4(config-pmap)#class CMAP
R4(config-pmap-c)#priority 2000 //LLQ,保障2Mbps并且低延时转发
R4(config-pmap-c)#exit
R4(config-pmap)#class class-default
R4(config-pmap-c)#fair-queue //接口默认FIFO,修改为WFQ。
R4(config-pmap-c)#exit
R4(config-pmap)#exit
R4(config)#interface g0/0
R4(config-if)#service-policy output PMAP //接口调用PMAP
```

注意：不要任何流量都CBLLQ，CBLLQ常见于语音和视频流量即可。

令牌桶理论：速率不是一个恒定的标准量，是一个突发量...限速限定的不是恒定的速率，而是限制在周期时间当中可以发送数据的总量。

CIR：承诺的信息速率（在周期时间当中显示数据流量的平均速率）每秒向令牌桶当中注入多少令牌

**TC：周期时间**

BC：承诺的突发量 = CIR × TC（在一个周期时间当中承诺给设备允许发送的数据量）令牌桶的容量。

**BE：超出的突发量**

PIR：超出的信息速率，向BE令牌桶当中注入令牌速率。（CB Policing）

拿到令牌的数据可以得到转发，拿不到令牌的数据就不允许转发。

**Policing（管控）**

拿到令牌的数据得到转发，拿不到令牌的数据将被丢弃

针对于网络中不重要的数据，可以适当允许丢包的数据可以选择使用Policing。

例如TCP的不重要的消息可以选择Policing限速，TCP丢了一两个包可以通过TCP重传线上。

**延时低**

入方向和出方向都可以使用policing限速

CAR

```
R3(config)#access-list 100 permit ip host 1.1.1.1 host 6.6.6.6
R3(config-if)#rate-limit input access-group 100 <CIR bps> <BC Byte> <BC+BE> conform-action
```

continue scan other rate limits

drop drop packet

set-dscp-continue set dscp, scan other rate limits

set-dscp-transmit set dscp and send it

set-mpls-exp-imposition-continue set exp during imposition, scan other rate limits

set-mpls-exp-imposition-transmit set exp during imposition and send it

set-prec-continue rewrite packet precedence, scan other rate limits

set-prec-transmit rewrite packet precedence and send it

set-qos-continue set qos-group, scan other rate limits

set-qos-transmit set qos-group and send it

transmit transmit packet

```
R3(config-if)#rate-limit input access-group 100 500000 31200 62400 conform-action transmit exceed-action drop
```

> 💡 限速500kbps,拿到令牌转发

```
R3(config)#access-list 100 permit ip host 1.1.1.1 host 6.6.6.6
R3(config)#access-list 101 permit ip host 1.1.1.1 any
R3(config-if)#rate-limit input access-group 100 500000 31200 62400 conform-action transmit exceed-action continue
```

> 💡 拿到令牌发,拿不到向下匹配

```
R3(config-if)#rate-limit input access-group 101 48000 31200 62400 conform-action transmit exceed-action drop
```

CB Policing - 利用MQC模块儿化的命令行使用policing

引入了双桶双速率

**例如用户发送的数据**

如果 Data < BC conform-action 从BC桶拿到令牌的数据流量行为动作

如果 BC < data < BC+BE exceed-action 从BE桶拿令牌的数据流量行为动作

如果 Data > BC+BE violation-action 拿不到令牌的数据流量行为动作

1 在接入设备上可以针对于流量分类并打标记

2. R2(config)#access-list 100 permit ip host 1.1.1.1 host 6.6.6.6
3. R2(config)#class-map CMAP
4. R2(config-cmap)#match access-group 100
5. R2(config-cmap)#exit
6. R2(config)#policy-map PMAP
7. R2(config-pmap)#class CMAP
8. R2(config-pmap-c)#
9. R2(config-pmap-c)#set dscp AF12
10. R2(config-pmap-c)#exit
11. R2(config-pmap)#exit
12. R2(config)#interface f0/0
13. R2(config-if)#service-policy input PMAP
14. R2(config-if)#exit

在需要限速的地方可以直接针对于打上标记的数据流量执行限速措施

```
R4(config)#class-map match-all CMP
R4(config-cmap)#match dscp AF12
R4(config-cmap)#exit
R4(config)#policy-map PMAP
R4(config-pmap)#class CMP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
R4(config-pmap-c)#policy-map PMAP
```

GTS

```
R3(config)#interface f0/0
R3(config-if)#traffic-shape ?
```

group configure token bucket: group <access-list> CIR (bps) [Bc (bits) [Be(bits)]] //针对于某一个类数据流量进行限速

rate configure token bucket: CIR (bps) [Bc (bits) [Be (bits)]] //直接针对于端口的所有数据流量进行限速

```
R3(config)#access-list 100 permit ip host 1.1.1.1 host 6.6.6.6
R3(config)#interface f0/0
R3(config-if)#traffic-shape group 100 5000000 25000000 25000000
```

**限流量限速5Mbps.**

CB Shaping - 利用MQ模块儿化的命令行使用Shaping

在接入设备上可以针对于流量分类并打标记

```
R2(config)#access-list 100 permit ip host 1.1.1.1 host 6.6.6.6
R2(config)#class-map CMAP
R2(config-cmap)#match access-group 100
R2(config-cmap)#exit
R2(config)#policy-map PMAP
R2(config-pmap)#class CMAP
R2(config-pmap-c)#
R2(config-pmap-c)#
R2(config-pmap-c)#
R2(config-pmap-c)#
R2(config-pmap-c)#
R2(config-if)#traffic-policy input PMAP
R2(config-if)#exit
R2(config-if)#exit
R2(config-if)#exit
```

在需要限速的地方可以直接针对于打上标记的数据流量执行限速措施

```
R3(config)#class-map CMAP
R3(config-cmap)#match dscp AF12
R3(config-cmap)#exit
R3(config)#policy-map PMAP
R3(config-pmap)#class CMAP
R3(config-pmap-c)#shape average 5000000
```

5Mbps,可以不用写BC和BE.

```
R3(config-pmap)#interface f0/0
R3(config-if)#service-policy output PMAP
R3#show policy-map int f0/0
```

**流量整形限速**

**RED（早期随机丢弃）**

Cisco路由器默认情况下当出接口的软件队列数量 ≥ 20 时，将会有 10% 的概率随机丢弃到软件队列当中的某一个数据包，避免软件队列排满之后造成后续的数据包 100% 丢包。

当软件队列当中数据包的个数到达一定限额时，软件队列中优先级较低的数据包将会被随机丢弃，并且软件队列中数据包个数越多，越高优先级的数据包容易被丢弃。

```
R2(config)#interface s1/0
R2(config-if)#random-detect //开关
R2(config-if)#random-detect prec-based //启用基于IP precedence的WRED
R2#show queueing random-detect
```

cclass Random drop Tail drop Minimum Maximum Mark

pkts/bytes pkts/bytes thresh thresh prob

0 0/0 0/0 20 40 1/10

1 0/0 0/0 22 44 1/10

2 0/0 0/0 24 48 1/10

3 0/0 0/0 26 52 1/10

4 0/0 0/0 28 56 1/10

5 0/0 0/0 31 62 1/10

6 0/0 0/0 33 66 1/10

7 0/0 0/0 35 70 1/10

rsvp 0/0 0/0 37 74 1/10

```
R2(config)#interface s1/0
R2(config-if)#random-detect //开关
R2(config-if)#random-detect DSCP-based //启用基于IP DSCP的WRED
R2#show queueing random-detect
```

dscp Random drop Tail drop Minimum Maximum Mark

pkts/bytes pkts/bytes thresh thresh prob

af11 0/0 0/0 33 40 1/10

af12 0/0 0/0 28 40 1/10

af13 0/0 0/0 24 40 1/10

af21 0/0 0/0 33 40 1/10

af22 0/0 0/0 28 40 1/10

af23 0/0 0/0 24 40 1/10

af31 0/0 0/0 33 40 1/10

af32 0/0 0/0 28 40 1/10

af33 0/0 0/0 24 40 1/10

af41 0/0 0/0 33 40 1/10

af42 0/0 0/0 28 40 1/10

af43 0/0 0/0 24 40 1/10

cs1 0/0 0/0 22 40 1/10

cs2 0/0 0/0 24 40 1/10

cs3 0/0 0/0 26 40 1/10

cs4 0/0 0/0 28 40 1/10

cs5 0/0 0/0 31 40 1/10

cs6 0/0 0/0 33 40 1/10

cs7 0/0 0/0 35 40 1/10

ef 0/0 0/0 37 40 1/10

rsvp 0/0 0/0 37 40 1/10

default 0/0 0/0 20 40 1/10

在接入设备上可以针对于流量分类并打标记

```
R2(config)#access-list 100 permit ip host 1.1.1.1 host 6.6.6.6
R2(config)#class-map CMAP
R2(config-cmap)#match access-group 100
R2(config-cmap)#exit
R2(config)#policy-map PMAP
R2(config-pmap)#class CMAP
R2(config-pmap-c)#
R2(config-pmap-c)#set dscp AF12
R2(config-pmap-c)#exit
R2(config-pmap)#exit
R2(config)#interface f0/0
R2(config-if)#service-policy input PMAP
R2(config-if)#exit
```

在需要限速的地方可以直接针对于打上标记的数据流量执行限速，保障带宽，拥塞避免

```
R4(config)#class-map match-all CMAP
R4(config-cmap)#match dscp AF12
R4(config-cmap)#exit
R4(config)#class-map match-all CMAP2
R4(config-cmap)#match dscp EF
R4(config-cmap)#exit
R4(config)#policy-map PMAP
R4(config-pmap)#class CMAP
R4(config-pmap-c)#police 100000000
```

26. R4(config-pmap-c-police)#conform-action transmit
27. R4(config-pmap-c-police)#exceed-action transmit
28. R4(config-pmap-c-police)#violate-action drop
29. R4(config-pmap-c-police)#exit
30. R4(config-pmap-c)#bandwidth percent 10
31. R4(config-pmap-c)#exit
32. R4(config-pmap)#class CMAP2
33. R4(config-pmap-c)#priority percent 20
34. R4(config-pmap-c)#exit
35. R4(config-pmap)#class class-default
36. R4(config-pmap-c)#fair-queue
37. R4(config-pmap-c)#random-detect dscp-based
38. R4(config-pmap)#exit
39. R4(config)#interface g0/0
40. R4(config-if)#service-policy output PMAP