### Ch. 2: Secant Method Convergence Proof

Let $f(x) = x^2 - a$ for $a > 0$.

We apply the **Secant method** to solve $f(x) = 0$ with initial guesses $x_0 > x_1 > \sqrt{a}$:

$$
x_{k+1} = x_k - \frac{f(x_k) (x_k - x_{k-1})}{f(x_k) - f(x_{k-1})}, \quad \text{for} \quad k = 1, 2, \cdots
$$

---

### Step 1: Well-definedness of Iteration

Since $x_0 > x_1 > \sqrt{a} > 0$, for $k = 1$, the denominator

$$
f(x_k) - f(x_{k-1}) = x_k^2 - x_{k-1}^2 = (x_k - x_{k-1})(x_k + x_{k-1}) \neq 0
$$

so $x_2$ is defined. In general, for $k \geq 1$:

$$
x_{k+1} = x_k - \frac{(x_k^2 - a)(x_k - x_{k-1})}{(x_k - x_{k-1})(x_k + x_{k-1})} 
= x_k - \frac{x_k^2 - a}{x_k + x_{k-1}} 
= \frac{x_k x_{k-1} + a}{x_k + x_{k-1}}
$$

---

### Step 2: Monotonicity Toward $\sqrt{a}$

We show $x_{k+1} > \sqrt{a}$ by computing:

$$
x_{k+1} - \sqrt{a} 
= \frac{x_k x_{k-1} + a - \sqrt{a}(x_k + x_{k-1})}{x_k + x_{k-1}} 
= \frac{(x_k - \sqrt{a})(x_{k-1} - \sqrt{a})}{x_k + x_{k-1}} > 0
\tag{1}
$$

since $x_k, x_{k-1} > \sqrt{a}$.

---

### Step 3: Strict Decrease of the Sequence

From (1), we have:

$$
0 < x_{k+1} - \sqrt{a} < x_k - \sqrt{a}
$$

which implies that the sequence $\{x_k\}$ is strictly decreasing and bounded below by $\sqrt{a}$.

---

### Step 4: No Stagnation

To show the Secant iteration is well-defined for all $k$, we must verify $x_{k+1} \neq x_k$. Suppose not:

If $x_{k+1} = x_k$, then from the update formula:

$$
x_k = \frac{x_k x_{k-1} + a}{x_k + x_{k-1}} 
\Rightarrow x_k (x_k + x_{k-1}) = x_k x_{k-1} + a 
\Rightarrow x_k^2 = a
$$

contradicting $x_k > \sqrt{a}$. Hence $x_{k+1} \neq x_k$.

---

### Conclusion

The sequence $\{x_k\}$ is:
- Strictly decreasing,
- Bounded below by $\sqrt{a}$,
- Monotonic with a limit.

Therefore, the Secant iteration **always converges**.

### Ch. 3: Divided Difference Interpretation in Hermite Interpolation

Let the polynomial

$$
\begin{align}
P_n(x)  & \stackrel{\text{def}}{=} a_0 + a_1(x - x_0) + a_2(x - x_0)^2 + \cdots  \\
 & + a_{n+1}(x - x_0)^2(x - x_1)\cdots(x - x_{n-1}) 
\end{align}
\tag{1}
$$

interpolate a function $f(x)$ at distinct points $x_0, x_1, \cdots, x_n$ such that:

$$
P_n(x_j) = f(x_j), \quad j = 0, 1, \cdots, n \quad \text{and} \quad P_n'(x_0) = f'(x_0)
$$

Show that $a_2 = f[x_0, x_0, x_1]$.

---

### Step 1: Evaluate at $x = x_0$

From equation (1), substituting $x = x_0$ gives:

$$
a_0 = P_n(x_0) = f(x_0)
$$

---

### Step 2: Differentiate and Evaluate at $x = x_0$

Now consider the first divided difference:

$$
\frac{P_n(x) - f(x_0)}{x - x_0} = a_1 + a_2(x - x_0) + \cdots + a_{n+1}(x - x_0)(x - x_1)\cdots(x - x_{n-1})
$$

Letting $x \to x_0$ yields:

$$
\lim_{x \to x_0} \frac{P_n(x) - f(x_0)}{x - x_0} = P_n'(x_0) = f'(x_0) \Rightarrow a_1 = f'(x_0)
$$

---

### Step 3: Use Divided Difference Formula at $x = x_1$

Now plug $x = x_1$ into the expression for $P_n(x)$ and observe:

$$
f[x_0, x_1] = \frac{f(x_1) - f(x_0)}{x_1 - x_0} = f[x_0, x_0] + a_2(x_1 - x_0)
$$

Note: $f[x_0, x_0] = f'(x_0)$ by definition of repeated nodes in Hermite interpolation.

So:

$$
f[x_0, x_1] = f'(x_0) + a_2(x_1 - x_0) \Rightarrow a_2 = \frac{f[x_0, x_1] - f'(x_0)}{x_1 - x_0} = f[x_0, x_0, x_1]
$$

---

### Conclusion

Hence, we conclude:

$$
a_2 = f[x_0, x_0, x_1]
$$

This shows that the coefficient $a_2$ in the Hermite-type Newton form corresponds to the **second-order divided difference** with a repeated node.

### Ch. 4: Richardson Extrapolation to Eliminate $O(h)$ and $O(h^2)$ Terms

Let $0 < \alpha_1 < \alpha_2 < 1$, and suppose $N(h)$ is an approximation to a value $M$ for each $h > 0$ such that:

$$
M = N(h) + k_1 h + k_2 h^2 + k_3 h^3 + \cdots
$$

We want to find constants $\mu_1$ and $\mu_2$ such that the expression

$$
\frac{N(h) + \mu_1 N(\alpha_1 h) + \mu_2 N(\alpha_2 h)}{1 + \mu_1 + \mu_2}
$$

is an $O(h^3)$ approximation to $M$.

---

### Step 1: Expand Each Approximation

Use the asymptotic expansion at three different scales:

$$
\begin{aligned}
M &= N(h) + k_1 h + k_2 h^2 + k_3 h^3 + \cdots \\
M &= N(\alpha_1 h) + k_1 (\alpha_1 h) + k_2 (\alpha_1 h)^2 + k_3 (\alpha_1 h)^3 + \cdots \\
M &= N(\alpha_2 h) + k_1 (\alpha_2 h) + k_2 (\alpha_2 h)^2 + k_3 (\alpha_2 h)^3 + \cdots
\end{aligned}
$$

---

### Step 2: Combine the Approximations

Form the weighted average:

$$
\begin{align}
M  & = \frac{N(h) + \mu_1 N(\alpha_1 h) + \mu_2 N(\alpha_2 h)}{1 + \mu_1 + \mu_2}  \\
 & + \frac{1 + \mu_1 \alpha_1 + \mu_2 \alpha_2}{1 + \mu_1 + \mu_2} k_1 h \\
 &  + \frac{1 + \mu_1 \alpha_1^2 + \mu_2 \alpha_2^2}{1 + \mu_1 + \mu_2} k_2 h^2 + O(h^3)
\end{align}

$$

To eliminate $O(h)$ and $O(h^2)$ terms, set the coefficients of $h$ and $h^2$ to zero:

$$
\begin{cases}
1 + \mu_1 \alpha_1 + \mu_2 \alpha_2 = 0 \\
1 + \mu_1 \alpha_1^2 + \mu_2 \alpha_2^2 = 0
\end{cases}
$$

---

### Step 3: Solve the System

This leads to a linear system:

$$
\begin{pmatrix}
\alpha_1 & \alpha_2 \\
\alpha_1^2 & \alpha_2^2
\end{pmatrix}
\begin{pmatrix}
\mu_1 \\
\mu_2
\end{pmatrix}
= 
\begin{pmatrix}
-1 \\
-1
\end{pmatrix}
$$

Thus,

$$
\begin{pmatrix}
\mu_1 \\
\mu_2
\end{pmatrix}
= -\begin{pmatrix}
\alpha_1 & \alpha_2 \\
\alpha_1^2 & \alpha_2^2
\end{pmatrix}^{-1}
\begin{pmatrix}
1 \\
1
\end{pmatrix} = -\frac{1}{\alpha_{1}\alpha_{2}(\alpha_{2}-\alpha_{1})} \begin{pmatrix}
a_{2}^{2} & -a_{1}^{2} \\
-a_{2} & a_{1} 
\end{pmatrix}\begin{pmatrix}
1 \\
1
\end{pmatrix} = \frac{1}{\alpha_{1}\alpha_{2}(\alpha_{2}-\alpha_{1})} \begin{pmatrix}
a_{1}^{2} - a_{2}^{2} \\
a_{2} - a_{1}
\end{pmatrix} 
$$

---

### Conclusion

With $\mu_1$ and $\mu_2$ chosen as above, the combination

$$
\frac{N(h) + \mu_1 N(\alpha_1 h) + \mu_2 N(\alpha_2 h)}{1 + \mu_1 + \mu_2}
$$

provides an approximation to $M$ accurate to **order $O(h^3)$**.


### Ch. 5: Conditions for Second-Order Accuracy in a Multistep Method

Consider the initial value problem:

$$
y' = f(t, y), \quad y(t_0) = Y_0 \tag{1}
$$

and the multistep method:

$$
w_{j+1} = w_j + h \left( \alpha f(t_{j+1}, w_{j+1}) + \beta f(t_j, w_j) + \gamma f(t_{j-1}, w_{j-1}) \right) \tag{2}
$$

for $j = 0, 1, 2, \cdots$.

---

### Objective

Find conditions on the coefficients $\alpha$, $\beta$, and $\gamma$ such that (2) is **second-order accurate** for solving (1).

---

### Local Truncation Error (LTE) Expansion

By definition:
- $y'(t_j) = f(t_j, y(t_j))$
- $y''(t_j) = \frac{\partial f}{\partial t} + \frac{\partial f}{\partial y} f$

The local truncation error is:

$$
\begin{aligned}
\tau_{j+1}(h) &= \frac{y(t_{j+1}) - y(t_j)}{h} - \left( \alpha f(t_{j+1}, y(t_{j+1})) + \beta f(t_j, y(t_j)) + \gamma f(t_{j-1}, y(t_{j-1})) \right) \\
&= y'(t_j) + \frac{h}{2} y''(t_j) + O(h^2) \\
& - \left[ (\alpha + \beta + \gamma) f(t_j, y(t_j)) 
+ (\alpha h - \gamma h) \left( \frac{\partial f}{\partial t} + \frac{\partial f}{\partial y} f \right) + O(h^2) \right]
\end{aligned}
$$

---

### Canceling First- and Second-Order Terms

To make the method second-order accurate, the LTE must be $O(h^2)$.
We thus require:

$$
\alpha + \beta + \gamma = 1, \quad \alpha - \gamma = \frac{1}{2}
$$

---

### Ch. 6: Positive Definiteness of a Tridiagonal Matrix

Let $h_j > 0$ for $j = 0, 1, \cdots, n$, and define the matrix $A$ as:

$$
A \stackrel{\text{def}}{=} \begin{pmatrix}
2(h_0 + h_1) & h_1 & & \\
h_1 & 2(h_1 + h_2) & h_2 & \\
& \ddots & \ddots & \ddots \\
& & h_{n-2} & 2(h_{n-2} + h_{n-1}) & h_{n-1} \\
& & & h_{n-1} & 2(h_{n-1} + h_n)
\end{pmatrix}
$$

---

### Goal

Show that $A$ is **symmetric positive definite**.

---

### Step 1: Symmetry

By construction, $A$ is symmetric since $A_{i,j} = A_{j,i}$ for all $i, j$.

---

### Step 2: Positive Definiteness

Let $\mathbf{x} = \begin{pmatrix} x_1 \\ \vdots \\ x_n \end{pmatrix}$ be a nonzero vector. Compute the quadratic form:

$$
\mathbf{x}^T A \mathbf{x}
= 2 \sum_{j=1}^n x_j^2 (h_j + h_{j-1}) + 2 \sum_{j=2}^n x_j x_{j-1} h_{j-1}
$$

Rewriting the second sum:

$$
= 2 \sum_{j=1}^n x_j^2 (h_j + h_{j-1}) 
+ \sum_{j=2}^n \left[ (x_j + x_{j-1})^2 - x_j^2 - x_{j-1}^2 \right] h_{j-1}
$$

Simplify:

$$
= \sum_{j=1}^n x_j^2 (h_j + h_{j-1}) + x_n^2 h_n + x_1^2 h_0 + \sum_{j=2}^n (x_j + x_{j-1})^2 h_{j-1}
$$

Each term is nonnegative, and since $\mathbf{x} \neq 0$ and all $h_j > 0$, **at least one term is strictly positive**. Hence:

$$
\mathbf{x}^T A \mathbf{x} > 0 \quad \text{for all nonzero } \mathbf{x}
$$

---

### Conclusion

Matrix $A$ is **symmetric** and **positive definite**.




