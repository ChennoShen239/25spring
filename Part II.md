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