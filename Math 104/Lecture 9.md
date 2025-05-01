# Lecture 9
>This the course note for math 104 chapter 9, which should be used together with [[Ch9.pdf]]

> [!PDF|yellow] [[Ch9.pdf#page=1&selection=23,0,23,19&color=yellow|Ch9, p.1]]
> > Riemann integrable
>
> Riemann 可积

> [!PDF|yellow] [[Ch9.pdf#page=1&selection=199,0,248,2&color=yellow|Ch9, p.1]]
> > Proposition 1.1. Suppose that f, g : A → R and f ≤ g. Then sup A f ≤ sup A g, inf A f ≤ inf A g.
>
> The function supremum and infimum keep the orders

> [!PDF|yellow] [[Ch9.pdf#page=2&selection=270,0,336,2&color=yellow|Ch9, p.2]]
> > Proposition 1.3. If f, g : A → R are bounded functions, then sup A (f + g) ≤ sup A f + sup A g, inf A (f + g) ≥ inf A f + inf A g.
>
> Essentially, this is just the definition

> [!PDF|yellow] [[Ch9.pdf#page=2&selection=464,0,537,1&color=yellow|Ch9, p.2]]
> > Proposition 1.4. If f, g : A → R are bounded functions, then sup A f − sup A g ≤ sup A |f − g|, inf A f − inf A g ≤ sup A f − g | .
>
> This is fun so let's do a little bit more about it:

first of all, the whole proposition should be like this:
If $f,g:A\to \mathbb{R}$ are bounded functions, then $$
\lvert \sup{f}-\sup{g} \rvert \leq \sup{\lvert f-g \rvert } \quad \lvert \inf{f}-\inf{g} \rvert \leq \sup{\lvert f-g \rvert }

$$
The proof of sketch is then basically:
1. given $f=f-g+g$, then
$$

\underbrace{ \sup{f} \leq \sup{f-g} + \sup{g} }_{ \text{prop. 1.3} } \leq \sup{\lvert f-g \rvert } + \sup{g}

$$
2. so we have
$$

\sup{f} - \sup{g} \leq \sup{\lvert f-g \rvert }

$$
3. it's easy to see if we exchange the $f$ and $g$, we can have
$$

\lvert \sup{f} -\sup{g} \rvert \leq \sup{\lvert f-g \rvert }

$$
4. replace $f$ by $-f$ and $g$ by $-g$, we have
$$

\lvert \sup{-f} -\sup{-g} \rvert =\lvert -\inf{f} + \inf{g} \rvert \leq \sup{\lvert f-g \rvert }

$$
which finishes the proof.

> [!PDF|yellow] [[Ch9.pdf#page=3&selection=258,0,340,0&color=yellow|Ch9, p.3]]
> > Proposition 1.5. If f, g : A → R are bounded functions such that |f (x) − f (y)| ≤ |g(x) − g(y)| for all x, y ∈ A, then sup A f − inf A f ≤ sup A g − inf A
>
> This one is similar to the Lipschitz condition , so the basic idea is to let the RHS:
$$\lvert g(x) - g(y) \rvert \leq \sup{g} - \inf{g}$$

> then we'll have the whole inequality by just the definition of supremum

Don't be so impatient. Let's go through the proof again:

since for all $x,y \in A$, we have $$
\lvert f(x) - f(y) \rvert \leq \lvert g(x) - g(y) \rvert
$$
then given $$
\lvert g(x) -g(y) \rvert  \leq \sup{g} - \inf{g} \equiv \text{osc}  g
$$
so that $$
\text{osc} f \equiv \sup{f} - \inf{f}  =  \underbrace{ \sup_{x,y \in A}{\left\{ f(x) - f(y)  \right\} } \leq \sup{g} - \inf{g}  }_{ \text{sup preserves the order}  }\equiv \text{osc} g
$$

> [!PDF|red] [[Ch9.pdf#page=4&selection=6,29,6,45&color=red|Ch9, p.4]]
> >  almost disjoint
>
> They share no points or only one point

> [!PDF|yellow] [[Ch9.pdf#page=4&selection=24,0,50,1&color=yellow|Ch9, p.4]]
> > Definition 2.1. Let I be a nonempty, compact interval. A partition of I is a finite collection {I1, I2, . . . , In} of almost disjoint, nonempty, compact subintervals whose union is I.
>
> Note the partition is eventually by the end points and if we use end points to represent, then we'll have one more point than intervals.

To use the partitions, we need to memorize $$
P = \left\{ I_{1} , I_{2} ,\dots,I_{n} \right\}
$$
or $$
P = \left\{ x_{0}, x_{1}, x_{2},\dots ,x_{n} \right\}
$$
> [!PDF|yellow] [[Ch9.pdf#page=5&selection=101,0,220,1&color=yellow|Ch9, p.5]]
> > Definition 2.2. Define the upper Riemann sum of f with respect to the partition P by U (f ; P ) = nX k=1 Mk |Ik| = nX k=1 Mk (xk − xk−1) , and the lower Riemann sum of f with respect to the partition P by L(f ; P ) = nX k=1 mk |Ik| = nX k=1 mk (xk − xk−1) .
> 
> For the $U(f;P)$, we use the suprema $M_{k}$ and for the $L(f;P)$, we use the infima $m_{k}$

>[!Darboux Sum]
>We're actually studying something called the Darboux sum, not strictly Riemann sum. The key difference is we take upper and lower bounds for the Darboux sum but we take a $\xi_{k}$ in each $I_{k}$ for Riemann sum.

> [!PDF|red] [[Ch9.pdf#page=5&selection=327,27,361,1&color=red|Ch9, p.5]]
> > tegral of f on [a, b] by U (f ) = inf P ∈Π U (f ; P ).
> 
> Note that. we use the $\inf{}$  to set the $U$ and use $\sup{}$ to set the $L$

![[output 2.png]]
> [!PDF|yellow] [[Ch9.pdf#page=6&selection=0,15,48,12&color=yellow|Ch9, p.6]]
> > Definition 2.3. A function f : [a, b] → R is Riemann integrable on [a, b] if it is bounded and its upper integral U (f ) and lower integral L(f ) are equal. In that case, the Riemann integral of f on [a, b], denoted by
> 
> This definition comes from $U(f) =L(f)$

Note that if we say some integral is not defined as a Riemann integral, then it may be that:
1. The upper or lower Riemann sums of $f$ are not well-defined (has $\infty$ or $-\infty$)
2. The $f$ is so discontinuous that $U(f) \neq L(f)$.

> [!PDF|red] [[Ch9.pdf#page=7&selection=360,8,386,1&color=red|Ch9, p.7]]
> > n this example, the infimum of the upper Riemann sums is not attained and U (f ; P ) > U (f ) for every partition P .
> 
> We don't need the $U(f)$ to be attained by a particular $P$, we just know it's an infimum and that's enough

> [!PDF|yellow] [[Ch9.pdf#page=8&selection=0,0,63,68&color=yellow|Ch9, p.8]]
> > Example 2.5. The Dirichlet function f : [0, 1] → R is defined by f (x) = ( 1 if x ∈ [0, 1] ∩ Q, 0 if x ∈ [0, 1]\Q. That is, f is one at every rational number and zero at every irrational number.
> 
> This one is pretty famous! The key proof is to find that every interval $I_{k}$, one must have $M_{k} =1,m_{k} =1$, therefore the $U(f) = 1\neq L(f)=0$


> [!PDF|yellow] [[Ch9.pdf#page=8&selection=196,0,246,1&color=yellow|Ch9, p.8]]
> > Definition 2.4. A partition Q = {J1, J2, . . . , Jm} is a refinement of a partition P = {I1, I2, . . . , In} if every interval Ik in P is an almost disjoint union of one or more intervals Jℓ in Q.
> 
> Ok this one is pretty annoying, it's called 几乎不相交并 in Chinese, and the basic idea is that we add more separation points to the partition $P$

For a better understanding, the better way is to use the "endpoint" definition. $Q$ is a refinement of $P$ is $P \subset Q$.

> [!PDF|red] [[Ch9.pdf#page=8&selection=398,0,402,1&color=red|Ch9, p.8]]
> > Example 2.7. Given two partitions, neither one need be a refinement of the other. 
> 
> This one is fun, if we take all the separation points of the two, then we can get the smallest refinement

> [!PDF|yellow] [[Ch9.pdf#page=9&selection=4,0,82,1&color=yellow|Ch9, p.9]]
> > Theorem 2.1. Suppose that f : [a, b] → R is bounded, P is a partitions of [a, b], and Q is refinement of P . Then U (f ; Q) ≤ U (f ; P ), L(f ; P ) ≤ L(f ; Q).
>
> Let's dive into this one!

>[!Intuition]
>Intuitively, this means that if the interval $[a,b]$ is split into more sub intervals, then the upper sum will be smaller and closer to $U(f)$, and the lower sum will be greater and closer to $L(f)$.

*Proof*.
Let $Q$ be a refinement of $P$, and since $P=\left\{ I_{k} \right\}_{k=1}^{n},Q=\left\{ J_{k} \right\}_{k=1}^{m}$, so we have $m\geq n$, then we define $$
M_{k} = \sup_{I_{k}}{f} \quad M_{\ell}' = \sup_{J_{\ell}}{f}
$$
and $m_{k},m'_{\ell }$ follow. since $Q$ is a refinement of $P$, then we can write each interval $I_{k}$ in $P$ as an almost disjoint union of intervals in $Q$, i.e. $$
I_{k} = \sum_{\ell=p_{k}}^{q_{k}} J_{\ell}
$$
1. if $p_{k} = q_{k}$ then the $I_{k}$ is not more separated
2. otherwise the $J_{\ell}$s refine the $I_{k}$
so it's natural that $$
p_{1} = 1, p_{k+1} = q_{k} +1 ,q_{n} = m
$$
It's easy to see that $$
\underbrace{ \sum_{\ell=p_{k}}^{q_{k}} M_{\ell}'\lvert J_{\ell} \rvert \leq \sum_{\ell=p_{k}}^{q_{k}} M_{k} \lvert J_{\ell} \rvert  }_{ \text{by def. of supremum} }=M_{k} \lvert I_{k} \rvert 
$$
it follows that $$
U(f;Q) = \underbrace{ \sum_{\ell=1}^{m} M_{\ell}' \lvert J_{\ell} \rvert =\sum_{k=1}^{n} \sum_{\ell=p_{k}}^{q_{k}} M_{\ell}'\lvert J_{\ell} \rvert  }_{ \text{transform the partition from } Q\text{ to } P }\leq \sum_{i=1}^{n} M_{k}\lvert I_{k} \rvert =U(f;P)
$$
similarly we have the lower bound result since $$
\sum_{\ell=p_{k}}^{q_{k}} m_{\ell}'\lvert J_{\ell} \rvert \geq m_{k} \lvert I_{k} \rvert 
$$
> So natural, but you have to dive into the definition and represent the interval again.

> [!PDF|yellow] [[Ch9.pdf#page=10&selection=68,0,115,1&color=yellow|Ch9, p.10]]
> > Proposition 2.1. If f : [a, b] → R is bounded and P, Q are partitions of [a, b], then L(f ; P ) ≤ U (f ; Q).
> 
> The importance comes from that $P,Q$ are arbitrary

Later we use prop 2.1 to prove prop 2.2:
$$
L (f) \leq U(f)
$$ for all $f: \left[ a,b \right] \to \mathbb{R}$ 
The key idea is to use prop 2.1 for every 2 possible partitions in $\Pi$.

> [!PDF|yellow] [[Ch9.pdf#page=10&selection=376,0,438,4&color=yellow|Ch9, p.10]]
> > Theorem 3.1 (MOST USEFUL!). A bounded function f : [a, b] → R is Riemann integrable if and only if for every ϵ > 0 there exists a partition P of [a, b], which may depend on ϵ, such that U (f ; P ) − L(f ; P ) < ϵ.
> 
> So we can try to find the $P$ given $\epsilon$

>换言之：只要能够把**某个划分的上下黎曼和的差距做得足够小**，就可以断定该函数是黎曼可积的。这一判据在实际检验函数可积性时非常有效。

The proof in funnier on the converse side (integrable $\to$ Cauchy)
1. If $f$ is integrable, then given any $\epsilon>0$, we must have $Q,R$ such that $$
U(f;Q) < U(f) + \frac{\epsilon}{2} ,L(f;R) > L(f) - \frac{\epsilon}{2}
$$
2. then we take the common refinement of $Q,R$ ,that is, $P$, then we know $$
\underbrace{ U(f;P) - L (f;P) \leq U(f;Q) - L(f;R)  }_{ U(f;P) \leq U(f;Q),L(f;P) \geq L(f;R) } < \underbrace{ U(f) - L(f) + {\epsilon} = \epsilon }_{ f \text{ integrable} }
$$
> this is just theorem 2.1

> [!PDF|yellow] [[Ch9.pdf#page=11&selection=345,1,375,2&color=yellow|Ch9, p.11]]
> > efinition 3.1. The oscillation of a bounded function f on a set A is osc f A = sup A f − inf A f.
> 
> This is basically the definition of oscillation, but this is for a function $f$, not a Riemann sum


> [!PDF|yellow] [[Ch9.pdf#page=11&selection=520,18,534,21&color=yellow|Ch9, p.11]]
> > This is the case if we can find a sufficiently refined partition P such that the oscillation of f on most intervals is arbitrarily small, and the sum of the lengths of the remaining intervals (where the oscillation of f is large) is arbitrarily small.
> 
> We set the $I_{k}$ with large $\text{osc}_{I_{k}}f$ so small, that is, assign it with small $\lvert I_{k} \rvert$, then deal with the rest of $I_{k}$s easily

> [!PDF|yellow] [[Ch9.pdf#page=12&selection=0,0,62,14&color=yellow|Ch9, p.12]]
> > Proposition 3.1. Suppose that f, g : [a, b] → R are bounded functions and g is integrable on [a, b]. If there exists a constant C ≥ 0 such that asc I f ≤ Casc I g on every interval I ⊂ [a, b], then f is integrable.
> 
> The ideas is to control the oscillation of $f$ by an integrable function $g$

I guess this prop 3.1 is the most useful one once you manage the representation of $\text{ osc} f$.

> [!PDF|red] [[Ch9.pdf#page=12&selection=201,0,216,19&color=red|Ch9, p.12]]
> > Theorem 4.1. A continuous function f : [a, b] → R on a compact interval is Riemann integrable.
> 
> Seems very useful for a continuous function

**证明：**

由于连续函数在紧集上一定是**有界的**，因此我们只需验证它满足**定理 11.23（即柯西判据）**。

取任意 $\varepsilon > 0$。

连续函数在紧集上是**一致连续的**，因此存在 $\delta > 0$，使得对所有 $x, y \in [a, b]$，只要满足 $|x - y| < \delta$，就有：

$$
|f(x) - f(y)| < \frac{\varepsilon}{b - a}
$$

接下来，取一个划分 $P = \{I_1, I_2, \dots, I_n\}$ 使得每个子区间 $|I_k| < \delta$。  
例如，我们可以将区间 $[a, b]$ 均分成 $n$ 个等长子区间，每段长度为 $\frac{b - a}{n}$，并选取 $n > \frac{b - a}{\delta}$。

由于 $f$ 是连续函数，它在每个紧子区间 $I_k$ 上都能取得最大值 $M_k$ 和最小值 $m_k$，分别在某些点 $x_k, y_k \in I_k$ 处达到。

因为 $|I_k| < \delta$，所以这些点之间的距离 $|x_k - y_k| < \delta$，于是：

$$
M_k - m_k = \underbrace{ f(x_k) - f(y_k) < \frac{\varepsilon}{b - a} }_{ \text{ by definition of continuous function} }
$$

因此，上下黎曼和之差为：

$$
\begin{aligned}
U(f; P) - L(f; P) &= \sum_{k=1}^n M_k |I_k| - \sum_{k=1}^n m_k |I_k| \\
&= \sum_{k=1}^n (M_k - m_k) |I_k| \\
&< \frac{\varepsilon}{b - a} \sum_{k=1}^n |I_k| = \frac{\varepsilon}{b - a} \cdot (b - a) = \varepsilon
\end{aligned}
$$

由此可见，对于任意 $\varepsilon > 0$，我们都可以找到一个划分使得上下黎曼和之差小于 $\varepsilon$，这就满足了**柯西判据**。

因此，根据**定理 3.1**，函数 $f$ 是**黎曼可积的**。证毕。
> [!PDF|yellow] [[Ch9.pdf#page=13&selection=116,0,131,19&color=yellow|Ch9, p.13]]
> > Theorem 4.2. A monotonic function f : [a, b] → R on a compact interval is Riemann integrable.
> 
> This one is kinda funnier, the key idea in proving this is to set all the $I_{k}$ equal to $\frac{b-a}{n}$ so that we can cancel out all of the internal terms while doing the Riemann sums.

> [!PDF|yellow] [[Ch9.pdf#page=13&selection=292,7,292,38&color=yellow|Ch9, p.13]]
> > summing up a telescoping series
> 
> They call it a *telescoping series,* but basically it's just the former equals to the latter

> [!PDF|yellow] [[Ch9.pdf#page=14&selection=123,0,167,2&color=yellow|Ch9, p.14]]
> > Theorem 5.1. If f : [a, b] → R is integrable and c ∈ R, then cf is integrable and Z b a cf = c Z b a f.
> 
> Linearity

**证明：**

先设 $c \geq 0$。  
对于任意子集 $A \subset [a, b]$，有：
$$
\sup_A (cf) = c \sup_A f, \quad \inf_A (cf) = c \inf_A f
$$

因此对任意划分 $P$，有：
$$
U(cf; P) = c U(f; P)
$$

对 $[a, b]$ 上所有划分的集合 $\Pi$ 取下确界，得：
$$
U(cf) = \inf_{P \in \Pi} U(cf; P) = \inf_{P \in \Pi} c U(f; P) = c \inf_{P \in \Pi} U(f; P) = c U(f)
$$

同理：
$$
L(cf; P) = c L(f; P), \quad L(cf) = c L(f)
$$

若 $f$ 是可积的，则：
$$
U(cf) = c U(f) = c L(f) = L(cf)
$$

由此可知 $cf$ 可积，且：
$$
\int_a^b cf = c \int_a^b f
$$
接着考虑 $-f$。  
因为：
$$
\sup_A (-f) = - \inf_A f, \quad \inf_A (-f) = - \sup_A f
$$

所以：
$$
U(-f; P) = -L(f; P), \quad L(-f; P) = -U(f; P)
$$

进一步得到：
$$
U(-f) = \inf_{P \in \Pi} U(-f; P) = \inf_{P \in \Pi} [-L(f; P)] = - \sup_{P \in \Pi} L(f; P) = -L(f)
$$

$$
L(-f) = \sup_{P \in \Pi} L(-f; P) = \sup_{P \in \Pi} [-U(f; P)] = - \inf_{P \in \Pi} U(f; P) = -U(f)
$$

因此，若 $f$ 可积，则 $-f$ 也可积，且：
$$
\int_a^b (-f) = - \int_a^b f
$$

---

最后，若 $c < 0$，则可写为 $c = -|c|$，结合上述结论可得：  
$cf$ 可积，且有：
$$
\int_a^b cf = c \int_a^b f
$$
> You see the steps?
> 1. prove linearity holds for $c >0$ since for the positive $c$ we don't need to shift $\sup{}$ or $\inf{}$.
> 2. prove it holds for $-1$
> 3. so for all $c\leq 0,$ they're just $c = -\lvert c \rvert$

> [!PDF|yellow] [[Ch9.pdf#page=15&selection=305,0,357,2&color=yellow|Ch9, p.15]]
> > Theorem 5.2. If f, g : [a, b] → R are integrable functions, then f + g is integrable, and Z b a (f + g) = Z b a f + Z b a g.
> 
> For this, we can complete the proof for linearity

### 定理 5.2  
若 $f, g : [a, b] \to \mathbb{R}$ 是可积函数，则 $f + g$ 也是可积函数，且有：
$$
\int_a^b (f + g) = \int_a^b f + \int_a^b g
$$

---

**证明：**

我们首先证明：若 $f, g : [a, b] \to \mathbb{R}$ 是有界函数（不一定可积），则有：
$$
U(f + g) \leq U(f) + U(g), \quad L(f + g) \geq L(f) + L(g)
$$

设 $P = \{I_1, I_2, \dots, I_n\}$ 是 $[a, b]$ 的一个划分。则：

$$
\begin{aligned}
U(f + g; P) &= \sum_{k=1}^n \sup_{I_k}(f + g) \cdot |I_k| \\
&\leq \sum_{k=1}^n \sup_{I_k} f \cdot |I_k| + \sum_{k=1}^n \sup_{I_k} g \cdot |I_k| \\
&= U(f; P) + U(g; P)
\end{aligned}
$$

>here the key idea is $$
\sup{(f+g)} \leq \sup{f} + \sup{g}
$$

令 $\varepsilon > 0$，由于上黎曼积分是上和的下确界，存在划分 $Q, R$ 满足：
$$
U(f; Q) < U(f) + \frac{\varepsilon}{2}, \quad U(g; R) < U(g) + \frac{\varepsilon}{2}
$$

设 $P$ 是 $Q$ 与 $R$ 的一个共同细化，则：
$$
U(f; P) < U(f) + \frac{\varepsilon}{2}, \quad U(g; P) < U(g) + \frac{\varepsilon}{2}
$$

从而：
$$
U(f + g) \leq U(f + g; P) \leq \underbrace{ U(f; P) + U(g; P) < U(f) + U(g) + \varepsilon }_{ \text{ by construction of }P }
$$

由于此不等式对任意 $\varepsilon > 0$ 成立，故：
$$
U(f + g) \leq U(f) + U(g)
$$

类似地，对于下黎曼和有：
$$
L(f + g; P) \geq L(f; P) + L(g; P)
$$

因此对任意 $\varepsilon > 0$，有：
$$
L(f + g) > L(f) + L(g) - \varepsilon \Rightarrow L(f + g) \geq L(f) + L(g)
$$

---

若 $f, g$ 是可积函数，则有：
$$
U(f + g) \leq U(f) + U(g) = L(f) + L(g) \leq L(f + g)
$$

又因为总有 $U(f + g) \geq L(f + g)$，故可得：
$$
U(f + g) = L(f + g)
$$

即 $f + g$ 是黎曼可积函数。  
并且不等式中的等号也成立，因此：
$$
\int_a^b (f + g) = \int_a^b f + \int_a^b g
$$

证毕。

> [!PDF|red] [[Ch9.pdf#page=16&selection=358,0,359,28&color=red|Ch9, p.16]]
> > The product of integrable functions is also integrable, as is the quotient provided it remains bounded.
> 
> We only know it's integrable but don't know the precise form of it


> [!PDF|yellow] [[Ch9.pdf#page=16&selection=379,0,433,11&color=yellow|Ch9, p.16]]
> > Theorem 5.3. If f, g : [a, b] → R are integrable, then f g : [a, b] → R is integrable. If, in addition, g̸ = 0 and 1/g is bounded, then f /g : [a, b] → R is integrable.
> 
> Note that we're going to prove this based on a simple trick


### 定理 5.3  
若 $f, g : [a, b] \to \mathbb{R}$ 是可积函数，则乘积函数 $fg : [a, b] \to \mathbb{R}$ 也是可积的。  
若进一步满足 $g \neq 0$ 且 $1/g$ 有界，则商函数 $f/g : [a, b] \to \mathbb{R}$ 也是可积的。

---

**证明：**

我们首先证明：**可积函数的平方是可积的**。

若 $f$ 是可积的，则它是有界的，即存在某个 $M \geq 0$，使得对所有 $x \in [a, b]$ 有 $|f(x)| \leq M$。

对于任意 $x, y \in [a, b]$，有：
$$
\left|  f^2(x) - f^2(y) \right| = |f(x) + f(y)| \cdot |f(x) - f(y)| \leq 2M \cdot |f(x) - f(y)|
$$

对区间 $I \subset [a, b]$ 上的 $x, y$ 取上确界，有：
$$
\sup_I f^2 - \inf_I f^2 \leq 2M (\sup_I f - \inf_I f)
$$

即：
$$
\operatorname{osc}_I (f^2) \leq 2M \cdot \operatorname{osc}_I (f)
$$

根据振幅控制定理（命题 11.25），$f^2$ 可积。

再考虑恒等式：
$$
fg = \frac{1}{4} \left[ (f + g)^2 - (f - g)^2 \right]
$$

由于 $f + g$ 与 $f - g$ 是可积的，其平方也是可积的（由前面所证），故 $fg$ 也可积。

>值得一提的是：利用平方差恒等式表示乘积的技巧非常古老——古巴比伦人就曾使用该方法配合平方表计算乘积。

---

以类似方式考虑商函数。若 $g \neq 0$ 且 $|1/g| \leq M$，则：
$$
\left| \frac{1}{g(x)} - \frac{1}{g(y)} \right| = \frac{|g(x) - g(y)|}{|g(x)g(y)|} \leq M^2 \cdot |g(x) - g(y)|
$$

对区间 $I \subset [a, b]$ 取上确界，有：
$$
\sup_I \left( \frac{1}{g} \right) - \inf_I \left( \frac{1}{g} \right) \leq M^2 (\sup_I g - \inf_I g)
$$

即：
$$
\operatorname{osc}_I \left( \frac{1}{g} \right) \leq M^2 \cdot \operatorname{osc}_I g
$$

由命题 11.25 可知：若 $g$ 可积，则 $1/g$ 可积。因此：
$$
\frac{f}{g} = f \cdot \frac{1}{g}
$$
也是可积函数。

证毕。
> [!PDF|yellow] [[Ch9.pdf#page=17&selection=216,0,253,1&color=yellow|Ch9, p.17]]
> > Theorem 5.4. Suppose that f, g : [a, b] → R are integrable and f ≤ g. Then Z b a f ≤ Z b a g
> 
> The direct monotonicity outcome is proved below:

### 定理 5.4  
设 $f, g : [a, b] \to \mathbb{R}$ 是可积函数，且满足 $f \leq g$。  
则有：
$$
\int_a^b f \leq \int_a^b g
$$

---

**证明：**

首先，设 $f \geq 0$ 且可积。  
取划分 $P$ 为单个区间 $[a, b]$，则有：
$$
L(f; P) = \inf_{[a, b]} f \cdot (b - a) \geq 0
$$

因此：
$$
\int_a^b f = L(f) \geq L(f; P) \geq 0
$$
>Until here, the basic idea is to prove that a non-negative function's integral is non-negative

若 $f \geq g$，则令 $h = f - g \geq 0$。  
由于积分的线性性，有：
$$
\int_a^b f - \int_a^b g = \underbrace{ \int_a^b h \geq 0 }_{ \text{above proof} }
$$

这就证明了定理。

 > [!PDF|yellow] [[Ch9.pdf#page=17&selection=391,0,458,1&color=yellow|Ch9, p.17]]
> > Theorem 5.5. Suppose that f : [a, b] → R is integrable and M = sup [a,b] f, m = inf [a,b] f . Then m(b − a) ≤ Z b a f ≤ M (b − a).
> 
> Use the definition and it's trivial

> [!PDF|red] [[Ch9.pdf#page=18&selection=57,0,103,2&color=red|Ch9, p.18]]
> > Theorem 5.6. If f : [a, b] → R is continuous, then there exists x ∈ [a, b] such that f (x) = 1 b − a Z b a f.
> 
> This is the famous mean value theorem (MVT)

I think you need to go over this proof since this seems non trivial.
*Proof*.
Since $f$ is continuous function on a compact interval $[a,b]$ , the extreme value theorem implies it attains its maximum $M$ and minimum value $m$ 

From thm 5.5 we know $$
m \leq \frac{1}{b-a} \int _{[a,b]}f  \leq M
$$
By intermediate value theorem, $f$ takes on every value between $m$ and $M$, so the result follows.



> [!PDF|yellow] [[Ch9.pdf#page=18&selection=185,0,218,1&color=yellow|Ch9, p.18]]
> > Theorem 5.7. If f is integrable, then |f | is integrable and Z b a f ≤ Z b a |f |.
> 
> I think it's more important to know that $\lvert f \rvert$ is also integrable

### 定理 5.7  
若 $f$ 是可积函数，则 $|f|$ 也是可积的，并且有：
$$
\int_a^b f \leq \int_a^b |f|
$$

---

**证明：**

首先，假设 $|f|$ 是可积的。  
由于对所有 $x \in [a, b]$ 有：
$$
-|f(x)| \leq f(x) \leq |f(x)|
$$

根据积分的单调性（定理 11.36），可得：
$$
- \int_a^b |f| \leq \int_a^b f \leq \int_a^b |f|
$$

从而推出：
$$
\int_a^b f \leq \int_a^b |f|
$$

---

为了完成证明，我们还需说明：**若 $f$ 可积，则 $|f|$ 也可积**。

对任意 $x, y \in [a, b]$，由**反三角不等式**有：
$$
\left||f(x)| - |f(y)|\right| \leq |f(x) - f(y)|
$$

因此对任意子区间 $I \subset [a, b]$ 有：
$$
\sup_I |f| - \inf_I |f| \leq \sup_I f - \inf_I f
$$

即：
$$
\operatorname{osc}_I |f| \leq \operatorname{osc}_I f
$$
> we still follow the same thought: find a integrable function to control the oscillation

由命题 3.1 可知：若 $f$ 可积，则 $|f|$ 也可积。

综上所述，$|f|$ 是可积的，且有：
$$
\int_a^b f \leq \int_a^b |f|
$$

证毕。


> [!PDF|red] [[Ch9.pdf#page=19&selection=65,0,102,0&color=red|Ch9, p.19]]
> > Proposition 5.1. If f : [a, b] → R is a continuous function such that f ≥ 0 and R b a f = 0, then f = 0
> 
> This one is crucial, just keep in mind there's a $f\equiv 0$ property

> [!PDF|yellow] [[Ch9.pdf#page=19&selection=374,0,439,1&color=yellow|Ch9, p.19]]
> > Theorem 5.8. Suppose that f : [a, b] → R and a < c < b. Then f is Riemann integrable on [a, b] if and only if it is Riemann integrable on [a, c] and [c, b]. Moreover, in that case, Z b a f = Z c a f + Z b c f
> 
> 
此性质是指对**积分区间**的可加性，而非对被积函数的线性性。
### 定理 5.8  
设 $f : [a, b] \to \mathbb{R}$ 且 $a < c < b$，  
则 $f$ 在区间 $[a, b]$ 上是黎曼可积的，当且仅当它在 $[a, c]$ 和 $[c, b]$ 上都是黎曼可积的。  
此外，在这种情况下，有：
$$
\int_a^b f = \int_a^c f + \int_c^b f
$$

---

**证明：**

设 $f$ 在区间 $[a, b]$ 上可积。  
则对任意 $\varepsilon > 0$，存在一个划分 $P$ 使得：
$$
U(f; P) - L(f; P) < \varepsilon\tag{Cauchy}
$$

令 $P' = P \cup \{c\}$，即在划分 $P$ 中加入点 $c$ 构成细化划分（若 $c \in P$，则 $P' = P$）。

将 $P'$ 拆分为两个子划分：
- $Q = P' \cap [a, c]$ 是 $[a, c]$ 的划分
- $R = P' \cap [c, b]$ 是 $[c, b]$ 的划分

那么有：
$$
\underbrace{ U(f; P') = U(f; Q) + U(f; R) }_{ \text{from the separation} }, \quad L(f; P') = L(f; Q) + L(f; R)
$$

于是：
$$
\begin{align}
U(f; Q) - L(f; Q)  & = \underbrace{ U(f; P') - L(f; P') }_{ \leq U(f;P) - L(f;P) \text{ due to refinement} } - \underbrace{ [U(f; R) - L(f; R)] }_{ \geq 0 }  \\
 & \leq U(f; P) - L(f; P) < \varepsilon
\end{align}

$$

因此 $f$ 在 $[a, c]$ 上可积。交换 $Q$ 和 $R$ 的角色，同理可证 $f$ 在 $[c, b]$ 上也可积。

---

反过来，若 $f$ 在 $[a, c]$ 和 $[c, b]$ 上都可积，  
则存在划分 $Q$ 和 $R$，分别对应 $[a, c]$ 和 $[c, b]$，使得：
$$
U(f; Q) - L(f; Q) < \frac{\varepsilon}{2}, \quad U(f; R) - L(f; R) < \frac{\varepsilon}{2}
$$

令 $P = Q \cup R$，则：
$$
U(f; P) - L(f; P) = [U(f; Q) - L(f; Q)] + [U(f; R) - L(f; R)] < \varepsilon
$$

所以 $f$ 在 $[a, b]$ 上可积。

---

最后，若 $f$ 可积，则根据上述划分 $P, Q, R$ 有：
$$
\begin{align}
\int_a^b f \leq U(f; P)  & = U(f; Q) + U(f; R)  \\
 & < L(f; Q) + L(f; R) + \varepsilon  \\
 & < \int_a^c f + \int_c^b f + \varepsilon
\end{align}

$$

同理有：
$$
\begin{align}
\int_a^b f \geq L(f; P)  & = L(f; Q) + L(f; R)  \\
 & > U(f; Q) + U(f; R) - \varepsilon  \\
 & > \int_a^c f + \int_c^b f - \varepsilon
\end{align}
$$

由于 $\varepsilon > 0$ 是任意的，可得：
$$
\int_a^b f = \int_a^c f + \int_c^b f
$$

证毕。

> [!PDF|yellow] [[Ch9.pdf#page=21&selection=6,0,7,62&color=yellow|Ch9, p.21]]
> > First, we show that changing the values of a function at finitely many points doesn’t change its integrability of the value of its integral.
> 
> This one is good!

> [!PDF|yellow] [[Ch9.pdf#page=21&selection=9,0,71,2&color=yellow|Ch9, p.21]]
> > Proposition 6.1. Suppose that f, g : [a, b] → R and f (x) = g(x) except at finitely many points x ∈ [a, b]. Then f is integrable if and only if g is integrable, and in that case Z b a f = Z b a g.
> 
> Let's now dive into the proof!

### 命题 6.1

设 $f, g : [a, b] \to \mathbb{R}$，且 $f(x) = g(x)$ 除了在有限多个点 $x \in [a, b]$。

那么：

- 若 $f$ 可积，则 $g$ 也可积；
- 并且有：

$$
\int_a^b f = \int_a^b g.
$$

---

### 证明

只需证明当 $f$ 与 $g$ 仅在**一点** $c \in [a, b]$ 上取值不同的情形。更一般的结论可通过多次应用此结果得到。

由于 $f$ 与 $g$ 仅在一点处不同，所以：

- $f$ 有界当且仅当 $g$ 有界；
- 若 $f, g$ 无界，则它们都不可积。

若 $f, g$ 有界，且存在常数 $M > 0$，使得 $|f|, |g| \leq M$，我们将证明它们具有相同的上积分与下积分。其原因是，对于一个在差异点附近足够细的划分，它们的上下和之差可以任意小。

设 $\varepsilon > 0$。选取划分 $P$ 满足：

$$
U(f; P) < U(f) + \frac{\varepsilon}{2}.
$$

设 $Q = \{I_1, \dots, I_n\}$ 是 $P$ 的细化划分refinement，并且每个区间满足 $|I_k| < \delta$，其中：

$$
\delta = \frac{\varepsilon}{8M}.
$$

在此划分下，$g$ 最多在两个区间上与 $f$ 不同（例如 $c$ 是划分点的端点）。

在这些区间 $I_k$ 上有：

$$
\lvert\sup_{I_k} g - \sup_{I_k} f  \rvert  \leq \sup_{I_k} |g| + \sup_{I_k} |f| \leq 2M,
$$

其余区间上则有：

$$
\sup_{I_k} g - \sup_{I_k} f = 0.
$$

因此：

$$
|U(g; Q) - U(f; Q)| < 2M \cdot 2\delta < \frac{\varepsilon}{2}.
$$

利用上积分对细化划分的单调性，我们有：

$$
\begin{aligned}
U(g) &\leq U(g; Q) \\
&< \underbrace{ U(f; Q) + \frac{\varepsilon}{2} }_{ \delta = \frac{\epsilon}{8M} }  \\ 
&\leq \underbrace{ U(f; P) + \frac{\varepsilon}{2}  }_{ Q \text{ is a refinement of } P }\\
&< U(f) + \varepsilon.
\end{aligned}
$$

由于该不等式对任意 $\varepsilon > 0$ 成立，得到：

$$
U(g) \leq U(f).
$$

交换 $f$ 与 $g$ 的角色，类似地可得：

$$
U(f) \leq U(g),
$$

从而：

$$
U(f) = U(g).
$$

对下积分的推理与上述类似（或者对 $-f, -g$ 应用上积分的结论），可得：

$$
L(f) = L(g).
$$

因此：

- $f$ 可积 $\Leftrightarrow U(f) = L(f)$；
- $g$ 可积 $\Leftrightarrow U(g) = L(g)$；
- 且当可积时，有：

$$
\int_a^b f = \int_a^b g.
$$

> [!PDF|yellow] [[Ch9.pdf#page=22&selection=3,0,59,2&color=yellow|Ch9, p.22]]
> > Proposition 6.2. Suppose that f : [a, b] → R is bounded and integrable on [a, r] for every a < r < b. Then f is integrable on [a, b] and Z b a f = lim r→b− Z r a f.
> 
> 下一个命题允许我们从一个函数在稍小区间上的可积性推出其在整个区间上的可积性。
### 命题 6.2


设 $f : [a, b] \to \mathbb{R}$ 是**有界**函数，且对所有 $a < r < b$，$f$ 在 $[a, r]$ 上可积。

则：

- $f$ 在 $[a, b]$ 上可积；
- 且有：

$$
\int_a^b f = \lim_{r \to b^-} \int_a^r f.
$$

---

### 证明

由于 $f$ 有界，存在常数 $M > 0$ 使得 $|f| \leq M$ 在 $[a, b]$ 上成立。

给定 $\varepsilon > 0$，取：

$$
r = b - \frac{\varepsilon}{4M},
$$

（假设 $\varepsilon$ 足够小，使得 $r > a$）。

因为 $f$ 在 $[a, r]$ 上可积，存在划分 $Q$ 使得：

$$
U(f; Q) - L(f; Q) < \frac{\varepsilon}{2}.
$$

令 $P = Q \cup \{b\}$，则 $P$ 是 $[a, b]$ 的划分，其最后一个区间为 $[r, b]$。

由于 $f$ 有界，有：

$$
\sup_{[r, b]} f - \inf_{[r, b]} f \leq 2M.
$$

因此：

$$
\begin{aligned}
U(f; P) - L(f; P) &= \left(U(f; Q) - L(f; Q)\right) + \left(\sup_{[r, b]} f - \inf_{[r, b]} f\right) \cdot (b - r) \\
&< \frac{\varepsilon}{2} + 2M \cdot (b - r) \\
&= \frac{\varepsilon}{2} + \underbrace{ 2M\cdot \frac{\varepsilon}{4M}  }_{ r = b - \frac{\varepsilon}{4M}, }= \varepsilon.
\end{aligned}
$$

因此，由定理 11.23，$f$ 在 $[a, b]$ 上可积。
进一步，由积分的可加性可得：

$$
\left| \int_a^b f - \int_a^r f  \right| = \left| \int_r^b f  \right| \leq M \cdot (b - r) \to 0 \quad \text{当 } r \to b^-.
$$

故有：

$$
\int_a^b f = \lim_{r \to b^-} \int_a^r f.
$$
> [!PDF|yellow] [[Ch9.pdf#page=22&selection=391,0,410,22&color=yellow|Ch9, p.22]]
> > Theorem 6.1. If f : [a, b] → R is a bounded function with finitely many discontinuities, then f is Riemann integrable.
> 
> There're 2 demands:
> 1. $f$ is bounded
> 2. $f$ has finitely many discontinuities

### 证明

将区间 $[a, b]$ 拆分为若干子区间，并使 $f$ 的间断点正好是这些子区间的端点之一，利用 **定理 5.8**（关于积分的可加性），我们只需证明下述特殊情况：

函数 $f$ 仅在 $[a, b]$ 的一个端点间断，例如在右端点 $b$ 处不连续。

在这种情况下，$f$ 在任意较小的区间 $[a, r]$（其中 $a < r < b$）上是连续的，因此是可积的。

根据**命题 6.2**（关于右端点极限的积分收敛性），可得：

$$
f \text{ 在 } [a, b] \text{ 上也可积}.
$$
### 例 6.2

定义函数 $f : \left[0, \frac{1}{\pi}\right] \to \mathbb{R}$ 为：

$$
f(x) =
\begin{cases}
\operatorname{sgn}[\sin(1/x)] & \text{若 } x \ne \frac{1}{n\pi}, \text{其中 } n \in \mathbb{N}, \\
0 & \text{若 } x = 0 \text{ 或 } x = \frac{1}{n\pi}, \text{其中 } n \in \mathbb{N},
\end{cases}
$$

其中 $\operatorname{sgn}$ 是符号函数，定义为：

$$
\operatorname{sgn}(x) =
\begin{cases}
1 & \text{若 } x > 0, \\
0 & \text{若 } x = 0, \\
-1 & \text{若 } x < 0.
\end{cases}
$$

---

这个函数在 $x \to 0^+$ 的过程中，在 $1$ 和 $-1$ 之间振荡了**可数无穷多次**（见图2）。

它在 $x = \frac{1}{n\pi}$ 处有**跳跃间断点**，在 $x = 0$ 处有一个**本质间断点**。

尽管如此，$f$ 仍然是黎曼可积的。

---

原因如下：

- $f$ 在 $\left[0, \frac{1}{\pi}\right]$ 上是有界的；
- 对于任意 $0 < r < \frac{1}{\pi}$，函数 $f$ 在区间 $[r, \frac{1}{\pi}]$ 上是**分段连续的**，且仅有**有限多个间断点**；
- 根据**定理 6.1**，$f$ 在每个 $[r, \frac{1}{\pi}]$ 上是黎曼可积的；
- 然后根据**命题 6.2**，可推得 $f$ 在整个区间 $[0, \frac{1}{\pi}]$ 上是可积的。

**因此，尽管 $f$ 在 $x=0$ 处具有本质间断，仍然：**

$$
f \text{ 在 } \left[0, \frac{1}{\pi} \right] \text{ 上是黎曼可积的。}
$$
> [!PDF|red] [[Ch9.pdf#page=24&selection=57,1,74,0&color=red|Ch9, p.24]]
> > t has jump discontinuities at x = 1/(nπ) and an essential discontinuity at x = 0.
> 
> What are these discontinuities?

1. For jump discontinuity, this is the *first kind*, that is : 

$$
\lim_{ x \to c^{-} } f(x) \neq \lim_{ x \to c^+ }  f(x)
$$
2. For essential discontinuity, the *second kind*, at least one of the left limit or the right limit doesn't exist.

---
Here are something else in the class:

**Definition**: Let $f: [a,b] \to \mathbb{R}$ be a function. A function $F: [a,b] \to \mathbb{R}$ is called a **primitive function** or **antiderivative** of $f$ on $[a,b]$ if $F$ is differentiable on $(a,b)$ and satisfies
$$
F'(x) = f(x), \quad \forall x \in (a,b).
$$

---

**Theorem (Fundamental Theorem of Calculus I):**  
Let $f: [a,b] \to \mathbb{R}$ be Riemann integrable, and let $F: [a,b] \to \mathbb{R}$ be differentiable on $(a,b)$ such that  
$$
F'(x) = f(x), \quad \forall x \in (a,b).
$$  
Then  
$$
\int_a^b f(x) \, dx = F(b) - F(a).
$$

**Proof:**  

Let $P = \{x_0, x_1, \dots, x_n\}$ be a partition of $[a,b]$ with $a = x_0 < x_1 < \dots < x_n = b$. For each subinterval $[x_{i-1}, x_i]$, by the Mean Value Theorem (since $F$ is differentiable on $(x_{i-1}, x_i)$ and hence continuous on $[x_{i-1}, x_i]$), there exists $c_i \in (x_{i-1}, x_i)$ such that:
$$
F(x_i) - F(x_{i-1}) = F'(c_i)(x_i - x_{i-1}) = f(c_i)(x_i - x_{i-1}).
$$

Now sum over all subintervals:
$$
F(b) - F(a) = \sum_{i=1}^n \left[F(x_i) - F(x_{i-1})\right] = \sum_{i=1}^n f(c_i)(x_i - x_{i-1}).
$$

This is a **Riemann sum** for $f$ over the partition $P$ with sample points $c_i \in (x_{i-1}, x_i)$.

Since $f$ is Riemann integrable on $[a,b]$, as the mesh of the partition $\|P\| \to 0$, the Riemann sum converges to the integral:
$$
\lim_{\|P\| \to 0} \sum_{i=1}^n f(c_i)(x_i - x_{i-1}) = \int_a^b f(x)\, dx.
$$

Thus,
$$
F(b) - F(a) = \int_a^b f(x)\, dx.
$$

$\blacksquare$

---
**Theorem (Fundamental Theorem of Calculus II):**  
Let $f: [a,b] \to \mathbb{R}$ be Riemann integrable. Define $F: [a,b] \to \mathbb{R}$ by  
$$
F(x) = \int_a^x f(t)\, dt.
$$  
Then:
1. $F$ is continuous on $[a,b]$;
2. If $f$ is continuous at some $x_0 \in (a,b)$, then $F$ is differentiable at $x_0$ and  
$$
F'(x_0) = f(x_0).
$$

---

**Proof:**

**(1) Continuity of $F$ on $[a,b]$:**

Let $x \in [a,b]$ and $h$ be a small increment such that $x + h \in [a,b]$. Then
$$
F(x + h) - F(x) = \int_a^{x+h} f(t)\, dt - \int_a^x f(t)\, dt = \int_x^{x+h} f(t)\, dt.
$$

By the integrability of $f$, $f$ is *bounded*: there exists $M > 0$ such that $|f(t)| \leq M$ for all $t \in [a,b]$. Then:
$$
|F(x + h) - F(x)| = \left| \int_x^{x+h} f(t)\, dt \right| \leq \int_x^{x+h} |f(t)|\, dt \leq M|h|.
$$

Thus, as $h \to 0$, $|F(x+h) - F(x)| \to 0$, so $F$ is continuous at $x$. Since $x \in [a,b]$ was arbitrary, $F$ is continuous on $[a,b]$.

---

**(2) Differentiability at $x_0 \in (a,b)$ where $f$ is continuous:**

We consider the definition of the derivative:
$$
\frac{F(x_0 + h) - F(x_0)}{h} = \frac{1}{h} \int_{x_0}^{x_0 + h} f(t)\, dt, \quad \text{for small } h \text{ with } x_0 + h \in [a,b].
$$

By the **Mean Value Theorem for Integrals**, since $f$ is continuous at $x_0$, for any $\varepsilon > 0$, there exists $\delta > 0$ such that for all $t \in [x_0, x_0 + h]$ (or $[x_0 + h, x_0]$ if $h < 0$),
$$
|f(t) - f(x_0)| < \varepsilon.
$$

Then:
$$
\left| \frac{1}{h} \int_{x_0}^{x_0 + h} f(t)\, dt - f(x_0) \right| = \left| \frac{1}{h} \int_{x_0}^{x_0 + h} (f(t) - f(x_0))\, dt \right| \leq \underbrace{ \frac{1}{|h|} \int_{x_0}^{x_0 + h} |f(t) - f(x_0)|\, dt }_{  <\frac{1}{|h|} \int_{x_0}^{x_0 + h} \varepsilon\, dt} < \varepsilon.
$$

So:
$$
\lim_{h \to 0} \frac{F(x_0 + h) - F(x_0)}{h} = f(x_0),
$$
i.e., $F'(x_0) = f(x_0)$.

$\blacksquare$
> We can think of an example, let $f(x) = 0$ on $[0,1]\setminus\left\{  \frac{1}{2}  \right\}$ and $f\left( \frac{1}{2} \right) = 1$. We can always see that $F(x)$ = 0 and $F'(x)\equiv0$ but then $F'\left( \frac{1}{2} \right)\neq f\left( \frac{1}{2} \right)$.

One notation is that if we say $f \in R([a,b])$, then we say it's Riemann integrable on $[a,b]$.

1. trivial proof
2. True of False
	1. Real number 
	2. sequential limits and convergence
	3. squeeze theorem
	4. Cauchy Criterion
	5. series, convergence 