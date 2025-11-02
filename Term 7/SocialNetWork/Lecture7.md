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
1. An agent who places *high* weight on *self* will maintain belief while others converge to that

agent’s belief