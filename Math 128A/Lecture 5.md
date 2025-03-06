---
date created: 2025-03-05 21:23
date updated: 2025-03-05 21:32
---

# Polynomial Interpolation

## Lemma: Generalized Rolle's Theorem

Let $f(x) \in C^n[a, b]$ satisfy:

$$
f(x_i) = 0, \quad i = 1, 2, 3, \dots, n,
$$

where $a \leq x_1 < x_2 < \cdots < x_n \leq b$ are mutually distinct. Then there exists a $\xi \in [a, b]$ such that:

$$
f^{(n-1)}(\xi) = 0.
$$

## Polynomial Interpolation Error

### **Theorem**

_Suppose $x_0, \dots, x_n$ are distinct numbers in the interval $[a, b]$ and $f \in C^{n+1}[a, b]$. Then, for each $x \in [a, b]$, a number $\xi(x)$ between $x_0, \dots, x_n$ exists with:_

$$
f(x) = P(x) + \frac{f^{(n+1)}(\xi(x))}{(n+1)!} (x - x_0)(x - x_1) \cdots (x - x_n),
$$

_where $P(x)$ is the interpolating polynomial._

### Proof

- If $x = x_i$, for $i = 0, \dots, n$, then the theorem holds trivially since $f(x_i) = P(x_i)$.
- Now let $x \neq x_i$ for all $i$. Define the function $g(t)$ for $t \in [a, b]$:

$$
g(t) \stackrel{\text{def}}{=} (f(t) - P(t)) - (f(x) - P(x)) \frac{(t - x_0)(t - x_1) \cdots (t - x_n)}{(x - x_0)(x - x_1) \cdots (x - x_n)},
$$

or equivalently:

$$
g(t) = (f(t) - P(t)) - (f(x) - P(x)) \prod_{j=0}^{n} \frac{(t - x_j)}{(x - x_j)} \in C^{n+1}[a, b].
$$

The function $g(t)$ vanishes at $n+2$ distinct points:

$$
g(x) = 0, \quad g(x_k) = 0, \quad \forall k = 0, 1, \dots, n.
$$

By the Generalized Rolle's Theorem, there must be a $\xi$ between $x$ and the nodal points such that:

$$
g^{(n+1)}(\xi) = 0.
$$

Compute the $(n+1)$-th derivative:

$$
g^{(n+1)}(\xi) = \left( f(t) - P(t) \right)^{(n+1)} \big|_{t=\xi} - (f(x) - P(x)) \left( \prod_{j=0}^{n} \frac{(t - x_j)}{(x - x_j)} \right)^{(n+1)} \big|_{t=\xi},
$$

> since $P(t)$ is a polynomial of degree $\leq n$, $P^{(n+1)}(t) = 0$,

so:

$$
g^{(n+1)}(\xi) = f^{(n+1)}(\xi) - (f(x) - P(x)) \frac{(n+1)!}{\prod_{j=0}^{n} (x - x_j)} = 0.
$$

Thus:

$$
f(x) - P(x) = \frac{f^{(n+1)}(\xi(x))}{(n+1)!} \prod_{j=0}^{n} (x - x_j),
$$

or:

$$
f(x) = P(x) + \frac{f^{(n+1)}(\xi(x))}{(n+1)!} (x - x_0)(x - x_1) \cdots (x - x_n).
$$

### **Corollary**

Suppose $x_0, x_1, \dots, x_n$ are distinct numbers in the interval $[a, b]$ and $f$ is a polynomial of degree at most $n$. Then $P(x) = f(x)$.

> this happens when you know there are $n+1$ nodes already specified for interpolation.

### Uniqueness Theorem

**Theorem**: _Assume that the nodal points $x_0, \dots, x_n$ are mutually distinct. Then the interpolating <mark style="background: #FF5582A6;">polynomial</mark> $P(x)$ of degree $\leq n$ is unique._

### Example: Error Bound Calculation

Given:

$$
f(x) = P(x) + \frac{f^{(3)}(\xi(x))}{3!} (x - 2)(x - 2.75)(x - 4),
$$

where $P(x)$ is the interpolating polynomial on $[2, 4]$. Find upper bounds on:

$$
|f^{(3)}(\xi(x))| \quad \text{and} \quad |(x - 2)(x - 2.75)(x - 4)| \quad \text{for} \quad x \in [2, 4],
$$

separately, then combine them to bound the error.

**Solution**:

- Compute the third derivative:$$
  f^{(3)}(x) = -6 x^{-4}, \quad |f^{(3)}(\xi(x))| \leq 6 \cdot 2^{-4} = 6 \cdot \frac{1}{16} = \frac{3}{8},

  $$
  since $x \in [2, 4]$, the maximum of $|f^{(3)}(x)|$ occurs at $x = 2$.

- Define the polynomial:
  $$
  g(x) \stackrel{\text{def}}{=} (x - 2)(x - 2.75)(x - 4) = x^3 - \frac{35}{4} x^2 + \frac{49}{2} x - 22.
  $$

- Find the maximum of $|g(x)|$ by computing critical points:
  $$
  \frac{dg(x)}{dx} = 3 x^2 - \frac{35}{2} x + \frac{49}{2} = \frac{1}{2} (3 x - 7)(2 x - 7),
  $$

  critical points at $x = \frac{7}{3} \approx 2.333$ and $x = \frac{7}{2} = 3.5$.

- Evaluate $|g(x)|$ at critical points and endpoints:
  $$
  \left| g\left(\frac{7}{2}\right) \right| = \frac{9}{16}, \quad \left| g\left(\frac{7}{3}\right) \right| = \frac{25}{108} < \frac{9}{16},
  $$

  at endpoints $x = 2$ and $x = 4$, $g(2) = g(4) = 0$, so:
  $$
  \max_{x \in [2, 4]} |g(x)| = \frac{9}{16}.
  $$
- Combine the bounds:
  $$
  |f(x) - P(x)| \leq \frac{1}{3!} \cdot |f^{(3)}(\xi(x))| \cdot |(x - 2)(x - 2.75)(x - 4)| \leq \frac{1}{6} \cdot \frac{3}{8} \cdot \frac{9}{16} = \frac{9}{256} \approx 0.03.
  $$

#### Analysis

- **Estimate errors with polynomial interpolation**: The error term provides a way to bound the difference between the function and its interpolating polynomial.

#### Computation

- **How to compute $P(x)$ numerically**: Methods like Neville's Method or Divided Differences can be used (detailed below).

## Section 3.2: Polynomial Interpolation - Neville’s Method

### Neville’s Method (I)

- Let $Q(x)$ interpolate $f(x)$ at $x_0, x_1$.
- Let $\hat{Q}(x)$ interpolate $f(x)$ at $x_1, x_2$.

Then:

$$
P(x) := \frac{(x - x_2) Q(x) - (x - x_0) \hat{Q}(x)}{x_0 - x_2},
$$

interpolates $f(x)$ at $x_0, x_1, x_2$.

#### General Form

Build a higher-degree interpolating polynomial **from lower-degree polynomials:**

- Let $Q(x)$ interpolate $f(x)$ at $x_0, x_1, \dots, x_k$.
- Let $\hat{Q}(x)$ interpolate $f(x)$ at $x_1, \dots, x_k, x_{k+1}$.

Then:

$$
P(x) \stackrel{\text{def}}{=} \frac{(x - x_{k+1}) Q(x) - (x - x_0) \hat{Q}(x)}{x_0 - x_{k+1}} \tag{Neville's},
$$

interpolates $f(x)$ at $x_0, x_1, \dots, x_k, x_{k+1}$.

### Neville’s Method: Proof

Given:

- $Q(x)$ interpolates $f(x)$ at $x_0, x_1, \dots, x_k$,
- $\hat{Q}(x)$ interpolates $f(x)$ at $x_1, \dots, x_k, x_{k+1}$,

define:

$$
P(x) \stackrel{\text{def}}{=} \frac{(x - x_{k+1}) Q(x) - (x - x_0) \hat{Q}(x)}{x_0 - x_{k+1}}.
$$

Evaluate at the endpoints:

- For $j = 0$:
  $$
  P(x_0) = \frac{(x_0 - x_{k+1}) Q(x_0) - (x_0 - x_0) \hat{Q}(x_0)}{x_0 - x_{k+1}} = Q(x_0) = f(x_0),
  $$
- For $j = k+1$:
  $$
  P(x_{k+1}) = \frac{(x_{k+1} - x_{k+1}) Q(x_{k+1}) - (x_{k+1} - x_0) \hat{Q}(x_{k+1})}{x_0 - x_{k+1}} = \hat{Q}(x_{k+1}) = f(x_{k+1}).
  $$

For $j = 1, \dots, k$, both $Q(x_j)$ and $\hat{Q}(x_j)$ equal $f(x_j)$, so $P(x_j) = f(x_j)$. Thus, $P(x)$ interpolates $f(x)$ at $x_0, x_1, \dots, x_k, x_{k+1}$.
> The key here is to verify the new interpolation $P(x)$ passes all $j=0,1,\cdots k+1$
#### Neville’s Recursion

For $i \leq j$, define $Q_i(x_i) \stackrel{\text{def}}{=} f(x_i)$, and:

$$
Q_{i, i+1, \dots, j+1}(x) \stackrel{\text{def}}{=} \frac{(x - x_{j+1}) Q_{i, i+1, \dots, j}(x) - (x - x_i) Q_{i+1, \dots, j+1}(x)}{x_i - x_{j+1}} \tag{recursion}.
$$

> To better remember, just keep in mind that the numbers in the subscript of $Q$ represent the indices of the sample points that the interpolation passes through.
![](https://xljxkbafyo.feishu.cn/space/api/box/stream/download/asynccode/?code=OTA5NWE2YjQzNDZhMDk4YmM1YjFkNzQzNzRiYzFhNDBfZjNWOE0wN0dzOXIyVFdwcFVuQ2JuV1E4Q2twZGttMkdfVG9rZW46QXVSb2JOWUNHb0VUMzZ4dnRZbmNRaEJMblNmXzE3NDEyMzk5MTY6MTc0MTI0MzUxNl9WNA)  
```python
def neville_original(x, f, target_x):
    n = len(x)
    Q = [[0] * n for _ in range(n)]  # 创建二维数组

    # 初始化
    for i in range(n):
        Q[i][i] = f[i]

    # 填充表格
    for k in range(1, n):
        for i in range(n - k):
            Q[i][i+k] = ((target_x - x[i+k]) * Q[i][i+k-1] - (target_x - x[i]) * Q[i+1][i+k]) / (x[i] - x[i+k])

    return Q[0][n-1]  # 最终结果存储在 Q[0][n-1]
```

### Neville’s Method: Memory Re-use Version

Update rule for memory re-use:

$$
Q_i(x) \stackrel{\text{def}}{=} \frac{(x - x_{i+1}) Q_i(x) - (x - x_i) Q_{i+1}(x)}{x_i - x_{i+1}}.
$$

![](https://xljxkbafyo.feishu.cn/space/api/box/stream/download/asynccode/?code=MWQzZDNhMmQ4OWNjZjA1MzBiZTM0Y2E1OWM5YzU0NDhfY09kWXl5WXBPRzhiN2dkekp0bFVSZURKUXdMQ2owdkVfVG9rZW46R2kxTmJkUlJFb3JpcTV4bXJ0VWN6VkFwbnFiXzE3NDEyNDAwNjM6MTc0MTI0MzY2M19WNA)

```python
def neville_memory_reuse(x, f, target_x):
    n = len(x)
    Q = f.copy()  # 初始化 Q 为样本点的函数值

    for k in range(1, n):
        for i in range(n - k):
            Q[i] = ((target_x - x[i + k]) * Q[i] - (target_x - x[i]) * Q[i + 1]) / (x[i] - x[i + k])
    
    return Q[0]  # 最终结果存储在 Q[0]
```

## Section 3.3: Divided Differences

### Introduction

Given $n+1$ distinct points $(x_0, f(x_0)), (x_1, f(x_1)), \dots, (x_n, f(x_n))$, the interpolating polynomial of degree $\leq n$ is:

$$\begin{align}
P(x) &= a_0 + a_1 (x - x_0) + a_2 (x - x_0)(x - x_1) + \dots \\&+ a_n (x - x_0)(x - x_1) \cdots (x - x_{n-1}),
\end{align}
$$

with $P(x_0) = f(x_0), P(x_1) = f(x_1), \dots, P(x_n) = f(x_n)$.
> So this interpolation polynomial passes $n+1$ nodal points.

### Divided Differences Definition

Divided differences are defined as:

$$
f[x_i] = f(x_i), \quad f[x_i, x_{i+1}] = \frac{f(x_{i+1}) - f(x_i)}{x_{i+1} - x_i}.
$$

Let $x = x_1$ in:

$$
\frac{P(x) - f(x_0)}{x - x_0} = a_1 + a_2 (x - x_1) + \dots + a_n (x - x_1) \cdots (x - x_{n-1}),
$$

it follows that:

$$
a_1 = \frac{P(x_1) - f(x_0)}{x_1 - x_0} = f[x_0, x_1] = P[x_0, x_1].
$$
>If you are a bit confused, just keep in mind that $P$ is essentially just a replacement for the function name $f$,  and you will be able to understand it.

Then:

$$
\begin{align}
\frac{P(x) - P(x_0)}{x - x_0} &= f[x_0, x_1] + a_2 (x - x_1) + \dots \\&+ a_n (x - x_1) \cdots (x - x_{n-1})\\& = P[x_0, x],
\end{align}

$$

and:

$$
\frac{P[x_0, x] - P[x_0, x_1]}{x - x_1} = a_2 + \dots + a_n (x - x_2) \cdots (x - x_{n-1}),
$$
> To understand or remember this, it's quite usual to see $P[x_{0},x_{1}]$ as the coefficient directly $f[x_{0},x_{1}]$. And I believe it's quite easy to verify.

thus at $x = x_2$:

$$
a_2 = \frac{P[x_0, x_2] - P[x_0, x_1]}{x_2 - x_1} \stackrel{\text{def}}{=} f[x_1, x_0, x_2].
$$

By extension (noted as an exercise):

$$
f[x_0, x_1, x_2] \stackrel{\text{exercise}}{=} f[x_0, x_1, x_2].
$$

### Recursive Divided Differences

For all $i, j$ (common nodes in blue):

$$
f[x_i, x_{i+1}, \dots, x_j, x_{j+1}] = \frac{f[x_{i+1}, \dots, x_j, x_{j+1}] - f[x_i, x_{i+1}, \dots, x_j]}{x_{j+1} - x_i}.
$$
> To better memorize, you should see the $x_{j+1}$ in the $f[x_{i+1} \cdots x_{j+1}  ]$ and the $x_{i}$ in the latter term.

Then, for the polynomial:

$$
P(x) = a_0 + a_1 (x - x_0) + a_2 (x - x_0)(x - x_1) + \dots + a_n (x - x_0)(x - x_1) \cdots (x - x_{n-1}),
$$

we have:

$$
\begin{aligned}
a_0 &= f[x_0], \\
a_1 &= f[x_0, x_1], \\
a_2 &= f[x_0, x_1, x_2], \\
&\vdots \\
a_n &= f[x_0, x_1, \dots, x_n].
\end{aligned}
$$

### Newton Divided Difference

#### Coefficients and Divided Differences Table

Coefficients are numbers on top of all $f[\cdot]$ columns.

![](https://xljxkbafyo.feishu.cn/space/api/box/stream/download/asynccode/?code=OWZhZDg0YzA5YjIzMzQyOWI5OTdiMTJkYWZjYjIxOTFfeEdlTUgxTkhzU25id0lmOHdOaW5ubndRNThnY2tRU2xfVG9rZW46UU1MN2J4NzRVb2hCQXZ4VEZERWNnS2VnblBoXzE3NDEyNDIwNDc6MTc0MTI0NTY0N19WNA)

The interpolating polynomial $P(x)$ is given by:

$$
P(x) = a_0 + a_1 (x - x_0) + a_2 (x - x_0)(x - x_1) + a_3 (x - x_0)(x - x_1)(x - x_2) + a_4 (x - x_0)(x - x_1)(x - x_2)(x - x_3),
$$

where the coefficients $a_0, a_1, a_2, a_3, a_4$ are the divided differences $f[x_0], f[x_0, x_1], f[x_0, x_1, x_2], f[x_0, x_1, x_2, x_3], f[x_0, x_1, x_2, x_3, x_4]$, respectively.

#### Newton Divided Difference Theorem

**Theorem**: Suppose that $f \in C^n[a, b]$ and $x_0, x_1, \dots, x_n$ are distinct nodes in $[a, b]$. Then a number $\xi \in (a, b)$ exists such that:

$$
f[x_0, x_1, \dots, x_n] = \frac{f^{(n)}(\xi)}{n!}.
$$

**Proof**: Let $g(x) = f(x) - P(x)$, where:

$$
P(x) = a_0 + a_1 (x - x_0) + a_2 (x - x_0)(x - x_1) + \dots + a_n (x - x_0)(x - x_1) \cdots (x - x_{n-1}).
$$

Since $g(x_j) = f(x_j) - P(x_j) = 0$ for $j = 0, 1, \dots, n$, by the Generalized Rolle's Theorem, a number $\xi \in (a, b)$ exists such that $g^{(n)}(\xi) = 0$. Compute:

$$
g^{(n)}(\xi) = f^{(n)}(\xi) - P^{(n)}(\xi) = f^{(n)}(\xi) - a_n n! = f^{(n)}(\xi) - f[x_0, x_1, \dots, x_n] n! = 0.
$$

Thus:

$$
f[x_0, x_1, \dots, x_n] = \frac{f^{(n)}(\xi)}{n!}.
$$

![](https://xljxkbafyo.feishu.cn/space/api/box/stream/download/asynccode/?code=OGQ5YmJjZmNmOTNiNmFhNGJmZjc0ODk3ZWQ5NTJlYjNfRVVvWFRjYkpBNHU2ZlpSRWVNclRVQmJBM01wZHVyd1FfVG9rZW46R1pmVGJ4WE1Wb2lFaHF4RUEzamNyd2FTbjFlXzE3NDEyNDIzNzY6MTc0MTI0NTk3Nl9WNA)
![](https://xljxkbafyo.feishu.cn/space/api/box/stream/download/asynccode/?code=MmVhMzk0OGVjMDE5OTI5YWI4ZGU2ZjQyMTg4YzNlZmJfWHBXSUJ0Wjlaa2c1MXF5ZDdHR0tGZDhaSFNsTzdGdTVfVG9rZW46WGR2eGJUUmpFbzA5NW54YWFVYmNtNHRobkJoXzE3NDEyNDIzOTI6MTc0MTI0NTk5Ml9WNA)

### Divided Difference Algorithms

#### Algorithm 1: NDD1, $O(n)$ Memory

This algorithm implements Newton's Divided Difference method with $O(n)$ memory usage.

**Description**:

- This function implements Newton's Divided Difference Algorithm.
- $F$ is the vector of coefficients.
- Updated by Ming Gu for Math 128A, Spring 2015.

```Matlab
function F = NDD1(x, f)
    N = length(x);
    F = f;
    for k = 2:N
        for j = N:-1:k
            F(j) = (F(j) - F(j-1)) / (x(j) - x(j-k+1));
        end
    end
```

#### Algorithm 2: NewtonDividedDifference, $O(n^2)$ Memory (Book Version)

This algorithm implements Newton's Divided Difference method with $O(n^2)$ memory usage, as described in the book version.

**Description**:

- This function implements Newton's Divided Difference Algorithm.
- $F$ is the vector of coefficients.
- Written by Ming Gu for Math 128A, Fall 2008.

```matlab
function F = NewtonDividedDifference(x, f)
    n = length(x);
    P = diag(f);
    for k = 2:n
        for j = k-1:-1:1
            P(k,j) = (P(k,j+1) - P(k-1,j)) / (x(k) - x(j));
        end
    end
    F = P(:,1);
```

#### Correspondence Between Algorithm and Mathematical Notation

1. **Meaning of Matrix $P$**:

   - Matrix $P$ is a divided difference table, where $P(i, j)$ represents the divided difference $f[x_{j-1}, x_j, \dots, x_{i-1}]$.
   - Row index $i$ corresponds to the endpoint $x_{i-1}$ of the divided difference.
   - Column index $j$ corresponds to the starting point $x_{j-1}$ of the divided difference.
   - Initially, $P = \text{diag}(f)$, so $P(i, i) = f(x_{i-1})$, the zeroth-order divided difference $f[x_{i-1}]$.

2. **Divided Difference Computation Formula**:

   - The update formula in the algorithm:
     $$
     P(k, j) = \frac{P(k, j+1) - P(k-1, j)}{x(k) - x(j)},
     $$
     corresponds to the mathematical recursive formula for divided differences:
     $$
     f[x_{j-1}, x_j, \dots, x_{k-1}] = \frac{f[x_j, x_{j+1}, \dots, x_{k-1}] - f[x_{j-1}, x_j, \dots, x_{k-2}]}{x_{k-1} - x_{j-1}}.
     $$
   - Here, $P(k, j+1)$ corresponds to $f[x_j, x_{j+1}, \dots, x_{k-1}]$ (divided difference from $x_j$ to $x_{k-1}$).
   - $P(k-1, j)$ corresponds to $f[x_{j-1}, x_j, \dots, x_{k-2}]$ (divided difference from $x_{j-1}$ to $x_{k-2}$).
   - $x(k) - x(j)$ corresponds to $x_{k-1} - x_{j-1}$, the denominator of the divided difference, representing the distance between the endpoints.

3. **Extraction of Coefficients $F$**:
   - $F = P(:,1)$ extracts the first column of matrix $P$:
     - $F(1) = P(1,1) = f[x_0]$,
     - $F(2) = P(2,1) = f[x_0, x_1]$,
     - $F(3) = P(3,1) = f[x_0, x_1, x_2]$,
     - $\dots$,
     - $F(n) = P(n,1) = f[x_0, x_1, \dots, x_{n-1}]$.
   - These values are precisely the coefficients $a_0, a_1, \dots, a_{n-1}$ of the Newton interpolating polynomial.
