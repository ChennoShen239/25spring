# Lecture 8
> This is the lecture note for MATH 104, which should be used together with [[Ch8.pdf]]

> [!PDF|yellow] [[Ch8.pdf#page=1&selection=133,0,148,1&color=yellow|Ch8, p.1]]
> > The convergence is uniform on every interval |x| < ρ where 0 ≤ ρ < R.
>
> you see the difference? you need to specify a $\rho$ instead of directly using an $R$

> [!PDF|yellow] [[Ch8.pdf#page=2&selection=274,35,274,81&color=yellow|Ch8, p.2]]
> > very power series has a radius of convergence.
>
> The key is that everyone has it!

Check the key results!
1. the series converges absolutely for $\lvert x-c \rvert<R$
2. diverges for $\lvert x-c \rvert>R$
3. for the given $\rho \in[0,R)$
	1. the series converges uniformly on $\lvert x-c \rvert<\rho$
	2. the sum of series is continuous on $\lvert x-c \rvert<\rho$
#### 证明（设 $c = 0$ 无损一般性）

假设幂级数 $\sum_{n=0}^{\infty} a_n x^n$ 在某个 $x_0 \ne 0$ 上收敛。因为收敛，所以级数的项趋于零，因此它们有界，存在常数 $M \geq 0$，使得：

$$
|a_n x_0^n| \leq M \quad \text{对所有 } n = 0, 1, 2, \dots
$$

若 $|x| < |x_0|$，则：

$$
|a_n x^n| = |a_n x_0^n| \left|\frac{x}{x_0}\right|^n \leq M r^n \quad \text{其中 } r = \left|\frac{x}{x_0}\right| < 1
$$

因为 $\sum M r^n$ 是收敛的几何级数，所以 $\sum a_n x^n$ 绝对收敛。

于是，如果级数在某个 $x_0 \in \mathbb{R}$ 上收敛，则在所有 $|x| < |x_0|$ 上都绝对收敛。

令：

$$
R = \sup \left\{ |x| \geq 0 : \sum a_n x^n \text{ 收敛} \right\}
$$

- 若 $R = 0$，则级数仅在 $x = 0$ 收敛；
- 若 $R > 0$，则级数在 $|x| < R$ 内绝对收敛，并在 $|x| > R$ 时发散；
- 若 $R = \infty$，则该级数在所有实数 $x$ 上都收敛。

最后，设 $0 \leq \rho < R$ 且 $|x| \leq \rho$。**选取一个 $\sigma > 0$，使得 $\rho < \sigma < R$**。由于 $\sum |a_n \sigma^n|$ 收敛，存在 $M$ 使得：

$$
|a_n \sigma^n| \leq M
$$

于是：

$$
|a_n x^n| = |a_n \sigma^n| \left| \frac{x}{\sigma} \right|^n \leq M r^n, \quad \text{其中 } r = \frac{\rho}{\sigma} < 1
$$

由于几何级数 $\sum M r^n$ 收敛，因此由 $M$-检验（第 5.2 定理），该级数在 $|x| \leq \rho$ 上一致收敛。又根据定理 9.16，级数和函数在 $|x| \leq \rho$ 上连续。

由于这对任意 $0 \leq \rho < R$ 成立，故级数和函数在 $|x| < R$ 上连续。

###  M 检验（Weierstrass M-test）

设 $\{f_n(x)\}$ 是定义在集合 $D$ 上的一列函数。如果存在一个数列 $\{M_n\}$ 满足：

- 对所有 $x \in D$，都有 $|f_n(x)| \leq M_n$；
- 数项级数 $\sum_{n=0}^{\infty} M_n$ 收敛；

那么函数级数 $\sum_{n=0}^{\infty} f_n(x)$ 在 $D$ 上一致收敛。

---

###  定理 9.16（函数列一致收敛 $\Rightarrow$ 极限函数连续）

设：

- 每个 $f_n : D \to \mathbb{R}$ 都是连续函数；
- 且 $\sum_{n=0}^{\infty} f_n(x)$ 在 $D$ 上一致收敛于函数 $f(x)$；

则 $f(x)$ 在 $D$ 上是连续函数。


> [!PDF|red] [[Ch8.pdf#page=3&selection=504,51,516,1&color=red|Ch8, p.3]]
> > lso note that a power series need not converge uniformly on |x − c| < R.
>
> Keep in mind that 3.1 is different from 1!

> [!PDF|yellow] [[Ch8.pdf#page=3&selection=74,27,103,1&color=yellow|Ch8, p.3]]
> > hus, if the power series converges for some x0 ∈ R, then it converges absolutely for every x ∈ R with |x| < |x0|.
>
> The key in proving the convergence is to prove that given $x_{0}$, all $x \in[0,x_{0})$ converges absolutely

> [!PDF|red] [[Ch8.pdf#page=3&selection=341,6,354,0&color=red|Ch8, p.3]]
> > then it follows from Theorem 9.16 that the sum is continuous on |x| ≤ ρ
>
> If a sequence of continuous functions ($f_{n}$) converges uniformly to a function $f$ on an interval, then the limit function $f$ is also continuous on that interval.


> [!PDF|yellow] [[Ch8.pdf#page=4&selection=0,12,54,1&color=yellow|Ch8, p.4]]
> > Theorem 2.2. Suppose that an̸ = 0 for all sufficiently large n and the limit R = lim n→∞ an an+1 exists or diverges to infinity. Then the power series ∞X n=0 an(x − c)n has a radius of convergence R.
>
> The key is to implement **the ratio test**
>
> $$
> L = \lim_{  n \to \infty } \left\lvert  \frac{a_{n+1}}{a_{n}}  \right\rvert <1
> $$
>
> Then $\sum_{i=1}^{\infty}a_{n}$ converges absolutely

> [!PDF|yellow] [[Ch8.pdf#page=4&selection=159,0,222,19&color=yellow|Ch8, p.4]]
> > Theorem 2.3 (Hadamard). The radius of convergence R of the power series ∞X n=0 an(x − c)n is given by R = 1 lim supn→∞ |an|1/n where R = 0 if the limsup diverges to ∞, and R = ∞ if the limsup is 0.
>
> This one is crucial!

Basically this is just the root test to determine an $r =\lim_{ n \to \infty }\sup{\lvert a_{n}(x-c)^{n} \rvert^{1/n}}=\lvert x-c \rvert\lim_{ n \to \infty }\sup{\lvert a_{n} \rvert}^{1/n}$

then the goal is to let this $r<1$.

---

> [!PDF|yellow] [[Ch8.pdf#page=5&selection=145,0,146,0&color=yellow|Ch8, p.5]]
> > Proposition 3.1.
>
> These properties hold within the $T= \min \left\{ R,S \right\}$ but  the radius of convergence for the new series may be larger.

有时，$f + g$ 或 $fg$ 的幂级数的收敛半径可能大于 $f$ 和 $g$ 各自幂级数的收敛半径。

例如，如果 $g = -f$，那么 $f + g = 0$，它的幂级数恒为零，因此无论 $f$ 的幂级数收敛半径是多少，$f + g$ 的幂级数的收敛半径都是 $\infty$。

此外，如果一个幂级数在其中心点处不为零且收敛，那么它的**倒数函数**（即 $1/f$）也可以展开成一个幂级数。


> [!PDF|yellow] [[Ch8.pdf#page=6&selection=44,0,45,29&color=yellow|Ch8, p.6]]
> > The reciprocal of a convergent power series that is nonzero at its center also has a power series expansion.
>
> We now try to solve for the new coefficients

we know that $$
f(x) = \sum_{i=0}^{\infty}  a_{i} x^{i}

$$
and $f(0)\neq{0}$, so we know there is a
$$

f(x) \cdot \frac{1}{f(x)} =1

$$
then lets think of $1$ as a series, then we know $c_{0}=1,c_{i\geq 0} =0$. We set $$
\frac{1}{f(x)} = \sum_{n=0}^{\infty}b_{n}x^{n} 
$$

then we know for the product,

$$
c_{n} = \sum_{k=0}^{n} a_{n-k}b_{k}
$$

for $n=0$, we have $$
a_{0}b_{0} = 1,b_{0} = \frac{1}{a_{0}}

$$
then for all $n>0$, we know
$$

0 = \sum_{k=0}^{n}  a_{n-k}b_{k}

$$
assume we have known $\left\{ b_{k} \right\}_{k=0}^{n-1}$, then the new $b_{n}$ can be obtained simply from $$
b_{n} a_{0} + \sum_{k=0}^{n-1} a_{n-k}b_{k}=0\implies b_{n} =-\frac{1}{a_{0}}\sum_{k=0}^{n-1} a_{n-k}b_{k}
$$

> But still no information about the $\frac{1}{f}$'s radius of convergence!


> [!PDF|yellow] [[Ch8.pdf#page=6&selection=129,0,177,1&color=yellow|Ch8, p.6]]
> > Theorem 4.1. Suppose that the power series ∞X n=0 an(x − c)n has a radius of convergence R. Then the power series ∞X n=1 nan(x − c)n−1 also has a radius of convergence R.
>
> i.e. the derivative of a convergent series has the same radius of convergence $R$

For the proof of it, we need to separate the sequence into 2 terms:
1. $nr^{n-1}$ : this is guaranteed by the ratio test
2. $\lvert a_{n}\rho^{n} \rvert$: this is guaranteed by the definition of the radius of convergence.

then we combine the 2 terms:
let 

$$
r = \lvert x \rvert /\rho ,r \in(0,1)
$$
Then the original $\sum_{i=1}^{\infty}\lvert na_{n}x^{n-1} \rvert$  will become:
$$
\lvert na_{n}x^{n-1} \rvert = n \lvert a_{n} (r\rho)^{n-1} \rvert = \underbrace{ \frac{n}{\rho} }_{ \text{ constant} } \overbrace{ nr^{n-1}  }^{ \text{ratio test} }\underbrace{ \lvert a_{n}\rho^{n} \rvert  }_{ \text{assumption }\rho <R }
$$

> [!PDF|yellow] [[Ch8.pdf#page=6&selection=277,0,277,19&color=yellow|Ch8, p.6]]
> > The ratio test show
>
> Notice that we're talking about $\sum_{n=0}^{\infty}nr^{n-1}$ instead of $\sum_{n=1}^{\infty}na_{n}x^{n-1}$

Then the convergence gives boundedness: $\left\{ nr^{n-1} \right\}_{n=0}^{\infty}$ is bounded by $M$
- given $\sum_{n=0}^{\infty}\lvert a_{n}\rho^{n} \rvert$ converges (by definition)
- then we know

$$
\lvert na_{n}x^{n-1} \rvert \leq \frac{M}{\rho} \lvert a_{n}\rho^{n} \rvert \implies \sum_{n=0}^{\infty}  n a_{n} x^{n-1}   \text{ converges abs.}
$$

> [!PDF|yellow] [[Ch8.pdf#page=7&selection=144,0,146,29&color=yellow|Ch8, p.7]]
> > Theorem 4.2. Suppose that the power series
>
> It exists, we have one , it should be equal: $f'=g$
> But notice the steps:
> 1. this holds for $0<\rho<R$
> 2. this holds for $\forall \rho<R \implies [0,R)$
### 定理 4.3：幂级数的可导性与系数表达式

设函数 $f(x)$ 可以表示为幂级数：

$$
f(x) = \sum_{n=0}^{\infty} a_n(x - c)^n
$$

且其收敛半径为 $R > 0$。那么：

1. **在区间 $|x - c| < R$ 内，$f(x)$ 是无限次可导的**；
2. **每一阶导数都可以通过对幂级数逐项求导得到**；
3. **每一项的系数 $a_n$ 满足**：

$$
a_n = \frac{f^{(n)}(c)}{n!}
$$

这说明：幂级数的系数 $a_n$ 正是函数 $f(x)$ 在 $x = c$ 处的第 $n$ 阶导数除以 $n!$，即 $f(x)$ 的**泰勒展开系数**。

---


> [!PDF|yellow] [[Ch8.pdf#page=7&selection=373,4,373,28&color=yellow|Ch8, p.7]]
> > nfinitely differentiable
>
> with the same $R$


> [!PDF|yellow] [[Ch8.pdf#page=7&selection=394,0,460,1&color=yellow|Ch8, p.7]]
> > Theorem 4.3. If the power series f (x) = ∞X n=0 an(x − c)n has radius of convergence R > 0, then f is infinitely differentiable in |x − c| < R and an = f (n)(c) n!
>
> This one is interesting!

The Taylor expansion results come directly from setting $x=0(c)$

> [!PDF|yellow] [[Ch8.pdf#page=8&selection=303,0,365,1&color=yellow|Ch8, p.8]]
> > Corollary 4.1. If two power series ∞X n=0 an(x − c)n, ∞X n=0 bn(x − c)n have nonzero-radius of convergence and are equal in some neighborhood of 0 , then an = bn for every n = 0, 1, 2, . . ..
>
> The corollary shows that if $f=g$ then we must have this one-to-one 
> $$a_{n} = b_{n} = \frac{f^{(n)}(c)}{n!}$$
	

> [!PDF|yellow] [[Ch8.pdf#page=9&selection=73,0,101,1&color=yellow|Ch8, p.9]]
> > Proposition 5.1. For every x, y ∈ R, E(x)E(y) = E(x + y).
> 
> Very quick thought: use $c_{n} = \sum_{k=0}^{n}a_{n-k}b_{k}$

> [!PDF|yellow] [[Ch8.pdf#page=10&selection=0,16,20,1&color=yellow|Ch8, p.10]]
> > Proposition 5.3. Suppose that n is a non-negative integer. Then lim x→∞ xn ex = 0.
> 
> This is the fact that $\exp(x)$ has the higher order than any polynomial

