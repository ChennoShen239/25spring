## Test equations for stiff ODEs

$$
\frac{dy}{dt} = \lambda y,\quad y(0) = \alpha,\quad \text{for } \lambda < 0.
$$

- Test equation has transient solution $y(t) = \alpha e^{\lambda t}$ that decays to 0 as $t \to \infty$.
- Lipschitz constant $L = |\lambda|$ can be large even as the solution decays to 0.

- 测试方程具有瞬态解 $y(t) = \alpha e^{\lambda t}$，当 $t \to \infty$ 时，该解趋于 0。
- Lipschitz 常数 $L = |\lambda|$ 即使在解趋于 0 的情况下也可能很大。
### Desired properties of numerical methods:

- **Convergence**:  
  $$
  \lim_{h \to 0} |y(t_j) - w_j| = 0.
  $$

- **Numerical stability**: small error in $\alpha$ implies small error in $w_j$.
## Euler’s Method

$$
\frac{dy}{dt} = \lambda y,\quad y(0) = \alpha,\quad \text{for } \lambda < 0.
$$
- Euler’s method: $w_0 = \alpha$,  
  $$
  w_{j+1} = w_j + h \lambda w_j = (1 + \lambda h) w_j,
  $$
  for $j = 0, 1, \cdots$
- Solving for $w_j$:  
  $$
  w_j = (1 + \lambda h)^j w_0 = (1 + \lambda h)^j \alpha
  $$
  $$
  |y(t_j) - w_j| = \left| e^{\lambda h j} - (1 + \lambda h)^j \right| |\alpha|
  $$
- For convergence, need:  $$
  |1 + \lambda h| < 1,\quad \text{or} \quad -2 < \lambda h < 0.
  $$

---

- Now assume a round-off error of $\delta$ in $w_0$:  
  $$
  \widehat{w}_0 = \alpha + \delta.
  $$

- Euler’s method numerically produces, for $j = 0, 1, \cdots$:  
  $$
  \widehat{w}_{j+1} = (1 + \lambda h) \widehat{w}_j = (1 + \lambda h)^{j+1} (\alpha + \delta).
  $$

- Round-off error at step $(j + 1)$:  
  $$
  \widehat{w}_{j+1} - w_{j+1} = (1 + \lambda h)^{j+1} \delta.
  $$

- For numerical stability, need:  
  $$
  |1 + \lambda h| < 1,\quad \text{or} \quad -2 < \lambda h < 0.
  $$

> **Bad news**: Larger $|\lambda|$ ⇒ resolving fast decaying solution with tiny $h$
## Implicit Trapezoid

Test equation:  
$$
\frac{dy}{dt} = \lambda y,\quad y(0) = \alpha,\quad \text{for } \lambda < 0.
$$

- **Implicit Trapezoid**   ( **隐式梯形法**  )
  $$
  w_{j+1} = w_j + \frac{h}{2} \left( f(t_{j+1}, w_{j+1}) + f(t_j, w_j) \right) 
         = w_j + \frac{\lambda h}{2} (w_{j+1} + w_j)
  $$

- **Solving for** $w_j$:  
  $$
  w_j = \left( \frac{1 + \frac{\lambda h}{2}}{1 - \frac{\lambda h}{2}} \right)^j \alpha
  $$

- **Absolute stability**  
  $$
  \left| \frac{1 + \frac{\lambda h}{2}}{1 - \frac{\lambda h}{2}} \right| < 1
  $$
  for as long as $\mathrm{Re}(\lambda h) < 0$.
## Implicit Trapezoid with Newton Iteration

- **Implicit Trapezoid**
  $$
  w_{j+1} = w_j + \frac{h}{2} \left( f(t_{j+1}, w_{j+1}) + f(t_j, w_j) \right)
  $$

- $w_{j+1}$ is root to  
  $$
  \mathbf{F}(w) \overset{\text{def}}{=} w - w_j - \frac{h}{2} \left( f(t_{j+1}, w) + f(t_j, w_j) \right) = 0
  $$

- **Newton Iteration**: $w_{j+1}^{(0)} = w_j$ (no predictor); for $\ell = 0, 1, \cdots$
  $$
\begin{align}
  w_{j+1}^{(\ell+1)}  & = w_{j+1}^{(\ell)} - \frac{\mathbf{F}(w_{j+1}^{(\ell)})}{\mathbf{F}'(w_{j+1}^{(\ell)})} \\
 &  = w_{j+1}^{(\ell)} - \frac{
    w_{j+1}^{(\ell)} - w_j - \frac{h}{2} \left( f(t_{j+1}, w_{j+1}^{(\ell)}) + f(t_j, w_j) \right)
  }{
    1 - \frac{h}{2} \frac{\partial f}{\partial y}(t_{j+1}, w_{j+1}^{(\ell)})
  }
\end{align}

  $$
## Trapezoid is more reliable for stiff ODEs

## Section 6.1

## Solving Linear Equations

- **Example**: solving for $x_1, x_2, x_3, x_4$ in a system of linear equations:

$$
\begin{aligned}
E_1\!: &\quad x_1 + x_2 \phantom{{} - x_3} + 3x_4 = 4, \\
E_2\!: &\quad 2x_1 + x_2 - x_3 + x_4 = 1, \\
E_3\!: &\quad 3x_1 - x_2 - x_3 + 2x_4 = -3, \\
E_4\!: &\quad -x_1 + 2x_2 + 3x_3 - x_4 = 4.
\end{aligned}
$$

#### Solution techniques (elementary operations)

- Multiply equation $E_j$ by any constant $\lambda$ and add to equation $E_i$, $i \ne j$, with the resulting equation used in place of $E_i$:  
  $$
  (E_i + \lambda E_j) \rightarrow (E_i)
  $$

- Equations $E_i$ and $E_j$ can be swapped in order:  
  $$
  (E_i) \leftrightarrow (E_j)
  $$
## Solving Linear Equations with Pivoting

### Initial system:
$$
\begin{aligned}
E_1\!: &\quad x_1 - x_2 + 2x_3 - x_4 = -8 \\
E_2\!: &\quad 2x_1 - 2x_2 + 3x_3 - 3x_4 = -20 \\
E_3\!: &\quad x_1 + x_2 + x_3 = -2 \\
E_4\!: &\quad x_1 - x_2 + 4x_3 + 3x_4 = 4
\end{aligned}
$$

### Step 1: Eliminate $x_1$ from $E_2$, $E_3$, $E_4$
$$
\begin{aligned}
(E_2 - 2E_1) &\rightarrow (E_2) \\
(E_3 - E_1) &\rightarrow (E_3) \\
(E_4 - E_1) &\rightarrow (E_4)
\end{aligned}
$$

### New system:
$$
\begin{aligned}
E_1\!: &\quad x_1 - x_2 + 2x_3 - x_4 = -8 \\
E_2\!: &\quad \phantom{x_1}  - x_3 - x_4 = 6 \\
E_3\!: &\quad \phantom{x_1} 2x_2- x_3 - x_4 = -4 \\
E_4\!: &\quad \phantom{x_1} 2x_3 + 4x_4 = 12
\end{aligned}
$$


### Step 2: Pivoting — swap $E_2 \leftrightarrow E_3$

$$
\begin{aligned}
E_1\!: &\quad x_1 - x_2 + 2x_3 - x_4 = -8 \\
E_2\!: &\quad -x_3 - x_4 = -4 \\
E_3\!: &\quad 2x_2 - x_3 + x_4 = 6 \\
E_4\!: &\quad 2x_3 + 4x_4 = 12
\end{aligned}
$$

### Step 3: Eliminate $x_3$ from $E_4$:  
$$
(E_4 + 2 \times E_2) \rightarrow (E_4)
$$
$$
\begin{aligned}
E_4\!: &\quad 2x_4 = 4
\end{aligned}
$$
### Backward substitution:
$$
x_4 = 2,\quad x_3 = 2,\quad x_2 = 3,\quad x_1 = -7
$$
## Matrices and Vectors

- **Matrix and vector**  
  $$
  A = \begin{pmatrix}
  a_{11} & a_{12} & \cdots & a_{1n} \\
  a_{21} & a_{22} & \cdots & a_{2n} \\
  \vdots & \vdots & \ddots & \vdots \\
  a_{m1} & a_{m2} & \cdots & a_{mn}
  \end{pmatrix}
  \overset{\text{def}}{=} (a_{ij}) \in \mathbb{R}^{m \times n},\quad
  b = \begin{pmatrix}
  b_1 \\ b_2 \\ \vdots \\ b_m
  \end{pmatrix}
  \in \mathbb{R}^m
  $$

- **Example** system:
  $$
  \begin{aligned}
  E_1\!: &\quad x_1 + x_2 + 3x_4 = 4 \\
  E_2\!: &\quad 2x_1 + x_2 - x_3 + x_4 = 1 \\
  E_3\!: &\quad 3x_1 - x_2 - x_3 + 2x_4 = -3 \\
  E_4\!: &\quad -x_1 + 2x_2 + 3x_3 - x_4 = 4
  \end{aligned}
  $$

- **Coefficient matrix** $A$:
  $$
  A \overset{\text{def}}{=} \begin{pmatrix}
  1 & 1 & 0 & 3 \\
  2 & 1 & -1 & 1 \\
  3 & -1 & -1 & 2 \\
  -1 & 2 & 3 & -1
  \end{pmatrix}
  $$

- **Unknown vector** $\mathbf{x}$:
  $$
  \mathbf{x} \overset{\text{def}}{=} \begin{pmatrix}
  x_1 \\ x_2 \\ x_3 \\ x_4
  \end{pmatrix}
  $$

- **Right-hand side vector** (RHS) $b$:
  $$
  \mathbf{b} \overset{\text{def}}{=} \begin{pmatrix}
  4 \\ 1 \\ -3 \\ 4
  \end{pmatrix}
  $$
## Gaussian Elimination for $A \in \mathbb{R}^{2 \times 2},\ a_{11} \ne 0$

Matrix form:
$$
A = \begin{pmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{pmatrix},\quad
b = \begin{pmatrix} b_1 \\ b_2 \end{pmatrix},\quad
x = \begin{pmatrix} x_1 \\ x_2 \end{pmatrix}
$$

### Algorithm GE:

$$
\begin{aligned}
\ell &= \frac{a_{21}}{a_{11}} & \text{(elimination: } E_2 - \ell E_1 \rightarrow E_2 \text{)} \\
a_{22} &= a_{22} - \ell \cdot a_{12} & \text{(matrix overwrite)} \\
b_2 &= b_2 - \ell \cdot b_1 & \text{(RHS overwrite)} \\
x_2 &= \frac{b_2}{a_{22}} & \text{(backward substitution)} \\
x_1 &= \frac{b_1 - a_{12} \cdot x_2}{a_{11}}
\end{aligned}
$$

> **How could Algorithm GE go wrong?**

---

### Numerical Experiment

- **Random $2 \times 2$ system**:
  $$
  A = \text{randn}(2,2),\quad b = \text{randn}(2,1)
  $$

- **Make $(1,1)$ entry small** (ill-conditioning test):  
  for $k = 1, 2, \dots, 17$  
  $$
  B = A,\quad B(1,1) = \text{randn} / 10^k
  $$

- Solve $Bx = b$ using **Algorithm GE**  
- Compute residual:
  $$
  r \overset{\text{def}}{=} b - Bx
  $$

> Plot: $k$ vs. $\max(|r|)$
![[Pasted image 20250422215440.png]]
## General Linear Equations

- System of equations:
$$
\begin{aligned}
E_1\!: &\quad a_{11}x_1 + a_{12}x_2 + \cdots + a_{1n}x_n = b_1 \\
E_2\!: &\quad a_{21}x_1 + a_{22}x_2 + \cdots + a_{2n}x_n = b_2 \\
&\quad \vdots \\
E_n\!: &\quad a_{n1}x_1 + a_{n2}x_2 + \cdots + a_{nn}x_n = b_n
\end{aligned}
$$

- Matrix form:
$$
A \overset{\text{def}}{=} \begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{n1} & a_{n2} & \cdots & a_{nn}
\end{pmatrix},\quad
b \overset{\text{def}}{=} \begin{pmatrix}
b_1 \\ b_2 \\ \vdots \\ b_n
\end{pmatrix},\quad
x \overset{\text{def}}{=} \begin{pmatrix}
x_1 \\ x_2 \\ \vdots \\ x_n
\end{pmatrix}
$$

- Equation $E_j$ maps to **row $j$** of $A$:  
  $$
  (a_{j1}, a_{j2}, \cdots, a_{jn}),\quad 1 \le j \le n
  $$

- Variable $x_k$ relates to **column $k$** of $A$:  
  $$
  \begin{pmatrix}
  a_{1k} \\ a_{2k} \\ \vdots \\ a_{nk}
  \end{pmatrix},\quad 1 \le k \le n
  $$

- **Pivoting**: choose **largest entry in absolute value** in the first column:
  $$
  \text{piv} \overset{\text{def}}{=} \arg\max_{1 \le j \le n} |a_{j1}|,\quad
  (|a_{\text{piv},1}| = \max_{1 \le j \le n} |a_{j1}|)
  $$

- Then exchange equations $E_1$ and $E_{\text{piv}}$:
  $$
  (E_1 \leftrightarrow E_{\text{piv}})
  $$
- **Elimination** of $x_1$ from $E_2$ through $E_n$:
  $$
  \left( E_j - \frac{a_{j1}}{a_{11}} E_1 \right) \rightarrow (E_j),\quad
  \left| \frac{a_{j1}}{a_{11}} \right| \le 1,\quad 2 \le j \le n
  $$
> This is because we have already have $E_{\text{piv}}$ in the $1$ st row so that any other rows will have a less equal coefficient $a_{j1}$ compared to $a_{11} = a_{\text{piv},1}$

- **New row $j$ of $A$**:
  $$
  \left( a_{j1}\ a_{j2}\ \cdots\ a_{jn} \right)
  - \frac{a_{j1}}{a_{11}} \left( a_{11}\ a_{12}\ \cdots\ a_{1n} \right)
   = \left( 0,\ a_{j2} - \frac{a_{j1}}{a_{11}} a_{12},\ \cdots,\ a_{jn} - \frac{a_{j1}}{a_{11}} a_{1n} \right),\quad 2 \le j \le n
  $$

- **New $j^{\text{th}}$ component of $b$**:
  $$
  b_j - \frac{a_{j1}}{a_{11}} b_1
  $$
## Gaussian Elimination with Partial Pivoting (III)

- **New** matrix $A$:
$$
\textbf{new } A = \begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
0 & \mathbf{a}_{22} & \cdots & \mathbf{a}_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
0 & \mathbf{a}_{n2} & \cdots & \mathbf{a}_{nn}
\end{pmatrix}
\quad \text{(overwrite } A \text{)}
$$

- **Where**:
$$
\mathbf{a_{jk}} = a_{jk} - \frac{a_{j1}}{a_{11}} a_{1k},\quad 2 \le j \le n,\quad 2 \le k \le n
$$

- **New** vector $b$:
$$
\textbf{new } b = \begin{pmatrix}
b_1 \\
\mathbf{b_2} \\
\vdots \\
\mathbf{b_n}
\end{pmatrix}
\quad \text{(overwrite } b \text{)}
$$

- **Where**:
$$
\mathbf{b_j} = b_j - \frac{a_{j1}}{a_{11}} b_1,\quad 2 \le j \le n
$$

> **Note**: Bold-faced entries are computed from the elimination process.
## Gaussian Elimination with Partial Pivoting (IV)

Matrix form:
$$
A = \begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
0 & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
0 & a_{n2} & \cdots & a_{nn}
\end{pmatrix},\quad
b = \begin{pmatrix}
b_1 \\ b_2 \\ \vdots \\ b_n
\end{pmatrix}
$$

- Repeat the same process on $E_s$ for $s = 2, \dots, n-1$:
  - **Pivoting**: choose largest absolute entry:
    $$
    \textbf{piv} \overset{\text{def}}{=} \arg\max_{s \le j \le n} |a_{js}|,\quad
    (|a_{\text{piv},s}| = \max_{s \le j \le n} |a_{js}|)
    $$

  - Swap equations $E_s \leftrightarrow E_{\text{piv}}$

- **Eliminating** $x_s$ from $E_{s+1}$ through $E_n$:
  $$
  \left(E_j - \frac{a_{js}}{a_{ss}} E_s \right) \rightarrow (E_j),\quad s+1 \le j \le n
  $$

- Update matrix entries:
  $$
  \mathbf{a_{jk}} = a_{jk} - \frac{a_{js}}{a_{ss}} a_{sk}
  \quad \text{(overwrite)}\quad a_{jk},\quad s+1 \le j \le n,\quad s+1 \le k \le n
  $$

- Update right-hand side:
  $$
  \mathbf{b_j} = b_j - \frac{a_{js}}{a_{ss}} b_s
  \quad \text{(overwrite)}\quad b_j,\quad s+1 \le j \le n
  $$
## Equations after Gaussian Elimination, Backward Substitution

Matrix form after elimination:

$$

A = \begin{pmatrix}

a_{11} & a_{12} & \cdots & a_{1n} \\

0 & a_{22} & \cdots & a_{2n} \\

\vdots & \vdots & \ddots & \vdots \\

0 & 0 & \cdots & a_{nn}

\end{pmatrix},\quad

b = \begin{pmatrix}

b_1 \\ b_2 \\ \vdots \\ b_n

\end{pmatrix}

$$

- For $s = n, n-1, \dots, 1$:

$$

x_s = \frac{b_s - \sum_{k=s+1}^{n} a_{sk} x_k}{a_{ss}}

$$

- MATLAB command for solution:

```matlab
x = A\b
```
## Gaussian Elimination: Cost Analysis (I)

- For $s = 1, 2, \dots, n - 1$:

  - **Pivoting**: $(n - s + 1)$ comparisons
    $$
    \text{piv} = \arg\max_{s \le j \le n} |a_{js}|,\quad E_s \leftrightarrow E_{\text{piv}}
    $$

  - **Eliminating** $x_s$ from $E_{s+1}$ through $E_n$:
    $$
    a_{jk} = a_{jk} - \frac{a_{js}}{a_{ss}} a_{sk},\quad s + 1 \le j \le n,\quad s + 1 \le k \le n
    $$
    $$
    b_j = b_j - \frac{a_{js}}{a_{ss}} b_s,\quad s + 1 \le j \le n
    $$

### Counting operations

- Compute `piv` for each $s$, and perform swaps $E_s \leftrightarrow E_{\text{piv}}$
- For each $s$, compute ratios $\frac{a_{js}}{a_{ss}}$ for each $j \ge s + 1$
- For each $s$, compute $a_{jk}$ for each pair of $j, k \ge s + 1$
- For each $s$, compute $b_j$ for each $j \ge s + 1$

> Do not count integer operations; do not count memory costs.
### Elimination cost:

- Compute ratios $\frac{a_{js}}{a_{ss}}$:
  $$
  \sum_{s=1}^{n-1} (n - s) = \frac{n(n - 1)}{2}
  $$

- Compute $a_{jk}$:
  $$
  \sum_{s=1}^{n-1} 2(n - s)^2 = \frac{n(n - 1)(2n - 1)}{3}
  $$

- Compute $b_j$:
  $$
  \sum_{s=1}^{n-1} 2(n - s) = n(n - 1)
  $$

### Grand total (cubic term only):
$$
\frac{2}{3} n^3 \quad \text{additions and multiplications}
$$

## Gaussian Elimination with Partial Pivoting (GEPP)

**Example**: Solve $Ax = b$ with GEPP, where  
$$
\mathbf{r} \overset{\text{def}}{=} b - Ax
$$

- **Blue**: $A \in \mathbb{R}^{n \times n}$, $b \in \mathbb{R}^n$ both random
- **Red**: $A \in \mathbb{R}^{n \times n}$ is the **Wilkinson matrix**:
  $$
  A = \begin{pmatrix}
  1 &        &        & 1 \\
  -1 & 1      &        & 1 \\
  -1 & -1     & 1      & 1 \\
  \vdots & \vdots & \ddots & \vdots \\
  -1 & -1     & \cdots & 1
  \end{pmatrix},\quad
  b \in \mathbb{R}^n\ \text{random}
  $$

### Plot:
- y-axis: $\max |\mathbf{r}|$  
- x-axis: $n$
![[Pasted image 20250422221540.png]]
**Legend**:  
- Blue line: random $A$  
- Red dashed line: Wilkinson $A$
>Partial Pivoting not enough for numerical stability

## Gaussian Elimination with Complete Pivoting, $A \in \mathbb{R}^{2 \times 2}$

Matrix form:
$$
A = \begin{pmatrix}
a_{11} & a_{12} \\
a_{21} & a_{22}
\end{pmatrix},\quad
b = \begin{pmatrix}
b_1 \\ b_2
\end{pmatrix},\quad
x = \begin{pmatrix}
x_1 \\ x_2
\end{pmatrix}
$$

- **Pivoting**: choose largest entry in absolute value:
  $$
  (\text{ip}, \text{jp}) \overset{\text{def}}{=} \arg\max_{1 \le i,j \le 2} |a_{ij}|,\quad
  (|a_{\text{ip},\text{jp}}| = \max_{1 \le i,j \le 2} |a_{ij}|)
  $$

- **Exchange** equations $E_1 \leftrightarrow E_{\text{ip}}$
- **Exchange** columns/variables $1 \leftrightarrow \text{jp}$
- **Perform** Gaussian Elimination on the resulting $2 \times 2$ system without further pivoting
- **Note**: Complete pivoting is too expensive in general
## §6.3 Matrix Algebra

### **Definition**: Let

$$
A = \begin{pmatrix}
a_{1,1} & a_{1,2} & \cdots & a_{1,m} \\
a_{2,1} & a_{2,2} & \cdots & a_{2,m} \\
\vdots & \vdots & \ddots & \vdots \\
a_{n,1} & a_{n,2} & \cdots & a_{n,m}
\end{pmatrix}
\overset{\text{def}}{=} (a_{ij}) \in \mathbb{R}^{n \times m}
$$

$$
B = \begin{pmatrix}
b_{1,1} & b_{1,2} & \cdots & b_{1,m} \\
b_{2,1} & b_{2,2} & \cdots & b_{2,m} \\
\vdots & \vdots & \ddots & \vdots \\
b_{n,1} & b_{n,2} & \cdots & b_{n,m}
\end{pmatrix}
\overset{\text{def}}{=} (b_{ij}) \in \mathbb{R}^{n \times m}
$$

Then
$$
C \overset{\text{def}}{=} \begin{pmatrix}
\alpha a_{1,1} + \beta b_{1,1} & \cdots & \alpha a_{1,m} + \beta b_{1,m} \\
\alpha a_{2,1} + \beta b_{2,1} & \cdots & \alpha a_{2,m} + \beta b_{2,m} \\
\vdots & \ddots & \vdots \\
\alpha a_{n,1} + \beta b_{n,1} & \cdots & \alpha a_{n,m} + \beta b_{n,m}
\end{pmatrix}
= \alpha A + \beta B \in \mathbb{R}^{n \times m}
$$

---

### **Example**: Let
$$
A = \begin{pmatrix}
2 & -1 & 7 \\
3 & 1 & 0
\end{pmatrix},\quad
B = \begin{pmatrix}
4 & 2 & -8 \\
0 & 1 & 6
\end{pmatrix} \in \mathbb{R}^{2 \times 3}
$$

Then
$$
C \overset{\text{def}}{=} A - 2B =
\begin{pmatrix}
-6 & -5 & 23 \\
3 & -1 & -12
\end{pmatrix} \in \mathbb{R}^{2 \times 3}
$$
## Matrix-vector product, linear equations, and dot product

System of equations:
$$
\begin{aligned}
a_{11}x_1 + a_{12}x_2 + \cdots + a_{1n}x_n &= b_1 \\
a_{21}x_1 + a_{22}x_2 + \cdots + a_{2n}x_n &= b_2 \\
\vdots \qquad \qquad\qquad & \vdots \\
a_{n1}x_1 + a_{n2}x_2 + \cdots + a_{nn}x_n &= b_n
\end{aligned}
$$

Let:
$$
A = \begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{n1} & a_{n2} & \cdots & a_{nn}
\end{pmatrix},\quad
b = \begin{pmatrix}
b_1 \\ b_2 \\ \vdots \\ b_n
\end{pmatrix},\quad
x = \begin{pmatrix}
x_1 \\ x_2 \\ \vdots \\ x_n
\end{pmatrix}
$$

Matrix-vector product:
$$
Ax \overset{\text{def}}{=} \begin{pmatrix}
a_{11}x_1 + a_{12}x_2 + \cdots + a_{1n}x_n \\
a_{21}x_1 + a_{22}x_2 + \cdots + a_{2n}x_n \\
\vdots \\
a_{n1}x_1 + a_{n2}x_2 + \cdots + a_{nn}x_n
\end{pmatrix},\quad \text{for any } A \in \mathbb{R}^{n \times m},\ x \in \mathbb{R}^m
$$

The equations become:
$$
Ax = b
$$

Each component:
$$
(Ax)_j = \left( a_{j1}x_1 + a_{j2}x_2 + \cdots + a_{jn}x_n \right) = \left( a_{j1}\ a_{j2}\ \cdots\ a_{jn} \right) 
\begin{pmatrix}
x_1 \\ x_2 \\ \vdots \\ x_n
\end{pmatrix}
$$

> Each component in $Ax$ is just a dot product
## Matrix-Matrix Product

Let
$$
A = \begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1m} \\
a_{21} & a_{22} & \cdots & a_{2m} \\
\vdots & \vdots & \ddots & \vdots \\
a_{n1} & a_{n2} & \cdots & a_{nm}
\end{pmatrix} \in \mathbb{R}^{n \times m},\quad
B = \begin{pmatrix}
b_{11} & b_{12} & \cdots & b_{1p} \\
b_{21} & b_{22} & \cdots & b_{2p} \\
\vdots & \vdots & \ddots & \vdots \\
b_{m1} & b_{m2} & \cdots & b_{mp}
\end{pmatrix} \in \mathbb{R}^{m \times p}
$$

### Column Partition:
$$
B = \left( \mathbf{b}_1\ \mathbf{b}_2\ \cdots\ \mathbf{b}_p \right),\quad
\mathbf{b}_j \overset{\text{def}}{=} \begin{pmatrix}
b_{1j} \\ b_{2j} \\ \vdots \\ b_{mj}
\end{pmatrix} \in \mathbb{R}^m,\quad j = 1, \dots, p
$$

### Definition:
$$
AB = A \left( \mathbf{b}_1\ \mathbf{b}_2\ \cdots\ \mathbf{b}_p \right)
\overset{\text{def}}{=} \left( A\mathbf{b}_1\ A\mathbf{b}_2\ \cdots\ A\mathbf{b}_p \right) \in \mathbb{R}^{n \times p}
$$

### Entry-wise Formula:
$$
(AB)_{jk} = (A \mathbf{b}_k)_j =
\left( a_{j1}\ a_{j2}\ \cdots\ a_{jm} \right)
\mathbf{b}_k = \sum_{i=1}^m a_{ji} b_{ik}
$$

## Theorem: Matrix Multiplication Associativity

Let  
$$
A \in \mathbb{R}^{n \times m},\quad
B \in \mathbb{R}^{m \times p},\quad
C \in \mathbb{R}^{p \times k}
$$

Then
$$
A(BC) = (AB)C \quad \blacksquare
$$

---

### Proof:

Start with the $(s,t)$-entry of $A(BC)$:
$$
(A(BC))_{st} = \sum_{i=1}^{m} a_{si} (BC)_{it}
$$

Expand the inner product:
$$
= \sum_{i=1}^{m} a_{si} \left( \sum_{j=1}^{p} b_{ij} c_{jt} \right)
$$

Switch order of summation:
$$
= \sum_{j=1}^{p} \left( \sum_{i=1}^{m} a_{si} b_{ij} \right) c_{jt}
$$

Recognize this as matrix multiplication:
$$
= \sum_{j=1}^{p} (AB)_{sj} c_{jt}
$$

Thus:
$$
= ((AB)C)_{st} \quad \blacksquare
$$
## Special Matrices and MATLAB Commands

| **Matrix Type**         | **Symbol / Definition**                                                                                      | **MATLAB Command** |
|-------------------------|--------------------------------------------------------------------------------------------------------------|--------------------|
| **square** matrix       | $A \in \mathbb{R}^{n \times n}$                                                                               | —                  |
| **diagonal** matrix     | $D = \begin{pmatrix} d_1 & & \\ & \ddots & \\ & & d_n \end{pmatrix}$                                          | `diag(D)`          |
| **identity** matrix     | $I = \begin{pmatrix} 1 & & \\ & \ddots & \\ & & 1 \end{pmatrix}$                                              | `eye(n)`           |
| **upper-triangular**    | $U = \begin{pmatrix} u_{11} & u_{12} & \cdots & u_{1n} \\ & u_{22} & \cdots & u_{2n} \\ & & \ddots & \vdots \\ & & & u_{nn} \end{pmatrix}$ | `triu(A)`          |
| **lower-triangular**    | $L = \begin{pmatrix} l_{11} & & & \\ l_{21} & l_{22} & & \\ \vdots & \vdots & \ddots & \\ l_{n1} & l_{n2} & \cdots & l_{nn} \end{pmatrix}$ | `tril(A)`          |
## Inverse Matrices

- A square matrix $A \in \mathbb{R}^{n \times n}$ is **non-singular** if there exists a matrix $B \in \mathbb{R}^{n \times n}$ such that:
  $$
  AB = BA = I
  $$

- $B \overset{\text{def}}{=} A^{-1}$ is the **inverse** of $A$.
- A matrix without an inverse is called **singular**.
---

### Examples:

- Let
  $$
  A = \begin{pmatrix}
  2 & -1 \\
  1 & 2
  \end{pmatrix},\quad
  A^{-1} = \frac{1}{5} \begin{pmatrix}
  2 & 1 \\
  -1 & 2
  \end{pmatrix}
  $$
  Then $A$ is **non-singular**.

- Let
  $$
  C = \begin{pmatrix}
  2 & -1 \\
  0 & 0
  \end{pmatrix}
  $$
  Then $C$ is **singular**.

## Solving $Ax = b$ with Inverse

- If $A^{-1}$ is available:
  $$
  x = Ix = (A^{-1}A)x = A^{-1}(Ax) = A^{-1}b \quad \Longleftarrow \quad \textbf{so easy?}
  $$

---

### Example

Let
$$
A = \begin{pmatrix}
1 & 2 & -1 \\
2 & 1 & 0 \\
-1 & 1 & 2
\end{pmatrix},\quad
A^{-1} = \frac{1}{9} \begin{pmatrix}
-2 & 5 & -1 \\
4 & -1 & 2 \\
-3 & 3 & 3
\end{pmatrix},\quad
b \in \mathbb{R}^3
$$

Then the solution is:
$$
x = \frac{1}{9} \begin{pmatrix}
-2 & 5 & -1 \\
4 & -1 & 2 \\
-3 & 3 & 3
\end{pmatrix} b
$$

---

### Catch:
**$A^{-1}$ is rarely available and harder to compute than $x$.**
## Facts about $A^{-1}$

Assume $A^{-1}$ exists.

- $A^{-1}$ is unique.
- $(A^{-1})^{-1} = A$.
- If $B^{-1}$ exists and $A, B \in \mathbb{R}^{n \times n}$, then
  $$
  (AB)^{-1} = B^{-1} A^{-1}
  $$
## What if I have to compute $A^{-1}$ anyway?

- $A^{-1}$ is the solution to:
  $$
  AX = I,\quad X \in \mathbb{R}^{n \times n}
  $$

- Partition:
$$
  X = \left( \mathbf{x}_1\ \mathbf{x}_2\ \cdots\ \mathbf{x}_n \right),\quad
  I = \left( \mathbf{e}_1\ \mathbf{e}_2\ \cdots\ \mathbf{e}_n \right) =
  \begin{pmatrix}
  1 & & \\
  & \ddots & \\
  & & 1
  \end{pmatrix}
  $$

- Then:
  $$
  AX = I \;\Leftrightarrow\;
  A \begin{pmatrix} \mathbf{x}_1 & \mathbf{x}_2 & \cdots & \mathbf{x}_n \end{pmatrix}
  = \begin{pmatrix} \mathbf{e}_1 & \mathbf{e}_2 & \cdots & \mathbf{e}_n \end{pmatrix}
  \;\Leftrightarrow\;
  A \mathbf{x}_j = \mathbf{e}_j,\quad \text{for } j = 1, \ldots, n
  $$

> **computing $A^{-1}$** is to solve $n$ systems of equations with the same $A$.

## GEPP for solving 

$A \mathbf{x} = B \;\overset{\text{def}}{=}\; \begin{pmatrix} b_{11} & b_{12} & \cdots & b_{1n} \\ b_{21} & b_{22} & \cdots & b_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ b_{n1} & b_{n2} & \cdots & b_{nn} \end{pmatrix}$

### Elimination

Let  
$$
A = \begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{n1} & a_{n2} & \cdots & a_{nn}
\end{pmatrix}
$$

For $s = 1, 2, \cdots, n-1$:

- **pivoting**: choose largest entry in absolute value:  
$$
  \text{piv} \overset{\text{def}}{=} \arg\max_{s \leq j \leq n} |a_{js}|,\quad E_s \leftrightarrow E_{\text{piv}}
  $$
- **eliminating** $x_s$ from $E_{s+1}$ through $E_n$:  
  $$
  a_{jk} = a_{jk} - \frac{a_{js}}{a_{ss}} a_{sk} \quad \text{(overwrite)} \quad \text{for } s+1 \leq j, k \leq n \quad \text{(1)}
  $$  $$
  b_{jk} = b_{jk} - \frac{a_{js}}{a_{ss}} b_{sk} \quad \text{(overwrite)} \quad \text{for } s+1 \leq j, k \leq n \quad \text{(2)}
  $$
- **cost** of equations (1) and (2):  
  $$
  \sum_{s=1}^{n-1} 2(n - s)^2 \approx \frac{2}{3} n^3
  $$

---

### Backward Substitution

Let  
$$
A = \begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
0 & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \cdots & a_{nn}
\end{pmatrix}
$$

- For $s = n, n-1, \cdots, 1$:  
  $$
  x_{sj} = \frac{b_{sj} - \sum_{k=s+1}^{n} a_{sk} x_{kj}}{a_{ss}},\quad j = 1, \cdots, n \quad \text{(3)}
  $$

- **cost** of equation (3):  
  $$
  \sum_{s,j=1}^{n} 2(n - s) \approx n^3
  $$

---

### Total Cost:  
$$
\text{equations (1) + (2) + (3)} \approx \frac{7}{3} n^3
$$


这个幻灯片讲的是使用 **部分主元高斯消元法（GEPP, Gaussian Elimination with Partial Pivoting）** 解线性方程组 $A \mathbf{x} = B$ 的**计算成本分析**，重点解释了每个步骤为什么会有 $\frac{7}{3} n^3$ 的计算量（以加法和乘法次数为单位）。

---

### 一、步骤分解和来源

我们先来看高斯消元法的两个主要阶段：

---

#### **阶段 1：消元（elimination）**

这个阶段是把矩阵 $A$ 化为上三角形式（也同时对 $B$ 做同样的变换）。

对每一列 $s = 1, \cdots, n - 1$：

1. **pivoting**：选择第 $s$ 列中绝对值最大的元素，花费 $(n - s + 1)$ 次比较（但通常忽略比较的代价，不计入总成本）。

2. **消元更新 $A$（式(1)）**：

$$

a_{jk} = a_{jk} - \frac{a_{js}}{a_{ss}} a_{sk}, \quad s+1 \le j, k \le n

$$

- 对每个 $s$，$j$ 从 $s+1$ 到 $n$，$k$ 从 $s+1$ 到 $n$
- 所以是 $(n - s)^2$ 次计算，乘以 2（减法 + 乘法）
总开销：

$$

\sum_{s=1}^{n-1} 2(n - s)^2 \approx \frac{2}{3}n^3

$$
> Maybe you should keep in mind that $$
\sum_{k=1}^{N} k^{2} = \frac{N(N+1)(2N+1)}{6}
$$

3. **消元更新 $B$（式(2)）**：

$$

b_{jk} = b_{jk} - \frac{a_{js}}{a_{ss}} b_{sk}, \quad s+1 \le j \le n, k \le n

$$

- 与式(1)同理，也是 $(n - s)^2$ 次计算

- 同样是 $\frac{2}{3}n^3$

---

#### **阶段 2：回代（backward substitution）**

这时 $A$ 已经是上三角矩阵，要解出每一列解 $x_j$：

- 对每个 $j = 1, \cdots, n$，我们从 $s = n, n - 1, \cdots, 1$ 回代解 $x_{sj}$：

$$

x_{sj} = \frac{b_{sj} - \sum_{k = s+1}^{n} a_{sk} x_{kj}}{a_{ss}}

$$

- 内层求和 $(n - s)$ 次

- 一共是 $n$ 个 $j$ 和 $n$ 层 $s$，所以总共大约是：

$$

\sum_{s=1}^{n} n(n - s) \approx n^3

$$
## Matrix Transpose: $A^T$

### Definition

Let  
$$
A = \begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn}
\end{pmatrix} \in \mathbb{R}^{m \times n}
\Rightarrow
A^T \overset{\text{def}}{=}
\begin{pmatrix}
a_{11} & a_{21} & \cdots & a_{m1} \\
a_{12} & a_{22} & \cdots & a_{m2} \\
\vdots & \vdots & \ddots & \vdots \\
a_{1n} & a_{2n} & \cdots & a_{mn}
\end{pmatrix} \in \mathbb{R}^{n \times m}
$$

### Example

$$
A = \begin{pmatrix}
2 & 4 & 7 & 1 \\
2 & -9 & -1 & 2
\end{pmatrix} \in \mathbb{R}^{2 \times 4},
\quad
A^T = \begin{pmatrix}
2 & 2 \\
4 & -9 \\
7 & -1 \\
1 & 2
\end{pmatrix} \in \mathbb{R}^{4 \times 2}
$$

### Theorem

$$
(A^T)^T = A, \quad (AB)^T = B^T A^T
$$

If $A^{-1}$ exists, then  
$$
(A^{-1})^T = (A^T)^{-1} \quad \square
$$
