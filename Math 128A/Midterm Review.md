# Lecture 1
**Extreme Value Theorem**: let $f$ be a continuous function on $[a,b]$, then $\exists c,d\in [a,b]$  such that $$
f(d) \leq f(x)\leq f(c)\quad \forall x \in [a,b]
$$
**Mean Value Theorem**: Let $f$ be 
1. continuous on $[a,b]$
2. differentiable on $(a,b)$
then there $\exists c\in (a,b)$ such that $$
f'(c) = \frac{f(a)-f(b)}{a-b}
$$
**Intermediate Value Theorem**:
Let $f$ be a function such that:
3. $f$ is continuous on $[a,b]$
4. $k$ is any real number between $f(a)$ and $f(b)$
then $\exists x \in(a,b)$ such that $$
f(x) = k
$$
**Binary Machine Numbers**
A non-zero double-precision floating point number is represented as: $$
x = (-1)^{s}2^{c-1023}(1+f)
$$
we have:
- sign bits $s$
- characteristic $c$: $$
c = \sum_{i=1}^{11} c_{i}\cdot 2^{11-i}
$$
- mantissa $f$: $$
f = \sum_{i=1}^{52} f_{i} \left( \frac{1}{2} \right)^{i}
$$
- total $1+11+ 52 = 64$ bits.

**Round-off errors**
For a positive real number:

$$y = 0.d_1d_2\cdots d_kd_{k+1}d_{k+2}\cdots \times 10^n,$$

- Chopping:
$$fl(y) = 0.d_1d_2\cdots d_k \times 10^n.$$

- Rounding:
$$fl(y) = 0.\delta_1\delta_2\cdots\delta_k \times 10^n,$$
where rounding is performed as follows:
- if $d_{k+1} < 5$ , rounding equals to chopping
- otherwise, add $1$ to $d_{k}$ and truncate at $d_{k}$.

**Relative Error for k-Digit Rounding**
let $y = 0.d_{1}d_{2}\dots d_{k}d_{k+1}\dots \times 10^{n}$, where $d_{1} \geq 1$. then let $f(y)$ be the **rounded** value.
- if $d_{k+1}<5$, then $|y-f(y)| = 0.00\dots 0d_{k+1}\dots \times 10^{n}\leq 0.499 \times 10^{n-k}$ 
- if $d_{k+1} \geq 5$, then $|y-f(y)| = 0.00\dots 0 (10-d_{k+1})\dots \times 10^{n}\leq 0.5 \times 10^{n-k}$
so we have the maximum absolute error: $$
|y -f (y)|\leq 0.5 \times 10^{n-k}
$$
**the maximum relative error** $$
\frac{|y-f(y)|}{|y|} \leq \frac{0.5 \times 10^{n-k}}{0.1\times 10 ^{n}} = 0.5 \times 10 ^{-k + 1}
$$
# Lecture 2
**Quadratic formulas** for $ax^{2 }+ bx + c = 0$:
$$
x_{1,2} = \frac{-b \pm \sqrt{ b^{2} - 4ac }}{2a}
$$
but if $|4ac| \ll b^{2}$, then one of the roots will be $0$. A better approach is:
1. let $\delta  = \sqrt{ b^{2} - 4ac }$
2. let $$
x_{1 } = \begin{cases}
-\frac{b + \delta}{2a} & b>0 \\
\frac{-b + \delta}{2a} & b\leq 0 \\

\end{cases}
$$
3. use Vieta's formula $$
x_{2} = \frac{c}{ax_{1}}
$$

**Horner's method**
let $f(x)$ be evaluated for a given $x$:
$$
\begin{align}
f(x)  & = \sum_{i=1}^{n} a_{i}x^{i-1} \\
 &  = a_{1} + x(a_{2} + x(\dots+x(a_{n-1}+ xa_{n}))) 
\end{align}
$$
