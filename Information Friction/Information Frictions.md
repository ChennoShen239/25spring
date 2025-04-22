> NBER workshop

**今天为止：**  
我们一直假设**完全信息**与**理性预期**（“FIRE”）
**今天的重点：**  
偏离 FIRE 的情形（“信息摩擦”）
- **信息不完全**（例如：噪声信息、信息粘性）
- **偏离理性预期**（例如：外推、认知贴现、Level-k 思维）
这是当前解释宏观与金融中关键谜题的有力候选框架，例如：
- 为什么 **通胀、投资、消费** 对**总量冲击**反应如此缓慢？（但对个体冲击却不是？） 
- 为什么**资产价格**对冲击**反应过度**？

- **小问题：** 偏离 FIRE 的模型通常很难在简单的代表性个体（RA）模型基础上进行模拟  
  - 例如：[Mankiw and Reis, 2007]，[Maćkowiak and Wiederholt, 2015]

- **今天的目标：** 构建一个**连贯的框架**来建模和模拟偏离 FIRE 的情形  
  - 不仅适用于 RA，还适用于异质个体（HA）！

- 本次内容主要基于我们在 [Auclert et al., 2020] 中发展的方法  
  - 有趣的新工作：[Bardoczy et al., 2023] 使用了这一方法

设我们有货币政策的 IKC 方程：
$$dY = M_r\,dr + M\,dY\tag{1}$$

其中 $M_r \equiv \frac{\partial C}{\partial r}$，$M \equiv \frac{\partial C}{\partial Y}$ 是家庭侧的雅可比矩阵，适用于：
- 异质个体（HA）、代表性个体（RA）、时变代理（TA）、零利率下限（ZL）等模型。

假设家庭对整个经济**完全是短视的（myopic）**：
- 他们仅在第 $t$ 期开始对 $dr_t$ 有反应，
- 也仅在第 $t$ 期开始对 $dY_t$ 有反应。

那么此时的 $dY$ 会是多少？我们能否在方程 (1) 的基础上进行调整以反映这种行为？

### 操作雅可比矩阵（Manipulating the Jacobians）

- 从 “FIRE” 框架下的 iMPCs 开始（$M_r$ 类似）：

$$
M =
\begin{pmatrix}
M_{00} & M_{01} & M_{02} & M_{03} & \cdots \\
M_{10} & M_{11} & M_{12} & M_{13} & \cdots \\
M_{20} & M_{21} & M_{22} & M_{23} & \cdots \\
M_{30} & M_{31} & M_{32} & M_{33} & \cdots \\
\vdots & \vdots & \vdots & \vdots & \ddots
\end{pmatrix}
\quad\Rightarrow\quad
M =
\begin{pmatrix}
M_{00} & 0      & 0      & 0      & \cdots \\
M_{10} & M_{00} & 0      & 0      & \cdots \\
M_{20} & M_{10} & M_{00} & 0      & \cdots \\
M_{30} & M_{20} & M_{10} & M_{00} & \cdots \\
\vdots & \vdots & \vdots & \vdots & \ddots
\end{pmatrix}
$$

- 每一列 $s$ 表示消费对“第 $s$ 期产出上升”这一新闻冲击的响应  
- 在我们的“行为型（behavioral）”模型中，第 $s$ 期的新闻冲击在第 $s$ 期之前**完全无效应**  
- 那么在第 $s$ 期之后会发生什么？——变成了对一个**意外冲击（unanticipated shock）** 的反应！

我们把这种变换称为 **“雅可比矩阵操作（Jacobian manipulation）”**  
> 注：$M$ 的每一列的净现值（NPV）是多少？

### 预期矩阵（Expectations Matrix）

- 另一种视角：**个体是如何对某一日期 $s$ 的冲击形成预期的？**  
- 我们可以定义一个矩阵 $E$，其中每一列 $s$ 表示对“第 $s$ 期冲击为 1”的预期。

- 在 **FIRE 模型** 中，$E$ 如下：

$$
E =
\begin{pmatrix}
1 & 1 & 1 & 1 & \cdots \\
1 & 1 & 1 & 1 & \cdots \\
1 & 1 & 1 & 1 & \cdots \\
1 & 1 & 1 & 1 & \cdots \\
\vdots & \vdots & \vdots & \vdots & \ddots
\end{pmatrix}
$$

- 在 **行为型模型** 中，$E$ 变为：

$$
E =
\begin{pmatrix}
1 & 0 & 0 & 0 & \cdots \\
1 & 1 & 0 & 0 & \cdots \\
1 & 1 & 1 & 0 & \cdots \\
1 & 1 & 1 & 1 & \cdots \\
\vdots & \vdots & \vdots & \vdots & \ddots
\end{pmatrix}
$$

- 因此，$E_{t,s}\,dY_s$ 就表示 **个体在 $t$ 期对 $dY_s$ 的期望值**。

### 那么我们如何求解 $dY$ 的一般均衡（GE）响应？

- 其实只需使用 $M$ 和 $M_r$：
  
$$
dY = M_r\,dr + M\,dY
$$

- 这就是核心思想：
	- 通过对雅可比矩阵的结构进行操作，**无需新增任何计算成本**，  
	- 就可以求解我们的 **短视型（myopic）经济模型**！

![[Pasted image 20250421213441.png]]
### 求解财政政策下的行为型 IKC（behavioral IKC）

- 另一个应用场景：我们希望求解**财政乘数（fiscal multipliers）**，
- 但假设个体**既不预期未来税收**，也**不预期未来收入**。

那么，**正确的 IKC 形式**应该是什么？
$$
dY = dG - M\,dT + M\,dY
$$
- 下一步：将这个思路**推广到更一般的信念形成模型**中！


### 我们将作出的一些一般性假设

我们会默认以下几个隐含假设：

- 个体仅对**总量变量的变动**表现出“行为型”反应；
	- 稳态（steady state）不受影响；
	- 对**个体收入过程**没有行为偏离。

- 偏离 FIRE 的成分与个体状态变量**正交**；
	- 这个假设是可以放松的，但超出本次讨论范围（参见 [Guerreiro, 2022]）。

### 可分型 vs 不可分型的 FIRE 偏离（Separable vs Non-separable Deviations）

我们区分两类概念上不同的 FIRE 偏离形式：

- **可分型（Separable）偏离：**  
  - 一单位的第 $s$ 期新闻冲击**不会改变**对其他时期冲击的预期；  
  - 例如：我们之前讨论的情况！

- **不可分型（Non-separable）偏离：**  
  - 一单位的第 $s$ 期新闻冲击**会改变**对其他时期冲击的预期；  
  - 例如：**外推（extrapolation）**。我在 $s=0$ 期观察到高产出，因此相信 $s>0$ 时期也会有高产出。

> 注意：这是一个新的术语体系，目前不确定是否有他人也以此方式分类。

---

**接下来：我们只关注可分型偏离。不可分型属于另一个方向。**
### 一般性的预期矩阵（General Expectations Matrix）

- 考虑一个一般形式的矩阵 $E = (E_{t,s})$  
- 元素 $E_{t,s}$ 表示 **个体在第 $t$ 期对“第 $s$ 期单位冲击” 的平均预期**
- 若满足**可分性与线性性**，则 $E_{t,s}\,dY_s$ 表示**第 $t$ 期对 $dY_s$ 的预期**

我们将基于以下两个假设之一：
1. 个体在冲击发生时已经对其有**准确预期**，即对所有 $t \geq s$，都有 $E_{t,s} = 1$；
2. 或者：雅可比矩阵 $M$ 具有这样的结构：**对过去冲击的认知不会改变行为**。
---
- 一个典型的例子：

$$
E =
\begin{pmatrix}
1 & * & * & * & \cdots \\
1 & 1 & * & * & \cdots \\
1 & 1 & 1 & * & \cdots \\
1 & 1 & 1 & 1 & \cdots \\
\vdots & \vdots & \vdots & \vdots & \ddots
\end{pmatrix}
$$

- 对应的 **FIRE 基准** 为：

$$
E =
\begin{pmatrix}
1 & 1 & 1 & 1 & \cdots \\
1 & 1 & 1 & 1 & \cdots \\
1 & 1 & 1 & 1 & \cdots \\
1 & 1 & 1 & 1 & \cdots \\
\vdots & \vdots & \vdots & \vdots & \ddots
\end{pmatrix}
$$
### 一般的 Jacobian 操作（General Jacobian Manipulation）

- 我们如何利用 $E$ 和一个 **FIRE 下的 Jacobian $M$** 来构造“行为型”下的 Jacobian $\tilde{M}$？
- 考虑一个将在第 $s$ 期生效的单位新闻冲击（unit news shock）。它的反应过程如何？
- 在每个时间点 $\tau$，对该冲击的预期发生变化的幅度为：$E_{\tau,s} - E_{\tau-1,s}$
- 关键：这是一个**提前 $s - \tau$ 期**的新闻冲击  
  $⇒$ 因此对应的是 $M$ 的第 $s - \tau$ 列！

---

- 所以：$\tilde{M}$ 的第 $s$ 列可以表示为：

$$
\tilde{M}_{t,s} = \sum_{\tau=0}^{\min\{t,\,s\}} \underbrace{ (E_{\tau,s} - E_{\tau-1,s}) \cdot M_{t-\tau,\,s-\tau} }_{ \text{date-} t \text{ effect of date -}\tau \text{ expectation revision of date-} s\text{ shock} }
$$其中约定 $E_{-1,s} = 0$

> 该表达式的含义：  
> 每一项表示“第 $t$ 期对第 $s$ 期冲击的响应”，  
> 是由“第 $\tau$ 期关于第 $s$ 期冲击的**预期修正**”所引起的。

### 进一步理解 Jacobian 操作：FIRE 与无前瞻对比

- 回顾通用形式：

$$
\tilde{M}_{t,s} = \sum_{\tau=0}^{\min\{t,\,s\}} (E_{\tau,s} - E_{\tau-1,s}) \cdot M_{t-\tau,\,s-\tau}
$$
#### **FIRE 情形：** $E_{t,s} = 1$ 对所有 $t \geq 0$

- 仅有 $\tau = 0$ 项不为零（因 $E_{-1,s} = 0$）  
  ⇒ 得到 $\tilde{M}_{t,s} = M_{t,s}$，正是原始 Jacobian。
#### **无前瞻（No-foresight）情形：** $E_{t,s} = 0$ 对所有 $t < s$

- 仅当 $\tau = s$ 时，$(E_{\tau,s} - E_{\tau-1,s}) = 1$  
  ⇒ 当 $t < s$ 时无效应（$\tilde{M}_{t,s} = 0$）  
  ⇒ 当 $t \geq s$ 时：$\tilde{M}_{t,s} = M_{t-s,\,0}$

这正是我们前面构造出的“行为型 Jacobian 矩阵”。
#### 补充说明：也可以使用“假新闻矩阵”（fake news matrix）来表达：

$$
\tilde{M}_{t,s} = \sum_{\tau=0}^{\min\{t,\,s\}} E_{\tau,s} \cdot F_{t-\tau,\,s-\tau}
$$

其中 $F$ 是每一时期对虚假新闻冲击的响应函数。
 - Next, we’ll walk through examples from the literature 
 - For each, there is an E and an M
### (1) 信息粘性（Sticky Information）

- [Mankiw and Reis, 2002] 提出了一个基于信息摩擦的**名义刚性**微观基础。
- 设有质量为 1 的价格制定者群体，他们理想中希望设定的价格为边际成本加成：

$$
\log P_{it} = \log \mu + \log MC_t
$$
其中 $MC_t$ 是一个随机过程。
- 核心思想：每期只有一个随机比例 $1 - \theta$ 的价格制定者能获得最新的信息。  
  - 这就是所谓的“**信息粘性模型**”。
- 在极限情形 $\theta = 0$ 时，所有人每期都获得新信息，回归为**完全灵活价格模型**：
$$
\log P_t = \log \mu + \log MC_t
$$
### (1) 信息粘性的嵌套形式（Nesting Sticky Information）

- 更一般地，我们希望知道 $\log P_t$ 对 $\log MC_t$ 的 Jacobian。
- 在 FIRE 情形下，Jacobian 是单位矩阵：$M = I$
---
- 对于信息粘性模型，其**预期矩阵 $E$** 和对应的“行为型”Jacobian $\tilde{M}$ 为：

$$
E =
\begin{pmatrix}
1 - \theta & 1 - \theta & 1 - \theta & \cdots \\
1 - \theta^2 & 1 - \theta^2 & 1 - \theta^2 & \cdots \\
1 - \theta^3 & 1 - \theta^3 & 1 - \theta^3 & \cdots \\
\vdots & \vdots & \vdots & \ddots
\end{pmatrix}
\quad\Rightarrow\quad
\tilde{M} =
\begin{pmatrix}
1 - \theta & 0 & 0 & \cdots \\
0 & 1 - \theta^2 & 0 & \cdots \\
0 & 0 & 1 - \theta^3 & \cdots \\
\vdots & \vdots & \vdots & \ddots
\end{pmatrix}
$$

---
- 有了这个 $\tilde{M}$，我们就可以对任意的边际成本冲击 $d \log MC_t$ 求解 $\log P_t$ 的响应：
$$
d \log P_t = \tilde{M} \cdot d \log MC_t
$$
### (2) 预期粘性（Sticky Expectations）

- 上述方法仅适用于**过去冲击的信息不会影响行为**的情形  
  ⇒ **这在异质个体（HA）模型中并不成立！**
- 一个简单的替代方案来自 [Carroll et al., 2020]：  
  假设每个个体在单位冲击**真正发生**时都会学习到它。
- 这样就可以将该方法推广应用于 HA 模型。
---
- 预期矩阵 $E$ 与对应的行为型 Jacobian $\tilde{M}$ 为：

$$
E =
\begin{pmatrix}
1 & 1 - \theta & 1 - \theta & \cdots \\
1 & 1 & 1 - \theta^2 & \cdots \\
1 & 1 & 1 & \cdots \\
\vdots & \vdots & \vdots & \ddots
\end{pmatrix}
$$

$$
\tilde{M} =
\begin{pmatrix}
M_{00} & (1 - \theta)M_{01} & (1 - \theta)M_{02} & \cdots \\
M_{10} & (1 - \theta)M_{11} + \theta M_{00} & (1 - \theta)M_{12} + \theta(1 - \theta)M_{01} & \cdots \\
M_{20} & (1 - \theta)M_{21} + \theta M_{10} & \cdots & \cdots \\
\vdots & \vdots & \vdots & \ddots
\end{pmatrix}
$$
- 详见 [Auclert et al., 2020]，其中对该思路进行了全面讨论，并将其用于一般均衡分析。
![[Pasted image 20250421220549.png]]
- 中间值的 $\theta$ 会生成强烈的“驼峰型”响应（hump-shaped response）
- 其中一部分原因是**内生的**：  当初期的 $dY$ 较小时 $⇒$ 消费 $dC$ 也会随之下降。

### (3) 分散信息（Dispersed Information）

- 此类模型假设个体在学习速度上存在高度异质性：  
	- 有些人立即掌握全部信息，另一些则要晚很多。
- 那么如果我们假设所有个体**学习得一样快**，会发生什么？
---
- 为了说明这一点，考虑一个由 $MA(∞)$ 过程生成的 $dY_s$：
$$
\widetilde{dY}_t = \sum_{s=0}^{\infty} dY_s\,\varepsilon_{t-s}, \quad \varepsilon_t \sim \mathcal{N}(0, \tau_\varepsilon^{-1})
$$
- 含义是：当冲击 $\varepsilon_t$ 发生（如 $\varepsilon_t = 1$）时，$\widetilde{dY}_t$ 的冲击响应函数（IRF）就是 $(dY_s)$。
---

- 有两种方式来建模“分散信息”：
	1. 关于**外生过程**的信息分散：个体获得关于 $\varepsilon_t$ 的信号；
	2. 关于**内生过程**的信息分散：个体获得关于 $\widetilde{dY}_t$ 的信号。
- 第 2 种更难处理！（思考一下为什么？）  
  ⇒ 我们现在先处理第 1 种情况。

### 分散信息与创新（Dispersed Information about Innovation）

- 假设每个个体 $i$ 接收到关于当前与过去创新的信号：

$$
s^{(i)}_{j,t} = \varepsilon_{t-j} + \nu^{(i)}_{j,t}, \quad \nu^{(i)}_{j,t} \sim \mathcal{N}(0, \tau_j^{-1}) \text{ i.i.d.}
$$

- 允许每期扰动具有不同精度 $\tau_j$（任意指定）。
- 设在 $t = 0$ 发生一次性冲击：$\varepsilon_0 = 1$  
- 个体对 $\varepsilon_0$ 的平均预期如何演化？
- 根据贝叶斯更新（Bayesian updating）：

$$
\mathbb{E}_t[\varepsilon_0] = \frac{\sum_{j=0}^t \tau_j}{\tau_\varepsilon + \sum_{j=0}^t \tau_j} \equiv 1 - \theta_t
$$

- 详见 [Auclert et al., 2020] 的附录。类似模型也见 [Angeletos and Huo, 2021]。

---

### 分散信息（续）

- 给定 $\theta_t$，预期矩阵 $E$ 看起来几乎与信息粘性模型一致：
$$
E =
\begin{pmatrix}
1 & 1 - \theta_0 & 1 - \theta_0 & 1 - \theta_0 & \cdots \\
1 & 1 & 1 - \theta_1 & 1 - \theta_1 & \cdots \\
1 & 1 & 1 & 1 - \theta_2 & \cdots \\
1 & 1 & 1 & 1 & \cdots \\
\vdots & \vdots & \vdots & \vdots & \ddots
\end{pmatrix}
$$

- 实际上，只要给定一组 $\tau_j$，就可以**复制信息粘性 / 预期粘性模型**的行为。
	- 直觉：在一阶近似下，**只有平均预期是关键**  
	- **谁拥有了哪些信息并不重要**。

Plot similar to sticky expectations, but a bit less hump-shaped
![[Pasted image 20250421221318.png]]

### (4) 认知贴现（Cognitive Discounting）

- [Gabaix, 2020] 引入了“认知贴现”的概念
- 核心思想：个体对 **$h$ 期后发生的冲击**的反应相当于将该冲击视为大小被缩减为 $\theta^h$ 的冲击。
- 等价地说：个体**预期单位冲击的大小为 $\theta^h$**
---
- 相应的预期矩阵 $E$ 为：

$$
E =
\begin{pmatrix}
1 & \theta & \theta^2 & \theta^3 & \cdots \\
1 & 1 & \theta & \theta^2 & \cdots \\
1 & 1 & 1 & \theta & \cdots \\
1 & 1 & 1 & 1 & \cdots \\
\vdots & \vdots & \vdots & \vdots & \ddots
\end{pmatrix}
$$

---
- 概念上，这与“分散信息”或“信息粘性”不同：
	- 分散信息 / 信息粘性：相对**第一个时期**的预期滞后或分散；
	- 认知贴现：相对**对角线项**进行逐步**削弱**（dampening）。
Doesn’t generate humps, but dampens forward guidance very strongly
![[Pasted image 20250421221612.png]]

### (5) Level-$k$ 思维（Level $k$ Thinking）

- [Farhi and Werning, 2019] 是首篇将**异质个体（HA）** 与 **FIRE 偏离**结合的论文。
- 他们采用了 **Level-$k$ 思维模型**，可在我们的入门经济框架下解释如下：
  - $k = 1$：所有个体认为**产出处于稳态**；
  - $k = 2$：所有个体认为其他所有人都是 $k = 1$；
  - $k = 3$：所有个体认为其他人是 $k = 2$；
  - $\dots$ 依此类推。

### Level-$k = 1$：初阶行为（回顾）

- Level-1 思维很好处理，实际上这就是我们最开始的例子。
- 对应的预期矩阵 $E$ 为：
$$
E =
\begin{pmatrix}
1 & 0 & 0 & 0 & \cdots \\
1 & 1 & 0 & 0 & \cdots \\
1 & 1 & 1 & 0 & \cdots \\
1 & 1 & 1 & 1 & \cdots \\
\vdots & \vdots & \vdots & \vdots & \ddots
\end{pmatrix}
$$
- 对应的 Jacobian 为：

$$
M^{(1)} =
\begin{pmatrix}
M_{00} & 0 & 0 & 0 & \cdots \\
M_{10} & M_{00} & 0 & 0 & \cdots \\
M_{20} & M_{10} & M_{00} & 0 & \cdots \\
M_{30} & M_{20} & M_{10} & M_{00} & \cdots \\
\vdots & \vdots & \vdots & \vdots & \ddots
\end{pmatrix}
$$

- 对应的 IKC 方程为：
$$
dY^{(1)} = M_r\,dr + M^{(1)} \cdot dY^{(1)}
$$
---

### 更高阶：Level-$k > 1$
- 通过递推求解：
$$
dY^{(k+1)} = M_r\,dr + M \cdot dY^{(k)} 
\quad + \quad M^{(1)} \cdot \left(dY^{(k+1)} - dY^{(k)}\right)
$$

- 理解方式：
  - $M \cdot dY^{(k)}$：所有人**预期其他人是 Level-$k$ 思维**；
  - $M^{(1)} \cdot (dY^{(k+1)} - dY^{(k)})$：**个体对偏离 Level-$k$ 没有意识**，因此只使用 Level-1 响应来处理偏差。

![[Pasted image 20250421222018.png]]

### 结论（Conclusion）

- **信息刚性（information rigidities）** 可以非常自然地嵌套在**序列空间（sequence space）**框架中。

- 这不仅为我们提供了一个在代表性个体（RA）模型中进行模拟的**直接方法**，  同样也能**有效应用于异质个体（HA）模型**！
