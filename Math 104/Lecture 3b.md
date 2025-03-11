# 3. Completeness, Compactness

A sequence $(x_n)$ in a set $X$ is a function $f: \mathbb{N} \to X$, where $x_n = f(n)$ is the $n$th term in the sequence.

**Definition 3.1.** Let $(X, d)$ be a metric space. A sequence $(x_n)$ in $X$ converges to $x \in X$, written $x_n \to x$ as $n \to \infty$ or:

$$
\lim_{n \to \infty} x_n = x,
$$

if for every $\epsilon > 0$ there exists $N \in \mathbb{N}$ such that:

$$
n > N \implies d(x_n, x) < \epsilon.
$$

That is, $x_n \to x$ in $X$ if $d(x_n, x) \to 0$ in $\mathbb{R}$. Equivalently, $x_n \to x$ as $n \to \infty$ if for every neighborhood $U$ of $x$ there exists $N \in \mathbb{N}$ such that $x_n \in U$ for all $n > N$.

**Example 3.1.** If $d$ is the discrete metric on a set $X$ in Example 1.1, then a sequence $(x_n)$ converges in $(X, d)$ if and only if it is eventually constant. That is, there exists $x \in X$ and $N \in \mathbb{N}$ such that $x_n = x$ for all $n > N$; and, in that case, the sequence converges to $x$.
> recall the discrete metric $$
d(x, y) = \begin{cases} 0 & \text{if } x = y, \\ 1 & \text{if } x \neq y. \end{cases}\tag{discrete metric}
$$

**Example 3.2.** For $\mathbb{R}$ with its standard absolute-value metric, Definition 3.1 is the definition of the convergence of a real sequence.
> i.e. $$
d(x,y) = |x-y|
$$

As for subsets of $\mathbb{R}$, we can give a sequential characterization of closed sets in a metric space.

**Theorem 3.1.** A subset $F \subset X$ of a metric space $X$ is closed if and only if the limit of every convergent sequence in $F$ belongs to $F$.

**Proof.**

- First suppose that $F$ is closed, meaning that $F^c$ is **open**. If $(x_n)$ is a sequence in $F$ and $x \in F^c$, then there is a neighborhood $U \subset F^c$ of $x$ which contains no terms in the sequence, so $(x_n)$ cannot converge to $x$. Thus, the limit of every convergent sequence in $F$ belongs to $F$.

- Conversely, suppose that $F$ is not closed. Then $F^c$ is **not open**, and there exists a point $x \in F^c$ such that every neighborhood of $x$ contains points in $F$. Choose $x_n \in F$ such that $x_n \in B_{1/n}(x)$. Then $(x_n)$ is a sequence in $F$ whose limit $x$ does not belong to $F$, which proves the result.
> the latter part proves the $\leftarrow$ part.

**Recall:** A Cauchy sequence is equivalent to a convergent sequence in $\mathbb{R}$. However, in general, in a metric space, **this is not true**. We define the completeness of metric spaces in terms of Cauchy sequences.

**Definition 3.2.** Let $(X, d)$ be a metric space. A sequence $(x_n)$ in $X$ is a Cauchy sequence if for every $\epsilon > 0$ there exists $N \in \mathbb{N}$ such that:

$$
m, n > N \implies d(x_m, x_n) < \epsilon.
$$

**Remark 3.1.** Every convergent sequence is Cauchy: if $x_n \to x$, then given $\epsilon > 0$ there exists $N$ such that $d(x_n, x) < \epsilon/2$ for all $n > N$, and then for all $m, n > N$ we have:

$$
d(x_m, x_n) \leq d(x_m, x) + d(x_n, x) < \epsilon.
$$

Complete spaces are ones in which the converse is also true.
> Remark 3.1 shows that Convergence $\to$ Cauchy is true for all spaces, but only in **complete** spaces the reverse is also true.

**Definition 3.3.** A metric space is complete if every Cauchy sequence converges to a point in the space.

**Example 3.3.** If $d$ is the discrete metric on a set $X$, then $(X, d)$ is a complete metric space since every Cauchy sequence is eventually constant.

**Example 3.4.** The space $(\mathbb{R}, |\cdot|)$ is complete, but the metric subspace $(\mathbb{Q}, |\cdot|)$ is not complete.

In a complete space, we have the following simple criterion for the **completeness** of a subspace.

**Proposition 3.1.** A subspace $(A, d_A)$ of a complete metric space $(X, d)$ is complete if and only if **$A$ is closed in $X$.**

**Proof.**

- If $A$ is a closed subspace of a complete space $X$ and $(x_n)$ is a Cauchy sequence in $A$, then $(x_n)$ is a Cauchy sequence in $X$, so it converges to $x \in X$. Since $A$ is closed, $x \in A$, which shows that $A$ is complete.
> here we use the theorem 3.1, $(x_{n})$ is a Cauchy sequence in a closed subspace, then it must converge to the point $x \in A$, which proves that the completeness.

- Conversely, if $A$ is not closed, then by Theorem 3.1 there is a convergent sequence in $A$ whose limit does not belong to $A$. Since it converges, the sequence is Cauchy, but it doesn’t have a limit in $A$, so $A$ is not complete.
> We prove it by Cauchy not to convergence in $A$ to show 

Now, the "MONSTER" comes: compactness.

**Definition 3.4.** Let $X$ be a metric space. A set $K \subset X$ is **compact** if every open cover of $K$ has a finite subcover. That is, if $\{ G_i : i \in I \}$ is a collection of open sets such that $K \subset \bigcup_{i \in I} G_i$, then there is a finite subcollection $\{ G_{i_1}, G_{i_2}, \ldots, G_{i_n} \}$ such that:

$$
K \subset \bigcup_{k=1}^n G_{i_k}.
$$

This definition is often called the **finite-covering property**. However, it is very abstract. In a metric space, we prefer to use the following equivalent but more useful definition:
> **定义3.4.** 设 $X$ 是一个度量空间。如果 $K \subset X$ 的每一个开覆盖都有一个有限子覆盖，则称集合 $K$ 是**紧致**的。也就是说，如果 $\{G_i : i \in I\}$ 是一个开集族，使得 $K \subset \bigcup_{i \in I} G_i$，那么存在一个有限子集 $\{G_{i_1}, G_{i_2}, \ldots, G_{i_n}\}$，使得：

$$
K \subset \bigcup_{k=1}^n G_{i_k}.
$$

>这个定义通常被称为**有限覆盖性质**。然而，它非常抽象。在度量空间中，我们更倾向于使用以下等价但更实用的定义：

**Definition 3.5.** A subset $K \subset X$ of a metric space $X$ is sequentially compact if every sequence in $K$ has a convergent subsequence whose limit belongs to $K$.
>**定义3.5.** 度量空间 $X$ 的子集 $K \subset X$ 是**序列紧致**的，如果 $K$ 中的每一个序列都存在一个收敛的子序列，且该子序列的极限属于 $K$。

Compare this definition with the Bolzano-Weierstrass theorem in $\mathbb{R}$. This definition generalizes the Bolzano-Weierstrass theorem.

**Theorem 3.2.** A set in a metric space is compact if and only if it is sequentially compact.

**Exercise 3. (Hard)** In $\mathbb{R}$ with the classical absolute value distance, prove a set is compact if and only if it’s bounded and closed.

**Hint:** Use the Bolzano-Weierstrass theorem and Theorem 3.1 for closed sets.
> **Proof:**
> 
> *⇒* Suppose $K \subset \mathbb{R}$ is compact. We need to show $K$ is closed and bounded.
> 
> 1. **Closed:** By Theorem 3.1, if $K$ is not closed, there exists a convergent sequence $(x_n) \subset K$ with limit $x \notin K$. But since $K$ is compact, every sequence in $K$ has a convergent subsequence with limit in $K$, contradicting $x \notin K$. Hence, $K$ must be closed.
> 
> 2. **Bounded:** Assume $K$ is unbounded. Then for each $n \in \mathbb{N}$, we can choose $x_n \in K$ such that $|x_n| > n$. This sequence $(x_n)$ has no convergent subsequence (as it escapes to infinity), contradicting the compactness of $K$. Thus, $K$ is bounded.
> 
> *⇐* Suppose $K \subset \mathbb{R}$ is closed and bounded. We need to show $K$ is compact, i.e., every sequence in $K$ has a convergent subsequence with limit in $K$.
> 
> 3. **Bolzano-Weierstrass Application:** Since $K$ is bounded, any sequence $(x_n) \subset K$ is bounded. By the Bolzano-Weierstrass theorem, $(x_n)$ has a convergent subsequence $(x_{n_k})$.
> 
> 4. **Limit in $K$:** Let $x = \lim_{k \to \infty} x_{n_k}$. Since $K$ is closed (by Theorem 3.1), $x \in K$. Therefore, every sequence in $K$ has a convergent subsequence with limit in $K$, so $K$ is compact.
> 
> This completes the proof.



The correct generalization to an arbitrary metric space of the characterization of compact sets in $\mathbb{R}$ as closed and bounded replaces "closed" with "complete" and "bounded" with "totally bounded," which is defined as follows.
> 在任意度量空间中，紧致集合的特征化是将 $\mathbb{R}$中的“闭”和“有界”分别替换为“完备”和“完全有界”，其定义如下。

**Definition 3.6.** Let $(X, d)$ be a metric space. A subset $A \subset X$ is **totally bounded** if for every $\epsilon > 0$ there exists a finite set $\{ x_1, x_2, \ldots, x_n \}$ of points in $X$ such that:

$$
A \subset \bigcup_{i=1}^n B_\epsilon(x_i).
$$

> **定义3.6.** 设 $(X,d)$是一个度量空间。如果对于每一个 $\epsilon>0$，都存在 $X$ 中的一个有限点集 $\{ x_{1},x_{2},\dots,x_{n} \}$，使得：
> 
> $$
 A \subset \bigcup_{i=1}^n B_\epsilon(x_i),
 $$
> 
> 则称 $X$ 的子集 $A \subset X$ 是**完全有界**的。


The proof of the following result is then completely analogous to the proof of the Bolzano-Weierstrass theorem for $\mathbb{R}$.

**Theorem 3.3.** A subset $K \subset X$ of a metric space $X$ is sequentially compact if and only if it is **complete** and **totally bounded.**

---

