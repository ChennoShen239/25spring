# Lecture 5: Strategic Network Formation Models

## 5.1 JW 96
Let  $u_{i}(g)$ be the payoff to $i$ if the network is $g$
- undirected network formation
Consider a game
- each agent announces who they wish to link
- a link forms iff both name each other
Nash Eq.
- no agent can gain from changing their action
Consider a formation game w/ 2 agents![[Pasted image 20251020204611.png]]
- 2 equilibria!
## 5.2
**Pairwise Stability**
1. No single agent gains from severing a link – relationships must be beneficial to be maintained
2. No pair of agents both gain from adding a link (at least one strictly) – beneficial relationships are pursued when available

*Notation*:
For a network $g$:
- $g-ij$ is the network where $ij$ is **removed**
- $g+ji$ is the network where $ij$ is **added**
So the definition becomes:
1. $u_{i}(g)\ge u_{i}(j-ij)$ for $i$ and $ij$ in $g$
2. $u_{i}(g+ij)>u_{i}(g)\implies u_{j}(g+ij)<u_{j}(g)$ for $ij$ not in $g$
>a weak concept, but often narrows things down

![[Pasted image 20251020205033.png]]

*Example: Coauther JW96*
Agents get value form collaboration:
- let $d_{i}$ be the time that $i$ spend on the paper
- then $$
u_{i}(g) =\sum_{j:ij\in g}^{n} \left[ \frac{1}{d_{i}}+\frac{1}{d_{j}}+\frac{1}{d_{i}d_{j}} \right]=1+\sum_{j:ij\in g}^{n} \left[ \frac{1}{d_{j}}+\frac{1}{d_{i}d_{j}} \right]
	$$where $d_{i}$ is the degree of a node $i$
- no direct costs to links

Consider the $n=4$ game:
![[Pasted image 20251020205420.png]]

Only the last one is **Pairwise Stable**

## Efficiency
*Pareto Efficient*
A network $g$ is Pareto efficient iff there doesn't exist $g'$ such that $$
u_{i}(g')\ge u_{i}(g)
$$for all $i$ and the inequality holds strictly for some $i$
*Efficient*
A network $g$ is efficient iff $g$ maximized $\sum_{i=1}^{n}u_{i}(g)$

So in the previous case:![[Pasted image 20251020210230.png]]

And there are some additional structures:
![[Pasted image 20251020210852.png]]


*Externalities*
- Negative externality:$$
u_{k}(g+ij)\le u_{k}(g)
$$for some $k\neq i,j$
- Positive externality:$$
u_{k}(g+ij)\ge u_{k}(g)
$$for some $k\neq i,j$
> An example of pos. ext. is connections model in JW 96

## 5.4 Network Formation and Transfers

**What are transfers**
- Outside intervention, taxing or subsidizing relationships
	- e.g., government support of RD relationship
- Bargaining among the individuals involved in the relationships
- Favors exchanged among friends….

**Formally**
Change utilities from $u_{i}(g)$ to $u_{i}+t_{i}(g)$
> e.g. Tax on having more than one link

*Egalitarian Transfers*
- Let the tax be $$
t_{i}(g) = \sum_{j=1}^{n} \frac{u_{j}(g)}{n}-u_{i}(g)
$$then $$
u_{i}(g) +t_{i}(g)=\sum_{j=1}^{n} \frac{u_{j}(g)}{n}
$$So that **every agent has societal incentives**


**Basic Requirements on Transfers**
1. completely isolated nodes that generate no value get $0$
2. Nodes that are completely interchangeable get same transfers

![[Pasted image 20251020234615.png]]

**This is not an eq w/ transfer cause**:
The node with payoff of 5 can always sever a link and get a higher payoff $6>5$

*Coase Theorem*:
w/o frictions, transfers can solve inefficiencies:
> "A theory is not like an airline or bus timetable. We are not interested simply in the accuracy of its predictions. A theory also serves as a base for thinking. It helps us to understand what is going on by enabling us to organize our thoughts.”
>
>—Ronald Coase

- transfers fail to lead to efficiency…
- What's special here?
	- Combination of *multiple externalities* that all need to be handled at once

>[!note]
>在网络形成的过程中，任何一个连接的建立或切断，都会同时对网络中的许多其他个体产生各种复杂且相互关联的影响（既有正面的也有负面的）。这些影响不能被单独、依次地解决，而必须作为一个整体系统被同时考虑和处理，这使得通过简单的协商或补偿来达到整体效率变得极其困难。

## 5.5 Pairwise Nash Stability

Recall the announcement game:
- Agents simultaneously announce their preferred sets of neighbors $S_{i}$
- The map is $$
g(S)=\{ ij|i\in S_{j} \cap j\in S_{i} \}
$$
*Nash Stability*
Formally, $$
u_{i}(g(S))\ge u_{i}(g(S_{i}',S_{-i})) \forall i,S_{i}'
$$that is, no agent strictly benefits any alternative announcement $S_{i}'$
*Proposition*: $g$ is Nash stable iff no agent wants to delete **some set of** their links.

![[Pasted image 20251021003001.png]]

>[!Why is the NW one not NS?]
>当前状态：中间的行动者连接着另外两个人，他的收益是 -1。另外两个人的收益也是 -1。分析中间的行动者：他目前的收益是 -1。如果他切断与右边那个人的连接：网络会变成右下角的“一条连接和一个孤立点”的状态。在这种新状态下，他（作为连接的一端）的收益会变成 1。比较：因为 1 > -1，他有非常强烈的动机去单方面**切断**一条连接。
>
>**结论**：因为存在一个行动者可以通过单方面行动来提高自身收益，所以这个“V”字形网络不是纳什稳定的。


*Pairwise Nash stable*
Pairwise Nash stable = both pairwise stable and Nash stable
>Captures multiple link changes (deletion)

---
## Backup

### An improving path JW02
- change one link at a time
- sequence of adjacent networks
	- link is added **if it benefits both agents** and at least one strictly
	- Link is deleted **if either agent benefits from its deletion**
![[Pasted image 20251021104526.png]]

> Pairwise-Nash stable networks are in the red area.

### Stochastic Stability

-  Add trembles/errors to improving paths
- Start at some network and randomly choose a link to action upon:
	- add a link if both prefer and at least one strictly
	- delete a link also 
	- **reverse  the decision with prob**. $\epsilon>0$
	- **This is the so called trembles/errors**

This ends up a **finite state, irreducible and aperiodic Markov Chain** 
- So it has *stationary distribution*

So in the above example, let the state be $s=$ # of links and $$
\Pi(\varepsilon)=
\begin{pmatrix}
1-\varepsilon & \varepsilon & 0 & 0 \\
\frac{1-\varepsilon}{3} & \varepsilon & \frac{2(1-\varepsilon)}{3} & 0 \\
0 & \frac{2\varepsilon}{3} & \frac{2-\varepsilon}{3} & \frac{1-\varepsilon}{3} \\
0 & 0 & \varepsilon & 1-\varepsilon
\end{pmatrix}.
$$
to see this, let $\pi_{ij}=\Pr \{ s_{t}=j|s_{t-1}=i \}$ be the $(i,j)$ entry of $\Pi(\epsilon)$, then for the 
1. 1st row: only form one link if the decision is reversed: $\pi_{12}=\epsilon$
2. 2nd row: w/o error, go to $s=0$ w/ prob. $\frac{1}{3}$ and go to $s=2$ w/ prob. $\frac{2}{3}$, w/ error delete the decision so state at $s=1$ w/ prob. $\epsilon$
3. 3rd row: chooses one link:
	1. if it's the existing link, then it's optimal to do nothing and go to $s=1$ with prob. $\frac{2\epsilon}{3}$
	2. if is's the link that doesn't exist the it's optimal to add it and go to $s=3$ with prob. $\frac{1-\epsilon}{3}$
	3. then stay at $s=2$ with prob. $1-\frac{2\epsilon}{3}-\frac{1-\epsilon}{3}=\frac{2-\epsilon}{3}$
4. 4th row: stay at $s=4$ w/0 error and prob. $1-\epsilon$

The stationary distribution is 
$$\mu(\varepsilon) = \left( \frac{\varepsilon(1-\varepsilon)}{1+2\varepsilon}, \frac{3\varepsilon^2}{1+2\varepsilon}, \frac{3\varepsilon(1-\varepsilon)}{1+2\varepsilon}, \frac{(1-\varepsilon)^2}{1+2\varepsilon} \right)$$
and we can see that $$
\lim_{ \epsilon \to 0 } \mu(\epsilon)=(0,0,0,1)
$$so **完全网络**被定义为这个模型中**唯一的“随机稳定” (Stochastically Stable) 状态**

>[!Why not the same for the two PNS?]
>- 既然两个都是稳定的，为什么在引入“微小错误”并取极限后，只有“完全网络”活了下来，而“空网络”的概率变成了0？
>     
> - **答案**：**“逃离”这两个稳定状态的“成本”（所需的错误数量）是不同的。**
>     
>     - **逃离“空网络” (状态0)**：
>         
>         1. 你只需要犯**一次错误**：以 $\epsilon$ 的概率非理性地“增加”一条连接，进入状态1。
>             
>         2. 一旦到了状态1，**理性**的“改善路径”（概率 $1-\epsilon$）就会接管，把你推向状态2，然后再推向状态3。
>             
>         3. 所以，逃离“空网络”这个吸引盆地，**只需要1次错误**。这个逃离事件的发生概率与 $\epsilon^1$ 成正比。
>             
>     - **逃离“完全网络” (状态3)**：
>         
>         1. 你需要犯**一次错误**：以 $\epsilon$ 的概率非理性地“删除”一条连接，进入状态2。
>             
>         2. **但是**，一旦到了状态2，**理性**的“改善路径”会立刻把你**推回**状态3！
>             
>         3. 为了真正逃离并一路回到状态0，你必须在状态2时**再犯一次错误**（以 $\epsilon$ 的概率删除连接进入状态1），然后在状态1时**理性地**（或再犯一次错）删除连接进入状态0。
>             
>         4. 所以，逃离“完全网络”这个吸引盆地，**至少需要连续两次错误**。这个逃离事件的发生概率与 $\epsilon^2$ 成正比。
> 
> 
### Ideas
1. "More errors needed to leave the 'basin of attraction' of complete network than to leave the basin of attraction of empty network
2. More generally, need to keep track of basins of attraction of many states (via a theorem of Friedlin and Wentzel 1984)
