**Problem 1 (10 points)**

Suppose that $(x_n)$ is an increasing sequence with a convergent subsequence. Prove that $(x_n)$ is a convergent sequence.

**Answer 1**

1. Assume the subsequence $\{x_{n_k}\}$ converges to the limit $c$. Then, for any $\epsilon > 0$, there exists $K > 0$ such that for any $k > K$,
$$|x_{n_k} - c| \le \epsilon$$
2. Since $\{x_{n_k}\}$ is an increasing subsequence (as $(x_n)$ is increasing) and converges to $c$, it must be that $x_{n_k} \le c$ for all $k$. 
3. Thus, the inequality $|x_{n_k} - c| \le \epsilon$ implies $c - \epsilon \le x_{n_k} \le c$. Since $(x_n)$ is an increasing sequence and has a subsequence $\{x_{n_k}\}$ converging to $c$, $c$ must be an *upper* bound for the sequence $(x_n)$. 
	1. If there were some $x_M > c$, then for any $n_k > M$, we would have $x_{n_k} \ge x_M > c$, which contradicts $x_{n_k} \to c$ (as they must eventually be $\le c$).
4. So, $(x_n)$ is an increasing sequence that is bounded above by $c$.By the *Monotone Convergence Theorem*, an increasing sequence that is bounded above converges. 
5. Therefore, $(x_n)$ is a convergent sequence.
Let $\lim_{n\to\infty} x_n = L$. Since $c$ is the limit of a subsequence of $(x_n)$, it must be that $L=c$.

**Problem 2 (10 points)**

Assume $f(x)$ is first order differentiable ($f'(x)$ exists) in $[-1,1]$ and $\sum_{n=1}^{\infty} f(1/n)$ absolutely converges. Prove: $f'(0)=0$.

**Answer 2**

1. Since $\sum_{n=1}^{\infty} f(1/n)$ absolutely converges, the terms of the series must approach zero, i.e., $\lim_{n\to\infty} f(1/n) = 0$.
2. Since $f(x)$ is differentiable in $[-1,1]$, it is *continuous* in $[-1,1]$, and in particular, continuous at $x=0$.
3. Therefore, $f(0) = \lim_{x\to 0} f(x)$. Taking the sequence $x_n = 1/n \to 0$, we have $f(0) = \lim_{n\to\infty} f(1/n) = 0$.
4. Assume, for contradiction, that $f'(0) = c \ne 0$. By the definition of the derivative:
$$ f'(0) = \lim_{x\to 0} \frac{f(x) - f(0)}{x - 0} = \lim_{x\to 0} \frac{f(x)}{x} = c $$
	1. Since $c \ne 0$, this implies that for $x$ sufficiently close to $0$ (i.e., for $0 < |x| < \delta$ for some $\delta > 0$), we have $\left|\frac{f(x)}{x}\right| \ge \frac{|c|}{2}$. (The PDF uses $\delta/2$ in the inequality; using $|c|/2$ is standard).
	2. This *means* $|f(x)| \ge \frac{|c|}{2} |x|$ for $0 < |x| < \delta$.
5. Let $x = 1/n$. For $n$ large enough such that $1/n < \delta$ (i.e., $n > N_0 = 1/\delta$), we have:
$$ |f(1/n)| \ge \frac{|c|}{2n} $$
6. We are given that $\sum_{n=1}^{\infty} f(1/n)$ converges absolutely, which means $\sum_{n=1}^{\infty} |f(1/n)|$ converges.
	1. However, the series $\sum_{n=N_0+1}^{\infty} \frac{|c|}{2n} = \frac{|c|}{2} \sum_{n=N_0+1}^{\infty} \frac{1}{n}$ diverges because the harmonic series $\sum \frac{1}{n}$ diverges, and $|c|/2 \ne 0$.
	2. By the *Comparison* *Test*, since $|f(1/n)| \ge \frac{|c|}{2n}$ for sufficiently large $n$, and $\sum \frac{|c|}{2n}$ diverges, the series $\sum |f(1/n)|$ must also *diverge*.
	3. This is a contradiction to the given condition that $\sum f(1/n)$ absolutely converges.
7. Therefore, the assumption $f'(0) \ne 0$ must be false. Hence, $f'(0)=0$.

**Problem 3 (10 points)**

Assume $f$ is a decreasing and continuous function on $\mathbb{R}$ and $\{x_n\}$ is a bounded sequence. Prove:
(a) (5 points) $\inf_n f(x_n) = f(\sup_n x_n)$
(b) (5 points) $\liminf_{n\to\infty} f(x_n) = f(\limsup_{n\to\infty} x_n)$

**Answer 3**

We prove part (b). The proof for part (a) is analogous.
1. Let $M = \limsup_{n\to\infty} x_n$. Since $\{x_n\}$ is a bounded sequence, $M$ exists and is a finite real number.
2. Let $L_f = \liminf_{n\to\infty} f(x_n)$. We want to show $L_f = f(M)$.

3. Step 1: Show $L_f \ge f(M)$.
	1. By the definition of $\limsup x_n = M$, for any $\epsilon > 0$, there exists an $N_0 \in \mathbb{N}$ such that for all $n > N_0$, $x_n < M + \epsilon$.
	2. Since $f$ is a decreasing function, if $x_n < M + \epsilon$, then $f(x_n) > f(M + \epsilon)$ (assuming $M+\epsilon$ is in the domain where $f$ is defined, which holds because $x_n$ are in domain of $f$).
	3. Thus, for $n > N_0$, $f(x_n) > f(M + \epsilon)$.
	4. This implies that $\inf_{k \ge n} f(x_k) \ge f(M + \epsilon)$ for $n > N_0$.
	5. Taking the limit as $n \to \infty$:
$$ L_f = \lim_{n\to\infty} \left( \inf_{k \ge n} f(x_k) \right) \ge f(M + \epsilon) $$
	6. Since this inequality holds for any $\epsilon > 0$, and $f$ is continuous at $M$, we can let $\epsilon \to 0^+$:
$$ L_f \ge \lim_{\epsilon \to 0^+} f(M + \epsilon) = f(M) $$

4. Step 2: Show $L_f \le f(M)$.
	1. By the definition of $\limsup x_n = M$, for any $\epsilon > 0$ and for any $N_1 \in \mathbb{N}$, there exists an $n > N_1$ such that $x_n > M - \epsilon$.
	2. Since $f$ is a decreasing function, if $x_n > M - \epsilon$, then $f(x_n) < f(M - \epsilon)$.
	3. This means that for any $N_1$, the set $\{f(x_n) : n > N_1\}$ contains at least one value that is less than $f(M - \epsilon)$.
	4. Therefore, $\inf_{k \ge N_1} f(x_k) \le f(x_n) < f(M - \epsilon)$ for that particular $n$.
	5. So, $\inf_{k \ge N_1} f(x_k) < f(M - \epsilon)$ for any $N_1$.
	6. Taking the limit as $N_1 \to \infty$:
$$ L_f = \lim_{N_1\to\infty} \left( \inf_{k \ge N_1} f(x_k) \right) \le f(M - \epsilon) $$
	7. Since this holds for any $\epsilon > 0$, and $f$ is continuous at $M$, we can let $\epsilon \to 0^+$:
$$ L_f \le \lim_{\epsilon \to 0^+} f(M - \epsilon) = f(M) $$

5. Combining Step 1 ($L_f \ge f(M)$) and Step 2 ($L_f \le f(M)$), we conclude that $L_f = f(M)$.
6. Thus, $\liminf_{n\to\infty} f(x_n) = f(\limsup_{n\to\infty} x_n)$.

For part (a): $\inf_n f(x_n) = f(\sup_n x_n)$
Let $S = \sup_n x_n$. Since $\{x_n\}$ is bounded, $S$ exists.
1.  For any $n$, $x_n \le S$. Since $f$ is decreasing, $f(x_n) \ge f(S)$. This means $f(S)$ is a lower bound for the set $\{f(x_n) : n \in \mathbb{N}\}$. Therefore, $\inf_n f(x_n) \ge f(S)$.
2.  Since $S = \sup_n x_n$, there exists a subsequence $\{x_{n_k}\}$ such that $\lim_{k\to\infty} x_{n_k} = S$. 
	1. Since $f$ is continuous, $\lim_{k\to\infty} f(x_{n_k}) = f(\lim_{k\to\infty} x_{n_k}) = f(S)$.
	2. For every $k$, $f(x_{n_k})$ is one of the values in the set $\{f(x_n)\}$.
	3. Therefore, $\inf_n f(x_n) \le f(x_{n_k})$ for all $k$.
	4. Taking the limit as $k \to \infty$: $\inf_n f(x_n) \le \lim_{k\to\infty} f(x_{n_k}) = f(S)$.
Combining both inequalities, $\inf_n f(x_n) = f(\sup_n x_n)$.

**Problem 4 (10 points)**

Suppose $f(x)$ is a first order differentiable function on $[a, b]$ such that $f(a) \ne 0$ and $f(b) \ne 0$. Assume there is a sequence of distinct points $x_n$ in $[a, b]$ such that $f(x_n)=0$ for all $n$. Let $c = \liminf_{n\to\infty} x_n$.
Prove:
(1) (4 points) $c \in (a,b)$.
(2) (6 points) $f(c)=f'(c)=0$.

**Answer 4**

(1) Prove $c \in (a,b)$.
1. Since $x_n \in [a,b]$ for all $n$, the sequence $\{x_n\}$ is *bounded*. The $\liminf_{n\to\infty} x_n = c$ exists and $c \in [a,b]$ (as $[a,b]$ is a *closed therefore compact* set).
2. We are given that $f$ is differentiable, hence continuous, on $[a,b]$.
3. We are also given $f(a) \ne 0$. 
	1. By *continuity* of $f$ at $a$, there exists a $\delta_a > 0$ such that for all $x \in [a, a+\delta_a) \cap [a,b]$, $f(x) \ne 0$. 
	2. Since $f(x_n)=0$ for all $n$, it must be that $x_n \notin [a, a+\delta_a)$ for all $n$. This implies that $\inf_{k \ge n} x_k \ge a+\delta_a$ for all $n$, 
	3. *so $c = \liminf x_n \ge a+\delta_a > a$. Thus $c \ne a$.*
4. Similarly, since $f(b) \ne 0$, by *continuity* of $f$ at $b$, there exists a $\delta_b > 0$ such that for all $x \in (b-\delta_b, b] \cap [a,b]$, $f(x) \ne 0$. 
	1. Since $f(x_n)=0$, $x_n \notin (b-\delta_b, b]$. If $c=b$, then there would be a subsequence $x_{n_k} \to b$, which would mean for $k$ large enough $x_{n_k} \in (b-\delta_b, b]$, a contradiction. Thus $c \ne b$.
5. Since $c \in [a,b]$ and $c \ne a$ and $c \ne b$, it must be that $c \in (a,b)$.

(2) Prove $f(c)=f'(c)=0$.
1. Since $c = \liminf_{n\to\infty} x_n$, there exists a *subsequence* $\{x_{n_k}\}$ of $\{x_n\}$ such that $\lim_{k\to\infty} x_{n_k} = c$.
2. Since $f$ is differentiable on $[a,b]$, it is *continuous* on $[a,b]$. Therefore,
$$ f(c) = f\left(\lim_{k\to\infty} x_{n_k}\right) = \lim_{k\to\infty} f(x_{n_k}) $$
3. Given $f(x_n)=0$ for all $n$, so $f(x_{n_k})=0$ for all $k$.
$$ f(c) = \lim_{k\to\infty} 0 = 0 $$
So, $f(c)=0$.

4. Now, we want to show $f'(c)=0$. Since $f$ is differentiable at $c$,
$$ f'(c) = \lim_{x\to c} \frac{f(x)-f(c)}{x-c} $$
	1. We can use the subsequence $x_{n_k} \to c$. Since the points $x_n$ are distinct, for $k$ large enough (so $n_k$ is large enough), $x_{n_k} \ne c$.
	2. Thus, we can evaluate the limit using this subsequence:
$$ f'(c) = \lim_{k\to\infty} \frac{f(x_{n_k})-f(c)}{x_{n_k}-c} $$
	3. We *know* $f(x_{n_k})=0$ and we just *proved* $f(c)=0$.
$$ f'(c) = \lim_{k\to\infty} \frac{0-0}{x_{n_k}-c} = \lim_{k\to\infty} 0 = 0 $$
5. Thus, $f'(c)=0$.

**Problem 5 (10 points)**

a) (5 points) Given a *continuous* function $f(x)$ on $(0,1)$, we assume
$$f(1/3) < \lim_{x\to 0^+} f(x) < f(2/3)$$
$$f(1/3) < \lim_{x\to 1^-} f(x) < f(2/3)$$
Prove: There exist $x_1, x_2 \in (0,1)$ such that $f(x_2) \le f(x) \le f(x_1)$ for any $x \in (0,1)$.
(This means $f$ attains its maximum and minimum on $(0,1)$.)

b) (5 points) Given a *differentiable* function $f(x)$ and a point $c$, we assume that there exist two sequences $\{x_n\}$, $\{y_n\}$ such that $x_n < c$, $f(x_n) < f(c)$, $\lim_{n\to\infty} x_n = c$, and $y_n > c$, $f(y_n) < f(c)$, $\lim_{n\to\infty} y_n = c$. Prove: $f'(c)=0$.

**Answer 5**

a) Let $L_0 = \lim_{x\to 0^+} f(x)$ and $L_1 = \lim_{x\to 1^-} f(x)$.
The given conditions are:
(i) $f(1/3) < L_0 < f(2/3)$
(ii) $f(1/3) < L_1 < f(2/3)$

To prove $f$ attains its maximum:
1. Let $M_0 = f(2/3)$. From (i) and (ii), $L_0 < M_0$ and $L_1 < M_0$. 
	1. *Since $L_0 < M_0$, there exists an* $\epsilon_1 > 0$ (e.g., $\epsilon_1 = (M_0 - L_0)/2$) and a $\delta_1 > 0$ such that for all $x \in (0, \delta_1)$, $f(x) < L_0 + \epsilon_1 < M_0$.
	2. Since $L_1 < M_0$, there exists an $\epsilon_2 > 0$ (e.g., $\epsilon_2 = (M_0 - L_1)/2$) and a $\delta_2 > 0$ such that for all $x \in (1-\delta_2, 1)$, $f(x) < L_1 + \epsilon_2 < M_0$.
2. Choose $\delta = \min(\delta_1, 1-\delta_2, 1/3, 1-(2/3))$. Let $K = [\delta, 1-\delta]$. $K$ is a closed and bounded interval in $(0,1)$, and $1/3, 2/3 \in K$. Since $f$ is continuous on $(0,1)$, it is continuous on $K$. 
3. By the *Extreme Value Theorem*, $f$ attains its maximum value on $K$ at some point $x_1 \in K$. So $f(x_1) \ge f(x)$ for all $x \in K$. In particular, $f(x_1) \ge f(2/3) = M_0$.
4. For $x \in (0, \delta)$ or $x \in (1-\delta, 1)$ (i.e., $x \notin K$), we have $f(x) < M_0 \le f(x_1)$. Thus, $f(x_1)$ is the maximum value of $f(x)$ on $(0,1)$.

To prove $f$ attains its minimum:
1. Let $m_0 = f(1/3)$. From (i) and (ii), $L_0 > m_0$ and $L_1 > m_0$.
	1. Since $L_0 > m_0$, there exists an $\epsilon_3 > 0$ (e.g., $\epsilon_3 = (L_0 - m_0)/2$) and a $\delta_3 > 0$ such that for all $x \in (0, \delta_3)$, $f(x) > L_0 - \epsilon_3 > m_0$.
	2. Since $L_1 > m_0$, there exists an $\epsilon_4 > 0$ (e.g., $\epsilon_4 = (L_1 - m_0)/2$) and a $\delta_4 > 0$ such that for all $x \in (1-\delta_4, 1)$, $f(x) > L_1 - \epsilon_4 > m_0$.
2. Choose $\delta' = \min(\delta_3, 1-\delta_4, 1/3, 1-(2/3))$. Let $K' = [\delta', 1-\delta']$.$f$ attains its *minimum value on* $K'$ at some point $x_2 \in K'$. So $f(x_2) \le f(x)$ for all $x \in K'$. In particular, $f(x_2) \le f(1/3) = m_0$.
3. For $x \in (0, \delta')$ or $x \in (1-\delta', 1)$ (i.e., $x \notin K'$), we have $f(x) > m_0 \ge f(x_2)$ Thus, $f(x_2)$ is the minimum value of $f(x)$ on $(0,1)$.

Therefore, there exist $x_1, x_2 \in (0,1)$ such that $f(x_2) \le f(x) \le f(x_1)$ for any $x \in (0,1)$.

>[!note]
>The key is to govern the function value near $0$ or $1$ by some compact interval and then use the EVT on that compact interval.

b) Given $f$ is differentiable at $c$. Thus $f'(c)$ exists. The definition of $f'(c)$ is $$\lim_{h\to 0} \frac{f(c+h)-f(c)}{h}$$
1. This means the left-hand limit and right-hand limit must exist and be equal to $f'(c)$.
$$ f'(c) = \lim_{x\to c^-} \frac{f(x)-f(c)}{x-c} \quad \text{and} \quad f'(c) = \lim_{x\to c^+} \frac{f(x)-f(c)}{x-c} $$
2. Consider the sequence $\{x_n\}$: $x_n < c$, $\lim_{n\to\infty} x_n = c$, and $f(x_n) < f(c)$.
	1. For these terms, $f(x_n)-f(c) < 0$ and $x_n-c < 0$.
	2. Thus, the Newton quotient $\frac{f(x_n)-f(c)}{x_n-c} > 0$.
	3. Taking the limit using this sequence:
$$ \lim_{x\to c^-} \frac{f(x)-f(c)}{x-c} = \lim_{n\to\infty} \frac{f(x_n)-f(c)}{x_n-c} \ge 0 $$
	4. So, $f'(c) \ge 0$.

3. Consider the sequence $\{y_n\}$: $y_n > c$, $\lim_{n\to\infty} y_n = c$, and $f(y_n) < f(c)$.
	1. For these terms, $f(y_n)-f(c) < 0$ and $y_n-c > 0$.
	2. Thus, the Newton quotient $\frac{f(y_n)-f(c)}{y_n-c} < 0$.
	3. Taking the limit using this sequence:
$$ \lim_{x\to c^+} \frac{f(x)-f(c)}{x-c} = \lim_{n\to\infty} \frac{f(y_n)-f(c)}{y_n-c} \le 0 $$
	4. So, $f'(c) \le 0$.

4. Since we have $f'(c) \ge 0$ and $f'(c) \le 0$, it must be that $f'(c)=0$.


**Problem 6 (15 points)**

Define $\mathbb{C}([0,1])$ as the space of *continuous* functions on $[0,1]$ and $\mathcal{I}$ as the space of *continuous* and *increasing* functions on $[0,1]$.
(a) (5 points) Let $X=\mathbb{C}([0,1])$. Prove: $$d_1(f,g) = \int_0^1 |f(x)-g(x)|dx$$ is a metric.
(b) (10 points) Let $X=\mathcal{I}$ and metric $$d_\infty(f,g) = \sup_{x\in[0,1]} |f(x)-g(x)|$$ Prove: $(X, d_\infty)$ is a complete metric space.

**Answer 6**

(a) To prove $d_1(f,g) = \int_0^1 |f(x)-g(x)|dx$ is a metric on $\mathbb{C}([0,1])$, we verify the metric axioms for $f, g, h \in \mathbb{C}([0,1])$:
1.  **Non-negativity and Identity of Indiscernibles**: $d_1(f,g) \ge 0$, and $d_1(f,g) = 0 \iff f=g$.
    * Since $|f(x)-g(x)| \ge 0$ for all $x$, the integral $\int_0^1 |f(x)-g(x)|dx \ge 0$. So $d_1(f,g) \ge 0$.
    * If $f(x)=g(x)$ for all $x \in [0,1]$, then $|f(x)-g(x)|=0$, so $\int_0^1 0 dx = 0$. Thus $d_1(f,f)=0$.
    * If $d_1(f,g) = \int_0^1 |f(x)-g(x)|dx = 0$: Let $k(x) = |f(x)-g(x)|$. Then $k(x)$ is a non-negative continuous function. If the integral of a non-negative continuous function over an interval is zero, the function must be identically zero on that interval. Thus, $|f(x)-g(x)|=0$ for all $x \in [0,1]$, which implies $f(x)=g(x)$ for all $x \in [0,1]$, so $f=g$.

2.  **Symmetry**: $d_1(f,g) = d_1(g,f)$.
    $$ d_1(f,g) = \int_0^1 |f(x)-g(x)|dx = \int_0^1 |-(g(x)-f(x))|dx = \int_0^1 |g(x)-f(x)|dx = d_1(g,f) $$

3.  **Triangle Inequality**: $d_1(f,h) \le d_1(f,g) + d_1(g,h)$.
    For any $x \in [0,1]$, by the triangle inequality for real numbers:
    $$ |f(x)-h(x)| = |(f(x)-g(x)) + (g(x)-h(x))| \le |f(x)-g(x)| + |g(x)-h(x)| $$
    Integrating both sides from $0$ to $1$ (integrals preserve non-strict inequalities):
    $$ \int_0^1 |f(x)-h(x)|dx \le \int_0^1 (|f(x)-g(x)| + |g(x)-h(x)|)dx $$
    $$ \int_0^1 |f(x)-h(x)|dx \le \int_0^1 |f(x)-g(x)|dx + \int_0^1 |g(x)-h(x)|dx $$
    Thus, $d_1(f,h) \le d_1(f,g) + d_1(g,h)$.
*All three conditions are satisfied, so $d_1(f,g)$ is a metric.*

(b)  To prove $(X, d_\infty)$ is complete, we take an arbitrary *Cauchy sequence* $\{f_n\}$ in $X$ and show it converges to a limit $f$ which is also in $X$.
1.  Let $\{f_n\}$ be a Cauchy sequence in $(X, d_\infty)$. This means for any $\epsilon > 0$, there exists $N_0 \in \mathbb{N}$ such that for all $n, m > N_0$,
    $$ d_\infty(f_n, f_m) = \sup_{x\in[0,1]} |f_n(x)-f_m(x)| < \epsilon $$
2.  This condition implies that for each fixed $x \in [0,1]$, *the sequence of real numbers $\{f_n(x)\}$ is a Cauchy sequence in $\mathbb{R}$. Since $\mathbb{R}$ is complete, $\{f_n(x)\}$ converges for each $x$*. Let $f(x) = \lim_{n\to\infty} f_n(x)$ for each $x \in [0,1]$. This defines the pointwise limit function $f$.
3.  The Cauchy condition in $d_\infty$ is precisely the definition of a *uniformly Cauchy* sequence. A *uniformly* Cauchy sequence of functions on $[0,1]$ converges *uniformly* to a *limit* function. Thus, $f_n \to f$ *uniformly* on $[0,1]$.
4.  Since each $f_n$ is *continuous* on $[0,1]$ and $f_n \to f$ *uniformly* on $[0,1]$, the limit function $f$ is also *continuous* on $[0,1]$.
5.  We must show that $f \in X$, which means $f$ must also be increasing.
	1. Let $x_1, x_2 \in [0,1]$ such that $x_1 < x_2$.
	2. Since each $f_n \in \mathcal{I}$, $f_n$ is increasing, so $f_n(x_1) \le f_n(x_2)$ for all $n$.
	3. Taking the limit as $n\to\infty$ on both sides of the inequality (since limits preserve non-strict inequalities):
    $$ \lim_{n\to\infty} f_n(x_1) \le \lim_{n\to\infty} f_n(x_2) $$
    $$ f(x_1) \le f(x_2) $$
	4. This shows that $f$ is an increasing function.
6.  Since $f$ is continuous on $[0,1]$ and increasing on $[0,1]$, $f \in \mathcal{I} = X$.
    We have shown that an arbitrary Cauchy sequence $\{f_n\}$ in $X$ converges (uniformly) to a function $f$ which is also *in* $X$.
    Therefore, $(X, d_\infty)$ is a *complete* metric space. (This uses the property that a closed subset of a complete metric space is complete, and $\mathcal{I}$ can be shown to be a closed subset of $\mathbb{C}([0,1])$ with the $d_\infty$ metric.)

**Problem 7 (15 points)**

Let $f$ be a bounded function on $[0,1]$. Given any partition $P = \{0=p_0 < p_1 < \dots < p_m = 1\}$ on $[0,1]$, we *define*
$$len(P) = \max_{0 \le k \le m-1} (p_{k+1} - p_k)$$
We also define $$U_n = \inf_{P, len(P) \ge 1/n} U(f;P)$$ and $$L_n = \sup_{P, len(P) \ge 1/n} L(f;P)$$
Prove:
1. (5 points) $\lim_{n\to\infty} U_n$ and $\lim_{n\to\infty} L_n$ exist.
2. (10 points) $f$ is Riemann integrable on $[0,1]$ if and only if $\lim_{n\to\infty} U_n = \lim_{n\to\infty} L_n$.

*(Note: The condition $len(P) \ge 1/n$ is unusual for definitions related to Riemann integrability, which typically use $len(P) \le \delta$ or $len(P) \to 0$. The solution below follows the PDF's claim about monotonicity based on this definition.)*

**Answer 7**

1.  Let $S_n = \{P \text{ is a partition of } [0,1] : len(P) \ge 1/n \}$.
    $U_n = \inf_{P \in S_n} U(f;P)$
    $L_n = \sup_{P \in S_n} L(f;P)$
    1. As $n$ increases, $1/n$ decreases. The condition $len(P) \ge 1/n$ becomes less restrictive, meaning more partitions satisfy it.
    2. So, if $n_1 < n_2$, then $1/n_1 > 1/n_2$. Thus, if $P \in S_{n_1}$ (i.e., $len(P) \ge 1/n_1$), then $len(P) \ge 1/n_1 > 1/n_2$, so $P \in S_{n_2}$. This means $S_{n_1} \subseteq S_{n_2}$.
    3. Therefore:
	    1. $U_{n_1} = \inf_{P \in S_{n_1}} U(f;P) \ge \inf_{P \in S_{n_2}} U(f;P) = U_{n_2}$. So, $(U_n)$ is a *decreasing* sequence.
	    2. $L_{n_1} = \sup_{P \in S_{n_1}} L(f;P) \le \sup_{P \in S_{n_2}} L(f;P) = L_{n_2}$. So, $(L_n)$ is an *increasing* sequence.
    4. Since $f$ is a bounded function on $[0,1]$, let $m = \inf_{x\in[0,1]} f(x)$ and $M = \sup_{x\in[0,1]} f(x)$.
    5. For any partition $P$, $m \cdot (1-0) \le L(f;P) \le U(f;P) \le M \cdot (1-0)$.So, $m \le L_n \le U_n \le M$ for all $n$.
	    1. $(U_n)$ is a decreasing sequence bounded below by $m$. By the *Monotone Convergence Theorem*, $\lim_{n\to\infty} U_n$ exists.
	    2. $(L_n)$ is an increasing sequence bounded above by $M$. By the *Monotone Convergence Theorem*, $\lim_{n\to\infty} L_n$ exists.

2.  As $n \to \infty$, $1/n \to 0$. 
	1. The condition $len(P) \ge 1/n$ eventually includes all partitions $P$ (since for any fixed partition $P$, $len(P) > 0$, so for $n$ large enough, $1/n < len(P)$, which means $len(P) > 1/n$).
	2. Thus, the set $S_n$ tends towards the set of all possible partitions of $[0,1]$.
	3. Therefore,
    $$\lim_{n\to\infty} U_n = \inf_{P} U(f;P) = \overline{\int_0^1} f(x)dx$$ *(the upper Darboux integral).*
    $$\lim_{n\to\infty} L_n = \sup_{P} L(f;P) = \underline{\int_0^1} f(x)dx$$ *(the lower Darboux integral).*
    4. A function $f$ is Riemann integrable on $[0,1]$ if and only if its upper Darboux integral equals its lower Darboux integral, i.e., $\overline{\int_0^1} f(x)dx = \underline{\int_0^1} f(x)dx$.
    5. Therefore, $f$ is Riemann integrable on $[0,1]$ if and only if $\lim_{n\to\infty} U_n = \lim_{n\to\infty} L_n$.

**Problem 8 (20 points)**

Prove:
Theorem 1. Suppose that $f: [a,b] \to \mathbb{R}$ and $a<c<b$. Then $f$ is Riemann integrable on $[a,b]$ if and only if it is Riemann integrable on $[a,c]$ and $[c,b]$. Moreover, in that case,
$$ \int_a^b f = \int_a^c f + \int_c^b f $$

**Answer 8**

This is a standard theorem in Riemann integration. The proof typically involves two directions:

($\Rightarrow$) Assume $f$ is *Riemann* *integrable* on $[a,b]$. We need to show $f$ is Riemann integrable on $[a,c]$ and $[c,b]$.
1. $f$ is Riemann integrable on $[a,b]$ means that for any $\epsilon > 0$, there exists a partition $P$ of $[a,b]$ such that $U(f,P) - L(f,P) < \epsilon$.
2. We can refine $P$ to include the point $c$ without increasing $U(f,P) - L(f,P)$. Let $P^* = P \cup \{c\}$. Then $P^*$ is a partition of $[a,b]$ containing $c$.
3. $P^*$ induces a partition $P_1$ of $[a,c]$ and a partition $P_2$ of $[c,b]$.We have $U(f,P^*) = U(f,P_1) + U(f,P_2)$ and $L(f,P^*) = L(f,P_1) + L(f,P_2)$.
4. So, $U(f,P^*) - L(f,P^*) = (U(f,P_1) - L(f,P_1)) + (U(f,P_2) - L(f,P_2))$.
5. Since $U(f,P_1) - L(f,P_1) \ge 0$ and $U(f,P_2) - L(f,P_2) \ge 0$, we have:
$$U(f,P_1) - L(f,P_1) \le U(f,P^*) - L(f,P^*) \le U(f,P) - L(f,P) < \epsilon$$
$$U(f,P_2) - L(f,P_2) \le U(f,P^*) - L(f,P^*) \le U(f,P) - L(f,P) < \epsilon$$
This shows that $f$ is Riemann integrable on $[a,c]$ and on $[c,b]$.

($\Leftarrow$) Assume $f$ is Riemann integrable on $[a,c]$ and on $[c,b]$. We need to show $f$ is Riemann integrable on $[a,b]$.
1. Since $f$ is Riemann integrable on $[a,c]$, for any $\epsilon > 0$, there exists a partition $P_1$ of $[a,c]$ such that $U(f,P_1) - L(f,P_1) < \epsilon/2$.
2. Since $f$ is Riemann integrable on $[c,b]$, for any $\epsilon > 0$, there exists a partition $P_2$ of $[c,b]$ such that $U(f,P_2) - L(f,P_2) < \epsilon/2$.
3. Let $P = P_1 \cup P_2$. Then $P$ is a partition of $[a,b]$.
$$U(f,P) = U(f,P_1) + U(f,P_2)$$
$$L(f,P) = L(f,P_1) + L(f,P_2)$$
4. So, $$U(f,P) - L(f,P) = (U(f,P_1) - L(f,P_1)) + (U(f,P_2) - L(f,P_2)) < \epsilon/2 + \epsilon/2 = \epsilon$$
This shows that $f$ is Riemann integrable on $[a,b]$.

**Moreover, in that case, $\int_a^b f = \int_a^c f + \int_c^b f$**:
If $f$ is integrable on all three intervals, then for any $\epsilon > 0$, we can choose a partition $P_1$ for $[a,c]$ and a partition $P_2$ for $[c,b]$ such that:
$$ L(f,P_1) \le \int_a^c f dx \le U(f,P_1) \quad \text{and} \quad U(f,P_1) - L(f,P_1) < \frac{\epsilon}{2} $$
and
$$ L(f,P_2) \le \int_c^b f dx \le U(f,P_2) \quad \text{and} \quad U(f,P_2) - L(f,P_2) < \frac{\epsilon}{2} $$
Let $P = P_1 \cup P_2$. Then $P$ is a partition of $[a,b]$.
We know that
$$ L(f,P) = L(f,P_1) + L(f,P_2) $$
and
$$ U(f,P) = U(f,P_1) + U(f,P_2) $$
Therefore,
$$ L(f,P_1) + L(f,P_2) \le \int_a^b f dx \le U(f,P_1) + U(f,P_2) $$
We also have the sum of the individual integrals:
$$ L(f,P_1) + L(f,P_2) \le \int_a^c f dx + \int_c^b f dx \le U(f,P_1) + U(f,P_2) $$
Now, consider the absolute difference:
$$ \left| \int_a^b f dx - \left( \int_a^c f dx + \int_c^b f dx \right) \right| $$
Since both $\int_a^b f dx$ and $\left( \int_a^c f dx + \int_c^b f dx \right)$ *lie in the interval* $[L(f,P_1)+L(f,P_2), U(f,P_1)+U(f,P_2)]$, *their difference must be less than or equal to the length of this interval:*
$$ \left| \int_a^b f dx - \left( \int_a^c f dx + \int_c^b f dx \right) \right| \le (U(f,P_1)+U(f,P_2)) - (L(f,P_1)+L(f,P_2)) $$
$$ = (U(f,P_1)-L(f,P_1)) + (U(f,P_2)-L(f,P_2)) $$
$$ < \frac{\epsilon}{2} + \frac{\epsilon}{2} = \epsilon $$
Since $\epsilon$ is an arbitrary positive number, the absolute difference must be 0.
Therefore, we must have:
$$ \int_a^b f dx = \int_a^c f dx + \int_c^b f dx $$