## 第2章	MOS器件物理基础

#### 学习集成电路设计的一些思路：

（热学+电磁学 $\longrightarrow$ ）量子力学 $\longrightarrow$ 固体物理、半导体物理、器件物理 $\longrightarrow$ 电路设计

将半导体器件看作黑盒子，只关注伏安特性曲线在电路中的运用

#### $MOSFET$ 基本介绍

![image-20240709000742746](https://raw.githubusercontent.com/heiheiha798/Razavi-Notes/main/img/image-20240709000742746.png)

$Metal-Oxide-Semiconductor\ Field-Effect\ Transistor$

四端器件：栅、源、漏、衬 （ $Gate、Source、Drain、Bulk$ ）

源：提供载流子的终端

漏：收集载流子的终端

对于NMOS和PMOS，载流子不同会导致电流方向等一系列差别，但很显然这些差别应该是对称的

重要尺寸：源漏通道的横向尺寸栅长 $L$ ，垂直方向栅宽 $W$ ，氧化层厚度 $t_{ox}$ ，

典型工作时 $GD$ 二极管反偏，所以 $n$ 阱往往接高电位

$MOS$ 符号：

![image-20240709001959403](https://raw.githubusercontent.com/heiheiha798/Razavi-Notes/main/img/image-20240709001959403.png)

NMOS和PMOS器件的衬底端通常接地和接 $V_{DD}$ ，所以通常省略 $B$ 端

#### $MOS$ 的 $I-V$ 特性

考虑一个 $NFET$ ，衬底默认接地，栅压 $V_{G}$ 从 $0V$ 刚开始上升时， $p$ 衬底中的空穴受高电势排斥，形成耗尽层， $SD$ 之间近似断路；随着 $V_{G}$ 的不断增大，
