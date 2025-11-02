## 7.1 The wisdom of the crowd
Question: *how to weight an Ox?*
Key to the wisdom:
1. diverse opinions from many people
2. no systematic biases
3. proper aggregation of the opinions

## 7.2 Herd Behavior
Shows in:
1. purchasing decisions
2. job search
3. opinion formation 

**Modelling Herd Behavior**

(Banerjee-1992, Bikhchandani-et-al-1992)
1. there are 2 restaurants A and B
2. $n$ tourists want to find the better one to dine in
	1. each gets a signal $a,b$ about which one is better
	2. arrive sequentially $1,2,3\dots$
	3. makes the choice upon arrival
		1. so that they make decisions based on *signal* and *other's actions*
---
suppose the $1$ st and the 2nd tourists choose A
- for $1$, he must gets $a$
- for $2$, we have prior distribution $$
\Pr \{ s_{2}=a \}=\Pr \{ s_{2}=b \}=\frac{1}{2}
$$and then given $a_{2}=A$, we have $$
\Pr\{ s_{2}=a|a_{2}=A \}= \frac{\Pr\{s_{2}=a,a_{2}=A \}}{\Pr \{  a_{2}=A \}}=\frac{\Pr\{ a_{2}=A|s_{2}=a \}\Pr\{ s_{2}=a \}}{\Pr\{ a_{2}=A \}}
$$and $\Pr \{ a_{2}=A \}=\frac{1}{2}+\frac{1}{2} \times \frac{1}{2}=\frac{3}{4}$, so we have $$
\Pr\{ s_{2}=a|a_{2}=A \}=\frac{1}{2} \times \frac{4}{3}=\frac{2}{3}
$$
*now* you are the $3$rd tourist. 
- if $s_{3}=a$, then it's optimal to go to $A$
- if $s_{3}=b$, then consider the signal of the 3 people:
	- $\Pr \{ s=aab \}=\frac{2}{3}$
	- $\Pr \{ s=abb \}=\frac{1}{3}$
	- so it's probable that the signals are $aab$ and therefore you *should* choose $A$ too!

> [!corollary]
> **推论（后续所有人）：**
> 
> 一旦出现“**前两人做出同样选择**”这种公开证据，它就相当于形成了**足以压过任何一个人的单独私有信号**的公共信息优势。于是第 3 人开始无视自己的信号跟随 A第 4、5… 个看到连续 A 更会跟随，如此形成**羊群效应/信息瀑布**：大家都选 A，逐步忽视各自的私有信息。

so consequently, behaviors/beliefs might be *manipulated*
- shill 托
## 7.3 Sequential vs. Repeated Learning

- Sequential learning 
	- often from *others' actions*
	- Key: each agent acts only *once*
	- Often follows *Bayes' rule*
- Repeated Learning
	- linear, reduced form, updating *DeGroot*
	- Bayesian Updating.

## 7.4 DeGroot 1974 social learning model
- Individuals $\{ 1,2,\dots,n \}$
- $T$ denotes the *weighted directed* network, which is a *row-stochastic* matrix
	- so $T=(T_{ij})_{n\times n}$ where $T_{ij}\in [0,1]$ is the weight of how $i$ believes in $j$ and $\sum_{j=1}^{n}T_{ij}=1,\forall i$
>行随机确保每次更新都是凸组合，所以每个 $b_{i}(t)$ 始终介于邻居上一期信念的范围内。
- Start with initial beliefs $\vec{b}(0)=[b_{i}(0) \in[0,1]]$
- and the update process is $$
\vec{b}(t)=T \vec{b}(t-1)
$$or $$
b_{i}(t)=\sum_{j=1}^{n} T_{ij}b_{j}(t-1)
$$
> note that one repeatedly average beliefs of self with neighbors

---
**one example of this**
we have $$
T=\begin{bmatrix}
\frac{1}{3} & \frac{1}{3} & \frac{1}{3} \\
\frac{1}{2} & \frac{1}{2} & 0 \\
 \frac{1}{2} & 0 & \frac{1}{2}
\end{bmatrix}
$$and the network is:
![[Pasted image 20251102184652.png]]

---

## 7.5 Convergence

Q: *will beliefs converge?*

**Definition** $T$ converges if $\lim_{ t \to \infty }T^{t}b$ exists for all $b$

- $T$ is aperiodic if the *greatest common divisor of its cycle lengths* is $1$
	- formally, we define $$
\mathrm{per}(i)=\gcd\{t\ge1:\ (T^{t})_{ii}>0\},
$$which is the *gcd* of lengths of the walk from $i$ to $i$.

*Suppose $T$ is strongly connected:*
- that is, there exists a path from every $i$ to every $j$
*$T$ is convergent $\iff$ it's aperiodic*
and moreover:
*$T$ is convergent $\iff$ there exists a consensus*


**What if the network is not strongly connected?**
- Break into *closed* communicating classes and
- study them
![[Pasted image 20251102190732.png]]
> DeGroot/马尔可夫视角看，这些是**吸收/回返**的“洼地”，信息一旦流入就出不去。

## 7.6 Consensus
*Suppose the process does converge*
- Does everyone reach the same ending belief?
E.g. for a network $$\begin{aligned}
T = \begin{pmatrix}
0 & 1/2 & 1/2 \\
1 & 0 & 0 \\
0 & 1 & 0
\end{pmatrix}
\end{aligned}$$
we have $$
T^{\infty}=
\begin{pmatrix}
2/5 & 2/5 & 1/5 \\
2/5 & 2/5 & 1/5 \\
2/5 & 2/5 & 1/5
\end{pmatrix}
$$
Q: what's $1$'s ending belief?
A: the ending belief is $\frac{2}{5}b_{1}(0)+\frac{2}{5}b_{2}(0)+\frac{1}{5}b_{3}(0)$
And that holds for *all others!*
**Consensus:** everyone ending up with the same conclusion *regardless* of their initial beliefs.

## 7.7 Limiting Beliefs?

**Consensus:** The rows of $T^{t}$ converge to the same row vector 

Q: What's the *consensus* and *who are the influential agents* in terms of steering the limiting belief?

**Influence Measure**
- Looking for a row vector $s$ that $\lim_{ t \to \infty }T^{t}b(0)=\vec{1}sb(0)=b(\infty)$

即**所有人收敛到同一个数**，这个数就是初始信念的 **s-加权平均**。 于是把 s 解释为：**每个体对长期共识的相对影响权重**（$s_{i}$ 越大，个体 i 的长期影响越强）

Then note that $$
\begin{align}
\lim_{ t \to \infty } T^{t}b(0) & =\vec{1}sb(0)
 \\
 & =\lim_{ t \to \infty } T^{t+1}b(0) = \vec{1}sTb(0)
\end{align}
$$that is $$
sb(0)= sTb(0)
$$
holds for all $b(0)$. So we have $$
s=sT
$$所以 $s$ 是 $T$ 的左特征向量，特征值为 1（也叫平稳分布）：$s^\top$ 满足 $T^\top s^\top = s^\top$。

**So who has influence?**
- High influence from being paid attention to by people with *high influence*
- Power measures
**Example 1. Stubborn Agents**
1. An agent who places *high* weight on *self* will maintain belief while others *converge* to that agent’s belief
2. Similarly, groups that are highly *introspective* will have substantial influence.
	- 若一组节点 $S$ 内部互相赋权高、对外赋权低（“内省”），对应矩阵的 $S \times S$ 子块近似行和为 1、指向外部的权重很小。马尔可夫/DeGroot 视角下，$S$ 近似封闭类（near-closed class），信息一旦进来就不怎么流出。
	- 结果：这组的总影响 $\sum_{i \in S} s_i$ 很大；外部节点长期会被拉向 $S$ 的组内共识。若 $S$ 完全封闭且原始，组内一定形成共识，外部节点的极限是这些封闭类共识的概率加权

**Example 2. Equal Weighting**
Let $A$ be an undirected network, representing connections, suppose equally weight across one's neighbors:
- Let $d_{i}$ be $i$ 's out degree in $A$
- then $T_{ij}=\frac{1}{d_{i}}$ holds for all $(i,j)\in \{ 1,2,\dots,n \}\times \{ 1,\dots n \}$
*That is, learn from friends and weight them all equally*.

---
So who has influence in this case?
- Let $D=\sum_{k=1}^{n}d_{k}$ be the total degree
**Claim:** Influence $s_{i}=\frac{d_{i}}{D}$ for each $i$
*Proof*. we need to verify $$
s=sT
$$and in this case it's 
$$
s_{i}=\sum_{j=1}^{n} s_{j}T_{ji}
$$
so we have 
$$
\begin{align}
s_{i}=\sum_{j=1}^{n} s_{j}T_{ji} & =\sum_{j=1,T_{ji}>0}^{n} \left( \frac{d_{j}}{D}  \right)\left( \frac{1}{d_{j}} \right) \\
 & =\sum_{j=1,T_{ji}>0}^{n} \frac{1}{D} \\
 & = \frac{d_{i}}{D}=s_{i}
\end{align}
$$
## 7.9 Wise in DeGroot Learning>
**Uncertainty Structure**
- Suppose true state is $\mu$
- Agent $i$ sees $b_{i}(0)=\mu+\epsilon_{i}$
	- where $\epsilon_{i}$ is drawn from a bounded mean-zero distribution
- Signal distributions may differ across agents but are *independent conditional on $\mu$*

Consider large societies:
- if they pooled their information, they would have an accurate estimate of $\mu$
>[!LLN]
>如果把所有信息直接汇总成均值$\bar{b_{n}}=\frac1n\sum_ib_i(0)$,则
$$\mathbb{E}[\bar{b}_n]=\mu,\quad\mathrm{Var}(\bar{b}_n)=\frac1{n^2}\sum_i\mathrm{Var}(\varepsilon_i)\leq\frac{\sigma_{\max}^2}n\to0,$$
大数定律$\Rightarrow\bar{b}_n\to\mu$。这说明：人数越多，潜在上可以任意接近真值。

**Wise** consider a sequence of societies $$
T,T^2,\dots T^{(n)},\dots
$$
*Wise* if consensus in $T^{(n)}$ converges to the truth as $n\to \infty$

Then is a society wise?
把长期共识写成
$${\rm Consensus} = \mu + \underbrace{ \sum_{i=1}^{n} s_i^{(n)} \varepsilon_i }_{ W_{n} },$$

其中 $s^{(n)} = (s_1^{(n)}, \ldots, s_n^{(n)})$ 是第 $n$ 个社会的影响力权重 $(s_i^{(n)} \geq 0, \sum_i s_i^{(n)} = 1)$, $\varepsilon_i$ 为零均值、相互独立、方差有界且下界 $\sigma_{\min}^2 > 0$ 的误差。

*社会 wise 就是 $W_n \xrightarrow{p} 0$（共识以概率收敛到真值 $\mu$）。*

That is $$
W_n\xrightarrow{p}0\quad\Longleftrightarrow\quad\max_is_i^{(n)}\to0.
$$
Wise crowds $\iff$ max influence vanishes.

**Eg.1 No opinion leaders**
Recall $s_{i}=\sum_{j=1}^{n}T_{ji}s_{j}$
- If there is some $i$ w/ $$
T_{ji}>a>0
$$for all $j$, then $s_{i}>a$
- so can't have too strong an *opinion leader*
>[!Note]
>**直觉**
> 
> 每个人都至少拿出$a$的注意力给同一个人$i$。不管社会多大，这个人的噪声/偏见都会以至少$a$的权重进入最终共识，噪声无法被“摊薄”。
> 
> “**现实吗**？”
> 
> 很多场景是现实的：大众媒体/平台、统一的信息源(搜索引擎首页、算法推荐流)等—大家都固定给它一部分权重。于是只要该源带有偏见，偏见会传染给所有人，整体就难以达到“群体智慧”。

**Eg.2 Reciprocal Attention**
- Suppose that $T$ is column stochastic
	- so each agent also receives weight one
- Then $s=\frac{1}{n}\vec{1}$ is a unit  LHS eigenvector, and so $T$ is wise
- so *reciprocal trust implies wisdom*

## BACKUP

> [!notes]
> # 幻灯片解释（一）：收敛速度、同质相吸与谱分解
> 
> 这些页主要在讲：**DeGroot 型学习的“收敛速度”如何由“同质相吸（homophily）”决定**，以及用**谱分解**看“稳态＋偏离”的衰减。
> 
> ---
> 
> ## 1) 关注的问题：沿途会发生什么？
> - 不只是“最终会不会共识”，还关心：
>   - **收敛速度**快不快？
>   - **中途**各个体的估计长什么样？
>   - **哪些网络结构**让它快/慢？
> 
> ---
> 
> ## 2) 同质相吸（Homophily）如何影响速度？
> - **定义**：人更倾向于和“相似的人”互动（同群体内连边概率高，跨群体低）。
> - **直观结论（Golub–Jackson, *QJE* 2012）**：**同质相吸会减慢共识的收敛**。
>   - **组内**容易先达成一致；
>   - **跨组**交流稀疏 ⇒ 信息在不同群体之间“混合”慢 ⇒ 整体共识拖很久，常出现**长期多意见集团**。
> - 他们还发现：总体边的**密度**不是决定因素；关键是**跨组交往的相对频率**。组内再密，若跨组桥接弱，混合仍慢。
> 
> ---
> 
> ## 3) 形式化结果（QJE 2012 的要点）
> - 多类型随机图（近似 SBM）设定：类型集 $\mathcal G$，连边概率矩阵 $P=(p_{ab})$，每组规模 $n_a$。学习矩阵 $W=D^{-1}A$（等权平均）。
> - 定义**组级转移矩阵**：
>   $$
>   F_{ab}=\frac{n_b\,p_{ab}}{\sum_c n_c\,p_{ac}}.
>   $$
> - 结论：在规模足够大、各组不消失且密度可比的条件下，
>   $$
>   \lambda_2\big(W\big)\ \approx\ \lambda_2\big(F\big)
>   $$
>   以高概率成立。**收敛快慢主要由“组与组如何相连”的粗粒度结构决定**。
> - **速度与特征值**：对行随机 $W$，$\lambda_1=1$，其余 $|\lambda_i|<1$。
>   $$
>   \|b(t)-\mathbf 1(s^\top b(0))\|\ \lesssim\ C\,|\lambda_2|^{\,t}.
>   $$
>   同质相吸越强 ⇒ $|\lambda_2|\to1$ ⇒ **越慢**。
> 
> ---
> 
> ## 4) 谱分解视角：稳态 + 偏离
> - **谱分解**：
>   $$
>   W^{t}=\sum_{i=1}^{n}\lambda_i^{\,t}\,P_{\lambda_i},
>   $$
>   其中 $\lambda_1=1$，$P_{\lambda_i}$ 是对应投影。
> - **含义**：
>   - $P_{\lambda_1}$ 给出**稳态**（$W^\infty=\mathbf 1 s^\top$）。
>   - 其余项是**偏离模式**，按 $|\lambda_i|^t$ 指数衰减；主导项是 $\lambda_2$。
> 
> 
> ---
> 
> # 幻灯片解释（二）：经验证据——DeGroot vs Bayes
> 
> 主题：**现实中，人们到底按哪种规则在网络里学习？**对比 **DeGroot（线性加权平均）** 与 **Bayes（贝叶斯理性）**，并给出两篇实证/实验结果。
> 
> ---
> 
> ## DeGroot vs. Bayes：各自优缺点
> - **DeGroot**：$b(t+1)=T\,b(t)$；**可解、可估**（共识、影响力、速度都清楚）；**缺点**：非理性（重复计数、相关性处理粗糙）。
> - **Bayes**：规范最优；但在网络中**计算与信息需求极高**（需追踪相关性与路径），全理性难以实现。
> - **经验问题**：现实行为**更像哪一种**？
> 
> ---
> 
> ## Chandrasekhar–Larreguy–Xandri（Econometrica 2020）
> - **混合模型**：部分个体**贝叶斯**，部分**DeGroot/线性启发式**。
> - **识别/估计**：结合**结构估计**与**约简式**证据，在实验室与田野测。
> - **发现**：
>   - 现实中**确为混合型**；
>   - **贝叶斯型比例因情境而变**：田野（印度村民）≈ **10%**；实验室（墨西哥大学生）≈ **50%**。
> - **含义**：单一模型难以解释；**行为–理性并存**更贴近数据（受任务复杂度、教育、激励等影响）。
> 
> ---
> 
> ## Grimm–Mengel（JEEA 2020）
> - **结果**：
>   1. **网络结构信息**本身会影响正确率（知道全局结构会改变行为与结果）——与**纯 DeGroot**不符（只看本地权重）。
>   2. **完全贝叶斯**在拟合数据上**不如 DeGroot**（过度理性假设与现实偏离）。
>   3. 个体会**折扣相关信息**，但方式**粗糙/启发式**，非严格贝叶斯权重。
> - **含义**：现实行为介于 DeGroot 与 Bayes 之间：能感知相关性与结构，但不做最优计算。
> 
> ---
> 
> ## Learning: Summary（理论诊断表）
> - **极限**：
>   - 是否**收敛/共识**？
>   - **谁有影响力**（左特征向量 $s$）？
>   - 有真值时，是否**趋真（wise）**（$\max_i s_i\to0$）？
> - **沿途**：
>   - **速度**由第二特征值模 $|\lambda_2|$ 控制（谱隙越大越快）。
>   - **偏差/异质**：哪些节点先靠拢、哪些滞后（由特征向量与路径权重决定）。
> 
> ---
> 
> ## Social Learning Models：小结
> - **DeGroot/近视型**：
>   - **优点**：把网络纳入核心；可达成共识、可（在条件下）wise；影响力与速度**可刻画可估计**。
>   - **缺点**：**不完全理性**；易出现羊群、极化、意见领袖支配等偏差。
> - **Bayesian（规范）**：
>   - **优点**：避免重复计数，理论最优。
>   - **缺点**：在网络中**计算要求极高**；很多“受限贝叶斯”版本让**网络作用变弱**或近似均值化。
> 
> ---
> 
> ## 总体 Takeaways
> 1. **现实不是纯 DeGroot，也不是纯 Bayes**：更像**混合/启发式+部分理性**。
> 2. **网络结构信息**确实影响正确率与收敛路径（支持“网络很重要”）。
> 3. **相关性折扣**存在但非最优 ⇒ 需要容纳“近似理性”的模型。
> 4. 实证建议：估计**混合份额**（Bayes vs DeGroot）、加入**相关性折扣参数**与**网络认知误差**；用谱指标（$|\lambda_2|$、$s_{\max}$）预测速度与明智性并与数据校验。

