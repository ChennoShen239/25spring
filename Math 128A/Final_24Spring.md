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

---

### 6. Matrix Inverse and Determinant

Let  
$$A = \begin{pmatrix}1 & 1 & 1\\ 0 & 3 & \alpha\\ 0 & 1 & 2\end{pmatrix} \in \mathbb{R}^{3 \times 3}.$$

- Compute the determinant of $A$.
- For what values of $\alpha$ does $A^{-1}$ exist? Compute $A^{-1}$ when it exists.

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

---

### 8. Lipschitz and ODE System

**(a)** Let function  
$$f(t, y_1, y_2) = ty_1 - 2\sin(y_2) + t^2 - 1.$$  
Find the Lipschitz constant for $f(t, y_1, y_2)$ on the domain  
$$\mathcal{D} = \{(t, y_1, y_2) \mid 0 \leq t \leq 1,\; -\infty < y_1 < \infty,\; -\infty < y_2 < \infty\}.$$

**(b)** Convert the following second-order initial value differential equation into a system of first-order initial value differential equations:  
$$y'' + y = te^t,\quad 0 \leq t \leq 1,\quad y(0) = 1,\quad y'(0) = -1.$$

---

**Your Name and SID:**  
