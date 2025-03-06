# Lecture 1
**Theorem 2.1** consider the polynomial equation $n\ge1$ 
$$x^{n}+ c_{n-1}x^{n-1}+ \cdots+ c_{1}x +c_{0} = 0$$
where the coefficients are integers and $c_{0} \ne 0$. Any rational solution of this must be an integer that divides $c_0$ .

**Definition 6.2** Suppose that $A \subset \mathbb{R}$ is a set of real numbers.
- If $M\in \mathbf{R}$ is an upper bound of $\mathbf{A}$ such that $M \le M'$ for every upperbound $M'$ of $\mathbf{A}$, then $$
M =\sup  \mathbf{A}
$$
- One useful property: if $\max \mathbf{A}$ exists, then $\sup \mathbf{A} = \max \mathbf{A}$ .

**Theorem 7.1** Completeness Axiom
Every nonempty set $\mathbf{S}$ of real numbers that is bounded from above has a supremum, i.e.
$$
\\\exists \sup \mathbf{S} , \text{ and } \sup \mathbf{S} \in \mathbf{R}
$$

**Corollary 7.2** Archimedean Property
if $a,b>0$, then for some positive integer $n$, we have $na>b$

# Lecture 2
**Proposition 1.1** for all $x,y\in \mathbf{R}$:
1. $|x|\ge 0, |x|=0 \iff x=0$
2. $|-x| =|x|$
3. $|x+y| \leq |x| + |y|$
4. $|xy| = |x|\cdot|y|$
5. $|x-y| \geq  ||x|-|y||$

**Proposition 1.2** A set $A\subseteq \mathbf{R}$ is bounded iff there exists a real number $M\ge 0$ such that $$
|x| \leq M,\forall x \in A
$$
**Proposition 3.1** If a sequence converges, then its limit is unique.

**Theorem 4.1** A sequence $(x_{n})$ is bounded if it has a limit when $n\to \infty$

**Theorem 5.1** A monotone sequence of real numbers converges iff it's bounded

**Definition 6.1** Suppose that $(x_{n})$ is a sequence of real numbers. Then $$
y_{n } =\sup \{ x_{k} :k\geq n \},\lim_{ n \to \infty } \sup x_{n} = \lim_{ n \to \infty } y_{n}
		$$
>  Note that $y_{n}$ is monotone decreasing. we can also write it as $$
\lim_{ n \to \infty } \sup x_{n}  = \inf_{n\in \mathbf{N}} \left(\sup_{k\geq n}x_{n}\right)
$$

**Theorem 6.1** Let $(x_{n})$ be a real sequence, then $y = \lim_{ n \to \infty }\sup x_{n}$ iff $y\in \mathbf{R}$ statisfies one of the following conditions.
1. $y\ne \infty \text{ and } y \ne -\infty$, for every $\epsilon >0$:
	1. there exists $N\in \mathbf{N}$ such that $x_{n}<y+\epsilon$ for all $n>N$
	2. for every $N\in \mathbf{N}$, there exists $n>N$ such that $x_{n}>y-\epsilon$
2. $y = \infty$ , then $(x_{n})$ is not bounded from above
3. $y = - \infty$ , then $x_{n} \to - \infty$ as $n\to \infty$.

**Oscillation** If $\lim_{ n \to \infty }\sup x_{n }\ne \lim_{ n \to \infty } \inf x_{n}$, then we say the sequence $(x_{n})$ oscillates

**Corollary 8.1** If a sequence has subsequences that converge to differenct limits, then the sequence diverges.

**Theorem 9.1** Bolzano-Weierstrass
Every bounded sequence of real numbers has a **convergent subsequence.**

**Theorem 9.2** if $(x_{n})$ is bouned sequence of real numbers such that every convergent subsequence has the same limit $L$, then $(x_{n})$ converges to $L$.

# Lecture 3

**Proposition 1.1** a series $\sum a_{n}$ with positive terms $a_{n}\ge_{0}$ converges iif its partial sums $$
\sum_{k=1}^n a_{k} \le M
$$ are bounded from above.

**Theorem 2.1** Cauchy condition
the series $\sum a_{n}$ converges iff for every $\epsilon >0$ there exists $N\in \mathbf{N}$ such that the tail of the series are arbitrarily small $$
\left|\sum_{k=m+1}^n a_{k} \right| < \epsilon ,\forall ~n>m>N
$$
**Corollary 2.1** If $\sum a_{n}$ converges, then $a_{n} \to 0$

**Definition 3.2** The positive and negative parts of a real number $a \in \mathbb{R}$ are given by $$
a^+ = \begin{cases}
a & a \ge {0} \\
0 & o.w. 
\end{cases}, a^- = \begin{cases}
0  & a \ge 0 \\
|a| & o.w.
\end{cases}
$$it follows that $$
0\leq a^+,a^-\leq|a|, a= a^+ -  a^-,|a| = a^+ + a^-
$$
**Propostion 3.1** 
1. An absolutely convergent series converges
2. $\sum a_{n}$ converges absolutely iff the series $\sum a^+_{n},\sum a^-_{n}$ both converge.
	1. furthermore, in this case $$
\sum_{n=1}^\infty a_{n} = \sum_{n=1}^\infty a_{n}^+ - \sum_{n=1}^\infty a_{n}^-. \sum_{n=1}^\infty |a_{n}| = \underbrace{ \sum_{n=1}^\infty a_{n}^+ + \sum_{n=1}^\infty a_{n}^- }_{\text{ by defintion} }
$$
**Proof of sketch** for the second part, we should notice that $$
0\leq \sum |a_{k}|  = \sum a_{k}^+ + \sum a_{k}^-
$$
so $\sum|a_{k}|$ is cauchy if $\sum a_{k}^ +$ and $\sum a_{k}^-$ are cauchy
and $$
\begin{align}
0  & \le \sum a_{k}^+ \le \sum |a_{k}| \\
0 & \le \sum a_{k}^- \le \sum |a_{k}|
\end{align}

$$
so  $\sum a_{k}^ +$ and $\sum a_{k}^-$ are cauchy if $\sum |a_{k}|$ is cauchy.

**Theorem 4.1** Comparison test
suppose that $b_{n}\ge 0$ and $\sum b_{n}$ converges, if $|a_{n}| \le b_{n}$, then $\sum a_{n}$ converges absolutely.
> The key is that they both satisfy Cauchy condition

**Theorem 4.2** Ratio test
suppose that $(a_{n})$ is a sequence of nonzero real numbers:
- it converges absolutely if $$\lim_{ n \to \infty }\sup |\frac{a_{n+1}}{a_{n}}|<1$$
- it diverges if $$
\lim_{ n \to \infty } \inf{| \frac{a_{n+1}}{a_{n}}|} > 1
$$
> either possibility may occur when the limit in the ratio test is $1$ 

**Theorem 4.3** Root test
suppose that $(a_{n})$ is a sequence of real numbers and let $$
r= \lim_{ n \to \infty } \sup{|a_{n}|^{1/n}}
$$then the series $\sum a_n$ converges absolutely if $0 \leq r<1$ and diverges if $1<r\leq \infty$

**Theorem 4.4** Integral test
suppose that $(a_{n})$ is a sequence of positive real numbers, then suppose there is a **decreasing** function $f:\left[ 1,\infty \right] \to \mathbb{R}$ such that $f(n) = a_n$ . Then $\sum a_{n}$ converges iff $\int_{1}^\infty f(x)dx$ converges.


**Theorem 5.1** Alternating series
suppose that $(a_{n})$ is a **decreasing** sequence of nonnegative real numbers such that $a_{n}\to 0$ as $n \to \infty$ . Then the alternating series converges.$$
\sum_{n=1}^\infty (-1)^{n+1} a_{n}
$$
**Definition 7.1** a series $\sum b_{m}$ is a rearrangement of a series $\sum a_{n}$ if there is a **one to one, onto function** $f:\mathbb{N} \to \mathbb{N}$ such that $b_{m} = a_{f(m)}$. 
- if $\sum b_{m}$ is a rearrangement of $\sum a_{n}$, with $n =f(m)$, then $\sum a_{n}$ is a rearrangement of $\sum b_{m}$ , with $m =f^{-1}(n)$.

**Theorem 7.1** every rearrangement of an absolutely convergent series  converges to the same limit.
> Proof.
> suppose $\sum a_{n}$ is convergent with $a_{n}\geq 0$. Given $\varepsilon >0$, choose $N \in \mathbb{N}$ such that $$
0\le \sum_{k=N}^\infty a_{k} < \varepsilon
$$ since $f$ is one to one and onto, there exists $M \in \mathbb{N}$ such that $$
\{ 1,2,\dots N\} \subseteq f^{-1}(\{ 1,2,\dots,M \})
$$ all the terms $a_{1} \to a_{N}$ is included among the $b_{1}\to b_{M}$ . For example we can take $$
M = \max \{  m \in \mathbb{N}|1\leq f(m)\leq N \}
$$ so if $m>M$, then $$
\sum_{k=1}^N a_{k } \leq \sum_{j=1}^m b_{j} \leq \sum_{k+1}^\infty a_{k}
$$ holds for all $m >M$. Then we have $$
0\leq \sum_{k=1}^\infty a_{k} - \sum_{j=1}^m b_{j} < \varepsilon
$$ which proves that $$
\sum_{j=1}^\infty b_{j} = \sum_{k=1}^{\infty} a_{k}
	$$ if $\sum a_{n}$ is absolutely convergent, then the positive and negative parts of the the series $\sum a^{+},\sum a^{-}$ converge. if $\sum b_{m}$ is the rearrangement of $\sum a_{k}$, then $\sum b_{m}^{+}$ and $\sum b_{m}^{-}$ are the rearrangements of the 2 respectively.
	It follows that they converge and $$
\sum_{m=1}^{\infty} b_m^+ = \sum_{n=1}^{\infty} a_n^+, \quad \sum_{m=1}^{\infty} b_m^- = \sum_{n=1}^{\infty} a_n^-.
$$ then by proposition 3.1 we have $\sum b_{m}$ is absolutely convergent and $$
\sum_{m=1}^\infty b_m = \sum_{m=1}^\infty b_m^+ - \sum_{m=1}^\infty b_m^- = \sum_{n=1}^\infty a_n^+ - \sum_{n=1}^\infty a_n^- = \sum_{n=1}^\infty a_n,
$$

**Theorem 7.2** if a series is conditionally convergent, then it has rearrangement that converge to any real number.

