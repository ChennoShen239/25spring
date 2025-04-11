### Gaussian Quadrature
- Given $n > 0$, choose both distinct nodes $x_1, \cdots, x_n \in [-1, 1]$ and weights $c_1, \cdots, c_n$, so quadrature
$$\int_{-1}^{1} f(x) dx \approx \sum_{j=1}^{n} c_j f(x_j),\tag{1}$$
gives the greatest degree of precision (DoP).
- $2n$ parameters, allowing exact quadrature for $2n$ monomials
$$\int_{-1}^{1} f(x) dx = \sum_{j=1}^{n} c_j f(x_j), \quad \text{for} \quad f(x) = 1, x, x^2, \cdots, x^{2n-1}\tag{2}$$
directly solving (2) can be very hard. But for $n = 2$,
$$\int_{-1}^{1} f(x) dx \approx f\left(-\frac{1}{\sqrt{3}}\right) + f\left(\frac{1}{\sqrt{3}}\right)$$
- exact for $f(x) = 1, x, x^2, x^3$,
- not for $f(x) = x^4$.
exactly for **cubic**![[Screenshot 2025-03-31 at 20.26.45.png]]

### Gaussian Quadrature by Legendre polynomials:
Let $P_0(x) = 1, P_1(x) = x,$
$$(n + 1)P_{n+1}(x) = (2n + 1)xP_n(x) - nP_{n-1}(x)$$ for $n \geq 1.$

- $P_n(x)$ has degree $n$, always with $n$ distinct roots $x_1, x_2, \cdots, x_n \in (-1, 1)$
- MUTUALLY ORTHOGONAL:
$$\int_{-1}^{1} P_n(x)P_j(x)\,dx = 0,\quad$$ for $j < n$ , or equivalently $$
\int _{-1}^{1}P_{n}(x)Q(x) \, dx  = 0 \text{ for } \mathbf{deg}(Q) \leq n-1 \tag{1}
$$
**Thm:** $\int_{-1}^{1} P_n(x)Q(x)\,dx = 0$ for any $Q(x)$ with degree $< n$

Gaussian quadrature: 
$$\int_{-1}^{1} f(x)\,dx \approx c_1f(x_1) + c_2f(x_2) + \cdots + c_nf(x_n),\quad c_i \overset{\text{def}}{=} \int_{-1}^{1} L_i(x)\,dx$$
quadrature exact for polynomial with degree $\leq n - 1$

**Thm**: Gaussian Quadrature DoP = $2n-1$

Proof of **Thm**:

Let $P(x)$ have $\mathbf{deg}\leq 2n-1$, then we can get $$
P(x)  = P_{n}(x)Q(x) + R(x),\quad \mathbf{deg} \text{ of }Q(x),R(x) \leq n-1 \tag{2}
$$
Therefore $$
\begin{align}
		\int _{-1}^{1}P(x) \, dx  &  = \int _{-1}^{1}(P_{n }Q + R) \, dx  \tag{from (2)}\\
 & = \int _{-1}^{1} R \, dx \tag{from (1)}\\
 & = \sum_{i=1}^{n} c_{i}R(x_{i})  \tag{Gaussian quadrature}\\
 &  = \sum_{i=1}^{n }  c_{i}P(x_{i})  \tag{Legendre nodes}
\end{align}

$$
The last equation comes from the simple fact that $\left\{ x_{i} \right\}_{i=1}^{n}$ are the $n$ roots of $P_{n}(x)$.

### Hermite Interpolation on roots of Legendre polynomials

- Given Legendre roots $\left\{ x_{i} \right\}_{i=1}^{n}$ with $\left\{ \left( x_{i},f(x_{i}),f'(x_{i}) \right) \right\}_{i=1}^{n}$,
- Interpolating polynomial $H(x)$ of degree $\leq 2n-1$ satisfies:
$$
H(x_{j}) =f(x_{j})\quad H'(x_{j}) = f'(x_{j}),\quad \forall j=1,\dots ,n
$$
- recall theorem for each $x \in[a,b]$, there exists $\xi(x)\in[a,b]$ such that $$
\begin{align}
R(x) & := f(x) - H(x) \\
 & = \frac{f^{(2n)}(\xi(x))}{(2n)!} \prod_{i=1}^{n} (x-x_{i})^{2} 
\end{align}
$$
- then we integrate $f$ over $[-1,1]$:
$$
\begin{align}
\int _{-1}^{1}f(x) \, dx  &  = \int _{-1}^{1}H(x) \, dx + \int _{-1}^{1}R(x) \, dx \\
 & = \sum_{i=1}^{n} c_{i}H (x_{i}) + \int _{-1}^{1}R(x) \, dx \\
 &  = \sum_{i=1}^{n} c_{i}H (x_{i})  + \int _{-1}^{1}\frac{f^{(2n)}(\xi(x))}{(2n)!} \prod_{i=1}^{n} (x-x_{i})^{2}  \, dx  \\
 & = \sum_{i=1}^{n} c_{i}H (x_{i})  + \underbrace{ \frac{f^{(2n)}(\xi)}{(2n)!} \int_{-1}^{1} \prod_{i=1}^{n} (x-x_{i})^{2} \, dx  }_{ \text{defined as } \mathbf{R}}
\end{align}

$$
- take one step further, we have:
$$\begin{align}
\mathbf{R}  &  =\frac{f^{(2n)}(\xi)}{(2n)!} \int_{-1}^{1} \prod_{i=1}^{n} (x-x_{i})^{2} \, dx  \\
\end{align}

$$
- Now we use the property of Legendre polynomials. Let $P_{n}(x)=c_{n}\prod_{i=1}^{n}(x-x_{i})$, then we know we just trying to find out $$
		I = \int_{-1}^{1}\prod_{i=1}^{n} (x-x_{i})^{2}  \, dx  =\int _{-1}^{1} \left[  \frac{P_{n}(x)}{c_{n}}\right]^{2} \, dx 
$$
- given orthogonality, we have $$
\int _{-1}^{1}P_{m}P_{j} \, dx = \begin{cases}
0 & m \neq j \\
\frac{2}{2m+1} & o.w.
\end{cases}
$$
- By the **Rodrigues Formula,** we have $$
\begin{align}
P_{n}(x) &  = \frac{1}{2^{n}n!} \frac{d^{n}}{dx^{n}}\left[ (x^{2}-1)^{n} \right]  \\
 & = c_{n} \prod_{i=1}^{n} (x- x_{n})
\end{align}
$$
therefore $c_{n}$ is the coefficient of the $x^{n}$ term in $P_{n}$, just the $x^{2n}$ term after taking $n$ derivatives, i.e. $$
\begin{align}  c_{n}  &  = \frac{1}{2^{n}n!} (2n)(2n-1)\dots (n+1)\\ &  = \frac{(2n)!}{2^{n}(n!)^{2}}
\end{align}
$$
- then let's substitute this into the integral  $$
\begin{align}
\mathcal{I}  & =\frac{1}{c_{n}^{2}} \int _{-1}^{1}\left[ P_{n}(x) \right] ^{2} \, dx  \\
 & = \frac{2}{2n+1} \frac{2^{2n}(n!)^{4}}{((2n)!)^{2}} \\
 & = \frac{2\cdot2^{2n}(n!)^{3} (n-1)!}{(2n+1)!(2n-1)!}
\end{align}
$$
- and therefore the $\mathbf{R}$:
$$
\begin{align}
\mathbf{R} &  = \frac{f^{(2n)}(\xi)}{(2n)!} \frac{2\cdot2^{2n}(n!)^{3} (n-1)!}{(2n+1)!(2n-1)!} \\
 &  = f^{(2n)}(\xi) \frac{2^{2n}(n!)^{3} (n-1)!}{(2n+1)!(2n)!(2n-1)!} \\
 &  = O\left( \frac{4^{-n}\left| f^{(2n)}(\xi) \right| }{(2n)!} \right)
\end{align}
$$
- So this is quite rapid convergence for smooth functions
> it's easier to understand that $$
\frac{(n!)^{3}(n-1)!}{(2n+1)!(2n-1)!}
$$quickly converge to 0 since basically they have the same numbers but decays in geometric rate. The rest of the $\mathbf{R}$ will not decay and therefore remains in the $O$ part

**Gaussian Quadrature good for given $n$, Simpson good for given tolerance.**


### Double Integral = Integral of Integral function

$$\int\int_R f(x,y) dA = \int_a^b \left( \int_c^d f(x,y) dy \right) dx$$
$$= \int_a^b g(x) dx, \text{ with } g(x) \overset{\text{def}}{=} \int_c^d f(x,y) dy$$

General approach in a nutshell

> Approximate $\int_a^b g(x) dx$ with ANY quadrature
$$\int_a^b g(x) dx \approx c_1 g(x_1) + c_2 g(x_2) + \cdots + c_n g(x_n)$$

> For each node $x_i$, approximate $g(x_i) = \int_c^d f(x_i, y) dy$ with ANY quadrature.

Rest is book keeping: work out 2D quadrature / error estimate

Ok let's get started:
1. first approximate $\int _{a}^{b}g(x) \, dx = \sum_{i=1}^{n}c_{i}g(x_{i})+\mathbf{R}(g)$
2. for $1\leq i\leq n$, approximate $g(x_{i})$ with m-point quadrature $$
g(x_{i}) = \int_{c}^{d}f(x_{i},y)  \, dy = \sum_{i=1}^{n} \hat{c_{i}}f(x_{1},y_{1}) + \mathbf{\hat{R}}(f(x_{i},\cdot))
$$
3. so the quadrature will be like: $$
\begin{align}
\iint_{\mathbb{R}}f(x,y)dA & = \int_{a}^{b}g(x) \, dx  \\
 & = \sum_{i=1}^{n} c_{i}g(x_{i}) + \mathbf{R}(g) \\
 & =\sum_{i=1}^{n} c_{i}\left( \sum_{j=1}^{n} \hat{c}_{j}f(x_{i},y_{j})+\mathbf{\hat{R} }(f(x_{i},\cdot)) \right) + \mathbf{R }(g)\\
 & =\underbrace{ \sum_{i=1}^{n} \sum_{j=1}^{n} c_{i} \hat{c}_{j}f(x_{i},y_{j}) }_{ \text{2D quadrature} } + \underbrace{ \left( \sum_{i=1}^{n} \mathbf{R}(f(x_{i},\cdot)) \right) + \mathbf{R }(g) }_{ \text{error estimate} }
\end{align}
$$
Let $R = \left[ a,b \right]\times \left[ c,d \right]$, by Simpson's Rule we'll have $$
\begin{align}
(x_{1},x_{2},x_{3  }) & =\left( a, \frac{a+b}{2},b \right) \\
(y_{1},y_{2},y_{3})  & = \left( c, \frac{c+d}{2},d \right)
\end{align}
$$
> here let's review about the Simpson's rule: 
> - for the simple Simpson's rule, we just take 3 points and assign them weights as $\left( \frac{1}{6}h, \frac{4}{6}h, \frac{1}{6}h \right)$
> - for the *composite Simpson's rule*, we basically divide the $[a,b]$ into $n$ equal-spaced intervals and apply the simple Simpson's rule to each. In the end the approximation will look like this $$
	\int _{a}^{b} f(x)\, dx =\frac{h}{3} \left[ f(x_{0}) + 4\sum_{i=1,odd}^{n-1} f(x_{i}) + 2 \sum_{i=2,even}^{n-2}f (x_{i}) + f(x_{n})  \right]
$$where we have $h = \frac{b-a}{n},x_{i} = a+i h$


$$m=n=3, g(x) \overset{\text{def}}{=} \int_c^d f(x,y) dy$$

Simpson's Rule on $[a,b]$:
$$(x_1, x_2, x_3) = (a, \frac{a+b}{2}, b).$$
$$\int_a^b g(x) dx = c_1 g(x_1) + c_2 g(x_2) + c_3 g(x_3) - \frac{h^5}{90} g^{(4)}(\xi),$$
$$h = \frac{b-a}{2}, \quad (c_1, c_2, c_3) = \frac{h}{3}(1, 4, 1).$$
> just keep in mind there's a $-\frac{h^{5}}{90}g^{(4)}(\xi)$ !

> to simply derive this:
> 真实积分为：
> $$I = 2h g(m) + \frac{h^3}{3} g''(m) + \frac{h^5}{60} g^{(4)}(m) + \cdots.$$
> Simpson公式采用三点插值，其公式（写成 $h=\frac{b-a}{2}$）为
> $$S = \frac{h}{3}\left[g(m-h) + 4g(m) + g(m+h)\right].$$
> 对$g(m\pm h)$也做泰勒展开：
> $$g(m\pm h) = g(m) \pm hg'(m) + \frac{h^2}{2}g''(m) \pm \frac{h^3}{6}g'''(m) + \frac{h^4}{24}g^{(4)}(m) + \cdots.$$
> 将$g(m-h)$和$g(m+h)$相加，可以得到：
> $$g(m-h) + g(m+h) = 2g(m) + h^2g''(m) + \frac{h^4}{12}g^{(4)}(m) + \cdots.$$
> 因此Simpson公式变为：
> $$S = \frac{h}{3}\left[2g(m) + h^2g''(m) + \frac{h^4}{12}g^{(4)}(m) + 4g(m)\right] = \frac{h}{3}\left[6g(m) + h^2g''(m) + \frac{h^4}{12}g^{(4)}(m)\right].$$
> 即
> $$S = 2h g(m) + \frac{h^3}{3} g''(m) + \frac{h^5}{36} g^{(4)}(m) + \cdots.$$
> 现在比较真实积分$I$和Simpson近似$S$的差异：
> $$I - S = \left(2h g(m) + \frac{h^3}{3} g''(m) + \frac{h^5}{60} g^{(4)}(m) + \cdots\right) - \left(2h g(m) + \frac{h^3}{3} g''(m) + \frac{h^5}{36} g^{(4)}(m) + \cdots\right).$$
> 因此主要的差别来自四次项：
> $$I - S = \left( \frac{1}{60} - \frac{1}{36} \right) h^5 g^{(4)}(m) + \cdots$$
> 计算系数：
> $$\frac{1}{60} - \frac{1}{36} = \frac{6-10}{360} = -\frac{4}{360} = -\frac{1}{90}$$
> 所以误差为
> $$I - S = -\frac{h^5}{90} g^{(4)}(m) + \cdots$$
> 由于实际情况中 $g^{(4)}$ 的取值可能在整个区间内变化，根据中值定理，我们可引入一个介于$a$ 和$b$之间的点 $\xi$ 来表示：
> $$I - S = -\frac{h^5}{90} g^{(4)}(\xi)$$
> 这就是Simpson公式中误差项的由来。误差项表明Simpson公式在积分时对四阶及更高阶的项会产生误差，其大小与$h^5$ 和$g^{(4)}$ 的值成正比。

Simpson's Rule on $[c,d]$:
$$(y_1, y_2, y_3) = (c, \frac{c+d}{2}, d).$$
$$g(x_i) = \int_c^d f(x_i, y) dy = \widehat{c}_1 f(x_i, y_1) + \widehat{c}_2 f(x_i, y_2) + \widehat{c}_3 f(x_i, y_3) - \frac{k^5}{90} \frac{\partial^4 f}{\partial^4 y}(x_i, \eta_i),$$
$$k = \frac{d-c}{2}, \quad (\widehat{c}_1, \widehat{c}_2, \widehat{c}_3) = \frac{k}{3}(1, 4, 1).$$
$$
\begin{aligned}
 \iint_Rf(x,y)dA&=\left(\sum_{i=1}^n\sum_{j=1}^mc_i\hat{c}_jf(x_i,y_j)\right) -\frac{k^4(d-c)}{180}\left(\sum_{i=1}^mc_i\frac{\partial^4f}{\partial^4y}(x_i,\eta_i)\right)-\frac{h^4(b-a)}{180}\int_c^d\frac{\partial^4f}{\partial^4x}(\xi,y)dy \\
 & =\left(\sum_{i=1}^n\sum_{j=1}^mc_i\hat{c}_jf(x_i,y_j)\right)  -\frac{k^4(d-c)}{180}\left(\underbrace{ \sum_{i=1}^mc_i }_{ \text{sum to }(b -a ) }\underbrace{ \frac{\partial^4f}{\partial^4y}(\hat{x},\hat{y}) }_{ \text{independent of } i}\right)-\frac{h^4(b-a)}{180}\underbrace{ (d-c)\frac{\partial^4f}{\partial^4x}(\xi,\eta)  }_{ \text{MVT for integrals} }\\
 & =\sum_{i=1}^n\sum_{j=1}^mc_i\hat{c}_jf(x_i,y_j)  -\underbrace{ \frac{(b-a)(d-c)}{180}\left(k^4\frac{\partial^4f}{\partial^4y}(\hat{x},\hat{y})+h^4\frac{\partial^4f}{\partial^4x}(\xi,\eta)\right). }_{ \text{error term} }
\end{aligned}
$$


- **Error bounds** can be derived from here. For example:
$$\int \int_R \log(x + 2y) \, dA$$ with $n = 7$, $m = 5$

$$R = \{(x,y) | 1.2 \leq x \leq 2.4, 0.2 \leq y \leq 1, \}$$
$$h = \frac{2.4 - 1.2}{7-1} = 0.2, k = \frac{1 - 0.2}{5-1} = 0.2.$$
$$\frac{\partial^4 f}{\partial^4 x} = -\frac{6}{(x+2y)^4}, \quad \frac{\partial^4 f}{\partial^4 y} = -\frac{96}{(x+2y)^4}.$$
$$\left| \frac{\partial^4 f}{\partial^4 x} \right| \leq \frac{6}{(1.2 + 2 \times 0.2)^4} \approx 0.91553$$ for $(x,y) \in R,$
$$\left| \frac{\partial^4 f}{\partial^4 y} \right| \leq \frac{96}{(1.2 + 2 \times 0.2)^4} \approx 14.648.$$
$$
\begin{align}
Quad\_Error  & = \frac{(b-a)(d-c)}{180} \Biggl[ k^4 \frac{\partial^4 f}{\partial^4 y}(\xi, \eta) + h^4 \frac{\partial^4 f}{\partial^4 x}(\xi, \eta) \Biggr]  \\
 & \leq \frac{(2.4-1.2)(1-0.2)}{180} (0.2^4 \times 14.648 + 0.2^4 \times 0.91553) \\
 & \approx 1.328 \times 10^{-4}
\end{align}
$$
> theoretical error bound
### 2D Gaussian Quadratures

We have the definition $$
R = [a,b]\times[c,d]$$
and the integral we want is $$
\iint_{R}f(x,y)dA
	$$
we do a simple substitution $$
x  =\frac{a+b}{2}+\frac{b-a}{2}u,\quad y=\frac{c+d}{2}+\frac{d-c}{2}v\quad\mathrm{for}\quad u,v\in[-1,1]. 
$$
then double integral becomes $$
\begin{align}
\iint_{R}fdA  & = \frac{(b-a)(d-c)}{4}\int_{-1}^{1}\hat{g}(u)  \, du \\
 & = \frac{(b-a)(d-c)}{4} \int _{-1}^{1}\underbrace{ \int _{-1}^{1}f(x(u),y(v)) \, dv }_{ \hat{g}(u) }  \, du 
\end{align}
$$
- **n-points** the Gaussian quadrature for $\int _{-1}^{1}\hat{g}(u) \, du$ is $\sum_{i=1}^{n}c_{i}\hat{g}(u_{i})$
- for $1\leq i\leq n$, let $$
x_{i} = \frac{a+b}{2} + \frac{b-a}{2}u_{i}, \hat{g}(u_{i})= \int _{-1}^{1}f(x_{i},y(v)) \, dv 
$$
- **m-points** the Gaussian quadrature for $\hat{g}(u_{i})$ is $$
\sum_{j=1}^{m} \hat{c}_{j}f\left( x_{i}, \underbrace{ \frac{c+d}{2} + \frac{d-c}{2}v_{j} }_{ y_{j} } \right)
$$
- the whole Gaussian quadrature is $$
\iint_{R} fdA \approx \frac{(b-a)(d-c)}{4} \sum_{i=1}^{n} \sum_{j=1}^{m} c_{i}\hat{c}_{j}f(x_{i},y_{j})
$$
**Gaussian quadrature is more accurate**
> additional calculation:
> - to calculate the weights $c_{j}$ s we can use this formula $$
c_{i} = \frac{2}{(1-x_{j}^{2})[P_{n}'(x_{j})]^{2}}
$$where $x_{j}$ are the roots for the Legendre polynomials
> - it seems that we'll be given the table?

## Initial Value ODE

### Lipschitz condition

**Definition**: function $f(t, y)$ satisfies a Lipschitz condition in the variable $y$ on a set $D \subset \mathbb{R}^2$ if a constant $L > 0$ exists with
$$|f(t, y_1) - f(t, y_2)| \leq L |y_1 - y_2|,$$
whenever $(t, y_1), (t, y_2)$ are in $D$. $L$ is Lipschitz constant.
> you can't be forgetting this after the review of the conflict cost paper

**Example** 1: Show that $f(t, y) = t|y|$ satisfies a Lipschitz condition on the region
$$D = \{(t, y) \mid 0 \leq t \leq T\}.$$

Solution: For any $(t, y_1), (t, y_2)$ in $D$,
$$|f(t, y_1) - f(t, y_2)| = |t|y_1| - t|y_2|| \leq t |y_1 - y_2| \leq L |y_1 - y_2|,$$
for $L = T$.
**Example** 2: to show Lipschitz condition is not satisfied on $D=\left\{ (t,y)|0\leq t\leq T \right\}$ for $f = ty^{2}$. 
Solution: just note that $$
\lvert f(t,y_{1}) - f(t,y_{2}) \rvert  = t \lvert y_{1}^{2} - y_{2}^{2} \rvert  = t \lvert y_{1} + y_{2} \rvert \lvert y_{1} - y_{2} \rvert 
$$
but $t \lvert y_{1} + y_{3} \rvert$ can be arbitrarily large.
### Convex Set
**Definition**: a set $D \in \mathbb{R}^{2}$ is convex if whenever $(t_{1},y_{1})$ and $(t_{2},y_{2})$ are in $D$, then $$
(1-\lambda) (t_{1},y_{1}) +\lambda (t_{2},y_{2}) \in D\quad \forall \lambda \in[0,1]
$$
> the whole line is in the set

**Theorem**: suppose $f(t,y)$ is defined on  a convex set $D \in \mathbb{R}^{2}$, then if a constant $L>0$ exists with $$
\left| \frac{ \partial f }{ \partial y } (t,y)\right|\leq L \quad \forall (t,y) \in D
$$
then $f$ satisfies a Lipschitz condition with Lipschitz constant $L$.

> proof of sketch: just use the mean value theorem, $$
\lvert f(t,y_{1})- f(t,y_{2}) \rvert  = \frac{ \partial f }{ \partial y }(t,\xi) \lvert y_{1} - y_{2} \rvert 
$$where $\xi \in[y_{1},y_{2}]$

**Still the same** $f = ty^{2}$,  we can prove it satisfies Lipschitz condition on the region $$
D= \left\{ (t,y)| 0\leq t\leq T,-Y\leq y\leq Y \right\} 
$$
We're given the initial value problem $$
y'(t) = ty^{2}(t),y(t_{0}) = \alpha>0
$$
then we have a unique solution to this to be $$
y(t) = \frac{2\alpha}{2+\alpha(t_{0}^{2}-t^{2})}
$$
> this is trivial once you remember to integrate both sides

So the denominator vanishes at $$
t = \sqrt{ \frac{2}{\alpha}+t_{0}^{2} } = \mathrm{T}
$$
so for $0<t_{0}<T <\mathrm{T}$, the ODE solution is bounded on $$
D =\left\{ (t,y)|t_{0}\leq t\leq T \right\} 
$$
for $T>\mathrm{T}$, the solution is not defined on $t = \mathrm{T}$.

### Well-posed problem
The initial-value problem
$$\frac{dy}{dt}=f(t,y), \quad a \leq t \leq b, \quad y(a)=\alpha,$$
is said to be a **well-posed** problem if:

- A unique solution, $y(t)$, to the problem exists, and
- There exist constants $\varepsilon_0 > 0$ and $k > 0$ such that for any $\varepsilon$, with $\varepsilon_0 > \varepsilon > 0$, whenever $\delta(t)$ is continuous with $|\delta(t)| < \varepsilon$ for all $t$ in $[a,b]$, and when $|\delta_0|<\varepsilon$, the initial-value problem
$$\frac{dz}{dt}=f(t,z)+\delta(t), \quad a \leq t \leq b, \quad z(a)=\alpha+\delta_0,$$
has a unique solution $z(t)$ that satisfies
$$|z(t)-y(t)| < k\varepsilon \quad \text{for all } t \text{ in } [a,b].$$
> Definition in English:
> 1. a unique ODE solution exists
> 2. small changes (perturbation) to  ODE imply small changes to solution

![[output.png]]

**Theorem**: Suppose $$
D = [a,b] \times \mathbb{R}
$$
if $f$ is continuous and satisfies a Lipschitz condition in the variable $y$ on the set $D$ , then the initial value problem $$
\frac{ \partial y }{ \partial t }  = f(t,y), t \in[a,b] \quad y(a)= \alpha
$$
is well-posed.

> this is way too hard to prove!

![[output (1).png]]

**Example**: show that the initial-value problem $$
\frac{ \partial y }{ \partial t } = y - t^{2}+1,t\in[0,2]
$$
is well-posed on $$
D = [0,2]\times \mathbb{R}
$$
**Solution**: because $$
\frac{ \partial f }{ \partial y } (t,y) = 1,\left| \frac{ \partial f }{ \partial y } (t,y) \right| = 1

$$
then $f(t,y) = y-t^2 +1$ satisfies a Lipschitz condition in $y$ on $D$ with Lipschitz constant $1$. Therefore the ODE is well-posed. In fact $$
y(t) = 1+ t^{2} + 2t - \frac{1}{2}\exp(t)
$$
