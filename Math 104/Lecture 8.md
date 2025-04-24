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
> The key is to implement the ratio test
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

> [!PDF|yellow] [[Ch8.pdf#page=5&selection=145,0,146,0&color=yellow|Ch8, p.5]]
> > Proposition 3.1.
>
> These properties hold within the $T= \min \left\{ R,S \right\}$ but  the radius of convergence for the new series may be larger.


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

For the proof of it,

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

