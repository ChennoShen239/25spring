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

