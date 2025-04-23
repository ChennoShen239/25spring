> This is the course note for ECON 236B Lecture 11, please use it with [[Lecture_11.pdf]]

> [!PDF|yellow] [[Lecture_11.pdf#page=4&selection=0,13,0,13&color=yellow|Lecture_11, p.4]]
> > Keynes (1936)
> 
> **凯恩斯（1936）**：即便不考虑投机带来的不稳定性，人类天性的某些特征本身也会造成不稳定性——我们大量的积极行动，更多是依赖于一种自发的乐观情绪，而非建立在道德的、享乐的或经济的数学预期之上。
> 
> 我们之所以做出许多带有积极意义的决策，而这些决策的全部后果往往需要在未来很长一段时间里逐步显现，其原因，大概只能归结为“动物精神”——一种自发的行动冲动而非不作为的倾向，而不是出于对各种量化收益与其概率加权平均的理性计算。

“集体动物精神” $⇒$ “商业周期”？  
“新凯恩斯主义”是否意味着：不再包含动物精神的凯恩斯主义？

> [!PDF|yellow] [[Lecture_11.pdf#page=5&selection=0,0,0,31&color=yellow|Lecture_11, p.5]]
> > Pigou (1927)’s Theory of Cycles
> 
> **皮古（1927）的周期理论**：
>
>经济衰退与繁荣的产生，是由于经济主体在准确预测未来经济对资本的需求方面存在困难。
>
>当人们对未来持乐观态度时，他们会出于对未来需求的预期而决定积累资本。
>
>而一旦这些预期未能实现，就会出现一段时间的投资收缩期，从而很可能引发经济衰退。

## 宏观经济学中的经典多重均衡模型

### 宏观经济学中关于协调失灵的经典模型

- **特点**：具有“强烈的互补性”（strong complementarities）
- **模型特征**：允许存在多重均衡（multiple equilibria）

---

### “动物精神”（Animal Spirits）的角色

- 被视为在多个均衡之间的**信念转移**
- 即使**基本面和对基本面的信念保持不变**，均衡也可能发生变化

---

### 为什么这类模型在当下不再流行

- 虽然在 1980 年代影响深远（如 Diamond, 1982；Benhabib & Farmer, 1994），但现今使用较少
- 面临以下困难：
  - **难以进行政策和福利分析**
  - **“太阳斑”（sunspots）与“均衡切换”缺乏明确的实证对应物**
  - **强互补性**通常依赖于**非标准假设**


## 具有强互补性的协调博弈（Coordination Games with Strong Complementarity）

每个个体 $i$ 的最优行为为：

$$
k_i = G(K, \theta_i)
$$

其中 $K = \int k_i \, di$ 表示总体行为水平。

---

### 弱互补性（Weak Complementarity）

- 条件：  
  $$
  \frac{\partial G}{\partial K} \in (0, 1) \quad \forall K
  $$
- 含义：理性化结果唯一  
- 示例：线性“选美博弈”模型（如前几讲所述）

---

### 强互补性（Strong Complementarity）

- 条件：  
  $$
  \frac{\partial G}{\partial K} > 1 \quad \text{在某些 } K \text{ 上成立}
  $$
- 含义：可能出现多个均衡  
> Just go to the figure and you'll see
- 应用场景：
  - 货币危机
  - 债务危机  
- 代表文献：Obstfeld（1996）、Calvo（1998）

## 多重均衡模型的问题（Issues of Multiple Equilibria Models）

- **难以进行政策和福利分析**
- **难以找到“太阳斑”（sunspots）和“均衡切换”的确切实证对应物**
- **强互补性通常依赖于非标准假设**
- **多重均衡的存在缺乏“鲁棒性”**
  - 需要**完美协调**
  - “全球博弈”（Global Games）框架表明：一旦引入**不完全协调**（如微小的不确定性），就会导致**均衡唯一性**

## 收益与最优反应（Payoff and Best Responses）

存在**强烈的战略互补性**：

- 个体只有在**现状即将崩溃时才愿意发起攻击**
- 而**现状是否崩溃**取决于是否有**足够多的个体发动攻击**

---

### 更清晰的表示方式

将个体 $i$ 的效用函数重写如下（假设 $b > c > 0$）：

$$
u_i = U(a_i, A, \theta) =
\begin{cases}
a_i (b - c) & \text{若 } A \geq \theta \\
- a_i c & \text{若 } A < \theta
\end{cases}
$$

其中：

- $a_i \in \{0, 1\}$ 表示个体是否发动攻击（1 为攻击，0 为不攻击）  
- $A$ 表示总体攻击人数（或攻击比例）  
- $\theta$ 是临界阈值（现状崩溃的条件）

---

### 最优反应函数（Best Response）

在 $\theta$ 已知的前提下，个体的最优反应为：

$$
g(A, \theta) = \arg \max_{a \in \{0, 1\}} U(a_i, A, \theta) =
\begin{cases}
1 & \text{若 } A \geq \theta \\
0 & \text{若 } A < \theta
\end{cases}
$$

---

这表明每个个体的最优行为高度依赖于他人行为的总量 —— 是**协调博弈**中的典型特征。
## 完美协调基准（Perfect Coordination Benchmark）

假设所有个体**完全了解基本面** $\theta$（即 $\theta$ 是公共知识）。

---

### 三种情形：

1. **当 $\theta \leq \underline{\theta} \equiv 0$ 时**  
   - 政权必然崩溃  
   - **唯一均衡**：所有个体都选择攻击

2. **当 $\theta > \bar{\theta} \equiv 1$ 时**  
   - 政权无论面临多大规模的攻击都能幸存  
   - **唯一均衡**：所有个体都不攻击

3. **当 $\theta \in (\underline{\theta}, \bar{\theta}]$ 时**  
   - 出现**多重均衡**，由**自我实现的信念（self-fulfilling beliefs）**所支持：

     - 若个体预期**其他人都会攻击**，那么攻击是个体的最优策略，最终导致现状被放弃  
     - 若个体预期**其他人都不攻击**，那么不攻击是个体的最优策略，最终现状得以维持

---

### 多重均衡的根源：

- 来自于**完美协调**的假设  
- 个体“只有在**确定**所有人都攻击时才会选择攻击”  
- 即均衡的选择依赖于一个精确的、协调一致的共同信念

## 不完全战略互动与均衡唯一性（Imperfect Strategic Interactions and Equilibrium Uniqueness）

引入**带噪声的私人信号**，打破完美协调：

$$
x_i = \theta + \varepsilon_i, \quad \varepsilon_i \overset{\text{i.i.d.}}{\sim} \mathcal{N}(0, \sigma^2_\varepsilon)
$$

其中 $\theta$ 的分布为“非信息型先验”（uninformed prior）。

---

### 如何转化为博弈中的“战略不确定性”（Strategic Uncertainty）

- 个体无法准确知道 $\theta$，因此也**无法确定其他人是否会攻击**
- 出现**不完全协调（Imperfect Coordination）**

---

### 关键结果（Global Games 的核心发现）

只要 $\sigma_\varepsilon > 0$，**无论多么小**，均衡就会**唯一**：

- 存在一组唯一的、理性化的阈值：
  - $x^*$：个体层面的攻击阈值——个体仅当 $x_i < x^*$ 时选择攻击
  - $\theta^*$：政权崩溃的全局阈值 ——只有当 $\theta < \theta^*$ 时，政权最终会崩溃

> [!PDF|yellow] [[Lecture_11.pdf#page=16&selection=32,0,54,1&color=yellow|Lecture_11, p.16]]
> > But both xk and xk converge to x∗ as k → ∞.
> 
> This is basically how you solve a global game

## 不完全协调与均衡选择（Imperfect Coordination and Equilibrium Selection）

在存在**不完全协调**与**战略不确定性**的情况下：

- 无法无摩擦地协调于“攻击”或“不攻击”的某个特定均衡  
- 个体对他人行为的分布产生“平滑化”的信念：

  ⋆ 一些接收到**较高信号**的人仍会选择攻击  
  ⋆ 一些接收到**较低信号**的人会选择不攻击  

$⟶$ 最终导向一个**唯一均衡**

---

### 反思：“多重均衡”是否真的能代表“动物精神”？

- 虽然传统模型用**多重均衡**来模拟“动物精神”带来的突然转变  
- 但“全球博弈”（Global Game）框架下：
  - 依然可以描述**突然的“制度转变”**（regime switching）  
  - 然而，**均衡是唯一的**，只是它对 $\theta$ 接近阈值时的变动**极其敏感**

---

### 优势：

- 在这种模型下可以进行**政策分析**与**福利分析**

## 标准唯一均衡框架下的现代研究路径（Modern Approaches within the Standard Unique Equilibrium Framework）

### 1. **新闻冲击（News Shocks）**
- 指对未来全要素生产率（TFP）的消息性预期变化  
- 代表性文献：
  - *Beaudry and Portier (2006)*
  - *Jaimovich and Rebelo (2009)*
  - *Schmitt-Grohe and Uribe (2012)*

---

### 2. **噪声冲击（Noise Shocks）**
- 指对未来 TFP 的**错误或带偏信念**，这些信念与实际 TFP 过程正交  
- 代表性文献：
  - *Lorenzoni (2009)*
  - *Blanchard, Huillier & Lorenzoni (2013)*

---

### 3. **关于总需求的信念冲击**
- 个体对**总需求的信念变化**，并不依赖于对 TFP 的信念  
- 代表性文献：
  - *Angeletos & La’O (2013)*
  - *Angeletos, Collard & Dellas (2018, 2020)*

---

### 4. **完全行为路径（Fully Behavioral Approaches）**
- 如“诊断性预期（diagnostic expectations）”模型  
- 代表性文献：
  - *Bordalo, Gennaioli, Shleifer (2018)*
  - *Bordalo, Gennaioli, Shleifer, Terry (2020)*

---

这些研究在**均衡唯一性保持不变**的前提下，引入了对信念、预期或心理偏差的建模，从而解释现实中看似由“动物精神”驱动的宏观波动。

## Barro-King 悖论（The Barro-King Conundrum）

无论何种类型的总需求（AD）冲击，都会在总供给（AS）端遇到一个悖论（Barro 和 King, 1984）：

- AD 冲击指的是仅影响**当前总需求**、但**不影响当前总供给**的冲击  
- 其中也包括对**未来 TFP**的新闻冲击（news shocks）和噪声冲击（noise shocks）
### 悖论的核心：

若冲击不影响 $A_t$，而仅改变了对未来的预期（例如未来 $A_{t+1}, A_{t+2}, \dots$），那么当期的生产 $y_t$ 不变；但在理性的、无摩擦的模型下，这种纯粹的预期冲击很难解释为什么**当前经济会发生显著波动**。

> [!PDF|yellow] [[Lecture_11.pdf#page=21&selection=165,0,165,9&color=yellow|Lecture_11, p.21]]
> > AD shocks
> 
> Here the AD shock can be interpreted as the shock to $\beta$ so that consumer wants more today.

## 第一条出路：新凯恩斯主义 / 粘性价格模型（The First Way Out: NK / Sticky-Price Models）

引入价格或工资刚性，使得**总供给端可以响应总需求变化**。

---

### 核心机制：劳动需求不再是最优的

$$
\underbrace{\frac{U_n(c_t, n_t)}{U_c(c_t, n_t)}}_{\text{消费与劳动的边际替代率（MRS）}} = \underbrace{w_t}_{\text{工资}} \neq \underbrace{f_n(A_t, n_t)}_{\text{劳动的边际产出（MPL）}}
$$

- 在粘性价格模型中，工资或价格调整缓慢  
- 如果是**工资刚性**，则劳动供给也不是最优的  
- 因此，**当期的总供给（AS）可以对总需求（AD）冲击作出反应**

---

### 但需注意：

- **只有在货币政策（MP）未能实现灵活价格情形下的最优配置时**，AD 才会对 AS 产生实际影响  
- 换言之：

  > AD 冲击的效应 = 货币扩张或收缩的效应

---

### 宏观表现（沿着菲利普斯曲线）：

- 通胀与产出**同向变动**（co-movement）
- 即：
  - 需求驱动的经济波动往往伴随着**通胀或通缩**
  - 否则无法在粘性模型中实现当期产出变化
## 第二条出路：可变资本使用率与资本调整成本（The Second Way Out）

- 引入**可变的资本使用率**（variable utilization）和**资本调整成本**  
⟶ 导致企业在生产决策中具有**前瞻性（forward-looking）**  
⟶ 出现**生产的跨期替代**（intertemporal substitution in production）  
⟶ 总供给（AS）可以对总需求（AD）冲击作出反应

---

### 代表性文献：

- Jaimovich and Rebelo (2009)
- Angeletos & Lian (2022)

---

该机制为总需求冲击引起的现实产出波动提供了另一种理论基础，**无需依赖价格或工资刚性**。

---

## 下一步

接下来我们将介绍**将信心、情绪与动物精神具体化**（operationalize confidence, sentiments, and animal spirits）的一些不同路径。


## Jaimovich and Rebelo (2009) 模型的三个核心要素

---

### 要素一：**可变的资本使用率（Variable Capital Utilization）**

$$
Y_t = A_t (u_t K_t)^{1 - \alpha} N_t^{\alpha}
$$

- $u_t$ 表示资本的使用强度（utilization rate）
- 更高的 $u_t$ 可以提升产出，但也可能带来更高的折旧成本

---

### 要素二：**投资的调整成本（Adjustment Costs of Investment）**

$$
K_{t+1} = I_t \left[1 - \phi \left(\frac{I_t}{I_{t-1}}\right)\right] + \left[1 - \delta(u_t)\right] K_t
$$

- 投资变动存在调整成本 $\phi(\cdot)$，通常在投资变化剧烈时成本更高  
- $\delta(u_t)$ 为与使用率相关的折旧率
- **未来投资增加 ⟹ 当前投资也会增加**  
  ⟶ 形成**跨期的投资决策传导**

---

### 要素三：**劳动供给中的微弱财富效应 + 消费习惯形成**

偏好函数如下：

$$
U = E_0 \sum_{t=0}^{\infty} \beta^t \cdot \frac{\left(C_t - \psi N_t^{\theta} X_t\right)^{1 - \sigma} - 1}{1 - \sigma}
$$

其中消费习惯项：

$$
X_t = C_t^{\gamma} X_{t-1}^{1 - \gamma}
$$

- $\gamma = 1$：为标准的 KPR（King-Plosser-Rebelo）型偏好，存在显著的财富效应  
- $\gamma = 0$：无财富效应，但存在消费习惯形成（habit formation）

---

### 关键机制：

- **消费习惯形成**使得：  
  > 未来消费预期上升 ⟹ 当前消费也上升  
- **投资调整机制**使得：  
  > 未来投资预期上升 ⟹ 当前投资也上升  
- 配合可变资本使用率，使得**总供给可以对预期的总需求变化做出响应**，即使没有价格刚性

---

这为构建不依赖粘性价格但仍可响应“信心冲击”或“动物精神”的 DSGE 模型提供了基础。

## 噪声冲击模型（Noise Shocks）——以 Lorenzoni (2009) 为例

### 基本思想

Lorenzoni (2009) 提出了一种与新闻冲击密切相关的机制：**噪声冲击（Noise Shocks）**，其特点为：

- 对未来 TFP（全要素生产率）的**信念发生冲击**  
- 冲击来源于关于未来 TFP 的**公共信号中含有噪声**
- 这些信号会：
  - 提高对未来 TFP 的预期
  - 推升预期总需求
  - **但这些信号与实际的当前和未来 TFP 过程正交（orthogonal）**
- 因此，它可能是对凯恩斯“动物精神”更贴切的建模方式

---

### 模型设定：Lorenzoni (2009)

- 基于**新凯恩斯主义模型框架**，尤其是粘性价格下的**总供给方（AS）**
- 关注的是对 **TFP 持久成分（persistent component）** 的噪声信号
- 信号结构使得经济主体对未来生产率过于乐观（或悲观），从而改变其当前决策

---

### 噪声冲击的动态效应：

- **短期效应**：
  - 提高预期总需求
  - 推动当前的产出、就业和通胀上升

- **长期效应**：
  - 由于信号与真实 TFP 无关，长期并无实际影响
  - 即：**无长期产出或生产率效应**

---

### 总结

Lorenzoni (2009) 展示了：

- **纯信念变化（无基本面依据）**也可以通过新凯恩斯机制在短期内产生真实波动
- 为“动物精神”提供了结构性、理性预期框架下的微观基础

## Lorenzoni (2009)：带有噪声信号的代表性个体模型设定

为了说明模型机制，考虑一个**无异质信息**（no disperse information）的简化版本：

---

### 1. TFP 过程分解为**永久性**和**暂时性**两部分：

$$
a_t = x_t + \eta_t
$$

- $x_t$：TFP 的**永久性成分**（permanent component）  
- $\eta_t$：TFP 的**暂时性成分**（temporary component），  
  $$\eta_t \sim \mathcal{N}(0, \sigma^2_\eta)$$

其中，永久性成分服从单位根过程：

$$
x_t = x_{t-1} + \varepsilon_t, \quad \varepsilon_t \sim \mathcal{N}(0, \sigma^2_\varepsilon)
$$

---

### 2. 关于 $x_t$ 的公共信号：

代表性个体接收到一个关于 $x_t$ 的**带噪声的公共信号** $s_t$：

$$
s_t = x_t + e_t, \quad e_t \sim \mathcal{N}(0, \sigma^2_e)
$$

其中 $e_t$ 即为**噪声冲击（noise shock）**。

---

### 3. 信息结构：

经济主体观察到：

- $a_t$：当期 TFP（含暂时项）
- $s_t$：关于永久成分 $x_t$ 的公共噪声信号

因此，$(a_t, s_t)$ 构成了对 $x_t$ 的不完全信息来源。

---

## Lorenzoni (2009) 模型结构（需求、供给与货币政策）

---

### 1. 总需求方程（Aggregate Demand）：  
由**对数效用**下的标准欧拉方程推导得出：

$$
y_t = \mathbb{E}_t [y_{t+1}] - i_t + \mathbb{E}_t [\pi_{t+1}]
$$

- 其中 $\mathbb{E}_t[\cdot]$ 表示给定当前信息集 $(a_t, s_t)$ 下的期望  
- 表示当前产出 $y_t$ 取决于对未来产出和通胀的预期，以及当期名义利率 $i_t$

---

### 2. 新凯恩斯主义菲利普斯曲线（New Keynesian Phillips Curve）：

$$
\pi_t = \kappa (y_t - a_t) + \beta \mathbb{E}_t [\pi_{t+1}]
$$

- 当前通胀 $\pi_t$ 由产出缺口 $(y_t - a_t)$ 决定  
- $a_t$ 是当期 TFP，$\kappa$ 为价格刚性系数，$\beta$ 为贴现因子

---

### 3. 货币政策规则（Monetary Policy Rule）：

$$
i_t = i^* + \phi \pi_t
$$

- 名义利率 $i_t$ 对当前通胀作出反应，但**不直接响应自然利率或 TFP 水平变化**
- 因此，该规则**无法复制价格完全灵活情形下的最优配置**

---

## Lorenzoni (2009)：均衡与学习机制

---

### 一、均衡条件（Equilibrium）

总产出与通胀由对未来永久性 TFP 的信念 $E_t[x_t]$ 所驱动：

#### 产出：

$$
y_t = \frac{1}{1 + \phi \kappa} \mathbb{E}_t[x_t] + \frac{\phi \kappa}{1 + \phi \kappa} a_t
$$

#### 通胀（NKPC）：

$$
\pi_t = \frac{\kappa}{1 + \phi \kappa} \left(\mathbb{E}_t[x_t] - a_t\right)
$$

- $\phi$：货币政策对通胀的反应强度  
- $\kappa$：价格刚性参数  
- $a_t$：当前 TFP  
- $\mathbb{E}_t[x_t]$：对**TFP 的永久性成分**的预期  
- 均衡中，**预期误差会引发产出与通胀的偏离**

---

### 二、学习机制（Learning Process）

个体对 $x_t$ 的预期更新遵循加权平均的贝叶斯型规则：

$$
\mathbb{E}_t[x_t] = \rho \mathbb{E}_{t-1}[x_{t-1}] \; + \; (1 - \rho) \left( \delta s_t + (1 - \delta) a_t \right)
$$

- 第一项 $\rho \mathbb{E}_{t-1}[x_{t-1}]$ 是**过去的先验**  
- 第二项是基于当前信息 $(s_t, a_t)$ 的**信号加权更新**，其中：
  - $s_t = x_t + e_t$：关于 $x_t$ 的带噪公共信号
  - $\delta \in [0,1]$ 控制主体**更依赖噪声信号还是当前 TFP**
- $\rho \in [0,1]$ 控制学习的**惯性程度**

---

### 模型核心直觉：

- 如果 $\delta$ 较高：个体对噪声信号过度依赖 → **容易受“错误信念”驱动**  
- 预期 $E_t[x_t]$ 偏高 ⟹ 当前产出 $y_t$ 与通胀 $\pi_t$ 被拉高  
- 即使真实的 $x_t$ 没有变化，**信念本身即可驱动经济波动**

## Lorenzoni (2009)：冲击的动态效应

---

### 一、**永久性技术冲击（Permanent Technology Shock）**

对于单位技术冲击 $\varepsilon_t$，其对未来第 $\tau$ 期的动态响应为：

- **产出**：

$$
\frac{dy_{t+\tau}}{d\varepsilon_t} = \frac{1 - \rho^{\tau + 1}}{1 + \phi \kappa}
$$

- **就业**：

$$
\frac{dn_{t+\tau}}{d\varepsilon_t} = -\frac{\rho^{\tau + 1}}{1 + \phi \kappa}
$$

- **通胀**：

$$
\frac{d\pi_{t+\tau}}{d\varepsilon_t} = -\frac{\kappa \rho^{\tau + 1}}{1 + \phi \kappa}
$$

#### 解读：

- 产出**逐步向新的长期水平调整**
- 就业与通胀**短期下降**（由于生产率上升减少了对劳动的需求）
- 存在**跨期替代效应**和价格粘性共同作用

---

### 二、**噪声冲击（Noise Shock）**

对于单位噪声冲击 $e_t$，其对未来第 $\tau$ 期的动态响应为：

- **产出**：

$$
\frac{dy_{t+\tau}}{de_t} = \frac{\rho^\tau (1 - \rho)\delta}{1 + \phi \kappa}
$$

- **就业**：

$$
\frac{dn_{t+\tau}}{de_t} = \frac{\rho^\tau (1 - \rho)\delta}{1 + \phi \kappa}
$$

- **通胀**：

$$
\frac{d\pi_{t+\tau}}{de_t} = \frac{\rho^\tau \kappa (1 - \rho)\delta}{1 + \phi \kappa}
$$

#### 解读：

- 产出、就业和通胀**在短期内上升**
- **完全由错误信念驱动**（并无基本面变化）
- $\rho^\tau$ 使得效应**逐步衰减**
- **长期无效应**：由于实际 TFP 未发生变化，预期最终会回归

---

### 小结对比：

| 冲击类型         | 长期产出效应 | 短期就业与通胀反应 | 驱动机制         |
|------------------|--------------|---------------------|------------------|
| 永久性技术冲击   | 有           | 就业和通胀下降      | 基本面提升       |
| 噪声冲击         | 无           | 就业和通胀上升      | 信念偏误 / 动物精神 |

> Please read this one carefully!


## 情绪（Sentiments）与对 TFP 的信念正交

忠于凯恩斯关于“动物精神”或“信心”的原始概念：

- “动物精神”或“信心波动”是指：
  > 与对**当前和未来 TFP（全要素生产率）的信念正交（orthogonal）

- 换句话说，信心波动并非源于对供给基本面的判断  
  → 例如，可能源自对**总需求（aggregate demand）**的信念变化？

---

这种设定与传统**多重均衡模型中的信念驱动机制**相一致：

- 在传统 sunspot 模型中，不同均衡间的切换常由纯粹信念驱动

---

### 在唯一均衡框架内建模信心波动的可能性

基于 Angeletos 和 La’O (2013)，以及 Angeletos, Collard & Dellas (2018) 的研究：

设经济中存在分散交易（decentralized trading），则：

- 个体对总产出的平均预期可以偏离实际值：

  $$
  \int \mathbb{E}_{i,t} [y_t] \, di = y_t + \xi_t
  $$

- 但个体对 TFP 的平均预期却**等于真实值**：

  $$
  \int \mathbb{E}_{i,t} [A_t] \, di = A_t
  $$

其中：

- $\xi_t$：代表**纯粹的信心（sentiment）扰动**，影响对总需求的看法而非供给面  
- 这种信心冲击不影响结构性生产力判断，但会推动个体行为偏离均衡

---

### 含义：

这种设定为**在唯一均衡理论中引入“动物精神”**提供了基础，同时避免了传统模型中多重均衡难以识别的问题。

## 替代性识别“动物精神”的方法

直接测量**与 TFP 信念正交的总需求信念（beliefs about aggregate demand）**非常困难。

---

### 一种替代性方法：

- **识别出一种冲击**，它在**商业周期频率**内对宏观变量波动的贡献最大

---

### 这种冲击的特征：

- 在解释**宏观变量之间的共动（comovements）方面起到关键作用  
- 在所有时间尺度上，与 **TFP 和通胀无关**  
- 因此可能代表一种“非通胀型的动物精神冲击”**（non-inflationary animal spirits shock）

## 实证实现方法（Empirical Implementation）

- 利用 **结构向量自回归模型（SVAR）** 识别冲击，该冲击在**特定频率区间内**对某一宏观变量的波动解释力最大  
- 类似于在**频域上的主成分分析（PCA）**

---

### 实施方式：

- 通过设定目标变量，识别出五类主要冲击，分别对应：
  - **失业率**
  - **产出**
  - **劳动小时数**
  - **消费**
  - **投资**

---

### 核心发现：

- 这五类冲击是**高度可替代的**：
  - 它们引起的**冲击响应函数（IRFs）几乎一致**
  - 它们之间具有**高度相关性**
- 因此，这些冲击可以被视为**统一的“商业周期共动成分”**

---

### 特征总结：

- **能够解释商业周期期间的宏观变量共动**
- 但与**TFP 和通胀变量正交**
  ⟶ 这类冲击可被解释为**非通胀型的“动物精神”冲击**

## 将“情绪”建模为对总需求冲击的信念过度反应  
——基于 Angeletos & Lian (2022)《信心与总需求冲击的传播》

---

### 主要观点：

- **情绪（sentiment）被建模为对其他总需求（AD）冲击的**信念**过度反应（belief over-reaction）**
- 该信念变化：
  - 与对 TFP（全要素生产率）的信念**正交**
  - 与前述实证证据（如 SVAR 识别的共动但非通胀冲击）相一致

---

### 理论与实证的统一：

- 情绪冲击不再是“神秘的”或“外生的”（no longer *exotic*）  
- 具有**信心乘数效应（confidence multiplier）**

---

### 动态机制：

- **产出 → 消费者与投资者预期 → 产出**  
  ⟶ 构成一个**信心驱动的反馈循环（feedback loop）**

---

### 政策含义：

- 即使供给面无变动，仅由**信念机制**即可放大或持续总需求冲击  
- 为理解“情绪驱动的经济波动”提供了**结构性微观基础**

## 信心与总需求冲击的传播（Confidence and the Propagation of Demand Shocks）

---

### 供给侧设定（Supply Side）

- 与本课程中讲到的“**第二条出路**”相同：
  - 可变资本使用率
  - 投资调整成本
  - 前瞻性生产决策
  ⟶ 总供给端可以响应总需求变化

---

### 总需求侧机制（Demand Side）

- **“岛屿模型”结构**，经济中存在多个消费者/企业，每个面临**异质冲击**
- 个体掌握的信息：
  - 自身的贴现率
  - 自身的收入与利率
- 但对**总需求冲击**的信息不完全，或者**对宏观变化缺乏关注**

---

### 信念传播机制：

1. 出现**总需求冲击**（aggregate demand shock）  
2. 导致每个个体观察到自己的**收入或需求变化**
3. 个体将这一变化**理性地误解为自身的异质性冲击**（即个体性收入/需求波动）
4. 由于大多数人都出现类似“误解”，导致社会中形成对“个体性收入/需求”的集体信念变化
   ⟶ 实质上是**总需求冲击引发的信心传播**

---

### 扩展的行为解释：

- 可被解释为**过度外推（extrapolation）**等更广义的行为偏差
- 与微观实证中关于预期形成的证据一致（如人们倾向于根据近期波动预测未来）

---

### 核心含义：

该机制展示了即使个体是理性的，也可能因信息不全或误解，将总需求冲击错认为个体冲击，从而**自发形成情绪波动**并推动宏观波动。

## 诊断性预期（Diagnostic Expectations）

### 信心（情绪）可被建模为：
对**宏观供给冲击**（如 TFP 变化）的**信念过度反应**  
例如：**诊断性预期模型（diagnostic expectations）** 中的形式如下：

$$
\mathbb{E}_t^{\theta}[A_{t+1}] = \mathbb{E}_t[A_{t+1}] + \theta \left( \mathbb{E}_t[A_{t+1}] - \mathbb{E}_{t-1}[A_{t+1}] \right)
$$

- $\theta > 0$ 表示个体在预期中**过度强调信息的新变化**
- 这种机制产生“**信心膨胀与崩溃**”的动态行为特征

---

### 应用实例

#### 信贷周期（Credit Cycles）：  
Bordalo, Gennaioli, Shleifer (2018)

#### 商业周期（Business Cycles）：  
Bordalo, Gennaioli, Shleifer, Terry (2020)

---

### 模型特征：

- 构建于**现实商业周期模型（RBC）**框架之上
- 具有：
  - **异质性企业**
  - **风险性债务融资**

---

### 信贷市场的典型动态：

1. **繁荣期**：  
   - 信贷市场表现乐观，信用利差（credit spread）处于低位
   - 投资加速，经济增长强劲

2. **紧缩期**：  
   - 市场信心逆转，信用利差上升
   - 投资增速下降，GDP 增长放缓

---

这类模型表明：**即使基本面冲击是有限的**，若经济主体的信念具有**系统性偏差或过度反应**，也可引发与现实中“繁荣—紧缩”周期高度一致的宏观波动。
