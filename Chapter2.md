## 第2章	MOS器件物理基础

#### 学习集成电路设计的一些思路：

（热学+电磁学 $\longrightarrow$ ）量子力学 $\longrightarrow$ 固体物理、半导体物理、器件物理 $\longrightarrow$ 电路设计

将半导体器件看作黑盒子，只关注伏安特性曲线在电路中的运用



#### $MOSFET$ 基本介绍

<img src="https://raw.githubusercontent.com/heiheiha798/Razavi-Notes/main/img/image-20240709000742746.png" style="zoom:80%;">

$Metal-Oxide-Semiconductor\ Field-Effect\ Transistor$

四端器件：栅、源、漏、衬 （ $Gate、Source、Drain、Bulk$ ）

源：提供载流子的终端

漏：收集载流子的终端

重要尺寸：源漏通道的横向尺寸栅长 $L$ ，垂直方向栅宽 $W$ ，氧化层厚度 $t_{ox}$ ，

典型工作时 $GD$ 二极管反偏，所以 $n$ 阱往往接高电位

$MOS$ 符号：

<img src="https://raw.githubusercontent.com/heiheiha798/Razavi-Notes/main/img/image-20240709001959403.png" style="zoom:80%;">

NMOS和PMOS器件的衬底端通常接地和接 $V_{DD}$ ，所以通常省略 $B$ 端



#### $MOS$ 的 $I-V$ 特性

以 $NFET$ 为例

阈值电压 $V_{TH}$ ：通常定义为界面的少子浓度等于多子浓度时的栅压
$$
V_{TH}=\Psi_{MS}+2\Psi_F+\frac{Q_{dep}}{C_{ox}}
$$
$\Psi_{MS}$ 是多晶硅栅和硅衬底的功函数差电压值

$\Psi_{F}=\frac{kT}{q}ln(\frac{N_{sub}}{n_i})$ ，其中 $N_{sub}$ 是衬底掺杂浓度， $n_i$ 是硅本征载流子浓度

$Q_{dep}$ 是耗尽区电荷（ $Q_{dep}=\sqrt{4 q \varepsilon_{si} |\Psi_{F}|N_{sub}}$ ）

$C_{ox}$ 是单位面积的栅氧化层的电容

制造中往往在沟道区注入杂质调整阈值电压
$$
\begin{equation}
\begin{split}
Q_{d} &= WC_{ox}(V_{GS}-V_{TH})\\\Rightarrow
Q_{d}(x) &= WC_{ox}[V_{GS}-V(x)-V_{TH}]\\\Rightarrow
I_{D} &= -WC_{ox}[V_{GS}-V(x)-V_{TH}]v\\\Rightarrow
I_{D} &= WC_{ox}[V_{GS}-V(x)-V_{TH}]\mu_{n}\frac{dV(x)}{dx}\\\Rightarrow
\int_{x=0}^{L} I_{D}dx &= \int_{V=0}^{V_{DS}}WC_{ox}\mu_{n}[V_{GS}-V(x)-V_{TH}]dV\\\Rightarrow
I_{D} &= \mu_{n}C_{ox}\frac{W}{L}[(V_{GS}-V_{TH})V_{DS}-\frac{1}{2}V_{DS}^2]
\end{split}
\end{equation}
$$
称 $V_{GS}-V_{TH}$ 为过驱动电压， $\frac{W}{L}$ 为宽长比

注意：这里的积分上限是 $L$，这意味着我们默认沟道全导通，这让我们得到了一个抛物线

在抛物线的起始区域做线性近似，得到
$$
I_D \approx \mu_{n}C_{ox}\frac{W}{L}(V_{GS}-V_{TH})V_{DS}
$$
这意味着我们可以将 $MOS$ 器件看作一个压控线性电阻，这段称为“欧姆区”

考虑 $V_{GS}$ 比较大，超过抛物线的极值点，即 $V_{DS}>V_{GS}-V_{TH}$ 时，注意到
$$
Q_{d}(x) = WC_{ox}[V_{GS}-V(x)-V_{TH}]
$$
这意味某些区域中少子浓度太低，还处在耗尽状态，这导致沟道被夹断，其长度小于 $L$ ，这将改变积分的上限
$$
\begin{equation}
\begin{split}
\int_{x=0}^{L'} I_{D}dx &= \int_{V=0}^{V_{GS}-V_{TH}}WC_{ox}\mu_{n}[V_{GS}-V(x)-V_{TH}]dV\\\Rightarrow
I_{D}L' &= \frac{1}{2}WC_{ox}\mu_{n}(V_{GS}-V_{TH})^2\\\Rightarrow
I_{D} &= \frac{1}{2}\frac{W}{L'}C_{ox}\mu_{n}(V_{GS}-V_{TH})^2
\end{split}
\end{equation}
$$
若忽略 $L'$ 和  $L$ 的差别，则器件的电流恒定，成为压控流源，这段称为“饱和区”

对于 $PFET$ 器件，只需将所有有正负意义的物理量取反即可

综上推导：<img src="https://raw.githubusercontent.com/heiheiha798/Razavi-Notes/main/img/image-20240709093424846.png" style="zoom:60%;">

定义跨导 ：
$$
g_m=\frac{\partial I_D}{\partial V_{GS}}|_{V_{DS,const}}
=\mu_nC_{ox}\frac{W}{L}(V_{GS}-V_{TH})
$$
在处理小信号时要用到



#### 二级效应

##### 体效应

$V_{s}=V_{D}=0$ ， $V_{G}$ 略小于 $V_{TH}$ ，当 $V_{B}$ 变负时，耗尽层吸引更多的电子，使得 $V_{TH}$ 增大
$$
V_{TH}=V_{TH0}+\gamma(\sqrt{|2\Psi_{F}+V_{SB}|}-\sqrt{|2\Psi_{F}|})\\
其中\gamma=\frac{\sqrt{2q\varepsilon_{si}N_{sub}}}{C_{ox}}
$$

##### 沟道长度调制

在之前的积分中我们认为沟道夹断后 $L=L'$ ，实际上 $L'$ 是$V_{DS}$ 的函数，不妨设
$$
\begin {equation}
\begin{split}
L' &= L-\delta L\\
又:I_{D}L' &= \frac{1}{2}WC_{ox}\mu_{n}(V_{GS}-V_{TH})^2\\\Rightarrow
I_{D} &\approx \frac{1}{2}WC_{ox}\mu_{n}(V_{GS}-V_{TH})^2(1+\lambda V_{DS})
\end{split}
\end{equation}
$$

其中 $\lambda$ 是沟道长度调制系数，沟道越长， $\lambda$ 值越小

##### 亚阈值导电性

当 $V_{GS}\approx V_{TH}$ 时存在指数关系的源漏电流
$$
I_D=I_0exp(\frac{V_{GS}}{\zeta V_T})
$$
称器件工作在弱反型区

<img src="https://raw.githubusercontent.com/heiheiha798/Razavi-Notes/main/img/image-20240709122337494.png" style="zoom:70%;">

考虑亚阈值导电性负效应使得伏安曲线平滑，但同时也使得 $V_{TH}$ 的定义模糊，我们重新定义 $V_{TH}$ 为两段曲线外推交点对应的电压值

认为过渡点导数连续：
$$
\begin{equation}
\begin{split}
\frac{I_D}{\zeta V_{T}} &=\frac{2I_D}{(V_{GS}-V_{TH})_1}\\\Rightarrow
(V_{GS}-V_{TH})_1 &=2\zeta V_T
\end{split}
\end{equation}
$$



#### MOS器件模型

##### MOS器件版图

源、漏、栅区域必须有一个或多个“接触窗口”，窗口填满金属并与上层金属线连接

<img src="https://raw.githubusercontent.com/heiheiha798/Razavi-Notes/main/img/image-20240709144646994.png" style="zoom:60%;">

值得注意的是：多晶硅栅要超出沟道区域一定的量以确保晶体管的边缘有安全的定界

<img src="https://raw.githubusercontent.com/heiheiha798/Razavi-Notes/main/img/image-20240709144708041.png" style="zoom:60%;">

##### MOS器件电容

认为电容存在于 $MOSFFET$ 四端的任意两个之间

<img src="https://raw.githubusercontent.com/heiheiha798/Razavi-Notes/main/img/image-20240709145156867.png" style="zoom:50%;">

电容的分类：

<img src="https://raw.githubusercontent.com/heiheiha798/Razavi-Notes/main/img/image-20240709150342613.png" style="zoom:50%;">

​	1.栅和沟道之间的氧化层电容 $C_1=WLC_{ox}$

​	2.衬底和沟道之间的耗尽层电容 $C_2=WL\sqrt{q\varepsilon_{si}N_{sub}/(4\Psi_F)}$

​	3.多晶硅栅与源和漏的覆盖而产生的电容 $C_3$ 和 $C_4$ ，单位宽度的覆盖电容用 $C_{ov}$ 表示

​	4.源/漏区与衬底之间的结电容，一般分解为下极板电容 $C_j$ 和侧壁电容 $C_{jsw}$ 分别表示单位面积的电容和单位长度的电容

<img src="https://raw.githubusercontent.com/heiheiha798/Razavi-Notes/main/img/image-20240709150502279.png" style="zoom:50%;">

源漏结电容一般近似用面积和周长计算： $C_{DB}=C_{SB}=S_{面积}C_j+L_{周长}C_{jsw}$ 

覆盖电容 $C_{GD}=C_{GS}=C_{ov}W$ 

栅—衬底电容 $C_{GB}=(WLC_{ox})C_d/(WLC_{ox}+C_d)$ 其中耗尽层电容 $C_d=WL\sqrt{q\varepsilon_{si}N_{sub}/(4\Psi_F)}$

在 $S$ 和 $D$ 电位近似相等时，栅—沟道电容被栅源和栅漏平分，这时 $C_{GD}=C_{GS}=\frac12 WLC_{ox}+C_{ov}W$

在 $NMOS$ 管工作在饱和区时，沟道电子集中在 $S$ 区， $V_{GD}\approx WC_{ov}$ ， $V_{GS}\approx WC_{ox}+2WL_{eff}C_{ox}/3$

(注： $\frac23$ 的系数推导来自于R. S. Muller and T. I. Kamins .Device Electronics for Integrated Circuits. Second Ed.,New York : Wiley,1986.我推不出来, GPT不想回答我)

<img src="https://raw.githubusercontent.com/heiheiha798/Razavi-Notes/main/img/image-20240709185328400.png" style="zoom:70%">

##### MOS小信号模型

当信号显著影响偏置工作点时使用上述规律进行分析，当信号对偏置影响很小时，可以在大信号偏置的基础上进行一阶分析

当 $MOSFETs$ 偏置在饱和区时， 小信号 $\delta V=V_{GS}$ 引起的漏电流增量为 $g_mV_{GS}$ 可以等效为一个压控流源

<img src="https://raw.githubusercontent.com/heiheiha798/Razavi-Notes/main/img/image-20240709191527463.png" style="zoom:70%;">

考虑沟道长度调制效应后 $I_D=\frac12 \mu_nC_{ox}\frac{W}{L}(V_{GS}-V_{TH})^2(1+\lambda V_{DS})$

这时电路的传递系数多了一个线性电阻 
$$
r_o
=\frac{\partial V_{DS}}{\partial I_D}
=\frac{1}{\frac12 \mu_nC_{ox}\frac{W}{L}(V_{GS}-V_{TH})^2\lambda}
=\frac{1+\lambda V_{DS}}{\lambda I_D} 
\approx \frac{1}{\lambda I_D}
$$
考虑体效应后漏电电流是衬底电压的函数，用 $DS$ 之间的电流源模拟这一关系， $I=g_{mb}V_{BS}$ 
$$
\begin {equation}
\begin {split}
g_{mb} & = \frac{\partial I_D}{\partial V_{BS}}\\
& = \mu_{n}C_{ox}\frac{W}{L}(V_{GS}-V_{TH})(-\frac{\partial V_{TH}}{\partial V_{BS}})
\end {split}
\end {equation}
$$


根据 $V_{TH}=V_{TH0}+\gamma(\sqrt{|2\Psi_{F}+V_{SB}|}-\sqrt{|2\Psi_{F}|})$
$$
\begin {equation}
\begin {split}
\Rightarrow  \frac{\partial V_{TH}}{\partial V_{BS}} & = -\frac{\partial V_{TH}}{\partial V_{SB}}\\
& = - \frac{\gamma}{2}(2\Psi_F+V_{SB})^{-\frac12}
\end {split}
\end {equation}
$$
结合 $g_m=\mu_nC_{ox}\frac{W}{L}(V_{GS}-V_{TH})$ ：
$$
g_{mb}=g_m\frac{\gamma}{2\sqrt{2\Psi_F+V_{SB}}}=\eta g_m
$$
从式子中可以看出： $V_{SB}$ 增加时体效应效果会变弱；同时  $g_mV_{GS}$ 和 $g_{ms}V_{BS}$ 有相同的极性，这意味着衬底可以看成另一个栅

综合电容和各种二级效应，可以得到完整的 $MOS$ 小信号模型

<img src="https://raw.githubusercontent.com/heiheiha798/Razavi-Notes/main/img/image-20240709201446110.png" style="zoom:70%;">
