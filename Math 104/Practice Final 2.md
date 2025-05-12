# Mathematical Problems (10 points each)

## Problem 1

$$a_n=\frac{(0.3)^n+(0.7)^n}{1+(0.8)^n}.\:\mathrm{Compute}\:\operatorname*{lim}_n a_n^{1/n}.$$

### Answer 1

In the numerator, the term $(0.7)^n$ is more important than $(0.3)^n$. In the denominator, the term $1$ is more important than $(0.8)^{n}$. So intuitively, one can approximate the expression for $a_{n}$ as $(0.7)^n$. More precisely, we can write
$$a_n=(0.7)^n\frac{1+(0.3/0.7)^n}{1+(0.8)^n}=0.7^nb_n.$$We can show $b_{n}\to1$ as $n\rightarrow\infty$, and for any $x>0$, we have $x^{1/n}\to1$ as $n\to\infty$, hence $\operatorname*{lim}_{n}b_{n}^{1/n}=1$. Hence$$\lim_n a_n^{1/n}=\lim_n (0.7 \cdot b_n^{1/n}) = 0.7 \cdot 1 = 0.7.$$

## Problem 2

Suppose $a_{n}>0$ and $\sum_{n}a_{n}$ converges. Prove that
$$\sum_n \frac{(-1)^na_n+a_{2n}}{2}$$
converges.

### Answer 2

Because $\sum_{n}a_{n}$ converges, this implies $a_n \to 0$.
The series $\sum_{n}(-1)^{n}a_{n}$ converges. If $a_n$ is monotonically decreasing (often an implicit assumption for such problems if not stated for the Alternating Series Test), it converges by AST. If $\sum a_n$ implies $\sum |a_n|$ converges (i.e., absolute convergence), then $\sum (-1)^n a_n$ converges absolutely. Given $\sum a_n$ converges and $a_n > 0$, it means $\sum |a_n|$ converges. Thus, $\sum (-1)^n a_n$ converges absolutely.

Also, since $a_n > 0$, and $\sum a_n$ converges, the series $\sum_{n}a_{2n}$ is a series of positive terms. Since $a_{2n} \le a_k$ for $k \le 2n$ (if decreasing) or generally, the terms $a_{2n}$ are a subset of the terms $a_n$. More formally, since $a_n>0$, $0 \leq \sum_{k=N}^{M}a_{2k} \leq \sum_{j=2N}^{2M}a_{j}$ (or $\sum_{j=N}^{2M}a_j$). As $\sum a_n$ converges, its partial sums are bounded and $a_n \to 0$. The series $\sum a_{2n}$ must also converge. For example, $\sum_{n=1}^N a_{2n} \le \sum_{k=1}^{2N} a_k$. Since $\sum a_k$ converges, its partial sums are bounded, so the partial sums of $\sum a_{2n}$ are bounded, and since $a_{2n} > 0$, $\sum a_{2n}$ converges.

Thus, $\sum_n \frac{(-1)^na_n+a_{2n}}{2} = \frac{1}{2}\sum_n (-1)^na_n + \frac{1}{2}\sum_n a_{2n}$.
Since both series on the right converge, their sum (and thus the original series) converges.

## Problem 3

Fix a positive number $a$, and choose $x_{1}>\sqrt{a}$. Define $x_{2},x_{3},\cdots$ iteratively by
$$x_{n+1}=\frac{x_n+a/x_n}{2}.$$
Prove that $L_{n}$ converges to $u$. Hint: for any $x,y>0$, we have $\frac{x+y}{2}\geq\sqrt{xy}$.
*(Note: The problem statement uses $L_n$ and $u$. Based on standard interpretations and the answer, it is assumed $L_n$ refers to the sequence $x_n$, and the target limit $u$ is $\sqrt{a}$.)*

### Answer 3

We first prove that $x_{n}\geq\sqrt{a}$ (assuming $L_n$ is the sequence $x_n$).
For $n=1$, $x_1 > \sqrt{a}$ is given.
Assume $x_k \geq \sqrt{a}$ for some $k \geq 1$. Then $x_k > 0$.
Using the AM-GM inequality (hint),
$$x_{k+1}=\frac{x_k+a/x_k}{2}\geq\sqrt{x_k \cdot \frac{a}{x_k}}=\sqrt{a}.$$
So, by induction, $x_n \geq \sqrt{a}$ for all $n \geq 1$.

Next, we prove that the sequence $(x_n)$ is non-increasing for $n \geq 1$.
$$x_{n+1} - x_n = \frac{x_n+a/x_n}{2} - x_n = \frac{x_n+a/x_n-2x_n}{2} = \frac{a/x_n-x_n}{2} = \frac{a-x_n^2}{2x_n}.$$
Since $x_n \geq \sqrt{a}$, $x_n^2 \geq a$, so $a-x_n^2 \leq 0$. Also $x_n > 0$.
Thus, $x_{n+1} - x_n \leq 0$, which means $x_{n+1} \leq x_n$.
The sequence $(x_n)$ (i.e., $L_n$) is monotone decreasing (non-increasing) and bounded below by $\sqrt{a}$. Therefore, it converges to a limit, let's call it $L$.
Since $x_n \geq \sqrt{a}$ for all $n$, the limit $L$ must satisfy $L \geq \sqrt{a}$.
Taking the limit as $n\to\infty$ in the recursive definition:
$$L = \frac{L+a/L}{2}.$$Multiplying by $2L$ (note $L \ge \sqrt{a} > 0$, so $L \neq 0$):$$2L^2 = L^2+a$$$$L^2 = a$$$$L = \pm\sqrt{a}.$$
Since we know $L \geq \sqrt{a}$, we must have $L=\sqrt{a}$.
Thus, $L_n$ (i.e., $x_n$) converges to $\sqrt{a}$ (so $u=\sqrt{a}$).

## Problem 4

Let $K=[0,1]$, and $C(K)$ be the set of all real valued continuous functions on $K$. Recall that the distance function
$$d(f,g)=\sup\limits_{x\in K}|f(x)-g(x)|,\quad\forall f,g\in C(K)$$
makes $C(K)$ a metric space. Show that $C(K)$ is a complete metric space, and show that $C(K)$ is not sequentially compact (i.e. give an example of a sequence in $C(K)$ where there is no convergent subsequence).

### Answer 4

**(Completeness of $C(K)$)** (See Rudin Thm 7.8)
To show that $C(K)$ is complete, we need to show that every Cauchy sequence in $C(K)$ converges to a limit in $C(K)$.
Suppose $(f_{n})$ is a Cauchy sequence in $C(K)$. This means that for any $\epsilon > 0$, there exists an integer $N$ such that for all $n, m > N$, $d(f_n, f_m) = \sup_{x\in K}|f_n(x)-f_m(x)| \leq \epsilon$.

1.  **Pointwise convergence:** For each fixed $x \in K$, the inequality $|f_n(x)-f_m(x)| \leq \epsilon$ for $n,m > N$ implies that the sequence of real numbers $(f_n(x))$ is a Cauchy sequence in $\mathbb{R}$. Since $\mathbb{R}$ is complete, $(f_n(x))$ converges. Let $f(x) = \lim_{n\to\infty} f_n(x)$ for each $x \in K$. This defines a function $f: K \to \mathbb{R}$.

2.  **Uniform convergence:** We need to show that $f_n \to f$ uniformly on $K$.
    Since $(f_n)$ is Cauchy in $C(K)$, for any $\epsilon > 0$, there exists $N$ such that for all $n, m > N$ and for all $x \in K$,
    $$|f_n(x)-f_m(x)|\leq\epsilon.$$
    Let $m \to \infty$ in this inequality. Since $f_m(x) \to f(x)$ for each $x$, we get, for $n > N$ and for all $x \in K$:
    $$|f_n(x)-f(x)|\leq\epsilon.$$
    This means $\sup_{x\in K}|f_n(x)-f(x)| \leq \epsilon$ for all $n > N$. This is precisely the definition of uniform convergence, i.e., $f_n \to f$ in the metric $d$.

3.  **Continuity of the limit function $f$:** Since each $f_n$ is continuous on $K$ and $f_n \to f$ uniformly on $K$, the limit function $f$ is also continuous on $K$. Thus, $f \in C(K)$.

Therefore, every Cauchy sequence in $C(K)$ converges to a function in $C(K)$, so $C(K)$ is a complete metric space.

**(Non-sequential compactness of $C(K)$)**
To show that $C(K)$ is not sequentially compact, we need to provide an example of a sequence in $C(K)$ that has no convergent subsequence.
Consider $K=[0,1]$. Let $f_n(x) = x^n$ for $n=1, 2, \dots$.
Each $f_n$ is continuous on $[0,1]$, so $f_n \in C(K)$.
The sequence $(f_n)$ is bounded in $C(K)$ since $d(f_n, 0) = \sup_{x\in[0,1]} |x^n| = 1$ for all $n \ge 1$.
The pointwise limit of this sequence is $f(x) = \begin{cases} 0 & \text{if } 0 \le x < 1 \\ 1 & \text{if } x=1 \end{cases}$.
This limit function $f(x)$ is not continuous on $[0,1]$.
If a subsequence $(f_{n_k})$ were to converge in $C(K)$ to some function $g \in C(K)$, then it must converge uniformly to $g$. Uniform convergence implies pointwise convergence, so $g(x)$ would have to be $f(x)$. But $f(x)$ is not in $C(K)$, which is a contradiction. Therefore, no subsequence of $(f_n)$ can converge in $C(K)$.
Thus, $C(K)$ is not sequentially compact.

*(The original answer key mentioned $f_n(x)=n$. For $K=[0,1]$, if $f_n(x)=n$ is interpreted as the constant function, then $d(f_n, f_m) = |n-m|$. This sequence is unbounded in $C(K)$ and is not Cauchy, so it has no convergent subsequence. The example $f_n(x)=x^n$ is a bounded sequence that still has no convergent subsequence in $C(K)$ because its pointwise limit is discontinuous, preventing uniform convergence to a continuous function.)*

## Problem 5

Is it true that, if $f:(0,1)\to\mathbb{R}$ is uniformly continuous then $f$ is bounded? If false, give a counter-example; if true, give a proof.

### Answer 5

True.
If $f:(0,1)\to\mathbb{R}$ is uniformly continuous, then for any $\epsilon > 0$, there exists a $\delta > 0$ such that for all $x, y \in (0,1)$, if $|x-y| < \delta$, then $|f(x)-f(y)| < \epsilon$.

Let $\epsilon = 1$. Then there exists a $\delta_1 > 0$ such that if $|x-y| < \delta_1$, then $|f(x)-f(y)| < 1$.
Choose an integer $N$ such that $N > 1/\delta_1$. This means $1/N < \delta_1$.
Cover the interval $(0,1)$ by $N$ subintervals. For example, let $x_k = k/N$ for $k=0, 1, \dots, N$. These points define intervals $[x_k, x_{k+1}]$ of length $1/N$. However, since the domain is $(0,1)$, we need to be slightly more careful or use points within $(0,1)$.

Let $x_0 \in (0,1)$ be any fixed point (e.g., $x_0 = 1/2$).
For any $x \in (0,1)$, the distance $|x-x_0| < 1$.
We can find a sequence of points $y_0, y_1, \dots, y_m$ such that $y_0 = x_0$, $y_m = x$, and $|y_j - y_{j-1}| < \delta_1$ for all $j=1, \dots, m$. The number of steps, $m$, can be chosen such that $m \leq \lceil |x-x_0|/\delta_1 \rceil +1 \leq \lceil 1/\delta_1 \rceil + 1$. Let $M = \lceil 1/\delta_1 \rceil + 1$. So $m \leq M$.
Then,
$$|f(x) - f(x_0)| = |f(y_m) - f(y_0)| = \left|\sum_{j=1}^m (f(y_j) - f(y_{j-1}))\right|$$
$$ \leq \sum_{j=1}^m |f(y_j) - f(y_{j-1})| < \sum_{j=1}^m 1 = m \leq M.$$
So, $|f(x) - f(x_0)| < M$.
This implies $|f(x)| < |f(x_0)| + M$.
Since $x_0$ is fixed, $f(x_0)$ is a fixed value. $M$ is a fixed positive integer (dependent on $\epsilon=1$ via $\delta_1$).
Thus, $f(x)$ is bounded on $(0,1)$.

## Problem 6

Let $f$ be a periodic continuous function on $\mathbb{R}$ with period $T=1$, i.e $f(x+1)=f(x)$ for all $x\in\mathbb{R}$. Show that for any $c\in(0,1)$, there exists an $x\in\mathbb{R}$ such that $f(x)=f(x+c)$.

### Answer 6

Define a new function $g(x) = f(x+c) - f(x)$. We want to show that there exists an $x \in \mathbb{R}$ such that $g(x)=0$.
Since $f$ is continuous, $g$ is also continuous.
Also, $f$ is periodic with period 1. Let's check if $g$ is periodic:
$g(x+1) = f(x+1+c) - f(x+1) = f(x+c) - f(x) = g(x)$.
So $g(x)$ is also periodic with period 1.

Consider the integral of $g(x)$ over one period, for example, from $0$ to $1$:
$$\int_0^1 g(x) dx = \int_0^1 (f(x+c) - f(x)) dx = \int_0^1 f(x+c) dx - \int_0^1 f(x) dx$$
For the first integral $\int_0^1 f(x+c) dx$, let $u = x+c$. Then $du = dx$.
When $x=0$, $u=c$. When $x=1$, $u=1+c$.
So, $\int_0^1 f(x+c) dx = \int_c^{1+c} f(u) du$.
Since $f$ is periodic with period 1, $\int_c^{1+c} f(u) du = \int_0^1 f(u) du$. (The definite integral of a periodic function over any interval of length equal to its period is constant).
Therefore,
$$\int_0^1 g(x) dx = \int_0^1 f(u) du - \int_0^1 f(x) dx = 0.$$
Since $g(x)$ is a continuous function and its integral over a period is 0, one of the following must be true:
1.  $g(x) = 0$ for all $x \in \mathbb{R}$. In this case, $f(x)=f(x+c)$ for all $x$.
2.  $g(x)$ takes both positive and negative values. If $g(x_1) > 0$ for some $x_1$ and $g(x_2) < 0$ for some $x_2$, then by the Intermediate Value Theorem, there must be an $x$ between $x_1$ and $x_2$ (or $x_1$ and $x_2$ possibly shifted by periods) such that $g(x)=0$.
If $g(x)$ is not identically zero, but, say, $g(x) \ge 0$ for all $x$ and $g(x_0)>0$ for some $x_0$, then $\int_0^1 g(x) dx > 0$, which contradicts the result that the integral is 0. Similarly if $g(x) \le 0$ for all $x$ and is not identically zero.
Thus, there must be some $x$ for which $g(x)=0$, meaning $f(x+c) - f(x) = 0$, or $f(x)=f(x+c)$.

**Alternative for $c=1/2$ (as suggested in the problem):**
Let $g(x) = f(x+1/2) - f(x)$.
Consider $g(x+1/2) = f(x+1/2+1/2) - f(x+1/2) = f(x+1) - f(x+1/2)$.
Since $f(x+1) = f(x)$, we have $g(x+1/2) = f(x) - f(x+1/2) = -(f(x+1/2) - f(x)) = -g(x)$.
So, $g(x+1/2) = -g(x)$.
If $g(x_0) = 0$ for some $x_0$, then we are done.
If $g(x) \neq 0$ for all $x$. Suppose $g(x_0) > 0$ for some $x_0$. Then $g(x_0+1/2) = -g(x_0) < 0$.
Since $g$ is continuous, and $g(x_0)$ and $g(x_0+1/2)$ have opposite signs, by the Intermediate Value Theorem, there must exist an $x^*$ in the interval $(x_0, x_0+1/2)$ such that $g(x^*) = 0$.

## Problem 7

Suppose $f$ is differentiable on $\mathbb{R}$, and $1\leq f^{\prime}(x)\leq2$ for all $x\in\mathbb{R}$ and $f(0)=0$. Show that $x\leq f(x)\leq2x$ for all $x>0$.

### Answer 7

Let $x > 0$. Since $f$ is differentiable on $\mathbb{R}$, it is continuous on $[0,x]$ and differentiable on $(0,x)$.
By the Mean Value Theorem (MVT), there exists a $c \in (0,x)$ such that
$$f'(c) = \frac{f(x) - f(0)}{x - 0}$$
Given that $f(0)=0$, this simplifies to
$$f'(c) = \frac{f(x)}{x}$$
We are also given that $1 \leq f'(y) \leq 2$ for all $y \in \mathbb{R}$. In particular, for $c \in (0,x)$, we have $1 \leq f'(c) \leq 2$.
Substituting $f'(c) = f(x)/x$, we get
$$1 \leq \frac{f(x)}{x} \leq 2$$
Since $x > 0$, we can multiply the inequality by $x$ without changing the direction of the inequalities:
$$x \cdot 1 \leq x \cdot \frac{f(x)}{x} \leq x \cdot 2$$
$$x \leq f(x) \leq 2x$$
This holds for all $x > 0$.

## Problem 8

Let $X$ be a metric space, and $A,B$ be two compact subsets of $X$. Is it true that $A\cap B$ is compact? If so, give a proof; if not, give a counter-example.

### Answer 8

True. $A \cap B$ is compact.

**Proof:**
Let $A$ and $B$ be two compact subsets of a metric space $X$.
In a metric space, a compact set is necessarily closed.
Therefore, $A$ is a closed set and $B$ is a closed set.

The intersection of any collection of closed sets is closed. Thus, $A \cap B$ is a closed set.
Since $A \cap B = \{x \in X \mid x \in A \text{ and } x \in B\}$, it follows that $A \cap B \subseteq A$.
So, $A \cap B$ is a closed subset of the compact set $A$.
A fundamental property of compact sets in a metric space (or Hausdorff space) is that any closed subset of a compact set is itself compact.
Since $A$ is compact and $A \cap B$ is a closed subset of $A$, $A \cap B$ must be compact.

## Problem 9
$$h(x)=\frac{1}{e^x-1}-\frac{1}{x}.\:\mathrm{Compute}\:\lim_{x\to0}h(x).$$

### Answer 9

We want to compute $\lim_{x\to0}h(x)$ where $h(x)=\frac{1}{e^x-1}-\frac{1}{x}$.
First, combine the terms into a single fraction:
$$h(x) = \frac{x - (e^x-1)}{x(e^x-1)} = \frac{x - e^x + 1}{xe^x-x}$$
As $x \to 0$:
Numerator: $0 - e^0 + 1 = 0 - 1 + 1 = 0$.
Denominator: $0 \cdot e^0 - 0 = 0 - 0 = 0$.
This is an indeterminate form of type $\frac{0}{0}$, so we can apply L'Hôpital's Rule.

Let $N(x) = x - e^x + 1$ and $D(x) = xe^x - x$.
$N'(x) = \frac{d}{dx}(x - e^x + 1) = 1 - e^x$.
$D'(x) = \frac{d}{dx}(xe^x - x) = (1 \cdot e^x + x \cdot e^x) - 1 = e^x + xe^x - 1$.

So, $\lim_{x\to0} h(x) = \lim_{x\to0} \frac{N'(x)}{D'(x)} = \lim_{x\to0} \frac{1-e^x}{e^x+xe^x-1}$.
Substitute $x=0$ into the new numerator and denominator:
New Numerator: $1 - e^0 = 1 - 1 = 0$.
New Denominator: $e^0 + 0 \cdot e^0 - 1 = 1 + 0 - 1 = 0$.
This is again an indeterminate form $\frac{0}{0}$, so we apply L'Hôpital's Rule a second time.

Let $N_1(x) = 1 - e^x$ and $D_1(x) = e^x + xe^x - 1$.
$N_1'(x) = \frac{d}{dx}(1 - e^x) = -e^x$.
$D_1'(x) = \frac{d}{dx}(e^x + xe^x - 1) = e^x + (1 \cdot e^x + x \cdot e^x) - 0 = e^x + e^x + xe^x = 2e^x + xe^x$.

So, $\lim_{x\to0} h(x) = \lim_{x\to0} \frac{N_1'(x)}{D_1'(x)} = \lim_{x\to0} \frac{-e^x}{2e^x+xe^x}$.
Now, substitute $x=0$:
$$\frac{-e^0}{2e^0 + 0 \cdot e^0} = \frac{-1}{2 \cdot 1 + 0} = \frac{-1}{2}$$
Thus, $\lim_{x\to0}h(x) = -1/2$.

## Problem 10

Let $f_{n}(x)=\frac{n+\sin(x)}{2n+\sin^{2}x}$ for $x\in\mathbb{R}$. Compute
$$\operatorname*{lim}_{n\to\infty}\int_{1}^{2}f_{n}(x)dx.$$
(The following 'squeezing lemma' may be useful: if there exist sequences of functions $g_{n}(x),h_{n}(x)$, such that $g_{n}(x)\leq f_{n}(x)\leq h_{n}(x)$ and $g_{n}$ and $h_{n}$ converges to $f$ uniformly, then $f_{n}\to f$ uniformly).

### Answer 10

We need to compute $\operatorname*{lim}_{n\to\infty}\int_{1}^{2}f_{n}(x)dx$ for $f_{n}(x)=\frac{n+\sin(x)}{2n+\sin^{2}x}$.

1.  **Find the pointwise limit of $f_n(x)$:**
    Divide the numerator and denominator by $n$:
    $$f_n(x) = \frac{1+\frac{\sin(x)}{n}}{2+\frac{\sin^{2}(x)}{n}}$$
    As $n\to\infty$, $\frac{\sin(x)}{n} \to 0$ and $\frac{\sin^{2}(x)}{n} \to 0$ (since $|\sin(x)| \leq 1$ and $\sin^2(x) \leq 1$).
    So, the pointwise limit is $f(x) = \lim_{n\to\infty} f_n(x) = \frac{1+0}{2+0} = \frac{1}{2}$.

2.  **Check for uniform convergence on $[1,2]$:**
    We need to evaluate $|f_n(x) - f(x)|$:
    \begin{align*} |f_n(x) - \frac{1}{2}| &= \left| \frac{n+\sin(x)}{2n+\sin^{2}(x)} - \frac{1}{2} \right| \\ &= \left| \frac{2(n+\sin x) - (2n+\sin^2 x)}{2(2n+\sin^2 x)} \right| \\ &= \left| \frac{2n+2\sin x - 2n - \sin^2 x}{4n+2\sin^2 x} \right| \\ &= \left| \frac{2\sin x - \sin^2 x}{4n+2\sin^2 x} \right|\end{align*}
    Let $g(s) = 2s - s^2$ for $s = \sin x \in [-1, 1]$.
    $g'(s) = 2-2s$. $g'(s)=0 \implies s=1$.
    Values at endpoints and critical point: $g(1)=2(1)-1^2=1$. $g(-1)=2(-1)-(-1)^2 = -2-1=-3$.
    So, the maximum absolute value of the numerator $2\sin x - \sin^2 x$ on $[-1,1]$ is $|-3|=3$.
    For the denominator, $4n+2\sin^2 x \geq 4n + 2(0) = 4n$ (since $\sin^2 x \ge 0$).
    Thus,
    $$|f_n(x) - \frac{1}{2}| \leq \frac{3}{4n}$$
    Since $\lim_{n\to\infty} \frac{3}{4n} = 0$, and this bound $\frac{3}{4n}$ is independent of $x$, the sequence $f_n(x)$ converges uniformly to $f(x)=1/2$ on $\mathbb{R}$, and therefore on $[1,2]$.

3.  **Interchange limit and integral:**
    Since $f_n(x) \to f(x)=1/2$ uniformly on $[1,2]$, and each $f_n(x)$ is continuous (as $\sin x, \sin^2 x$ are continuous and $2n+\sin^2 x \ge 2n > 0$ for $n \ge 1$), we can interchange the limit and the integral:
    $$\operatorname*{lim}_{n\to\infty}\int_{1}^{2}f_{n}(x)dx = \int_{1}^{2}\left(\operatorname*{lim}_{n\to\infty}f_{n}(x)\right)dx$$
    $$= \int_{1}^{2}\frac{1}{2}dx$$
    $$= \left[ \frac{1}{2}x \right]_{1}^{2} = \frac{1}{2}(2) - \frac{1}{2}(1) = 1 - \frac{1}{2} = \frac{1}{2}$$
    The limit is $1/2$.