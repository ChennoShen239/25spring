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
