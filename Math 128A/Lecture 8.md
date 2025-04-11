# §4.4 Composite Numerical Integration

## Composite Simpson's Rule: 
$n = 2m, x_j = a + j h, h = \frac{b-a}{n}$

![[Screenshot 2025-03-15 at 16.30.19.png]]
**Example** : 
$$
	\int _{0}^{\pi/2} \sin \lambda x\, dx  = -\frac{1}{\lambda}\int _{0}^{\pi/2}  \, d\cos \lambda x  = \frac{1}{\lambda}\left( 1-\cos \frac{\lambda \pi}{2} \right) 
$$
**Simpson's rule**;
$$
\int_{0}^{\pi/2} \sin \lambda x dx \approx \frac{\pi}{12}\left(4  \sin \left( \frac{\pi \lambda}{4} \right)+ \sin \frac{\pi \lambda}{2}\right)
$$

- **Quadrature**:
 $$\int_{a}^{b} f(x) dx = \sum_{j=1}^{m} \int_{x2(j-1)}^{x2j} f(x) dx$$

$$= \sum_{j=1}^{m} \left( \frac{h}{3} \left( f(x_{2(j-1)}) + 4f(x_{2j-1}) + f(x_{2j}) \right) - \frac{f^{(4)}(\xi_j)}{90} h^5 \right)$$

$$= \frac{h}{3} \left( f(a) + 2 \sum_{j=1}^{m-1} f(x_{2j}) + 4 \sum_{j=1}^{m} f(x_{2j-1}) + f(b) \right) - \frac{h^5}{90} \sum_{j=1}^{m} f^{(4)}(\xi_j)$$

$$= \frac{h}{3} \left( f(a) + 2 \sum_{j=1}^{m-1} f(x_{2j}) + 4 \sum_{j=1}^{m} f(x_{2j-1}) + f(b) \right) - \frac{(b-a)h^4}{180} f^{(4)}(\xi)$$
- **Error**:
  $$
  \text{Error} = -\frac{(b-a) h^4}{180} f^{(4)}(\mu)
  $$
- **DoP = 3**: $f^{(4)}(\xi) = 0$ for $f(x) = 1, x, x^2, x^3$.

**By definition**: in contrast:
$$
\int_a^bf(x)dx=\lim_{n\to\infty}h\left(f(a)+\sum_{j=1}^{m-1}f(x_{2j})+\sum_{j=1}^mf(x_{2j-1})+f(b)\right)
$$
### Trapezoidal Rule $n =1,x_{0}= a,x_{1} =b,h =b-a$
$$
\int _{a}^{b}f(x) \, dx  = \frac{h}{2}(f(a)+f(b)) - \frac{f''(\xi)}{12}h^{3}
$$
- DoP = $1$ since $f''(\xi) = 0$ for $f(x) = 1,x$
### Composite Trapezoidal Rule $x_{j} = a+jh,h=\frac{b-a}{n},0\leq j\leq n$.
$$
\begin{align}
 \int _{a}^{b}f(x) \, dx  &  =\sum_{i=1}^{n} \int _{x_{j-1}}^{x_{j}}f(x)  \, dx  \\
 &  = \sum_{i=1}^{n} \left( \frac{h}{2}(f(x_{j-1})+f(x_{j})) -\frac{f''(\xi)}{12}h^{3} \right)  \\
 &  = \frac{h}{2}\left( f(a) + \sum_{j=1}^{n-1} f(x_{j})+f(b) \right) - \frac{(b-a)h^{2}}{2}f''(\xi)
\end{align}
$$

---

## Example: Composite Simpson's Rule

- **Integral**: $\int_0^\pi \sin x \, dx$
- **Tolerance**: $|\text{Error}| \leq 10^{-5}$
- **Solution**:
  - $|f^{(4)}(\mu)| = |\sin \mu| \leq 1$
  - $|\text{Error}| = \left| \frac{\pi h^4}{180} f^{(4)}(\mu) \right| \leq \frac{\pi h^4}{180} \leq 10^{-5}$
  - $$\frac{\pi^5}{180 n^4} \leq 10^{-5} \implies n \geq \pi \left( \frac{\pi}{180 \cdot 10^{-5}} \right)^{1/4} \approx 20.3$$
  - Choose $n = 2m = 22$, so $m = 11$, $h = \frac{\pi}{22}$
  - Approximation:
    $$
    \int_0^\pi \sin x \, dx \approx \frac{\pi}{66} \left( 2 \sum_{j=1}^{10} \sin \left( \frac{j \pi}{11} \right) + 4 \sum_{j=1}^{11} \sin \left( \frac{(2j-1) \pi}{22} \right) + 2 \right) \approx 2.0000046
    $$

---

## Round-Off Error Stability
- **Points**: $n = 2m,x_{j} = a + jh,h = \frac{b-a}{n},0\leq j\leq n$ 
- **Model**: $f(x_i) = \hat{f}(x_i) + e_i$, $|e_i| \leq \epsilon$
- **Composite Simpson's**:
  $$
  \int_a^b f(x) \, dx \approx \frac{h}{3} \left( f(a) + 2 \sum_{j=1}^{m-1} f(x_{2j}) + 4 \sum_{j=1}^m f(x_{2j-1}) + f(b) \right) \stackrel{\text{def}}{=} \mathcal{I}(f)
  $$
Then we'll see:
$$
\mathcal{I} (f) = \mathcal{I}(\hat{f}) + \frac{h}{3}\left( e_{0}+2\sum_{i=1}^{m-1} e_{2j}+ 4\sum_{j=1}^{m} e_{2j-1}+e_{n} \right)
$$
by triangle inequality: 
$$
|\mathcal{I} (f) - \mathcal{I}(\hat{f})| \leq \frac{h}{3}\left( |e_{0}|+2\sum_{j=1}^{m-1} |e_{2j}|+ 4\sum_{j=1}^{m}  |e_{2j-1}|+|e_{n}|\right) \leq hn \epsilon = (b-a) \epsilon
$$
so this is **Numerically Stable.**

---

## §4.5 Recursive Composite Trapezoidal Rule

- **Definition**: $n = 2^k, h_j = \frac{b-a}{2^j}$
- **Quadrature**:
  $$
  \int_a^b f(x) \, dx = \frac{h_{k-1}}{2} \left( f(a) + 2 \sum_{j=1}^{2^{k-1}-1} f(x_j) + f(b) \right) \stackrel{\text{def}}{=} R_{k,1}
  $$
- **Series Expansion**:
  $$
  \int_a^b f(x) \, dx = \underbrace{ \frac{h_{k-1}}{2}\left( f(a)+ 2 \sum_{j=1}^{n-1} f(x_{j})+f(b) \right) }_{ := \mathbf{R}_{k,1} }+ \sum_{j=1}^\infty K_j h_{k-1}^{2j}
  $$
- **Example**:
  - $R_{1,1} = \frac{h_0}{2} (f(a) + f(b)) = \frac{b-a}{2} (f(a) + f(b)):=\mathcal{N}_{1}(h_{0})$
  - $R_{2,1} = \frac{h_1}{2} (f(a) + 2 f(a + h_1) + f(b)) = \frac{1}{2} (R_{1,1} + h_0 f(a + h_1)):=N_{1}\left( \frac{h_{0}}{2} \right)$
  - $$
\mathbf{R}_{k,1} = \frac{1}{2}\left( \mathbf{R}_{k-1,1}+ h_{k-2}\sum_{j=1}^{2^{k-2}} f(a+(2j-1)h_{k-1}) \right):=N_{1}\left( \frac{h_{0}}{2^{k-1}} \right)
$$![[Screenshot 2025-03-15 at 17.08.09.png]]
---
#### Example
Romberg Extrapolation for $\int _{0}^{\pi}\sin x \, dx,n=1,2,2^{2},2^{3},2^{4},2^{5}$

$$
\begin{aligned}
R_{1,1} & =\frac{\pi}{2}\left(\sin(0)+\sin(\pi)\right)=0, \\
R_{2,1} & =\frac{1}{2}\left(R_{1,1}+\pi\sin\left(\frac{\pi}{2}\right)\right)=1.57079633, \\
R_{3,1} & =\frac{1}{2}\left(R_{2,1}+\frac{\pi}{2}\sum_{j=1}^{2}\sin\left(\frac{(2j-1)\pi}{4}\right)\right)=1.89611890, \\
R_{4,1} & =\frac{1}{2}\left(R_{3,1}+\frac{\pi}{4}\sum_{j=1}^{4}\sin\left(\frac{(2j-1)\pi}{8}\right)\right)=1.97423160, \\
R_{5,1} & =\frac{1}{2}\left(R_{4,1}+\frac{\pi}{8}\sum_{j=1}^{8}\sin\left(\frac{(2j-1)\pi}{16}\right)\right)=1.99357034, \\
R_{6,1} & =\frac{1}{2}\left(R_{5,1}+\frac{\pi}{16}\sum_{j=1}^{32}\sin\left(\frac{(2j-1)\pi}{32}\right)\right)=1.99839336.
\end{aligned}`
$$


## Recursive Composite Simpson's Rule
$$\begin{align}
\int_a^b f(x) dx  & \approx \frac{h}{3}\left(f(a)+2\sum_{j=1}^{m-1}f(x_{2j})+4\sum_{j=1}^{m}f(x_{2j-1})+f(b)\right)-\frac{(b-a)h^4}{12}f^{(4)}(\mu) \\
 & =\frac{h}{3}\left(f(a)+2\sum_{j=1}^{m-1}f(x_{2j})+4\sum_{j=1}^{m}f(x_{2j-1})+f(b)\right)+\sum_{j=2}^{\infty}K_jh^{2j} \\
 & =R_{k,1}+\sum_{j=2}^{\infty}K_j h_k^{2j-1}
\end{align}$$ for $n=2^k, h_t=\frac{b-a}{2^t}$
$$\int_{a}^{b} f(x) dx \approx \mathbf{R}_{t,1} + \sum_{j=2}^{\infty} K_{j} h_{t-1}^{2j}, \text{ for } n = 2^{k}, t \leq k.$$
$$\mathbf{R}_{1,1} = \frac{b-a}{6} (f(a) + 4\mathbf{T}_{1} + f(b)), \quad \mathbf{T}_{1} = f((a+b)/2), \quad \mathbf{S}_{0} = 0$$
$$\vdots \quad \vdots$$
$$\mathbf{T}_{k} = \sum_{j=1}^{2^{k-1}} f(a + (2j-1)h_{k}),$$
$$\mathbf{R}_{k,1} = \frac{h_{k-1}}{3} (f(a) + 2\mathbf{S}_{k-1} + 4\mathbf{T}_{k} + f(b)),$$
$$\mathbf{S}_{k} = \mathbf{S}_{k-1} + \mathbf{T}_{k}, k = 2, \cdots, \log_{2}n.$$


---

## Romberg Extrapolation

- **Definition**: Even-term Richardson extrapolation to improve accuracy.
- **Example**: $\int_0^\pi \sin x \, dx$ with $n = 1, 2, 2^2, 2^3, 2^4, 2^5$
  - Table (partial):
    ```
    2.09439511  1.57079633  1.89611890  2.00455976  1.99857073  2.00026917
    1.97423160  1.99998313  2.00000555  2.00001659  1.99999975  2.00000001
    ```
  - 33 function evaluations used.

---

## Tricks of the Trade for $\int_a^b f(x) \, dx$

- **Composite Simpson/Trapezoidal**: Add more equi-spaced points.
- **Romberg Extrapolation**: Obtain higher-order rules from lower-order rules.
- **Adaptive Quadrature**: Add points only when necessary, focusing on regions requiring accuracy.

---

## §4.6 Adaptive Quadrature Methods

- **Function**: $y(x) = e^{-3x} \sin 4x$
  - Oscillatory for small $x$, nearly 0 for large $x$.
  - Applications: Mechanical engineering (spring and shock absorber systems).
![[Screenshot 2025-03-15 at 17.37.15.png]]
### Adaptive Quadrature (I)

- **Formula**:
  $$
  \int_a^b f(x) \, dx = S(a, b) - \frac{h^5}{90} f^{(4)}(\xi), \quad \xi \in (a, b)
  $$
  where
  $$
  S(a, b) = \frac{h}{3} \left( f(a) + 4 f(a + h) + f(b) \right), \quad h = \frac{b-a}{2}
  $$
![[Screenshot 2025-03-15 at 17.37.42.png]]
### Adaptive Quadrature (II)
![[Screenshot 2025-03-15 at 17.41.00.png]]

### Adaptive Quadrature (III)
![[Screenshot 2025-03-15 at 17.42.48.png]]
function quad($f$, $[a, b]$, $\tau$) of matlab

For a given tolerance $\tau$,

> composite Simpson: $S(a, b)$, $S(a, \frac{a+b}{2})$ and $S(\frac{a+b}{2}, b)$.

> Romberg extrapolation:
$$Q_1 = S(a, \frac{a+b}{2}) + S(\frac{a+b}{2}, b), \quad Q = Q_1 + \frac{1}{15}(Q_1 - S(a, b)).$$

> if
$$|Q - Q_1| \leq \tau,$$
return $Q$ (Adaptive Simpson returns $Q_1$)

> else return
$$\text{quad}(f, [a, \frac{a+b}{2}], \tau/2) + \text{quad}(f, [\frac{a+b}{2}, b], \tau/2).$$

## §4.7 Gaussian Quadrature

### Gaussian Quadrature (I)
![[Screenshot 2025-03-15 at 18.04.25.png]]
- **Goal**: For $n > 0$, choose nodes $x_1, \ldots, x_n \in [-1, 1]$ and weights $c_1, \ldots, c_n$ to maximize **DoP**:
  $$
  \int_{-1}^1 f(x) \, dx \approx \sum_{j=1}^n c_j f(x_j) \tag{1}
  $$
- **Parameters**: $2n$ (nodes and weights), exact for $f(x) = 1, x, \ldots, x^{2n-1}$.

### Gaussian Quadrature, $n=2$ (I)

- **Setup**:
  $$
  \int_{-1}^1 f(x) \, dx \approx c_1 f(x_1) + c_2 f(x_2)
  $$
- **Conditions**: Exact for $f(x) = 1, x, x^2, x^3$,i.e. this holds:
$$
\int _{-1}^{1}f(x)dx = c_{1}f(x_{1})+c_{2}f(x_{2}) \, dx
$$
$$
  c_1 + c_2 = 2, \quad c_1 x_1 + c_2 x_2 = 0, \quad c_1 x_1^2 + c_2 x_2^2 = \frac{2}{3}, \quad c_1 x_1^3 + c_2 x_2^3 = 0
  $$
- **Solution**: $x_1 = -\frac{1}{\sqrt{3}}$, $x_2 = \frac{1}{\sqrt{3}}$, $c_1 = c_2 = 1$
  $$
  \int_{-1}^1 f(x) \, dx \approx f\left(-\frac{1}{\sqrt{3}}\right) + f\left(\frac{1}{\sqrt{3}}\right)
  $$
- **DoP**: 3 (exact for $1, x, x^2, x^3$, not $x^4$).

### Gaussian Quadrature by Legendre Polynomials

- **Recurrence**:
  $$
  P_0(x) = 1, \quad P_1(x) = x, \quad (n+1) P_{n+1}(x) = (2n+1) x P_n(x) - n P_{n-1}(x)
  $$
> this one is particularly important

- **Properties**: $P_n(x)$ has degree $n$, with $n$ distinct roots in $(-1, 1)$.
	- so we use the $n$ roots as the $\left\{ x_{j} \right\}_{j=1}^{n}$ for the quadrature
- **Orthogonality**:
	- mutually orthogonal:
	$$
\int _{-1}^{1}P_{n}(x)P_{j}(x) \, dx =0, \quad \forall j<n 
$$
	- **Thm**:$$
  \int_{-1}^1 P_n(x) Q(x) \, dx = 0 \text{ for any } Q(x) \text{ with } \deg(Q) < n
  $$

**Theorem**: Gaussian Quadrature DoP = $2n - 1$

- **Proof**:
  - The quadrature exact for polynomial of deg $\leq n-1$. Let $P(x)$ have $\deg \leq 2n - 1$: 
    $$
    P(x) = P_n(x) Q(x) + R(x), \quad \deg(Q), \deg(R) \leq n - 1\tag{2}
    $$
  - Then:
    $$
    \int_{-1}^1 P(x) \, dx = \int_{-1}^1 [P_n(x) Q(x) + R(x)] \, dx = \int_{-1}^1 R(x) \, dx
    $$
    - $\int_{-1}^1 P_n(x) Q(x) \, dx = 0$ by orthogonality.
    - Quadrature exact for $\deg \leq n - 1$, so:
      $$
      \int_{-1}^1 R(x) \, dx = \sum_{j=1}^n c_j R(x_j) = \sum_{j=1}^n c_j P(x_j)
      $$
>用 Legendre 多项式的根作为节点，是因为它们**与正交性天然兼容**，能“杀掉”积分中的高阶项、最大程度地提升精度，而且误差项最小，是构造高斯求积公式时的最优选择。


### Hermite Interpolation with Legendre Roots

- **Given**: Roots $x_1, \ldots, x_n$ of $P_n(x)$ with $(x_j, f(x_j), f'(x_j))$.
- **Interpolant**: $H(x)$ of degree $\leq 2n - 1$ satisfies:
  $$
  H(x_j) = f(x_j), \quad H'(x_j) = f'(x_j), \quad j = 1, \ldots, n
  $$
- **Error**: for each $x \in [a,b]$, there exists $\xi(x) \in [a,b]$,
  $$
  f(x) = H(x) + \underbrace{ \frac{f^{(2n)}(\xi(x))}{(2n)!} (x - x_1)^2 \cdots (x - x_n)^2 }_{ :=R(x) }
  $$
**Review**: construction of Hermite interpolation polynomials
- our goal is $$
H(x) = \sum_{i=1}^{n} f(x_{j})h_{j}(x) + f'(x_{j})k_{j}(x)
$$
- to construct the $h_{j}$ and $k_{j}$ here, we first need Lagrange basis poly: $$
\ell_{j}(x) = \prod_{i=1,i\neq j}^{n} \frac{x-x_{i}}{x_{j}-x_{i}} 
$$
so that $$
\ell_{j}(x_{i}) = \begin{cases}
1 & x_{i}=x_{j} \\
0 & o.w.
\end{cases}
$$
- so basically we want $$
h_{j}(x_{j}) = 1,h_{j}'(x_{j})=0,k_{j}(x_{j})=0,k_{j}'(x_{j}) =1
$$
- then we have this $$
\begin{align}
h_{j}(x)  & = [1-2\ell'_{j}(x_{j})(x-x_{j})] \ell_{j}(x)^{2} \\
k_{j}(x) & = (x-x_{j})\ell_{j}(x)^{2}
\end{align}
$$
> also remember this: $$
\begin{align}
h_{j}  & = [1-2\ell'_{j}(x_{j})(x-x_{j})] \ell_{j}^{2}
 \\
k_{j} & = (x-x_{j})\ell_{j}^{2}\end{align}
$$
- and therefore we get the Hermite poly using above steps


### Gaussian Quadrature Error

- **Integration**:
  $$
  \int_{-1}^1 f(x) \, dx = \int_{-1}^1 H(x) \, dx + \int_{-1}^1 \frac{f^{(2n)}(\xi(x))}{(2n)!} (x - x_1)^2 \cdots (x - x_n)^2 \, dx
  $$
  - $\deg(H) \leq 2n - 1$, so $\int_{-1}^1 H(x) \, dx = \sum_{j=1}^n c_j H(x_j) = \sum_{j=1}^n c_j f(x_j)$.
- **Error Term**:
  $$\begin{align}
\text{Error}  & = \frac{f^{(2n)}(\xi)}{(2n)!} \int_{-1}^1 (x - x_1)^2 \cdots (x - x_n)^2 \, dx  \\
 & = \frac{2^{2n} (n!)^3 (n-1)!}{(2n+1)! (2n)! (2n-1)!} f^{(2n)}(\xi) \\
 &  =O\left( \frac{4^{-n}|f^{(2n)}(\xi)|}{(2n)!} \right)
\end{align}
  
  $$

### MATLAB Code for Legendre Nodes and Weights

```matlab
function [c, x] = Legendre(n)
    b = transpose(1:n-1);
    b = b ./ sqrt((2*b-1) .* (2*b+1));
    B = diag(b, 1) + diag(b, -1);
    [Q, D] = eig(B);
    x = diag(D);
    x(abs(x) < 1e-15) = 0;
    c = 2 * transpose(Q(1,:).^2);
end
```

- Rapid convergence for smooth functions.

---

## Simpson/Trapezoidal vs. Gaussian Quadrature

- **Simpson/Trapezoidal**:
	- Composite rules: 
		- Add equi-spaced points.
	- Romberg extrapolation: 
		- Higher-order from lower-order rules.
	- Adaptive quadrature: 
		- Add points **only when necessary.**
- **Gaussian Quadrature**:
	- Nodes vary with $n$.
	- Optimal for fixed $n$, while Simpson excels for given tolerance.

