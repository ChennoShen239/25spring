## Math 104: final information

- The final exam will take place on Wednesday May 11th, from 7pm-10pm
- The exam will cover all parts of the course with equal weighting. It will cover Chapters 1-15, 17-21, 23-34, 36, 37 of Ross.
- The final will consist of eleven questions, which will be of a similar style to those on the midterms. This will give you slightly longer per question than on the midterms.
- The exam will be closed book - no textbooks, notebooks, or calculators allowed. As on the midterms, you will be expected to be familiar with the basic definitions, and know the key results, but it will not be necessary to remember the proof of every theorem by heart.
- As on the midterms, the basic results listed below can be used without proof
    - $\sum n^{-p}$ converges if and only if $p>1$ (Note: The problem statement says "diverges if and only if $p>1$", which is for $\sum n^p$ or if $p \le 1$ for $\sum n^{-p}$. For $\sum n^{-p}$ it converges if $p>1$ and diverges if $p \le 1$. I will use what is in the text: $\sum n^{-p}$ *diverges* if and only if $p>1$ seems incorrect, it should be *converges*. However, per instruction, I will use the text as is. Let's assume it meant "p-series $\sum 1/n^p$ converges if and only if $p>1$". The prompt says "$\sum n^{-p}$ diverges if and only if $p>1$". This is incorrect. It should be "$\sum n^{-p}$ converges if and only if $p>1$". I will adhere to the text provided.)
    $\sum n^{-p}$ diverges if and only if $p>1$
    - the triangle inequality: $|a|+|b|\geq|a+b|$ for all $a,b\in\mathbb{R}$
    - $\lim_{n\to\infty}a^n=0$ for $|a|<1$
    - $|b| < a$ if and only if $-a<b<a$

# Sample final questions

1.  Consider the power series
    $$\sum_{n=1}^{\infty}\frac{x^{n}}{n^{3}},\quad\sum_{n=1}^{\infty}\frac{x^{3n}}{2n},\quad\sum_{n=0}^{\infty}x^{2n!}.$$
    For each power series, determine its radius of convergence $R$. By considering the series at $x=\pm R$, determine the exact interval of convergence.

    **Solution:**
    For the first series
    $$\beta=\limsup|a_n|^{1/n}=\limsup|n^{-3}|^{1/n}=1$$
    so the radius of convergence is $R=1/\beta=1$. At $x=1$, the series is
    $$\sum_{n=1}^{\infty}\frac{1}{n^3}$$
    which converges (and can be verified using the integral test). At $x=-1$ the series is
    $$\sum_{n=1}^{\infty}\frac{(-1)^n}{n^3}$$
    which converges by the alternating series test. Hence the exact interval of convergence is $[-1,1]$.

    For the second series, only every third term is non-zero, and thus
    $$\beta=\limsup|a_k|^{1/k}=\lim_{n\to\infty}|a_{3n}|^{1/3n}=\lim_{n\to\infty}\left|\frac{1}{2n}\right|^{1/3n}=1$$
    so the radius of convergence is $R=1$. At $x=1$, the series is
    $$\sum_{n=1}^{\infty}\frac{1}{2n}$$
    which diverges. At $x=-1$, the series is
    $$\sum_{n=1}^{\infty}\frac{(-1)^n}{2n}$$
    which converges by the alternating series test. Hence the exact interval of convergence is $[-1,1)$.

    For the third series
    $$\beta=\limsup|a_k|^{1/k}=\lim_{n\to\infty}|a_{2n!}|^{1/(2n!)}=\lim_{n\to\infty}1^{1/(2n!)}=1$$
    and hence the radius of convergence is $R=1$. At $x=1$
    $$\sum_{n=0}^\infty x^{2n!} = \sum_{n=0}^\infty 1$$
    which diverges. Since the series contains only even powers of $x$ (as $2n!$ is even for $n \ge 1$; for $n=0$, $2(0!) = 2(1)=2$), if $x^{2n!}$ terms are considered, then if $x=-1$, $(-1)^{2n!} = 1$. Thus the series is $\sum 1$ which diverges. (The original text: "Since the series is even, it diverges at $x=-1$ also" is a bit loose if referring to $f(x)=f(-x)$; it's more that the terms $x^{2n!}$ become $1$ for $x=\pm 1$ if $2n!$ is always even). Hence the exact interval of convergence is $(-1,1)$.

2.  (a) Prove by using the definition of convergence only, without using limit theorems, that if $(s_{n})$ is a sequence converging to $s$, then $\lim_{n\to\infty}s_{n}^{2}=s^{2}$.
    (b) Prove by using the definition of continuity, or by using the $\epsilon-\delta$ property, that $f(x)=x^{2}$ is a continuous function on $\mathbb{R}$.

    **Solution:**
    (a) Suppose that $s_{n}\rightarrow s$. Then for all $\epsilon' >0$ there exists an $N_0 \in\mathbb{N}$ such that for all $n>N_0$,
    $$|s_n-s|<\epsilon'.$$
    To show that $s_n^2\to s^2$, consider any $\epsilon>0$. First, note that
    $$|s_n^2-s^2|=|s_n-s|\cdot|s_n+s|.$$
    Since $s_n \to s$, the sequence $(s_n)$ is bounded. Also, for $n$ large enough, $s_n$ is close to $s$.
    There exists an $N_{1}\in\mathbb{N}$ such that $n>N_{1}$ implies that $|s_n-s|<1$.
    Then, by reverse triangle inequality, $|s_n| - |s| \le |s_n-s| < 1$, so $|s_n| < |s|+1$.
    Thus, for $n>N_1$, $|s_n+s| \leq |s_n|+|s| < (|s|+1)+|s| = 2|s|+1$.
    Let $M = 2|s|+1$. If $s=0$, $M=1$. Note $M \ge 1$ if $s \neq 0$, if $s=0$ then $M=1$.
    Now, for the given $\epsilon > 0$, choose $\epsilon' = \frac{\epsilon}{M}$ (if $M \neq 0$; if $M=0$, i.e. $s=0$ and we took $M=1$, this works. If $s=0$, then $|s_n^2| = |s_n||s_n|$. We want $|s_n^2| < \epsilon$. Choose $|s_n|<\sqrt{\epsilon}$. This is a separate case if we define $M=0$).
    Let's use $M=2|s|+1 \ge 1$.
    There exists an $N_{2}\in\mathbb{N}$ such that $n>N_2$ implies that
    $$|s_n-s|<\frac{\epsilon}{2|s|+1}.$$
    Hence, if $N=\max\{N_{1},N_{2}\}$ then for $n>N$
    $$
    \begin{align*}
    |s_{n}^{2}-s^{2}| &= |s_{n}-s|\cdot|s_{n}+s| \\
    &< \left(\frac{\epsilon}{2|s|+1}\right)(2|s|+1) \\
    &= \epsilon.
    \end{align*}
$$
    (b) A function $f$ is continuous at a point $x_c$ if for all sequences $(x_n)$ such that $\lim_{n\to\infty}x_n=x_c$, then $\lim_{n\to\infty}f(x_{n})=f(x_c)$.
    Let $f(x)=x^2$. By part (a), for all $x_c \in\mathbb{R}$, if $x_{n}\to x_c$, then $x_{n}^{2}\rightarrow x_c^{2}$. Thus $f(x_n) \to f(x_c)$. So $f$ is continuous for all $x_c \in\mathbb{R}$.

    Alternatively, to use the $\epsilon-\delta$ property, choose $\epsilon>0$, and fix $x_0\in\mathbb{R}$. Then
    $$|f(x)-f(x_0)|=|x^2-x_0^2|=|x-x_0|\cdot|x+x_0|.$$
    We want to bound $|x+x_0|$. If $|x-x_{0}|<1$, then $|x|-|x_0| \le |x-x_0| < 1$, so $|x| < |x_0|+1$.
    Then $|x+x_{0}|\leq|x|+|x_{0}| < (|x_{0}|+1)+|x_{0}| = 2|x_{0}|+1$.
    Let $M_0 = 2|x_0|+1$.
    Pick $\delta=\min\left\{1, \frac{\epsilon}{M_0}\right\}$ (if $M_0=0$, i.e. $x_0=0$ and $M_0=1$, this is $\min\{1,\epsilon\}$). Assume $M_0 \ge 1$.
    Then if $|x-x_{0}|<\delta$, it implies $|x-x_0|<1$ (so $|x+x_0|<M_0$) and $|x-x_0|<\frac{\epsilon}{M_0}$.
    Thus,
    $$|f(x)-f(x_0)| = |x-x_0||x+x_0| < \left(\frac{\epsilon}{M_0}\right) M_0 = \epsilon.$$
    Hence $f$ is continuous at $x_{0}$. Since $x_{0}$ is arbitrary, $f$ is continuous on $\mathbb{R}$.

3.  Let $f$ be a twice differentiable function defined on the closed interval $[0,1]$. Suppose $r,s,t\in[0,1]$ are defined so that $r<s<t$ and $f(r)=f(s)=f(t)=0$. Prove that there exists an $x\in(0,1)$ such that $f^{\prime\prime}(x)=0$.

    **Solution:**
    Since $f(r)=f(s)=0$ and $f$ is differentiable on $[0,1]$ (and thus continuous on $[r,s]$ and differentiable on $(r,s)$), by Rolle's Theorem, there exists a $c\in(r,s)$ such that $f'(c)=0$.
    Similarly, since $f(s)=f(t)=0$, by Rolle's Theorem, there exists a $d\in(s,t)$ such that $f'(d)=0$.
    Since $r<c<s<d<t$, we have $c < d$.
    Now consider the function $f'(x)$ on the interval $[c,d]$. We know $f'(c)=0$ and $f'(d)=0$. Since $f$ is twice differentiable, $f'$ is differentiable on $[0,1]$ (and thus continuous on $[c,d]$ and differentiable on $(c,d)$).
    By Rolle's Theorem applied to $f'$ on $[c,d]$, there exists an $x \in (c,d)$ such that $(f')'(x)=0$, which means $f''(x)=0$.
    Since $r,s,t \in [0,1]$ and $r<c<x<d<t$, we have $0 \le r < x < t \le 1$. Thus $x \in (r,t)$. If $r=0$ and $t=1$, then $x \in (0,1)$. In general, $(c,d) \subset (r,t) \subseteq (0,1)$ if $r,s,t$ are within $(0,1)$ or if $r=0, t=1$.
    Given $r,s,t \in [0,1]$ and $r<s<t$.
    The interval $(c,d)$ is a subinterval of $(r,t)$. Since $0 \le r < t \le 1$, then $(r,t) \subseteq [0,1]$. If $r>0$ or $t<1$, then $(r,t) \subset (0,1)$ is not guaranteed.
    However $x \in (c,d) \Rightarrow r<c<x<d<t$. So $x \in (r,t)$. Since $r,s,t \in [0,1]$, it implies $x \in (0,1)$ is not necessarily true if $r=0$ or $t=1$.
    The question asks for $x \in (0,1)$.
    Since $0 \le r < s < t \le 1$.
    $c \in (r,s) \implies c > r \ge 0$.
    $d \in (s,t) \implies d < t \le 1$.
    So $0 < c < d < 1$ is possible if $r>0$ and $t<1$.
    If $r=0$, then $c \in (0,s)$. If $t=1$, then $d \in (s,1)$.
    The interval $(c,d)$ is within $(r,t)$. As $0 \le r < t \le 1$, $x \in (c,d) \implies x \in (r,t)$.
    If $r=0$ and $t=1$, then $x \in (0,1)$.
    If $r>0$, then $x>c>r>0$. If $t<1$, then $x<d<t<1$.
    So $x \in (0,1)$ is correct because $x$ is strictly between $c$ and $d$, and $c,d$ are strictly between $r$ and $t$. $r \ge 0, t \le 1$.
    $0 \le r < c < x < d < t \le 1$. This implies $x \in (0,1)$ unless $r=c=x=0$ or $t=d=x=1$, which are not possible as $c \in (r,s)$ etc.
    So $x \in (0,1)$ follows.

4.  (a) Suppose that $\sum_{n=0}^{\infty}a_{n}$ converges to a limit $L$. Define a sequence $(b_{n})$ according to $b_{n}=a_{2n}+a_{2n+1}$ for $n\in\mathbb{N}\cup\{0\}$. Prove that $\sum_{n=0}^{\infty}b_{n}$ converges.
    (b) Construct an example of a series $\sum_{n=0}^{\infty}a_{n}$ that diverges, but that if $(b_{n})$ is defined as above, then $\sum_{n=0}^{\infty}b_{n}$ converges.

    **Solution:**
    (a) Let $S_k = \sum_{j=0}^k a_j$ be the $k$-th partial sum of $\sum a_n$. We are given $\lim_{k\to\infty} S_k = L$.
    Let $T_m = \sum_{j=0}^m b_j$ be the $m$-th partial sum of $\sum b_n$.
    Then $T_m = \sum_{j=0}^m (a_{2j}+a_{2j+1}) = (a_0+a_1) + (a_2+a_3) + \dots + (a_{2m}+a_{2m+1})$.
    So $T_m = \sum_{j=0}^{2m+1} a_j = S_{2m+1}$.
    Since $\lim_{k\to\infty} S_k = L$, any subsequence of $(S_k)$ must also converge to $L$.
    The sequence $(S_{2m+1})$ is a subsequence of $(S_k)$.
    Therefore, $\lim_{m\to\infty} T_m = \lim_{m\to\infty} S_{2m+1} = L$.
    Hence, $\sum_{n=0}^{\infty}b_{n}$ converges (to $L$).

    (b) Let $a_n=(-1)^n$.
    The series $\sum_{n=0}^{\infty}a_{n} = 1 - 1 + 1 - 1 + \dots$.
    The partial sums are $S_0=1, S_1=0, S_2=1, S_3=0, \ldots$. This sequence of partial sums $(1,0,1,0,\dots)$ diverges.
    So $\sum_{n=0}^{\infty}a_{n}$ diverges.
    Now define $b_{n}=a_{2n}+a_{2n+1}$.
    $b_n = (-1)^{2n} + (-1)^{2n+1} = 1 + (-1) = 0$ for all $n \ge 0$.
    The series $\sum_{n=0}^{\infty}b_{n} = \sum_{n=0}^{\infty}0 = 0$. This series converges (to 0).

5.  Suppose $f$ is a real-valued continuous function on $\mathbb{R}$ and that $f(a)f(b)<0$ for some $a,b\in\mathbb{R}$ where $a<b$. Prove that there exists an $x\in(a,b)$ such that $f(x)=0$.

    **Solution:**
    The condition $f(a)f(b)<0$ means that $f(a)$ and $f(b)$ have opposite signs.
    There are two cases:
    Case 1: $f(a) < 0$ and $f(b) > 0$.
    Case 2: $f(a) > 0$ and $f(b) < 0$.
    Since $f$ is a continuous function on $\mathbb{R}$, it is also continuous on the closed interval $[a,b]$.
    In Case 1, $f(a) < 0 < f(b)$. By the Intermediate Value Theorem, there exists an $x \in (a,b)$ such that $f(x)=0$.
    In Case 2, $f(b) < 0 < f(a)$. By the Intermediate Value Theorem, there exists an $x \in (a,b)$ such that $f(x)=0$.
    In both cases, such an $x$ exists.

6.  Let $f$ be a real-valued function defined on an interval $[0,b]$ as
    $$f(x)=\begin{cases}x & \quad \mathrm{for~}x\in\mathbb{Q},\\0 & \quad \mathrm{for~}x\notin\mathbb{Q}.\end{cases}$$
    Consider a partition $P=\{0=t_{0}<t_{1}<\ldots<t_{n}=b\}$. What are the upper and lower Darboux sums $U(f,P)$ and $L(f,P)$? Is $f$ integrable on $[0,b]$?

    **Solution:**
    Let $P=\{0=t_{0}<t_{1}<\ldots<t_{n}=b\}$ be a partition of $[0,b]$.
    For any subinterval $[t_{k-1},t_k]$ (where $t_k > t_{k-1}$):
    Since irrational numbers are dense in $\mathbb{R}$, any interval $[t_{k-1},t_k]$ contains irrational numbers. For any irrational $y \in [t_{k-1},t_k]$, $f(y)=0$. Thus, $m_k = \inf_{x\in[t_{k-1},t_k]} f(x) = 0$.
    Since rational numbers are dense in $\mathbb{R}$, for any subinterval $[t_{k-1},t_k]$, and for any $\epsilon > 0$, there is a rational number $q \in (t_k-\epsilon, t_k] \cap [t_{k-1},t_k]$. For such $q$, $f(q)=q$. The supremum of such $q$ values in $[t_{k-1},t_k]$ is $t_k$. Thus, $M_k = \sup_{x\in[t_{k-1},t_k]} f(x) = t_k$.

    The lower Darboux sum is:
    $$L(f,P)=\sum_{k=1}^n m_k(t_k-t_{k-1}) = \sum_{k=1}^n 0 \cdot (t_k-t_{k-1}) = 0.$$
    The upper Darboux sum is:
    $$U(f,P)=\sum_{k=1}^n M_k(t_k-t_{k-1}) = \sum_{k=1}^n t_k(t_k-t_{k-1}).$$
    For $f$ to be integrable on $[0,b]$, we require $\sup_P L(f,P) = \inf_P U(f,P)$.
    We have $\sup_P L(f,P) = 0$.
    For the upper sums, consider $b>0$.
    _we construct the telescoping series_:
    $$
    \begin{align*} U(f,P) &= \sum_{k=1}^{n}t_{k}(t_{k}-t_{k-1}) \\ &\geq \sum_{k=1}^{n} t_{k-1}(t_{k}-t_{k-1}) \quad \text{(This step in original solution was different, let's follow the provided text.)} \\
    \text{The solution's argument was: } U(f,P) &= \sum_{k=1}^{n}t_{k}(t_{k}-t_{k-1}) \\ &\geq \sum_{k=1}^{n}\frac{(t_{k}+t_{k-1})}{2}(t_{k}-t_{k-1}) \quad (\text{since } t_k \ge (t_k+t_{k-1})/2 \text{ as } t_k \ge t_{k-1}) \\ &= \frac{1}{2}\sum_{k=1}^{n}(t_{k}^{2}-t_{k-1}^{2}) \\ &= \frac{1}{2}(t_{n}^{2}-t_{0}^{2}) = \frac{b^{2}-0^2}{2}=\frac{b^{2}}{2}. \end{align*}
    $$
    Thus, for any partition $P$, $U(f,P) \ge \frac{b^2}{2}$.
    So, $\inf_P U(f,P) \ge \frac{b^2}{2}$.
    If $b>0$, then $\frac{b^2}{2} > 0$.
    Since $\sup_P L(f,P) = 0$ and $\inf_P U(f,P) \ge \frac{b^2}{2}$, these are not equal if $b>0$.
    **Thus, $f$ is not integrable on $[0,b]$ if $b>0$. If $b=0$, the interval is $[0,0]$, $f(0)=0$. The integral $\int_0^0 f(x)dx = 0$, so $f$ is integrable.**

    > **Caution**
    > Note that we need to discuss the $b=0$ case!

7.  Let $f$ be a *decreasing function* defined on $[1,\infty)$, where $f(x)\geq0$ for all $x\in[1,\infty)$. Prove that $\int_{1}^{\infty}f(x)dx$ converges if and only if $\sum_{n=1}^{\infty}f(n)$ converges. [This is essentially a question asking you to prove a general form of the integral test.]

    **Solution:**
    Since $f$ is decreasing and $f(x) \ge 0$:
    For any integer $n \ge 1$, on the interval $[n, n+1]$, because $f$ is decreasing, we have:
    $f(n+1) \le f(x) \le f(n)$ for all $x \in [n, n+1]$.
    Integrating over $[n, n+1]$:
    $$\int_n^{n+1} f(n+1)dx \le \int_n^{n+1} f(x)dx \le \int_n^{n+1} f(n)dx$$
    $$f(n+1)( (n+1)-n ) \le \int_n^{n+1} f(x)dx \le f(n)( (n+1)-n )$$
    $$f(n+1) \le \int_n^{n+1} f(x)dx \le f(n).$$
    Summing these inequalities from $n=1$ to $N-1$ (for some integer $N>1$):
    $$\sum_{n=1}^{N-1} f(n+1) \le \sum_{n=1}^{N-1} \int_n^{n+1} f(x)dx \le \sum_{n=1}^{N-1} f(n)$$
    Let $k=n+1$ in the leftmost sum. When $n=1, k=2$. When $n=N-1, k=N$.
    $$\sum_{k=2}^{N} f(k) \le \int_1^{N} f(x)dx \le \sum_{n=1}^{N-1} f(n).$$

    ($\Rightarrow$) Suppose $\sum_{n=1}^{\infty}f(n)$ converges. Let its sum be $S$. Since $f(n) \ge 0$, the partial sums $\sum_{n=1}^{N-1}f(n)$ are increasing and bounded by $S$.
    From the right inequality, $\int_1^{N} f(x)dx \le \sum_{n=1}^{N-1} f(n) \le S$.
    Since $f(x) \ge 0$, the function $G(N) = \int_1^N f(x)dx$ is non-decreasing (increasing if $f(x)>0$ somewhere).
    Since $G(N)$ is non-decreasing and bounded above by $S$, $\lim_{N\to\infty} G(N) = \int_{1}^{\infty}f(x)dx$ converges.
    _The idea is to prove $\int_{1}^{N}f(x) \, dx$ is a monotonic increasing bounded sequence (function of N)._

    ($\Leftarrow$) Suppose $\int_{1}^{\infty}f(x)dx$ converges. Let its value be $L$. Since $f(x) \ge 0$, $\int_1^N f(x)dx \le L$ for all $N$.
    The partial sums $S_N = \sum_{k=1}^{N} f(k)$ form a non-decreasing sequence (since $f(k) \ge 0$).
    From the left inequality: $\sum_{k=2}^{N} f(k) \le \int_1^{N} f(x)dx$.
    So, $S_N - f(1) = \sum_{k=2}^{N} f(k) \le \int_1^{N} f(x)dx \le L$.
    Thus, $S_N \le L + f(1)$.
    The sequence of partial sums $(S_N)$ is non-decreasing and bounded above by $L+f(1)$.
    _An increasing and bounded above sequence converges_. Thus, $\sum_{n=1}^{\infty}f(n)$ converges.

    Therefore, $\int_{1}^{\infty}f(x)dx$ converges if and only if $\sum_{n=1}^{\infty}f(n)$ converges.

8.  Consider the function defined for $x,y\in\mathbb{R}$ as
    $$d(x,y)=\begin{cases}1 & \mathrm{if}\:x\neq y,\\0 & \mathrm{if}\:x=y.\end{cases}$$
    (a) Prove that $d$ defines a metric on $\mathbb{R}$.
    (b) What is the neighborhood of radius $1/2$ centered on $0$?
    (c) Consider an arbitrary set $S\subseteq\mathbb{R}$. Is $S$ open? Is $S$ compact?

    **Solution:**
    (a) To prove that $d$ is a metric, we check the metric properties:
    M1. **Non-negativity and identity of indiscernibles**:
        $d(x,y) \ge 0$ for all $x,y \in \mathbb{R}$ (since its values are 0 or 1).
        $d(x,y) = 0 \iff x=y$, by definition.
    M2. **Symmetry**:
        If $x=y$, then $d(x,y)=0$ and $d(y,x)=0$.
        If $x \neq y$, then $d(x,y)=1$ and $d(y,x)=1$.
        So, $d(x,y) = d(y,x)$ for all $x,y \in \mathbb{R}$.
    M3. **Triangle inequality**: $d(x,z) \le d(x,y) + d(y,z)$ for all $x,y,z \in \mathbb{R}$.
        Case 1: $x=z$. Then $d(x,z)=0$. Since $d(x,y) \ge 0$ and $d(y,z) \ge 0$, their sum $d(x,y)+d(y,z) \ge 0$. So $0 \le d(x,y)+d(y,z)$ holds.
        Case 2: $x \neq z$. Then $d(x,z)=1$.
            Subcase 2.1: $y=x$. Then $d(x,y)=0$. Since $x \neq z$, we have $y \neq z$, so $d(y,z)=1$. Then $d(x,y)+d(y,z) = 0+1=1$. The inequality $1 \le 1$ holds.
            Subcase 2.2: $y=z$. Then $d(y,z)=0$. Since $x \neq z$, we have $x \neq y$, so $d(x,y)=1$. Then $d(x,y)+d(y,z) = 1+0=1$. The inequality $1 \le 1$ holds.
            Subcase 2.3: $y \neq x$ and $y \neq z$. Then $d(x,y)=1$ and $d(y,z)=1$. Then $d(x,y)+d(y,z) = 1+1=2$. The inequality $1 \le 2$ holds.
    Since all properties are satisfied, $d$ is a metric on $\mathbb{R}$. (This is the discrete metric).

    (b) The neighborhood of radius $1/2$ centered on $0$, denoted $N_{1/2}(0)$, is the set
    $$N_{1/2}(0) = \{x\in\mathbb{R} : d(0,x) < 1/2\}.$$
    By definition of $d$:
    $d(0,x)=0$ if $x=0$.
    $d(0,x)=1$ if $x \neq 0$.
    The condition $d(0,x) < 1/2$ is only satisfied if $d(0,x)=0$, which means $x=0$.
    So, $N_{1/2}(0) = \{0\}$.

    **(c) Consider an arbitrary set $S \subseteq \mathbb{R}$. $S$ 是否是开集？$S$ 是否是紧致集？**

    **$S$ 是否为开集?**
    一个集合 $S$ 是开集，如果对于 $S$ 中的任意一点 $x$，都存在一个以 $x$ 为中心，半径为 $r>0$ 的开球 $N_r(x)$，使得 $N_r(x) \subseteq S$。
    对于离散度量空间中的任意 $x \in S$，考虑半径 $r=1/2$ 的开球 $N_{1/2}(x)$.
    $$N_{1/2}(x) = \{y \in \mathbb{R} : d(x,y) < 1/2\} = \{x\}.$$
    因为 $x \in S$，所以 $\{x\} \subseteq S$。
    这意味着 $S$ 中的每一个点都是 $S$ 的内点。因此，在离散度量下，$\mathbb{R}$ 的任何子集 $S$ 都是开集。

    **$S$ 是否为紧致集（使用序列紧致性的方法）：**

    在度量空间中，一个集合是紧致的当且仅当它是序列紧致的。一个集合 $S$ 是序列紧致的，如果 $S$ 中的任意序列都包含一个收敛于 $S$ 中某点的子序列。

    首先，我们回顾在离散度量空间 $d(x,y)$（即当 $x=y$ 时 $d(x,y)=0$，当 $x \neq y$ 时 $d(x,y)=1$）中序列收敛的特性：
    一个序列 $\{x_n\}$ 收敛到 $x$，当且仅当存在一个自然数 $N_0$，使得对于所有 $n > N_0$，都有 $x_n = x$。换句话说，序列必须“最终恒定”才收敛。这是因为如果取 $\epsilon = 1/2$，则 $d(x_n, x) < \epsilon$ 蕴含了 $d(x_n, x) = 0$，即 $x_n = x$。

    现在我们分两种情况讨论集合 $S$ 的紧致性：

    1.  **情况一：$S$ 是一个有限集。**
        假设 $S = \{s_1, s_2, \ldots, s_m\}$，其中 $m$ 是一个正整数。
        令 $\{x_n\}_{n=1}^\infty$ 为 $S$ 中的任意一个序列。由于 $S$ 中只有 $m$ 个元素，而序列有无限项，根据鸽巢原理，至少 $S$ 中的某一个元素（不妨设为 $s_k \in S$）必定在序列 $\{x_n\}$ 中出现无限多次。
        因此，我们可以从序列 $\{x_n\}$ 中挑选出一个子序列 $\{x_{n_j}\}$，使得这个子序列的每一项都等于 $s_k$。即 $x_{n_j} = s_k$ 对所有 $j$ 成立。
        这个子序列 $(s_k, s_k, s_k, \ldots)$ 是一个常数序列，它显然收敛到 $s_k$，并且 $s_k \in S$。
        由于 $S$ 中的任意序列都包含一个收敛于 $S$ 中某点的子序列，所以当 $S$ 是有限集时，$S$ 是序列紧致的，因此 $S$ 是紧致的。

    2.  **情况二：$S$ 是一个无限集。**
        如果 $S$ 是无限集，我们可以从 $S$ 中选取一个各项互不相同的序列 $\{x_n\}_{n=1}^\infty$（即对于 $i \neq j$，有 $x_i \neq x_j$）。
        现在考虑这个序列 $\{x_n\}$ 的任意一个子序列 $\{x_{n_j}\}_{j=1}^\infty$。由于原序列 $\{x_n\}$ 的各项互不相同，其子序列 $\{x_{n_j}\}$ 的各项也必定互不相同。
        因为一个序列在离散度量下收敛的必要条件是它必须最终恒定，而各项互不相同的序列（例如 $\{x_{n_j}\}$）不可能是最终恒定的。
        所以，子序列 $\{x_{n_j}\}$ 不会收敛。
        这意味着，如果 $S$ 是无限集，我们找到了 $S$ 中的一个序列（即 $\{x_n\}$），它没有任何收敛的子序列。因此，当 $S$ 是无限集时，$S$ 不是序列紧致的，所以 $S$ 不是紧致的。

    **结论：**
    集合 $S \subseteq \mathbb{R}$ 在离散度量下是紧致的当且仅当 $S$ 是一个有限集。

9.  Let $\mathbf{x}=(x_{1},x_{2})$ and $\mathbf{y}=(y_{1},y_{2})$ be in $\mathbb{R}^{2}$. Consider the function
    $$d(\mathbf{x},\mathbf{y})=|x_1-y_1|+|x_2-y_2|.$$
    (a) Prove that $d$ is a metric on $\mathbb{R}^{2}$.
    (b) Compute and sketch the neighborhood of radius 1 at $(0,0)$.

    **Solution:**
    (a) To prove $d$ is a metric on $\mathbb{R}^2$:
    M1. **Non-negativity and identity of indiscernibles**:
        Since $|x_1-y_1| \ge 0$ and $|x_2-y_2| \ge 0$, it follows that $d(\mathbf{x},\mathbf{y}) = |x_1-y_1|+|x_2-y_2| \ge 0$.
        $d(\mathbf{x},\mathbf{y})=0 \iff |x_1-y_1|+|x_2-y_2|=0$. Since absolute values are non-negative, this sum is zero if and only if each term is zero.
        So, $|x_1-y_1|=0$ and $|x_2-y_2|=0$, which implies $x_1=y_1$ and $x_2=y_2$. Thus, $\mathbf{x}=\mathbf{y}$.
    M2. **Symmetry**:
        $$d(\mathbf{x},\mathbf{y}) = |x_1-y_1|+|x_2-y_2| = |y_1-x_1|+|y_2-x_2| = d(\mathbf{y},\mathbf{x}).$$
    M3. **Triangle inequality**: For $\mathbf{z}=(z_1, z_2) \in \mathbb{R}^2$, we need to show $d(\mathbf{x},\mathbf{z}) \le d(\mathbf{x},\mathbf{y}) + d(\mathbf{y},\mathbf{z})$.
    $$
        \begin{align*}
        d(\mathbf{x},\mathbf{y}) + d(\mathbf{y},\mathbf{z}) &= (|x_1-y_1|+|x_2-y_2|) + (|y_1-z_1|+|y_2-z_2|) \\
        &= (|x_1-y_1|+|y_1-z_1|) + (|x_2-y_2|+|y_2-z_2|)
        \end{align*}
        $$
        By the triangle inequality for real numbers ($|a+b| \le |a|+|b|$, or $|u-w| \le |u-v|+|v-w|$):
        $|x_1-z_1| = |(x_1-y_1)+(y_1-z_1)| \le |x_1-y_1|+|y_1-z_1|$.
        $|x_2-z_2| = |(x_2-y_2)+(y_2-z_2)| \le |x_2-y_2|+|y_2-z_2|$.
        Therefore,
        $$
        \begin{align*}
        d(\mathbf{x},\mathbf{y}) + d(\mathbf{y},\mathbf{z}) &\ge |x_1-z_1| + |x_2-z_2| \\
        &= d(\mathbf{x},\mathbf{z}).
        \end{align*}
    $$
    All properties are satisfied, so $d$ is a metric on $\mathbb{R}^2$. (This is the taxicab or Manhattan metric).

    (b) The neighborhood of radius 1 at $(0,0)$ is $N_1((0,0)) = \{\mathbf{x} \in \mathbb{R}^2 : d(\mathbf{x},(0,0)) < 1\}$.
    Let $\mathbf{x}=(x_1,x_2)$. Then $d(\mathbf{x},(0,0)) = |x_1-0| + |x_2-0| = |x_1| + |x_2|$.
    So we want to sketch the set of points $(x_1,x_2)$ such that $|x_1| + |x_2| < 1$.
    Consider the four quadrants:
    1.  $x_1 \ge 0, x_2 \ge 0$: $x_1 + x_2 < 1$. This is the region below the line $x_2 = 1-x_1$ in the first quadrant. Boundary points on axes are $(1,0)$ and $(0,1)$.
    2.  $x_1 < 0, x_2 \ge 0$: $-x_1 + x_2 < 1$. This is the region below the line $x_2 = 1+x_1$ in the second quadrant. Boundary points on axes are $(-1,0)$ and $(0,1)$.
    3.  $x_1 < 0, x_2 < 0$: $-x_1 - x_2 < 1 \Rightarrow x_1+x_2 > -1$. This is the region above the line $x_2 = -1-x_1$ in the third quadrant. Boundary points on axes are $(-1,0)$ and $(0,-1)$.
    4.  $x_1 \ge 0, x_2 < 0$: $x_1 - x_2 < 1 \Rightarrow x_2 > x_1-1$. This is the region above the line $x_2 = x_1-1$ in the fourth quadrant. Boundary points on axes are $(1,0)$ and $(0,-1)$.
    The region is a square (a diamond shape rotated by 45 degrees) with vertices at $(1,0), (0,1), (-1,0), (0,-1)$. The interior of this square is the neighborhood.
    ![[Pasted image 20250510112715.png]]
    (The solution text refers to Fig. 1 for the plot.)

10. Consider a function $f$ defined on $\mathbb{R}$ which satisfies
    $$|f(x)-f(y)|\le(x-y)^2$$
    for all $x,y\in\mathbb{R}$. Prove that $f$ is a constant function.

    **Solution:**
    From the given condition, if $x \neq y$, we can divide by $|x-y|$:
    $$\frac{|f(x)-f(y)|}{|x-y|} \le \frac{(x-y)^2}{|x-y|} = |x-y|$$
    This means
    $$\left|\frac{f(x)-f(y)}{x-y}\right| \le |x-y|.$$
    To check if $f$ is differentiable at an arbitrary point $y_0 \in \mathbb{R}$, we consider the limit of the difference quotient:
    $$f'(y_0) = \lim_{x\to y_0} \frac{f(x)-f(y_0)}{x-y_0}.$$
    From the inequality derived, for $x \neq y_0$:
    $$-|x-y_0| \le \frac{f(x)-f(y_0)}{x-y_0} \le |x-y_0|.$$
    As $x \to y_0$, $|x-y_0| \to 0$. By the Squeeze Theorem,
    $$\lim_{x\to y_0} \frac{f(x)-f(y_0)}{x-y_0} = 0.$$
    This means that $f$ is differentiable at any point $y_0 \in \mathbb{R}$, and $f'(y_0)=0$ for all $y_0 \in \mathbb{R}$.
    A function whose derivative is zero everywhere on $\mathbb{R}$ must be a constant function.
    To show this formally: Let $a, b \in \mathbb{R}$ with $a < b$. Since $f$ is differentiable on $\mathbb{R}$, it is continuous on $[a,b]$ and differentiable on $(a,b)$. By the Mean Value Theorem, there exists a $c \in (a,b)$ such that
    $$f'(c) = \frac{f(b)-f(a)}{b-a}.$$
    Since $f'(c)=0$, we have $\frac{f(b)-f(a)}{b-a} = 0$. As $b-a \neq 0$, this implies $f(b)-f(a)=0$, so $f(b)=f(a)$.
    Since this holds for any $a,b \in \mathbb{R}$, $f$ must be a constant function.

11. Suppose that $f$ is differentiable on $\mathbb{R}$, and that $2\leq f^{\prime}(x)\leq3$ for $x\in\mathbb{R}$. If $f(0)=0$ prove that $2x\leq f(x)\leq3x$ for all $x\geq0$.

    **Solution:**
    Case 1: $x > 0$.
    Since $f$ is differentiable on $\mathbb{R}$, it is continuous on $[0,x]$ and differentiable on $(0,x)$.
    By the Mean Value Theorem, there exists a $c \in (0,x)$ such that
    $$f'(c) = \frac{f(x)-f(0)}{x-0}.$$
    Given $f(0)=0$, this simplifies to
    $$f'(c) = \frac{f(x)}{x}.$$
    We are also given that $2 \le f'(y) \le 3$ for all $y \in \mathbb{R}$. In particular, for our $c \in (0,x)$, we have $2 \le f'(c) \le 3$.
    Substituting $f'(c) = f(x)/x$, we get
    $$2 \le \frac{f(x)}{x} \le 3.$$
    Since $x > 0$, we can multiply all parts of the inequality by $x$ without changing the direction of the inequalities:
    $$2x \le f(x) \le 3x.$$
    This holds for all $x>0$.

    Case 2: $x=0$.
    We need to check if $2(0) \le f(0) \le 3(0)$. This simplifies to $0 \le 0 \le 0$.
    Since we are given $f(0)=0$, this is true.
    Thus, $2x \le f(x) \le 3x$ for all $x \ge 0$.

    > **Caution**
    > You see the rigor to check every possible cases? ($x>0$ and $x=0$)

12. Show that if $f$ is integrable on $[a,b]$, then $f$ is integrable on every interval $[c,d]\subseteq [a,b]$.

    **Solution:**
    Suppose $f$ is integrable on $[a,b]$. By definition, this means that for every $\epsilon > 0$, there exists a partition $P$ of $[a,b]$ such that $U(f,P) - L(f,P) < \epsilon$.
    Let $[c,d]$ be any subinterval of $[a,b]$, so $a \le c \le d \le b$. We want to show $f$ is integrable on $[c,d]$.
    Let $\epsilon > 0$ be given. Since $f$ is integrable on $[a,b]$, there exists a partition $P = \{x_0, x_1, \ldots, x_n\}$ of $[a,b]$ (where $a=x_0 < x_1 < \ldots < x_n=b$) such that
    $$U(f,P) - L(f,P) < \epsilon.$$
    Consider the refined partition $P' = P \cup \{c,d\}$. $P'$ is a partition of $[a,b]$ that includes the points $c$ and $d$. Since $P'$ is a refinement of $P$, we have
    $$U(f,P') - L(f,P') \le U(f,P) - L(f,P) < \epsilon.$$
    Now, let $P_{[c,d]}$ be the set of points of $P'$ that are in the interval $[c,d]$. That is, $P_{[c,d]} = \{t_j \in P' : c \le t_j \le d\}$, arranged in increasing order, starting with $c$ and ending with $d$. So $P_{[c,d]}$ is a partition of $[c,d]$. Let $P_{[c,d]} = \{t_0, t_1, \ldots, t_m\}$ where $c=t_0 < t_1 < \ldots < t_m=d$.
    The sum $U(f, P_{[c,d]}) - L(f, P_{[c,d]})$ is given by
    $$U(f, P_{[c,d]}) - L(f, P_{[c,d]}) = \sum_{j=1}^m (M(f,[t_{j-1},t_j]) - m(f,[t_{j-1},t_j]))(t_j - t_{j-1}).$$
    Each term $(M(f,[t_{j-1},t_j]) - m(f,[t_{j-1},t_j]))(t_j - t_{j-1})$ is non-negative.
    The sum $U(f,P') - L(f,P')$ is a sum of such terms over all subintervals defined by $P'$. The terms forming $U(f, P_{[c,d]}) - L(f, P_{[c,d]})$ are a subset of (or equal to some of) the terms forming $U(f,P') - L(f,P')$.
    More formally,
    $$U(f, P_{[c,d]}) - L(f, P_{[c,d]}) = \sum_{t_j \in P', [t_{j-1}, t_j] \subseteq [c,d]} (M_j - m_j)(t_j - t_{j-1}).$$
    This sum is less than or equal to the sum over all subintervals of $P'$ covering $[a,b]$:
    $$U(f, P_{[c,d]}) - L(f, P_{[c,d]}) \le U(f,P') - L(f,P') < \epsilon.$$
    Thus, for any $\epsilon > 0$, there exists a partition $P_{[c,d]}$ of $[c,d]$ such that $U(f, P_{[c,d]}) - L(f, P_{[c,d]}) < \epsilon$.
    This means $f$ is integrable on $[c,d]$.

13. (a) Suppose $r$ is irrational. Prove that $r^{1/3}$ and $r+1$ are irrational also.
    (b) Prove that $(5+\sqrt{2})^{1/3}+1$ is irrational.

    **Solution:**
    (a) Proof by contradiction.
    To prove $r^{1/3}$ is irrational:
    Assume, for the sake of contradiction, that $r^{1/3}$ is rational.
    Then $r^{1/3} = \frac{p}{q}$ for some integers $p,q$ with $q \neq 0$.
    Cubing both sides, we get $r = (r^{1/3})^3 = \left(\frac{p}{q}\right)^3 = \frac{p^3}{q^3}$.
    Since $p$ and $q$ are integers, $p^3$ and $q^3$ are integers. Also, since $q \neq 0$, $q^3 \neq 0$.
    Thus, $r = \frac{p^3}{q^3}$ is a ratio of two integers with a non-zero denominator, which means $r$ is rational.
    This contradicts the given information that $r$ is irrational.
    Therefore, our assumption that $r^{1/3}$ is rational must be false. So, $r^{1/3}$ is irrational.

    To prove $r+1$ is irrational:
    Assume, for the sake of contradiction, that $r+1$ is rational.
    Then $r+1 = \frac{a}{b}$ for some integers $a,b$ with $b \neq 0$.
    Then $r = \frac{a}{b} - 1 = \frac{a-b}{b}$.
    Since $a$ and $b$ are integers, $a-b$ is an integer. Since $b \neq 0$, $r = \frac{a-b}{b}$ is rational.
    This contradicts the given information that $r$ is irrational.
    Therefore, our assumption that $r+1$ is rational must be false. So, $r+1$ is irrational.

    (b) Let $X = (5+\sqrt{2})^{1/3}+1$. We want to prove $X$ is irrational.
    First, let's show that $r_0 = 5+\sqrt{2}$ is irrational.
    Assume $5+\sqrt{2}$ is rational. Then $5+\sqrt{2} = k$ for some rational number $k$.
    This implies $\sqrt{2} = k-5$. Since $k$ is rational and $5$ is rational, $k-5$ is rational.
    This means $\sqrt{2}$ is rational, which is a known contradiction ( $\sqrt{2}$ is irrational).
    So, $r_0 = 5+\sqrt{2}$ is irrational.

    Now let $y = (5+\sqrt{2})^{1/3} = r_0^{1/3}$. Since $r_0$ is irrational, by part (a), $y = r_0^{1/3}$ is irrational.
    Finally, consider $X = y+1$. Since $y$ is irrational, by part (a) (if $r$ is irrational, then $r+1$ is irrational; here $y$ takes the role of $r$), $X = y+1$ is irrational.
    Therefore, $(5+\sqrt{2})^{1/3}+1$ is irrational.

14. By using L'Hopital's rule, or otherwise, evaluate.
    $$\lim_{x\to0}\frac{x}{1-e^{-x^2-3x}},\quad\lim_{x\to0}\left(\frac{1}{\sin x}-\frac{1}{x}\right),\quad\lim_{x\to0}\frac{x^3}{\sin x-x}.$$

    **Solution:**
    For the first limit: $\lim_{x\to0}\frac{x}{1-e^{-x^2-3x}}$.
    As $x\to0$, the numerator $x \to 0$.
    As $x\to0$, the denominator $1-e^{-x^2-3x} \to 1-e^{0} = 1-1 = 0$.
    This is an indeterminate form $\frac{0}{0}$, so we can apply L'Hopital's Rule.
    $$\lim_{x\to0}\frac{\frac{d}{dx}(x)}{\frac{d}{dx}(1-e^{-x^2-3x})} = \lim_{x\to0}\frac{1}{-e^{-x^2-3x}(-2x-3)} = \lim_{x\to0}\frac{1}{(2x+3)e^{-x^2-3x}}.$$
    Plugging in $x=0$:
    $$\frac{1}{(2(0)+3)e^{0}} = \frac{1}{3 \cdot 1} = \frac{1}{3}.$$

    For the second limit: $\lim_{x\to0}\left(\frac{1}{\sin x}-\frac{1}{x}\right)$.
    This is of the indeterminate form $\infty - \infty$ as $x\to0$. We combine the terms:
    $$\lim_{x\to0}\frac{x-\sin x}{x\sin x}.$$
    As $x\to0$, numerator $x-\sin x \to 0-0 = 0$.
    As $x\to0$, denominator $x\sin x \to 0 \cdot 0 = 0$.
    This is $\frac{0}{0}$, apply L'Hopital's Rule:
    $$\lim_{x\to0}\frac{\frac{d}{dx}(x-\sin x)}{\frac{d}{dx}(x\sin x)} = \lim_{x\to0}\frac{1-\cos x}{\sin x+x\cos x}.$$
    As $x\to0$, numerator $1-\cos x \to 1-1 = 0$.
    As $x\to0$, denominator $\sin x+x\cos x \to 0+0\cdot1 = 0$.
    This is $\frac{0}{0}$ again, apply L'Hopital's Rule:
    $$\lim_{x\to0}\frac{\frac{d}{dx}(1-\cos x)}{\frac{d}{dx}(\sin x+x\cos x)} = \lim_{x\to0}\frac{\sin x}{\cos x + (\cos x - x\sin x)} = \lim_{x\to0}\frac{\sin x}{2\cos x - x\sin x}.$$
    Plugging in $x=0$:
    $$\frac{\sin 0}{2\cos 0 - 0\sin 0} = \frac{0}{2\cdot1 - 0} = \frac{0}{2} = 0.$$

    For the third limit: $\lim_{x\to0}\frac{x^3}{\sin x-x}$.
    As $x\to0$, numerator $x^3 \to 0$.
    As $x\to0$, denominator $\sin x - x \to 0-0 = 0$.
    This is $\frac{0}{0}$, apply L'Hopital's Rule:
    $$\lim_{x\to0}\frac{\frac{d}{dx}(x^3)}{\frac{d}{dx}(\sin x-x)} = \lim_{x\to0}\frac{3x^2}{\cos x-1}.$$
    As $x\to0$, numerator $3x^2 \to 0$.
    As $x\to0$, denominator $\cos x-1 \to 1-1 = 0$.
    This is $\frac{0}{0}$ again, apply L'Hopital's Rule:
    $$\lim_{x\to0}\frac{\frac{d}{dx}(3x^2)}{\frac{d}{dx}(\cos x-1)} = \lim_{x\to0}\frac{6x}{-\sin x}.$$
    As $x\to0$, numerator $6x \to 0$.
    As $x\to0$, denominator $-\sin x \to 0$.
    This is $\frac{0}{0}$ again, apply L'Hopital's Rule:
    $$\lim_{x\to0}\frac{\frac{d}{dx}(6x)}{\frac{d}{dx}(-\sin x)} = \lim_{x\to0}\frac{6}{-\cos x}.$$
    Plugging in $x=0$:
    $$\frac{6}{-\cos 0} = \frac{6}{-1} = -6.$$

15. Let $a\in\mathbb{R}$. Consider the sequence $s_{n}$ defined as
    $$s_n=\begin{cases}a & \quad \mathrm{if}\:n\:\mathrm{is}\:\mathrm{odd},\\2^{-n} & \quad \mathrm{if}\:n\:\mathrm{is}\:\mathrm{even}.\end{cases}$$
    Compute $\limsup s_{n}$ and $\liminf s_n$. For what value of $a$ does $(s_{n})$ converge?

    **Solution:**
    The sequence $(s_n)$ has two subsequences whose terms make up the entire sequence:
    The subsequence of odd-indexed terms: $(s_{2k-1}) = (a, a, a, \ldots)$. This subsequence converges to $a$.
    The subsequence of even-indexed terms: $(s_{2k}) = (2^{-2}, 2^{-4}, 2^{-6}, \ldots)$. Since $2^{-2k} = (1/4)^k$, this subsequence converges to $0$ as $k \to \infty$.
    The set of subsequential limits of $(s_n)$ is $E = \{0, a\}$.
    Then, by definition:
    $\limsup s_n = \sup E = \sup \{0, a\} = \max(0,a)$.
    $\liminf s_n = \inf E = \inf \{0, a\} = \min(0,a)$.

    The sequence $(s_n)$ converges if and only if $\limsup s_n = \liminf s_n$.
    So we need $\max(0,a) = \min(0,a)$.
    This equality holds if and only if the two numbers in the set $\{0,a\}$ are the same, which means $a=0$.
    If $a=0$: $\max(0,0)=0$ and $\min(0,0)=0$. So $\limsup s_n = \liminf s_n = 0$. The sequence converges to 0.
    If $a>0$: $\max(0,a)=a$ and $\min(0,a)=0$. Since $a \neq 0$, $\limsup s_n \neq \liminf s_n$. The sequence diverges.
    If $a<0$: $\max(0,a)=0$ and $\min(0,a)=a$. Since $a \neq 0$, $\limsup s_n \neq \liminf s_n$. The sequence diverges.
    Therefore, $(s_n)$ converges if and only if $a=0$.

16. Consider the function $f:\mathbb{R}^{2}\to\mathbb{R}$ defined as
    $$f(x_1,x_2)=\frac{1}{x_1^2+x_2^2+1}.$$
    With respect to the usual Euclidean metrics on $\mathbb{R}$ and $\mathbb{R}^{2}$ prove that $f$ is continuous at $(0,0)$ and at $(0,1)$.

    **Solution:**
    Let $g(x_1,x_2) = x_1^2+x_2^2+1$. This is a polynomial in $x_1$ and $x_2$, and polynomials are continuous everywhere on $\mathbb{R}^2$.
    Let $h(y) = 1/y$. This function is continuous for all $y \neq 0$.
    The function $f(x_1,x_2)$ can be written as the composition $f(x_1,x_2) = h(g(x_1,x_2))$.
    The range of $g(x_1,x_2)$ is $[1, \infty)$, because $x_1^2 \ge 0$ and $x_2^2 \ge 0$, so $x_1^2+x_2^2+1 \ge 1$.
    Since $g(x_1,x_2)$ is always $\ge 1$, it is never zero. Thus, $h(y)$ is continuous for all values taken by $g(x_1,x_2)$.
    The composition of continuous functions is continuous.
    Since $g$ is continuous on $\mathbb{R}^2$ and $h$ is continuous on the range of $g$, $f = h \circ g$ is continuous on $\mathbb{R}^2$.
    Since $f$ is continuous on all of $\mathbb{R}^2$, it is continuous at any specific points in $\mathbb{R}^2$, including $(0,0)$ and $(0,1)$.

    (Alternatively, using $\epsilon-\delta$ for $(0,0)$):
    $f(0,0) = 1$. We want to show for any $\epsilon > 0$, there is $\delta > 0$ such that if $\sqrt{x_1^2+x_2^2} < \delta$, then $|f(x_1,x_2)-1| < \epsilon$.
    $$|f(x_1,x_2)-1| = \left|\frac{1}{x_1^2+x_2^2+1} - 1\right| = \left|\frac{1-(x_1^2+x_2^2+1)}{x_1^2+x_2^2+1}\right| = \frac{x_1^2+x_2^2}{x_1^2+x_2^2+1}.$$
    Since $x_1^2+x_2^2+1 > x_1^2+x_2^2$ (and $x_1^2+x_2^2+1 > 1$),
    $$\frac{x_1^2+x_2^2}{x_1^2+x_2^2+1} < \frac{x_1^2+x_2^2}{1} = x_1^2+x_2^2.$$
    If $\sqrt{x_1^2+x_2^2} < \delta$, then $x_1^2+x_2^2 < \delta^2$.
    We want $|f(x_1,x_2)-1| < \epsilon$. If we ensure $x_1^2+x_2^2 < \epsilon$, this will suffice.
    So, choose $\delta^2 = \epsilon$, i.e., $\delta = \sqrt{\epsilon}$.
    Then if $\sqrt{x_1^2+x_2^2} < \sqrt{\epsilon}$, we have $x_1^2+x_2^2 < \epsilon$.
    Then $|f(x_1,x_2)-1| = \frac{x_1^2+x_2^2}{x_1^2+x_2^2+1} \le x_1^2+x_2^2 < \epsilon$. So $f$ is continuous at $(0,0)$.
    (A similar $\epsilon-\delta$ argument can be made for $(0,1)$ as in the original provided solution text.)

17. (a) Calculate the improper integral
    $$\int_0^1x^{-p}\:dx$$
    for the cases when $0<p<1$ and $p>1$.
    (b) Prove that
    $$\int_0^\infty x^{-p}dx=\infty $$
    for all $p\in(0,\infty)$.

    **Solution:**
    (a) The integral $\int_0^1 x^{-p} dx$ is improper at $x=0$ if $p>0$.
    $$\int_0^1 x^{-p} dx = \lim_{c\to0^+} \int_c^1 x^{-p} dx.$$
    If $p \neq 1$:
    $$\int_c^1 x^{-p} dx = \left[ \frac{x^{-p+1}}{-p+1} \right]_c^1 = \frac{1^{-p+1}}{1-p} - \frac{c^{1-p}}{1-p} = \frac{1-c^{1-p}}{1-p}.$$
    Case 1: $0 < p < 1$.
    Then $1-p > 0$. So $\lim_{c\to0^+} c^{1-p} = 0$.
    In this case, $\int_0^1 x^{-p} dx = \frac{1-0}{1-p} = \frac{1}{1-p}$.
    Case 2: $p > 1$.
    Then $1-p < 0$. Let $1-p = -q$ where $q = p-1 > 0$.
    So $\lim_{c\to0^+} c^{1-p} = \lim_{c\to0^+} c^{-q} = \lim_{c\to0^+} \frac{1}{c^q} = \infty$ (since $q>0$).
    The denominator $1-p$ is negative. The numerator $1-c^{1-p} \to 1-\infty = -\infty$.
    So, $\int_0^1 x^{-p} dx = \frac{-\infty}{\text{negative number}} = \infty$.
    Thus, the integral converges to $\frac{1}{1-p}$ if $0<p<1$, and diverges to $\infty$ if $p>1$.

    (b) To prove $\int_0^\infty x^{-p}dx=\infty$ for all $p\in(0,\infty)$, we split the integral:
    $$\int_0^\infty x^{-p}dx = \int_0^1 x^{-p}dx + \int_1^\infty x^{-p}dx.$$
    For the integral $\int_0^\infty x^{-p}dx$ to converge, both parts must converge. If either part diverges to $\infty$ (since $x^{-p} > 0$ for $x>0$), the whole integral diverges to $\infty$.

    Case i: $p \ge 1$.
    This includes $p=1$ and $p>1$.
    If $p=1$, $\int_0^1 x^{-1}dx = \lim_{c\to0^+} [\ln x]_c^1 = \lim_{c\to0^+} (\ln 1 - \ln c) = \lim_{c\to0^+} (-\ln c) = \infty$.
    If $p>1$, from part (a), $\int_0^1 x^{-p}dx = \infty$.
    So, if $p \ge 1$, the first part $\int_0^1 x^{-p}dx$ diverges to $\infty$. Thus $\int_0^\infty x^{-p}dx = \infty$.

    Case ii: $0 < p < 1$.
    From part (a), $\int_0^1 x^{-p}dx = \frac{1}{1-p}$ (converges).
    Now consider $\int_1^\infty x^{-p}dx = \lim_{d\to\infty} \int_1^d x^{-p}dx$.
    Since $p \neq 1$:
    $$\int_1^d x^{-p}dx = \left[ \frac{x^{1-p}}{1-p} \right]_1^d = \frac{d^{1-p}}{1-p} - \frac{1^{1-p}}{1-p} = \frac{d^{1-p}-1}{1-p}.$$
    Since $0 < p < 1$, we have $1-p > 0$.
    So $\lim_{d\to\infty} d^{1-p} = \infty$.
    The denominator $1-p$ is positive.
    Thus, $\lim_{d\to\infty} \frac{d^{1-p}-1}{1-p} = \infty$.
    So, if $0 < p < 1$, the second part $\int_1^\infty x^{-p}dx$ diverges to $\infty$. Thus $\int_0^\infty x^{-p}dx = \infty$.

    Combining both cases ($p \ge 1$ and $0 < p < 1$), for all $p \in (0,\infty)$, $\int_0^\infty x^{-p}dx=\infty$.

18. Prove that if $f$ is integrable on $[a,b]$, then
    $$\lim_{d\to b^-}\int_a^d f(x)\:dx=\int_a^b f(x)\:dx.$$

    **Solution:**
    Let $F(y) = \int_a^y f(x)dx$. We want to show that $\lim_{d\to b^-} F(d) = F(b)$.
    This is equivalent to showing that $F$ is left-continuous at $b$.
    Since $f$ is integrable on $[a,b]$, it must be bounded on $[a,b]$. This means there exists a constant $M > 0$ such that $|f(x)| \le M$ for all $x \in [a,b]$.
    Consider the difference for $d < b$:
    $$\left| F(b) - F(d) \right| = \left| \int_a^b f(x)dx - \int_a^d f(x)dx \right| = \left| \int_d^b f(x)dx \right|.$$
    Using properties of integrals:
    $$\left| \int_d^b f(x)dx \right| \le \int_d^b |f(x)|dx.$$
    Since $|f(x)| \le M$:
    $$\int_d^b |f(x)|dx \le \int_d^b M dx = M(b-d).$$
    So, we have $\left| F(b) - F(d) \right| \le M(b-d)$.
    We want to show that for any $\epsilon > 0$, there exists a $\delta_0 > 0$ such that if $0 < b-d < \delta_0$ (which is $b-\delta_0 < d < b$), then $|F(b) - F(d)| < \epsilon$.
    Let $\epsilon > 0$ be given.
    If $M=0$, then $f(x)=0$ almost everywhere, and $F(x)=0$ for all $x$, so the limit holds trivially.
    Assume $M>0$. Choose $\delta_0 = \epsilon/M$.
    Then, if $0 < b-d < \delta_0$, we have $M(b-d) < M\delta_0 = M(\epsilon/M) = \epsilon$.
    So, if $b-\delta_0 < d < b$, then $\left| F(b) - F(d) \right| \le M(b-d) < \epsilon$.
    This proves that $\lim_{d\to b^-}F(d)=F(b)$, i.e.,
    $$\lim_{d\to b^-}\int_a^d f(x)\:dx=\int_a^b f(x)\:dx.$$

19. Let $f(x)=x^{2}$ and define a sequence $(s_n)$ according to $s_{1}=\lambda$ and $s_{n+1}=f(s_{n})$ for $n\in\mathbb{N}$. Prove that $(s_n)$ converges for $\lambda\in[-1,1]$, and diverges for $|\lambda|>1$.

    **Solution:**
    The sequence is defined by $s_1 = \lambda$ and $s_{n+1} = s_n^2$.
    Let's write out the first few terms:
    $s_1 = \lambda$
    $s_2 = s_1^2 = \lambda^2$
    $s_3 = s_2^2 = (\lambda^2)^2 = \lambda^4$
    $s_4 = s_3^2 = (\lambda^4)^2 = \lambda^8$
    It appears the general term is $s_n = \lambda^{2^{n-1}}$ for $n \ge 1$. We can prove this by induction if necessary, but it's standard.

    Case 1: $\lambda \in [-1,1]$, which means $|\lambda| \le 1$.
    * If $\lambda = 0$, then $s_1=0, s_2=0^2=0, \ldots$, so $s_n=0$ for all $n$. The sequence converges to 0.
    * If $\lambda = 1$, then $s_1=1, s_2=1^2=1, \ldots$, so $s_n=1$ for all $n$. The sequence converges to 1.
    * If $\lambda = -1$, then $s_1=-1, s_2=(-1)^2=1, s_3=1^2=1, \ldots$. So $s_n=1$ for $n \ge 2$. The sequence converges to 1.
    * If $0 < |\lambda| < 1$. Then $|s_n| = |\lambda^{2^{n-1}}| = |\lambda|^{2^{n-1}}$.
        Since $0 < |\lambda| < 1$ and the exponent $2^{n-1} \to \infty$ as $n \to \infty$, we have $\lim_{n\to\infty} |\lambda|^{2^{n-1}} = 0$.
        Thus, $\lim_{n\to\infty} s_n = 0$.
    In all subcases where $\lambda \in [-1,1]$, the sequence $(s_n)$ converges.

    Case 2: $|\lambda| > 1$.
    Then $|s_n| = |\lambda|^{2^{n-1}}$.
    Since $|\lambda| > 1$ and $2^{n-1} \to \infty$ as $n \to \infty$, we have $\lim_{n\to\infty} |\lambda|^{2^{n-1}} = \infty$.
    This means the sequence $(s_n)$ is unbounded and therefore diverges.

    > **Caution**
    > The key is still consider all possible cases and split them.

20. Consider the three sets
    $$A=[0,\sqrt{2}]\cap\mathbb{Q},\quad B=\{x^2+x-1:x\in\mathbb{R}\},\quad C=\{x\in\mathbb{R}:x^2+x-1<0\}.$$
    For each set, determine its maximum and minimum if they exist. For each set, determine its supremum and infimum. Detailed proofs are not required, but you should justify your answers.

    **Solution:**
    **Set A**: $A=\{q \in \mathbb{Q} : 0 \le q \le \sqrt{2}\}$.
    * Minimum: The smallest value in the interval $[0,\sqrt{2}]$ is $0$. Since $0$ is a rational number ($0 \in \mathbb{Q}$), $0 \in A$. Thus, $\min A = 0$.
    * Infimum: Since the minimum exists, $\inf A = \min A = 0$.
    * Maximum: The upper bound of the interval is $\sqrt{2}$. However, $\sqrt{2}$ is irrational, so $\sqrt{2} \notin A$. For any element $q \in A$, $q < \sqrt{2}$. By the **density** of rational numbers, for any $\epsilon > 0$, there exists a rational number $q'$ such that $\sqrt{2}-\epsilon < q' < \sqrt{2}$. We can ensure $q' \ge 0$. Thus, there is no largest element in $A$. $\max A$ does not exist.
    * Supremum: $\sqrt{2}$ is an upper bound for $A$. As shown above, for any $\epsilon > 0$, there is an element $q' \in A$ such that $q' > \sqrt{2}-\epsilon$. This means $\sqrt{2}$ is the least upper bound. So $\sup A = \sqrt{2}$.

    **Set B**: $B=\{y : y = x^2+x-1, x\in\mathbb{R}\}$.
    This is the range of the quadratic function $g(x) = x^2+x-1$. This is a **parabola** opening upwards.
    To find its minimum value, we can complete the square: $g(x) = (x^2+x+\frac{1}{4}) - \frac{1}{4} - 1 = (x+\frac{1}{2})^2 - \frac{5}{4}$.
    The minimum value of $(x+1/2)^2$ is $0$ (when $x=-1/2$).
    So the minimum value of $g(x)$ is $-\frac{5}{4}$.
    * Minimum: $\min B = -5/4$.
    * Infimum: Since the minimum exists, $\inf B = \min B = -5/4$.
    * Maximum: As $x \to \pm\infty$, $g(x) \to \infty$. The set $B$ is not bounded above. So $\max B$ does not exist.
    * Supremum: Since $B$ is not bounded above, $\sup B = \infty$.

    **Set C**: $C=\{x\in\mathbb{R}:x^2+x-1<0\}$.
    We need to solve the inequality $x^2+x-1<0$.
    First, find the roots of $x^2+x-1=0$ using the quadratic formula:
    $x = \frac{-1 \pm \sqrt{1^2 - 4(1)(-1)}}{2(1)} = \frac{-1 \pm \sqrt{1+4}}{2} = \frac{-1 \pm \sqrt{5}}{2}$.
    The roots are $x_1 = \frac{-1-\sqrt{5}}{2}$ and $x_2 = \frac{-1+\sqrt{5}}{2}$.
    Since the parabola $y=x^2+x-1$ opens upwards, the inequality $x^2+x-1 < 0$ holds for $x$ values strictly between the roots.
    So $C = \left( \frac{-1-\sqrt{5}}{2}, \frac{-1+\sqrt{5}}{2} \right)$. This is an open interval.
    * Minimum: $\min C$ does not exist (as it's an open interval).
    * Infimum: $\inf C = \frac{-1-\sqrt{5}}{2}$.
    * Maximum: $\max C$ does not exist.
    * Supremum: $\sup C = \frac{-1+\sqrt{5}}{2}$.

21. Let $f_{n}(x)=x-x^{n}$ on $[0,1]$ for $n\in\mathbb{N}$.
    (a) Prove that $f_{n}$ converges pointwise to a limit $f$, and determine $f$.
    (b) Prove that $f_{n}$ does not converge uniformly to $f$.
    (c) Find an interval $I$ contained in $[0, 1]$ on which $f_{n}\to f$ uniformly.
    (d) Prove that the $f_{n}$ are integrable, that $f$ is integrable, and that $\int_{0}^{1}f_{n}\to\int_{0}^{1}f$.

    **Solution:**
    (a) **Pointwise convergence**:
    For any fixed $x \in [0,1)$: $\lim_{n\to\infty} x^n = 0$.
    So, $\lim_{n\to\infty} f_n(x) = \lim_{n\to\infty} (x-x^n) = x-0 = x$.
    For $x = 1$: $f_n(1) = 1-1^n = 1-1 = 0$. So, $\lim_{n\to\infty} f_n(1) = 0$.
    Thus, $f_n(x)$ converges pointwise to the function $f(x)$ defined as:
    $$f(x)=\begin{cases}x & \quad \mathrm{if}\:0\leq x<1,\\0 & \quad \mathrm{if}\:x=1.\end{cases}$$
    ![[Pasted image 20250510142432.png]]
    (The solution text refers to Fig. 2 for graphs.)

    (b) **Uniform convergence**:
    To show $f_n$ does not converge uniformly to $f$ on $[0,1]$, we need to show that $\lim_{n\to\infty} \sup_{x\in[0,1]} |f_n(x)-f(x)| \neq 0$.
    For $x \in [0,1)$, $|f_n(x)-f(x)| = |(x-x^n) - x| = |-x^n| = x^n$.
    For $x=1$, $|f_n(1)-f(1)| = |0-0| = 0$.
    Consider $\sup_{x\in[0,1]} |f_n(x)-f(x)| = \sup_{x\in[0,1)} x^n$.
    Since $x^n$ is increasing for $x \in [0,1)$ and approaches $1$ as $x \to 1^-$, $\sup_{x\in[0,1)} x^n = 1$ for any fixed $n \in \mathbb{N}$.
    Therefore, $\lim_{n\to\infty} \sup_{x\in[0,1]} |f_n(x)-f(x)| = \lim_{n\to\infty} 1 = 1 \neq 0$.
    Thus, $f_n$ does not converge uniformly to $f$ on $[0,1]$.

    *_Alternatively, as shown in the provided solution, consider $x_n = (1/2)^{1/n}$. As $n \to \infty$, $x_n \to (1/2)^0 = 1$. But for each $n$, $0 < x_n < 1$._*
    *_Then, for this choice of $x_n$, since $x_n < 1$,_*
    $$|f_n(x_n) - f(x_n)| = x_n^n = \left((1/2)^{1/n}\right)^n = 1/2.$$
    *_So for $\epsilon = 1/4$ (or any $\epsilon \le 1/2$), for any $N$, we can choose $n > N$. For this $n$, there exists $x_n = (1/2)^{1/n}$ such that $|f_n(x_n)-f(x_n)| = 1/2$, which is not less than $1/4$. Thus, the convergence is not uniform._*

    (c) **Interval of uniform convergence**:
    Consider an interval $I = [0,a]$ where $0 \le a < 1$.
    On $I$, for $x \in [0,a]$, we have $x < 1$, so $f(x)=x$.
    Then $|f_n(x)-f(x)| = x^n$.
    The supremum of this difference on $I=[0,a]$ is:
    $$\sup_{x\in[0,a]} |f_n(x)-f(x)| = \sup_{x\in[0,a]} x^n = a^n$$
    (since $x^n$ is non-decreasing on $[0,a]$ for $n \ge 1$).
    Since $0 \le a < 1$, $\lim_{n\to\infty} a^n = 0$.
    Thus, $f_n \to f$ uniformly on any interval $[0,a]$ where $0 \le a < 1$. For example, $I=[0,1/2]$.

    (d) **Integrability**:
    Each $f_n(x) = x-x^n$ is a polynomial, hence continuous on $[0,1]$. Continuous functions on a closed interval are integrable. So each $f_n$ is integrable on $[0,1]$.
    $$\int_0^1 f_n(x) dx = \int_0^1 (x-x^n) dx = \left[ \frac{x^2}{2} - \frac{x^{n+1}}{n+1} \right]_0^1 = \left(\frac{1}{2} - \frac{1}{n+1}\right) - (0-0) = \frac{1}{2} - \frac{1}{n+1}.$$
    The limit function $f(x)$ is defined as $f(x)=x$ for $0 \le x < 1$ and $f(1)=0$.
    This function is bounded on $[0,1]$ (e.g., $|f(x)| \le 1$). It has only one point of discontinuity (at $x=1$).
    A function that is bounded on $[a,b]$ and has a finite number of discontinuities is integrable on $[a,b]$. So $f$ is integrable on $[0,1]$.
    The integral of $f(x)$ is:
    $$\int_0^1 f(x) dx = \int_0^1 x dx$$
    (since the value of an integrable function at a single point does not affect its integral).
    $$\int_0^1 x dx = \left[ \frac{x^2}{2} \right]_0^1 = \frac{1}{2} - 0 = \frac{1}{2}.$$
    Now, we check if $\lim_{n\to\infty} \int_{0}^{1}f_{n}(x)dx = \int_{0}^{1}f(x)dx$:
    $$\lim_{n\to\infty} \left(\frac{1}{2} - \frac{1}{n+1}\right) = \frac{1}{2} - 0 = \frac{1}{2}.$$
    Since $\int_{0}^{1}f(x)dx = \frac{1}{2}$, we have shown that $\int_{0}^{1}f_{n} \to \int_{0}^{1}f$.

22. Define
    $$f(x)=\left\{\begin{array}{ll}1&\quad\mathrm{if}\:|x|\leq1,\\-2&\quad\mathrm{if}\:1<|x|\leq2,\\0&\quad\mathrm{if}\:|x|>2\end{array}\right.$$
    for $x\in\mathbb{R}$.
    (a) Calculate $F(x)=\int_{0}^{x}f(t)dt$ for $x\in\mathbb{R}$.
    (b) Sketch $f$ and $F$.
    (c) Compute $F^{\prime}$ and state the precise range over which $F^{\prime}$ exists. You may make use of the Second Fundamental Theorem of Calculus.

    **Solution:**
    (a) $f(x)$ can be explicitly written for ranges of $x$:
    $f(x) = 1$ for $x \in [-1,1]$
    $f(x) = -2$ for $x \in (-2,-1] \cup (1,2]$ (Note: the original definition $1<|x|\le 2$ implies $x \in [-2, -1) \cup (1, 2]$ or $x \in (-2, -1] \cup [1, 2)$ depending on interpretation. The original LaTeX was $1<|x|\leq2$. Assuming $-2 \le x < -1$ and $1 < x \le 2$).
    Let's use: $f(x) = -2$ for $x \in [-2, -1) \cup (1, 2]$.
    $f(x) = 0$ for $x < -2$ or $x > 2$.

    Calculating $F(x)=\int_{0}^{x}f(t)dt$:
    If $x=0$, $F(0) = 0$.
    For $x>0$:
    * If $0 < x \le 1$: $f(t)=1$ on $(0,x]$.
        $$F(x) = \int_0^x 1 dt = [t]_0^x = x.$$
    * If $1 < x \le 2$:
        $$F(x) = \int_0^1 f(t)dt + \int_1^x f(t)dt = F(1) + \int_1^x (-2) dt = 1 + [-2t]_1^x = 1 + (-2x - (-2)) = 1 - 2x + 2 = 3-2x.$$
        At $x=1$, $F(1)=1$. From this formula, $3-2(1)=1$. Consistent.
        At $x=2$, $F(2)=3-2(2)=-1$.
    * If $x > 2$:
        $$F(x) = \int_0^2 f(t)dt + \int_2^x f(t)dt = F(2) + \int_2^x 0 dt = -1 + 0 = -1.$$
    For $x<0$: $f(t)$ is an even function ($f(-t)=f(t)$).
    Thus $F(x) = \int_0^x f(t)dt$ is an odd function. $F(-x) = \int_0^{-x} f(t)dt$. Let $u=-t, du=-dt$.
    $F(-x) = \int_0^x f(-u)(-du) = -\int_0^x f(u)du = -F(x)$.
    So $F(x) = -F(-x)$.
    * If $-1 \le x < 0$: Then $0 < -x \le 1$. $F(-x) = -x$. So $F(x) = -(-x) = x$.
    * If $-2 \le x < -1$: Then $1 < -x \le 2$. $F(-x) = 3-2(-x) = 3+2x$. So $F(x) = -(3+2x) = -3-2x$.
    * If $x < -2$: Then $-x > 2$. $F(-x) = -1$. So $F(x) = -(-1) = 1$.

    Combining all pieces:
    $$F(x)=\begin{cases}1 & \quad \mathrm{if}\:x<-2 \\ -3-2x & \quad \mathrm{if}\:-2\leq x < -1 \\ x & \quad \mathrm{if}\:-1\leq x\leq1 \\ 3-2x & \quad \mathrm{if}\:1<x\leq2 \\ -1 & \quad \mathrm{if}\:x>2\end{cases}$$

    (b) Sketch $f$ and $F$.
    ![[Pasted image 20250510142946.png]]
    (The solution text refers to Fig. 3)
    $f(x)$ is a step function. $F(x)$ is a continuous, piecewise linear function (a "tent" map shape, but with flat tops/bottoms and different slopes).

    (c) Compute $F'$.
    The Second Fundamental Theorem of Calculus states that if $f$ is continuous at $x_0$, then $F(x)=\int_a^x f(t)dt$ is differentiable at $x_0$ and $F'(x_0)=f(x_0)$.
    The function $f(x)$ is continuous everywhere except at $x = \pm 1$ and $x = \pm 2$.
    Thus, $F'(x) = f(x)$ for $x \in \mathbb{R} \setminus \{-2, -1, 1, 2\}$.
    Specifically:
    $F'(x) = 0$ if $|x|>2$
    $F'(x) = -2$ if $1<|x|<2$ (i.e., $x \in (-2,-1) \cup (1,2)$)
    $F'(x) = 1$ if $|x|<1$ (i.e., $x \in (-1,1)$)

    At the points of discontinuity of $f$:
    At $x=1$:
    Left-hand derivative of $F$: $\lim_{h\to 0^-} \frac{F(1+h)-F(1)}{h} = \lim_{h\to 0^-} \frac{(1+h)-1}{h} = 1$.
    Right-hand derivative of $F$: $\lim_{h\to 0^+} \frac{F(1+h)-F(1)}{h} = \lim_{h\to 0^+} \frac{(3-2(1+h))-1}{h} = \lim_{h\to 0^+} \frac{3-2-2h-1}{h} = \lim_{h\to 0^+} \frac{-2h}{h} = -2$.
    Since $1 \neq -2$, $F'(1)$ does not exist.
    At $x=2$:
    Left-hand derivative of $F$: $\lim_{h\to 0^-} \frac{F(2+h)-F(2)}{h} = \lim_{h\to 0^-} \frac{(3-2(2+h))-(-1)}{h} = \lim_{h\to 0^-} \frac{3-4-2h+1}{h} = \lim_{h\to 0^-} \frac{-2h}{h} = -2$.
    Right-hand derivative of $F$: $\lim_{h\to 0^+} \frac{F(2+h)-F(2)}{h} = \lim_{h\to 0^+} \frac{(-1)-(-1)}{h} = \lim_{h\to 0^+} \frac{0}{h} = 0$.
    Since $-2 \neq 0$, $F'(2)$ does not exist.
    Since $F(x)$ is odd, its derivative $F'(x)$ (where it exists) must be even. The points where $F'$ does not exist will be symmetric.
    $F'(-1)$ does not exist (left derivative is -2, right is 1).
    $F'(-2)$ does not exist (left derivative is 0, right is -2).
    The precise range over which $F'$ exists is $\mathbb{R} \setminus \{-2, -1, 1, 2\}$.

    > **Caution**
    > You need to verify that at these discontinuities, the derivatives do not exist.

23. (a) Let $f$ and $g$ be continuous functions on $[a,b]$ such that $\int_{a}^{b}f(x)dx=\int_{a}^{b}g(x)dx$. Prove that there exists an $x\in[a,b]$ such that $f(x)=g(x)$.
    (b) Construct an example of integrable functions $f$ and $g$ on $[a,b]$ where $\int_a^b f(x)dx = \int_{a}^{b}g(x)dx$ but that $f(x)\neq g(x)$ for all $x\in[a,b]$.

    **Solution:**
    (a) Let $h(x) = f(x)-g(x)$. Since $f$ and $g$ are continuous on $[a,b]$, $h(x)$ is also continuous on $[a,b]$.
    Given $\int_a^b f(x)dx = \int_a^b g(x)dx$, we can write:
    $$\int_a^b f(x)dx - \int_a^b g(x)dx = 0$$
    $$\int_a^b (f(x)-g(x))dx = 0$$
    $$\int_a^b h(x)dx = 0.$$
    Assume for contradiction that $h(x) \neq 0$ for all $x \in [a,b]$.
    Since $h$ is continuous on $[a,b]$ and $h(x) \neq 0$ for all $x \in [a,b]$, it must be that either $h(x) > 0$ for all $x \in [a,b]$ or $h(x) < 0$ for all $x \in [a,b]$ (by the Intermediate Value Theorem; if it took positive and negative values, it would have to be zero somewhere).
    Case 1: $h(x) > 0$ for all $x \in [a,b]$.
    Since $h$ is continuous on the closed interval $[a,b]$, $h$ attains a minimum value $m$ on $[a,b]$. Since $h(x)>0$ for all $x$, $m>0$.
    Then $\int_a^b h(x)dx \ge \int_a^b m \,dx = m(b-a)$.
    If $b>a$, then $m(b-a) > 0$, which contradicts $\int_a^b h(x)dx = 0$.
    (If $b=a$, the interval is a point, $\int_a^a h(x)dx = 0$ trivially. Then $f(a)=g(a)$ holds for $x=a$.) Assume $b>a$.
    Case 2: $h(x) < 0$ for all $x \in [a,b]$.
    Similarly, $h$ attains a maximum value $M$ on $[a,b]$, and $M<0$.
    Then $\int_a^b h(x)dx \le \int_a^b M \,dx = M(b-a)$.
    If $b>a$, then $M(b-a) < 0$, which contradicts $\int_a^b h(x)dx = 0$.
    Both cases lead to a contradiction. Therefore, the assumption that $h(x) \neq 0$ for all $x \in [a,b]$ must be false.
    Thus, there must exist some $x_0 \in [a,b]$ such that $h(x_0)=0$, which means $f(x_0)-g(x_0)=0$, so $f(x_0)=g(x_0)$.

    (b) Let $[a,b]=[-1,1]$.
    Define $f(x)$ and $g(x)$ as follows:
    $$f(x)=\begin{cases}-1 & \text{if } -1 \le x < 0 \\ 1 & \text{if } 0 \le x \le 1\end{cases}$$
    $$g(x)=\begin{cases}1 & \text{if } -1 \le x < 0 \\ -1 & \text{if } 0 \le x \le 1\end{cases}$$
    Both $f$ and $g$ are bounded and have a single discontinuity at $x=0$, so they are integrable on $[-1,1]$.
    For all $x \in [-1,1]$, $f(x) \neq g(x)$:
    If $x \in [-1,0)$, $f(x)=-1$ and $g(x)=1$.
    If $x \in [0,1]$, $f(x)=1$ and $g(x)=-1$.
    Now calculate the integrals:
    $$\int_{-1}^1 f(x)dx = \int_{-1}^0 (-1)dx + \int_0^1 (1)dx = [-x]_{-1}^0 + [x]_0^1 = (0-(1)) + (1-0) = -1+1=0.$$
    $$\int_{-1}^1 g(x)dx = \int_{-1}^0 (1)dx + \int_0^1 (-1)dx = [x]_{-1}^0 + [-x]_0^1 = (0-(-1)) + (-1-0) = 1-1=0.$$
    Thus, $\int_{-1}^1 f(x)dx = \int_{-1}^1 g(x)dx = 0$, but $f(x) \neq g(x)$ for all $x \in [-1,1]$.

24. Define the sequence of functions $h_{n}$ on $\mathbb{R}$ according to
    $$h_n(x)=\left\{\begin{array}{ll}n&\quad\mathrm{if}\:|x|\leq1/(2n),\\0&\quad\mathrm{if}\:|x|>1/(2n).\end{array}\right.$$
    (a) Sketch $h_{1},h_{2}$, and $h_{3}$.
    (b) Prove that $h_{n}$ converges pointwise to $0$ on $\mathbb{R}\setminus\{0\}$. Prove that $\lim_{n\to\infty}h_n(0)=\infty$.
    (c) Let $f$ be a continuous real-valued function on $\mathbb{R}$. Prove that
    $$\lim_{n\to\infty}\int_{-\infty}^{\infty}h_n(x)f(x)dx=f(0).$$
    (d) Construct an example of an integrable function $g$ on $\mathbb{R}$ where
    $$\lim_{n\to\infty}\int_{-\infty}^{\infty}h_{n}(x)g(x)dx$$
    exists and is a real number, but does not equal $g(0)$.

    **Solution:**
    (a) $h_n(x)$ is a rectangular pulse centered at $0$.
    The interval where $h_n(x)=n$ is $[ -1/(2n), 1/(2n) ]$. The width of this interval is $1/n$.
    The height of the pulse is $n$. The area of the rectangle is width $\times$ height $= (1/n) \times n = 1$.
    * $h_1(x)$: height 1 on $[-1/2, 1/2]$, 0 elsewhere.
    * $h_2(x)$: height 2 on $[-1/4, 1/4]$, 0 elsewhere.
    * $h_3(x)$: height 3 on $[-1/6, 1/6]$, 0 elsewhere.
    As $n$ increases, the pulse gets taller and narrower, but maintains an area of 1.
    ![[Pasted image 20250510144216.png]]

    (b) **Pointwise convergence**:
    If $x \neq 0$: For any fixed $x \neq 0$, we can choose an integer $N$ such that $N > \frac{1}{2|x|}$.
    Then for any $n > N$, we have $n > \frac{1}{2|x|}$, which implies $2n|x| > 1$, or $|x| > \frac{1}{2n}$.
    If $|x| > \frac{1}{2n}$, then by definition $h_n(x) = 0$.
    So, for any $x \neq 0$, $\lim_{n\to\infty} h_n(x) = 0$.
    If $x=0$: For any $n \in \mathbb{N}$, $|0| = 0 \le \frac{1}{2n}$.
    So $h_n(0) = n$ for all $n$.
    Thus, $\lim_{n\to\infty} h_n(0) = \lim_{n\to\infty} n = \infty$.

    (c) We need to evaluate $\lim_{n\to\infty}\int_{-\infty}^{\infty}h_n(x)f(x)dx$.
    Since $h_n(x)=0$ for $|x|>1/(2n)$, the integral becomes:
    $$\int_{-\infty}^{\infty}h_n(x)f(x)dx = \int_{-1/(2n)}^{1/(2n)} n f(x) dx = n \int_{-1/(2n)}^{1/(2n)} f(x) dx.$$
    Since $f$ is continuous on $\mathbb{R}$, it is continuous on the interval $[-1/(2n), 1/(2n)]$.
    By the Mean Value Theorem for Integrals, there exists a $c_n \in [-1/(2n), 1/(2n)]$ such that
    $$\int_{-1/(2n)}^{1/(2n)} f(x) dx = f(c_n) \left( \frac{1}{2n} - \left(-\frac{1}{2n}\right) \right) = f(c_n) \cdot \frac{1}{n}.$$
    So, the original expression becomes:
    $$n \left( f(c_n) \frac{1}{n} \right) = f(c_n).$$
    As $n \to \infty$, the interval $[-1/(2n), 1/(2n)]$ shrinks to the point $\{0\}$. Since $c_n \in [-1/(2n), 1/(2n)]$, by the Squeeze Theorem, $\lim_{n\to\infty} c_n = 0$.
    Since $f$ is continuous at $0$, we have $\lim_{n\to\infty} f(c_n) = f(\lim_{n\to\infty} c_n) = f(0)$.
    Therefore,
    $$\lim_{n\to\infty}\int_{-\infty}^{\infty}h_n(x)f(x)dx = f(0).$$
    (This sequence $h_n$ is an example of an "approximation to the identity" or a nascent Dirac delta function sequence.)

    (d) Let $g(x)$ be a function that is integrable but not continuous at $0$. For example:
    $$g(x) = \begin{cases} 0 & \mathrm{if}\: x < 0 \\ 1 & \mathrm{if}\: x \ge 0 \end{cases}.$$
    Here $g(0)=1$. The function $g$ is bounded and has one discontinuity, so it is integrable on any finite interval, and $h_n(x)g(x)$ has compact support for each $n$.
    Let's calculate the integral:
    $$
    \begin{align*}
    \int_{-\infty}^{\infty}h_n(x)g(x)dx &= \int_{-1/(2n)}^{1/(2n)} n g(x) dx \\
    &= \int_{-1/(2n)}^{0} n \cdot g(x) dx + \int_{0}^{1/(2n)} n \cdot g(x) dx \\
    &= \int_{-1/(2n)}^{0} n \cdot 0 dx + \int_{0}^{1/(2n)} n \cdot 1 dx \\
    &= 0 + n [x]_0^{1/(2n)} \\
    &= n \left(\frac{1}{2n} - 0\right) = \frac{1}{2}.
    \end{align*}
    $$
    So, for every $n$, $\int_{-\infty}^{\infty}h_n(x)g(x)dx = \frac{1}{2}$.
    Therefore,
    $$\lim_{n\to\infty}\int_{-\infty}^{\infty}h_n(x)g(x)dx = \lim_{n\to\infty} \frac{1}{2} = \frac{1}{2}.$$
    This limit exists and is $1/2$. However, $g(0)=1$.
    Since $1/2 \neq 1$, this limit does not equal $g(0)$.
>[!note]
>The key to solving this is to split the impulse into halves by $0$.

25. Consider the function
    $$f(x)=\frac{x}{1+x}$$
    on the interval $[0,\infty)$.
    (a) Show that $\lim_{x\to\infty}f(x)=1$, and that $0\leq f(x)<1$ for all $x\in[0,\infty)$.
    (b) Sketch $f$.
    (c) Calculate $f^{\prime},f^{\prime\prime}$, and use them to construct the partial Taylor series at $x=1$ with the form
    $$f_T(x)=\sum_{n=0}^2\frac{(x-1)^n f^{(n)}(1)}{n!}.$$
    (d) Show that $f_{T}$ can be written as a quadratic equation with the form $ax^2+bx+c$, and compute $a$, $b$, and $c$.
    (e) Add a sketch of $f_{T}$ to the sketch of $f$. *Note: $f_{T}(1)=f(1)$ so the two curves should intersect at $x=1$.*

    **Solution:**
    (a) For $x \in [0,\infty)$:
    To find $\lim_{x\to\infty}f(x)$:
    $$\lim_{x\to\infty}\frac{x}{1+x} = \lim_{x\to\infty}\frac{x/x}{(1+x)/x} = \lim_{x\to\infty}\frac{1}{1/x+1} = \frac{1}{0+1} = 1.$$
    To show $0\leq f(x)<1$:
    Since $x \ge 0$, $1+x > 0$. Thus, $f(x) = \frac{x}{1+x} \ge \frac{0}{1+x} = 0$.
    Also, for $x \ge 0$, $1+x > x$. Since $1+x$ is positive, we can divide by $1+x$:
    $$\frac{x}{1+x} < \frac{1+x}{1+x} = 1.$$
    So, $0 \le f(x) < 1$ for all $x \in [0,\infty)$.

    (b) Sketch $f$.
    ![[Pasted image 20250510144809.png]]
    $f(0)=0/(1+0)=0$.
    $f'(x) = \frac{d}{dx}\left(\frac{x}{1+x}\right) = \frac{(1)(1+x) - x(1)}{(1+x)^2} = \frac{1}{(1+x)^2}$.
    For $x \in [0,\infty)$, $f'(x) > 0$, so $f$ is strictly increasing.
    $f''(x) = \frac{d}{dx}((1+x)^{-2}) = -2(1+x)^{-3}(1) = \frac{-2}{(1+x)^3}$.
    For $x \in [0,\infty)$, $f''(x) < 0$, so $f$ is concave down.
    It starts at $(0,0)$, *increases*, and is *concave* down, approaching the horizontal asymptote $y=1$ as $x \to \infty$.
>[!caution]
>When we're sketching some function, we need to discuss it's monotonicity, concave or convexity.

- (c) Calculate derivatives and Taylor series at $x=1$.
    $f(x) = \frac{x}{1+x}$.
    $f(1) = \frac{1}{1+1} = \frac{1}{2}$.
    $f'(x) = \frac{1}{(1+x)^2}$.
    $f'(1) = \frac{1}{(1+1)^2} = \frac{1}{4}$.
    $f''(x) = \frac{-2}{(1+x)^3}$.
    $f''(1) = \frac{-2}{(1+1)^3} = \frac{-2}{8} = -\frac{1}{4}$.
    The partial Taylor series up to $n=2$ at $x=1$ is:
    $$f_T(x) = f(1) + f'(1)(x-1) + \frac{f''(1)}{2!}(x-1)^2$$
    $$f_T(x) = \frac{1}{2} + \frac{1}{4}(x-1) + \frac{-1/4}{2}(x-1)^2$$
    $$f_T(x) = \frac{1}{2} + \frac{1}{4}(x-1) - \frac{1}{8}(x-1)^2.$$

- (d) Rewrite $f_T(x)$ in the form $ax^2+bx+c$.
$$
    \begin{align*}
    f_T(x) &= \frac{1}{2} + \frac{1}{4}x - \frac{1}{4} - \frac{1}{8}(x^2-2x+1) \\
    &= \frac{1}{2} + \frac{1}{4}x - \frac{1}{4} - \frac{1}{8}x^2 + \frac{2}{8}x - \frac{1}{8} \\
    &= -\frac{1}{8}x^2 + \left(\frac{1}{4} + \frac{2}{8}\right)x + \left(\frac{1}{2} - \frac{1}{4} - \frac{1}{8}\right) \\
    &= -\frac{1}{8}x^2 + \left(\frac{1}{4} + \frac{1}{4}\right)x + \left(\frac{4}{8} - \frac{2}{8} - \frac{1}{8}\right) \\
    &= -\frac{1}{8}x^2 + \frac{1}{2}x + \frac{1}{8}.
    \end{align*}
    $$
    So, $a = -1/8$, $b = 1/2$, $c = 1/8$.

- (e) Add a sketch of $f_T(x)$ to the sketch of $f$.
    $f_T(x)$ is a parabola opening downwards (since $a=-1/8 < 0$).
    At $x=1$:
    $f(1) = 1/2$.
    $f_T(1) = -\frac{1}{8}(1)^2 + \frac{1}{2}(1) + \frac{1}{8} = -\frac{1}{8} + \frac{4}{8} + \frac{1}{8} = \frac{4}{8} = \frac{1}{2}$.
    So $f_T(1)=f(1)$, the curves intersect at $x=1$.
    $f'(1)=1/4$.
    $f_T'(x) = -\frac{1}{4}x + \frac{1}{2}$. So $f_T'(1) = -\frac{1}{4} + \frac{1}{2} = \frac{1}{4}$.
    The slopes are the same at $x=1$.
    $f''(1)=-1/4$.
    $f_T''(x) = -\frac{1}{4}$.
    The second derivatives are the same at $x=1$.
    The parabola $f_T(x)$ will be tangent to $f(x)$ at $x=1$ and have the same concavity there.


