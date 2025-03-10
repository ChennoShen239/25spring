# Approximation theory

## Least Squares Approximation and Orthogonal Polynomials

### Problem Setup
Suppose we are given data points $(x_i, y_i)$, $i = 1, \ldots, m$, where $x_i, y_i \in \mathbb{R}$. We aim to find a function $f(x) \approx y_i$ that belongs to a restricted class of functions to avoid overfitting.

#### Linear Fitting
For example, consider linear functions parametrized by a slope $a_1$ and an intercept $a_0$:
$$ f_a(x) = a_1 x + a_0, $$
where $\vec{\mathbf{a}} = (a_0, a_1)$ is the parameter vector.

#### Polynomial Fitting
More generally, we can consider polynomials of degree $n$:
$$ f_a(x) = a_n x^n + a_{n-1} x^{n-1} + \cdots + a_0 = \sum_{j=0}^n a_j x^j, $$
where $\vec{a} = (a_0, \ldots, a_n) \in \mathbb{R}^{n+1}$.

#### General Basis Functions
Even more generally, given a set of basis functions $g_0, \ldots, g_{p-1}$, we define:
$$ f_a(x) = \sum_{j=0}^{p-1} a_j g_j(x), \tag{*} $$
with $\vec{a} = (a_0, \ldots, a_{p-1})' \in \mathbb{R}^p$. For polynomials, choose $g_j(x) = x^j$, $j = 0, \ldots, p-1$. Note that we use zero-indexing for the parameter vector components.

### Least Squares Approximation
In least squares, we seek to minimize:
$$ \min_{\vec{a} \in \mathbb{R}^p} F(\vec{a}), \quad F(\vec{a}) := \sum_{i=1}^m (f_a(x_i) - y_i)^2. $$
Using the form in $(*)$, this becomes a linear algebra problem:
$$
\begin{aligned}
\sum_{i=1}^m (f_{\vec{a}}(x_i) - y_i)^2 &= \sum_{i=1}^m \left( \left[ \sum_{j=0}^{p-1} a_j g_j(x_i) \right] - y_i \right)^2 \\
&= \sum_{i=1}^m \left( \sum_{j=0}^{p-1} g_{ij} a_j - y_i \right)^2 \\
&= \sum_{i=1}^m ([G \vec{a}]_i - y_i)^2 \\
&= \| G \vec{a} - \vec{y} \|_2^2,
\end{aligned}
$$
where $G = (g_{ij}) = (g_j(x_i))$ is an $m \times p$ matrix, with rows $i = 1, \ldots, m$ and columns $j = 0, \ldots, p-1$. Here, $\vec{y} = (y_1, \ldots, y_m)$.
> Here let's be precise about the matrix, we have $$
G =(g_{ij}) = (g_{j}(x_{i})), \text{i.e. } G = \begin{bmatrix}
g_{0}(x_{1 }) & g_{1}(x_{1}) & \dots  & g_{p-1}(x_{1}) \\
g_{0}(x_{2 }) & g_{1}(x_{2}) & \dots  & g_{p-1}(x_{2}) \\ \vdots & \vdots &  & \vdots \\
g_{0}(x_{m}) & g_{1}(x_{m}) & \dots & g_{p-1}(x_{m})
\end{bmatrix}
$$then basically the notation $[G \vec{a}]_{i} = \begin{bmatrix}g_{0}(x_{i}) & g_{1}(x_{i}) &\dots & g_{p-1}(x_{i})\end{bmatrix}\cdot\vec{a}$, i.e. the $i$'s row of the matrix $G$.
#### Solving the Normal Equations
The optimization problem is:
$$ \min_{\vec{a} \in \mathbb{R}^p} \| G \vec{a} - \vec{y} \|_2^2. $$
Taking the gradient of $F(\vec{a})$ and setting it to zero:
$$ \nabla F(\vec{a}) = 2 G^\top (G \vec{a} - \vec{y}) = 0, $$
we obtain the normal equations:
$$ G^\top G \vec{a} = G^\top \vec{y}. $$
This is a positive definite linear system $A \vec{a} = \vec{b}$, where $A = G^\top G$ and $\vec{b} = G^\top \vec{y}$. A unique solution exists if $G$ has rank $p$, requiring $m \geq p$. For polynomial least squares ($g_j(x) = x^j$), this holds if all $x_i$ are distinct.
> notice that the mat $A = G'G$ is $p \times p$, and $A$ is invertible iff $A$ is full rank, i.e. $r(A) = p$, which requires $r(G) = \min \{ m,p \}= p$, i.e. $m \geq p$. i.e. the columns in $G$ is linearly independent. However, $m\geq p$ doesn't guarantee $r(G) = p$.
### Nonlinear Function Classes
Sometimes, the function class is not of the form $(*)$, e.g., exponential functions:
$$ f_{b,c}(x_i) = b e^{c x_i}, \quad b, c \in \mathbb{R}. $$
To fit $y_i \approx b e^{c x_i}$, take the logarithm:
$$ \log y_i \approx \log b + c x_i. $$
Define $\tilde{y}_i = \log y_i$, $a_0 = \log b$, and $a_1 = c$, transforming the problem to:
$$ \tilde{y}_i \approx a_0 + a_1 x_i, $$
which is linear least squares on $(x_i, \tilde{y}_i)$. Solve for $a_0, a_1$, then recover $b = e^{a_0}$, $c = a_1$. 
> Note: This approximates $\log y_i$, not $y_i$, differing from direct nonlinear least squares.

---

## Interlude: Inner Products and Gram-Schmidt

### Inner Products
*Consider functions $f: [a, b] \to \mathbb{R}$ on a continuous interval. An inner product $\langle \cdot, \cdot \rangle$ on a vector space $\mathcal{V}$ satisfies:*
- *Linearity: $\langle u + v, w \rangle = \langle u, w \rangle + \langle v, w \rangle$,*
- *Homogeneity: $\langle \lambda u, v \rangle = \lambda \langle u, v \rangle$,*
- *Symmetry: $\langle u, v \rangle = \langle v, u \rangle$,*
- *Positive definiteness: $\langle u, u \rangle \geq 0$, with equality if and only if $u = 0$.*

The dot product on $\mathbb{R}^n$ is a classic example. An inner product induces a norm:
$$ \|u\| = \sqrt{\langle u, u \rangle}, $$
and orthogonality: $u, v$ are orthogonal if $\langle u, v \rangle = 0$.

### Gram-Schmidt Process
Given linearly independent vectors $\{v_1, \ldots, v_k\}$, Gram-Schmidt constructs an orthogonal set $\{u_1, \ldots, u_k\}$ spanning the same space:
1. $u_1 = v_1$,
2. For $i = 2, \ldots, k$:
$$ u_i = v_i - \sum_{j=1}^{i-1} \frac{\langle v_i, u_j \rangle}{\langle u_j, u_j \rangle} u_j. $$

### $L^2$ Inner Product
For continuous functions $C([a, b])$, the $L^2$ inner product is:
$$ \langle f, g \rangle_{L^2([a,b])} = \int_a^b f(x) g(x) \, dx. $$
The weighted $L^2$ inner product with a nonnegative weight $w(x)$ is:
$$ \langle f, g \rangle_{L^2([a,b]; w)} = \int_a^b f(x) g(x) w(x) \, dx. $$
$C([a, b])$ is a vector space under pointwise addition and scalar multiplication, with $\mathbb{P}_n$ (polynomials of degree $\leq n$) as a subspace. The monomials $M_k(x) = x^k$, $k = 0, \ldots, n$, form a basis for $\mathbb{P}_n$.

---

## Least Squares Over an Interval

### Continuous Least Squares
To approximate $f(x)$ over $[a, b]$ with $f_a(x) = \sum_{j=0}^{p-1} a_j g_j(x)$, **consider "infinitely many" points** $(x, f(x))$, $x \in [a, b]$. Discretize with a grid $x_i = a + i h$, $h = \frac{b - a}{m}$, $y_i = f(x_i)$. The discrete objective:
$$ \frac{1}{m} \sum_{i=1}^m (f_a(x_i) - f(x_i))^2 $$
approaches the $L^2$ norm as $m \to \infty$:
$$ \int_a^b (f_a(x) - f(x))^2 \, dx = \| f_a - f \|_{L^2([a,b])}^2. $$
> to see this we use Riemann sum, notice that $h =\frac{b-a}{m}$, so the optimization problem can be written as $$
\frac{h}{b-a} \sum_{i=1}^M(f_{a}(x_{i})-f(x_{i}))^{2}
$$ and if we take the limit $$\lim_{ h \to 0} \frac{h}{b-a} \sum_{i=1}^M(f_{a}(x_{i})-f(x_{i}))^{2} = \frac{1}{b-a} \int_{a}^b(f_a(x)-f(x))^{2}dx$$

### Normal Equations in the Limit
From the discrete normal equations $G^\top G \vec{a} = G^\top \vec{y}$, scale by $h$:
$$ h G^\top G \vec{a} = h G^\top \vec{y}. $$
As $m \to \infty$:
- $[h G^\top G]_{ij} = \sum_{k=1}^m g_i(x_k) g_j(x_k) h \to \int_a^b g_i(x) g_j(x) \, dx = \langle g_i, g_j \rangle_{L^2([a,b])}$,
- $[h G^\top \vec{y}]_i = \sum_{k=1}^m g_i(x_k) f(x_k) h \to \int_a^b g_i(x) f(x) \, dx = \langle g_i, f \rangle_{L^2([a,b])}$.
> here we have $h \to 0$.

Define the Gram matrix $A_{ij} = \langle g_i, g_j \rangle_{L^2([a,b])}$ and vector $b_i = \langle g_i, f \rangle_{L^2([a,b])}$. Solve:
$$ A \vec{a} = \vec{b}, $$
then recover $f_a(x) = \sum_{j=0}^{p-1} a_j g_j(x)$.
> Indeed here we have $A = hG'G$ and $\vec{b} = hG'\vec{y}$.
### Weighted Least Squares
For a weight $w(x)$, minimize:
$$ \| f_a - f \|_{L^2([a,b]; w)}^2. $$
Form $A_{ij} = \langle g_i, g_j \rangle_{L^2([a,b]; w)}$, $b_i = \langle g_i, f \rangle_{L^2([a,b]; w)}$, and solve $A \vec{a} = \vec{b}$.

---

## Orthogonal Polynomials

### Definition
*Using shorthand $\langle \cdot, \cdot \rangle_w = \langle \cdot, \cdot \rangle_{L^2([a,b]; w)}$, we seek polynomials $p_0, \ldots, p_n$ such that:*
$$ \langle p_i, p_j \rangle_w = 0 \text{ if } i \neq j, $$
*where $p_k$ has degree $k$. These are orthogonal polynomials w.r.t. $w$. If $\langle p_i, p_i \rangle_w = 1$, they are orthonormal; often, we make them monic ($p_k(x) = x^k + \text{lower terms}$).*

### Construction via Gram-Schmidt
Start with monomials $M_k(x) = x^k$. Set $p_0 = M_0 = 1$. Inductively:
$$ p_{k+1} = M_{k+1} - \sum_{i=0}^k \frac{\langle M_{k+1}, p_i \rangle_w}{\langle p_i, p_i \rangle_w} p_i. $$
This ensures $p_{k+1}$ is monic, orthogonal to $p_0, \ldots, p_k$, and $\text{span}(p_0, \ldots, p_k) = \mathbb{P}_k$.

### Theorem
*The sequence $p_0, p_1, \ldots$ is monic, orthogonal w.r.t. $\langle \cdot, \cdot \rangle_w$, and $p_0, \ldots, p_n$ is a basis for $\mathbb{P}_n$. For $k > l$, $p_k$ is orthogonal to all polynomials in $\mathbb{P}_l$.*

### Least Squares with Orthogonal Polynomials
For $f_a = \sum_{i=0}^n a_i p_i$, the Gram matrix is diagonal:
$$ A_{ij} = \begin{cases} \langle p_i, p_i \rangle_w & \text{if } i = j, \\ 0 & \text{otherwise}, \end{cases} $$
so:
> diagonal by construction using Gram-Schmit

$$ a_i = \frac{\langle f, p_i \rangle_w}{\langle p_i, p_i \rangle_w}, $$
> here $\left< f,p_{i} \right>_{w}$ comes from the vector $\vec{b} = hG'\vec{y}$ 
 
and the optimal approximator is:
$$ f_a = \sum_{i=0}^n \frac{\langle f, p_i \rangle_w}{\langle p_i, p_i \rangle_w} p_i, $$
which solves:
$$ \min_{p \in \mathbb{P}_n} \| p - f \|_w^2. $$

### Three-Term Recurrence
Orthogonal polynomials satisfy:
$$ p_{k+1}(x) = (x - \alpha_k) p_k(x) - \beta_k p_{k-1}(x), \quad k \geq 1, $$
where:
$$ \alpha_k = \frac{\langle x p_k, p_k \rangle_w}{\langle p_k, p_k \rangle_w}, \quad \beta_k = \frac{\langle p_k, p_k \rangle_w}{\langle p_{k-1}, p_{k-1} \rangle_w} > 0. $$

#### Legendre Polynomials
For $w \equiv 1$ on $[-1, 1]$, the monic Legendre polynomials $P_k$ follow:
$$ P_{k+1}(x) = x P_k(x) - \frac{k^2}{4(k^2 - 1)} P_{k-1}(x), $$
with $P_0(x) = 1$, $P_1(x) = x$. Examples:
- $P_2(x) = x^2 - \frac{1}{3}$,
- $P_3(x) = x^3 - \frac{3}{5} x$,
- $P_4(x) = x^4 - \frac{6}{7} x^2 + \frac{3}{35}$.

#### Chebyshev Polynomials
The **Chebyshev polynomials** are an extremely useful tool in numerical analysis due to their **equioscillation property** on the interval $[-1,1]$. 

Defined as $T_n(x) = \cos(n \cos^{-1}(x))$ on $[-1, 1]$, they satisfy:
$$ T_{n+1}(x) = 2x T_n(x) - T_{n-1}(x), $$
with $T_0(x) = 1$, $T_1(x) = x$. They are orthogonal w.r.t. $w(x) = \frac{1}{\sqrt{1 - x^2}}$. Leading term: $2^{n-1} x^n$. Monic version:
$$ \tilde{T}_n(x) = \frac{1}{2^{n-1}} T_n(x), \quad n \geq 1. $$
**Let's verify this**
using the property of $\cos x$, we have $$
\cos(a+b) + \cos(a-b) = 2\cos a \cos b
$$ so for $$
\begin{align}
T_{n+1}(x)  & = \cos((n+1)\cos ^{-1}x) \\
 & =2\cos(n\cos ^{-1}x)\cos(\cos ^{-1}x) - \cos ((n-1)\cos ^{-1}x) \\
 & = \underbrace{ 2x\cos (n\cos ^{-1}x) }_{ 2xT_{n}(x) }-\underbrace{ \cos ((n-1)\cos ^{-1}x) }_{ T_{n-1}(x) }
\end{align}

$$Just so simple!

**Chebyshev nodes** the zeros of $T_{n}$ is called chebyshev nodes, i.e.$$
n\cos ^{-1}x=\left( k+\frac{1}{2} \right)\pi \implies \cos ^{-1}x = \left( \frac{2k+1}{2n} \right)\pi \implies x= \cos\left( \frac{2k+1}{2n}\pi \right)
	$$ where $k=0,1,\dots n-1$ since $\cos ^{-1}x \le 1$ 
 
**Extrema** the extrema of $T_{n}$ are attained at $$
n \cos ^{-1}x =k\pi \implies \cos ^{-1}x = \frac{k}{n}\pi \implies x= \cos\left( \frac{k\pi}{n} \right)
$$
where $k = 1,2,\dots ,n-1$ 

**Orthogonality** to prove this, we first prove $f_{n}(y) =\cos (ny)$ are orthogonal w.r.t. unweighted $L^2$ inner product on $[0,\pi]$.
$$
\begin{align}
\int_{0}^{\pi}\cos(my) \cos(ny) dy &  =\int_{0}^{\pi} \frac{1}{2}(\cos((m+n)y) - \cos((m-n )y))dy \\
 & = \frac{1}{2} \int_{0}^{\pi}\cos((m+n)y)dy -\frac{1}{2}\int_{0}^{\pi} \cos((m-n)y)dy \\
 &  = 0-0 = 0
\end{align}
$$
then we use this property, and substitute $y =\cos ^{-1}x$, we have $$
\begin{align}
0 &  =\int_{0}^{\pi} f_{m}(\cos ^{-1}x) f_{n}(\cos ^{-1}x) d\cos ^{-1}x \\
 & =\underbrace{ \int_{-1}^{1} T_{m}(x) T_{n}(x) \frac{1}{\sqrt{ 1-x^{2} }}dx }_{ \left< T_{m},T_{n} \right> _{L^2\left( [-1,1];w=\frac{1}{\sqrt{ 1-x^{2} }} \right)} }
\end{align}
$$
**A greater interval** if you need to map $[-1,1]$ to $[a,b]$, then use $$
\tilde{x} = \frac{1}{2}((b-a)x+a+b)
	$$ where $x \in[-1,1]$ and $\tilde{x}\in[a,b]$.

---

## Economization of Power Series

### Minimax Property
**Theorem**
For **all monic** polynomials $\tilde{p}_n \in \tilde{\mathbb{P}}_n$:
$$ \frac{1}{2^{n-1}} = \max_{x \in [-1, 1]} |\tilde{T}_n(x)| \leq \max_{x \in [-1, 1]} |\tilde{p}_n(x)|. $$
Chebyshev polynomials minimize the extreme values.

### Degree Reduction
Given $p_n(x) = \sum_{k=0}^n a_k x^k$, reduce to $p_m \in \mathbb{P}_m$, $m < n$. 
> This may be needed since $n$ is too large.

Stepwise: we use $p_{n-1} \in \mathbb{P}_{n-1}$ to approximate $p_{n}$, then use $p_{n-2}\in \mathbb{P}_{n-2}$ to do the same for $p_{n-1}$ ...
**Criterion**
- Minimize $$\max_{x \in [-1, 1]} |p_n(x) - p_{n-1}(x)|$$
- this is called the **Minimax** problem
	- assume $a_{n} \neq 0$, so we know $\frac{p_{n}-p_{n-1}}{a_{n}}\in \tilde{\mathbb{P}}_{n}$ (monic)
	- so we equally minimize $$
\left| a_{n} \right| \max_{x \in[-1,1]}\left| \frac{p_{n}-p_{n-1}}{a_{n}} \right| 
$$
	- then use the **theorem** we know the minimum is obtained when $$
\tilde{T}_{n}(x) = \frac{p_{n}-p_{n-1}}{a_{n}}
$$
	- so the stepwise relation is $$
p_{n-1}(x) = p_{n}(x)-a_{n}\tilde{T}_{n}(x)
$$
> this even works when $a_{n}=0$.

## Lagrange interpolation meets Chebyshev polynomials

**Basic review** we have $(x_{i},y_{i}),i=0,1,\dots m$ distinct nodal points and we want the unique polynomial $p_{m} \in \mathbb{P}_{m}$ such that $$
p_{m}(x_{i}) = y_{i},\forall i=0,1,\dots m
$$
- Question: does $p$ approximate $f$ on some interval, as we take $m \to \infty$
- Answer: depends dramatically on how we choose the interpolation points $x_{i}$.

**Lagrange Basis Poly**
given interpolation points $\mathbf{x} = \left( x_{0,\dots,x_{m}} \right)$, we have $$
L_{j}(x;\mathbf{x}):= \prod_{i=1,i \neq j}^{m}  \frac{x-x_{i}}{x_{j}-x_{i}}
$$
for simplicity of notation, let $L_{j}(x) = L_{j}(x;\mathbf{x})$ 
**Key properties**
1. $L_{j}(x) \in \mathbb{P}_{m}$
2. $L_{j}(x_{i}) = \delta_{ij}$ 

we define $p \in \mathbb{P}_{m}$ via:
$$
p = \sum_{j=0}^{m} y_{j}L_{j}
$$
Then we define the **norm** as:
$$
\left| \left| g \right|  \right| _{L^\infty([a,b])} = \max_{x \in [a,b]}\left| g(x) \right|
$$
**Theorem**: Suppose $f \in C^{m+1}([a,b])$, and let $x_0, \ldots, x_m \in [a,b]$ be distinct interpolation points. Let $y_i = f(x_i)$ for $i=0, \ldots, m$, and let $p$ denote the Lagrange interpolating polynomial for the data $(x_i, y_i), i=0, \ldots, m$. Then for every $x \in [a,b]$ there exists $\xi = \xi(x) \in [a,b]$ such that
$$f(x) - p(x) = \frac{f^{(m+1)}(\xi)}{(m+1)!} \prod_{i=0}^m (x - x_i).$$
**Hence**, $$
\left| \left| f-p \right|  \right| _{L^\infty([a,b])}\leq \frac{\left| \left| f^{(m+1)} \right|  \right| _{L^\infty}}{(m+1)!}\left| \left| q_{\mathbf{x}} \right|  \right| _{L^{\infty}}
$$
where $q_{\mathbf{x}}:= \prod_{i=0}^{m}(x-x_{i})$ , since $\left| \left| q_{\mathbf{x}} \right| \right|_{l^{\infty}}\leq \left| b-a \right|^{m+1}$, we have $\left| \left| f-p \right| \right|_{L^{\infty}} = O(\left| b-a \right|^{m+1})$ 

**We choose Chebyshev nodes as interpolation nodes**
- we have $m+1$ nodal points, we need chebyshev nodes of $T_{m+1}$ 
- the zeros of $T_{n}$ are $$
\cos\left( \frac{2j-1}{2n}\pi \right),j=1,\dots,n

$$
- then we have $n=m+1$ i.e. the chebyshev nodes are $$
x_{j}= \cos\left( \frac{2j-1}{2(m+1)}\pi \right),j=1,2,\dots,m+1
$$
- with this choice, $$
\begin{align}
q_{\mathbf{x}}(x)  &  = \prod_{i=0}^{m} (x-x_{i}) \\
 & = C \tilde{T}_{m+1} (x) \tag{same zeros}\\
 &  = \underbrace{ \tilde{T}_{m+1}(x) }_{ \text{monic} }
\end{align}


$$
- then we know $\left| \left| q_{\mathbf{x}} \right| \right|_{L^{\infty}}=\max_{x \in[-1,1]} \left| \tilde{T}_{m+1}(x) \right| \leq \frac{1}{2^m}$ 
**Theorem**
suppose $f \in C^{m+1}([-1,1])$ and let $\mathbf{x}=(x_{0},\dots ,x_{m})$ such that $$
x_{j} = \cos\left( \frac{2j+1}{2(m+1)}\pi \right),j=0,\dots m
$$
then let $y_{j} =f(x_{j})$, let $p$ denote the Lagrange interpolating polynomial for the data, then $$
\left| \left| f-p \right|  \right| _{L^{\infty}}\leq \frac{\left| \left| f^{(m+1)} \right|  \right| _{L^{\infty}}}{2^{m}(m+1)!}
$$
and if we transform to $[a,b,]$, then we have $$
\left| \left| f-p \right|  \right| _{L^{\infty}([a,b])}\leq \left( \frac{b-a}{2} \right)^{m+1}\frac{\left| \left| f^{(m+1)} \right|  \right| _{L^{\infty}([a,b])}}{2^{m}(m+1)!}
$$
## Gauss quadrature for approximation theory
**Gauss quadrature** concerns the estimation of integrals of the form $$
		\int_{a}^{b}g(x)w(x)  \, dx 
$$
with quadrature rules of the form $$
\sum_{i=0}^{M} w_{i}g(x_{i})
$$
here we have the weight function $w:[a,b]\to\left[ 0,\infty \right)$ 

**Theorem**: Let $a < x_0 < \ldots < x_m < b$ be the zeros of $p_m$, the $(m+1)$-th orthogonal polynomial with respect to the weight function $w$ on the interval $[a, b]$, and let $\mathbf{x} = (x_0, \ldots, x_m)$. Define weights
$$w_i := \int_a^b L_i(x; \mathbf{x}) w(x) dx$$ 
> which is in fact $w_{i} : =\left< L_{i},w \right>$, i.e. the weight is determined by the interpolating poly $L_{i}$.

for $i = 0, \ldots, m$. Then
$$\int_a^b g(x) w(t) dt = \sum_{i=0}^{m} w_i g(x_i)$$ 
for all $g \in \mathbb{P}_{2m+1}$.
> given arbitrary nodes, any $g \in \mathbb{P}_{m}$ is equal to its own interpolating poly on the interpolation points $\mathbf{x}$  

**Theorem**: The optimization problem $$\min_{p \in \mathbb{P}_n} \| p - f \|_w^2$$ is solved by $$p = \sum_{k=0}^{n} \frac{\langle f, p_k \rangle_w}{\langle p_k, p_k \rangle_w} p_k,$$ where $\{p_k\}_{k=0}^\infty$ is an orthogonal polynomial sequence with respect to the weight function $w$ on $[a, b]$. 
- To implement this theorem, we need to compute integrals of the form $$\langle h_1, h_2 \rangle_w = \int_a^b h_1(x) h_2(x) w(x) dx,$$ **which can be approximated using Gaussian quadrature:** $$\langle h_1, h_2 \rangle_w \approx \sum_{i=0}^m w_i h_1(x_i) h_2(x_i).$$
> this is why this quadrature matters.

## Connecting  interpolation and least-square projection

**Approximate inner product** $\left< \phi,\psi \right>_{w}^{(m)}$ is defined by $$
\left< \phi,\psi \right> _{w}^{(m)}:= \sum_{i=0}^{m} \phi(x_{i})\psi(x_{i})w_{i}
$$
where $w_{i}$ and $\mathbf{x}$ are the Gauss quadrature weights and nodes for $w$. 
Then we are actually approximating $f$ by $$
			p = \sum_{k=0}^{n} \frac{\langle f, p_k \rangle_w^{(m)}}{\langle p_k, p_k \rangle_w^{(m)}} p_k,

$$
where we take the $m$ to be sufficiently large.
BUT if we pick $m=n$, then the $q$ is **exactly** the Lagrange interpolation polynomial

**Theorem**: With notation as in the preceding discussion, let $$q = \sum_{k=0}^{n} \frac{\langle f, p_k\rangle^{(n)}}{\langle p_k, p_k\rangle^{(n)}} p_k \in \mathbb{P}_n$$. Then $q$ coincides exactly with the Lagrange interpolating polynomial for $f$ using interpolation points $x_i$, $i = 0, \ldots, n$. That is, $q(x_i) = f(x_i)$ for all $i = 0, \ldots, n$.

> Proof.
> Let $\ell$ be the lagrange interpolating polynomial
> WTS: $q=\ell$ 
> Claim 1: $$
\left< p_{k},p_{k} \right> _{w}^{(n)} = \left< p_{k},p_{k} \right> _{w}
$$
	for all $k=0,\dots n$ 
	- to see this, note that $\left< p_{k},p_{k} \right>_{w} = \int _{a}^{b} p_{k}^{2}(x)w(x) \, dx$
	- since $p_{k}^{2}\in \mathbb{P}_{2n}$, the Gauss quadrature rule is exact, i.e. $$
\int _{a}^{b}p_{k}^{2}(x)w(x) \, dx = \sum_{i=0}^{n} p_{k}^{2}(x)w_{i}=\left< p_{k},p_{k} \right> _{w}^{(n)}$$
	which proves the claim
	Claim 2:$$
\left< f,p_{k} \right> _{w}^{(n)} = \left< \ell,p_{k} \right> _{w}^{(n)}$$
	- we verify this by $$
\left< f,p_{k} \right>_{w}^{(n)} = \sum_{i=0}^{n}  f(x_{i})p_{k}(x_{i})w_{i} = \sum_{i=0}^{n} \ell(x_{i})p_{k}(x_{i})w_{i} = \left< \ell,p_{k} \right> _{w}^{(n)}
$$
	Claim 3:$$
\left< \ell,p_{k} \right> _{w}^{(n)} = \left< \ell,p_{k} \right> _{w}
$$
	- we prove this  as in claim 1.
	Given all 3 claims, we now rewrite $q$ as $$
q =\sum_{k=0}^{n} \frac{\left< \ell,p_{k} \right> _{w}}{\left< p_{k},p_{k} \right> _{w}}p_{k}
$$
	so $q$ is the solution to the problem $$
\min_{\tilde{q}\in \mathbb{P}_{n}}\left| \left| \tilde{q}-\ell \right|  \right|_{w}^{2}
$$
	and the solution is trivially $\tilde{q} = \ell$. Q.E.D

## Pade approximation 
**Definition** a rational function $r$ of degree $N$ a a function of the form $$
r(x) = \frac{p(x)}{q(x)}
$$
where $p$ and $q$ are polynomials whose degrees **sum to $N$ 

**Pade approximation about $x =0$**
let's expand $p(x) = \sum_{k=0}^{n}p_{k}x^{k}$ and $q(x) = \sum_{k=0}^{m} q_{k}x^{k}$,
- for simplicity we let $p_{k} \equiv 0$ for all $k>n$ and $q_{k} \equiv 0$ for all $k>m$ .
- then we rewrite the 2 as $$
\begin{cases}
p(x) & =\sum_{k =0}^{\infty } p_{k}x^{k} \\
q(x) & =\sum_{k=0}^{\infty} q_{k}x^{k} \\ 
\end{cases}
$$
- wlog, we set $q_{0}=1$, then we have $n+m+1$ free parameters.
- the $\left[ \frac{n}{m} \right]$ **Pade approximant** of $f$ is defined by choosing parameters such that $$
r^{(k)}(0) = f^{(k)}(0)
$$ for $k=0,1,\dots,N$. 
**How to construct it**
1. let $f(x) = \sum_{k=0}^{\infty}a_{k}x^{k}$ be the Maclaurin series expansion of $f$,
2. then $$
f(x)-r(x) = f(x) -\frac{p(x)}{q(x)} = \frac{f(x)q(x)-p(x)}{q(x)}
$$
3. we want the $[f-r]^{(k)} = 0$, then we just need the $k$ **derivatives of the numerator to all be zero**
4.  we have $$
\begin{align}
f(x)q(x)-p(x) & =\left( \sum_{i=0}^{\infty} a_{k}x^{k} \right)\left( \sum_{j=0}^{\infty} q_{j}x^{j} \right) - \sum_{k=0}^{\infty} p_{k}x^{k}  \\
 & = \sum_{i,j=0}^{\infty}a_{i} q_{j}x^{i+j} -\sum_{k=1}^{\infty} p_{k}x^{k} \\
 &  = \sum_{k=0}^{\infty} \sum_{i=0}^{k} a_{i}q_{k-i} x^{k}-\sum_{k=0}^{\infty} p_{k}x^{k}  \\
 & =\sum_{k=0}^{\infty} \left( \underbrace{ \sum_{i=0}^{k} a_{i}q_{k-i}-p_{k}  }_{ \equiv 0 \text{ for all }k\leq N }\right)x^{k}
\end{align}
$$
5. so we require $$
p_{k} = \sum_{i=0}^{k} a_{i}q_{k-i}\text{ for all }k\leq N

$$
this are $N+1$ equations and $N+1$ unknowns.

From $q_{0} = 1$, we know that $p_{k} = \sum_{i=1}^{k}a_{i}q_{k-i}+a_{k}$ , then we write it as $$
p_{k} - \sum_{i=1}^{k} a_{i}q_{k-i} = a_{k}
$$
Then we define an $(N+1)\times m$ matrix $C =(C_{ki})$ where the row index starts from 0 and column index starts from 1, and $$
C_{ki} = \begin{cases}
a_{k-i} & i\leq k \\
0 & o.w.
\end{cases}
$$
so we have $$
p_{k} - \underbrace{ \sum_{i=1}^{m} C_{ki}q_{i} }_{ \text{since }q_{i }\equiv 0 ~\forall ~i>m } = a_{k}
$$
- Meanwhile, let $E =(E_{ki})$ be a $(N+1)\times(n+1)$ matrix where both indices are zero-indexed and $$
E_{ki}= \begin{cases}
1 & i=k\leq n \\
0, & o.w. \\  
\end{cases}

$$
so we have $p_{k} = \sum_{ki}E_{ki}p_{i}$ and $$
\sum_{i=0}^{n} E_{ki}p_{i} - \sum_{i=1}^{n}C_{ki}q_{i} = q_{k},\quad k=0,\dots N
$$
for example, we have $(m,n,N)= (3,3,6)$, then we have the 2 matirces $$
C=\begin{pmatrix}
0 & 0 & 0 \\
a_{0} & 0 & 0 \\
a_{1} & a_{0} & 0 \\
a_{2} & a_{1} & a_{0}  \\
a_{3} & a_{2} & a_{1} \\
a_{4} & a_{3} & a_{2}  \\
a_{5} & a_{4} & a_{3}
 \end{pmatrix} ,\quad E= \begin{pmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1 \\
0  & 0 & 0 & 0 \\
0 & 0 & 0 & 0 \\
0 & 0 & 0 & 0
\end{pmatrix}
$$ in general we can write $$
E = \begin{pmatrix}
I_{n+1} \\
0_{(N-n)\times(n+1)} 
\end{pmatrix}


$$
then if we let $\mathbf{a} = (a_{0},\dots,a_{N})'$  and let $\mathbf{p}$ and $\mathbf{q}$ be the vectors we can rewrite the problem as $$
E\mathbf{p} - C\mathbf{q} = \mathbf{a}
$$ 
or $$
\underbrace{ (E-C) }_{ :=A }\begin{pmatrix}
\mathbf{p} \\
\mathbf{q} 
\end{pmatrix} = \mathbf{a}
$$ Then it turns to a problem of solving $A\mathbf{x} = \mathbf{a}$.

## 28 Chebyshev Rational Approximation (8.4)

- The Padé approximant, like Taylor polynomials, is based on an expansion around a base point (which we took to be $x=0$), leading to approximations that are of nonuniform quality over an interval such as $[-1, 1]$.
- Assume we want to construct a rational approximation for $f$ of roughly uniform quality over $[-1, 1]$ (and we can reduce to this case from the general case $[a, b]$ by an appropriate linear transformation, as before).

> - 垫近似（Padé approximant），类似于泰勒多项式，是基于某个基点（此处我们取为 $x=0$）的展开，导致在区间（如 $[-1, 1]$）上的近似质量不均匀。

> - 假设我们希望构造一个关于函数$f$的有理近似，在区间$[-1, 1]$上具有大致均匀的质量（并且我们可以通过适当的线性变换将一般情况$[a, b]$简化为这种情形，如前所述）。
### First Step: Replace Taylor Series with Chebyshev Expansions

$$
r(x) = \frac{\sum_{k=0}^n p_k T_k(x)}{\sum_{k=0}^m q_k T_k(x)},
$$

where, without loss of generality (WLOG), we can assume $q_0 = 1$.

Again, we can extend $p_k$ and $q_k$ by zeros for $k > n$ and $k > m$, respectively, to obtain:

$$
r(x) = \frac{\sum_{k=0}^\infty p_k T_k(x)}{\sum_{k=0}^\infty q_k T_k(x)}.
$$

In fact, we will also extend $q_k$ by zeros for $k < 0$.

Suppose that:

$$
f(x) = \sum_{k=0}^\infty a_k T_k(x),
$$

where the coefficients are defined as:

$$
a_k = \frac{\langle f, T_k \rangle_w}{\langle T_k, T_k \rangle_w},
$$

and $w$ is the Chebyshev weight function $w(x) = \frac{1}{\sqrt{1 - x^2}}$.

- We shall only need to compute $a_0, \ldots, a_{N+m}$.
- The numerators $\langle f, T_k \rangle_w$ can generally be obtained by Gauss-Chebyshev quadrature.
- The denominators are problem-independent and can be computed directly as:
> - 我们仅需计算$a_0, \ldots, a_{N+m}$。
> - 分子$\langle f, T_k \rangle_w$通常可以通过高斯-切比雪夫求积法获得。
> - 分母与问题无关，可直接计算为：
$$
\langle T_k, T_k \rangle_w = \begin{cases}
\pi, & k = 0 \\
\pi/2, & \text{otherwise}.
\end{cases}
$$

### Idea: Expand in Chebyshev Polynomials

Expand $f(x) q(x) - p(x)$ in the Chebyshev polynomials $T_0, T_1, \ldots$, and insist that all terms up to order $N$ vanish.

Compute:

$$
\begin{aligned}
f(x) q(x) - p(x) &= \left( \sum_{i=0}^\infty a_i T_i(x) \right) \left( \sum_{j=0}^\infty q_j T_j(x) \right) - \sum_{k=0}^\infty p_k T_k(x) \\
&= \sum_{i,j=0}^\infty a_i q_j T_i(x) T_j(x) - \sum_{k=0}^\infty p_k T_k(x).
\end{aligned}
$$

- We encounter an obstacle: unlike monomials where $x^i x^j = x^{i+j}$, $T_i T_j$ is not itself a Chebyshev polynomial.
- However, we have the **important identity** (from homework):

$$
T_i T_j = \frac{1}{2} \left[ T_{i+j} + T_{|i-j|} \right],
$$

which is sufficient.

### Continue Computing

$$
\begin{aligned}
f q - p &= \frac{1}{2} \sum_{i,j=0}^\infty a_i q_j T_{i+j} + \frac{1}{2} \sum_{i,j=0}^\infty a_i q_j T_{|i-j|} - \sum_{k=0}^\infty p_k T_k \\
&= \frac{1}{2} \underbrace{ \sum_{k=0}^\infty \left( \sum_{i=0}^k a_i q_{k-i} \right) }_{ k=i+j } T_k + \frac{1}{2} \underbrace{ \left( \sum_{i=0}^m a_i q_i \right) }_{ |i-j|=0 } T_0 + \frac{1}{2} \underbrace{ \sum_{k=1}^\infty \left( \sum_{i=0}^{m-k} a_i q_{i+k} \right) }_{ j-i=k } T_k \\
&\quad + \frac{1}{2} \underbrace{ \sum_{k=1}^\infty \sum_{i=k}^{m+k} a_i q_{i-k} }_{ i-j=k } T_k - \sum_{k=0}^\infty p_k T_k.
\end{aligned}
$$

This yields the equations: 

- For $k = 0$:
  $$
  \sum_{i=0}^k a_i q_{k-i} + \sum_{i=0}^{m-k} a_i q_{i+k} - 2 p_k = 0,
  $$
- For $k \geq 1$:
  $$
  \sum_{i=0}^k a_i q_{k-i} + \sum_{i=0}^{m-k} a_i q_{i+k} + \sum_{i=k}^{m+k} a_i q_{i-k} - 2 p_k = 0.
$$

These are equivalent to:

- For $k = 0$:
  $$
  \sum_{i=0}^k a_{k-i} q_i + \sum_{i=k}^m a_{i-k} q_i - 2 p_k = 0,
  $$
- For $k \geq 1$:
  $$
  \sum_{i=0}^k a_{k-i} q_i + \sum_{i=k}^m a_{i-k} q_i + \sum_{i=0}^m a_{i+k} q_i - 2 p_k = 0.
$$

This time, we ignore the constraint $q_0 = 1$ for now and treat $q_0$ as a variable temporarily.

### Define Matrices

Form the $(N+1) \times (m+1)$ matrices $B^{(1)} = (B_{ki}^{(1)})$, $B^{(2)} = (B_{ki}^{(2)})$, and $B^{(3)} = (B_{ki}^{(3)})$ with zero-indexed rows and columns, defined by:

$$
B_{ki}^{(1)} = \begin{cases}
a_{k-i}, & i \leq k, \\
0, & \text{otherwise},
\end{cases} \quad
B_{ki}^{(2)} = \begin{cases}
a_{i-k}, & i \geq k, \\
0, & \text{otherwise},
\end{cases} \quad
B_{ki}^{(3)} = \begin{cases}
a_{i+k}, & k \geq 1, \\
0, & \text{otherwise},
\end{cases}
$$

and let:

$$
\tilde{C} = \frac{1}{2} \left( B^{(1)} + B^{(2)} + B^{(3)} \right).
$$

Then, letting $\tilde{\mathbf{q}} = (q_0, \ldots, q_m)^\top \in \mathbb{R}^{m+1}$ (now including $q_0$), we recover the equations:

$$
E \mathbf{p} - \tilde{C} \tilde{\mathbf{q}} = 0.
$$

Now, we reintroduce the constraint $q_0 = 1$ and let $\mathbf{c} \in \mathbb{R}^{N+1}$ and $C \in \mathbb{R}^{(N+1) \times m}$ be defined by the block equation:

$$
\tilde{C} = \begin{pmatrix} \mathbf{c} & C \end{pmatrix}, \quad \tilde{\mathbf{q}} = \begin{pmatrix} 1 \\ \mathbf{q} \end{pmatrix},
$$

to obtain:

$$
E \mathbf{p} - C \mathbf{q} = \mathbf{c}.
$$

### Vectorize the Equations

We may vectorize again as:

$$
\underbrace{\begin{pmatrix} E & -C \end{pmatrix}}_{=: A} \begin{pmatrix} \mathbf{p} \\ \mathbf{q} \end{pmatrix} = \mathbf{c},
$$

to obtain the $A \mathbf{x} = \mathbf{c}$ format that can be solved for $\mathbf{x} = \begin{pmatrix} \mathbf{p} \\ \mathbf{q} \end{pmatrix}$.

---

# 29 Fourier Series (8.5)

**Caution:** Notation here differs slightly from the book.

- **Caution:** For the discussion of Fourier topics, we reserve the letter $i$ for the complex number ($i^2 = -1$).
- We now consider functions $f: [-\pi, \pi] \to \mathbb{R}$ (by shifting and scaling, we can reduce to this domain from an arbitrary interval).

It is useful to view the domain of $f$ as extending to the entire real line $\mathbb{R}$ by stipulating that it is $2\pi$-periodic, i.e., $f(x + 2\pi k) = f(x)$ for all $k \in \mathbb{Z}$.
> 将函数$f$的定义域视为通过规定其为$2\pi$-周期的而扩展到整个实数轴$\mathbb{R}$是有用的，即对于所有$k \in \mathbb{Z}$，有$f(x + 2\pi k) = f(x)$。
### Basis Functions

Consider the functions:

$$
\phi_k(x) = \cos(kx), \quad k = 0, \ldots, n,
$$

so in particular $\phi_0 \equiv 1$, and:

$$
\psi_k(x) = \sin(kx), \quad k = 1, \ldots, n.
$$

- In fact, the collection $\{\phi_0, \ldots, \phi_n, \psi_1, \ldots, \psi_n\}$ is orthogonal with respect to the $L^2([-\pi, \pi])$ inner product. (In this section, we fix the notation $\langle \cdot, \cdot \rangle$ for this inner product.)
  - This means $\langle \phi_k, \phi_l \rangle = 0$ whenever $k \neq l$, $\langle \psi_k, \psi_l \rangle = 0$ whenever $k \neq l$, and $\langle \phi_k, \psi_l \rangle = 0$ for all $k, l$.
  - Additionally, $\langle \phi_0, \phi_0 \rangle = 2\pi$, $\langle \phi_k, \phi_k \rangle = \langle \psi_k, \psi_k \rangle = \pi$ for $k = 1, \ldots, n$.
- The verification is similar to our verification of orthogonality for Chebyshev polynomials, so we’ll skip it.

**Definition:** Set $\mathcal{T}_n := \text{span}(\phi_0, \ldots, \phi_n, \psi_1, \ldots, \psi_n)$ is called the set of trigonometric polynomials of degree $\leq n$. (We say a trigonometric polynomial in $\mathcal{T}_n$ has degree $n$ if the coefficient of either $\phi_n$ or $\psi_n$ is nonzero.)
> **定义：** 集合$\mathcal{T}_n := \text{span}(\phi_0, \ldots, \phi_n, \psi_1, \ldots, \psi_n)$被称为次数$\leq n$的三角多项式集合。（我们说一个在$\mathcal{T}_n$中的三角多项式有次数$n$，如果$\phi_n$或$\psi_n$的系数非零。）


- **Caution:** For some reason, the book excludes $\psi_n$ from $\mathcal{T}_n$, but this is unconventional and would complicate clarifying discussions below.

### Orthogonal Projection

Orthogonality ensures that the problem:

$$
\underset{\phi \in \mathcal{T}_n}{\operatorname*{min}} \|\phi - f\|^2
$$

is solved by:

$$
\phi = \frac{\langle f, \phi_0 \rangle}{\langle \phi_0, \phi_0 \rangle} \phi_0 + \sum_{k=1}^n \left[ \frac{\langle f, \phi_k \rangle}{\langle \phi_k, \phi_k \rangle} \phi_k + \frac{\langle f, \psi_k \rangle}{\langle \psi_k, \psi_k \rangle} \psi_k \right],
$$

or concretely:

$$
\phi(x) = \frac{a_0}{2} + \sum_{k=1}^n \left[ a_k \cos(kx) + b_k \sin(kx) \right],
$$

where:

$$
a_k = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \cos(kx) \, dx, \quad k = 0, \ldots, n,
$$

$$
b_k = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \sin(kx) \, dx, \quad k = 1, \ldots, n.
$$
> notice that $a_{k} = \frac{\left< f,\phi_{k} \right>}{\left< \phi_{k},\phi_{k} \right>}$ 
### Complex Perspective

A clarifying perspective is gained by extending the range of our functions to complex numbers.

We can extend the $L^2$ inner product to functions $g, h: [-\pi, \pi] \to \mathbb{C}$ via:

$$
\langle g, h \rangle = \int_{-\pi}^{\pi} g(x) \overline{h(x)} \, dx.
$$

**Note:** In general, an inner product over a complex vector space is linear in the first slot, with conjugate symmetry:

$$
\langle g, h \rangle = \overline{\langle h, g \rangle},
$$

implying conjugate linearity in the second slot:

$$
\langle g, h_1 + \lambda h_2 \rangle = \langle g, h_1 \rangle + \overline{\lambda} \langle g, h_2 \rangle.
$$
> **注意：** 一般来说，复向量空间上的内积在**第一个位置**是线性的，并具有共轭对称性：这意味着在**第二个位置**具有共轭线性：


Define $e_k: [-\pi, \pi] \to \mathbb{C}$ by:

$$
e_k(x) = e^{ikx},
$$

for every $k \in \mathbb{Z}$.

- In fact, $\langle e_k, e_l \rangle = 2\pi \delta_{kl}$, so the functions $\{e_{-n}, \ldots, e_n\}$ are orthogonal.
- Verify this:

$$
\begin{aligned}
\langle e_k, e_l \rangle &= \int_{-\pi}^{\pi} e_k(x) \overline{e_l(x)} \, dx \\
&= \int_{-\pi}^{\pi} e^{ikx} e^{-ilx} \, dx \\
&= \int_{-\pi}^{\pi} e^{i(k-l)x} \, dx.
\end{aligned}
$$

  - If $k = l$, $e^{i(k-l)x} = 1$, and the integral is $2\pi$.
  - Otherwise, $\langle e_k, e_l \rangle = \frac{1}{i(k-l)} \left[ e^{i(k-l)x} \right]_{x=-\pi}^{\pi} = 0$.
> we can use Euler's Formula $e^{i\theta} = \cos\theta + i\sin\theta$

**Theorem:** $\mathcal{T}_n \subset \mathcal{T}_n^\mathbb{C} := \text{span}^\mathbb{C}(\phi_0, \ldots, \phi_n, \psi_1, \ldots, \psi_n) = \text{span}^\mathbb{C}(e_{-n}, \ldots, e_n)$, where $\text{span}^\mathbb{C}$ indicates linear combinations with complex coefficients.

> **定理：** $\mathcal{T}_n \subset \mathcal{T}_n^\mathbb{C} := \text{span}^\mathbb{C}(\phi_0, \ldots, \phi_n, \psi_1, \ldots, \psi_n) = \text{span}^\mathbb{C}(e_{-n}, \ldots, e_n)$，其中$\text{span}^\mathbb{C}$表示具有复数系数的线性组合。
#### Proof

- Note that $\phi_0 = e_0$.
- It suffices to show that for $k \geq 1$, $\text{span}(\phi_k, \psi_k) = \text{span}(e_k, e_{-k})$.
- Euler’s formula gives:

$$
e^{ikx} = \cos(kx) + i \sin(kx), \quad e^{-ikx} = \cos(kx) - i \sin(kx),
$$

implying $e_k, e_{-k} \in \text{span}(\phi_k, \psi_k)$, hence $\text{span}(\phi_k, \psi_k) \subset \text{span}(e_k, e_{-k})$.

- Conversely, adding and subtracting yields:

$$
\cos(kx) = \frac{e^{ikx} + e^{-ikx}}{2}, \quad \sin(kx) = \frac{e^{ikx} - e^{-ikx}}{2i},
$$

proving $\phi_k, \psi_k \in \text{span}(e_k, e_{-k})$.

 > #### 证明
> 
> - 注意到$\phi_0 = e_0$。
> - 只需证明对于$k \geq 1$，有$\text{span}(\phi_k, \psi_k) = \text{span}(e_k, e_{-k})$。
> - 欧拉公式给出：
> 
> $$
 e^{ikx} = \cos(kx) + i \sin(kx), \quad e^{-ikx} = \cos(kx) - i \sin(kx),
 $$
> 
> 这意味着$e_k, e_{-k} \in \text{span}(\phi_k, \psi_k)$，因此$\text{span}(\phi_k, \psi_k) \subset \text{span}(e_k, e_{-k})$。
> 
> - 反之，通过加减可得：
> 
>$$
 \cos(kx) = \frac{e^{ikx} + e^{-ikx}}{2}, \quad \sin(kx) = \frac{e^{ikx} - e^{-ikx}}{2i},
 $$
> 
> 这证明了$\phi_k, \psi_k \in \text{span}(e_k, e_{-k})$。

It follows that:

$$
\underset{\phi \in \mathcal{T}_n^\mathbb{C}}{\operatorname*{min}} \|\phi - f\|^2
$$

is solved by:

$$
\phi = \sum_{k=-n}^n \frac{\langle f, e_k \rangle}{2\pi} e_k,
$$

or:

$$
\phi(x) = \sum_{k=-n}^n c_k e^{ikx},
$$

where:

$$
c_k = \frac{1}{2\pi} \int_{-\pi}^{\pi} f(x) e^{-ikx} \, dx.
$$

#### Real-Valued Functions

If $f$ is real-valued, the minimizer over $\mathcal{T}_n^\mathbb{C}$ coincides with that over $\mathcal{T}_n$, and we relate $c_k$ to $a_k, b_k$:

- For $k = 0$:

$$
c_0 = \frac{1}{2\pi} \int_{-\pi}^{\pi} f(x) \, dx = \frac{a_0}{2}.
$$

- For $k \geq 1$, using $e^{-ikx} = \cos(kx) - i \sin(kx)$:

$$
\begin{aligned}
c_k &= \frac{1}{2\pi} \int_{-\pi}^{\pi} f(x) \cos(kx) \, dx - \frac{i}{2\pi} \int_{-\pi}^{\pi} f(x) \sin(kx) \, dx \\
&= \frac{a_k - i b_k}{2},
\end{aligned}
$$

and similarly, $c_{-k} = \frac{a_k + i b_k}{2}$.

- Then:

$$
a_k = c_k + c_{-k}, \quad b_k = \frac{c_{-k} - c_k}{i}.
$$

#### Summary

$$
c_0 = \frac{a_0}{2}, \quad c_k = \frac{a_k - i b_k}{2}, \quad c_{-k} = \frac{a_k + i b_k}{2}, \quad k = 1, \ldots, n,
$$

and:

$$
a_0 = 2 c_0, \quad a_k = c_k + c_{-k}, \quad b_k = i (c_k - c_{-k}), \quad k = 1, \ldots, n.
$$

- In general, coefficients $c_k$ (or $a_k, b_k$) must be computed by numerical quadrature.
- The best choice here is the **trapezoidal** rule on an equispaced grid:
$$
x_k = -\pi + k h, \quad k = 0, \ldots, M+1,
$$
> - 通常，系数$c_k$（或$a_k, b_k$）需要通过数值积分来计算。
> - 这里最佳的选择是在等距网格上使用梯形法则：

where $h = \frac{2\pi}{M+1}$ is the grid spacing.

Concretely:

$$
\int_{-\pi}^{\pi} g(x) \, dx \approx h \sum_{k=0}^{M+1} \frac{g(x_k) + g(x_{k+1})}{2} = \frac{h}{2} \left[ g(x_0) + g(x_{M+1}) \right] + h \sum_{k=1}^M g(x_k).
$$

- This is exact for any trigonometric polynomial in $\mathcal{T}_M$, analogous to Gauss quadrature with $M+1$ points on $\mathbb{P}_{2M+1}$.
- Since $f$ generally does not lie in $\mathcal{T}_M$ for finite $M$, we choose a large $M$ (possibly $M \gg n$) for an excellent approximation.
> - 对于$\mathcal{T}_M$中的任何三角多项式，这都是精确的，类似于在$\mathbb{P}_{2M+1}$上使用$M+1$个点的高斯求积。
> - 由于对于有限的$M$，函数$f$通常不属于$\mathcal{T}_M$，因此我们选择一个较大的$M$（可能$M \gg n$）以获得极好的近似。
- If $f(-\pi) = f(\pi)$ (as in $2\pi$-periodicity), then $g(x_0) = g(x_{M+1})$, and the rule simplifies to:

$$
\int_{-\pi}^{\pi} g(x) \, dx \approx h \sum_{k=0}^M g(x_k),
$$

which is the left-endpoint Riemann sum!

---

# 30 Discrete Least Squares with Trigonometric Polynomials (8.5)

Sometimes, we are given only a subsampling of a periodic function on an equispaced grid:
> 有时，我们仅获得周期函数在等距网格上的子采样：
$$
x_j = -\pi + j h, \quad j = 0, \ldots, 2m-1,
$$

where $h = \frac{\pi}{m}$.

- Note that $x_{2m} = \pi$, which is redundant assuming periodicity.
- Suppose $y_j = f(x_j)$ for $j = 0, \ldots, 2m-1$.

We want to perform discrete least squares using the data $(x_j, y_j)$, $j = 0, \ldots, 2m-1$, and basis functions $e_k(x) = e^{ikx}$.
>我们希望使用数据点$(x_j, y_j)$，其中$j = 0, \ldots, 2m-1$，以及基函数$e_k(x) = e^{ikx}$，来执行离散最小二乘法。
### Range of Index $k$

Observe that for all $j = 0, \ldots, 2m-1$:

$$
\begin{aligned}
e_{k+2m}(x_j) &= e^{ik x_j} e^{i 2m x_j} \\
&= e^{ik x_j} e^{i 2m (-\pi + j \pi / m)} \\
&= e^{ik x_j} e^{-i 2\pi m} e^{i 2\pi j} \\
&= e^{ik x_j},
\end{aligned}
$$

i.e., $e_{k+2m} = e_k$ on the grid.

- It doesn’t make sense to choose a range for $k$ with more than $2m$ consecutive integers, as extras are **redundant**.
- Choose $k = -m, \ldots, m-1$, giving $2m$ parameters to fit $2m$ points exactly.
- After fitting, we can expand in $\{e_{-m}, \ldots, e_{m-1}\}$ to extrapolate to $[-\pi, \pi]$, zeroing out coefficients for a least squares fit in a smaller basis.
> - 选择超过$2m$个连续整数的$k$范围是没有意义的，因为多余的范围是冗余的。
> - 选择$k = -m, \ldots, m-1$，这样可以提供$2m$个参数来精确拟合$2m$个点。
> - 拟合后，我们可以在$\{e_{-m}, \ldots, e_{m-1}\}$中展开，以将结果外推到$[-\pi, \pi]$区间，并将系数置零，以便在更小的基中进行最小二乘拟合。
### Normal Equations

The normal equations are $A \mathbf{c} = \mathbf{b}$, where:

$$
A_{kl} = \sum_{j=0}^{2m-1} \overline{e_k(x_j)} e_l(x_j), \quad b_k = \sum_{j=0}^{2m-1} \overline{e_k(x_j)} y_j,
$$

with $k, l$ from $-m, \ldots, m-1$. The least squares fit is:

$$
\phi(x) = \sum_{k=-m}^{m-1} c_k e_k(x) = \sum_{k=-m}^{m-1} c_k e^{ikx}.
$$

Concretely:

$$
\begin{aligned}
b_k &= \sum_{j=0}^{2m-1} e^{-ik x_j} y_j \\
&= \sum_{j=0}^{2m-1} e^{-ik (-\pi + j h)} y_j \\
&= e^{ik \pi} \sum_{j=0}^{2m-1} e^{-i \frac{2\pi k j}{2m}} y_j,
\end{aligned}
$$

and:

$$
\begin{aligned}
A_{kl} &= \sum_{j=0}^{2m-1} e^{i (l-k) x_j} \\
&= \sum_{j=0}^{2m-1} e^{i (l-k) (-\pi + j \pi / m)} \\
&= e^{i (k-l) \pi} \sum_{j=0}^{2m-1} e^{i \frac{2\pi (l-k) j}{2m}}.
\end{aligned}
$$

The sum $\sum_{j=0}^{2m-1} e^{i \frac{2\pi (l-k) j}{2m}}$ is geometric with $r = e^{i \frac{2\pi (l-k)}{2m}}$:

- If $r \neq 1$ (i.e., $l-k$ not a multiple of $2m$), it equals $\frac{1 - r^{2m}}{1 - r} = 0$.
- Since $k, l \in \{-m, \ldots, m-1\}$, $k - l$ is a multiple of $2m$ only if $k = l$.
- When $k = l$, the sum is $2m$.

Thus, $A_{kl} = 2m \delta_{kl}$, and $A = 2m I$.

It follows that $\mathbf{c} = \frac{1}{2m} \mathbf{b}$, or:

$$
c_k = \frac{e^{ik \pi}}{2m} \sum_{j=0}^{2m-1} e^{-i \frac{2\pi k j}{2m}} y_j, \quad k = -m, \ldots, m-1.
$$
