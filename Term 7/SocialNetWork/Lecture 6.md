## 6.1 Diffusion
- disease
- ideas, basic information (know or not know)
- adopt a product or not
- shock, bankruptcy, etc.

**Griliches (1957): Hybrid Corn Diffusion**
![[Pasted image 20251021130536.png]]

> **一项新技术的采纳过程通常遵循一个S形的曲线，并且其扩散速度在不同地理区域是不同的，这主要是由经济因素决定的。**

## Bass Model
- A benchmark w/o explicit social structure
- 2 actions/states/behaviors 0 and 1
- $F(t)$ denotes the population who have adopted action $1$ at time $t$
	- so the whole population is normalized to $1$.
Let $p$ be the rate of spontaneous adoption, $q$ be the rate of imitation and suppose 
$$
\frac{dF(t)}{dt} =(p+qF(t))(1-F(t))
$$
and the solution is 
$$
F(t)=\frac{1-\exp(-(p+q)t)}{\left( 1+\frac{q}{p}\exp(-(p+q)t) \right)}
$$
**So how to get the S-shape?**
consider the different proportion $F(t)$
1. if $F(t)=0$, then $\frac{dF}{dt}=p$
2. if $F(t)=1$, then $\frac{dF}{dt}=0$
3. if $F(t)=\epsilon\in(0,1)$, then $\frac{dF}{dt}=(p+q\epsilon)(1-\epsilon)$

so initially, only the innovation $p$ matters, then $q$ takes over eventually slows down as $F(t)\to 1$

![[Pasted image 20251021131454.png]]

**How to get initial convexity?**
1. formally, we need 
$$
(p+q\epsilon)(1-\epsilon)>p
$$
and that is 
$$
p+q\epsilon -\epsilon p -q\epsilon^2 >p \implies q\epsilon>p\epsilon + q\epsilon^2 \implies q>p+q\epsilon
$$
holds for all $\epsilon>0$, so that is $q>p$

**Extension SIS model**
We have 2 states:
1. S: susceptible
2. I: infectious
> 在SIS模型中，一个“感染者 (I)”在使用或相信一段时间后，可能会放弃这个行为或观点，**重新变回“易感者 (S)”**。这个过程通常被称为 **“恢复”（Recovery）**


## 6.3 Random Networks and Diffusion
- Ideas spread via connections in the network
- nodes are linked if one would *infect* the other
- Will an infection take hold?
- How many nodes will it reach?

**Extent of diffusion**
1. Some one in the giant component is infected $\implies$ non-trivial diffusion
2. Size of the giant component $\implies$ likelihood of diffusion and its extent

**A Erdos-Renyi Framework**
Consider a network with $n=50$ nodes, let the link probability be $p=0.03$ :
![[Pasted image 20251021133048.png]]

> .02 is the threshold for emergence of cycles and a giant component

or $p=0.1$:
![[Pasted image 20251021133113.png]]

>.08 is the threshold for connection

*Size of the Giant Component*
- How big is it if there's one?

So the key is to recall the threshold functions:
1. If $p< \frac{1}{n}$, then the network is too isolated that the infection won't spread.
2. If $p> \frac{\log n}{n}$ then it should be all connected
>换句话说，巨型组件的大小约等于 $n$，它包含了网络中所有（或几乎所有）的节点。

So the key is to evaluate the case when 
$$
\frac{1}{n} < p< \frac{\log n}{n}
$$
*Calculation (Cohen et al. 2000)*
- Let $q$ be the fraction of nodes in the largest component
- so for **a single node**, the chance that it is in the giant component is $p$
**Observation**: a node is outside of the gc $\iff$ all of its neighbors are outside of the gc
- We have 
$$
\begin{align}
\Pr \{ i \text{ is not in gc} \} & =1-q \\
 & =\Pr \{ \text{all neighbors of } i \text{ not in gc} \} \\
 & =(1-q)^d
\end{align}
$$
where $d$ is the node $i$ 's  degree

Let $P(d)$ be the prob. that  **the node has $d$ neighbors** then we basically have this weighted average:
$$
1-q = \sum_{d} (1-q)^{d}P(d)
$$
and then we can solve for $q$

![[Pasted image 20251021140252.png]]

Let's now try to solve it!
Given the ER network, we have 
$$
P(d)= \frac{[(n-1)p]^{d}}{d!}\exp(-(n-1)p)
$$
which is a Poisson distribution, so the equation becomes:
$$
\begin{align}
1-q  & =\sum \frac{[(n-1)p]^{d}}{d!}\exp(-(n-1)p) (1-q)^d \\
 & =\exp(-(n-1)p) \sum \frac{[(n-1)p]^{d}}{d!}(1-q)^d \\
 & =\exp(-(n-1)p) \sum \frac{[(n-1)p(1-q)]^{d}}{d!}
\end{align}
$$
we approximate $e^x \approx \sum \frac{x^{d}}{d!}$, so the latter term becomes:
$$
\sum_{d=1}^{\infty} \frac{[(n-1)p(1-q)]^{d}}{d!} = \exp((n-1)p(1-q))
$$
and thus:
$$
1-q = \exp(-(n-1)p) \times \exp((n-1)p(1-q))=\exp(-(n-1)pq)
$$
or that is, by taking log:
$$
-(n-1)pq=\log (1-q)\implies -\frac{\log(1-q)}{q}=(n-1)p =\mathbb{E}[d]
$$

**Lesson**: giant component fraction, 𝑞, only depends on *expected degree*, $\mathbb{E}[d]$!!!

![[Pasted image 20251021141812.png]]


**Who is infected?**
probability of being in the giant component *for a node with $d$ neighbors*:
$$
1-(1-q)^{d}
$$
is increasing in $d$.
- SO **more connected, more likely to be infected**

## 6.5 Extensions
How to capture the following?
1. Immunity:
	1. delete a fraction of nodes and study the GC on remaining nodes
2. Probabilistic Infection
	1. Have some links fail, just lower $p$

>[!immunity]
>- **建模策略：“删除一部分节点，然后研究剩下节点的巨型组件”**
>     
>     - **为什么这个策略有效？** 一个免疫的节点，对于正在传播的特定“病毒”来说，就相当于从网络中消失了。它既不能接收，也不能转发。因此，最直接的模拟方法就是**将这些节点以及与它们相连的所有边从网络中彻底移除**。
>         
>     - **核心研究问题：** 当我们随机移除（或根据策略移除）一定比例的节点后，剩下的网络会变成什么样子？特别是，**剩下的网络中还存在巨型组件吗？**
>         
>     - **关键洞见——“群体免疫”的理论基础：** 这正是**群体免疫 (Herd Immunity)** 的核心网络科学原理。你不需要让100%的人都免疫。你只需要移除足够多的节点，以至于剩下的节点网络变得支离破碎，其平均连接数低于临界阈值，导致**巨型组件瓦解**。一旦巨型组件不复存在，任何新的感染都只会在孤立的小群体中传播几步，然后就会自行消亡，无法形成大规模流行病。
>         
>     - **结论：** 免疫（疫苗接种）的威力不仅仅在于保护了个体，更在于它通过**破坏网络的连通性**来保护整个社群。
>         


> [!prob]
>- **现实世界中的含义：**
>     
>     - **疾病：** 你接触了一个流感病人（你们之间存在连接），但由于你的免疫系统、通风条件好、接触时间短等原因，你**不一定**会被感染。传播是有一定概率的，而不是100%确定的。
>         
>     - **社会行为：** 你的朋友向你推荐了一首歌（存在连接），但你可能没看到他发的朋友圈，或者你就是不喜欢这种风格。这条信息的“连接”存在，但“传播”失败了。
>         
> - **建模策略：“让一些连接失效，效果等同于降低 p”**
>     
>     - **为什么这个策略有效？** 如果每次接触的传播概率不是100%，而是某个概率 β（比如 β=25%），那么我们可以想象在一个新的“有效网络”上进行传播。这个有效网络只包含那些“成功实现传播”的连接。
>         
>     - **具体操作：** 想象一下原始的社交网络。我们现在遍历每一条连接（边），然后“掷硬币”。每一条边有 β 的概率被保留下来，有 1-β 的概率被临时删除。最终，只有那些被保留下来的边才能传播病毒。
>         
>     - **与 p 的关系 (这是最巧妙的部分)：** 你的笔记中提到“just lower p”。这里的 p 指的是我们在E-R随机网络模型中定义的“任意两节点间存在连接的概率”。
>         
>         - 在一个原始网络中，平均每个人的朋友数（平均度）大约是 c = np。
>             
>         - 现在，如果每条连接都只有 β 的概率是有效的，那么**有效的平均朋友数**就变成了 c_effective = (np) * β = n(pβ)。
>             
>         - 这在数学上，**完全等同于**我们从一开始就用一个更小的连接概率 p' = pβ 来构建一个全新的、更稀疏的随机网络。
>             
>     - **结论：** 降低传播效率的措施（比如戴口罩、保持社交距离、洗手），其作用就是降低了传播概率 β。这相当于**削弱了网络的有效连接密度**。如果我们将 β 降得足够低，使得有效平均度 c_effective 降到临界阈值1以下，那么即使在原始网络中存在巨型组件，在**有效传播网络**中，巨型组件也会消失，从而阻止大规模流行。