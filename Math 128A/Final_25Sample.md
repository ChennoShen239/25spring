# Math128A: Sample Final Exam

This is a closed book exam, with the exception of a one-page cheat sheet on one side only. You are allowed to cite any results, up to Section 6.6 but excluding those in the exercises, from the textbook. Results from anywhere else will need to be justified. Completely correct answers given without justification will receive little credit. Partial solutions will get partial credit.

---

1.  Let $h>0$. Develop a finite difference method to approximate the *derivative* $f^{\prime}(x_{0})$ using function values $f(x_{0}-h), f(x_{0}+2h)$.
    (a) What is the order of your method?
    (b) Turn your method into a second order method with extrapolation.
***Solution*:** 
We seek an approximation $f'(x_0) \approx c_1 f(x_0-h) + c_2 f(x_0+2h)$.
Using Taylor expansions around $x_0$:
$f(x_0-h) = f(x_0) - h f'(x_0) + \frac{h^2}{2} f''(x_0) + O(h^3)$
$f(x_0+2h) = f(x_0) + 2h f'(x_0) + 2h^2 f''(x_0) + O(h^3)$

Substituting into the approximation:
$$\begin{align}
c_1 f(x_0-h) + c_2 f(x_0+2h)  & = (c_1+c_2)f(x_0)  \\
 & + (-c_1+2c_2)h f'(x_0)  \\
 & + (\frac{c_1}{2}+2c_2)h^2 f''(x_0) + O(h^3)
\end{align}$$
>[!Note]
>The key is to construct the equations based on this approximation

To approximate $f'(x_0)$, we set:
1.  $c_1+c_2 = 0 \implies c_2 = -c_1$
2.  $(-c_1+2c_2)h = 1$

Solving this system:
$$(-c_1-2c_1)h = 1 \implies -3c_1h = 1 \implies c_1 = -\frac{1}{3h}$$
Thus, $c_2 = \frac{1}{3h}$.
The finite difference formula is $$N(h) = \frac{f(x_0+2h) - f(x_0-h)}{3h}$$

**(a) Order of the method**

To find the order, we expand $N(h)$ using Taylor series for $f(x_0-h)$ and $f(x_0+2h)$ up to higher order terms:
$f(x_0-h) = f(x_0) - hf'(x_0) + \frac{h^2}{2}f''(x_0) - \frac{h^3}{6}f'''(x_0) + O(h^4)$
$f(x_0+2h) = f(x_0) + 2hf'(x_0) + 2h^2f''(x_0) + \frac{4h^3}{3}f'''(x_0) + O(h^4)$

$N(h) = \frac{1}{3h} \left[ (f(x_0+2h) - f(x_0)) - (f(x_0-h) - f(x_0)) \right]$
$N(h) = \frac{1}{3h} \left[ (2hf'(x_0) + 2h^2f''(x_0) + \frac{4h^3}{3}f'''(x_0)) - (-hf'(x_0) + \frac{h^2}{2}f''(x_0) - \frac{h^3}{6}f'''(x_0)) + O(h^4) \right]$
$N(h) = \frac{1}{3h} \left[ 3hf'(x_0) + \left(2-\frac{1}{2}\right)h^2f''(x_0) + \left(\frac{4}{3}+\frac{1}{6}\right)h^3f'''(x_0) + O(h^4) \right]$
$N(h) = f'(x_0) + \frac{1}{2}hf''(x_0) + \frac{1}{2}h^2f'''(x_0) + O(h^3)$.

The local truncation error is $LTE = f'(x_0) - N(h) = -\frac{h}{2}f''(x_0) - \frac{h^2}{2}f'''(x_0) + O(h^3)$.
The leading error term is $-\frac{h}{2}f''(x_0)$, so the method is first order ($O(h)$).

>[!Caution]
>Unlike in ODEs, the LTE here doesn't need to be divided by $h$, so keep this in mind!

**(b) Turn your method into a second order method with extrapolation**

The error expansion is $f'(x_0) = N(h) + K_1 h + K_2 h^2 + O(h^3)$, where $K_1 = -\frac{1}{2}f''(x_0)$.
Richardson extrapolation for a first-order method **uses $N(h)$ and $N(h/2)$.** 
The formula for the extrapolated value $N_2(h)$ is:
- $N_2(h) = 2N(h/2) - N(h)$.
- $N(h/2) = \frac{f(x_0+2(h/2)) - f(x_0-(h/2))}{3(h/2)} = \frac{f(x_0+h) - f(x_0-h/2)}{3h/2}$.

Substituting into $N_2(h)$:
$N_2(h) = 2 \left( \frac{f(x_0+h) - f(x_0-h/2)}{3h/2} \right) - \left( \frac{f(x_0+2h) - f(x_0-h)}{3h} \right)$
$N_2(h) = \frac{4(f(x_0+h) - f(x_0-h/2))}{3h} - \frac{f(x_0+2h) - f(x_0-h)}{3h}$
$N_2(h) = \frac{1}{3h} \left( 4f(x_0+h) - 4f(x_0-h/2) - f(x_0+2h) + f(x_0-h) \right)$.
This method $N_2(h)$ is second order ($O(h^2)$).

>[!note]
>The key idea here is to extrapolate using $N\left( \frac{h}{2} \right)$ to eliminate $K_{1}$, then we can get the key formula: $N_{2}(h)  = 2N\left( \frac{h}{2} \right)-N(h)$.

---
2.  Consider the iteration
    $$x_{k+1}=-(\alpha-1)x_k+\frac{1}{2}x_k^2,\quad k=0,1,\cdots,$$
    where $0<\alpha\leq1$ is given. Assume that the iteration converges to $0$ for all initial points $x_0$. What is the order of convergence for $0<\alpha<1$? What is the order of convergence for $\alpha=1$?

***Solution:***
Let the *fixed-point iteration* function be $g(x)$. The iteration is given by $x_{k+1} = g(x_k)$, where
$$g(x) = -(\alpha-1)x + \frac{1}{2}x^2 = (1-\alpha)x + \frac{1}{2}x^2.$$
We are given that the iteration converges to the fixed point $x^*=0$. The *order* of convergence is determined by the derivatives of $g(x)$ evaluated at $x^*=0$.

First, calculate the derivatives of $g(x)$:
$$g'(x) = \frac{d}{dx}\left((1-\alpha)x + \frac{1}{2}x^2\right) = (1-\alpha) + x$$
$$g''(x) = \frac{d}{dx}((1-\alpha) + x) = 1$$

Next, evaluate these derivatives at the fixed point $x^*=0$:
$$g'(0) = (1-\alpha) + 0 = 1-\alpha$$
$$g''(0) = 1$$

We now analyze the two cases for $\alpha$:

**Case 1: $0 < \alpha < 1$**

In this case, $1-\alpha$ satisfies $0 < 1-\alpha < 1$.
Therefore, $g'(0) = 1-\alpha$.
Since $0 < g'(0) < 1$, specifically $g'(0) \neq 0$.
When $g'(x^*) \neq 0$ and $|g'(x^*)| < 1$, the convergence is linear.
Thus, for $0 < \alpha < 1$, the order of convergence is **1 (linear)**.

>[!note]
>The key here is to think of this equation: $\lim_{ k \to \infty }\left\lvert  \frac{x_{k+1}-x^*}{x_{k}-x^*} \right\rvert = \lvert g'(x^*) \rvert$, and this can be derived by Taylor expansion.

**Case 2: $\alpha = 1$**

In this case, $1-\alpha = 1-1 = 0$.
Therefore, $g'(0) = 0$.
Since $g'(0) = 0$, the convergence is faster than linear. We look at the next derivative:
$g''(0) = 1$.
Since $g'(0) = 0$ and $g''(0) = 1 \neq 0$, the theory of fixed-point iteration states that the convergence is *quadratic*.
Thus, for $\alpha = 1$, the order of convergence is **2 (quadratic)**.

To summarize:
* For $0 < \alpha < 1$, the *order* of convergence is 1 (linear).
* For $\alpha = 1$, the *order* of convergence is 2 (quadratic).

>[!caution]
>You need to keep in mind the definition of the order of convergence and the rate of convergence!

---

3.  Determine the constants $C$ and $x_0$ so that the following quadrature
    $$\int_{-\infty}^{\infty}e^{-|x|}\:f(x)\:dx\approx C\:f(x_0)$$
    is exact for $f(x)=1$, $f(x)=x$.

***Solutions:***
The problem is to determine the constants $C$ and $x_0$ such that the quadrature rule
$$\int_{-\infty}^{\infty}e^{-|x|}f(x)dx \approx C f(x_0)$$
is exact for the functions $f(x)=1$ and $f(x)=x$. We enforce this exactness for each function.

**Case 1: $f(x)=1$**
The exact integral is:
$$ I_1 = \int_{-\infty}^{\infty} e^{-|x|} (1) dx $$
Since $e^{-|x|}$ is an *even* function, we have:
$$ I_1 = 2 \int_{0}^{\infty} e^{-x} dx = 2 \left[-e^{-x}\right]_{0}^{\infty} = 2 (0 - (-e^0)) = 2(1) = 2 $$
The approximation is:
$$ A_1 = C \cdot f(x_0) = C \cdot 1 = C $$
For the rule to be exact, $I_1 = A_1$, so:
$$ C = 2 \tag{1} $$

**Case 2: $f(x)=x$**
The exact integral is:
$$ I_2 = \int_{-\infty}^{\infty} e^{-|x|} x dx $$
The integrand $g(x) = x e^{-|x|}$ is an *odd* function, as $g(-x) = (-x)e^{-|-x|} = -x e^{-|x|} = -g(x)$. The integral of an odd function over a symmetric interval $(-\infty, \infty)$ is 0.
$$ I_2 = 0 $$
The approximation is:
$$ A_2 = C \cdot f(x_0) = C \cdot x_0 $$
For the rule to be exact, $I_2 = A_2$, so:
$$ C x_0 = 0 \tag{2} $$

**Solving for the constants**
We have the system of equations:
1.  $C = 2$
2.  $C x_0 = 0$

Substitute $C=2$ from (1) into (2):
$$ 2 x_0 = 0 $$
$$ x_0 = 0 $$

Therefore, the constants are $C=2$ and $x_0=0$.

---

4.  By performing *Gaussian elimination with partial pivoting*, find the permutation matrix $P$, the lower triangular matrix $L$ with 1’s on its diagonal, and the upper triangular matrix $U$ so that
    $$PA=LU,\quad\text{where}\quad A=\begin{pmatrix}0&1&1\\1&-2&-1\\1&-1&1\end{pmatrix}.$$
***Solutions:***

We want to find matrices $P, L, U$ such that $PA=LU$ for the given matrix $A$ using Gaussian elimination with partial pivoting. $L$ must have 1s on its diagonal.

Initial state:
$$ A = \begin{pmatrix} 0 & 1 & 1 \\ 1 & -2 & -1 \\ 1 & -1 & 1 \end{pmatrix}, \quad P = \begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix}, \quad L = \begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix} $$

**Step 1: Process column 1 ($k=1$)**

* **Partial Pivoting:**
    The first column of $A$ is $\begin{pmatrix} 0 \\ 1 \\ 1 \end{pmatrix}$. The element with the largest absolute value is 1, found in row 2 (element $a_{21}=1$) and row 3 (element $a_{31}=1$). We choose the one with the smaller row index, so we select row 2 as the pivot row.
    Swap row 1 and row 2.
    -   Swap rows 1 and 2 of $A$:
        $$ A \leftarrow \begin{pmatrix} 1 & -2 & -1 \\ 0 & 1 & 1 \\ 1 & -1 & 1 \end{pmatrix} $$
    -   Swap rows 1 and 2 of $P$:
        $$ P \leftarrow \begin{pmatrix} 0 & 1 & 0 \\ 1 & 0 & 0 \\ 0 & 0 & 1 \end{pmatrix} $$
    -   Swap $L_{1,j}$ with $L_{2,j}$ for $j < 1$. There are no such columns, so $L$ is unchanged by this rule for existing entries.
>[!Warning]
>Keep in mind if we swap rows during the PP in column $k$, for example row $a<b$, then we need to swap every entries in row $a$ and $b$ before the $k$-th column.
* **Elimination:**
    The pivot element is $a_{11}=1$.
    -   For row 2 ($i=2$): The element $a_{21}=0$. The multiplier $m_{21} = a_{21}/a_{11} = 0/1 = 0$.
        Store $L_{21}=0$. Row 2 remains $R_2 \leftarrow R_2 - 0 \cdot R_1$.
        The matrix $A$ is unchanged here.
    -   For row 3 ($i=3$): The element $a_{31}=1$. The multiplier $m_{31} = a_{31}/a_{11} = 1/1 = 1$.
        Store $L_{31}=1$. Perform $R_3 \leftarrow R_3 - m_{31} R_1 = R_3 - 1 \cdot R_1$:
        $$ R_3 = (1, -1, 1) - (1, -2, -1) = (1-1, -1-(-2), 1-(-1)) = (0, 1, 2) $$
    After elimination for column 1, the matrices are:
    $$ A \leftarrow \begin{pmatrix} 1 & -2 & -1 \\ 0 & 1 & 1 \\ 0 & 1 & 2 \end{pmatrix}, \quad L \leftarrow \begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 1 & 0 & 1 \end{pmatrix} $$
    $P$ remains $\begin{pmatrix} 0 & 1 & 0 \\ 1 & 0 & 0 \\ 0 & 0 & 1 \end{pmatrix}$.

**Step 2: Process column 2 ($k=2$)**

* **Partial Pivoting:**
    Consider elements below or at the diagonal in column 2: $a_{22}=1, a_{32}=1$. The maximum absolute value is 1. The current pivot element $a_{22}=1$ is suitable. No row swap is needed.
    $P, A, L$ (sub-diagonal part of column 1) remain unchanged from this sub-step.

* **Elimination:**
    The pivot element is $a_{22}=1$.
    -   For row 3 ($i=3$): The element $a_{32}=1$. The multiplier $m_{32} = a_{32}/a_{22} = 1/1 = 1$.
        Store $L_{32}=1$. Perform $R_3 \leftarrow R_3 - m_{32} R_2 = R_3 - 1 \cdot R_2$:
        $$ R_3 = (0, 1, 2) - (0, 1, 1) = (0-0, 1-1, 2-1) = (0, 0, 1) $$
    After elimination for column 2, the matrix $A$ has become $U$:
    $$ U = A \leftarrow \begin{pmatrix} 1 & -2 & -1 \\ 0 & 1 & 1 \\ 0 & 0 & 1 \end{pmatrix} $$
    The matrix $L$ is now fully determined:
    $$ L \leftarrow \begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 1 & 1 & 1 \end{pmatrix} $$
    $P$ remains $\begin{pmatrix} 0 & 1 & 0 \\ 1 & 0 & 0 \\ 0 & 0 & 1 \end{pmatrix}$.

**Final Result:**
The decomposition is:
$$ P = \begin{pmatrix} 0 & 1 & 0 \\ 1 & 0 & 0 \\ 0 & 0 & 1 \end{pmatrix} $$
$$ L = \begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 1 & 1 & 1 \end{pmatrix} $$
$$ U = \begin{pmatrix} 1 & -2 & -1 \\ 0 & 1 & 1 \\ 0 & 0 & 1 \end{pmatrix} $$

---

5.  Given an initial value ODE
    $$y'=f(t,y),\quad\mathrm{for}\quad a\leq t\leq b,\quad y(a)=\alpha.\tag{1}$$
    Consider the multi-step method for solving (1)
    $$w_{k+1}=-4w_{k}+5w_{k-1}+h\left(\gamma\:f(t_{k},w_{k})+\beta\:f(t_{k-1},w_{k-1})\right),\quad k=1,2,\cdots,N-1\tag{2}$$
    with starting values $w_{0},w_{1}$.
    (a) Choose the constants $\gamma$ and $\beta$ so the method (2) is of 2nd order.

***Solutions:***

>[!caution]
>Keep in mind how to construct the LTE $\tau_{k+1}(h)$!

**1. Define the Local Truncation Error (LTE)**

The given method can be rewritten as:
$$w_{k+1} + 4w_k - 5w_{k-1} - h(\gamma f_k + \beta f_{k-1}) = 0$$
The local truncation error $\tau_{k+1}(h)$ is found by *substituting the true solution $y(t)$ into the method* and dividing by $h$:
$$\tau_{k+1}(h) = \frac{y(t_{k+1}) + 4y(t_k) - 5y(t_{k-1})}{h} - \left(\gamma y'(t_k) + \beta y'(t_{k-1})\right)$$
For the method to be of order $p$, we need $\tau_{k+1}(h) = O(h^p)$. For a 2nd order method ($p=2$), we need $\tau_{k+1}(h) = O(h^2)$. This means terms in $\tau_{k+1}(h)$ of order $h^0$ and $h^1$ must be zero.

**2. Taylor Series Expansions**

Let's expand $y(t)$ and $y'(t)$ terms around $t_k$. We'll use $y_k$ for $y(t_k)$, $y'_k$ for $y'(t_k)$, etc.
* $y(t_{k+1}) = y_k + h y'_k + \frac{h^2}{2} y''_k + \frac{h^3}{6} y'''_k + \frac{h^4}{24} y^{(4)}_k + O(h^5)$
* $y(t_k) = y_k$
* $y(t_{k-1}) = y_k - h y'_k + \frac{h^2}{2} y''_k - \frac{h^3}{6} y'''_k + \frac{h^4}{24} y^{(4)}_k + O(h^5)$
* $y'(t_k) = y'_k$
* $y'(t_{k-1}) = y'_k - h y''_k + \frac{h^2}{2} y'''_k - \frac{h^3}{6} y^{(4)}_k + O(h^4)$

**3. Substitute Expansions into $\tau_{k+1}(h)$**

Let's first evaluate the fraction part of $\tau_{k+1}(h)$:
$$\begin{align*} \frac{1}{h} [  y(t_{k+1}) + 4y(t_k) - 5y(t_{k-1}) ] & = \frac{1}{h} [  (y_k + h y'_k + \frac{h^2}{2} y''_k + \frac{h^3}{6} y'''_k + \frac{h^4}{24} y^{(4)}_k) \\ & + 4y_k  - 5(y_k - h y'_k + \frac{h^2}{2} y''_k - \frac{h^3}{6} y'''_k + \frac{h^4}{24} y^{(4)}_k) ] \\&+ O(h^4) \end{align*}$$
Collecting terms by derivatives of $y_k$:
$$\begin{align*} &= \frac{1}{h} [(1+4-5)y_k + (h - 5(-h))y'_k + (\frac{h^2}{2} - 5\frac{h^2}{2})y''_k + (\frac{h^3}{6} - 5(-\frac{h^3}{6}))y'''_k + (\frac{h^4}{24} - 5\frac{h^4}{24})y^{(4)}_k] + O(h^4) \\ &= \frac{1}{h} [0 \cdot y_k + 6h y'_k - 2h^2 y''_k + h^3 y'''_k - \frac{4h^4}{24}y^{(4)}_k] + O(h^4) \\ &= 6y'_k - 2h y''_k + h^2 y'''_k - \frac{1}{6}h^3 y^{(4)}_k + O(h^4) \end{align*}$$
Now for the second part of $\tau_{k+1}(h)$:
$$\begin{align*} - (\gamma y'(t_k) + \beta y'(t_{k-1})) &= - [\gamma y'_k + \beta (y'_k - h y''_k + \frac{h^2}{2} y'''_k - \frac{h^3}{6} y^{(4)}_k)] + O(h^4) \\ &= -(\gamma+\beta)y'_k + \beta h y''_k - \frac{\beta h^2}{2} y'''_k + \frac{\beta h^3}{6} y^{(4)}_k + O(h^4)\end{align*}$$
Combining these parts to get $\tau_{k+1}(h)$:
$$\begin{align*} \tau_{k+1}(h) &= (6y'_k - 2h y''_k + h^2 y'''_k - \frac{1}{6}h^3 y^{(4)}_k) \\ & - ((\gamma+\beta)y'_k - \beta h y''_k + \frac{\beta h^2}{2} y'''_k - \frac{\beta h^3}{6} y^{(4)}_k) + O(h^4) \\ &=  (6 - (\gamma+\beta))y'_k  + (-2 + \beta)h y''_k + (1 - \frac{\beta}{2})h^2 y'''_k  + (-\frac{1}{6} + \frac{\beta}{6})h^3 y^{(4)}_k + O(h^4) \end{align*}$$

**4. Conditions for 2nd Order Accuracy**
For the method to be *2nd* order ($\tau_{k+1}(h) = O(h^2)$), the coefficients of $h^0$ (terms with $y'_k$) and $h^1$ (terms with $h y''_k$) in the expansion of $\tau_{k+1}(h)$ must be zero.
1.  *Coefficient* of $y'_k$ (term $h^0$):
    $$6 - \gamma - \beta = 0 \implies \gamma + \beta = 6$$
2.  *Coefficient* of $h y''_k$ (term $h^1$):
    $$-2 + \beta = 0 \implies \beta = 2$$

**5. Solve for $\gamma$ and $\beta$**
From condition (2), we get $\beta = 2$.
Substitute $\beta = 2$ into condition (1):
$\gamma + 2 = 6 \implies \gamma = 4$.
So, the constants are $\gamma = 4$ and $\beta = 2$.

**6. Check the Resulting Order**
Let's check the coefficient of $h^2 y'''_k$ with these values:
$1 - \frac{\beta}{2} = 1 - \frac{2}{2} = 1 - 1 = 0$.
The coefficient of $h^2$ is also zero. Now check the $h^3 y^{(4)}_k$ term:
$\frac{\beta-1}{6} = \frac{2-1}{6} = \frac{1}{6}$.
Since this coefficient is not zero, the local truncation error is:
$$\tau_{k+1}(h) = \frac{1}{6}h^3 y^{(4)}_k + O(h^4)$$
Because $\tau_{k+1}(h) = O(h^3)$, the method is actually of *3rd order*. A 3rd order method also satisfies the condition of being a 2nd order method.

**Conclusion:**
The constants are $\gamma = 4$ and $\beta = 2$.

---

6.  Compute $\mathrm{det}(A)$ with $A=\begin{pmatrix}1&2&0\\2&1&3\\0&4&\alpha\end{pmatrix}$. For which values of $\alpha$ is $\operatorname*{det}(A)=0$?

***Solution***:
This is so easy.

---

7.  Determine the exact conditions on the coefficients $a,b,c,d,e$ under which the following function is a cubic spline (i.e., $f\in C^{2}(-\infty,\infty)$):
    $$f(x)=\begin{cases}a(x-1)^2+b\:x^3,&\text{if }x\in(-\infty,0],\\c(x-1)^2,&\text{if }x\in[0,2],\\d(x-2)^3+e(x-1)^2,&\text{if }x\in[2,\infty).\end{cases}$$
***Solutions:***
To determine the conditions on the coefficients $a,b,c,d,e$ for the function $f(x)$ to be a cubic spline, $f(x)$ must be $C^2(-\infty,\infty)$. This means $f(x)$, $f'(x)$, and $f''(x)$ must be continuous at the knots $x=0$ and $x=2$.

The function is defined in three pieces:
1.  $S_0(x) = a(x-1)^2 + bx^3$ for $x \le 0$
2.  $S_1(x) = c(x-1)^2$ for $0 \le x \le 2$
3.  $S_2(x) = d(x-2)^3 + e(x-1)^2$ for $x \ge 2$

Let's find the first and second derivatives for each piece:

For $S_0(x) = a(x-1)^2 + bx^3$:
$S_0'(x) = 2a(x-1) + 3bx^2$
$S_0''(x) = 2a + 6bx$

For $S_1(x) = c(x-1)^2$:
$S_1'(x) = 2c(x-1)$
$S_1''(x) = 2c$

For $S_2(x) = d(x-2)^3 + e(x-1)^2$:
$S_2'(x) = 3d(x-2)^2 + 2e(x-1)$
$S_2''(x) = 6d(x-2) + 2e$

Now, we apply the continuity conditions at the knots.

**Continuity at $x=0$:**

1.  **Continuity of $f(x)$**: $S_0(0) = S_1(0)$
    $a(0-1)^2 + b(0)^3 = c(0-1)^2$
    $a(1) + 0 = c(1)$
    $a = c \quad \quad (1)$

2.  **Continuity of $f'(x)$**: $S_0'(0) = S_1'(0)$
    $2a(0-1) + 3b(0)^2 = 2c(0-1)$
    $-2a + 0 = -2c$
    $a = c \quad \quad (2)$ (This is the same as condition 1)

3.  **Continuity of $f''(x)$**: $S_0''(0) = S_1''(0)$
    $2a + 6b(0) = 2c$
    $2a = 2c$
    $a = c \quad \quad (3)$ (This is also the same as condition 1)

From the conditions at $x=0$, we get $a=c$.

**Continuity at $x=2$:**

1.  **Continuity of $f(x)$**: $S_1(2) = S_2(2)$
    $c(2-1)^2 = d(2-2)^3 + e(2-1)^2$
    $c(1)^2 = d(0)^3 + e(1)^2$
    $c = e \quad \quad (4)$

2.  **Continuity of $f'(x)$**: $S_1'(2) = S_2'(2)$
    $2c(2-1) = 3d(2-2)^2 + 2e(2-1)$
    $2c(1) = 3d(0) + 2e(1)$
    $2c = 2e$
    $c = e \quad \quad (5)$ (This is the same as condition 4)

3.  **Continuity of $f''(x)$**: $S_1''(2) = S_2''(2)$
    $2c = 6d(2-2) + 2e$
    $2c = 6d(0) + 2e$
    $2c = 2e$
    $c = e \quad \quad (6)$ (This is also the same as condition 4)

From the conditions at $x=2$, we get $c=e$.

**Summary of Conditions:**
The conditions for $f(x)$ to be a $C^2$ function (and thus a cubic spline, as each piece is a polynomial of degree at most 3) are:
1.  $a=c$
2.  $c=e$

Combining these conditions, we have:
$$a = c = e$$
There are no conditions imposed on the coefficients $b$ and $d$ by the $C^2$ continuity requirements at the knots. Therefore, $b$ and $d$ can be any real numbers.

**Final Conditions:**
The exact conditions on the coefficients for $f(x)$ to be a cubic spline are:
$a = c = e$, while $b$ and $d$ can be any real numbers.

---

8.  Does the function $f(t, y) = t^{2}y^{3}$ satisfy the Lipschitz condition on the domain
    $$\mathcal{D}\stackrel{\text{def}}{=}\{(t,y)\mid0\leq t\leq1,\:-\infty<y<\infty\}?$$
***Solutions:***
To determine if the function $f(t, y) = t^2 y^3$ satisfies the Lipschitz condition on the domain $\mathcal{D} = \{(t,y) \mid 0 \le t \le 1, -\infty < y < \infty\}$, we can examine its partial derivative with respect to $y$.

**1. Definition of Lipschitz Condition (with respect to $y$)**
A function $f(t,y)$ satisfies a Lipschitz condition with respect to $y$ on a domain $\mathcal{D}$ if there exists a positive constant $L$ (the Lipschitz constant) such that for any $(t, y_1)$ and $(t, y_2)$ in $\mathcal{D}$:
$$|f(t, y_1) - f(t, y_2)| \le L |y_1 - y_2|$$

**2. Calculate $\frac{\partial f}{\partial y}$**
For the given function $f(t, y) = t^2 y^3$:
$$ \frac{\partial f}{\partial y} = \frac{\partial}{\partial y} (t^2 y^3) $$
Treating $t$ as a constant with respect to $y$:
$$ \frac{\partial f}{\partial y} = t^2 \cdot (3y^2) = 3t^2 y^2 $$

**3. Analyze the Boundedness of $\left|\frac{\partial f}{\partial y}\right|$ on $\mathcal{D}$**
The domain $\mathcal{D}$ is defined by $0 \le t \le 1$ and $-\infty < y < \infty$.
We need to check if $\left|3t^2 y^2\right| = 3t^2 y^2$ (since $t^2 \ge 0$ and $y^2 \ge 0$) is bounded on this domain.

* The term $t^2$ is bounded: $0 \le t^2 \le 1$ (because $0 \le t \le 1$).
* The term $y^2$ is unbounded because $y$ can range from $-\infty$ to $\infty$. As $y \to \infty$ (or $y \to -\infty$), $y^2 \to \infty$.

Since $\left|\frac{\partial f}{\partial y}\right| = 3t^2 y^2$ can become arbitrarily large within the domain $\mathcal{D}$ (e.g., by taking $t=1$ and letting $y \to \infty$), it is not bounded.

**4. Conclusion**
Because the partial derivative $\left|\frac{\partial f}{\partial y}\right|$ is unbounded on the given domain $\mathcal{D}$, the function $f(t, y) = t^2 y^3$ **does not satisfy** the Lipschitz condition on this domain.