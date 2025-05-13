**Problem 1 (10 points)**

Compute $\lim_{n\to\infty} a_n^{1/n}$ where
$$a_n=\frac{(0.3)^n+(0.7)^n}{1+(0.8)^n}.$$

**Answer 1**

In the numerator, the term $(0.7)^n$ is more important than $(0.3)^n$. In the denominator, the term 1 is more important than $(0.8)^n$. So intuitively, one can approximate the expression for $a_n$ as $(0.7)^n$. More precisely, we can write
$$a_n=(0.7)^n\frac{1+(0.3/0.7)^n}{1+(0.8)^n}=0.7^n b_n$$
where $b_n = \frac{1+(0.3/0.7)^n}{1+(0.8)^n}$. We can show $b_n \to 1$ as $n \to \infty$. Since for any $x>0$, we have $x^{1/n} \to 1$ as $n \to \infty$, hence $\lim_{n\to\infty} b_n^{1/n}=1$. Hence
$$\lim_{n\to\infty} a_n^{1/n} = \lim_{n\to\infty} [ (0.7)^n b_n ]^{1/n} = \lim_{n\to\infty} (0.7) b_n^{1/n} = 0.7 \times 1 = 0.7.$$

**Problem 2 (10 points)**

Suppose $a_{n}>0$ and $\sum_{n=1}^{\infty} a_{n}$ converges. Prove that
$$\sum_{n=1}^{\infty} \frac{(-1)^n a_n + a_{2n}}{2}$$
converges.

**Answer 2**

We are asked to prove that $\sum_{n=1}^{\infty} \frac{(-1)^n a_n + a_{2n}}{2}$ converges. This is equivalent to proving that $\frac{1}{2} \sum_{n=1}^{\infty} (-1)^n a_n + \frac{1}{2} \sum_{n=1}^{\infty} a_{2n}$ converges. This will be true if both individual series $\sum_{n=1}^{\infty} (-1)^n a_n$ and $\sum_{n=1}^{\infty} a_{2n}$ converge.

1.  Consider the series $\sum_{n=1}^{\infty} (-1)^n a_n$.
    Since $a_n > 0$ and $\sum_{n=1}^{\infty} a_n$ converges, this means the series $\sum_{n=1}^{\infty} |(-1)^n a_n| = \sum_{n=1}^{\infty} a_n$ converges. By definition, this means the series $\sum_{n=1}^{\infty} (-1)^n a_n$ converges absolutely. Every absolutely convergent series is convergent. Thus, $\sum_{n=1}^{\infty} (-1)^n a_n$ converges.

2.  Consider the series $\sum_{n=1}^{\infty} a_{2n}$.
    Since $a_n > 0$ and $\sum_{n=1}^{\infty} a_n$ converges, the terms $a_{2n}$ are all positive. Also, for any partial sum $S_N = \sum_{n=1}^{N} a_{2n}$, we have $S_N = a_2 + a_4 + \dots + a_{2N} \le a_1 + a_2 + \dots + a_{2N} \le \sum_{k=1}^{\infty} a_k$. Since $\sum_{k=1}^{\infty} a_k$ converges to a finite value, the partial sums of $\sum a_{2n}$ are bounded above. As all terms $a_{2n}$ are positive, the sequence of partial sums is also non-decreasing. A non-decreasing sequence that is bounded above must converge. Thus, $\sum_{n=1}^{\infty} a_{2n}$ converges.

Since both $\sum_{n=1}^{\infty} (-1)^n a_n$ and $\sum_{n=1}^{\infty} a_{2n}$ converge, their linear combination
$$ \sum_{n=1}^{\infty} \frac{(-1)^n a_n + a_{2n}}{2} = \frac{1}{2} \sum_{n=1}^{\infty} (-1)^n a_n + \frac{1}{2} \sum_{n=1}^{\infty} a_{2n} $$
also converges.

**Problem 3 (10 points)**

Fix a positive number $a$, and choose $x_{1} > \sqrt{a}$. Define $x_{2}, x_{3}, \cdots$ iteratively by
$$x_{n+1} = \frac{1}{2} \left( x_n + \frac{a}{x_n} \right).$$
Prove that the sequence $(x_n)$ converges to $\sqrt{a}$. Hint: for any $x, y > 0$, we have $(x+y)/2 \ge \sqrt{xy}$.

**Answer 3**

We first prove that $x_n \ge \sqrt{a}$ for all $n \ge 1$. $x_1 > \sqrt{a}$ is given. Assume $x_k \ge \sqrt{a}$ for some $k \ge 1$. Then by the AM-GM inequality (the hint with $x=x_k, y=a/x_k$),
$$x_{k+1} = \frac{1}{2} \left( x_k + \frac{a}{x_k} \right) \ge \sqrt{x_k \cdot \frac{a}{x_k}} = \sqrt{a}.$$
So, by induction, $x_n \ge \sqrt{a}$ for all $n$. (Since $x_1 > \sqrt{a}$, $x_2 \ge \sqrt{a}$, etc.)

We then prove that $x_{n+1} \le x_n$ for $n \ge 1$.
$$x_n - x_{n+1} = x_n - \frac{1}{2} \left( x_n + \frac{a}{x_n} \right) = \frac{1}{2} \left( x_n - \frac{a}{x_n} \right) = \frac{x_n^2 - a}{2x_n}.$$
Since $x_n \ge \sqrt{a}$ (for $n \ge 1$, and for $n \ge 2$ if $x_1$ was just $>\sqrt{a}$ but not necessarily $\ge \sqrt{a}$... actually $x_n \ge \sqrt{a}$ holds for $n \ge 1$ from step 1 if we consider $x_1$ as the base case in a loose sense, or more strictly $x_n \ge \sqrt{a}$ for $n \ge 2$, and the sequence is decreasing from $x_2$ onwards), we have $x_n^2 \ge a$. So $x_n^2 - a \ge 0$. Also $x_n > 0$. Thus $x_n - x_{n+1} \ge 0$, which means $x_{n+1} \le x_n$ for $n \ge 1$.

Since $(x_n)_{n \ge 1}$ is a monotone decreasing sequence (or non-increasing) and is bounded from below by $\sqrt{a}$, the sequence $(x_n)$ converges. Let $x = \lim_{n\to\infty} x_n$ denote the limit. Since $x_n \ge \sqrt{a}$ for all $n$, the limit $x$ must satisfy $x \ge \sqrt{a}$. Consider the relation $x_{n+1} = \frac{1}{2} (x_n + a/x_n)$. Letting $n \to \infty$ on both sides, we have
$$x = \frac{1}{2} \left( x + \frac{a}{x} \right).$$
Solving for $x$:
$$2x = x + \frac{a}{x}$$
$$x = \frac{a}{x}$$
$$x^2 = a$$
Since $x \ge \sqrt{a}$ (and thus $x>0$), we must have $x = \sqrt{a}$.

**Problem 4 (10 points)**

Let $K=[0,1]$, and $C(K)$ be the set of all real-valued continuous functions on $K$. Recall that the distance function
$$d(f,g)=\sup_{x\in K}|f(x)-g(x)|, \quad \forall f, g \in C(K)$$
makes $C(K)$ a metric space. Show that $C(K)$ is a *complete metric space*, and show that $C(K)$ is **not sequentially** **compact** (i.e., give an example of a sequence in $C(K)$ where there is no convergent subsequence).

**Answer 4**

To show that $C(K)$ is complete, one needs to show that every Cauchy sequence in $C(K)$ is convergent. 
- Suppose $(f_n)$ is a Cauchy sequence in $C(K)$. Then for any $\epsilon > 0$, there exists $N_0$ such that for all $n, m > N_0$, $$d(f_n, f_m) = \sup_{x\in K} |f_n(x) - f_m(x)| \le \epsilon$$.
- *This implies that for each fixed $x \in K$, the sequence of real numbers $(f_n(x))$ is a Cauchy sequence in $\mathbb{R}$. Since $\mathbb{R}$ is complete, this sequence converges.* Let $f(x) = \lim_{n\to\infty} f_n(x)$ for each $x \in K$. This defines a function $f: K \to \mathbb{R}$.

Now we need to show *that $f_n \to f$ uniformly*, and *that $f \in C(K)$.*
- From the Cauchy condition, for any $\epsilon > 0$, there exists $N_0$ such that for all $n, m > N_0$ and any $x \in K$, we have $|f_n(x) - f_m(x)| \le \epsilon$.
- Fix $n > N_0$ and let $m \to \infty$ in the inequality. Since $f_m(x) \to f(x)$ for each $x$, we get
$$|f_n(x) - f(x)| \le \epsilon, \quad \forall x \in K, \forall n > N_0.$$
- This shows that $f_n \to f$ uniformly on $K$. Since each $f_n$ is *continuous* on $K$ and the convergence $f_n \to f$ is *uniform* on $K$, the *limit function $f$ is also continuous* on $K$. Thus $f \in C(K)$.
We have shown that the Cauchy sequence $(f_n)$ converges to $f \in C(K)$ in the metric $d$. Therefore, $C(K)$ is a complete metric space.

To show that $C(K)$ is not sequentially compact, we give an example of a sequence in $C(K)$ that has *no convergent subsequence.* 
- Consider the sequence of constant functions $f_n(x) = n$ for all $x \in K=[0,1]$. Each $f_n$ is continuous, so $f_n \in C(K)$.
- A sequence in a metric space that has a convergent *subsequence* must be bounded.
- The distance of $f_n$ from the zero function $\mathbf{0}(x)=0$ is $$d(f_n, \mathbf{0}) = \sup_{x\in K} |n - 0| = n$$
- Since $d(f_n, \mathbf{0}) = n \to \infty$ as $n \to \infty$, the sequence $(f_n)$ is unbounded in $C(K)$.
- An *unbounded* sequence cannot have a convergent subsequence (as any convergent sequence is necessarily bounded).
**Therefore, $C(K)$ is not sequentially compact.**

>[! 直观感受总结]
> 
> **1. 完备性 (Completeness)**
> 
> * $C([0,1])$ 足够“完整”。
> * 如果一个连续函数序列看起来想要“稳定下来”（即它们彼此之间的最大差距趋于0，形成柯西序列），那么它们总是能够成功地稳定下来，并且最终形成的那个极限函数也必定是一个连续函数，仍然属于 $C([0,1])$ 这个“连续函数的大家庭”。
> * 这个空间里没有因为“极限是非连续函数”而产生的“洞”或“缺陷”。
> 
> **2. 非序列紧性 (Not Sequentially Compact)**
> 
> * $C([0,1])$ 太“大”或太“自由”了，以至于它不具备序列紧性。
> * 这意味着我们可以找到一些身处 $C([0,1])$ 中的连续函数序列，但它们的任何一部分（子序列）都无法在 $C([0,1])$ 内部找到一个“归宿”（即收敛点）。具体表现为两种情况：
>     * **“整体跑远”型**：函数序列中的函数可以整体地“跑到无穷远”，例如 $f_n(x)=n$。这些函数的图像（水平线）不断上升，没有任何一个子序列能够稳定并收敛到一个固定的连续函数。
>     * **“试图变形/突破次元壁”型**：函数序列中的函数可能试图“演变”或“收敛”到一个不再是连续函数的形状，例如 $f_n(x)=x^n$。这个序列在逐点意义上想变成一个在 $x=1$ 处有跳跃的函数。由于这个“目标形状”不属于 $C([0,1])$（因为它不连续），所以没有任何子序列能够（在 $\sup$ 范数的意义下，即一致收敛）收敛到一个 $C([0,1])$ 中的成员。

**Problem 5 (10 points)**

Is it true that if $f:(0,1) \to \mathbb{R}$ is uniformly continuous, then $f$ is bounded? If false, give a counter-example; if true, give a proof.

**Answer 5**

It is true.
- If $f:(0,1) \to \mathbb{R}$ is uniformly continuous, then for any $\epsilon > 0$, there exists a $\delta > 0$ such that for any $x, y \in (0,1)$ with $|x-y| < \delta$, we have $|f(x) - f(y)| < \epsilon$.
- Fix $\epsilon = 1$. Then there exists a $\delta > 0$ such that if $x, y \in (0,1)$ and $|x-y| < \delta$, then $|f(x) - f(y)| < 1$.
- Let $N$ be a positive integer such that $N > 1/\delta$. This implies $1/N < \delta$.
- Fix a point $x_0 \in (0,1)$, for example $x_0 = 1/2$. For any $y \in (0,1)$, we want to bound $|f(y)|$.
	- The distance $|y - x_0| < 1$. *We can divide the interval between $y$ and $x_0$ into at most $N$ subintervals of length less than $1/N$* (and thus less than $\delta$).
	- Let $y \in (0,1)$. Define $M = \lceil |y-x_0| / (1/N) \rceil$. Since $|y-x_0| < 1$, $M \le N$.
- Consider a sequence of points $z_0 = y, z_1, \dots, z_M = x_0$ such that $z_k = y + k \frac{x_0-y}{M}$
	- Then $|z_k - z_{k-1}| = \frac{|x_0-y|}{M} \le \frac{|x_0-y|}{\lceil |y-x_0|N \rceil} \le \frac{|x_0-y|}{|y-x_0|N} = \frac{1}{N} < \delta$.
	- Thus, $|f(z_k) - f(z_{k-1})| < 1$ for each $k=1, \dots, M$.
	- Now, consider the difference $|f(y) - f(x_0)|$:
$$|f(y) - f(x_0)| = |f(z_0) - f(z_M)| = \left| \sum_{k=1}^M (f(z_{k-1}) - f(z_k)) \right|$$
	- By the triangle inequality:
$$ \le \sum_{k=1}^M |f(z_{k-1}) - f(z_k)| < \sum_{k=1}^M 1 = M.$$
- Since $M \le N$, we have $|f(y) - f(x_0)| < N$.
- This implies $|f(y)| - |f(x_0)| \le |f(y) - f(x_0)| < N$, so $|f(y)| < |f(x_0)| + N$.
- *Since $x_0$ is fixed (e.g., $1/2$), $f(x_0)$ is a fixed value. $N$ is also a fixed positive integer (depending only on $\delta$, which depends on $\epsilon=1$).*
- Thus, for any $y \in (0,1)$, $f(y)$ is bounded by $|f(1/2)| + N$. Therefore, $f$ is bounded on $(0,1)$.

>[!note]
>Here we need to control any $\lvert f(y) \rvert$ by splitting the interval $[y,x_{0}]$ into sub intervals with length $<\delta$ so that the $\lvert f(y) \rvert$ can eventually be controlled by $\lvert f(x_{0}) \rvert+N$.

**Problem 6 (10 points)**

Let $f$ be a periodic continuous function on $\mathbb{R}$ with period $T=1$, i.e., $f(x+1)=f(x)$ for all $x \in \mathbb{R}$. Show that for any $c \in (0,1)$, there exists an $x \in \mathbb{R}$ such that $f(x)=f(x+c)$. (If you wish, you can take $c=1/2$).

**Answer 6**

Define the function $g(x) = f(x+c) - f(x)$. We need to show that $g(x) = 0$ for some $x \in \mathbb{R}$.
- Since $f(x)$ is continuous and periodic with period 1, $g(x)$ is also continuous.
- Consider the integral of $g(x)$ over one period, say from an arbitrary $a$ to $a+1$:
$$\int_a^{a+1} g(x) dx = \int_a^{a+1} (f(x+c) - f(x)) dx = \int_a^{a+1} f(x+c) dx - \int_a^{a+1} f(x) dx.$$
- For the first integral, let $u = x+c$. Then $du=dx$. When $x=a, u=a+c$. When $x=a+1, u=a+1+c$.
- So, $\int_a^{a+1} f(x+c) dx = \int_{a+c}^{a+1+c} f(u) du$.
- Since $f$ is periodic with period 1, the integral of $f$ over any interval of length 1 is the same.
- Thus, $\int_{a+c}^{a+1+c} f(u) du = \int_a^{a+1} f(u) du$.
Therefore,
$$\int_a^{a+1} g(x) dx = \int_a^{a+1} f(u) du - \int_a^{a+1} f(x) dx = 0.$$
- If $g(x)$ is identically zero for all $x$, then $f(x+c)=f(x)$ for all $x$, and we are done.
- If $g(x)$ is not identically zero, then since $g(x)$ is continuous and its integral over any period is zero, $g(x)$ must take both positive and negative values within any period. (If $g(x)$ were always non-negative and not identically zero, its integral would be positive. If $g(x)$ were always non-positive and not identically zero, its integral would be negative.)
- Since $g(x)$ is continuous and takes both positive and negative values, by the Intermediate Value Theorem, there must exist some $x \in \mathbb{R}$ (e.g., within the interval $[a, a+1]$) such that $g(x)=0$. This means $f(x+c) - f(x) = 0$, or $f(x) = f(x+c)$.

For the specific case $c=1/2$:
- Define $g(x) = f(x+1/2) - f(x)$.
- Then $g(x+1/2) = f(x+1/2+1/2) - f(x+1/2) = f(x+1) - f(x+1/2)$.
- Since $f(x+1)=f(x)$, we have $$g(x+1/2) = f(x) - f(x+1/2) = -(f(x+1/2) - f(x)) = -g(x)$$.
So, $g(x+1/2) = -g(x)$.
- If $g(x_0) = 0$ for some $x_0$, we are done.
- If $g(x_0) \neq 0$ for all $x_0$. Suppose $g(x) > 0$ for some $x$. Then $g(x+1/2) = -g(x) < 0$. 
	- Since $g$ is continuous, and $g(x)$ and $g(x+1/2)$ have opposite signs, by the Intermediate Value Theorem, there must be some $x' \in (x, x+1/2)$ such that $g(x')=0$. 
	- A similar argument holds if $g(x) < 0$.
- Thus, unless $g(x)$ is identically zero (in which case the property holds for all $x$), there exists an $x'$ such that $g(x')=0$.

>[!Alternative proof] 
>I don't know why they give such an ugly proof for this. Just use MVT for intergrals and it's done.

**Proof:**

1.  Define the function $g(x) = f(x+c) - f(x)$. Since $f(x)$ is continuous on $\mathbb{R}$, and sums/differences/compositions of continuous functions are continuous, $g(x)$ is also continuous on $\mathbb{R}$. We want to show that $g(x) = 0$ for some $x \in \mathbb{R}$.

2.  Consider the integral of $g(x)$ over one period, for example, from $0$ to $1$ (any interval of length 1 will do, say $[a, a+1]$):
    $$\int_{0}^{1} g(x) dx = \int_{0}^{1} (f(x+c) - f(x)) dx = \int_{0}^{1} f(x+c) dx - \int_{0}^{1} f(x) dx.$$

3.  For the first integral, $\int_{0}^{1} f(x+c) dx$, let $u = x+c$. Then $du = dx$.
    When $x=0$, $u=c$.
    When $x=1$, $u=1+c$.
    So, $\int_{0}^{1} f(x+c) dx = \int_{c}^{1+c} f(u) du$.

4.  Since $f$ is periodic with period 1, the integral of $f$ over any interval of length 1 is the same. That is, $\int_{c}^{1+c} f(u) du = \int_{0}^{1} f(u) du$.
    (To see this, $\int_{c}^{1+c} f(u) du = \int_{c}^{1} f(u) du + \int_{1}^{1+c} f(u) du$. Let $v=u-1$ in the second part, then $dv=du$. When $u=1, v=0$. When $u=1+c, v=c$. So $\int_{1}^{1+c} f(u) du = \int_{0}^{c} f(v+1) dv = \int_{0}^{c} f(v) dv$. Thus $\int_{c}^{1+c} f(u) du = \int_{c}^{1} f(u) du + \int_{0}^{c} f(u) du = \int_{0}^{1} f(u) du$.)

5.  Therefore,
    $$\int_{0}^{1} g(x) dx = \int_{0}^{1} f(u) du - \int_{0}^{1} f(x) dx = 0.$$

6.  Now, we apply the **Mean Value Theorem for Integrals** to $g(x)$ on the interval $[0, 1]$.
    Since $g(x)$ is continuous on $[0, 1]$, there exists some $k \in [0, 1]$ such that:
    $$\int_{0}^{1} g(x) dx = g(k) \cdot (1-0)$$
    $$\int_{0}^{1} g(x) dx = g(k)$$

7.  From step 5, we know $\int_{0}^{1} g(x) dx = 0$.
    From step 6, we know $\int_{0}^{1} g(x) dx = g(k)$.
    Therefore, $g(k) = 0$.

8.  This means $f(k+c) - f(k) = 0$, or $f(k+c) = f(k)$ for some $k \in [0, 1]$ (and thus for some $k \in \mathbb{R}$).

This completes the proof.

**Problem 7 (10 points)**

Suppose $f$ is differentiable on $\mathbb{R}$, and $1 \le f'(x) \le 2$ for all $x \in \mathbb{R}$, and $f(0)=0$. Show that $x \le f(x) \le 2x$ for all $x > 0$.

**Answer 7**

We use the Mean Value Theorem. For any $x > 0$, $f$ is continuous on $[0, x]$ and differentiable on $(0, x)$ because it is differentiable on $\mathbb{R}$.
By the Mean Value Theorem, there exists some $c \in (0, x)$ such that
$$f'(c) = \frac{f(x) - f(0)}{x - 0}.$$
Given $f(0)=0$, this simplifies to
$$f'(c) = \frac{f(x)}{x}.$$
We are also given that $1 \le f'(y) \le 2$ for all $y \in \mathbb{R}$. Since $c \in (0,x)$, it follows that $1 \le f'(c) \le 2$.
Therefore,
$$1 \le \frac{f(x)}{x} \le 2.$$
Since $x > 0$, we can multiply all parts of the inequality by $x$ without changing the direction of the inequalities:
$$x \cdot 1 \le x \cdot \frac{f(x)}{x} \le x \cdot 2$$
$$x \le f(x) \le 2x.$$
This holds for all $x > 0$.

**Problem 8 (10 points)**

Let $X$ be a metric space, and $A, B$ be two compact subsets of $X$. Is it true that $A \cap B$ is compact? If so, give a proof; if not, give a counter-example.

**Answer 8**

True.
Let $A$ and $B$ be two compact subsets of a metric space $X$.
- In a metric space, a compact set is also *closed and bounded*. (More generally, in a Hausdorff space, any compact subset is closed).
- Since $A$ is compact in $X$ (a metric space, hence Hausdorff), $A$ is a closed subset of $X$.
- Similarly, $B$ is compact, so $B$ is a closed subset of $X$.
- *The intersection of two closed sets is closed.* Therefore, $A \cap B$ is a closed subset of $X$.
- Also, $A \cap B$ is a subset of $A$.
Since $A$ is compact and $A \cap B$ is a closed subset of the compact set $A$, it follows that $A \cap B$ is compact. (A closed subset of a compact set is compact).

Alternatively, using sequences:
1. Let $(x_n)$ be any sequence in $A \cap B$.
2. Since $x_n \in A \cap B$, it means $x_n \in A$ for all $n$. 
	1. Since $A$ is compact (and in a metric space, compact is equivalent to sequentially compact), there exists a subsequence $(x_{n_k})$ of $(x_n)$ such that $x_{n_k} \to x$ for some $x \in A$.
3. Now, the terms of this subsequence $(x_{n_k})$ are also in $B$ (since $x_n \in B$ for all $n$).
	1. Since $B$ is compact, it is closed. 
	2. Thus, the limit of a sequence of points in $B$ must also be in $B$. 
	3. Therefore, $x = \lim_{k\to\infty} x_{n_k}$ must also be in $B$.
4. So we have $x \in A$ and $x \in B$, which means $x \in A \cap B$.
5. We have shown that any sequence $(x_n)$ in $A \cap B$ has a subsequence $(x_{n_k})$ that converges to a limit $x$ which is also in $A \cap B$. 
*This means $A \cap B$ is sequentially compact, and thus compact.*

**Problem 9 (10 points)**

Let $h(x) = \frac{1}{e^x - 1} - \frac{1}{x}$. Compute $\lim_{x\to0} h(x)$.

**Answer 9**

First, combine the terms:
$$h(x) = \frac{1}{e^x - 1} - \frac{1}{x} = \frac{x - (e^x - 1)}{x(e^x - 1)} = \frac{x - e^x + 1}{xe^x - x}.$$
As $x \to 0$:
The numerator $x - e^x + 1 \to 0 - e^0 + 1 = 0 - 1 + 1 = 0$.
The denominator $xe^x - x \to 0 \cdot e^0 - 0 = 0 - 0 = 0$.
Since we have the indeterminate form $0/0$, we can apply L'Hôpital's Rule.
Let $N(x) = x - e^x + 1$ and $D(x) = xe^x - x$.
Then $N'(x) = \frac{d}{dx}(x - e^x + 1) = 1 - e^x$.
And $D'(x) = \frac{d}{dx}(xe^x - x) = (1 \cdot e^x + x \cdot e^x) - 1 = e^x + xe^x - 1$.
So, $\lim_{x\to0} h(x) = \lim_{x\to0} \frac{1 - e^x}{e^x + xe^x - 1}$.
As $x \to 0$:
The new numerator $1 - e^x \to 1 - e^0 = 1 - 1 = 0$.
The new denominator $e^x + xe^x - 1 \to e^0 + 0 \cdot e^0 - 1 = 1 + 0 - 1 = 0$.
We again have the indeterminate form $0/0$, so we apply L'Hôpital's Rule again.
Let $N''(x) = \frac{d}{dx}(1 - e^x) = -e^x$.
Let $D''(x) = \frac{d}{dx}(e^x + xe^x - 1) = e^x + (1 \cdot e^x + x \cdot e^x) = e^x + e^x + xe^x = 2e^x + xe^x$.
So, $\lim_{x\to0} h(x) = \lim_{x\to0} \frac{-e^x}{2e^x + xe^x}$.
Now, substitute $x=0$:
$$\frac{-e^0}{2e^0 + 0 \cdot e^0} = \frac{-1}{2(1) + 0} = \frac{-1}{2}.$$
Therefore, $\lim_{x\to0} h(x) = -1/2$.

**Problem 10 (10 points)**

Let $f_n(x) = \frac{n+\sin(x)}{2n+\sin^2(x)}$ for $x \in \mathbb{R}$. Compute $\lim_{n\to\infty} \int_{1}^{2} f_n(x) dx$.

**Answer 10**

First, find the pointwise limit of $f_n(x)$ as $n \to \infty$. For a fixed $x \in \mathbb{R}$:
$$f_n(x) = \frac{n+\sin(x)}{2n+\sin^2(x)} = \frac{n(1 + \frac{\sin x}{n})}{n(2 + \frac{\sin^2 x}{n})} = \frac{1 + \frac{\sin x}{n}}{2 + \frac{\sin^2 x}{n}}.$$
As $n \to \infty$, $\frac{\sin x}{n} \to 0$ and $\frac{\sin^2 x}{n} \to 0$ (since $\sin x$ and $\sin^2 x$ are bounded).
So, the *pointwise limit function* is $f(x) = \lim_{n\to\infty} f_n(x) = \frac{1+0}{2+0} = \frac{1}{2}$.

>[!caution]
>为了能够合法地将极限符号移到积分符号内部，我们需要比逐点收敛更强的条件。**一致收敛**是这样一个常用的充分条件

Next, we check for *uniform convergence* on $[1, 2]$.
Consider $|f_n(x) - f(x)|$:
$$|f_n(x) - \frac{1}{2}| = \left| \frac{n+\sin x}{2n+\sin^2 x} - \frac{1}{2} \right| = \left| \frac{2(n+\sin x) - (2n+\sin^2 x)}{2(2n+\sin^2 x)} \right|$$
$$= \left| \frac{2n+2\sin x - 2n - \sin^2 x}{4n+2\sin^2 x} \right| = \left| \frac{2\sin x - \sin^2 x}{4n+2\sin^2 x} \right|.$$
Since $-1 \le \sin x \le 1$ and $0 \le \sin^2 x \le 1$:
The numerator $|2\sin x - \sin^2 x| \le |2\sin x| + |-\sin^2 x| \le 2|\sin x| + \sin^2 x \le 2(1) + 1 = 3$.
The denominator $4n+2\sin^2 x \ge 4n + 2(0) = 4n$.
So, for all $x \in \mathbb{R}$ (and thus for $x \in [1,2]$):
$$|f_n(x) - \frac{1}{2}| \le \frac{3}{4n}.$$
Since $\lim_{n\to\infty} \frac{3}{4n} = 0$, and *this bound does not depend on $x$*, the sequence $(f_n)$ converges uniformly to $f(x)=1/2$ on $\mathbb{R}$, and therefore on $[1,2]$.

*Since $f_n(x)$ converges uniformly to $f(x)=1/2$ on $[1,2]$ and each $f_n(x)$ is continuous* (as $\sin x$ and $\sin^2 x$ are continuous, and the denominator $2n+\sin^2 x \ge 2n > 0$ for $n \ge 1$), we can *interchange the limit and the integral:*
$$\lim_{n\to\infty} \int_{1}^{2} f_n(x) dx = \int_{1}^{2} \lim_{n\to\infty} f_n(x) dx = \int_{1}^{2} f(x) dx.$$
Substituting $f(x) = 1/2$:
$$\int_{1}^{2} \frac{1}{2} dx = \left[ \frac{1}{2}x \right]_{1}^{2} = \frac{1}{2}(2) - \frac{1}{2}(1) = 1 - \frac{1}{2} = \frac{1}{2}.$$
Thus, $\lim_{n\to\infty} \int_{1}^{2} f_n(x) dx = 1/2$.