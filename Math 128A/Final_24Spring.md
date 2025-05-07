# Math128A: Final Exam

**This is a closed book exam, with the exception of a one-page cheat sheet on one side only. You are allowed to cite any results, up to Section 6.6 but excluding those in the exercises, from the textbook. Results from anywhere else will need to be justified. Completely correct answers given without justification will receive little credit. Partial solutions will get partial credit.**

---

### 1. Fixed Point Iteration

Let  
$$g(x) = \sqrt[3]{5x + 3}.$$

- Show that $g(x)$ has a fixed point at $P$ precisely when $f(p) = 0$, where  
  $$f(x) = x^3 - 5x - 3.$$

- Show that $g(x) \in [2, 3]$ for any $x \in [2, 3]$.

- Consider the fixed point iteration  
  $$x_{k+1} = g(x_k), \quad \text{for } k = 0, 1, \dots$$  
  with $x_0 \in [2, 3]$. Show that this iteration converges.


> **Solution:**  
> If $g(P) = P$, then $P = \sqrt[3]{5P + 3}$. Cubing both sides, we get:  
> $$P^3 = 5P + 3 \quad \Rightarrow \quad P^3 - 5P - 3 = 0 \quad \Leftrightarrow \quad f(P) = 0.$$  
> Hence, $P$ is a fixed point of $g$ if and only if $f(P) = 0$.

> **Solution:**  
> $g(x) = \sqrt[3]{5x + 3}$ is increasing and continuous. On $x \in [2, 3]$:
> - $g(2) = \sqrt[3]{13} \approx 2.38$  
> - $g(3) = \sqrt[3]{18} \approx 2.62$  
> So $g(x) \in [2.38, 2.62] \subset [2, 3]$. Therefore, $g(x) \in [2, 3]$ for all $x \in [2, 3]$.

> **Solution:**  
> To apply the Banach fixed-point theorem:
> 1. $g$ is continuous on $[2,3]$.
> 2. As shown above, $g([2,3]) \subset [2,3]$.
> 3. Show $g$ is a contraction:  
> Compute the derivative:  
> $$g'(x) = \frac{d}{dx} \left( (5x + 3)^{1/3} \right) = \frac{5}{3}(5x + 3)^{-2/3}.$$  
> On $x \in [2, 3]$, we have $5x + 3 \in [13, 18]$, so:
> $$|g'(x)| \leq \frac{5}{3} \cdot 13^{-2/3} \approx 0.43 < 1.$$  
> Thus, $g$ is a contraction mapping on $[2, 3]$.  
> Therefore, by the Banach fixed-point theorem, the iteration  
> $$x_{k+1} = g(x_k)$$  
> converges to the unique fixed point in $[2,3]$.

---

### 2. Quadrature Formula

Determine constants $a$, $b$, and $c$ such that the quadrature formula  
$$\int_{0}^{1} f(x)\,dx \approx af(0) + bf(1) + cf\left(\frac{1}{3}\right)$$  
has degree of precision 2.

> **Solution:**  
> A quadrature formula has degree of precision 2 if it integrates all polynomials of degree ≤ 2 exactly.  
> Let us require the formula to be exact for $f(x) = 1$, $x$, and $x^2$.
> 
> **Step 1: Use $f(x) = 1$**  
> $$
 \int_0^1 1\,dx = 1 = a\cdot 1 + b\cdot 1 + c\cdot 1 = a + b + c \quad \text{(Eq1)}
 $$
> 
> **Step 2: Use $f(x) = x$**  
> $$
 \int_0^1 x\,dx = \frac{1}{2} = a\cdot 0 + b\cdot 1 + c\cdot \frac{1}{3} = b + \frac{c}{3} \quad \text{(Eq2)}
$$
> 
> **Step 3: Use $f(x) = x^2$**  
> $$
 \int_0^1 x^2\,dx = \frac{1}{3} = a\cdot 0^2 + b\cdot 1^2 + c\cdot \left(\frac{1}{3}\right)^2 = b + \frac{c}{9} \quad \text{(Eq3)}
 $$
> 
> Now solve the system:
> - (Eq1): $a + b + c = 1$
> - (Eq2): $b + \frac{c}{3} = \frac{1}{2}$
> - (Eq3): $b + \frac{c}{9} = \frac{1}{3}$
> 
> **Step 4: Solve equations**  
> Subtract (Eq3) from (Eq2):
> $$
 \left(b + \frac{c}{3}\right) - \left(b + \frac{c}{9}\right) = \frac{1}{2} - \frac{1}{3} \Rightarrow \frac{2c}{9} = \frac{1}{6} \Rightarrow c = \frac{9}{12} = \frac{3}{4}
 $$
> Plug into (Eq2):  
> $$
 b + \frac{1}{4} = \frac{1}{2} \Rightarrow b = \frac{1}{4}
 $$
> Then use (Eq1):  
> $$
 a + \frac{1}{4} + \frac{3}{4} = 1 \Rightarrow a = 0
$$
> 
>**Final result:**  
> $$
 a = 0,\quad b = \frac{1}{4},\quad c = \frac{3}{4}
 $$


---

### 3. Quadrature Transformation

Consider a quadrature of the form  
$$\int_{-1}^{1} f(x)\,dx \approx \sum_{j=1}^{5} c_j f(x_j)$$  
for nodes $x_1, \dots, x_5 \in [-1, 1]$ and constants $c_1, \dots, c_5$. Assume the quadrature is exact for $f(x) = 1$, $x$.

Show that the following quadrature  
$$\int_a^b f(x)\,dx \approx \sum_{j=1}^5 \widehat{c}_j f(\widehat{x}_j) \tag{2}$$  
with $b > a$ and  
$$\widehat{c}_j = \frac{b-a}{2} c_j,\quad \widehat{x}_j = \frac{b+a}{2} + \frac{b-a}{2} x_j, \quad \text{for } j = 1,\dots,5$$  
is exact for $f(x) = 1$, $x$.

> **Solution:**
> Let the original quadrature rule be
> $$\int_{-1}^{1} g(y)\,dy \approx \sum_{j=1}^{5} c_j g(x_j)$$
> where $x_j \in [-1, 1]$ are nodes. This rule is exact for $g(y) = 1$ and $g(y) = y$.
> 1. For $g(y)=1$: $\int_{-1}^{1} 1\,dy = 2 = \sum_{j=1}^{5} c_j \cdot 1 \implies \sum_{j=1}^{5} c_j = 2 \quad (A)$.
> 2. For $g(y)=y$: $\int_{-1}^{1} y\,dy = 0 = \sum_{j=1}^{5} c_j x_j \implies \sum_{j=1}^{5} c_j x_j = 0 \quad (B)$.
>
> The transformed quadrature for $\int_a^b f(x)\,dx$ is
> $$\int_a^b f(x)\,dx \approx \sum_{j=1}^5 \widehat{c}_j f(\widehat{x}_j) \quad (2)$$
> with $\widehat{c}_j = \frac{b-a}{2} c_j$ and $\widehat{x}_j = \frac{b+a}{2} + \frac{b-a}{2} x_j$.
> We show this is exact for $f(x)=1$ and $f(x)=x$.
>
> **Case 1: $f(x) = 1$**
> The exact integral is $\int_a^b 1\,dx = b-a$.
> The quadrature sum is $\sum_{j=1}^5 \widehat{c}_j f(\widehat{x}_j) = \sum_{j=1}^5 \widehat{c}_j (1) = \sum_{j=1}^5 \frac{b-a}{2} c_j$.
> This simplifies to $\frac{b-a}{2} \sum_{j=1}^5 c_j$. Using (A), this is $\frac{b-a}{2} (2) = b-a$.
> Thus, the quadrature is exact for $f(x)=1$.
>
> **Case 2: $f(x) = x$**
> The exact integral is $\int_a^b x\,dx = \frac{b^2 - a^2}{2}$.
> The quadrature sum is $\sum_{j=1}^5 \widehat{c}_j f(\widehat{x}_j) = \sum_{j=1}^5 \widehat{c}_j \widehat{x}_j$.
> Substituting for $\widehat{c}_j$ and $\widehat{x}_j$:
> $$ \begin{align}
\sum_{j=1}^5 \left(\frac{b-a}{2} c_j\right) \left(\frac{b+a}{2} + \frac{b-a}{2} x_j\right)  & = \frac{b-a}{2} \sum_{j=1}^5 c_j \left(\frac{b+a}{2} + \frac{b-a}{2} x_j\right)  \\
 & = \frac{b-a}{2} \left( \frac{b+a}{2} \sum_{j=1}^5 c_j + \frac{b-a}{2} \sum_{j=1}^5 c_j x_j \right) 
\end{align}$$
> Using (A) and (B):
> $$ = \frac{b-a}{2} \left( \frac{b+a}{2} (2) + \frac{b-a}{2} (0) \right) = \frac{b-a}{2} (b+a) = \frac{b^2 - a^2}{2} $$
> Thus, the quadrature is exact for $f(x)=x$.


---

### 4. Matrix Properties and LU Factorization

Let  
$$A = \begin{pmatrix}1 & 1 & 0\\ 1 & 3 & -1\\ 0 & -1 & 1\end{pmatrix}.$$

- Show that the matrix $A$ is symmetric positive definite.
- Compute the LU factorization of $A$ without partial pivoting.
> **Solution:**
> Given $A = \begin{pmatrix}1 & 1 & 0\\ 1 & 3 & -1\\ 0 & -1 & 1\end{pmatrix}$.
>
> -   **Show $A$ is symmetric positive definite.**
>
>     $A$ is symmetric since $A = A^T$. For positive definiteness, we check the leading principal minors (Sylvester's Criterion):
>     1.  $M_1 = \det([1]) = 1 > 0$.
>     2.  $M_2 = \det\begin{pmatrix}1 & 1\\ 1 & 3\end{pmatrix} = (1)(3) - (1)(1) = 2 > 0$.
>     3.  $M_3 = \det(A) = 1\det\begin{pmatrix}3 & -1\\ -1 & 1\end{pmatrix} - 1\det\begin{pmatrix}1 & -1\\ 0 & 1\end{pmatrix} = 1(3-1) - 1(1-0) = 2-1 = 1 > 0$.
>     Since $A$ is symmetric and its leading principal minors are all positive, $A$ is symmetric positive definite.
>
> -   **Compute the LU factorization of $A$ without partial pivoting.**
>
>     We seek $A=LU$.
>     $$ A = \begin{pmatrix}1 & 1 & 0\\ 1 & 3 & -1\\ 0 & -1 & 1\end{pmatrix} $$
>     $R_2 \leftarrow R_2 - (1)R_1 \implies l_{21}=1$. ($A_{31}$ is already 0, so $l_{31}=0$.)
>     $$ \rightarrow \begin{pmatrix}1 & 1 & 0\\ 0 & 2 & -1\\ 0 & -1 & 1\end{pmatrix} $$
>     $R_3 \leftarrow R_3 - (-1/2)R_2 \implies l_{32}=-1/2$.
>     $$ \rightarrow \begin{pmatrix}1 & 1 & 0\\ 0 & 2 & -1\\ 0 & 0 & 1/2\end{pmatrix} = U $$
>     Thus,
>     $$ L = \begin{pmatrix}1 & 0 & 0\\ 1 & 1 & 0\\ 0 & -1/2 & 1\end{pmatrix} \quad \text{and} \quad U = \begin{pmatrix}1 & 1 & 0\\ 0 & 2 & -1\\ 0 & 0 & 1/2\end{pmatrix} $$
>     So, $A = LU = \begin{pmatrix}1 & 0 & 0\\ 1 & 1 & 0\\ 0 & -1/2 & 1\end{pmatrix} \begin{pmatrix}1 & 1 & 0\\ 0 & 2 & -1\\ 0 & 0 & 1/2\end{pmatrix}$.


---

### 5. Initial Value Problem

Show that the initial value ODE  
$$y' = -t|y| + 1,\quad \text{for } 0 \leq t \leq 1,\quad y(0) = 1$$  
is well-posed on  
$${\mathcal D} = \{(t, y) \mid 0 \leq t \leq 1,\; -\infty < y < \infty\}.$$

> **Solution:**
> An initial value problem (IVP) $y' = f(t,y)$, $y(t_0) = y_0$ is well-posed on a domain $\mathcal{D}$ if a unique solution exists and this solution depends continuously on the initial conditions. This is typically guaranteed if $f(t,y)$ is continuous on $\mathcal{D}$ and satisfies a Lipschitz condition with respect to $y$ on $\mathcal{D}$.
>
> For the given IVP:
> $$ y' = -t|y| + 1, \quad 0 \leq t \leq 1, \quad y(0) = 1 $$
> The function is $f(t,y) = -t|y| + 1$, and the domain is $\mathcal{D} = \{(t, y) \mid 0 \leq t \leq 1,\; -\infty < y < \infty\}$.
>
> 1.  **Continuity of $f(t,y)$ on $\mathcal{D}$**:
>     The function $t$ is continuous. The absolute value function $|y|$ is continuous for all $y$. The constant function $1$ is continuous. Since $f(t,y)$ is formed by products and sums of continuous functions ($-t \times |y| + 1$), $f(t,y)$ is continuous on the entire domain $\mathcal{D}$.
>
> 2.  **Lipschitz condition for $f(t,y)$ with respect to $y$ on $\mathcal{D}$**:
>     We need to show there exists a constant $L > 0$ such that for any $(t, y_1), (t, y_2) \in \mathcal{D}$:
>     $$ |f(t, y_1) - f(t, y_2)| \leq L |y_1 - y_2| $$
>     Let's compute the difference:
>     $$ \begin{align}
|f(t, y_1) - f(t, y_2)|  & = |(-t|y_1| + 1) - (-t|y_2| + 1)|  \\
 & =|-t|y_1| + t|y_2||  \\
 & = |-t(|y_1| - |y_2|)| 
\end{align}$$
>     Since $0 \leq t \leq 1$, $|-t| = t$.
>     $$ = t ||y_1| - |y_2|| $$
>     Using the reverse triangle inequality, $||y_1| - |y_2|| \leq |y_1 - y_2|$.
>     $$ t ||y_1| - |y_2|| \leq t |y_1 - y_2| $$
>     Since $0 \leq t \leq 1$ on the domain $\mathcal{D}$, the maximum value of $t$ is $1$.
>     Therefore,
>     $$ |f(t, y_1) - f(t, y_2)| \leq 1 \cdot |y_1 - y_2| = |y_1 - y_2| $$
>     Thus, $f(t,y)$ satisfies a Lipschitz condition with respect to $y$ on $\mathcal{D}$ with Lipschitz constant $L=1$.
>
> **Conclusion**:
> Since $f(t,y)$ is **continuous** on $\mathcal{D}$ and satisfies a **Lipschitz condition** in the variable $y$ on $\mathcal{D}$ (where $\mathcal{D}$ is of the form $[a,b] \times \mathbb{R}$), the initial value problem has a unique solution on $[0,1]$ and is **well-posed**. 

---

### 6. Matrix Inverse and Determinant

Let  
$$A = \begin{pmatrix}1 & 1 & 1\\ 0 & 3 & \alpha\\ 0 & 1 & 2\end{pmatrix} \in \mathbb{R}^{3 \times 3}.$$

- Compute the determinant of $A$.
- For what values of $\alpha$ does $A^{-1}$ exist? Compute $A^{-1}$ when it exists.
> **Solution:**
> Given the matrix
> $$A = \begin{pmatrix}1 & 1 & 1\\ 0 & 3 & \alpha\\ 0 & 1 & 2\end{pmatrix}.$$
>
> -   **Compute the determinant of $A$.**
>     We can compute the determinant by expanding along the first column:
>     $$ \begin{align}
\det(A)  & = 1 \cdot \det\begin{pmatrix}3 & \alpha\\ 1 & 2\end{pmatrix} - 0 \cdot \det\begin{pmatrix}1 & 1\\ 1 & 2\end{pmatrix} + 0 \cdot \det\begin{pmatrix}1 & 1\\ 3 & \alpha\end{pmatrix} \\
 &  = 1 \cdot ((3)(2) - (\alpha)(1))  \\
 & = 6 - \alpha
\end{align}$$
>     So, $\det(A) = 6 - \alpha$.
>
> -   **For what values of $\alpha$ does $A^{-1}$ exist? Compute $A^{-1}$ when it exists.**
>     The inverse $A^{-1}$ exists if and only if $\det(A) \neq 0$.
>     Therefore, $A^{-1}$ exists when $6 - \alpha \neq 0$, which means $\alpha \neq 6$.
>
>     When $\alpha \neq 6$, the inverse is given by $A^{-1} = \frac{1}{\det(A)} \text{adj}(A)$, where $\text{adj}(A)$ is the adjugate (transpose of the cofactor matrix) of $A$.
>
>     First, we find the cofactor matrix $C = (C_{ij})$:
>     $C_{11} = +\det\begin{pmatrix}3 & \alpha\\ 1 & 2\end{pmatrix} = 6 - \alpha$
>     $C_{12} = -\det\begin{pmatrix}0 & \alpha\\ 0 & 2\end{pmatrix} = 0$
>     $C_{13} = +\det\begin{pmatrix}0 & 3\\ 0 & 1\end{pmatrix} = 0$
>
>     $C_{21} = -\det\begin{pmatrix}1 & 1\\ 1 & 2\end{pmatrix} = -(2 - 1) = -1$
>     $C_{22} = +\det\begin{pmatrix}1 & 1\\ 0 & 2\end{pmatrix} = 2 - 0 = 2$
>     $C_{23} = -\det\begin{pmatrix}1 & 1\\ 0 & 1\end{pmatrix} = -(1 - 0) = -1$
>
>     $C_{31} = +\det\begin{pmatrix}1 & 1\\ 3 & \alpha\end{pmatrix} = \alpha - 3$
>     $C_{32} = -\det\begin{pmatrix}1 & 1\\ 0 & \alpha\end{pmatrix} = -(\alpha - 0) = -\alpha$
>     $C_{33} = +\det\begin{pmatrix}1 & 1\\ 0 & 3\end{pmatrix} = 3 - 0 = 3$
>
>     So the cofactor matrix is:
>     $$ C = \begin{pmatrix} 6-\alpha & 0 & 0 \\ -1 & 2 & -1 \\ \alpha-3 & -\alpha & 3 \end{pmatrix} $$
>     The adjugate matrix is $\text{adj}(A) = C^T$:
>     $$ \text{adj}(A) = \begin{pmatrix} 6-\alpha & -1 & \alpha-3 \\ 0 & 2 & -\alpha \\ 0 & -1 & 3 \end{pmatrix} $$
>     Therefore, for $\alpha \neq 6$:
>     $$ A^{-1} = \frac{1}{6-\alpha} \begin{pmatrix} 6-\alpha & -1 & \alpha-3 \\ 0 & 2 & -\alpha \\ 0 & -1 & 3 \end{pmatrix} = \begin{pmatrix} 1 & \frac{-1}{6-\alpha} & \frac{\alpha-3}{6-\alpha} \\ 0 & \frac{2}{6-\alpha} & \frac{-\alpha}{6-\alpha} \\ 0 & \frac{-1}{6-\alpha} & \frac{3}{6-\alpha} \end{pmatrix} $$
---

### 7. Continuity of Piecewise Function

Consider the piecewise function  
$$
P(x) = \begin{cases}
1, & \text{for } x \in (-1, 0],\\
a + bx + cx^2, & \text{for } x \in [0, 1)
\end{cases}
$$

Find conditions on constants $a$, $b$, and $c$ so that $P(x)$ is second-order continuously differentiable on $(-1, 1)$.
> **Solution:**
> For $P(x)$ to be second-order continuously differentiable on $(-1, 1)$, the function $P(x)$, its first derivative $P'(x)$, and its second derivative $P''(x)$ must all be continuous at the point $x=0$ where the definition of the function changes.
>
> Let $P_1(x) = 1$ for $x \in (-1, 0]$ and $P_2(x) = a + bx + cx^2$ for $x \in [0, 1)$.
>
> 1.  **Continuity of $P(x)$ at $x=0$ ($P \in C^0$)**:
>     We need $\lim_{x \to 0^-} P(x) = \lim_{x \to 0^+} P(x) = P(0)$.
>     -   $\lim_{x \to 0^-} P(x) = \lim_{x \to 0^-} P_1(x) = 1$.
>     -   $P_1(0) = 1$.
>     -   $\lim_{x \to 0^+} P(x) = \lim_{x \to 0^+} P_2(x) = a + b(0) + c(0)^2 = a$.
>     -   $P_2(0) = a$.
>     For continuity at $x=0$, we must have $1 = a$.
>     **Condition 1: $a = 1$.**
>
> 2.  **Continuity of $P'(x)$ at $x=0$ ($P \in C^1$)**:
>     First, we find the derivatives of the pieces:
>     -   $P_1'(x) = \frac{d}{dx}(1) = 0$ for $x \in (-1, 0)$.
>     -   $P_2'(x) = \frac{d}{dx}(a + bx + cx^2) = b + 2cx$ for $x \in (0, 1)$.
>     We need $\lim_{x \to 0^-} P'(x) = \lim_{x \to 0^+} P'(x)$.
>     -   $\lim_{x \to 0^-} P'(x) = 0$.
>     -   $\lim_{x \to 0^+} P'(x) = b + 2c(0) = b$.
>     For continuity of $P'(x)$ at $x=0$, we must have $0 = b$.
>     **Condition 2: $b = 0$.**
>
> 3.  **Continuity of $P''(x)$ at $x=0$ ($P \in C^2$)**:
>     Next, we find the second derivatives of the pieces:
>     -   $P_1''(x) = \frac{d}{dx}(0) = 0$ for $x \in (-1, 0)$.
>     -   $P_2''(x) = \frac{d}{dx}(b + 2cx)$. With $b=0$ from the previous step, $P_2'(x) = 2cx$, so $P_2''(x) = 2c$ for $x \in (0, 1)$.
>     We need $\lim_{x \to 0^-} P''(x) = \lim_{x \to 0^+} P''(x)$.
>     -   $\lim_{x \to 0^-} P''(x) = 0$.
>     -   $\lim_{x \to 0^+} P''(x) = 2c$.
>     For continuity of $P''(x)$ at $x=0$, we must have $0 = 2c$.
>     **Condition 3: $c = 0$.**
>
> Therefore, for $P(x)$ to be second-order continuously differentiable on $(-1, 1)$, the constants must satisfy:
> $$ a = 1, \quad b = 0, \quad c = 0 $$
> Under these conditions, $P(x) = 1$ for all $x \in (-1, 1)$, which is indeed a $C^2$ (in fact, $C^\infty$) function.

---

### 8. Lipschitz and ODE System

**(a)** Let function  
$$f(t, y_1, y_2) = ty_1 - 2\sin(y_2) + t^2 - 1.$$  
Find the Lipschitz constant for $f(t, y_1, y_2)$ on the domain  
$$\mathcal{D} = \{(t, y_1, y_2) \mid 0 \leq t \leq 1,\; -\infty < y_1 < \infty,\; -\infty < y_2 < \infty\}.$$

**(b)** Convert the following second-order initial value differential equation into a system of first-order initial value differential equations:  
$$y'' + y = te^t,\quad 0 \leq t \leq 1,\quad y(0) = 1,\quad y'(0) = -1.$$

> **Solution:**
>
> **(a) Lipschitz Constant**
>
> For $f(t, y_1, y_2) = ty_1 - 2\sin(y_2) + t^2 - 1$ on $\mathcal{D} = \{(t, y_1, y_2) \mid 0 \leq t \leq 1,\; -\infty < y_1 < \infty,\; -\infty < y_2 < \infty\}$:
> The partial derivatives with respect to $y_1$ and $y_2$ are:
> $$
\begin{align}
\frac{ \partial f }{ \partial y _{1}}  & = t \\
\frac{ \partial f }{ \partial y_{2}  } & = -2 \cos(y_{2})  
\end{align}
$$
> The suprema of their absolute values on $\mathcal{D}$ are:
> $$ M_1 = \sup_{0 \leq t \leq 1} |t| = 1 ,M_2 = \sup_{-\infty < y_2 < \infty} |-2\cos(y_2)| = 2$$
> Then, a Lipschitz constant is $L = \max \left\{ M_{1},M_{2} \right\}=2$. (based on $\ell_{1}$ norm)
>
> **(b) Convert to a System of First-Order IVPs**
>
> Given $y'' + y = te^t$, with $y(0) = 1$ and $y'(0) = -1$.
> Let $u_1(t) = y(t)$ and $u_2(t) = y'(t)$.
> Then the system is:
> $$ u_1'(t) = y'(t) = u_2(t) $$
> $$ u_2'(t) = y''(t) = te^t - y(t) = te^t - u_1(t) $$
> The initial conditions become:
> $$ u_1(0) = y(0) = 1 $$
> $$ u_2(0) = y'(0) = -1 $$
> So, the system is:
> $$ \begin{cases} u_1' = u_2, & u_1(0) = 1 \\ u_2' = te^t - u_1, & u_2(0) = -1 \end{cases} $$
> for $0 \leq t \leq 1$.



---

**Your Name and SID:**  
