### §3.6 Parametric Curve Approximation: $x = x(t), y = y(t)$

- Given $n+1$ distinct points:
  $$
  (x_0, y_0), (x_1, y_1), \ldots, (x_n, y_n)
  $$
  where
  $$
  x_j = x(t_j), \quad y_j = y(t_j), \quad j = 0, 1, \ldots, n
  $$

- Example:

| $i$   | 0   | 1   | 2   | 3    | 4   |
|-------|-----|-----|-----|------|-----|
| $t_i$ | 0   | 0.5 | 0.5 | 2.75 | 1   |
| $x$   | -1  | 0   | 1   | 0    | 1   |
| $y$   | 0   | 1   | 0.5 | 0    | -1  |

---

### Parametric Curve with Polynomial Interpolation

- $4^{th}$ degree interpolation on both $x = x(t)$ and $y = y(t)$:
  $$
  x(t) = \left( \left( \left( 6t - \frac{352}{3} \right) t + 60 \right) t - \frac{14}{3} \right) t - 1
  $$
  $$
  y(t) = \left( \left( \left( -\frac{54}{3} t + 4 \right) t - \frac{116}{3} \right) t + 11 \right) t
  $$
![[Screenshot 2025-03-15 at 12.25.41.png]]
---

### Bezier Curves in Computer Graphics

- **Design**: Piece-wise cubic Hermite polynomials.
- **Feature**: Each cubic Hermite polynomial is completely determined by function/derivative at endpoints.
- **Consequence**: Each portion of the curve can be changed while leaving most of the curve the same.
- Remark: "As such then, parametric curve can effectively evolve."

---

### Parametric Curves: Piece-wise Cubic Hermite Polynomials

- **Given (I)**: $n+1$ data points:
  $$
  (x(t_0), y(t_0)), \ldots, (x(t_n), y(t_n))
  $$
- **Given (II)**: $n+1$ derivatives $\frac{dy}{dx} \big|_{t=t_i}, 0 \leq i \leq n$

- **Find**: $2 \times n$ pieces of cubic Hermite polynomials:
  $$
  x = x(t), \quad y = y(t), \quad \text{for } t \in (t_i, t_{i+1}), \quad 0 \leq i \leq n
  $$
  such that:
  $$
  (x(t_i), y(t_i)) = (x(t_i), y(t_i)), \quad (x(t_{i+1}), y(t_{i+1})) = (x(t_{i+1}), y(t_{i+1}))
  $$
  $$
  \underbrace{ \frac{dy}{dx} \big|_{t_i} = \frac{y'(t_i)}{x'(t_i)}, \quad \frac{dy}{dx} \big|_{t_{i+1}} = \frac{y'(t_{i+1})}{x'(t_{i+1})} }_{ \text{ The same derivative at both end points} }
  $$

- Notes:
  - 8 parameters in $x_i(t), y_i(t)$ 
  > since  $x_{i},y_{i}$ are polynomials of degree $\leq 3$ 

  - Only 6 given conditions for each $i$
  - **Use guidepoints**
- Topic: Cubic Bezier Curve

---

### Guidepoints Guide Slopes (for $[t_i, t_{i+1}] = [0,1]$)

- Unique cubic Hermite polynomials $x(t), y(t)$ with:
  $$
  (x(0), y(0)) = (x_0, y_0), \quad (x(1), y(1)) = (x_1, y_1)
  $$
![[Screenshot 2025-03-15 at 12.31.26.png]]
Here we use 2 guidepoints: $$
(x_{0}+\alpha_{0},y_{0}+ \beta_{0}),\quad(x_{1}- \alpha_{1},y_{1}-\beta_{1})
$$
where $$
\begin{pmatrix}
x'(0) \\
y'(0) 
\end{pmatrix} = \begin{pmatrix}
\alpha_{0} \\
\beta_{0} 
\end{pmatrix},\quad\begin{pmatrix}
x'(1) \\
y'(1)
\end{pmatrix} = \begin{pmatrix}
\alpha_{1} \\
\beta_{1}
\end{pmatrix}
$$
then we will have $$
\frac{dy}{dx}|_{t=0} = \frac{\beta_{0}}{\alpha_{0}}, \frac{dy}{dx}|_{t=1} = \frac{\beta_{1}}{\alpha_{1}} 
$$
### Parametric Curves: Summary of Approaches

Given (I): $n+1$ data points $\left(x\left(t_{0}\right), y\left(t_{0}\right)\right), \cdots, \left(x\left(t_{n}\right), y\left(t_{n}\right)\right)$.  

Given (II): $n+1$ derivatives $\frac{dy}{dx} \bigg|_{t=t_{i}}, 0 \leq i \leq n$.  

### Approaches

1. **Polynomial Interpolations**  
   - Using $n+1$ data points for $x(t)$ and $y(t)$ respectively.  
   - Likely unreliable due to potential high-degree polynomial oscillations.

2. **Splines Approximations**  
   - Using $n+1$ data points for $x(t)$ and $y(t)$ respectively.  
   - More reliable and computationally expensive.

3. **Bezier Curves with Hermite Polynomials**  
   - Combines reliability with lower computational cost.  
   - Suitable for smooth curve fitting.

### Numerical Differentiation

Derivative of given function $f(x)$ at $x_0$

$$\begin{aligned}
f'(x_0) & = \lim_{h \to 0} \frac{f(x_0 + h) - f(x_0)}{h} \\
& \approx \frac{f(x_0 + h) - f(x_0)}{h}, \quad |h| \text{ tiny}
\end{aligned}$$

How good is this approximation?

By Taylor expansion, there is a $\xi$ between $x_0$ and $x_0 + h$,

$$\begin{aligned}
f(x_0 + h) & = f(x_0) + h f'(x_0) + \frac{1}{2} h^2 f''(\xi), \\
\text{therefore } f'(x_0) & = \frac{f(x_0 + h) - f(x_0)}{h} - \frac{1}{2} h f''(\xi) \\
& \approx \frac{f(x_0 + h) - f(x_0)}{h}.
\end{aligned}$$

1.  forward-difference formula for $h > 0$,
2. backward-difference formula for $h < 0$.
**Example**: Use the forward-difference formula to approximate the derivative of $f(x) = \ln(x)$ at $x_0 = 1.8$, using $h = 0.1, 0.05, 0.01$.

Because $f''(\xi) = -1/\xi^2$ for $\xi \in [x_0, x_0 + h] \subset [1.8, 1.9]$, it follows that the approximation error

$$\frac{1}{2} |h f''(\xi)| \leq \frac{1}{2} \left| \frac{h}{1.8^2} \right|.$$
### Numerical Differentiation via polynomial interpolation
Suppose $\{ x_{0},x_{1},\dots x_{n} \}:=\mathbf{X}$ are $n+1$ distinct numbers,
$$f(x) = \left( \sum_{j=0}^{n} f(x_j) L_j(x) \right) + \frac{f^{(n+1)}(\xi(x))}{(n+1)!} \prod_{i=0}^{n} (x - x_i), \quad L_j(x) = \prod_{i \neq j} \frac{(x - x_i)}{(x_j - x_i)},$$

for some $\xi(x)$, so
$$ \begin{align}
 f'(x)  & = \left( \sum_{j=0}^{n} f(x_j) L'_j(x) \right) + \left( \frac{f^{(n+1)}(\xi(x))}{(n+1)!} \right) \frac{d}{dx} \left( \prod_{i=0}^{n} (x - x_i) \right)\\
 & + \underbrace{ \frac{d}{dx} \left( \frac{f^{(n+1)}(\xi(x))}{(n+1)!} \right) \left( \prod_{i=0}^{n} (x - x_i) \right) }_{ =0, \forall x \in  \mathbf{X} }.
\end{align}
$$
so we just do one step further:$$
\begin{aligned}
f^{\prime}(x_k) & =\left(\sum_{j=0}^nf(x_j)L_j^{\prime}(x_k)\right)+\left(\frac{f^{(n+1)}(\xi(x_k))}{(n+1)!}\right)\left(\prod_{i\neq k}(x_k-x_i)\right) \\
 & \approx\sum_{j=0}^nf(x_j)L_j^{\prime}(x_k).
\end{aligned}
$$
this is **the $n+1$ point formula**, works for any nodal points.

#### Example
$n =1$, we have $2$ nodal points$$L_{0}(x) = \frac{x - x_{1}}{x_{0} - x_{1}}, \quad L'_{0}(x) = \frac{1}{x_{0} - x_{1}},$$
$$L_{1}(x) = \frac{x - x_{0}}{x_{1} - x_{0}}, \quad L'_{1}(x) = \frac{1}{x_{1} - x_{0}} = -L'_{0}(x)$$

so we have $$
f'(x_{0}) \approx f(x_{0}) L'_{0}(x_{0})+ f(x_{1})L'_{0}(x_{0}) = \frac{f(x_{0}) - f(x_{1})}{x_{0}-x_{1}} \underbrace{ = f'(x_{1}) }_{ \text{easy to verify} }
$$
Actually, for a given Lagrange Poly $$
L_j(x) = \prod_{i \neq j} \frac{(x - x_i)}{(x_j - x_i)}
$$
it's easy to see $$
L'_{j}(x) = \prod_{i \neq j}^{} \frac{1}{x_{j}-x_{i}} \cdot \sum_{i\neq j}\prod_{k\neq i,j}(x-x_{k}) 
$$
then for the nodal points $$
L_{j}'(x_{p}) = \begin{cases}
\sum_{i \neq j} \frac{1}{x_{j}-x_{i}} & x_{j} = x_{p} \\
\prod_{i \neq j} \frac{1}{x_{j}-x_{i}}\prod_{k \neq p,j} (x_{p}-x_{k}) & x_{j} \neq x_{p}
\end{cases} \quad \forall x_{p} \in \mathbf{X}
$$

### Second order derivatives, equi-spaced points
use Taylor expansion:
$$
\begin{aligned}
f(x_0+h) & =f(x_0)+f^{\prime}(x_0)h+\frac{1}{2}f^{\prime\prime}(x_0)h^2+\frac{1}{6}f^{\prime\prime\prime}(x_0)h^3 \\
 & \quad+\frac{1}{24}f^{(4)}(\xi_+)h^4, \\
f(x_0-h) & =f(x_0)-f^{\prime}(x_0)h+\frac{1}{2}f^{\prime\prime}(x_0)h^2-\frac{1}{6}f^{\prime\prime\prime}(x_0)h^3 \\
 & \quad+\frac{1}{24}f^{(4)}(\xi_-)h^4.
\end{aligned}
$$
then we add the 2 equations
$$
\begin{aligned}
f(x_0+h)+f(x_0-h) & =2f(x_0)+f^{\prime\prime}(x_0)h^2+\frac{h^4}{24}\left(f^{(4)}(\xi_+)+f^{(4)}(\xi_-)\right) \\
 & =2f(x_0)+f^{\prime\prime}(x_0)h^2+\frac{2h^4}{24}f^{(4)}(\xi).
\end{aligned}
$$
therefore we get the second order derivative
$$
f^{\prime\prime}(x_0)=\frac{f(x_0+h)+f(x_0-h)-2f(x_0)}{h^2}-\frac{h^2}{12}f^{(4)}(\xi).
$$
### Round off error instability
Three point midpoint formula:
$$
f'(x_{0}) = \frac{f(x_{0}+h)-f(x_{0}-h)}{2h} - \frac{h^2}{6}f^{(3)}(\xi)
$$
> Division by $2h$ magnifies the round-off error.

assume:
$$
\begin{aligned}
f(x_0+h)\quad & =\quad\widehat{f}(x_0+h)+e(x_0+h) \\
f(x_0-h)\quad & =\quad\widehat{f}(x_0-h)+e(x_0-h)
\end{aligned}
$$
for $\left| e(x_{0}) \pm h \right| \leq \epsilon$
then we have $$
\begin{aligned}
f^{\prime}(x_0) & -\frac{\widehat{f}(x_0+h)-\widehat{f}(x_0-h)}{2h} \\
 & =\frac{e(x_0+h)-e(x_0-h)}{2h}-\frac{h^2}{6}f^{(3)}(\xi)
\end{aligned}
$$
we assume $\left| f^{(3)}(\xi) \right|\leq M$, then we have $$
\left|f^{\prime}(x_0)-\frac{\widehat{f}(x_0+h)-\widehat{f}(x_0-h)}{2h}\right|\leq\frac{\epsilon}{h}+\frac{Mh^2}{6}\overset{\mathrm{def}}{\operatorname*{\operatorname*{=}}}e(h).
$$
and the error $e(h)$ is smallest at $$
h_{min} = \left( \frac{3\epsilon}{M} \right) ^{1/3} = O(\epsilon^{1/3})
$$
with $e_{min}(h)= \frac{1}{2}(9M\epsilon^{2})^{1/3}=O(\epsilon^{2/3})$.

### Richardson's Extrapolation
**Given** (I): A formula $N_1(h)$ that approximates an unknown constant $M$ for any $h \neq 0$.  
Example: $f'(x_0) \approx \frac{f(x_0 + h) - f(x_0)}{h}$

**Given** (II): Truncation error satisfies power series for $h \neq 0$
$$M - N_1(h) = K_1h + K_2h^2 + K_3h^3 + \cdots = O(h),\tag{1}$$
with (unknown) constants $K_1, K_2, K_3, \ldots$.

$$\left(f'(x_0) - \frac{f(x_0 + h) - f(x_0)}{h}\right) = -\frac{1}{2}hf''(x_0) - \cdots - \frac{1}{n!}h^{n-1}f^{(n)}(x_0) - \cdots$$

**Goal**: Generate higher order approximations

**Key**: Equation (1) works for any $h \neq 0$, including $\frac{h}{2}$.

> substitute $\frac{h}{2}$ instead of $h$:
$$M - N_1\left(\frac{h}{2}\right) = K_1\left(\frac{h}{2}\right) + K_2\left(\frac{h}{2}\right)^2 + K_3\left(\frac{h}{2}\right)^3 + \cdots.\tag{2}$$ 
$(2)\times2-(1):$
$$\begin{align} M - N_2(h)  & = -\frac{K_2}{2}h^2 - \frac{3K_3}{4}h^3 - \cdots - (1-2^{-(t-1)})K_th^t - \cdots \\


 &:= \hat{K}_2h^2 + \hat{K}_3h^3 + \cdots + \hat{K}_th^t + \cdots = O(h^2)
\end{align}$$, where$$N_2(h) = N_1\left(\frac{h}{2}\right) + \left(N_1\left(\frac{h}{2}\right) - N_1(h)\right).$$ 
Equation (3) again power series, but now 2nd order.
![[Screenshot 2025-03-15 at 15.17.59.png]]
![[Screenshot 2025-03-15 at 15.19.06.png]]
### Richardson's Extrapolation Table
![[Screenshot 2025-03-15 at 15.19.44.png]]
### Even power series 
The difference is that $$
M - N_{1}(h) = K_{1} h^{2} + K_{2} h^{4} + K_{3} h^{6}+ \dots = O(h^{2})

$$
just do the same and you will find
![[Screenshot 2025-03-15 at 15.22.57.png]]
![[Screenshot 2025-03-15 at 15.23.36.png]]
#### Example
we consider the Taylor expansion for a given function $f(x)$ with $h>0$. 
$$
\begin{aligned}
f(x+h)\quad & =\quad f(x)+f^{\prime}(x)h+\frac{1}{2}f^{\prime\prime}(x)h^2+\cdots+\frac{1}{n!}f^{(n)}(x)h^n+\cdots, \\
f(x-h)\quad & =\quad f(x)-f^{\prime}(x)h+\frac{1}{2}f^{\prime\prime}(x)h^2+\cdots+\frac{1}{n!}f^{(n)}(x)(-h)^n+\cdots.
\end{aligned}
$$
so we take the difference to get the derivative:
$$
\frac{f(x+h)-f(x-h)}{2h}=f^{\prime}(x)+\cdots+\frac{1}{(2t+1)!}f^{(2t+1)}(x)h^{2t}+\cdots.
$$
then we can define $$
N_{1}(h) = \frac{f(x+h)-f(x-h)}{2h}
$$
and this is a second order approximation. So for the 4th order approximation:
$$
\begin{align}
f^{\prime}(x) & \approx N_1(h)+\frac{N_1(h)-N_1(2h)}{3} \\
 & =\frac{f(x-2h)-8f(x-h)+8f(x+h)-f(x+2h)}{12h}.
\end{align}

$$
#### Example
**Approximate** $f'(2.0)$ with central difference $N_1(0.1)$ and extrapolation $N_2(0.1)$ for $f(x) = xe^x$.

**Solution**: $f'(x) = (1+x)e^x$, therefore $f'(2.0) = 3e^2 \approx 22.167$.

$$N_1(0.1) = \frac{f(2.1) - f(1.9)}{2 \times 0.1} \approx 22.229.$$

$$N_1(0.2) = \frac{f(2.2) - f(1.8)}{2 \times 0.2} \approx 22.414.$$

$$N_2(h) = N_1(h) + \frac{N_1(h) - N_1(2h)}{3} \approx 22.167.$$
### Numerical Integration
**Goal**: Numerical method / quadrature for approximating $\int_{a}^{b} f(x)dx$

**Approach**: Replacing $f(x)$ by a polynomial.

**Choose**: $n + 1$ points $a \leq x_0 < x_1 < \ldots < x_n \leq b$.

**Interpolation**:
$$f(x) = P(x) + \frac{f^{(n+1)}(\xi(x))}{(n+1)!} \prod_{j=0}^{n}(x - x_j), \quad P(x) = \sum_{j=0}^{n}f(x_j)L_j(x).$$

Approximate Integration:
$$\begin{align}
\int_{a}^{b} f(x)dx  & = \left( \int_{a}^{b}P(x)dx \right) + \frac{1}{(n+1)!} \int_{a}^{b}f^{(n+1)}(\xi(x)) \prod_{j=0}^{n}(x - x_j)dx \\
 & = \left( \sum_{j=0}^{n}a_jf(x_j) \right) + \frac{1}{(n+1)!} \int_{a}^{b}f^{(n+1)}(\xi(x)) \prod_{j=0}^{n}(x - x_j)dx \\
 & \approx \sum_{j=0}^{n}a_jf(x_j)
\end{align}$$
with $$
a_{j} = \int _{a}^{b}L_{j}(x) \, dx = \int _{a}^{b}\prod_{k\neq j}^{} \frac{x-x_{k}}{x_{j}-x_{k}} \, dx
$$
### The Trapezoidal Rule: $n=1, x_0=a, x_1=b, h=b-a$

- **Linear Interpolation**:
  $$
\begin{aligned}
P_1(x) & = & \frac{(x-x_1)}{(x_0-x_1)}f(x_0)+\frac{(x-x_0)}{(x_1-x_0)}f(x_1), \\
f(x) & = & P_1(x)+\frac{1}{2}f^{\prime\prime}(\xi(x))(x-x_0)(x-x_1).
\end{aligned}$$

- **Quadrature**:
  $$
  \int_a^b P_1(x) \, dx = \int_a^b \left[ \frac{(x - x_1)}{(x_0 - x_1)} f(x_0) + \frac{(x - x_0)}{(x_1 - x_0)} f(x_1) \right] dx
  $$
  $$
  = \frac{1}{2} \left[ \frac{(x - x_1)^2}{(x_0 - x_1)} f(x_0) + \frac{(x - x_0)^2}{(x_1 - x_0)} f(x_1) \right]_a^b = \frac{h}{2} (f(x_0) + f(x_1))
  $$

- **Error**:
  $$
  \text{error} = \int_a^b \frac{1}{2} f''(\xi(x)) (x - x_0)(x - x_1) \, dx
  $$
  $$
  = \frac{f''(\xi)}{2} \int_a^b (x - x_0)(x - x_1) \, dx = \frac{f''(\xi)}{12} (b - a)^3
  $$

---

### Simpson's Rule: $n=2, x_0=a, x_1=\frac{a+b}{2}, x_2=b, h=\frac{b-a}{2}$

- **Quadratic Interpolation**:
  $$
  P_2(x_j) = f(x_j), \quad j = 0, 1, 2
  $$
  $$\begin{align}
  P_2(x)  & = \frac{(x - x_1)(x - x_2)}{(x_0 - x_1)(x_0 - x_2)} f(x_0) \\
 &  + \frac{(x - x_1)(x - x_0)}{(x_2 - x_1)(x_2 - x_0)} f(x_2) \\
 &  + \frac{(x - x_0)(x - x_2)}{(x_1 - x_0)(x_1 - x_2)} f(x_1)
\end{align}

  $$
- **Interpolation Error**:
  $$
  f(x) = P_2(x) + \frac{1}{3!} f^{(4)}(\xi(x)) (x - x_0)(x - x_1)(x - x_2)
  $$
- **Simpson's Rule and Error**:
  $$
  \int_a^b f(x) \, dx = \int_a^b P_2(x) \, dx + \int_a^b \frac{1}{3!} f^{(4)}(\xi(x)) (x - x_0)(x - x_1)(x - x_2) \, dx
  $$
  $$
  \approx \int_a^b P_2(x) \, dx = \frac{h}{3} (f(x_0) + 4 f(x_1) + f(x_2))
  $$
- Then we follow the book, and we'll find the 
- **Quadrature Error**:
  $$\begin{align}
 & \frac{1}{3!} \int_a^b f^{(4)}(\xi(x)) (x - x_0)(x - x_1)(x - x_2) \, dx  \\
= & \frac{f^{(4)}(\xi)}{6}\underbrace{ \int _{a}^{b}(x-x_{0})(x - x_{1})(x- x_{2}) \, dx  }_{ \text{you can easily see this is }0 } \\
 = & 0
\end{align}
  
  $$
- Note: "Error estimate **wrong**. Need approach better than in book."

---

### Simpson's Rule: $n=3, x_0=a, x_1=\frac{a+b}{2}, x_2=b, h=\frac{b-a}{2}$

- **Cubic Interpolation with Double Node at $x_1$**:
  $$
  P_3(x_j) = f(x_j), \quad j = 0, 1, 2, \quad P_3'(x_1) = f'(x_1)
  $$
  $$\begin{align}
P_3(x) &  = \frac{(x - x_1)^2 (x - x_2)}{(x_0 - x_1)^2 (x_0 - x_2)} f(x_0) + \frac{(x - x_1)^2 (x - x_0)}{(x_2 - x_1)^2 (x_2 - x_0)} f(x_2) \\
 & + \frac{(x - x_0)(x - x_2)}{(x_1 - x_0)(x_1 - x_2)} \left( 1 - \frac{(x - x_1)(2 x_1 - x_0 - x_2)}{(x_1 - x_0)(x_1 - x_2)} \right) f(x_1) \\
 &   + \frac{(x - x_0)(x - x_1)(x - x_2)}{(x_1 - x_0)(x_1 - x_2)} f'(x_1)
\end{align}
  
  $$
- **Interpolation Error**:
  $$
  f(x) = P_3(x) + \frac{1}{4!} f^{(4)}(\xi(x)) (x - x_0)(x - x_1)^2 (x - x_2)
  $$

---

### Simpson's Rule: $n=3$ (Quadrature Rule)

- **Quadrature Rule**:
  $$\begin{align}
 \int_a^b P_3(x) \, dx &  = f(x_0) \int_a^b \frac{(x - x_1)^2 (x - x_2)}{(x_0 - x_1)^2 (x_0 - x_2)} \, dx + f(x_2) \int_a^b \frac{(x - x_1)^2 (x - x_0)}{(x_2 - x_1)^2 (x_2 - x_0)} \, dx \\
  & + f(x_1) \int_a^b \frac{(x - x_0)(x - x_2)}{(x_1 - x_0)(x_1 - x_2)} \left( 1 - \frac{(x - x_1)(2 x_1 - x_0 - x_2)}{(x_1 - x_0)(x_1 - x_2)} \right) \, dx \\
   & + f'(x_1) \int_a^b \frac{(x - x_0)(x - x_1)(x - x_2)}{(x_1 - x_0)(x_1 - x_2)} \, dx \\
 &  = \frac{h}{3} (f(x_0) + 4 f(x_1) + f(x_2))
\end{align}
  
  $$
- **Note**: "Stroke of luck: $f'(x_1)$ does not end up in quadrature"
- **Quadrature Error**:
  $$
\begin{align}
 \text{Quadrature Error}  & = \frac{1}{4!} \int_a^b f^{(4)}(\xi(x)) (x - x_0)(x - x_1)^2 (x - x_2) \, dx \\
 & = \frac{f^{(4)}(\xi)}{4!} \int_a^b (x - x_0)(x - x_1)^2 (x - x_2) \, dx  \\
 & = -\frac{f^{(4)}(\xi)}{90} h^5
\end{align}
 

 
  $$

---

### Simpson's Rule: $n=3$ (Final Form)

- **Final Formula**:
  $$
  \int_a^b f(x) \, dx = \frac{h}{3} (f(x_0) + 4 f(x_1) + f(x_2)) - \frac{f^{(4)}(\xi)}{90} h^5
  $$
- Note: "Book wrong $f'(x_1) \neq P'(x_1)$, Correct plot: $f'(x_1) = P'(x_1)$"

---

### Example: Approximate $\int_0^2 f(x) \, dx$ - Simpson Wins

|       | (a) | (b) | (c)       | (d)      | (e)    | (f) |
|-------|-----|-----|-----------|----------|--------|-----|
| $f(x)$| $x^4$ | $x^4$ | $(x+1)^{-1}$ | $\sqrt{1+x}$ | $\sin x$ | $\exp(x)$  |
| Exact Value | 2.667 | 6.400 | 1.099 | 2.958 | 1.416 | 6.389 |
| Trapezoidal | 4.000 | 16.000 | 1.333 | 3.326 | 0.909 | 8.389 |
| Simpson's | 2.667 | 6.667 | 1.111 | 2.964 | 1.425 | 6.421 |

- **Definition - Degree of Precision (DoP)**: Integer $n$ such that quadrature formula is **exact** for $f(x) = x^k$, for each $k = 0, 1, \ldots, n$ but inexact for $f(x) = x^{n+1}$
- **Theorem**: Quadrature formula is exact for all polynomials of degree at most $n$.
- **Simplification**: Only need to verify exactness on interval $[0,1]$. DoP = 1 for Trapezoidal Rule, DoP = 3 for Simpson.
