# CCNP 备考笔记（Study Guide）—— 从零开始的网络工程知识体系

> 基于444道CCNP真题解析提炼 | 面向初学者 | 精炼背诵版 | 中英对照

---

## 目录（Table of Contents）

1. [速记卡片：最高频考点一览（Quick Reference Cards）](#一速记卡片)
2. [SD-Access 软件定义接入（Software-Defined Access）](#二sd-access)
3. [SD-WAN 软件定义广域网（Software-Defined WAN）](#三sd-wan)
4. [路由协议（Routing Protocols）：OSPF vs EIGRP](#四路由协议)
5. [第一跳冗余协议（FHRP, First Hop Redundancy Protocol）：HSRP / VRRP / GLBP](#五第一跳冗余)
6. [组播（Multicast）：PIM & IGMP](#六组播)
7. [VXLAN（Virtual eXtensible LAN）& LISP（Locator/ID Separation Protocol）](#七vxlan--lisp)
8. [虚拟化（Virtualization）：Hypervisor & VM](#八虚拟化)
9. [NGFW 下一代防火墙（Next-Generation Firewall）& 威胁防御（Threat Defense）](#九安全)
10. [TrustSec & MACsec & IPsec](#十trustsec--macsec--ipsec)
11. [AAA 认证（Authentication）授权（Authorization）计费（Accounting）](#十一aaa)
12. [NAT 网络地址转换（Network Address Translation）](#十二nat)
13. [QoS 服务质量（Quality of Service）](#十三qos)
14. [NTP 网络时间协议（Network Time Protocol）](#十四ntp)
15. [自动化工具（Automation Tools）：Ansible / Puppet / Chef / SaltStack](#十五自动化工具)
16. [YANG / NETCONF / RESTCONF / JSON / XML](#十六数据建模与api)
17. [Python 基础考点（Python Essentials）](#十七python)
18. [EEM 嵌入式事件管理器（Embedded Event Manager）](#十八eem)
19. [REST API & HTTP 状态码（Status Codes）](#十九rest-api)
20. [网络设计（Network Design）：三层模型 / Spine-Leaf / 模块化（Modularity）](#二十网络设计)
21. [堆叠与虚拟化（Stacking & Virtualization）：StackWise / VSS / SSO / NSF](#二十一高可用)
22. [无线网络（Wireless）：WLC / CAPWAP / SD-Access Wireless](#二十二无线)
23. [附录（Appendix）：数字速查表](#二十三附录)

---

## 一、速记卡片

> 考前30分钟必背（Must-review 30min before exam）。以下是最容易混淆、最常考的核心对比。

### 1.1 四平面对照（Four Planes Comparison）（SD-Access & SD-WAN）

| 概念（Concept） | SD-Access | SD-WAN |
|------|-----------|--------|
| **控制平面（Control Plane）** | LISP | vSmart（OMP协议） |
| **数据平面（Data Plane）** | VXLAN | IPsec（WAN Edge/cEdge） |
| **策略平面（Policy Plane）** | CTS / SGT | vSmart分发策略（Policy Distribution） |
| **管理平面（Management Plane）** | DNAC | vManage |
| **编排平面（Orchestration Plane）** | - | vBond |

### 1.2 DNA Center 南北向API（Northbound / Southbound API）

| API方向（Direction） | 角色（Role） | 协议（Protocol） | 数据格式（Data Format） | 关键词（Keywords） |
|---------|------|------|---------|--------|
| **北向（Northbound）** | 控制器（Controller）→应用（Application） | RESTCONF / RESTful | JSON | Intent API, 面向结果（Outcome-Oriented） |
| **南向（Southbound）** | 控制器（Controller）→设备（Device） | NETCONF | XML | 多厂商SDK（Multivendor SDK）, 设备包（Device Package） |

### 1.3 路由协议速查（Routing Protocols Quick Reference）

| 特性（Feature） | OSPF | EIGRP |
|------|------|-------|
| **类型（Type）** | 链路状态（Link State） | 高级距离向量（Advanced Distance Vector） |
| **算法（Algorithm）** | Dijkstra (SPF, Shortest Path First) | DUAL（弥散更新算法，Diffusing Update Algorithm） |
| **IP协议号（IP Protocol Number）** | **89** | **88** |
| **组播地址（Multicast Address）** | 224.0.0.5 / 224.0.0.6 | 224.0.0.10 |
| **管理距离-内部（AD, Administrative Distance - Internal）** | 110 | 90 |
| **管理距离-外部（AD - External）** | 110 | 170 |
| **默认度量（Default Metric）** | Cost = 参考带宽（Reference Bandwidth）/接口带宽（Interface Bandwidth） | 带宽（Bandwidth）+ 延迟（Delay）(K1=1, K3=1) |
| **认证（Authentication）** | 支持MD5 | 支持MD5 |
| **非等价负载均衡（Unequal-Cost Load Balancing）** | 不支持 | 支持 (variance) |
| **路由标签（Route Tag）** | 支持 | 不支持 |
| **自动汇总（Auto-Summarization）** | 不支持 | 支持 (可关闭，no auto-summary) |
| **虚拟链路（Virtual Link）** | 支持 | - |

### 1.4 第一跳冗余协议（FHRP Comparison）

| 特性（Feature） | HSRP | VRRP | GLBP |
|------|------|------|------|
| **标准（Standard）** | 思科专有（Cisco Proprietary） | IEEE开放标准（Open Standard, RFC 5798） | 思科专有（Cisco Proprietary） |
| **虚拟MAC格式（Virtual MAC Format）** | 0000.0c07.acXX | 0000.5e00.01XX | 0000.0c07.acXX |
| **负载均衡（Load Balancing）** | 不支持(单Active) | 不支持(单Master) | **支持(多AVF, Active Virtual Forwarder)** |
| **IPv6支持（IPv6 Support）** | HSRPv2 | VRRPv3 | 不支持 |
| **默认优先级（Default Priority）** | 100 | 100 | - |
| **抢占（Preemption）** | 需配置preempt | 默认抢占（Default Preempt） | - |
| **HSRPv1组号范围（Group Range）** | 0-255 | - | - |
| **HSRPv2组号范围** | 0-4095 | - | - |

### 1.5 PIM模式速查（PIM Mode Comparison）

| 特性（Feature） | PIM Dense Mode（密集模式） | PIM Sparse Mode（稀疏模式） |
|------|---------------|-----------------|
| **模型（Model）** | Push (推送-泛洪, Flood) | Pull (拉取-按需, On-Demand) |
| **机制（Mechanism）** | Flood and Prune（泛洪与剪枝） | 显式Join（Explicit Join） |
| **RP, Rendezvous Point（汇聚点）** | **不需要** | **必须（Required）** |
| **适用场景（Use Case）** | 小规模/组成员密集（Small/Dense） | 大规模/组成员稀疏（Large/Sparse） |

### 1.6 HTTP状态码速查（HTTP Status Codes）

| 状态码（Status Code） | 含义（Meaning） |
|--------|------|
| **200 OK** | 请求成功（Success） |
| **201 Created** | 资源已创建（Resource Created） |
| **204 No Content** | 成功但无响应体（Success, No Response Body, DELETE常见） |
| **400 Bad Request** | 请求格式错误（Malformed Request, 如JSON格式错误） |
| **401 Unauthorized** | 未认证/凭据错误（Authentication Failed） |
| **403 Forbidden** | 已认证但无权限（Authenticated but No Permission） |
| **404 Not Found** | 资源不存在（Resource Not Found） |
| **500 Internal Server Error** | 服务器内部错误（Server Error） |
| **504 Gateway Timeout** | 网关超时（Gateway Timeout） |

### 1.7 Hypervisor速查（Hypervisor Types）

| 类型（Type） | 别称（Alias） | 安装位置（Installation） | 例子（Examples） |
|------|------|---------|------|
| **Type 1** | 裸机（Bare Metal） | 直接安装在硬件上（Directly on Hardware） | ESXi, Hyper-V, KVM |
| **Type 2** | 托管（Hosted） | 安装在OS上作为应用（On OS as Application） | VMware Workstation, VirtualBox |

### 1.8 自动化工具速查（Automation Tools Comparison）

| 工具（Tool） | Agent | 语言（Language） | 配置语法（Config Syntax） | 方法（Approach） | 架构（Architecture） |
|------|-------|------|---------|------|------|
| **Ansible** | 无(SSH, Agentless) | Python | YAML | 过程式（Procedural） | 推送（Push） |
| **Puppet** | 有（Agent-Based） | Ruby DSL | 专有DSL（Proprietary DSL） | 声明式（Declarative） | 拉取（Pull） |
| **Chef** | 有（Agent-Based） | Ruby | Ruby | 过程式（Procedural） | 拉取（Pull） |
| **SaltStack** | 有(Minion) | Python | YAML | 声明式（Declarative） | 推送+拉取（Push+Pull） |

### 1.9 SD-Access节点角色速查（Node Roles）

| 节点（Node） | 功能（Function） | 一句话（One-Liner） |
|------|------|--------|
| **Control Plane Node** | 维护EID-RLOC映射数据库（Mapping Database） | "谁在哪"的数据库（Who & Where DB） |
| **Edge Node** | 连接终端（Endpoints），提供Anycast Gateway | 终端的"入口"（Entry Point） |
| **Border Node** | 连接外部网络/其他fabric（External Networks） | fabric的"城门"（Gateway） |
| **Intermediate Node** | 纯underlay转发（Underlay Forwarding Only） | 只转发，不封装（Forward Only） |

### 1.10 SD-WAN四大组件速查（Four Core Components）

| 组件（Component） | 平面（Plane） | 一句话功能（One-Liner） |
|------|------|-----------|
| **vManage** | 管理平面（Management Plane） | GUI/API集中管理（Centralized Management） |
| **vSmart** | 控制平面（Control Plane） | 路由（Routing）+策略（Policy）+密钥分发（Key Distribution） |
| **vBond** | 编排平面（Orchestration Plane） | 设备首次入网认证（Onboarding）+NAT穿越（NAT Traversal, STUN） |
| **WAN Edge (cEdge/vEdge)** | 数据平面（Data Plane） | IPsec隧道（Tunnel）+实际转发（Forwarding） |

### 1.11 VRRP/HSRP选举规则（Election Rules）

```
1. 优先级（Priority）高的胜出（默认100）
2. 优先级相同时，接口IP地址（Interface IP Address）大的胜出
   → HSRP和VRRP都适用此规则
```

### 1.12 YANG四种节点类型（Four Node Types）

| 节点（Node） | 描述（Description） |
|------|------|
| **leaf** | 单个简单数据（整数integer、字符串string） |
| **leaf-list** | 同类型数据数组（Array of Same Type） |
| **container** | 组织相关节点的容器（无数据，Organizes Nodes, No Data） |
| **list** | 由key标识的多条记录（Key-Identified Records） |

### 1.13 加密技术应用层次（Encryption Technologies by OSI Layer）

| 技术（Technology） | OSI层（Layer） | 应用场景（Use Case） |
|------|-------|---------|
| **MACsec** | 二层（L2, Layer 2） | 交换机之间链路加密（逐跳, Hop-by-Hop） |
| **IPsec** | 三层（L3, Layer 3） | 站点间VPN隧道（端到端, End-to-End） |
| **TLS/SSL** | 四层（L4, Layer 4） | REST API通信(HTTPS) |
| **DTLS** | 四层（L4） | SD-WAN控制平面(UDP加密, UDP-Based Encryption) |

---

## 二、SD-Access

### 2.1 什么是SD-Access（Software-Defined Access）？

软件定义接入（SD-Access）是思科基于意图的网络（IBN, Intent-Based Networking）在园区网（Campus Network）的实现。它将传统园区网络改造为可编程的fabric架构（Programmable Fabric）。

### 2.2 核心理念：三平面分离（Three-Plane Separation）

```
┌──────────────────────────────────────┐
│  控制平面 Control Plane (LISP)        │
│  → 端点位置映射（EID-RLOC Mapping）、路由决策│
├──────────────────────────────────────┤
│  数据平面 Data Plane (VXLAN)           │
│  → 实际流量封装和转发（Encapsulation & Forwarding）│
├──────────────────────────────────────┤
│  策略平面 Policy Plane (CTS / SGT)     │
│  → 安全分段（Segmentation）、访问控制（Access Control）│
└──────────────────────────────────────┘
```

### 2.3 必背知识点（Must-Know Facts）

- **控制平面（Control Plane）** = LISP（管理EID↔RLOC映射）
- **数据平面（Data Plane）** = VXLAN（MAC-in-UDP封装，Encapsulation）
- **策略平面（Policy Plane）** = Cisco TrustSec（SGT安全组标签，Security Group Tag）
- **管理平面（Management Plane）** = Cisco Catalyst Center（即DNAC, DNA Center）
- **Underlay（底层网络）** = 纯三层IP网络（Pure L3 Network），推荐MTU 9100（Jumbo Frame支持VXLAN封装）
- **Overlay（叠加网络）** = 虚拟网络分段（Virtual Network Segmentation），与物理网络解耦（Decoupled from Physical Network）
- **Anycast Gateway（任播网关）**：所有Edge Node使用相同的网关IP/MAC，终端就近转发（Local Forwarding）
- **扩展节点（Extended Node）**：传统二层交换机通过802.1Q trunk连接到Edge Node

### 2.4 四个核心组件（Four Core Components）

| 组件（Component） | 功能（Function） |
|------|------|
| **Cisco Catalyst Center (DNAC)** | 自动化设计（Design）、部署（Deployment）、策略（Policy）、保障（Assurance） |
| **Identity Services Engine (ISE)** | 身份认证（Identity Authentication）+ 动态SGT分配（Dynamic SGT Assignment） |
| **Control Plane Node** | LISP映射服务器/解析器（Map Server / Map Resolver） |
| **Edge/Border Node** | 终端接入（Endpoint Access）/ fabric边界（Fabric Boundary） |

### 2.5 DNAC四大工作流（Four Workflows）

| 工作流（Workflow） | 功能（Function） |
|--------|------|
| **Design** | 网络设计（Network Design，绿地部署 Greenfield Deployment） |
| **Provision** | 设备配置（Configuration）和入网（Onboarding） |
| **Policy** | 基于组的访问控制策略（Group-Based Access Control） |
| **Assurance** | 监控（Monitoring）、数据关联分析（Data Correlation & Analysis）、排错（Troubleshooting） |

### 2.6 DNAC发现设备的方法（Device Discovery Methods）

三种方法：**CDP**（Cisco Discovery Protocol，思科发现协议）、**LLDP**（Link Layer Discovery Protocol，链路层发现协议）、**指定IP地址范围扫描**（IP Range Scan）

- CDP用于思科设备（Cisco Devices）
- LLDP用于多厂商设备（Multivendor Devices，开放标准IEEE 802.1AB）

---

## 三、SD-WAN

### 3.1 什么是SD-WAN（Software-Defined WAN）？

软件定义广域网（SD-WAN），将控制集中化（Centralized Control）、数据平面分布化（Distributed Data Plane），用overlay隧道（Tunnel）替代传统专线（Traditional Leased Line）。

### 3.2 四大组件 + 四大平面（Four Components & Four Planes）

| 组件（Component） | 平面（Plane） | 核心职责（Core Responsibility） |
|------|------|---------|
| **vManage** | 管理平面（Management Plane） | GUI管理、配置模板（Configuration Template）、监控（Monitoring）、软件升级（Software Upgrade） |
| **vSmart** | 控制平面（Control Plane） | OMP路由分发（Route Distribution）、策略（Policy）、IPsec密钥分发（Key Distribution） |
| **vBond** | 编排平面（Orchestration Plane） | 设备首次onboarding、认证（Authentication）、NAT穿越（NAT Traversal, STUN） |
| **cEdge/vEdge** | 数据平面（Data Plane） | IPsec隧道建立（Tunnel Establishment）、BFD链路检测（Link Detection）、实际转发（Forwarding） |

### 3.3 必背知识点（Must-Know Facts）

- **控制平面加密（Control Plane Encryption）**：DTLS/TLS
- **数据平面加密（Data Plane Encryption）**：IPsec
- **链路质量检测（Link Quality Detection）**：BFD（Bidirectional Forwarding Detection，双向转发检测，亚秒级丢包/延迟/抖动检测）
- **路由协议（Routing Protocol）**：OMP（Overlay Management Protocol，覆盖管理协议，vSmart↔WAN Edge）
- **vSmart → WAN Edge策略推送**：NETCONF协议
- **SD-WAN vs 传统WAN优势**：集中策略（Centralized Policy）、应用感知（Application-Aware）、零接触部署（ZTP, Zero-Touch Provisioning）、加密隧道（Encrypted Tunnels）
- **传统WAN优势**：更低数据平面开销（Lower Data Plane Overhead，无额外封装）
- **多云接入（Multi-Cloud Access）**：在云提供商（Cloud Provider）内部署虚拟WAN Edge将云VPC/VNet纳入fabric
- **BFD用于**：与动态路由协议（Dynamic Routing Protocol）配合提供亚秒级收敛（Sub-Second Convergence）

### 3.4 OMP的两大功能（Two Core Functions of OMP）

1. 通告网络前缀及其属性（Advertise Network Prefixes & Attributes，路由/TLOC/服务）
2. 分发加密密钥（Distribute Encryption Keys，IPsec keys）

---

## 四、路由协议

### 4.1 OSPF核心知识（OSPF Essentials）

**基本特征（Basic Characteristics）：**
- 类型（Type）：链路状态（Link State）
- 算法（Algorithm）：Dijkstra SPF（Shortest Path First，最短路径优先）
- IP协议号（IP Protocol Number）：**89**
- 组播地址（Multicast Address）：224.0.0.5 (All OSPF Routers) / 224.0.0.6 (All DRs, Designated Routers)
- 管理距离（AD, Administrative Distance）：110
- 度量（Metric） = 参考带宽（Reference Bandwidth）÷ 接口带宽（Interface Bandwidth）= Cost

**区域规则（Area Rules）：**
- 所有非骨干区域（Non-Backbone Area）必须直接连接到Area 0（骨干区域，Backbone Area）
- **虚拟链路（Virtual Link）**：通过非骨干区域将另一个非骨干区域连接到Area 0

**邻居建立条件（Neighborship Requirements）：**
- 接口必须在同一IP子网（Same IP Subnet，子网掩码Subnet Mask必须一致）
- Hello/Dead计时器（Timers）必须匹配
- 认证（Authentication）必须匹配
- Area ID必须相同
- MTU必须匹配

**认证（Authentication）：** 支持MD5

**路由标签（Route Tag）：** 支持

**路由汇总（Route Summarization）：** 需手动配置（`area X range`用于区域间Inter-Area，`summary-address`用于外部External）

### 4.2 EIGRP核心知识（EIGRP Essentials）

**基本特征（Basic Characteristics）：**
- 类型（Type）：高级距离向量（Advanced Distance Vector）
- 算法（Algorithm）：**DUAL**（Diffusing Update Algorithm，弥散更新算法）
- IP协议号（IP Protocol Number）：**88**
- 组播地址（Multicast Address）：224.0.0.10
- 管理距离（AD）：内部（Internal）=90，外部（External, D EX）=170
- 默认度量（Default Metric）= 带宽（Bandwidth, 最慢链路 Slowest Link）+ 延迟（Delay, 累积 Cumulative）

**K值（K-Values，默认Default）：** K1=1, K2=0, K3=1, K4=0, K5=0
- K1=带宽（Bandwidth），K3=延迟（Delay）→ 只有这两个默认启用

**特有优势（Unique Advantages）：**
- **不等价负载均衡（Unequal-Cost Load Balancing）**（variance命令）
- 可行后继（Feasible Successor, FS）提供快速收敛（Fast Convergence）
- **自动汇总（Auto-Summarization）**（默认开启，可用no auto-summary关闭）
- Query包（查询包）用于查询丢失路由

**认证（Authentication）：** 每个接口独立配置（Per-Interface），支持MD5。**Key ID必须匹配（Must Match）**。

**路由标签（Route Tag）：** 不支持

### 4.3 OSPF vs EIGRP 相似点（Similarities）

| 相似点（Similarity） | 说明（Description） |
|--------|------|
| 都支持MD5认证（MD5 Authentication） | 路由更新认证（Update Authentication） |
| 都支持VLSM/CIDR | 无类别路由协议（Classless Routing Protocol） |
| 都使用组播（Multicast） | OSPF=224.0.0.5/6, EIGRP=224.0.0.10 |

### 4.4 OSPF vs EIGRP 不同点（Differences）

| 不同点（Difference） | OSPF | EIGRP |
|--------|------|-------|
| 算法（Algorithm） | Dijkstra SPF | DUAL |
| 汇总（Summarization） | 手动配置（Manual） | 自动汇总（Auto, 可关） |
| 路由标签（Route Tag） | 支持 | 不支持 |
| 非等价负载均衡（Unequal-Cost LB） | 不支持 | 支持 |
| 虚拟链路（Virtual Link） | 支持 | 无 |
| 外部AD（External AD） | 110 | 170 |

### 4.5 PBR（Policy-Based Routing，基于策略的路由）

- 覆盖（Override）正常路由表（Routing Table）的转发决策
- 应用于接口**入站方向（Ingress/Inbound Direction）**
- 通过**route-map（路由映射）**配置（含match条件 + set next-hop）
- 功能（Capabilities）：基于源IP（Source IP）/协议（Protocol）/端口（Port）选路，协议敏感路由（Protocol-Sensitive Routing）
- deny在route-map的PBR中 = 返回正常路由表转发（Return to Normal Routing）

---

## 五、第一跳冗余

### 5.1 三种协议对比（Three-Protocol Comparison）

| 特性（Feature） | HSRP | VRRP | GLBP |
|------|------|------|------|
| 标准（Standard） | 思科专有（Cisco Proprietary） | **IEEE(RFC 5798)** | 思科专有（Cisco Proprietary） |
| 负载均衡（Load Balancing） | 不支持 | 不支持 | **支持(多AVF, Active Virtual Forwarder)** |
| IPv6 | HSRPv2支持 | VRRPv3支持 | 不支持 |
| 默认优先级（Default Priority） | 100 | 100 | - |
| 组播地址（Multicast Address） | 224.0.0.2(v1) | 224.0.0.18 | - |
| HSRPv1虚拟MAC | 0000.0c07.acXX | - | - |
| VRRP虚拟MAC | - | 0000.5e00.01XX | - |

### 5.2 选举规则（Election Rules）

```
优先级高的胜（Higher Priority Wins，默认100）
  → 优先级相同（Priority Tie）则IP地址大的胜（Higher IP Address Wins）
```

### 5.3 HSRP关键配置（HSRP Key Configurations）

- `standby 1 ip <VIP>`：设置虚拟IP（Virtual IP）
- `standby 1 priority <值>`：设置优先级（默认100）
- `standby 1 preempt`：故障恢复后抢占（Preempt After Recovery）
- `standby 1 preempt delay minimum <秒>`：抢占前等待时间（Delay Before Preemption）
- `standby 1 track <对象号> decrement <值>`：降低优先级（Priority Decrement）
- `standby use-bia`：使用接口烧录MAC（Burned-In Address, BIA）作为虚拟MAC
- `standby version 2`：启用HSRPv2（组号0-4095，毫秒级计时器 Millisecond Timers）

### 5.4 VRRP关键点（VRRP Key Points）

- 选举规则同HSRP（优先级→IP地址大→胜）
- VRRPv3支持IPv4和IPv6
- VRRPv2只支持IPv4
- 多厂商环境（Multivendor Environment）必须选VRRP
- `vrrp 1 preempt`：VRRP默认抢占（Preempt by Default）

### 5.5 GLBP关键点（GLBP Key Points）

- 唯一支持**多网关同时转发（Multiple Gateways Simultaneously Forwarding）**的FHRP
- 通过AVF（Active Virtual Forwarder，活动虚拟转发者）机制实现负载均衡（Load Balancing）
- 支持**加权负载均衡（Weighted Load Balancing）**（设备能力不同时使用）
- 最大化上行带宽利用（Maximize Uplink Utilization）

### 5.6 SSO（Stateful Switchover，状态化切换）vs FHRP

- **FHRP**：跨设备网关冗余（Gateway Redundancy Across Devices，设备间）
- **SSO**：单设备内主备引擎冗余（Active/Standby Engine Redundancy Within a Device，设备内）
- 两者互补（Complementary）：SSO保护引擎故障（Engine Failure），FHRP保护整机故障（Device Failure）

---

## 六、组播

### 6.1 组播协议角色分工（Multicast Protocol Roles）

| 协议（Protocol） | 运行范围（Scope） | 功能（Function） |
|------|---------|------|
| **IGMP（Internet Group Management Protocol）** | 主机（Host）↔ 路由器（Router） | 主机告诉路由器"我要这个组播组（Multicast Group）" |
| **PIM（Protocol Independent Multicast）** | 路由器 ↔ 路由器 | 路由器之间构建组播分发树（Distribution Tree） |

### 6.2 PIM密集模式 vs 稀疏模式（Dense Mode vs Sparse Mode）

| 特性（Feature） | Dense Mode（密集模式） | Sparse Mode（稀疏模式） |
|------|-----------|-------------|
| 分发模型（Distribution Model） | Push (Flood and Prune) | Pull (显式Join, Explicit Join) |
| 分发树（Distribution Tree） | 源树（Source Tree, (S,G)） | 共享树（Shared Tree, (*,G), 以RP为根） |
| RP（Rendezvous Point） | **不需要** | **必须（Required）** |
| 剪枝（Prune） | 主动发送Prune | 不泛洪所以不需要剪枝 |
| 适用（Use Case） | 小型/组成员密集（Small/Dense） | 大型/组成员稀疏（Large/Sparse） |

### 6.3 RP（Rendezvous Point，汇聚点）

- 仅在PIM-SM中使用
- 共享分发树（Shared Distribution Tree）的根节点（Root）
- 主要用于**启动新会话（Initiate New Sessions）**时（源注册Source Registration、接收者加入Receiver Join）
- **Auto-RP**：自动分发组↔RP映射（Automatically Distribute Group-to-RP Mappings）
- MRoutes（Static Multicast Routes，静态组播路由）：可覆盖RPF检查（RPF Check, Reverse Path Forwarding）

### 6.4 IGMP版本（IGMP Versions）

| 版本（Version） | 特性（Feature） |
|------|------|
| IGMPv2 | 基本成员报告（Membership Report）+ 离开组消息（Leave Group） |
| IGMPv3 | 新增**源特定成员报告（Source-Specific Membership Report）**（SSM支持，Source-Specific Multicast） |

### 6.5 IGMP Querier选举（Querier Election）

- 同一LAN段多路由器时选举查询器（Querier）
- **IP地址最低的（Lowest IP Address）**当选

### 6.6 RPF检查（Reverse Path Forwarding Check）

- 组播流量的反向路径转发检查
- 确保组播数据从正确的接口（Correct Interface）进入
- 不改变单播路由表（Unicast Routing Table）可通过的方法：静态mroutes（Static Multicast Routes）、MBGP（Multicast BGP）

---

## 七、VXLAN & LISP

### 7.1 VXLAN（Virtual eXtensible LAN，虚拟可扩展局域网）

- 全称：Virtual eXtensible LAN
- 作用：**二层overlay在三层网络上（L2 Overlay over L3 Network）**，提供网络虚拟化（Network Virtualization）
- 封装（Encapsulation）：**MAC-in-UDP**（原始帧Original Frame封装在UDP/IP中）
- VNI（VXLAN Network Identifier，VXLAN网络标识符）：24位标识符，最大**1600万个**虚拟网段（Virtual Segments）
- 多租户解决方案（Multi-Tenant Solution，超越VLAN的4096限制）
- SD-Access数据平面（Data Plane）= VXLAN
- 推荐MTU：**9100**（Jumbo Frame，巨型帧）

### 7.2 LISP（Locator/ID Separation Protocol，位置/身份分离协议）

- 全称：Locator/ID Separation Protocol
- 作用：位置（Location）与身份（Identity）分离
- **EID（Endpoint Identifier，端点标识符）**：标识"谁"（Who）
- **RLOC（Routing Locator，路由定位符）**：标识"在哪"（Where）
- 设备移动时 → **RLOC更新（Updated）**，EID不变

### 7.3 LISP组件功能（LISP Component Functions）

| 组件（Component） | 功能（Function） |
|------|------|
| **ITR（Ingress Tunnel Router）** | 入口隧道路由器，封装LISP包（Encapsulate） |
| **ETR（Egress Tunnel Router）** | 出口隧道路由器，解封装（Decapsulate），向MS注册EID前缀（Register EID Prefixes） |
| **Map Server (MS)** | 存储EID↔RLOC映射数据库（Mapping Database） |
| **Map Resolver (MR)** | 接收ITR查询（Query），转发给MS（Forward to MS） |
| **PITR（Proxy ITR）** | 代理ITR，将非LISP站点流量引入LISP fabric |

### 7.4 LISP vs VXLAN 区别（Difference）

| 特性（Feature） | LISP | VXLAN |
|------|------|-------|
| 功能（Function） | 控制平面（Control Plane）：端点↔位置映射 | 数据平面（Data Plane）：二层帧封装传输 |
| 在SD-Access的角色 | 控制平面 | 数据平面 |
| 封装（Encapsulation） | 不封装数据 | MAC-in-UDP |

---

## 八、虚拟化

### 8.1 Type 1 vs Type 2 Hypervisor

| 特性（Feature） | Type 1（裸机/Bare Metal） | Type 2（托管/Hosted） |
|------|--------------------------|----------------------|
| 安装位置（Installation） | 直接安装在硬件上（Directly on Hardware） | 安装在OS上（应用程序，On OS as Application） |
| 自带OS（Built-in OS） | **是（Yes）** | 否（No，依赖宿主机OS Host OS） |
| 例子（Examples） | VMware ESXi, Hyper-V, KVM | VMware Workstation, VirtualBox |
| 性能（Performance） | 高（High） | 较低（Lower） |

### 8.2 虚拟机 vs Hypervisor vs 容器（VM vs Hypervisor vs Container）

| 概念（Concept） | 说明（Description） |
|------|------|
| **VM（Virtual Machine，虚拟机）** | 需要hypervisor + 独立Guest OS（客户操作系统） |
| **Hypervisor** | 管理VM的软件层（Software Layer） |
| **Container（容器）** | 共享宿主机OS内核（Share Host OS Kernel），不需要独立Guest OS |
| **vSwitch（Virtual Switch，虚拟交换机）** | 让同宿主机VM互通（Intra-Host Communication） |

---

## 九、安全

### 9.1 传统防火墙（Traditional Firewall）vs 下一代防火墙（NGFW, Next-Generation Firewall）

| 能力（Capability） | 传统防火墙（Traditional FW） | NGFW |
|------|----------|------|
| 包过滤（Packet Filtering, 基于IP/端口） | ✓ | ✓ |
| 状态检测（Stateful Inspection） | ✓ | ✓ |
| NAT | ✓ | ✓ |
| VPN | ✓ | ✓ |
| **应用识别/控制（Application Visibility & Control, AVC）** | ✗ | **✓** |
| **集成IPS（Integrated Intrusion Prevention System）** | ✗ | **✓** |
| **深度包检测（DPI, Deep Packet Inspection）** | ✗ | **✓** |
| **恶意软件防护（Malware Protection）** | ✗ | **✓** |

### 9.2 NGFW部署模式（Deployment Modes）

| 模式（Mode） | 能阻断流量？（Block Traffic?） | 位置（Position） |
|------|------------|------|
| **Inline（内联模式）** | ✓ 能阻断（Can Block） | 串联在流量路径中（In-Path） |
| **Passive（被动模式）** | ✗ 只监控（Monitor Only） | 旁路（Out-of-Band） |
| **Tap（旁路模式）** | ✗ 只监控（Monitor Only） | 旁路（SPAN/Mirror） |

### 9.3 NGFW高级部署（Advanced Deployment）

- **集群（Clustering）**：横向扩展处理能力（Scale Out），可扩展性（Scalability）
- **多上下文模式（Multi-Context Mode）**：一台物理防火墙虚拟化为多台逻辑防火墙（Virtual Firewalls），为多个部门提供独立安全服务
- **数据中心东西向流量保护（East-West Traffic Protection）**：保护DC内服务器间通信（Server-to-Server Communication）

### 9.4 Cisco威胁防御体系（Cisco Cyber Threat Defense）

| 组件（Component） | 功能（Function） | 一句话（One-Liner） |
|------|------|--------|
| **AMP (Advanced Malware Protection)** | 终端恶意软件防护（Endpoint Malware Protection）+ 沙箱分析（Sandbox Analysis） | 恶意软件克星 |
| **FTD (Firepower Threat Defense)** | IPS/IDS + NGFW | 入侵检测与防御（Intrusion Detection & Prevention） |
| **StealthWatch** | NetFlow行为分析（Behavior Analysis）+ 异常检测（Anomaly Detection） | 网络流量"雷达"（Network Radar） |
| **ESA (Email Security Appliance)** | 邮件安全网关（Email Security Gateway） | 邮件威胁防护（Email Threat Protection） |
| **WSA (Web Security Appliance)** | Web安全网关（Web Security Gateway） | 可疑Web活动检测（Suspicious Web Detection） |
| **Umbrella** | DNS层安全（DNS-Layer Security） | DNS防护（DNS Protection） |
| **ISE** | 身份服务引擎（Identity Services Engine）+ pxGrid | 身份认证（Identity Authentication）+ 威胁协调（Threat Coordination） |

### 9.5 安全情报（Security Intelligence）

综合使用（Combines）：流量遥测（Traffic Telemetry）+ 上下文信息（Contextual Information）+ 文件信誉（File Reputation）→ 洞察威胁（Threat Insight）

### 9.6 文件沙箱（File Sandboxing）

- 在隔离环境中运行未知文件，观察行为（Observe Behavior in Isolated Environment）
- 防御零日恶意软件（Zero-Day Malware Protection）

---

## 十、TrustSec & MACsec & IPsec

### 10.1 TrustSec

- 基于**SGT（Security Group Tag，安全组标签）**的访问控制（Access Control）
- SGT是16位标签（16-bit Tag）嵌入数据包中
- 策略随标签走（Policy Follows Tag，不是随IP走）
- 优势（Benefits）：**简化访问管理（Simplified Access Management）** + **一致分段（Consistent Segmentation）**
- 不加密数据（分段≠加密，Segmentation ≠ Encryption）
- SGT分配方式（Assignment Methods）：**802.1X认证**、**Web认证（WebAuth, Web Authentication）**
- 主要组件（Main Components）：ISE + 网络基础设施（Network Infrastructure，交换机/路由器/防火墙）

### 10.2 MACsec (IEEE 802.1AE)

- **二层逐跳加密（L2 Hop-by-Hop Encryption）**
- 保护交换机间Trunk链路（Inter-Switch Trunk Links）
- 线速加密（Line-Rate Encryption，硬件实现 Hardware-Based）
- 通常与802.1X配合进行密钥管理（Key Management）
- 应用（Use Case）：数据中心DWDM/DCI链路（Data Center Interconnect）

### 10.3 IPsec

- **三层端到端加密（L3 End-to-End Encryption）**
- 站点间VPN（Site-to-Site VPN）
- SD-WAN数据平面加密
- 组件：ESP（Encapsulating Security Payload, 加密载荷）+ IKE（Internet Key Exchange, 密钥交换）

### 10.4 加密技术对比（Encryption Technology Comparison）

| 技术（Technology） | 层次（Layer） | 范围（Scope） | 场景（Use Case） |
|------|------|------|------|
| MACsec | L2 | 逐跳（Hop-by-Hop） | 交换机间链路（Inter-Switch Links） |
| IPsec | L3 | 端到端（End-to-End） | 站点间VPN（Site-to-Site VPN） |
| TLS/DTLS | L4+ | 端到端（End-to-End） | API/控制平面（Control Plane） |

---

## 十一、AAA

### 11.1 认证 vs 授权 vs 计费（Authentication vs Authorization vs Accounting）

| 概念（Concept） | 英文（English） | 回答的问题（Question Answered） |
|------|------|-----------|
| **认证** | Authentication | "你是谁？（Who are you?）" |
| **授权** | Authorization | "你能做什么？（What can you do?）" |
| **计费** | Accounting | "你做了什么？（What did you do?）" |

### 11.2 AAA方法列表逻辑（Method List Logic）

方法列表按顺序执行（Sequential Execution），第一个成功的方法结果生效：
```
aaa authentication login default group radius local
→ 先RADIUS → 不可达（Unreachable）则用本地数据库（Local Database）→ 都失败则拒绝（Deny）
```

### 11.3 方法列表关键字（Method List Keywords）

| 关键字（Keyword） | 含义（Meaning） |
|--------|------|
| `group radius` | RADIUS服务器组（Server Group） |
| `group tacacs+` | TACACS+服务器组 |
| `local` | 本地用户名数据库（Local Username Database） |
| `local-case` | 本地数据库，区分大小写（Case-Sensitive） |
| `none` | 不认证直接允许（No Authentication, Permit All） |
| `enable` | 使用enable密码（Enable Password） |
| `line` | 使用线路密码（Line Password） |
| `if-authenticated` | 只要已认证就授权通过（Authorize if Already Authenticated） |

### 11.4 常见配置模式（Common Configuration Patterns）

```
# TACACS+认证 + 本地回退（Fallback to Local）
aaa authentication login default group tacacs+ local

# RADIUS不可达时无需凭据（No Credentials if RADIUS Down，不安全但有时考题出现）
aaa authentication login default group radius none

# 命令授权（Command Authorization，控制能执行什么命令）
aaa authorization exec default group tacacs+ local

# 命令计费（Command Accounting，记录privilege 15命令）
aaa accounting commands 15 default start-stop group tacacs+

# 三层回退（Three-Level Fallback）：TACACS+ → 本地 → enable密码
aaa authentication login default group ISE-Servers local enable
```

### 11.5 RADIUS vs TACACS+

| 特性（Feature） | RADIUS | TACACS+ |
|------|--------|---------|
| 传输协议（Transport） | UDP | TCP |
| 加密（Encryption） | 仅加密密码（Password Only） | 加密整个载荷（Entire Payload） |
| 分离认证/授权（Separate AuthN/AuthZ） | 合并（Combined） | 分离（Separated） |
| 思科专有（Cisco Proprietary） | 否(开放标准, Open Standard) | 是 |

### 11.6 线路认证配置（Line Authentication Configuration）

- VTY线路（远程访问, Remote Access）：`login local`（本地数据库）、`login authentication <列表名>`
- Console线路：`login`（线路密码）、`login local`、`login authentication <列表名>`
- `transport input ssh`：只允许SSH（Secure Shell）
- `access-class <ACL号> in`：限制谁可以访问VTY
- `privilege level 15`（线路下, Under Line Configuration）：登录直接进特权模式（Privileged EXEC Mode）
- 注意区分：`exec-timeout`（空闲超时 Idle Timeout）vs `absolute-timeout`（绝对超时 Absolute Timeout）vs `session-limit`（会话数限制 Session Limit）

---

## 十二、NAT

### 12.1 NAT类型（NAT Types）

| 类型（Type） | 配置关键字（Config Keyword） | 映射关系（Mapping） |
|------|-----------|---------|
| **静态NAT（Static NAT）** | `ip nat inside source static` | 一对一永久映射（One-to-One Permanent） |
| **动态NAT（Dynamic NAT）** | `ip nat inside source list <ACL> pool <池名>` | 多对多（Many-to-Many），从池中分配（Allocate from Pool） |
| **PAT（Port Address Translation）** | `... overload` | 多对一（Many-to-One，端口复用 Port Multiplexing） |

### 12.2 静态NAT vs PAT

| 特性（Feature） | 静态NAT（Static NAT） | PAT (overload) |
|------|---------|----------------|
| 映射（Mapping） | 固定一对一（Fixed 1:1） | 动态多对一（Dynamic Many:1） |
| 双向发起（Bidirectional Initiation） | 可以（Yes） | 仅内部发起（Inside-Initiated Only） |
| 确定性（Deterministic） | 确定 | 不确定 |
| IP节省（IP Conservation） | 不节省 | 大幅节省 |
| 配置关键字（Keyword） | `static` | `overload` |

### 12.3 关键配置规则（Key Configuration Rules）

- `ip nat inside`：连接内网（Internal Network）的接口
- `ip nat outside`：连接外网（External Network）的接口
- 流量方向：**inside→outside = 源地址转换（Source NAT）**
- 流量方向：**outside→inside = 目标地址转换（Destination NAT）**
- ACL通配符掩码（Wildcard Mask）：标准ACL用反掩码（如`0.0.0.255`表示/24）

### 12.4 服务器负载均衡NAT（Server Load Balancing NAT）

- `type rotary`：轮询方式（Round-Robin）
- 配合`ip nat inside destination-list`实现入站负载均衡（Inbound Load Balancing）

---

## 十三、QoS

### 13.1 无线QoS金属等级（Wireless QoS Metal Levels）

| 等级（Level） | 优先级（Priority） | 用途（Use） |
|------|--------|------|
| **Platinum（铂金）** | 最高（Highest） | 语音（Voice，Fastlane模式） |
| **Gold（金）** | 高（High） | 视频（Video） |
| **Silver（银）** | 中（Medium） | 尽力而为数据（Best-Effort Data） |
| **Bronze（铜）** | 低（Low） | 背景流量（Background Traffic） |

### 13.2 QoS配置框架（MQC, Modular QoS CLI）

```
class-map（类映射） → 分类流量（Classify Traffic）
policy-map（策略映射） → 定义策略动作（Define Policy Actions）
service-policy（服务策略） → 将策略应用到接口（Apply Policy to Interface）
```

### 13.3 关键概念（Key Concepts）

- **LLQ（Low Latency Queuing，低延迟队列）**：`priority <带宽>`必须有带宽值（Must Specify Bandwidth）
- **CBWFQ（Class-Based Weighted Fair Queuing）**：保证带宽（Guaranteed Bandwidth）+ 拥塞时排队丢弃（Queue & Drop on Congestion）
- **PBR** 用于路由决策（Routing Decision），**QoS** 用于流量调度（Traffic Scheduling）——两者不同
- 入站标记（Ingress Marking）：`service-policy input` + `set dscp`

---

## 十四、NTP

### 14.1 NTP核心概念（NTP Core Concepts）

- **Stratum（层级）**：0=原子钟/GPS（Atomic Clock），1=直连stratum0（Directly Connected），数值越大越不可靠（Higher = Less Reliable）
- 每经过一个NTP跳（Hop），stratum+1
- `ntp master`：将自己设为NTP权威服务器（Authoritative Server，使用本地硬件时钟 Hardware Clock）
- 127.127.1.1 = 本地硬件时钟（Local Hardware Clock，NTP中的表示）
- `*~`在`show ntp associations`中 = 已同步（Synchronized）+ 已配置（Configured）

### 14.2 NTP配置（NTP Configuration）

| 命令（Command） | 用途（Purpose） |
|------|------|
| `ntp master` | 成为NTP主服务器（Master Server） |
| `ntp server <IP>` | 作为客户端向服务器同步（Client → Server Sync） |
| `ntp peer <IP>` | 对称模式（Symmetric Active Mode，对等体 Peer） |
| `ntp broadcast` | 接口下发送NTP广播（Send NTP Broadcast） |
| `ntp authenticate` | 启用NTP认证（Enable Authentication） |
| `ntp authentication-key 1 md5 <key>` | 定义密钥（Define Key） |
| `ntp trusted-key 1` | 信任密钥1（Trust Key 1） |
| `ntp source <接口>` | 指定NTP包源接口（Source Interface） |

### 14.3 NTP认证（NTP Authentication）

- 默认使用MD5哈希（Hash）
- 必须trusted-key才能用于认证（Key Must Be Trusted）

---

## 十五、自动化工具

### 15.1 四大工具对比（Four Automation Tools Comparison）

| 特性（Feature） | Ansible | Puppet | Chef | SaltStack |
|------|---------|--------|------|-----------|
| **Agent** | 不需要(SSH, Agentless) | 需要（Agent-Based） | 需要（Agent-Based） | 需要(Minion) |
| **语言（Language）** | Python | Ruby DSL | Ruby | Python |
| **配置语法（Config Syntax）** | YAML | 专有DSL（Proprietary DSL） | Ruby | YAML |
| **方法（Approach）** | **过程式（Procedural）** | **声明式（Declarative）** | **过程式（Procedural）** | **声明式（Declarative）** |
| **模型（Model）** | Push（推送） | Pull（拉取） | Pull（拉取） | Push+Pull |
| **架构（Architecture）** | 无主从 | 多主（Multi-Master） | - | Master/Minion |

### 15.2 过程式（Procedural）vs 声明式（Declarative）

| 方法（Approach） | 特征（Characteristic） | 代表工具（Tools） |
|------|------|---------|
| **过程式（Procedural）** | 定义"怎么做（How）"，按顺序执行步骤 | Ansible, Chef |
| **声明式（Declarative）** | 定义"要什么结果（What）"，工具自己实现 | Puppet, SaltStack |

### 15.3 配置管理（Configuration Management）vs 编排（Orchestration）

| 概念（Concept） | 基础设施（Infrastructure） | 代表工具（Tools） |
|------|---------|---------|
| **配置管理（Config Mgmt）** | 可变（Mutable Infrastructure） | Ansible, Puppet, Chef |
| **编排（Orchestration）** | 不可变（Immutable Infrastructure） | Terraform, K8s |

---

## 十六、数据建模与API

### 16.1 YANG

- **定义（Definition）**：数据建模语言（Data Modeling Language），描述数据的结构（Structure）、类型（Type）和约束（Constraints）
- **独立于传输协议（Transport-Independent）**（可配合NETCONF、RESTCONF、gRPC等）
- **四种节点（Four Node Types）**：leaf、leaf-list、container、list
- **enumeration（枚举）**：YANG支持的枚举类型（从预定义名称中引用值）
- YANG定义的是"数据长什么样（What Data Looks Like）"

### 16.2 NETCONF

- 网络配置协议（Network Configuration Protocol，RFC 6241）
- 使用**XML**编码（Encoding）
- 通过SSH传输（端口830, Port 830）
- 包含RPC操作：get-config、edit-config等
- 可使用XML filter（过滤器）限制返回数据量（Reduce Data Returned）
- vManage用NETCONF推送策略到vSmart

### 16.3 RESTCONF

- 基于HTTP的RESTful配置协议（RFC 8040）
- 使用JSON或XML
- HTTP方法：GET(读Read)、POST(创建Create)、PUT(替换Replace)、PATCH(修改Modify)、DELETE(删除Delete)
- DNAC和vManage**北向API（Northbound API）**使用RESTCONF

### 16.4 控制器API方向（Controller API Directions）

| API方向（Direction） | 通信对象（Communication） | 协议（Protocol） | 格式（Format） |
|---------|---------|------|------|
| **北向（Northbound）** | 控制器 → 应用/编排（Application/Orchestrator） | RESTCONF (RESTful) | **JSON** |
| **南向（Southbound）** | 控制器 → 网络设备（Network Device） | NETCONF | **XML** |

### 16.5 JSON格式规范（JSON Format Rules）

- 键名（Key Name）必须用**双引号（Double Quotes）**
- 字符串值（String Value）用**双引号**
- 数字（Number）和布尔值（Boolean）不加引号
- 数组（Array）用`[]`，对象（Object）用`{}`
- **最后一个元素后不能有逗号（No Trailing Comma）**
- `json.dumps(obj)`：Python对象 → JSON字符串（Serialize）
- `json.loads(str)`：JSON字符串 → Python对象（Deserialize）
- `json.dump(obj, file)`：写入文件（Write to File）
- `json.load(file)`：从文件读取（Read from File）

### 16.6 数据建模语言的优势（Benefits of Data Modeling Languages）

- 统一多厂商配置方法（Unified Multivendor Configuration）
- 数据易结构化（Structured）、分组（Grouped）、验证（Validated）
- 重构厂商特定配置为标准配置（Refactor Vendor-Specific to Standard）
- 功能易于扩展（Easier Feature Extensibility）

---

## 十七、Python

### 17.1 基础语法考点（Syntax Essentials）

```python
# range(n) 生成 0 到 n-1（Generates 0 to n-1）
for x in range(5):   # → 0,1,2,3,4
for x in range(6):   # → 0,1,2,3,4,5

# 列表乘法（List Multiplication）= 内容重复拼接（Repeat & Concatenate）
[1,2] * 3  # → [1,2,1,2,1,2]

# 列表索引（List Index）从0开始
list = [1,2,3,4]
list[3] = 10   # → [1,2,3,10]

# 取模运算（Modulo）
(3 * 5) % 2  # → 15 % 2 = 1（余数 Remainder）

# while循环
count = 8
while count > 4:  # → 8,7,6,5

# 百分比格式化（Percentage Formatting）
format(0.8, '.0%')   # → "80%"
format(0.08, '.0%')  # → "8%"

# 运算符优先级（Operator Precedence）：乘除 > 加减
num + 2 * 10  # 先 2*10=20，再加 num

# while循环终止条件
while loop != 999:  # loop等于999时终止（Terminates）

# 列表索引
list = [1,2,3,4]
list[3] = 10   # 索引3=第4个元素, → [1,2,3,10]
```

### 17.2 常用库（Common Libraries）

| 库（Library） | 用途（Purpose） |
|----|------|
| `json` | JSON序列化/反序列化（Serialization/Deserialization） |
| `requests` | HTTP/REST API调用（API Calls） |
| `ncclient` | NETCONF客户端（NETCONF Client，用于网络设备配置） |
| `paramiko` | SSH连接网络设备（SSH to Network Devices） |
| `jinja2` | 模板引擎（Template Engine） |
| `sqlite3` | 轻量数据库（Lightweight Database） |

### 17.3 import方式（Import Methods）

```python
import json              # 导入整个模块（Entire Module）→ json.dumps()
from json import dumps   # 导入特定函数（Specific Function）→ dumps()
from ncclient import manager  # 导入子模块（Sub-Module）
```

---

## 十八、EEM

### 18.1 EEM（Embedded Event Manager，嵌入式事件管理器）结构

```
event manager applet <名称 Name>
 event <触发条件 Trigger Condition>
 action <编号 Number> cli command "命令 Command"
```

### 18.2 常用event类型（Common Event Types）

| Event | 用途（Purpose） |
|-------|------|
| `event none` | 手动触发（Manual Trigger Only） |
| `event syslog pattern "..."` | 匹配syslog消息（Match Syslog Messages） |
| `event cli pattern "..." sync yes` | 匹配CLI命令（Match CLI Commands） |
| `event track <N> state unreachable` | Track对象状态变化（Track Object State Change） |
| `event timer watchdog time <秒>` | 定时触发（Periodic Timer） |
| `event neighbor-discovery` | CDP邻居发现（CDP Neighbor Discovery） |

### 18.3 常用action（Common Actions）

| Action | 用途（Purpose） |
|--------|------|
| `action X cli command "..."` | 执行CLI命令（Execute CLI Command） |
| `action X syslog msg "..."` | 生成syslog消息（Generate Syslog Message） |
| `action X syslog priority critical msg "..."` | 生成critical级别syslog（Critical-Level Syslog） |
| `action X snmp-trap strdata "..."` | 发送SNMP trap（Send SNMP Trap） |
| `action X puts "..."` | 输出到控制台（Print to Console, Tcl命令） |
| `action X mail server ...` | 发送邮件（Send Email） |
| `action X regexp "..." "$_cli_result" match <变量>` | 正则表达式匹配（Regex Matching） |

### 18.4 关键规则（Key Rules）

- 执行特权命令前需要`action X cli command "enable"`（先进入特权模式）
- 同步applet（`sync yes`）：阻塞用户输入直到执行完成（Block User Input Until Complete）
- `event none` = 纯手动触发（Manual Only，通过`event manager run`执行）
- `$_cli_result` = 上一个CLI命令的输出（Output of Previous CLI Command）

---

## 十九、REST API

### 19.1 HTTP方法（HTTP Methods）

| 方法（Method） | 作用（Action） |
|------|------|
| **GET** | 读取资源（Read/Retrieve Resource） |
| **POST** | 创建资源（Create Resource） |
| **PUT** | 替换/更新资源（Replace/Update Resource） |
| **PATCH** | 部分修改资源（Partial Modify Resource） |
| **DELETE** | 删除资源（Delete Resource） |

### 19.2 HTTP状态码（HTTP Status Codes）

| 状态码（Status Code） | 含义（Meaning） |
|--------|------|
| 200 OK | 成功（Success） |
| 201 Created | 创建成功（Resource Created） |
| **204 No Content** | 成功但无返回体（Success, No Body） |
| 400 Bad Request | 格式错误（Malformed Request, e.g. JSON Error） |
| **401 Unauthorized** | 未认证（Authentication Failed） |
| **403 Forbidden** | 已认证但无权限（Authenticated but Forbidden） |
| **404 Not Found** | 资源不存在（Resource Not Found） |
| 500 Internal Server Error | 服务器错误（Server Error） |
| **504 Gateway Timeout** | 网关超时（Gateway Timeout） |

### 19.3 REST API安全（REST API Security）

- **Basic Auth（基础认证）**：Base64编码用户名密码（需配合HTTPS，否则不安全）
- **OAuth 2.0**：令牌授权（Token-Based Authorization），不暴露密码（No Password Exposure）
- **JWT（JSON Web Token）**：编码的JSON令牌（Encoded JSON Token），用于安全交换信息（Secure Information Exchange）
- **HTTPS (TLS/SSL)**：保护传输中的凭据（Protect Credentials in Transit）
- **API Key**：简单无状态认证（Simple Stateless Authentication）
- **时间戳（Timestamp）**：防止重放攻击（Prevent Replay Attacks）
- **CORS（Cross-Origin Resource Sharing，跨源资源共享）**：防止浏览器跨源脚本攻击（Prevent Cross-Origin Script Attacks）
- **WAF（Web Application Firewall，Web应用防火墙）**：保护API平台（Secure API Platforms）

### 19.4 REST安全设计原则（REST Security Design Principles）

| 原则（Principle） | 含义（Meaning） |
|------|------|
| **Fail-Safe Defaults（故障安全默认）** | 默认拒绝（Deny by Default），显式授权（Explicitly Grant） |
| **Complete Mediation（完全中介）** | 每次访问都验证（Verify Every Access），不依赖缓存（No Cached Permissions） |
| **Least Privilege（最小权限）** | 只给完成任务所需的最小权限 |
| **Economy of Mechanism（机制经济性）** | 设计越简单越安全（Simpler = More Secure） |

### 19.5 HTTP/2

- **多路复用（Multiplexing）**：单个TCP连接并发多请求（Single Connection, Multiple Concurrent Requests）
- 区别于HTTP/1.1的串行请求（Serial Requests）

---

## 二十、网络设计

### 20.1 三层层次化模型（Three-Tier Hierarchical Model）

```
┌──────────────┐
│   核心层（Core Layer）│ ← 高速转发（High-Speed Forwarding），冗余（Redundancy），简单（Simplicity）
├──────────────┤
│   分布层（Distribution Layer）│ ← L2/L3边界（Boundary），策略（Policy），聚合（Aggregation）
├──────────────┤
│   接入层（Access Layer）│ ← 终端连接（Endpoint Connection），端口安全（Port Security）
└──────────────┘
```

| 层（Layer） | 功能（Function） | 不应做的事（Should NOT Do） |
|----|------|-----------|
| **核心层（Core）** | 高速转发、冗余三层链路（Redundant L3 Links） | QoS标记、安全策略（Security Policy）、FHRP |
| **分布层（Distribution）** | 流量聚合（Traffic Aggregation）、L2/L3边界、路由（Routing） | - |
| **接入层（Access）** | 连接终端（Connect Endpoints）、端口安全 | 路由决策（Routing Decisions） |

### 20.2 折叠核心（Collapsed Core）

- 中型网络（Medium-Sized Network）：**核心+分布合并（Merge Core & Distribution）** + 独立接入层（Separate Access Layer）
- 节省硬件成本（Save Hardware Cost）同时保持模块化（Modularity）

### 20.3 Spine-Leaf（脊叶架构）

```
    Spine   Spine
     │  ╲    │  ╱
     │   ╲  │ ╱
     │    ╲ │╱
    Leaf   Leaf   Leaf
     │      │      │
    服务器  服务器  服务器
```

- **Leaf（叶交换机）**：连接终端/服务器 → 转发到Spine
- **Spine（脊交换机）**：Leaf之间的高速转发
- Spine之间不互连（No Spine-to-Spine Links），Leaf之间不互连（No Leaf-to-Leaf Links）
- 所有Leaf连所有Spine（Full Mesh）

### 20.4 模块化设计（Modularity in Network Design）

- 自包含（Self-Contained）、可复用（Repeatable）的网络区块
- 好处：**可扩展性（Scalability）+ 快速故障隔离（Quick Failure Isolation）**
- 路由接入（Routed Access）设计便于迁移到SD-Access

### 20.5 传统WAN vs SD-WAN

| 特性（Feature） | 传统WAN（Traditional WAN） | SD-WAN |
|------|---------|--------|
| 配置方式（Configuration） | 逐台手动CLI（Manual Per-Device） | 集中模板化（Centralized Template） |
| 部署时间（Deployment Time） | 数周（Weeks） | 数小时（Hours） |
| 控制平面（Control Plane） | 分布式（Distributed） | 集中式（Centralized） |
| 数据平面开销（Data Plane Overhead） | 低（Low） | 较高（Higher，加密+封装） |
| 策略管理（Policy Management） | 逐台配置（Per-Device） | 集中统一（Centralized） |

---

## 二十一、高可用

### 21.1 StackWise

- 将多台物理交换机堆叠（Stack）为一台逻辑交换机（Logical Switch）
- 主交换机（Active/Primary）仅在**重置/重启（Reset/Reload）**时失去角色
- 新交换机加入**不触发重新选举（No Re-Election）**
- 新成员IOS/配置由主交换机自动同步（Auto-Sync）

### 21.2 VSS（Virtual Switching System，虚拟交换系统）

- **恰好合并两台（Exactly Two）**物理交换机
- 支持Catalyst 4500/6500系列和3750/3850
- 优势：**单一管理点（Single Point of Management）**，简化运维

### 21.3 SSO（Stateful Switchover，状态化切换）

- 主备RP（Route Processor，路由处理器）之间同步状态信息（路由表Routing Table、ARP、NAT转换等）
- 故障时备用RP无缝接管（Seamless Takeover）
- 优势：**韧性/可靠性（Resiliency）**

### 21.4 NSF（Non-Stop Forwarding，不间断转发）

- 与SSO配合：SSO同步状态（Synchronize State），NSF保持转发（Maintain Forwarding）
- RP切换期间：**数据沿已知路径继续转发（Forward Along Known Paths）**
- 路由协议收敛（Reconverge）后才更新FIB（Forwarding Information Base，转发表）

### 21.5 BFD（Bidirectional Forwarding Detection，双向转发检测）

- **亚秒级（Sub-Second，<1秒）**链路故障检测
- 与**动态路由协议（Dynamic Routing Protocols）**配合实现快速收敛（Fast Convergence）
- SD-WAN中用于检测数据平面隧道质量（Tunnel Quality：丢包Loss/延迟Latency/抖动Jitter）
- 前提：所有参与路由器需启用CEF（Cisco Express Forwarding）和IP路由
- BFD会增加CPU使用（非减少，Not Reducing CPU Usage）

---

## 二十二、无线

### 22.1 WLC SSO

- Active WLC（Wireless LAN Controller，无线局域网控制器）与AP建立CAPWAP隧道
- Standby从Active**复制（Copy）**AP和客户端数据库（Client Database）
- AP只与Active建立一条CAPWAP隧道

### 22.2 SD-Access无线（SD-Access Wireless）

- **控制平面（Control Plane）**：CAPWAP隧道 → WLC
- **数据平面（Data Plane）**：VXLAN隧道 → AP直接到Fabric Edge Node（绕过WLC, Bypass WLC）
- 好处：WLC不再是数据瓶颈（Data Bottleneck）
- **OTT（Over-the-Top）模式**：无线不集成到fabric，保持传统CAPWAP（Coexist with Traditional Deployment）

### 22.3 无线资源管理（RRM, Radio Resource Management）

- 即使在SD-Access中，RRM仍在WLC上执行
- 包括信道选择（Channel Selection）、功率调整（Power Adjustment）、负载均衡（Load Balancing）

---

## 二十三、附录

### 23.1 重要协议号（Important Protocol Numbers）

| 协议（Protocol） | IP协议号（IP Protocol #） | 组播地址（Multicast Address） | 端口（Port） |
|------|---------|---------|------|
| OSPF | **89** | 224.0.0.5/6 | - |
| EIGRP | **88** | 224.0.0.10 | - |
| VRRP | 112 | 224.0.0.18 | - |
| HSRPv1 | - | 224.0.0.2 | UDP 1985 |
| NETCONF | - | - | TCP **830** |
| SNMP | - | - | UDP 161/162 |

### 23.2 重要管理距离（Important Administrative Distances）

| 路由协议（Routing Protocol） | AD（Administrative Distance） |
|---------|-----|
| 直连（Connected） | 0 |
| 静态（Static） | 1 |
| EIGRP内部（Internal） | **90** |
| OSPF | **110** |
| EIGRP外部（External） | **170** |
| BGP外部（eBGP） | 20 |
| BGP内部（iBGP） | 200 |

### 23.3 MAC地址识别（MAC Address Identification）

| 协议（Protocol） | 虚拟MAC格式（Virtual MAC Format） |
|------|------------|
| HSRPv1 | **0000.0c07.ac**XX (XX=组号十六进制, Group Number in Hex) |
| HSRPv2 | 0000.0c9f.fXXX |
| VRRP | **0000.5e00.01**XX |

### 23.4 通配符掩码速记（Wildcard Mask Quick Reference）

```
/24 → 0.0.0.255 （255 - 每个字节的值 = 通配符掩码）
/30 → 0.0.0.3
/16 → 0.0.255.255
any → 255.255.255.255
host → 0.0.0.0
```

### 23.5 认证技术对比（Authentication Technology Comparison）

| 技术（Technology） | 类型（Type） | 安全性（Security） |
|------|--------|--------|
| HTTP Basic Auth | Base64编码（Encoding） | 低（Low，无HTTPS时） |
| OAuth 2.0 | Token授权（Token-Based Authorization） | 高（High） |
| JWT | 签名Token（Signed Token） | 高（High） |
| MD5 | 哈希（Hash） | 中（Medium，已不够安全） |
| SHA | 哈希（Hash） | 高（High） |

### 23.6 私有/公有IP范围（Private IP Ranges）

| 类别（Class） | 范围（Range） |
|------|------|
| A类私有（Class A Private） | 10.0.0.0/8 |
| B类私有（Class B Private） | 172.16.0.0/12 |
| C类私有（Class C Private） | 192.168.0.0/16 |

---

> **祝考试顺利通过！Good luck with your exam!** 🎯
>
> 建议复习顺序（Recommended Study Order）：先背第一章速记卡片（Quick Reference Cards）→ 再逐一阅读各章节（Read Each Section）→ 最后再做一遍速记卡片自我测试（Self-Test）。
