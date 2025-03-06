# Numerical Analysis Document

## Section 3.3: Divided Differences

### Introduction to Divided Differences

- **Given $n+1$ distinct points**:
  $$
  (x_0, f(x_0)), (x_1, f(x_1)), \dots, (x_n, f(x_n)),
  $$

- **Interpolating polynomial of degree $\leq n$**:
  $$
  \begin{aligned}
  P(x) = & a_0 + a_1 (x - x_0) + a_2 (x - x_0)(x - x_1) + \\
  & \dots + a_n (x - x_0)(x - x_1) \dots (x - x_{n-1}),
  \end{aligned}
  $$

  with $P(x_0) = f(x_0), P(x_1) = f(x_1), \dots, P(x_n) = f(x_n)$.

It follows:
$$
\begin{aligned}
a_0 &= P(x_0) = f(x_0), \\
\frac{P(x) - f(x_0)}{x - x_0} &= a_1 + a_2 (x - x_1) + \dots + a_n (x - x_1) \dots (x - x_{n-1}).
\end{aligned}
$$

### Definition of Divided Differences

Divided Differences:
$$
f[x_i] = f(x_i), \quad f[x_i, x_{i+1}] = \frac{f(x_{i+1}) - f(x_i)}{x_{i+1} - x_i}.
$$

Let $x = x_1$ in:
$$
\frac{P(x) - f(x_0)}{x - x_0} = a_1 + a_2 (x - x_1) + \dots + a_n (x - x_1) \dots (x - x_{n-1}).
$$

It follows that:
$$
a_1 = \frac{P(x_1) - f(x_0)}{x_1 - x_0} = f[x_0, x_1] = P[x_0, x_1].
$$

Further derivations:
$$
\begin{aligned}
\frac{P(x) - P(x_0)}{x - x_0} &= f[x_0, x_1] + a_2 (x - x_1) + \dots + a_n (x - x_2) \dots (x - x_{n-1}), \\
\frac{P[x_0, x] - P[x_0, x_1]}{x - x_1} &= a_2 + \dots + a_n (x - x_2) \dots (x - x_{n-1}),
\end{aligned}
$$

leading to:
$$
a_2 = \frac{P[x_0, x_1, x_2] - P[x_0, x_1]}{x_2 - x_1} = f[x_0, x_1, x_2].
$$


### Recursive Divided Differences

For all $i, j$ (common nodes in blue):
$$
f[x_i, x_{i+1}, \dots, x_j, x_{j+1}] = \frac{f[x_{i+1}, \dots, x_j, x_{j+1}] - f[x_i, x_{i+1}, \dots, x_j]}{x_{j+1} - x_i},
$$

Then in the polynomial:
$$
\begin{aligned}
P(x) &= a_0 + a_1 (x - x_0) + a_2 (x - x_0)(x - x_1) + \\
&\quad \dots + a_n (x - x_0)(x - x_1) \dots (x - x_{n-1}),
\end{aligned}
$$

we have, by mathematical induction:
$$
\begin{aligned}
a_0 &= f[x_0], \\
a_1 &= f[x_0, x_1], \\
a_2 &= f[x_0, x_1, x_2], \\
&\quad \vdots \\
a_n &= f[x_0, x_1, \dots, x_n].
\end{aligned}
$$

### Newton Divided Difference Example

#### Data Table

| $x$   | $f(x)$     |
|-------|------------|
| $x_0$ | 1.0 0.7651977 |
| $x_1$ | 1.3 0.6200860 |
| $x_2$ | 1.6 0.4554022 |
| $x_3$ | 1.9 0.2818186 |
| $x_4$ | 2.2 0.1103623 |

#### Calculations

- First-order divided differences:
  $$
  \begin{aligned}
  f[x_0, x_1] &= \frac{f[x_1] - f[x_0]}{x_1 - x_0} \\
              &= \frac{0.6200860 - 0.7651977}{1.3 - 1.0} \\
              &= -0.4837057,
  \end{aligned}
  $$

  $$
  f[x_1, x_2] = -0.5489460.
  $$

- Second-order divided difference (corrected from PAGE9):
  $$
  \begin{aligned}
  f[x_0, x_1, x_2] &= \frac{f[x_1, x_2] - f[x_0, x_1]}{x_2 - x_0} \\
                   &= \frac{-0.5489460 - (-0.4837057)}{1.6 - 1.0} \\
                   &= -0.1087339.
  \end{aligned}
  $$

#### Divided Difference Table

Coefficients are numbers on top of all $f[\dots]$ columns:

| $x$   | $f[x]$     | $f[x_{i-1}, x_i]$ | $f[x_{i-2}, x_{i-1}, x_i]$ | $f[x_{i-3}, \dots, x_i]$ | $f[x_{i-4}, \dots, x_i]$ |
|-------|------------|-------------------|-----------------------------|--------------------------|--------------------------|
| $x_0$ | 1.0 0.7651977 |                   |                             |                          |                          |
|       |            | -0.4837057        |                             |                          |                          |
| $x_1$ | 1.3 0.6200860 |                   | -0.1087339                  |                          |                          |
|       |            | -0.5489460        |                             | 0.0558784                |                          |
| $x_2$ | 1.6 0.4554022 |                   | -0.0494433                  |                          | 0.0680685                |
|       |            | -0.5786120        |                             |                          |                          |
| $x_3$ | 1.9 0.2818186 |                   | 0.0118183                   |                          |                          |
|       |            | -0.5715210        |                             |                          |                          |
| $x_4$ | 2.2 0.1103623 |                   |                             |                          |                          |

The polynomial (corrected from PAGE10):
$$
\begin{aligned}
P(x) &= a_0 + a_1 (x - x_0) + a_2 (x - x_0)(x - x_1) + a_3 (x - x_0)(x - x_1)(x - x_2) \\
&\quad + a_4 (x - x_0)(x - x_1)(x - x_2)(x - x_3),
\end{aligned}
$$

where $a_0 = 0.7651977$, $a_1 = -0.4837057$, $a_2 = -0.1087339$, $a_3 = 0.0558784$, $a_4 = 0.0680685$.

### Data Relations and Computation Flow

#### Data Relations

$$
f[x_0] \rightarrow f[x_{n-1}, x_n] \rightarrow f[x_{n-2}, x_{n-1}, x_n] \rightarrow \dots \rightarrow f[x_0, \dots, x_n],
$$

#### Computation Flow

$$
\begin{aligned}
f[x_0] &\uparrow \quad f[x_0, x_1], \\
f[x_1, x_2] &\uparrow \quad f[x_0, x_1, x_2],
\end{aligned}
$$

General flow:
$$
\begin{aligned}
f[x_{n-2}] &\uparrow f[x_{n-3}, x_{n-2}] \uparrow f[x_{n-4}, x_{n-3}, x_{n-2}] \uparrow \dots, \\
f[x_{n-1}] &\uparrow f[x_{n-2}, x_{n-1}] \uparrow f[x_{n-3}, x_{n-2}, x_{n-1}] \uparrow \dots, \\
f[x_n] &\uparrow f[x_{n-1}, x_n] \uparrow f[x_{n-2}, x_{n-1}, x_n] \uparrow \dots f[x_0, \dots, x_n].
\end{aligned}
$$

(Note: PAGE13 contains a typo in the first line, corrected here as $f[x_{n-2}]$.)

#### Storage with Memory Reuse

Output is $F_0, F_1, \dots, F_n$:
$$
\begin{aligned}
f[x_0] &= F_0, \\
f[x_1] &\leftarrow f[x_0, x_1] = F_1, \\
f[x_2] &\leftarrow f[x_0, x_1, x_2] = F_2.
\end{aligned}
$$

### Variation: Forward Differences

Let $x_1 = x_0 + h$, $x_2 = x_0 + 2h$:

$$
\begin{aligned}
f[x_0, x_1] &= f[x_0, x_0 + h] = \frac{f(x_0 + h) - f(x_0)}{h} \quad \text{(first order FD, at } x_0\text{)}, \\
f[x_0, x_1, x_2] &= f[x_0, x_0 + h, x_0 + 2h] = \frac{f[x_1, x_2] - f[x_0, x_1]}{2h} \\
&= \frac{f(x_2) + f(x_0) - 2 f(x_1)}{2 h^2} \quad \text{(second order FD, at } x_0\text{)}.
\end{aligned}
$$

#### Example

```matlab
>> x0 = 0; h = 0.1; x1 = x0 + h; x2 = x1 + h;
>> df1 = (exp(x1) - exp(x0)) / h;
>> df2 = (exp(x2) + exp(x0) - 2 * exp(x1)) / (2 * h^2);
>> disp([df1, exp(x0), df1 - exp(x0)])
     1.0517    1.0000    0.0517
>> disp([df2, exp(x0) / 2.0, df2 - exp(x0) / 2.0])
     0.5530    0.5000    0.0530
```

(Note: PAGE15 corrects the syntax for the MATLAB code, e.g., `h^2` instead of `h\wedge 2`.)

### Variation: Central Differences

Let $x_1 = x_0 + h$, $x_2 = x_1 + h$, $\bar{x}_0 = x_0 + h/2$:

$$
\begin{aligned}
f[x_0, x_1] &= f[x_0, x_0 + h] = \frac{f(x_0 + h) - f(x_0)}{h} \quad \text{(first order CD, at } \bar{x}_0\text{)}, \\
f[x_0, x_1, x_2] &= f[x_0, x_0 + h, x_0 + 2h] = \frac{f[x_1, x_2] - f[x_0, x_1]}{2h} \\
&= \frac{f(x_2) + f(x_0) - 2 f(x_1)}{2 h^2} \quad \text{(second order CD, at } x_1\text{)}.
\end{aligned}
$$

(Note: PAGE17 contains a repeated and incorrect line `x_1 = (x_1, x_2) + f(x_0) = 2 f(x_1)` which is ignored as it appears to be a formatting error.)

### Variation: Backward Differences

Let $x_{n-1} = x_n - h$, $x_{n-2} = x_n - 2h$:

$$
\begin{aligned}
f[x_{n-1}, x_n] &= f[x_n - h, x_n] = \frac{f(x_n) - f(x_n - h)}{h} \quad \text{(1st order, at } x_n\text{)}, \\
f[x_{n-2}, x_{n-1}, x_n] &= f[x_n - 2h, x_n - h, x_n] \\
&= \frac{f[x_n - h, x_n] - f[x_n - 2h, x_n - h]}{2h} \\
&= \frac{f(x_n) + f(x_{n-2}) - 2 f(x_{n-1})}{2 h^2} \quad \text{(2nd order BD, at } x_n\text{)}.
\end{aligned}
$$

#### Example

```matlab
>> x2 = 0.2; h = 0.1; x1 = x2 - h; x0 = x1 - h;
>> df1 = (exp(x2) - exp(x1)) / h;
>> df2 = (exp(x2) + exp(x0) - 2 * exp(x1)) / (2 * h^2);
>> disp([df1, exp(x2), df1 - exp(x2)])
     1.1623    1.2214    -0.0591
>> disp([df2, exp(x2) / 2.0, df2 - exp(x2) / 2.0])
     0.5530    0.6107    -0.0577
```

(Note: PAGE19 contains repeated output lines `0.6107 -0.0577` which are summarized in the `disp` output above.)

## Section 3.4: Double Nodes in Interpolation

### Double Nodes: Linear Interpolation

- **Given 2 distinct points**:
  $$
  (x_0, f(x_0)), (x_1, f(x_1)),
  $$

- **Interpolating polynomial of degree $\leq 1$**:
  $$
  P(x) = a_0 + a_1 (x - x_0),
  $$

  with $P(x_0) = f(x_0)$, $P(x_1) = f(x_1)$,

where:
$$
a_0 = f(x_0), \quad a_1 = \frac{f(x_1) - f(x_0)}{x_1 - x_0}.
$$

Now let $x_1 \to x_0$, we obtain:
$$
a_1 \stackrel{\text{def}}{=} f[x_0, x_0] = f'(x_0),
$$

$$
P(x) = a_0 + a_1 (x - x_0).
$$

The interpolating polynomial now satisfies:
$$
P(x_0) = f(x_0), \quad P'(x_0) = f'(x_0).
$$

### Double Nodes: Quadratic Interpolation

- **Given 3 distinct points**:
  $$
  (x_0, f(x_0)), (x_1, f(x_1)), (x_2, f(x_2)),
  $$

- **Interpolating polynomial of degree $\leq 2$**:
  $$
  P(x) = a_0 + a_1 (x - x_0) + a_2 (x - x_0)(x - x_1),
  $$

where we have:
$$
a_0 = f(x_0), \quad a_1 = f[x_0, x_1], \quad a_2 = f[x_0, x_1, x_2] = \frac{f[x_1, x_2] - f[x_0, x_1]}{x_2 - x_0}.
$$

Now let $x_2 \to x_1$, we obtain single node $x_0$, double node $x_1$:
$$
\begin{aligned}
f[x_1, x_1] &= f'(x_1), \\
a_2 &= f[x_0, x_1, x_1] \stackrel{\text{def}}{=} \frac{f[x_1, x_1] - f[x_0, x_1]}{x_1 - x_0} = \frac{f'(x_1) - f[x_0, x_1]}{x_1 - x_0}.
\end{aligned}
$$

The interpolating polynomial now satisfies:
$$
P(x_0) = f(x_0), \quad P(x_1) = f(x_1), \quad P'(x_1) = f'(x_1).
$$

### Double Nodes Twice: Cubic Interpolation (I)

- **Given 4 distinct points**:
  $$
  (x_0, f(x_0)), (x_1, f(x_1)), (x_2, f(x_2)), (x_3, f(x_3)),
  $$

- **Interpolating polynomial of degree $\leq 3$**:
  $$
  P(x) = a_0 + a_1 (x - x_0) + a_2 (x - x_0)(x - x_1) + a_3 (x - x_0)(x - x_1)(x - x_2),
  $$

where:
$$
a_0 = f[x_0],
$$

$$
a_1 = f[x_0, x_1],
$$

$$
a_2 = f[x_0, x_1, x_2] = \frac{f[x_1, x_2] - f[x_0, x_1]}{x_2 - x_0},
$$

$$
a_3 = f[x_0, x_1, x_2, x_3] = \frac{f[x_1, x_2, x_3] - f[x_0, x_1, x_2]}{x_3 - x_0}.
$$

### Double Nodes Twice: Cubic Interpolation (II)

Let $x_1 \to x_0$, and $x_3 \to x_2$. It follows that:
$$
\begin{aligned}
a_0 &= f[x_0], \\
a_1 &= f[x_0, x_0] = f'(x_0), \\
a_2 &= f[x_0, x_0, x_2] = \frac{f[x_0, x_2] - f[x_0, x_0]}{x_2 - x_0} = \frac{f[x_0, x_2] - f'(x_0)}{x_2 - x_0}, \\
f[x_0, x_2, x_2] &= \frac{f[x_2, x_2] - f[x_2, x_0]}{x_2 - x_0} = \frac{f'(x_2) - f[x_0, x_2]}{x_2 - x_0}, \\
a_3 &= f[x_0, x_0, x_2, x_2] = \frac{f[x_0, x_2, x_2] - f[x_0, x_0, x_2]}{x_2 - x_0}.
\end{aligned}
$$

This is a Hermite interpolation:
$$
P(x) = a_0 + a_1 (x - x_0) + a_2 (x - x_0)^2 + a_3 (x - x_0)^2 (x - x_2),
$$

satisfying (corrected from PAGE25 where $P'(x_2)$ is repeated):
$$
P(x_0) = f(x_0), \quad P'(x_0) = f'(x_0), \quad P(x_2) = f(x_2), \quad P'(x_2) = f'(x_2).
$$

### General Hermite Interpolation

- **Given $n+1$ distinct points**:
  $$
  (x_0, f(x_0), f'(x_0)), (x_1, f(x_1), f'(x_1)), \dots, (x_n, f(x_n), f'(x_n)),
  $$

- **Interpolating polynomial $H(x)$ of degree $\leq 2n + 1$ with**:
  $$
  \begin{aligned}
  H(x_0) &= f(x_0), & H'(x_0) &= f'(x_0), \\
  H(x_1) &= f(x_1), & H'(x_1) &= f'(x_1), \\
  &\vdots \\
  H(x_n) &= f(x_n), & H'(x_n) &= f'(x_n).
  \end{aligned}
  $$

- $2n + 2$ conditions, $2n + 2$ coefficients in $H(x)$.

### Divided Differences: Double Node Version

- **Given $m+1$ distinct points ($m = 2n + 1$)**:
  $$
  (z_0, f(z_0)), (z_1, f(z_1)), \dots, (z_m, f(z_m)),
  $$

- **Interpolating polynomial of degree $\leq m = 2n + 1$**:
  $$
  \begin{aligned}
  P(x) &= a_0 + a_1 (x - z_0) + a_2 (x - z_0)(x - z_1) + \\
  &\quad \dots + a_m (x - z_0)(x - z_1) \dots (x - z_{m-1}),
  \end{aligned}
  $$

satisfying:
$$
P(z_0) = f(z_0), \quad P(z_1) = f(z_1), \dots, P(z_m) = f(z_m).
$$

- **Coefficients satisfy**:
  $$
  a_j = f[z_0, z_1, \dots, z_j], \quad \text{for } j = 0, 1, \dots, m = 2n + 1.
  $$

- **Make each node a double node**:
  $$
  z_j \to x_{\lfloor j/2 \rfloor}, \quad \text{for } j = 0, 1, \dots, 2n + 1.
  $$

### Review: Newton Divided Difference Table

| $i$ | $f[z_i]$ | $f[z_{i-1}, z_i]$ | $f[z_{i-2}, z_{i-1}, z_i]$ | $\dots$ | $f[z_0, z_1, \dots, z_i]$ |
|-----|----------|-------------------|-----------------------------|---------|---------------------------|
| 0   | $f[z_0] \stackrel{\text{def}}{=} a_0$ |                   |                             |         |                           |
| 1   | $f[z_1]$ | $f[z_0, z_1] \stackrel{\text{def}}{=} a_1$ |                             |         |                           |
| 2   | $f[z_2]$ | $f[z_1, z_2]$     | $f[z_0, z_1, z_2] \stackrel{\text{def}}{=} a_2$ |         |                           |
| 3   | $f[z_3]$ | $f[z_2, z_3]$     |                             |         |                           |
| 4   | $f[z_4]$ | $f[z_3, z_4]$     |                             |         |                           |
| 5   | $f[z_5]$ | $f[z_4, z_5]$     |                             |         |                           |

(Note: PAGE29 seems incomplete and contains repeated entries; only the meaningful part is included.)

### Double Nodes with $m = 2n + 1$

For $x_j = z_{\lfloor j/2 \rfloor}$, $f[x_j, x_j] = f'(x_j)$:
$$
\begin{aligned}
f[x_0] &\stackrel{\text{def}}{=} a_0, \\
f[x_0, x_0] &\stackrel{\text{def}}{=} f'(x_0) \stackrel{\text{def}}{=} a_1, \\
f[x_0, x_0, x_1] &\stackrel{\text{def}}{=} a_2, \\
f[x_1, x_1] &\stackrel{\text{def}}{=} f'(x_1).
\end{aligned}
$$


### Hermite Interpolation Examples

- **Hermite Interpolation on $e^x$ on $[-1, 1]$** (PAGE31, PAGE32)
- **Hermite Interpolation on $\frac{1}{0.2 + x^2}$ on $[-1, 1]$** (PAGE33, PAGE34)

(Note: These pages mention "Coefficient's $a_j$ for Hermite Interpolation" but do not provide specific calculations.)

### Hermite Interpolation, Alternative Form

- **Given $n+1$ distinct points**:
  $$
  (x_0, f(x_0), f'(x_0)), (x_1, f(x_1), f'(x_1)), \dots, (x_n, f(x_n), f'(x_n)),
  $$

- **Interpolating polynomial $H(x)$ of degree $\leq 2n + 1$ with**:
  $$
  \begin{aligned}
  H(x_0) &= f(x_0), & H'(x_0) &= f'(x_0), \\
  H(x_1) &= f(x_1), & H'(x_1) &= f'(x_1), \\
  &\vdots \\
  H(x_n) &= f(x_n), & H'(x_n) &= f'(x_n).
  \end{aligned}
  $$

- **Alternative $H(x)$ form**:
  $$
  H(x) = \sum_{j=0}^n f(x_j) H_j(x) + \sum_{j=0}^n f'(x_j) \hat{H}_j(x),
  $$

where:
$$
H_j(x) = (1 - 2 (x - x_j) L_j'(x_j)) L_j^2(x), \quad \hat{H}_j(x) = (x - x_j) L_j^2(x),
$$

with:
$$
L_j(x) = \prod_{i \neq j} \frac{x - x_i}{x_j - x_i}.
$$

### Hermite Interpolation Error

**Theorem**: *Suppose $x_0, x_1, \dots, x_n$ are distinct numbers in the interval $[a, b]$ and $f \in C^{2n+2}[a, b]$. Then, for each $x \in [a, b]$, a number $\xi(x)$ between $x_0, x_1, \dots, x_n$ (hence $\in (a, b]$) exists with:*
$$
f(x) = H(x) + \frac{f^{(2n+2)}(\xi(x))}{(2n+2)!} (x - x_0)^2 (x - x_1)^2 \dots (x - x_n)^2,
$$

*where $H(x)$ is the interpolating polynomial.*

#### ***Proof***

If $x = x_0, x_1, \dots, x_n$, then error $= 0$ and the theorem holds. Now let $x$ be not equal to any node. Define function $g$ for $t \in [a, b]$:
$$
\begin{aligned}
g(t) \stackrel{\text{def}}{=} (f(t) - H(t)) - (f(x) - H(x)) \frac{(t - x_0)^2 (t - x_1)^2 \dots (t - x_n)^2}{(x - x_0)^2 (x - x_1)^2 \dots (x - x_n)^2} \\
= (f(t) - H(t)) - (f(x) - H(x)) \prod_{j=0}^n \frac{(t - x_j)^2}{(x - x_j)^2} \in C^{2n+2}[a, b].
\end{aligned}
$$

Then $g(t)$ vanishes at $n+2$ distinct points:
$$
g(x) = 0, \quad g(x_k) = 0, \quad \text{for } k = 0, 1, \dots, n,
$$

and $g'(t)$ vanishes at $n+1$ distinct points:
$$
g'(x_k) = 0, \quad \text{for } k = 0, 1, \dots, n.
$$

There must be a $\xi$ between $x$ and the nodal points such that:
$$
g^{(2n+2)}(\xi) = 0.
$$

Since:
$$
\begin{aligned}
g^{(2n+2)}(\xi) &= (f(t) - H(t))^{(2n+2)} \big|_{t=\xi} - (f(x) - H(x)) \left( \prod_{j=0}^n \frac{(t - x_j)^2}{(x - x_j)^2} \right)^{(2n+2)} \big|_{t=\xi} \\
&= f^{(2n+2)}(\xi) - (f(x) - H(x)) \frac{(2n+2)!}{\prod_{j=0}^n (x - x_j)^2} \\
&= 0,
\end{aligned}
$$

therefore:
$$
f(x) = H(x) + \frac{f^{(2n+2)}(\xi(x))}{(2n+2)!} (x - x_0)^2 (x - x_1)^2 \dots (x - x_n)^2.
$$

### Hermite Interpolation Limitations

**Hermite interpolation not good enough** (PAGE39):

- For small n: some approximation, but error not small enough  
- For large n: may not be any approximation  

## Section 3.5: A Car Wrapped in Splines

### Introduction to Splines

- **Given $n+1$ distinct points**:
  $$
  (x_0, f(x_0)), (x_1, f(x_1)), \dots, (x_n, f(x_n)),
  $$

- **Find cubic spline interpolant $S(x)$**:
  $$
  \text{for } x \in [x_j, x_{j+1}], \quad j = 0, 1, \dots, n-1,
  $$

  $$
  S(x) = S_j(x) \stackrel{\text{def}}{=} a_j + b_j (x - x_j) + c_j (x - x_j)^2 + d_j (x - x_j)^3,
  $$

  ($S(x)$ is piece-wise cubic: $4n$ unknowns).

- **Conditions**:
  $$
  S(x_j) = f(x_j), \quad j = 0, 1, \dots, n \quad (S(x) = f(x) \text{ at all nodes: } n+1 \text{ conditions}),
  $$

  $$
  S(x) \in C^2[x_0, x_n] \quad (\text{smooth enough: } 3(n-1) \text{ conditions}).
  $$

- $4n$ unknowns vs. $4n - 2$ conditions so far.

### The Splines Equations (I)

For $x \in [x_j, x_{j+1}]$, $j = 0, 1, \dots, n-1$:
$$
S(x) = S_j(x) \stackrel{\text{def}}{=} a_j + b_j (x - x_j) + c_j (x - x_j)^2 + d_j (x - x_j)^3,
$$

(Note: PAGE50 contains a typo where $\frac{1}{2} a_j$ should be $a_j$, corrected above.)

Introducing for $x \geq x_n$ (three artificial unknowns):
$$
S_n(x) = a_n + b_n (x - x_n) + c_n (x - x_n)^2,
$$

For $j = 0, 1, \dots, n$:
$$
a_j = S_j(x_j) = f(x_j),
$$

For $j = 0, 1, \dots, n-1$, let $h_j = x_{j+1} - x_j$:
$$
\begin{aligned}
a_{j+1} &= S_{j+1}(x_{j+1}) = S_j(x_{j+1}) = a_j + b_j h_j + c_j h_j^2 + d_j h_j^3, \\
b_j + c_j h_j + d_j h_j^2 &= \frac{a_{j+1} - a_j}{h_j} \quad (\ell_0),
\end{aligned}
$$

$$
S(x) \in C^0[x_0, x_n] \quad (3n + 2 \text{ unknowns, } n \text{ equations}),
$$

and $S(x_j) = f(x_j)$, for $j = 0, 1, \dots, n$.

### The Splines Equations (II)

For $j = 0, 1, \dots, n$:
$$
\begin{aligned}
S_j(x) &= a_j + b_j (x - x_j) + c_j (x - x_j)^2 + d_j (x - x_j)^3, \\
\Rightarrow S_j'(x) &= b_j + 2 c_j (x - x_j) + 3 d_j (x - x_j)^2,
\end{aligned}
$$

For $j = 0, \dots, n-1$:
$$
b_{j+1} = S_{j+1}'(x_{j+1}) = S_j'(x_{j+1}) = b_j + 2 c_j h_j + 3 d_j h_j^2 \quad (\ell_1),
$$

Ensures $S(x) \in C^1[x_0, x_n]$ (with $3n + 2$ unknowns, $2n$ equations).

### The Splines Equations (III)

For $j = 0, 1, \dots, n$:
$$
S_j''(x) = 2 c_j + 6 d_j (x - x_j),
$$

For $j = 0, \dots, n-1$:
$$
2 c_{j+1} = S_{j+1}''(x_{j+1}) = S_j''(x_{j+1}) = 2 c_j + 6 d_j h_j \quad (\ell_2),
$$

- Ensures $S(x) \in C^2[x_0, x_n]$ (with $3n + 2$ unknowns, $3n$ equations).

Summary of equations:
$$
\begin{aligned}
b_j + c_j h_j + d_j h_j^2 &= \frac{a_{j+1} - a_j}{h_j} \quad (\ell_0), \\
b_{j+1} &= b_j + 2 c_j h_j + 3 d_j h_j^2 \quad (\ell_1), \\
2 c_{j+1} &= 2 c_j + 6 d_j h_j \quad (\ell_2).
\end{aligned}
$$

Next: solve for $d_j$ in $(\ell_2)$ and $b_j$ in $(\ell_0)$, $j = 0, 1, \dots, n-1$.

### The Splines Equations (IV): Solving for $d_j$ and $b_j$

Equations:
$$
\begin{aligned}
b_j + c_j h_j + d_j h_j^2 &= \frac{a_{j+1} - a_j}{h_j}, \quad j = 0, \dots, n-1 \quad (\ell_0), \\
b_{j+1} &= b_j + 2 c_j h_j + 3 d_j h_j^2 \quad (\ell_1), \\
2 c_{j+1} &= 2 c_j + 6 d_j h_j \quad (\ell_2).
\end{aligned}
$$

Solve for $d_j$ from $(\ell_2)$:
$$
d_j = \frac{c_{j+1} - c_j}{3 h_j} \quad (\hat{\ell}_2),
$$

Solve for $b_j$ from $(\ell_0)$:
$$
b_j = -\frac{h_j}{3} (2 c_j + c_{j+1}) + \frac{a_{j+1} - a_j}{h_j} \quad (\hat{\ell}_0),
$$

Substitute $d_j$ into $(\ell_1)$:
$$
b_{j+1} = b_j + h_j (c_j + c_{j+1}) \quad (\hat{\ell}_1),
$$

Combine $(\hat{\ell}_1)$ and $(\hat{\ell}_0)$:
$$
-\frac{h_{j+1}}{3} (2 c_{j+1} + c_{j+2}) + \frac{a_{j+2} - a_{j+1}}{h_{j+1}} = -\frac{h_j}{3} (2 c_j + c_{j+1}) + \frac{a_{j+1} - a_j}{h_j} + h_j (c_j + c_{j+1}).
$$

### The Splines Equations (V)

Final equations, for $j = 1, \dots, n-1$:
$$
h_{j-1} c_{j-1} + 2 (h_{j-1} + h_j) c_j + h_j c_{j+1} = 3 \left( \frac{a_{j+1} - a_j}{h_j} - \frac{a_j - a_{j-1}}{h_{j-1}} \right),
$$

$n-1$ equations with $n+1$ unknowns (under-defined problem, needs two additional conditions).

#### Special Case: Natural Splines

Natural Splines: $S_0''(x_0) = S_{n-1}''(x_n) = 0$:
$$
c_0 = S_0''(x_0)/2 = 0, \quad c_n = S_{n-1}''(x_n)/2 = 0,
$$

- $n-1$ equations with $n-1$ unknowns:
  $$
  \begin{aligned}
  2 (h_0 + h_1) c_1 + h_1 c_2 &= 3 \left( \frac{a_2 - a_1}{h_1} - \frac{a_1 - a_0}{h_0} \right), \\
  h_{j-1} c_{j-1} + 2 (h_{j-1} + h_j) c_j + h_j c_{j+1} &= 3 \left( \frac{a_{j+1} - a_j}{h_j} - \frac{a_j - a_{j-1}}{h_{j-1}} \right), \quad 2 \leq j \leq n-3, \\
  h_{n-2} c_{n-2} + 2 (h_{n-2} + h_{n-1}) c_{n-1} &= 3 \left( \frac{a_n - a_{n-1}}{h_{n-1}} - \frac{a_{n-1} - a_{n-2}}{h_{n-2}} \right).
  \end{aligned}
  $$

#### Natural Splines: Equations in Matrix Form

- Equations for $\{c_j\}_{j=1}^{n-1}$.
- Equations for $\{d_j\}_{j=0}^{n-1}$, $\{b_j\}_{j=0}^{n-1}$ (not detailed in matrix form in the document).

#### Clamped Splines: $S_0'(x_0) = f'(x_0)$, $S_{n-1}'(x_n) = f'(x_n)$

Recall:
$$
\begin{aligned}
b_j &= -\frac{h_j}{3} (2 c_j + c_{j+1}) + \frac{a_{j+1} - a_j}{h_j} \quad (\hat{\ell}_0), \\
b_{j+1} &= b_j + h_j (c_j + c_{j+1}) \quad (\hat{\ell}_1),
\end{aligned}
$$

Equation for $c_0, c_1$:
$$
\begin{aligned}
f'(x_0) &= S_0'(x_0) = b_0 = -\frac{h_0}{3} (2 c_0 + c_1) + \frac{a_1 - a_0}{h_0}, \\
2 h_0 c_0 + h_0 c_1 &= 3 \left( \frac{a_1 - a_0}{h_0} - f'(x_0) \right),
\end{aligned}
$$

Equation for $c_{n-1}, c_n$ (corrected from PAGE66):
$$
\begin{aligned}
f'(x_n) &= S_{n-1}'(x_n) = b_{n-1} + h_{n-1} (c_{n-1} + c_n), \\
b_{n-1} &= -\frac{h_{n-1}}{3} (2 c_{n-1} + c_n) + \frac{a_n - a_{n-1}}{h_{n-1}}, \\
h_{n-1} c_{n-1} + 2 h_{n-1} c_n &= 3 \left( f'(x_n) - \frac{a_n - a_{n-1}}{h_{n-1}} \right),
\end{aligned}
$$

#### Clamped Splines: Equations in Matrix Form

- Equations for $\{c_j\}_{j=0}^n$ (matrix form not fully specified in the document).
- Equations for $\{d_j\}_{j=0}^{n-1}$, $\{b_j\}_{j=0}^{n-1}$:
  $$
  d_j = \frac{c_{j+1} - c_j}{3 h_j}, \quad b_j = -\frac{h_j}{3} (2 c_j + c_{j+1}) + \frac{a_{j+1} - a_j}{h_j}.
  $$

#### Clamped Splines MATLAB Code

```matlab
function Splines = clampedSplines(x, f, df)
    % This code implements the clamped splines
    % Written by Ming Gu for Math 128A, Fall 2008
    % Updated by Ming Gu for Math 128A, Spring 2015

    n = length(x);
    h = diff(x);
    rhs = 3 * [df(1); diff(f) ./ h; df(2)];
    A = diag(h, 1) + diag(h, -1) + 2 * diag([h(1:end-1) + h(2:end), 0]);

    % Compute the coefficients. This is a simple but very slow way to do it.
    c = A \ rhs;
```

#### Natural Splines Example: $f(x) = e^x$

Points: $x_0 = 0$, $x_1 = 1$, $x_2 = 2$, $x_3 = 3$.

#### Clamped Splines Example: $f(x) = e^x$

Points: $x_0 = 0$, $x_1 = 1$, $x_2 = 2$, $x_3 = 3$, with $f'(0) = 1$, $f'(3) = e^3$.

### Review: Splines

- **Given $n+1$ distinct points**:
  $$
  (x_0, f(x_0)), (x_1, f(x_1)), \dots, (x_n, f(x_n)),
  $$

- **Find cubic spline interpolant $S(x) \in C^2[x_0, x_n]$**:
  $$
  S(x) = S_j(x) \stackrel{\text{def}}{=} a_j + b_j (x - x_j) + c_j (x - x_j)^2 + d_j (x - x_j)^3,
  $$

  for $x \in [x_j, x_{j+1}]$, $0 \leq j \leq n-1$.

  $$
  S(x_j) = f(x_j), \quad 0 \leq j \leq n.
  $$

### A Duck in Splines

#### A Duck in Flight

Goal: To approximate the top profile of a duck in flight.

#### Duck Top Profile in Natural Splines

**Data Table for $a$ coefficients**:

| $x$   | 0.9 | 1.3 | 1.9 | 2.1 | 2.6 | 3.0 | 3.9 | 4.4 | 4.7 | 5.0 | 6.0 | 17.0 | 1.0 | 9.2 | 10.5 | 11.3 | 11.6 | 12.0 | 12.6 | 13.9 | 13.3 |
|-------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|------|-----|-----|------|------|------|------|------|------|------|
| $f(x)$| 1.3 | 1.5 | 1.8 | 2.1 | 2.6 | 2.7 | 2.4 | 2.1 | 2.8 | 2.1 | 2.5 | 2.3  | 2.3 | 2.3 | 1.4  | 0.9  | 0.7  | 0.6  | 0.5  | 0.4  | 0.2  |

(Note: PAGE75 and PAGE76 contain inconsistencies in the $x$ values (e.g., repeated 13.3); the table is presented as-is.)

#### Duck Top Profile in 20-Degree Polynomial Interpolation

(Note: No specific polynomial is provided in the document.)

## Section 3.6: Parametric Curve Approximation

### Parametric Curve: $x = x(t)$, $y = y(t)$

- **Given $n+1$ distinct points**:
  $$
  \begin{aligned}
  (x_0, y_0), (x_1, y_1), \dots, (x_n, y_n), \\
  x_j = x(t_j), \quad y_j = y(t_j), \quad 0 \leq j \leq n.
  \end{aligned}
  $$

#### Example

| $t$   | 0   | 0.25 | 0.5  | 0.75 | 1    |
|-------|-----|------|------|------|------|
| $x(t)$| -1  | 0    | 1    | 1    | 1    |
| $y(t)$| 1   | 1    | 0.5  | 0    | -1   |

- **4th-degree interpolation on $x = x(t)$ and $y = y(t)$**:
  $$
  \begin{aligned}
  x(t) &= \left( \left( \left( -1 + \frac{32}{3} t \right) t + 6 \right) t - \frac{14}{3} \right) t - 1, \\
  y(t) &= \left( \left( \left( -\frac{4}{3} t + 4 \right) t - \frac{11}{3} \right) t + 1 \right) t.
  \end{aligned}
  $$

### Bezier Curves in Computer Graphics

- **Design**: Piece-wise cubic Hermite polynomials.
- **Feature**: Each cubic Hermite polynomial is completely determined by function/derivative at endpoints.
- **Consequence**: Each portion of the curve can be changed while leaving most of the curve the same.

#### Bezier Curves with Guide Points

(Note: No further details provided in PAGE79.)

## Additional Notes

### Simple, but Not Simpler (PAGE40, PAGE41)

- There is an exception to every rule: Deep learning is not simple at all, yet works on everything.

### Carl de Boor (PAGE43, PAGE44)

- **Carl de Boor**: The book about Splines.
- **Carl-Wilhelm Reinhold de Boor** (incomplete information, PAGE44 contains a long list of numbers, likely an OCR error, summarized here).
