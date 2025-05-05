## Appetizer: power method
- **Power method**: the simplest iterative method for computing an eigenvector (in particular, the dominant eigenvector)
	- Iterative means that the eigenvector is constructed as a limit of a convergent sequence of vectors
- It can also be viewed as the simplest matrix-free method
    - Recall: matrix-free means that we only rely on matrix-vector multiplication (*do not necessarily need to construct the full matrix $A$*)
    - Recall: sometimes matvecs are cheaper to implement than forming the entire matrix $A$ and doing a full matvec
      * e.g., $A$ is sparse + low-rank
- In practice, one often only wants one or a few (i.e., $O(1)$) key eigenpairs
    - Important examples to follow
    - If matvec costs $O(n)$, then it is possible to achieve this in $O(n)$ time
    - Much better than a full diagonalization, which is always $O(n^3)$
  - Start with any initial vector $x \in \mathbb{R}^n$ (or $\mathbb{C}^n$).
    - Consider the sequence $Ax, A^2x, A^3x...$
    - What does this converge to?
		- Trick question: usually doesn't converge, or converges to zero vector
    - But if we 'suitably normalize' the sequence, what does it converge to? (Assume for simplicity that $A$ is diagonalizable)
        * The dominant eigenvector (if it exists), i.e., *the eigenvector whose eigenvalue has maximal absolute value*
- Indeed, suppose $A$ has a (strictly) dominant eigenpair $(\lambda_1, v_1)$ and $A$ is diagonalizable
    - In particular, $\lambda_1 \neq 0$.
    - Note that if $A$ is real, since all complex eigenvalues come in conjugate pairs, any dominant eigenvalue must also be real.
    - Then write $x = \sum_{i=1}^{n} c_i v_i$, where $v_2, \ldots, v_n$ complete $v_1$ to a basis of eigenvectors.
    - Then $A^k x = \sum_{i=1}^{n} c_i \lambda_i^k v_i$.
    - So $\lambda_1^{-k} A^k x = \sum_{i=1}^{n} c_i \left(\frac{\lambda_i}{\lambda_1}\right)^k v_i$ .
    - But for $i > 1$, $\left|\frac{\lambda_i}{\lambda_1}\right| < 1$, so $\left(\frac{\lambda_i}{\lambda_1}\right)^k \to 0$.
    - Hence $\lambda_1^{-k} A^k x \to c_1 v_1$.
    - Note that we're in trouble if $c_1 = 0$. We'll come back to this later.
-  In practice, we don't know $\lambda_1$, so we can't form the sequence $\{\lambda_1^{-k} A^k x\}_{k=0}^\infty$.
-  It is not important to know $\lambda_1$, we just need to normalize the iterates so that they don't collapse to zero or fly off to infinity.

Define 
$$u^{(k)} := \frac{A^k x}{\|A^k x\|}$$

where we adopt for now the 2-norm as our norm without including in the notation.
> I believe that here we have $x$ is arbitrarily picked, but we must have $c_{1} \neq 0$, otherwise the algorithm can't learn the perfect direction

- Note that as $k → ∞$, as long as $c_1 ≠ 0$, we have

$$u^{(k)} = \underbrace{ \frac{\sum_{i=1}^n c_i \lambda_i^k v_i}{||\sum_{i=1}^n c_i \lambda_i^k v_i||} ≈ \frac{c_1 λ_1^k v_1}{|c_1λ_1^k |\|v_1\|} }_{ \text{since } \lambda_{1} \text{ is the largest} } = \underbrace{ \frac{c_1}{|c_1|}\left(\frac{λ_1}{|λ_1|}\right)^k  }_{ =:z^{(k)} } \frac{v_1}{\lVert v_{1} \rVert } = z^{(k)} u_1$$
where $|z^{(k)}| = 1$. Hence in the real case, $z^{(k)} = ±1$.

- This implies the following.
- **Theorem**: With notation as above there exists a complex unit $z^{(k)}$ (which is ±1 in the real case) such that $\lim_{k→∞} \frac{u^{(k)}}{z^{(k)}} = \frac{v_1}{\|v_1\|}$.
- This suggests an algorithm that converges to $v_1$ (up to scaling), but how to terminate?

	- Given a guess $u^{(k)}$, we want to consider a stopping criterion based on the 'relative residual norm'
$$\frac{\|Au^{(k)} - λ_1 u^{(k)}\|}{λ_1}.$$
	- However, we don’t know $λ_1$, so we need to come up with an iterative guess for it……

- How to estimate eigenvalue given eigenvector guess?
	- Note that if $Au = λu$, then $u · (Au) = λ \|u\|^2$, hence $λ = \frac{u^\dagger Au}{\|u\|^2}$.
	- If $u$ is normalized, then we have $λ = u · (Au) = u^\dagger Au$.
	> this is how you estimate and update the guess of $\lambda$ 
	
	- Therefore guess $λ_1^{(k)} = u^{(k)} · (Au^{(k)})$, and estimate relative residual norm as
$$\frac{\|Au^{(k)} - λ_1^{(k)} u^{(k)}\|}{λ_1^{(k)}}.$$

- This suggests the practical algorithm (**power method**):
	- Given initial guesses $x^{(0)} ∈ ℝ^n$, maximum number of iterations $m$, ability to perform matvecs by A, tolerance $ε$.

	- For $k = 0, …, m$:
		* Set $u^{(k)} = x^{(k)} / \|x^{(k)}\|$.
		* Set $x^{(k+1)} = Au^{(k)}$.
		* Set $λ_1^{(k)} = u^{(k)} · x^{(k+1)}$.
		* If $\|x^{(k+1)} - λ_1^{(k)} u^{(k)}\| / λ_1^{(k)} ≤ ε$:
			- BREAK.
	- Return $(λ_1^{(k)}, u^{(k)})$.

- The power method works even if A is not diagonalizable, as long as there is a strictly dominant eigenvector
	- Proof more subtle, relies on Jordan normal form
-  Can generalize to the problem of finding $k ≥ 1$ most dominant eigenvectors (**subspace iteration**)
## Markov Chain
- Think of a system with $n$ different states, labeled $1,\ldots,n$
	- Interested in random transitions between states at discrete time steps
	- Specifically, suppose that for each state $j$, we are given a column of probabilities $p_j := (p_{1j},\ldots,p_{nj})^\top$
	- Given that we are in state $j$ at time $t$, *$p_{ij}$ represents the probability that we move to state $i$ at time $t+1$*
	- The transition probabilities only depend on the current state (Markov property)
	- To ensure the probabilistic interpretation we must have
		-  $p_{ij} \geq 0$ for all $i,j$
		-  $\sum_{i=1}^{n} p_{ij} = 1$ for all $j$
		- Can also write $\mathbf{1}^\top p_j = 1$ for all $j$, where $\mathbf{1}$ is the vector of all ones
		> the third one is basically the matrix version of the second property
		
	- $P = (p_{ij})$ satisfying these two properties is called **a (column) stochastic matrix**
		-  Can rephrase second property concisely as $P^\top \mathbf{1} = \mathbf{1}$.
		- Can write $P \geq 0$ to indicate entry-wise non-negativity.
	- $P$ is in addition **positive** if $p_{ij} > 0$ for all $i,j$, in which case we may write $P > 0$.
		- We will assume positivity later for simplicity.

- Note that $\pi \in \mathbb{R}^n$ defines a **probability distribution** over $\{1,\ldots,n\}$ if $\pi_i \geq 0$ for all $i$ and $\sum_{i=1}^{n} \pi_i = 1$. (We can write these properties alternatively as $\pi \geq 0$ and $\mathbf{1}^\top \pi = 1.$)

- Let $X_t \in \{1,\ldots,n\}$ be the random variable denoting our state at time $t$
	- **Claim**: If $\pi = (\pi_1,\ldots,\pi_n)^\top$ is the probability distribution for $X_t$ at time $t$, then the probability distribution $\pi'$ at time $t+1$ is $P\pi$
    * Check:
      $$\begin{aligned}
        \pi'_i &= \mathbf{P}(X_{t+1} = i) \\
              &= \sum_{j=1}^{n} \mathbf{P}(X_{t+1} = i \mid X_t = j) \mathbf{P}(X_t = j) \\
              &= \sum_{j=1}^{n} p_{ij} \pi_j \\
              &= [P\pi]_i
      \end{aligned}$$

	  - Therefore the evolution of the probability distribution of our state can be understood purely in terms of repeated application of the stochastic matrix $P$
- Notice that if $\mathbf{1}^\top \pi = 1$, then
  $$\mathbf{1}^\top (P\pi) = (P^\top \mathbf{1})^\top \pi = \mathbf{1}^\top \pi = 1$$

	- Moreover if $\pi \geq 0$ (entry-wise), then $P\pi \geq 0$ as well.
	- This is good because it confirms that $P$ maps probability distributions to probability distributions, as we suspected.

- For arbitrary initial distribution $\pi$, interested in the limit
$$\pi_\infty = \lim_{k \to \infty} P^k \pi$$
	- If it exists, $\pi_\infty$ should then be a probability vector as well.
	- If $\pi_\infty$ exists, then by taking the limit of both sides of $\pi_{k+1} = P(\pi_k)$, we obtain
$$\pi_\infty = P\pi_\infty.$$
- If the limit exists, $\pi_\infty$ is called the **equilibrium / invariant distribution**.
	- Thusly led to ask: are the conditions for the power method satisfied?
	- If so, then $\pi_\infty$ is the (suitably normalized) dominant eigenvector of $P$.

- **Perron-Frobenius Theorem**: Let $P$ be a positive stochastic matrix. Then $P$ admits a dominant eigenvector with eigenvalue 1.
	- More refined versions of the theorem are available with weaker assumptions.

## Sub-application: PageRank
- The Internet....is a directed graph.

	- Again given a collection of states (webpages) indexed 1,...,n.
	- A directed graph is a set E of edges $(i,j)$ (order matters).
    * Indicates a hyperlink from page i to page j.
- A directed graph is equivalently specified as an adjacency matrix A, defined by
$$A_{ij} = 
    \begin{cases}
        1, & (i,j) ∈ E \\
        0, & (i,j) ∉ E
    \end{cases}$$
- Want to rank pages according to some score.
    * Score should measure the 'centrality' of a webpage.
	    * Not really satisfactory just to measure how many pages link to it (why?).
    - PageRank offers such a score, an example of an eigenvector centrality measure.
- We will build a Markov chain (stochastic matrix) out of our adjacency matrix A.

	- In fact, example of a general recipe for producing a stochastic matrix from a nonnegative matrix.
	- Just appropriately normalize each column so that its sum is one.
	    * Assume each column has a nonzero entry, i.e., each page has a link to it.
	    * Otherwise, if there is a page that no one links to, we can throw it out.
	- Formula: define $\tilde{P}$ stochastic via $\tilde{P}^T = \text{diag}(A1)^{-1}A$, or$$\tilde{P}_{ji}=\begin{cases}
        \frac{1}{\deg^{-}(i)}, & (i,j) \in E \\
        0, & (i,j) \notin E,
    \end{cases}$$
	where $deg⁻(i)$ is the 'out degree' of a page.
	- **Probabilistic interpretation**: Markov chain on the webpages, at each time step pick a uniformly random hyperlink from current page and click it.
	- Not quite satisfactory yet...
		- *Power method may be very slow to converge*, as you will explore in the homework. By changing the problem slightly, we can ensure that it always converges rapidly.
- Introduce a damping factor $\tau \in (0,1)$.
    - Instead of clicking a random link, do the following:
        * With probability $\tau$, pick a uniformly random link on current page and click it.
        * With probability $1- \tau$, go to a random webpage picked uniformly from the entire set of webpages.
    - Corresponds to defining a new Markov chain$$P= \tau \tilde{P}+(1- \tau) \frac{1}{n} \mathbf{1} \mathbf{1}^T$$
	(note that $\mathbf{1} \mathbf{1}^T$ is just the matrix of all ones).

	- Note $P$ is stochastic and positive.
	- Hence (by Perron-Frobenius) can let $\pi^{(*)}$ be its dominant eigenvector, scaled so that $\pi^{(*)} \geq 0$ and $\mathbf{1}^{\top}\pi^{(*)} = 1$.
	    * $\pi_i^{(*)}$ is the PageRank score for webpage $i$.
	    * Corresponds to the fraction of time that our Markov chain spends on state $i$ in the long-time limit.
	- Can compute with power method.
- The **PageRank algorithm** is then just the power method applied to this matrix $P$, except even simpler: we don't need to normalize at each iteration (since the dominant eigenvalue is exactly 1).
	- Indeed, if we start with initial guess $\pi^{(0)}$ that is a probability distribution and then define $\pi^{(k+1)} = P\pi^{(k)}$ for all $k = 0, 1, 2, \ldots$, then it is guaranteed that $\pi^{(k)}$ is a probability distribution at every iteration, and $\lim_{k \to \infty} \pi^{(k)} = \pi^{(*)}$.

## Linear Algebra Review
- Review:
	 - eigenvalues
	 - diagonalization
	  - spectral theorem for symmetric matrices	
	  - viewing matrix factorizations as sums of rank-one matrices
	  - orthogonal matrices
	  - orthogonal projectors
	  - SVD (full, thin, compact, truncated)
	  - relation between SVD and spectral theorem
### 🔹 **Eigenvalues and Eigenvectors**

Let $A \in \mathbb{R}^{n \times n}$. A scalar $\lambda \in \mathbb{C}$ is an **eigenvalue** of $A$ if there exists a nonzero vector $v \in \mathbb{C}^n$ such that:
$$Av = \lambda v$$

- $v$ is the corresponding **eigenvector**
- Equivalently: $\det(A - \lambda I) = 0$
### 🔹 **Diagonalization**

A matrix $A \in \mathbb{R}^{n \times n}$ is **diagonalizable** if:
$$A = VDV^{-1}$$

- $D$ is diagonal, containing eigenvalues $\lambda_1, \dots, \lambda_n$
- $V$ has the corresponding eigenvectors as columns
- Diagonalizable $⇔$ A has a basis of eigenvectors $⇔$ geometric mult. = algebraic mult. for all eigenvalues
### 🔹 **Spectral Theorem (Symmetric Matrices)**

Let $A \in \mathbb{R}^{n \times n}$ be **symmetric**: $A = A^\top$

Then:$$A = Q \Lambda Q^\top$$

- $Q$ is orthogonal ($Q^\top Q = I$), columns are orthonormal eigenvectors
- $\Lambda$ is diagonal with real eigenvalues
- This is **orthogonal diagonalization**
### 🔹 **Matrix Factorizations as Sums of Rank-One Matrices**

Any diagonalizable $A \in \mathbb{R}^{n \times n}$ (or symmetric) can be written as:
$$A = \sum_{i=1}^n \lambda_i v_i v_i^\top$$

- $\lambda_i$ are eigenvalues    
- $v_i$ are orthonormal eigenvectors
- Each term $\lambda_i v_i v_i^\top$ is a **rank-one matrix**
### 🔹 **Orthogonal Matrices**

A matrix $Q \in \mathbb{R}^{n \times n}$ is **orthogonal** if:$$Q^\top Q = I \quad \text{or} \quad Q^{-1} = Q^\top$$
- Columns (and rows) of Q form an orthonormal basis
- $\|Qx\| = \|x\|$: orthogonal matrices preserve inner products and norms
### 🔹 **Orthogonal Projectors**

Let $V \in \mathbb{R}^{n \times k}$ have orthonormal columns. Then:
$$P = VV^\top$$

is the **orthogonal projector** onto the column space of $V$:
- $P^2 = P$,$P^\top = P$ (i.e. **idempotent and symmetric**)
- $Pv = v$ for $v \in \text{Col}(V)$
- $P^2 = P \Rightarrow \text{eigenvalues in } \{0, 1\}$
### 🔹 **Singular Value Decomposition (SVD)**

For any $A \in \mathbb{R}^{m \times n}$, there exists a factorization:
$$A = U \Sigma V^\top$$

- $U \in \mathbb{R}^{m \times m}$, $V \in \mathbb{R}^{n \times n}$: orthogonal
- $\Sigma \in \mathbb{R}^{m \times n}$: diagonal with non-negative singular values $\sigma_1 \ge \cdots \ge \sigma_r > 0$
**Variants:**
- **Full SVD**: as above
- **Thin SVD**: $A = U_r \Sigma_r V_r^\top$, where $U_r \in \mathbb{R}^{m \times r}, \Sigma_r \in \mathbb{R}^{r \times r}, V_r \in \mathbb{R}^{n \times r}$
- **Compact SVD**: same as thin, but only stores nonzero $\sigma_i$
- **Truncated SVD**: keep top$- k<rk < r$ terms for low-rank approximation
### 🔹 **Relation Between SVD and Spectral Theorem**

For a **symmetric** matrix $A \in \mathbb{R}^{n \times n}$:
- SVD and eigen-decomposition coincide:
$$A = Q \Lambda Q^\top \quad \text{(Spectral Thm)} \quad = Q |\Lambda| Q^\top \quad \text{(SVD, with } \sigma_i = |\lambda_i| \text{)}$$
For general A, we have:
- $A^\top A = V \Sigma^2 V^\top$  
- $A A^\top = U \Sigma^2 U^\top$

So SVD relates to the **spectral theorem** applied to $A^\top A$ and $AA^\top$, which are both symmetric and positive semidefinite.


## PCA

• Suppose we have a set of ‘data points’ $x_j \in \mathbb{R}^m$, $j = 1, \dots, n$ 
- $m$ is the dimension of the data space, $n$ is the number of data points
• Goal: want to find a **subspace** of dimension $k$ (given) that ‘captures’ the data as well as possible 
- In statistics terms, subspace that ‘**explains as much variance**’ as possible
• Assume that data has zero empirical mean, i.e., $\frac{1}{n} \sum_{i=1}^n x_i = 0$ 
- Always possible by replacing $x_i \leftarrow x_i - \frac{1}{n} \sum_{i=1}^n x_i$. 
- This is called **de-meaning the data.**
• Can form data matrix $X = [x_1, \dots, x_n] \in \mathbb{R}^{m \times n}$ 
- FYI: $\frac{1}{n} XX^T = \frac{1}{n} \sum_i x_i x_i^T$ is called the *empirical covariance* matrix
• Need quantitative formulation as an optimization problem 
- Want to optimize over $q_1, \dots, q_k$ (forming an orthonormal basis for best subspace)
- Let $Q = [q_1, \dots, q_k]$, so alternatively can optimize over $Q \in \mathbb{R}^{m \times k}$ such that $Q^T Q = I_k$ 
- There is not a completely standard name for a matrix satisfying $Q^T Q = I_k$, but we can say that such $Q$ is **partially orthogonal** or simply **has orthonormal columns.** 
-  Note: $P_Q := QQ^T$ is orthogonal projection onto $\text{span}(Q) = \text{col}(Q)$. 
---
好的，我们来证明 $P_Q = QQ^T$ 是到 $Q$ 的列空间 $\text{col}(Q)$ 上的正交投影算子 (Orthogonal Projection Operator)，其中 $Q$ 是一个 $m \times k$ 矩阵，其列向量是标准正交的 (Orthonormal Columns)，即 $Q^T Q = I_k$。

**证明思路:**

一个算子 $P$ 是到子空间 $S$ 的正交投影，需要满足两个核心条件：
1.  对于任意向量 $x$，投影结果 $Px$ 必须在子空间 $S$ 内。
2.  对于任意向量 $x$，残差向量 $(x - Px)$ 必须与子空间 $S$ 正交 (Orthogonal)。

**证明过程:**

设 $Q \in \mathbb{R}^{m \times k}$ 且 $Q^T Q = I_k$。令 $P_Q = QQ^T$。我们要投影到的子空间 (Subspace) 是 $S = \text{col}(Q)$，即 $Q$ 的列向量张成的空间 (span)。

1.  **验证投影结果在子空间内:**
    对于任意向量 $x \in \mathbb{R}^m$，我们计算 $P_Q x = (QQ^T)x = Q(Q^T x)$。
    令 $y = Q^T x$。由于 $Q \in \mathbb{R}^{m \times k}$ 且 $x \in \mathbb{R}^m$，所以 $y \in \mathbb{R}^k$ 是一个 $k$ 维向量。
    那么 $P_Q x = Qy = y_1 q_1 + y_2 q_2 + \dots + y_k q_k$，其中 $q_i$ 是 $Q$ 的第 $i$ 个列向量，$y_i$ 是向量 $y$ 的第 $i$ 个分量。
    根据定义，$Qy$ 是 $Q$ 的列向量的线性组合，因此 $P_Q x$ 必然位于 $Q$ 的列空间 $\text{col}(Q)$ 中。

2.  **验证残差向量与子空间正交:**
    我们需要证明残差向量 $x - P_Q x = x - QQ^T x$ 与子空间 $\text{col}(Q)$ 中的任意向量 $z$ 正交。
    一个向量与子空间 $\text{col}(Q)$ 正交，等价于它与该子空间的一组基 (Basis) 中的所有向量都正交。由于 $Q$ 的列向量是标准正交的，它们构成了 $\text{col}(Q)$ 的一组标准正交基。因此，我们只需要证明 $x - P_Q x$ 与 $Q$ 的所有列向量都正交即可。
    这可以用矩阵形式简洁地表示为： $Q^T (x - P_Q x) = 0$。
    我们来计算：
    $$\begin{align}
Q^T (x - P_Q x)  & = Q^T (x - QQ^T x)  \\
 & =Q'x - \underbrace{ Q'(Q  }_{ \text{by definition } = I_{k}  }Q'x) \\
 & =Q'x - I_{k} Q'x \\
 & = \mathbf{o}
\end{align} $$
由于结果是零向量，这表明残差向量 $x - P_Q x$ 与 $Q$ 的所有列向量都正交，因此它与整个子空间 $\text{col}(Q)$ 正交。

**结论:**
由于 $P_Q x = QQ^T x$ 满足：
a) $P_Q x \in \text{col}(Q)$
b) $(x - P_Q x) \perp \text{col}(Q)$
因此，$P_Q = QQ^T$ 确实是到 $Q$ 的列空间 $\text{col}(Q)$ 上的正交投影矩阵。

**补充性质 (可选):**
正交投影矩阵 $P$ 通常还具有以下性质：
* **幂等性 (Idempotence):** $P^2 = P$。
    $P_Q^2 = (QQ^T)(QQ^T) = Q(Q^T Q)Q^T = Q(I_k)Q^T = QQ^T = P_Q$。
* **对称性 (Symmetry / Self-adjointness):** $P^T = P$。
    $P_Q^T = (QQ^T)^T = (Q^T)^T Q^T = QQ^T = P_Q$。
这些性质也可以用来验证 $QQ^T$ 是一个正交投影矩阵。
---

• Objective function to be **minimized** is $$f(Q) := \sum_{i=1}^n \|x_i - P_Q x_i\|^2$$ 
- Measures the deviation of $x_i$ from its orthogonal projection onto the subspace (i.e., the closest point in the subspace), summed over all the data points $i$ 
- Clearly zero if $x_i \in \text{span}(Q)$ for all $i$, i.e., if all the data lies in the subspace 
- Measures deviation from this ideal scenario
• Notation: the ‘span’ of a matrix indicates the **span of its column**s. It is literally the same as the column space.
• Compute
$$ f(Q) = \sum_{i=1}^n \|x_i - P_Q x_i\|^2 = \sum_{i=1}^n \|(I - QQ^T)x_i\|^2 $$
- Note: $(I - QQ^T)x_i$ is the $i$-th column of $(I - QQ^T)X = X - QQ^T X$, and the squared Frobenius norm is the same as the sum of the squared column norms.
- Hence $f(Q) = \|X - QQ^T X\|_F^2$.
> This is by definition of the Forbenius norm
- Let $X = U \Sigma V^T = \sum_{i=1}^r \sigma_i u_i v_i^T$ be a **compact** SVD for $X$, where $r := \text{rank}(X)$.
	- Here $U = [u_1, \dots, u_r]$ ($m \times r$)and $V = [v_1, \dots, v_r]$. ($n \times r$)
- Let $\tilde{X} = \tilde{U} \tilde{\Sigma} \tilde{V}^T = \sum_{i=1}^k \sigma_i u_i v_i^T$ be a **truncated** SVD (to rank $k$).
	- Here $\tilde{U} = [u_1, \dots, u_k]$ $m \times k$ and $\tilde{V} = [v_1, \dots, v_k]$.($n \times k$)
- Note that $\text{rank}(QQ^T X) \le k$, so we know from the ‘best rank-$k$ approximation’ property of the truncated SVD that if we could choose $Q$ such that $QQ^T X = \tilde{U} \tilde{\Sigma} \tilde{V}^T$, it would be optimal.

根据 **Eckart-Young-Mirsky 定理**，这个 $\tilde{X}$ 是所有秩不超过 $k$ 的矩阵中，与原矩阵 X 在弗罗贝尼乌斯范数意义下**最接近**的矩阵。也就是说，$\lVert X-B \rVert^{2}_{F}$​ 的最小值在 $B = \tilde{X}$时取到，对于所有 $rank(B)≤k$。

- But then just choose $Q = \tilde{U}$, so
$$ QQ^T X = \sum_{i=1}^r \tilde{U} \tilde{U}^T \sigma_i u_i v_i^T = \sum_{i=1}^k \sigma_i u_i v_i^T = \tilde{U} \tilde{\Sigma} \tilde{V}^T $$
- if $1\leq i\leq k$, then $\tilde{U}'u_{i}=e_{i}$, that is the $i$-th standard base vector. So $\tilde{U} \tilde{U}'u_{i}=\tilde{U} e_{i}=u_{i}$
- if $i>k$, then by definition we have $\tilde{U}u_{i}= 0$.


• In summary, the optimal subspace is given by the span of the top $k$ left **singular vectors** of the (**de-meaned**) data matrix $X$.
- Alternatively, it is given by span of the dominant $k$ eigenvectors of the empirical covariance matrix $\frac{1}{n} XX^T$.
• For a data point $x_j$, its component $u_i \cdot x_j$ in the $i$-th singular vector is called the $i$-th **principal component** of the data.
- Thus the $j$-th column of the matrix $Q^T X \in \mathbb{R}^{k \times n}$, which is $(u_1 \cdot x_j, \dots, u_k \cdot x_j)^T \in \mathbb{R}^k$ is the vector consisting of the first $k$ principal components of the $j$-th data point. 

• We can use PCA for dimensionality reduction:
- The columns $y_j$ of $Y := Q^T X$ are the images of the data points $x_j$ under the linear transformation $Q^T$ mapping $\mathbb{R}^m \to \mathbb{R}^k$.
- Thus the map $Q^T$ can be thought of as ‘*compressing*’ our dataset.
- To *recover* the original dataset approximately from the compressed dataset, we can form $\tilde{X} = QY = QQ^T X$.
	- Recall that $Q$ was optimized to minimize the error $\| \tilde{X} - X \|_F$ of our recovery.
	- Thus, although the compression is ‘lossy,’ it is **as faithful as possible** given that we are compressing the data into dimension $k$.
> This $\tilde{X}$ is an orthogonal projection of $X$ on $\text{col}(Q)$


# 39 Subspace iteration

## 39.1 Basic algorithm

* Let $A \in \mathbb{R}^{n \times n}$ be diagonalizable (for simplicity). Let $\lambda_1, \dots, \lambda_n$ denote its eigenvalues (possibly repeated according to multiplicity), ordered such that $$|\lambda_1| \ge \dots \ge \underbrace{ |\lambda_k| > |\lambda_{k+1}|  }_{ \text{spectral gap}>0 }\ge \dots \ge |\lambda_n|$$
* Let $u_1, \dots, u_n$ denote a corresponding basis of eigenvectors, and let $U = [u_1, \dots, u_k] \in \mathbb{R}^{n \times k}$.
    * For now we are not assuming that $A$ is symmetric so these are not necessarily orthonormal!

* We want to find the subspace $\text{span}(U)$, in some sense.
* Let $W = [w_1, \dots, w_k] \in \mathbb{R}^{n \times k}$. (Initial guess.)
* **Theorem:** For ‘*generic*’ initial guess $W \in \mathbb{R}^{n \times k}$, there exists a suitable sequence of invertible matrices $C_l \in \mathbb{R}^{k \times k}$, $l = 0, 1, 2, \dots$, such that $$\lim_{l \to \infty} A^l W C_l = U$$
    * In the proof, we will say what we mean by ‘*generic*’ (generalizing condition for power method), and we will construct the sequence $C_l$.
* **Implication:** As $l \to \infty$, $A^l W = A(A(A(\dots AW) \dots )))$ does not literally ‘converge’ to $U$, but its span ‘converges’ to the $\text{span}(U)$ as a subspace.
    * However, if we literally form $A^l W$ for $l$ large, we will have issues with numerical overflow/underflow.
    * Therefore the actual practical algorithm will include a **generalization of the normalization procedure** used in the power method.

* This suggests the practical algorithm (**subspace iteration**), which we present for now without a stopping criterion:
    * Given generic initial guess $W \in \mathbb{R}^{n \times k}$, maximum number of iterations $m$, ability to perform matrix-vector multiplications by $A$.
    * Let $V$ have orthonormal columns with the same span as the columns of $W$. (This can be achieved by the Gram-Schmidt procedure, or equivalently, a rectangular QR factorization $W = VR$. The Matlab function `orth` can also be used.)
    * For $j = 0, 1, \dots, m$:
        * Set $W \leftarrow AV$. (Note that this entails $k$ matrix-vector multiplications by $A$, one for each column.)
        * Let $V$ have **orthonormal** columns with the same span as the columns of $W$. (*do the QR factorization again*)
    * Return $V$.

* Note that the bulk of the work in each iteration consists of (1) the $k$ matvecs by $A$ and (2) the orthonormalization of the $k$ columns of $W$.
    * The orthonormalization cost is $O(nk^2)$ as can verified by counting operations in Gram-Schmidt.
    * For example, if $A$ is sparse with $O(n)$ nonzero entries, then the cost of the matvecs is $O(nk)$ per iteration. If $A$ is completely dense (worst case), it is still only $O(n^2 k)$ per iteration.
    * Compare to the cost $O(n^3)$ of a complete **diagonalization**!
> The cost of subspace iteration is approximately $m \times O(nk + nk^{2})$ or $m \times O(n^{2} k + nk^{2})$.
* If the number of iterations $m$ is **sufficiently** large, then the final output $V$ will have columns forming an *orthonormal basis* for a subspace very close to $\text{span}(U)$.
* Later we will improve the algorithm to include a criterion for stopping when the algorithm has converged within a specified tolerance. However, this takes some more care than in the case of the power method.
* We will also explain later how to recover actual eigenpairs from the recovered subspace $\text{span}(V)$.

## 39.2 Convergence proof

* **Proof (of theorem):**
    * We will construct $C_l$ below and present the *genericity* condition on $W$ in ***bold italics***.
    * First let $P$ have columns $u_1, \dots, u_n$, so $$P = [U \mid V]$$ where $U=[u_1, \dots, u_k]$ and $V=[u_{k+1}, \dots, u_n]$. 
    > * (Note that the columns $u_i$ are not necessarily orthogonal since $A$ is not assumed symmetric.)
    > * Just let you know, this $P$ comes from $A = P\Lambda P^{-1}$ and we want the information (the first $k$ invariant subspace) of $A$.

    * Then $A = P \Lambda P^{-1}$, with $\Lambda = \text{diag}(\lambda_1, \dots, \lambda_n)$. We partition $\Lambda$ conformally with $P$:
        $$ \Lambda = \begin{pmatrix} \Lambda_1 & 0 \\ 0 & \Lambda_2 \end{pmatrix} $$
        where the top-left block $\Lambda_1 = \text{diag}(\lambda_1, \dots, \lambda_k)$ is $k \times k$, and $\Lambda_2 = \text{diag}(\lambda_{k+1}, \dots, \lambda_n)$ is $(n-k) \times (n-k)$. *Note that the diagonal matrix $\Lambda_1$ is invertible because $|\lambda_1| \ge \dots \ge |\lambda_k| > |\lambda_{k+1}| \ge 0$, implying $\lambda_1, \dots, \lambda_k$ are all non-zero.*
    * Let $Y = P^{-1} W$. We partition $Y$ conformally:
        $$ Y = \begin{pmatrix} Y_1 \\ Y_2 \end{pmatrix} $$
        where the top block $Y_1$ is $k \times k$ and $Y_2$ is $(n-k) \times k$. We assume the *genericity* condition on $W$, which translates to: ***$Y_1$ has full rank, i.e., is invertible***.
    * In this case, let $C_l = Y_1^{-1} \Lambda_1^{-l}$. Since $Y_1$ and $\Lambda_1$ are invertible, $C_l$ is invertible. Now we examine the limit:
        $$ A^l W C_l = (P \Lambda P^{-1})^l W C_l = P \Lambda^l P^{-1} W C_l = P \Lambda^l Y C_l $$
        Substituting the partitioned forms and the definition of $C_l$:
        $$ A^l W C_l = P \begin{pmatrix} \Lambda_1^l & 0 \\ 0 & \Lambda_2^l \end{pmatrix} \begin{pmatrix} Y_1 \\ Y_2 \end{pmatrix} (Y_1^{-1} \Lambda_1^{-l}) = P \begin{pmatrix} \Lambda_1^l Y_1 \\ \Lambda_2^l Y_2 \end{pmatrix} (Y_1^{-1} \Lambda_1^{-l}) $$
        $$ = P \begin{pmatrix} \Lambda_1^l Y_1 Y_1^{-1} \Lambda_1^{-l} \\ \Lambda_2^l Y_2 Y_1^{-1} \Lambda_1^{-l} \end{pmatrix} = P \begin{pmatrix} I_k \\ \Lambda_2^l Y_2 Y_1^{-1} \Lambda_1^{-l} \end{pmatrix} $$
    * We claim that the entire lower block $\Lambda_2^l Y_2 Y_1^{-1} \Lambda_1^{-l}$ in the last expression *converges to the zero* matrix as $l \to \infty$.
        * To see this, let $B := Y_2 Y_1^{-1}$ (a constant $(n-k) \times k$ matrix). We need to show that $M_l := \Lambda_2^l B \Lambda_1^{-l} \to 0$ as $l \to \infty$.
        * The $(i, j)$-th entry of $M_l$ is given by:
            $$ (M_l)_{ij} = (\lambda_{k+i})^l B_{ij} (\lambda_j)^{-l} = \left( \frac{\lambda_{k+i}}{\lambda_j} \right)^l B_{ij} $$
            for $i = 1, \dots, n-k$ and $j = 1, \dots, k$.
        * From the ordering of eigenvalues, we know $|\lambda_{k+i}| < |\lambda_k|$ for $i \ge 1$, and $|\lambda_j| \ge |\lambda_k|$ for $j \le k$. Therefore,
            $$ \left| \frac{\lambda_{k+i}}{\lambda_j} \right| \le \frac{|\lambda_{k+i}|}{|\lambda_k|} < 1 $$
            Since the *base* of the power has magnitude *strictly* less than 1, each entry $(M_l)_{ij} \to 0$ as $l \to \infty$. Thus, the matrix $M_l$ converges to the zero matrix.
    * Therefore, taking the limit as $l \to \infty$:
        $$ \lim_{l \to \infty} A^l W C_l = P \begin{pmatrix} I_k \\ 0 \end{pmatrix} = [U \mid V] \begin{pmatrix} I_k \\ 0 \end{pmatrix} = U I_k + V 0 = U $$
        as was to be shown.

## 39.3 Distance between subspaces

* We need to include a condition that allows us to detect when subspace iteration has converged to within a desired tolerance.
* It is tricky to do this because we want to think of subspace iteration as providing a sequence of subspaces. **How do we measure the distance between two subspaces?**
* One way to measure the distance between two subspaces is to *compute a matrix norm distance between their orthogonal projection matrices.*
* Consider two subspaces $\text{span}(V)$ and $\text{span}(\tilde{V})$, where $V \in \mathbb{R}^{n \times k}$ and $\tilde{V} \in \mathbb{R}^{n \times k}$ have orthonormal columns (i.e., $V^T V = I_k$ and $\tilde{V}^T \tilde{V} = I_k$).
    * Then $P := VV^T$ and $Q := \tilde{V}\tilde{V}^T$ are the corresponding $n \times n$ orthogonal projection matrices onto these subspaces.
    * **We will compute the squared Frobenius norm distance** $\|P - Q\|_F^2$.

* Need two facts involving the matrix **trace** $\text{Tr}[B]$ (also denoted $\text{tr}(B)$ or $\text{trace}(B)$) which is the sum of the diagonal elements of a square matrix $B$.
    * **Fact 1:** For any matrix $A$ (not necessarily square), $$\|A\|_F^2 = \text{Tr}[A^T A] = \text{Tr}[AA^T]$$
    * **Fact 2:** For any matrices $B$ ($m \times n$) and $C$ ($n \times m$), $\text{Tr}[BC] = \text{Tr}[CB]$ (Cyclic property of trace).
    * We verified in class, but it is a good exercise to try yourself!
---

### 推导矩阵迹的性质

**前提定义:**
* 一个 $m \times n$ 矩阵 $A$ 的元素记为 $A_{ij}$ ($i=1,\dots,m; j=1,\dots,n$)。
* 矩阵 $A$ 的转置 $A^T$ 是一个 $n \times m$ 矩阵，其元素为 $(A^T)_{ji} = A_{ij}$。
* 一个方阵 $M$ (设为 $n \times n$) 的迹 $\text{Tr}[M]$ 定义为其对角元素之和：$\text{Tr}[M] = \sum_{i=1}^n M_{ii}$。
* 一个 $m \times n$ 矩阵 $A$ 的弗罗贝尼乌斯范数 (Frobenius norm) 的平方定义为所有元素平方和：$\|A\|_F^2 = \sum_{i=1}^m \sum_{j=1}^n (A_{ij})^2$。
* 矩阵乘法 $(XY)_{ik} = \sum_{j} X_{ij} Y_{jk}$。

---

**性质 1 (Fact 1): $\|A\|_F^2 = \text{Tr}[A^T A] = \text{Tr}[AA^T]$**

我们要证明两个等式：

**(a) 证明 $\|A\|_F^2 = \text{Tr}[A^T A]$**

设 $A$ 是一个 $m \times n$ 的矩阵。那么 $A^T$ 是 $n \times m$ 的矩阵，$C = A^T A$ 是一个 $n \times n$ 的方阵。
我们需要计算 $\text{Tr}[C] = \sum_{j=1}^n C_{jj}$。

根据矩阵乘法定义，$C$ 的对角元素 $C_{jj}$ 为：
$$ C_{jj} = (A^T A)_{jj} = \sum_{i=1}^m (A^T)_{ji} A_{ij} $$
根据转置的定义，$(A^T)_{ji} = A_{ij}$。代入上式：
$$ C_{jj} = \sum_{i=1}^m A_{ij} A_{ij} = \sum_{i=1}^m (A_{ij})^2 $$
这个结果是矩阵 $A$ 第 $j$ 列所有元素的平方和。

现在计算迹 $\text{Tr}[A^T A] = \text{Tr}[C]$：
$$ \text{Tr}[A^T A] = \sum_{j=1}^n C_{jj} = \sum_{j=1}^n \left( \sum_{i=1}^m (A_{ij})^2 \right) $$
交换求和顺序（有限和可以自由交换顺序）：
$$ \text{Tr}[A^T A] = \sum_{i=1}^m \sum_{j=1}^n (A_{ij})^2 $$
根据弗罗贝尼乌斯范数平方的定义，这个结果恰好是 $\|A\|_F^2$。
因此，$\|A\|_F^2 = \text{Tr}[A^T A]$ 得证。

**(b) 证明 $\|A\|_F^2 = \text{Tr}[AA^T]$**

设 $A$ 是一个 $m \times n$ 的矩阵。那么 $A^T$ 是 $n \times m$ 的矩阵，$D = AA^T$ 是一个 $m \times m$ 的方阵。
我们需要计算 $\text{Tr}[D] = \sum_{i=1}^m D_{ii}$。

根据矩阵乘法定义，$D$ 的对角元素 $D_{ii}$ 为：
$$ D_{ii} = (AA^T)_{ii} = \sum_{j=1}^n A_{ij} (A^T)_{ji} $$
根据转置的定义，$(A^T)_{ji} = A_{ij}$。代入上式：
$$ D_{ii} = \sum_{j=1}^n A_{ij} A_{ij} = \sum_{j=1}^n (A_{ij})^2 $$
这个结果是矩阵 $A$ 第 $i$ 行所有元素的平方和。

现在计算迹 $\text{Tr}[AA^T] = \text{Tr}[D]$：
$$ \text{Tr}[AA^T] = \sum_{i=1}^m D_{ii} = \sum_{i=1}^m \left( \sum_{j=1}^n (A_{ij})^2 \right) $$
这个结果同样是 $\|A\|_F^2$。
因此，$\|A\|_F^2 = \text{Tr}[AA^T]$ 得证。

结合 (a) 和 (b)，性质 1 证毕。

---

**性质 2 (Fact 2): $\text{Tr}[BC] = \text{Tr}[CB]$ (迹的循环性质)**

设 $B$ 是一个 $m \times n$ 的矩阵，$C$ 是一个 $n \times m$ 的矩阵。那么 $BC$ 是一个 $m \times m$ 的方阵，$CB$ 是一个 $n \times n$ 的方阵。两者都可以计算迹。

计算 $\text{Tr}[BC]$：
首先计算 $BC$ 的对角元素 $(BC)_{ii}$ ($i=1, \dots, m$)：
$$ (BC)_{ii} = \sum_{j=1}^n B_{ij} C_{ji} $$
然后计算迹：
$$ \text{Tr}[BC] = \sum_{i=1}^m (BC)_{ii} = \sum_{i=1}^m \left( \sum_{j=1}^n B_{ij} C_{ji} \right) $$

计算 $\text{Tr}[CB]$：
首先计算 $CB$ 的对角元素 $(CB)_{jj}$ ($j=1, \dots, n$)：
$$ (CB)_{jj} = \sum_{k=1}^m C_{jk} B_{kj} $$
(为了避免下标混淆，这里用了 $k$ 作为内层求和下标。)
然后计算迹：
$$ \text{Tr}[CB] = \sum_{j=1}^n (CB)_{jj} = \sum_{j=1}^n \left( \sum_{k=1}^m C_{jk} B_{kj} \right) $$

现在比较两个结果：
$$ \text{Tr}[BC] = \sum_{i=1}^m \sum_{j=1}^n B_{ij} C_{ji} $$
$$ \text{Tr}[CB] = \sum_{j=1}^n \sum_{k=1}^m C_{jk} B_{kj} $$
我们可以把第二个式子里的下标 $k$ 换成 $i$（只是个哑变量）：
$$ \text{Tr}[CB] = \sum_{j=1}^n \sum_{i=1}^m C_{ji} B_{ij} $$
由于 $B_{ij}$ 和 $C_{ji}$ 都是标量，它们的乘积顺序可以交换：$C_{ji} B_{ij} = B_{ij} C_{ji}$。
$$ \text{Tr}[CB] = \sum_{j=1}^n \sum_{i=1}^m B_{ij} C_{ji} $$
最后，交换求和顺序（有限和可以自由交换顺序）：
$$ \text{Tr}[CB] = \sum_{i=1}^m \sum_{j=1}^n B_{ij} C_{ji} $$
我们发现这个结果与 $\text{Tr}[BC]$ 的表达式完全相同。

因此，$\text{Tr}[BC] = \text{Tr}[CB]$ 得证。

---

* **Computation:**
    * First, note that $P$ and $Q$ are symmetric ($P^T=P, Q^T=Q$) and idempotent ($P^2=P, Q^2=Q$). Expand using Fact 1:
        $$\begin{align}
\|P - Q\|_F^2  & = \text{Tr}[(P - Q)^T (P - Q)]  \\
 & = \text{Tr}[(P - Q)(P - Q)]  \\
 & = \text{Tr}[P^2 - QP - PQ + Q^2] 
\end{align} $$
    * Using idempotency ($P^2=P, Q^2=Q$) and Fact 2 ($\text{Tr}[QP] = \text{Tr}[PQ]$):
        $$ \|P - Q\|_F^2 = \text{Tr}[P] + \text{Tr}[Q] - 2\text{Tr}[PQ] $$
    * Substitute $P=VV^T$ and $Q=\tilde{V}\tilde{V}^T$:
        $$ \|P - Q\|_F^2 = \text{Tr}[VV^T] + \text{Tr}[\tilde{V}\tilde{V}^T] - 2\text{Tr}[VV^T \tilde{V}\tilde{V}^T] $$
    * Now use Fact 2 (cyclic property) to rearrange the matrices within the traces. Also use $V^T V = I_k$ and $\tilde{V}^T \tilde{V} = I_k$:
    > since we assume $V$ and $\tilde{V}$ to have orthonormal columns
        $$ \text{Tr}[VV^T] = \text{Tr}[V^T V] = \text{Tr}[I_k] = k $$
        $$ \text{Tr}[\tilde{V}\tilde{V}^T] = \text{Tr}[\tilde{V}^T \tilde{V}] = \text{Tr}[I_k] = k $$
        $$ \text{Tr}[VV^T \tilde{V}\tilde{V}^T] = \text{Tr}[\tilde{V}^T (VV^T) \tilde{V}] = \text{Tr}[\underbrace{ (\tilde{V}^T V) }_{ X' } \underbrace{ (V^T \tilde{V}) }_{ X }] $$
    * Let $X = V^T \tilde{V}$ (a $k \times k$ matrix). The last trace term becomes $\text{Tr}[X^T X]$. By Fact 1, $\text{Tr}[X^T X] = \|X\|_F^2 = \|V^T \tilde{V}\|_F^2$.
    * Substituting these back:
        $$ \|P - Q\|_F^2 = k + k - 2\|V^T \tilde{V}\|_F^2 = 2k - 2\|V^T \tilde{V}\|_F^2 $$
    * It is also useful to note that $\|P\|_F^2 = \text{Tr}[P^T P] = \text{Tr}[P^2] = \text{Tr}[P] = k$. So the “relative distance” can be computed as:
        $$ \frac{\|P - Q\|_F}{\|P\|_F} = \frac{\sqrt{2k - 2\|V^T \tilde{V}\|_F^2}}{\sqrt{k}} = \sqrt{\frac{2(k - \|V^T \tilde{V}\|_F^2)}{k}} = \sqrt{2 \left( 1 - \frac{\|V^T \tilde{V}\|_F^2}{k} \right)} $$
* **Theorem:** If $V$ and $\tilde{V}$ are $n \times k$ matrices with orthonormal columns, and $P=VV^T$ and $Q=\tilde{V}\tilde{V}^T$ are the orthogonal projection matrices onto $\text{span}(V)$ and $\text{span}(\tilde{V})$, respectively, then
    $$ \|P - Q\|_F^2 = 2 ( k - \|V^T \tilde{V}\|_F^2 ) $$
    and
    $$ \frac{\|P - Q\|_F}{\|P\|_F} = \sqrt{2 \left( 1 - \frac{1}{k} \|V^T \tilde{V}\|_F^2 \right)} . $$
* The key point is that we can compute the Frobenius norm distance $\|P - Q\|_F$ (or its square) using the formula involving $\|V^T \tilde{V}\|_F^2$ **without ever forming the $n \times n$ projection matrices $P$ and $Q$ explicitly**. Forming $P=VV^T$ or $Q=\tilde{V}\tilde{V}^T$ directly would cost roughly $O(n^2 k)$ operations, which is very expensive for large $n$.
    * Instead, the cost is dominated by forming the $k \times k$ matrix $X = V^T \tilde{V}$.
    * This matrix multiplication takes $O(nk^2)$ floating-point operations.
    * Calculating $\|X\|_F^2$ from $X$ takes only $O(k^2)$ operations. 
    * Thus, the total cost to evaluate the distance using this formula is only $O(nk^2)$, which is much more efficient.
## 39.4 Full pseudocode

* If $V$ is our current guess (orthonormal basis matrix) in subspace iteration and $\tilde{V}$ is the basis matrix from the next iteration, then **we can use the relative Frobenius norm distance** between the orthogonal projection matrices onto their spans,
    $$ \frac{\|VV^T - \tilde{V}\tilde{V}^T\|_F}{\|VV^T\|_F} = \sqrt{2 \left( 1 - \frac{1}{k} \|V^T \tilde{V}\|_F^2 \right)} $$
    as a measure of convergence.

* This suggests the following pseudocode for subspace iteration, now including a stopping criterion:

    * **Inputs:**
        * Generic initial guess matrix $W \in \mathbb{R}^{n \times k}$.
        * Maximum number of iterations $m$.
        * Ability to perform matrix-vector multiplications by $A$.
        * Convergence tolerance $\epsilon > 0$.

    * **Initialization:**
        * Compute $V \in \mathbb{R}^{n \times k}$ such that its columns are orthonormal and $\text{span}(V) = \text{span}(W)$. (e.g., using QR decomposition of $W$, or `orth(W)`).

    * **Iteration Loop:**
        * For $j = 0, 1, \dots, m$:
            * **Power Step:** Compute $W_{next} \leftarrow AV$. (Requires $k$ matrix-vector products).
            * **Orthonormalization:** Compute $\tilde{V} \in \mathbb{R}^{n \times k}$ such that its columns are orthonormal and $\text{span}(\tilde{V}) = \text{span}(W_{next})$. (e.g., using QR decomposition of $W_{next}$, or `orth(W_{next})`).
            * **Convergence Check:** Compute the relative distance measure between the current subspace (span $V$) and the next subspace (span $\tilde{V}$):
                $$ \delta := \sqrt{2 \left( 1 - \frac{1}{k} \|V^T \tilde{V}\|_F^2 \right)} $$
                *(Note: This calculation requires $O(nk^2)$ operations, dominated by forming $V^T \tilde{V}$)*.
            * **Update:** Set $V \leftarrow \tilde{V}$.
            * **Check & Stop:** If $\delta < \epsilon$, then BREAK (exit loop).

    * **Output:** Return the final matrix $V$.

* The output $V$ contains an orthonormal basis such that $\text{span}(V)$ is approximately equal to the target dominant invariant subspace $\text{span}(U)$.

## 39.5 Recovering eigenpairs via Rayleigh-Ritz

* **We will assume in this section that $A$ is symmetric.**
* Subspace iteration (assuming for simplicity that we have fully converged it) furnishes a matrix $V \in \mathbb{R}^{n \times k}$ whose columns form an orthonormal basis for $\text{span}(U)$, the span of the dominant $k$ eigenvectors of $A$. Thus, $$\text{span}(U) = \text{span}(V)$$
    * Since $A$ is symmetric, by the **spectral theorem**, we know that the eigenvectors $u_1, \dots, u_n$ can be chosen to form an orthonormal basis. Therefore, the columns $u_1, \dots, u_k$ of $U$ (the true dominant eigenvectors) can be assumed to be orthonormal, i.e., $U^T U = I_k$.

>[!spectral theorem]
>**谱定理（针对实对称矩阵 $A \in \mathbb{R}^{n \times n}$, $A^T = A$）的主要内容：**
> 1.  **所有特征值都是实数**: 对称矩阵 $A$ 的所有特征值 $\lambda_1, \dots, \lambda_n$ 都是实数。
> 2.  **可对角化**: 对称矩阵 $A$ 总是可以被对角化。
> 3.  **特征向量的正交性**:
>     * 对应于**不同**特征值的特征向量是**相互正交 (orthogonal)** 的。
>     * 更强的是：**存在**一个由 $A$ 的特征向量组成的 $\mathbb{R}^n$ 的**标准正交基 (orthonormal basis)**。这意味着我们可以找到 $n$ 个特征向量 $q_1, \dots, q_n$，它们不仅两两正交 ($q_i^T q_j = 0$ for $i \neq j$)，而且每个向量的长度都为 1 ($q_i^T q_i = 1$)。
> 4.  **正交对角化 (Orthogonal Diagonalization)**: 上述性质保证了对称矩阵 $A$ 可以被**正交对角化**。也就是说，存在一个**正交矩阵 (orthogonal matrix)** $Q$ 和一个**实对角矩阵 (real diagonal matrix)** $\Lambda$，使得：
> 
>     $$ A = Q \Lambda Q^T $$
> 
>     其中：
>     * $Q$ 是一个 $n \times n$ 的正交矩阵 ($Q^T Q = QQ^T = I_n$)。$Q$ 的列向量 $(q_1, \dots, q_n)$ 就是 $A$ 的那组标准正交的特征向量。
>     * $\Lambda$ 是一个 $n \times n$ 的对角矩阵，其对角线上的元素 $(\lambda_1, \dots, \lambda_n)$ 是 $A$ 的对应特征值。
> 

* However, the subspace iteration algorithm itself only returns the basis $V$; we have not actually recovered the **eigenpairs** (eigenvalues $\lambda_j$ and eigenvectors $u_j$).
    * There is some ambiguity in the task of recovering “THE” specific eigenvectors $u_1, \dots, u_k$ that form $U$. 
    * This is due to the arbitrary sign (or complex phase, though real symmetric matrices have real eigenvectors) of eigenvectors and potential non-uniqueness if there are repeated eigenvalues within the dominant group $\lambda_1, \dots, \lambda_k$. 
    * Therefore, we cannot hope to recover the exact matrix $U$ that we might have defined theoretically.
* Instead, our goal is to recover:
    * The dominant eigenvalues $\lambda_1, \dots, \lambda_k$ (perhaps up to permutation if some are equal).
    * A corresponding set of orthonormal eigenvectors $q_1, \dots, q_k$ such that $\text{span}(q_1, \dots, q_k) = \text{span}(U)$ and they satisfy the eigenvector equations $Aq_j = \lambda_j q_j$ for $j = 1, \dots, k$.
* It is useful to notice that the eigenvector equations $Au_j = \lambda_j u_j$ for $j = 1, \dots, k$, can be repackaged in the single matrix equation $AU = U \Lambda_1$, where $\Lambda_1 = \text{diag}(\lambda_1, \dots, \lambda_k)$ is the $k \times k$ diagonal matrix of the dominant eigenvalues (as used in the convergence proof).
* **Therefore, similarly, we seek an $n \times k$ matrix $Q = [q_1, \dots, q_k]$ with orthonormal columns ($Q^T Q = I_k$) such that $AQ = Q\Lambda_1$.**
* The **Rayleigh-Ritz procedure**,(瑞利-里兹) applied using the basis $V$ obtained from subspace iteration, provides a way to achieve this:
    * **Step 1:** Form the $k \times k$ matrix $\tilde{A} = V^T A V$. Since $A$ is symmetric, $\tilde{A}$ is also symmetric. ($\tilde{A}^T = (V^T A V)^T = V^T A^T (V^T)^T = V^T A V = \tilde{A}$).
>[!Note]
>What's this $\tilde{A}$
>1. 让 $V$ 的各个列向量作为$S =\text{span}(V)$ 的一个orthonormal basis
>2. for all $x \in S$, we have $x=Vy,y\in \mathbb{R}^{k}$ 其中 $y=V'x$ 为 $x$ 的坐标 
>3. 当我们让$A$ 作用在$x$上时，则$Ax$ 可能并不在 $S$
>4. 于是我们想到去找$Ax$ 在 $S$ 上的 projection
>5. 此时坐标为 $$y_{proj} = V'(P_{V}Ax) = V'(VV'Ax) = V'Ax$$
>6. 带入 $x= Vy$, 则有 $y_{proj} = V'AVy =\tilde{A}y$
>7. 换句话说，$\tilde{A}$ 就是原映射 $A$ 在$S$ 中的代表

 **Step 2:** Perform a complete eigen-decomposition (diagonalization) of the small $k \times k$ symmetric matrix $\tilde{A}$: 
	    * Find a $k \times k$ orthogonal matrix $\tilde{U}$ ($\tilde{U}^T \tilde{U} = I_k$) and a $k \times k$ diagonal matrix $\tilde{\Lambda}$ such that $\tilde{A} = \tilde{U} \tilde{\Lambda} \tilde{U}^T$. 
	    * The diagonal entries of $\tilde{\Lambda}$ are the eigenvalues of $\tilde{A}$ (called Ritz values), and the columns of $\tilde{U}$ are the corresponding orthonormal eigenvectors.
        * **Such a decomposition exists by the spectral theorem for symmetric matrices.**
	        * Computing it involves solving a standard $k \times k$ eigenvalue problem, which typically costs $O(k^3)$ operations (*independent of the original large dimension $n$*).
- **Step 3:** Construct the approximate eigenvectors of $A$ (called Ritz vectors) as $Q = V \tilde{U}$.
>[!note]
>我们在这里recover $Q = V \tilde{U}$从而达到将$u_{i} \in\mathbb{R}^{k}$ 转换回原始的 $\mathbb{R}^{n}$.
* There are two claims about this procedure:
    * **Claim 1:** The diagonal matrix of eigenvalues $\tilde{\Lambda}$ obtained from $\tilde{A}$ is equal to the diagonal matrix $\Lambda_1$ containing the **true dominant eigenvalues** of $A$. ($\tilde{\Lambda} = \Lambda_1$, perhaps up to permutation if eigenvalues are repeated).
    * **Claim 2:** The matrix $Q = V \tilde{U}$ constructed has orthonormal columns ($Q^T Q = I_k$) 
	    * and satisfies the desired matrix eigenvector equation $AQ = Q\Lambda_1$ (using the true $\Lambda_1$, which by Claim 1 equals $\tilde{\Lambda}$).

* **Proof of Claims:** We begin with a sub-claim relating the computed basis $V$ and the true basis $U$.
    * **Sub-claim:** $V = U O$ for some $k \times k$ orthogonal matrix $O$. Specifically, we can show $O = U^T V$ works.
        * **Proof that $V=U(U^T V)$:** Let $O=U^T V$. We compute $UO = U(U^T V) = (UU^T)V$. Since $A$ is symmetric, $U$ has orthonormal columns ($U^T U = I_k$), so $P_U = UU^T$ is the orthogonal projection matrix onto $\text{span}(U)$. Since subspace iteration converged fully, we have $\text{span}(V) = \text{span}(U)$. Projecting the columns of $V$ (which are already in $\text{span}(U)$) onto $\text{span}(U)$ leaves them unchanged. Therefore, $P_U V = (UU^T)V = V$. Thus, $V = UO$.
        * **Proof that $O=U^T V$ is orthogonal:** We compute $O^T O = (U^T V)^T (U^T V) = (V^T U^{TT}) (U^T V) = V^T U U^T V$. Again, since $UU^T = P_U$ and $P_U V = V$, we have $O^T O = V^T (UU^T V) = V^T (P_U V) = V^T V$. Since the columns of $V$ are orthonormal (output of subspace iteration), $V^T V = I_k$. Thus, $O^T O = I_k$, which means $O$ is an orthogonal matrix.
        * This completes the proof of the sub-claim ($V=UO$ with $O$ orthogonal).
* **Proof of Claim 1 ($\tilde{\Lambda} = \Lambda_1$):**
    * Using the sub-claim $V=UO$, we substitute into the definition of $\tilde{A}$:
        $$ \tilde{A} = V^T A V = (UO)^T A (UO) = O^T U^T A U O $$
    * Now use the matrix eigenvector equation $AU = U\Lambda_1$:
        $$ \tilde{A} = O^T U^T (U \Lambda_1) O = O^T (U^T U) \Lambda_1 O $$
    * Since $U^T U = I_k$:
        $$ \tilde{A} = O^T I_k \Lambda_1 O = O^T \Lambda_1 O $$
    * The equation $\tilde{A} = O^T \Lambda_1 O$ shows that $\tilde{A}$ is related to the diagonal matrix $\Lambda_1$ by an **orthogonal similarity transformation** (since $O$ is orthogonal, $O^T = O^{-1}$). This means that $\tilde{A}$ and $\Lambda_1$ have the same eigenvalues. The eigenvalues of $\Lambda_1$ are $\lambda_1, \dots, \lambda_k$. The eigenvalues of $\tilde{A}$ are the diagonal entries of $\tilde{\Lambda}$ from the eigendecomposition $\tilde{A} = \tilde{U} \tilde{\Lambda} \tilde{U}^T$. Therefore, the diagonal entries of $\tilde{\Lambda}$ must be $\lambda_1, \dots, \lambda_k$, possibly in a different order if some $\lambda_j$'s are equal. Assuming a consistent ordering (e.g., non-increasing), we have $\tilde{\Lambda} = \Lambda_1$. Claim 1 holds.
* **Proof of Claim 2 ($AQ = Q\Lambda_1$ and $Q^T Q = I_k$):**
    * First, check that $Q=V\tilde{U}$ has orthonormal columns:
        $$ Q^T Q = (V\tilde{U})^T (V\tilde{U}) = (\tilde{U}^T V^T) (V \tilde{U}) = \tilde{U}^T (V^T V) \tilde{U} $$
        Since $V^T V = I_k$ and $\tilde{U}$ is orthogonal ($\tilde{U}^T \tilde{U} = I_k$):
        $$ Q^T Q = \tilde{U}^T I_k \tilde{U} = \tilde{U}^T \tilde{U} = I_k $$
        So $Q$ indeed has orthonormal columns.
    * Now, we verify $AQ = Q\Lambda_1$. Start with $AQ$ and substitute $Q = V\tilde{U}$:
        $$ AQ = A(V\tilde{U}) $$
    * Substitute $V=UO$:
        $$ AQ = A(UO\tilde{U}) = (AU)O\tilde{U} $$
    * Use $AU = U\Lambda_1$:
        $$ AQ = (U\Lambda_1)O\tilde{U} = U\Lambda_1 O\tilde{U} $$
    * Insert $I_k = OO^T$ (since $O$ is orthogonal):
        $$ AQ = U (OO^T) \Lambda_1 O \tilde{U} = (UO) (O^T \Lambda_1 O) \tilde{U} $$
    * Use $UO = V$ and the earlier result $O^T \Lambda_1 O = \tilde{A}$:
        $$ AQ = V \tilde{A} \tilde{U} $$
    * Use the eigendecomposition $\tilde{A} = \tilde{U} \tilde{\Lambda} \tilde{U}^T$:
        $$ AQ = V (\tilde{U} \tilde{\Lambda} \tilde{U}^T) \tilde{U} = (V \tilde{U}) \tilde{\Lambda} (\tilde{U}^T \tilde{U}) $$
    * Use $V\tilde{U}=Q$ and $\tilde{U}^T \tilde{U} = I_k$:
        $$ AQ = Q \tilde{\Lambda} I_k = Q \tilde{\Lambda} $$
    * Finally, use Claim 1 ($\tilde{\Lambda} = \Lambda_1$):
        $$ AQ = Q \Lambda_1 $$
    * This establishes Claim 2.


# 40 随机 SVD (Randomized SVD)

* 假设我们有一个矩阵 $A \in \mathbb{R}^{m \times n}$，并且假定 $m \ge n$。
* 矩阵 $A$ 的全部信息包含在其**细奇异值分解 (thin SVD)** 中：$$A = \hat{U} \hat{\Sigma} \hat{V}^T$$，其中 $\hat{U} \in \mathbb{R}^{m \times n}$ 具有标准正交列，$\hat{\Sigma} \in \mathbb{R}^{n \times n}$ 是对角矩阵（包含奇异值 $\sigma_1 \ge \dots \ge \sigma_n \ge 0$），$\hat{V} \in \mathbb{R}^{n \times n}$ 是正交矩阵。
* 假设我们想要计算 $A$ 的**秩 $k$ 截断 SVD (rank-k truncated SVD)** $$A_k := U \Sigma V^T$$，其中 $U = \hat{U}_{:, 1:k} \in \mathbb{R}^{m \times k}$ 由前 $k$ 个左奇异向量组成，$\Sigma = \text{diag}(\sigma_1, \dots, \sigma_k) \in \mathbb{R}^{k \times k}$ 包含前 $k$ 个最大的奇异值，而 $V = \hat{V}_{:, 1:k} \in \mathbb{R}^{n \times k}$ 由前 $k$ 个右奇异向量组成。

* 注意，$A_k$ 可以通过分别应用**子空间迭代 + 瑞利-里兹**过程*两次*来计算：
    * 我们知道 $AA^T = \hat{U} \hat{\Sigma}^2 \hat{U}^T$ 的 $k$ 个主导特征向量构成了前 $k$ 个左奇异向量 $U$。（对应的特征值是前 $k$ 个奇异值的平方 $\sigma_1^2, \dots, \sigma_k^2$）。
    * 同时，$A^T A = \hat{V} \hat{\Sigma}^2 \hat{V}^T$ 的 $k$ 个主导特征向量构成了前 $k$ 个右奇异向量 $V$。（对应的特征值同样是前 $k$ 个奇异值的平方 $\sigma_1^2, \dots, \sigma_k^2$）。
    * 因此，我们可以分别对 $AA^T$ 和 $A^T A$ 应用子空间迭代（寻找 $k$ 个主导特征向量），以推导出前 $k$ 个左奇异向量 $U$ 和右奇异向量 $V$，以及前 $k$ 个奇异值（通过取特征值的平方根得到 $\Sigma$）。
    * **请注意**：这里字母 $V$ 的含义与之前讨论子空间迭代时的 $V$（表示迭代中的基矩阵）**不同**！在此处，$V$ 指的是**右奇异向量**矩阵。很抱歉，我们有时会用完直观易懂的字母！

>[!What do we mean by doing Rayleigh-Ritz?]
>Let's show how to get $U$ and $\Sigma$:
>1. let $B = AA' \in \mathbb{R}^{m\times m}$,  do subspace iteration to $B$, then we can get a orthonormal basis of the span of $k$ dominant eigenvectors. The output is $V_{basisL}$
>2. Apply Rayleigh-Ritz to $V_{basisL}$, we have $\tilde{\Lambda}_{B} \approx \text{diag}(\sigma_{1}^{2},\dots \sigma_{k}^{2}),Q_{L} \approx U$

* **随机 SVD (Randomized SVD)** 提供了一种近似计算截断 SVD $A_k$ 的**替代方法**。
    * 与子空间迭代不同，随机 SVD **不依赖于迭代算法的收敛**（除了最后一步中类似于瑞利-里兹过程需要对一个小矩阵进行完全 SVD，其成本我们通常视为可忽略不计）。
        * 事实上，如果奇异值 $\sigma_k$ 和 $\sigma_{k+1}$ 之间的**间隙 (gap)** ($\sigma_k - \sigma_{k+1}$) 很小，子空间迭代的收敛速度会**很慢**！
    * 另一方面，使用随机 SVD 时，我们可能需要接受一定的近似误差，其误差程度取决于 $A$ 的奇异值**衰减的速度**（我们稍后会看到）。

## 40.1 简化问题：秩为 k 的情况

* 为简单起见，假设 $\text{rank}(A) = k$，意味着 $A$ 的**值域 (range)** 维度为 $k$。
* 令 $Z = [z_1, \dots, z_k] \in \mathbb{R}^{n \times k}$ 的列向量是 $k$ 个“随机”向量（具体细节稍后会更仔细地阐述）。
* 注意 $Az_1, \dots, Az_k \in \text{range}(A)$。如果 $Z$ 是随机选取的，我们期望以 100% 的概率这些向量是**线性无关**的，因此它们能张成**整个子空间** $\text{range}(A)$，即我们期望 $\text{span}(Az_1, \dots, Az_k) = \text{span}(AZ) = \text{range}(A)$。

>[!range]
>The definition of range $A$ is: $$ \text{range}(A) = \left\{ y \in \mathbb{R}^{m}|y = Ax, x \in \mathbb{R}^{n}\right\} $$


* 事实上，在这个简化情况下，$\text{range}(A) = \text{span}(U)$。
    * 原因是，如果 $\text{rank}(A) = k$，那么奇异值 $\sigma_1, \dots, \sigma_k > 0$，但对于所有 $i > k$，$\sigma_i = 0$。
    * 因此，在 SVD 中，$A = \sum_{i=1}^k \sigma_i u_i v_i^T$，这个和在第 $k$ 项就终止了。
    * 由此得出 $\text{range}(A) = \text{span}(u_1, \dots, u_k) = \text{span}(U)$。 (这个结论我们在课堂上验证过，也是一个很好的练习！)

>[!Verification]
>The goal is to prove $\text{range}(A) = \text{span}(U),$ that is, 
>$$
\begin{align}
\text{range} (A) \subset \text{span}(U) \\
\text{span}(U) \subset \text{range}(A)
\end{align}
>$$
> then we prove them one by one:
> 1. for arbitrary $y \in \text{range}(A)$, then by definition, there exists an $x \in \mathbb{R}^{m}$ such that $y = Ax$
> 2. then we have 
>  $$
y = \sum_{i=1}^{k} \sigma_{i} u_{i}v'_{i}x$$
> then we let $c_{i} = \sigma_{i} v'_{i}x$ be a scalar, then we know $y = \sum_{i=1}^{k}c_{i}u_{i} \in \text{span}(U)$
> 3. we then prove the other side, let $z \in \text{span}(U)$ be arbitrary, then by definition, we know 
> $$
z = \sum_{i=1}^{k} d_{i}u_{i}
>$$
>since $Ax = \sum_{i=1}^{k}\sigma_{i}u_{i}v'_{i}x$, we just want find such $x \in \mathbb{R}^{n}$ such that:$$
\sum_{i=1}^{k} d_{i}u_{i} = \sum_{i=1}^{k}\sigma_{i}u_{i}v'_{i}x
>$$
>4. given $u_{1}\dots u_{k}$ are orthonormal, we have they're linear independent, so we just need 
> $$
\sigma_{i} v'_{i} x = d_{i}
>$$
>since $\sigma_{i}>0$, we know $v'_{i} x = \frac{d_{i}}{\sigma_{i}}$. Since $v_{i}$ are orthonormal, we can let $x = \sum_{i=1}^{k}\frac{d_{i}}{\sigma_{i}}v_{i}$, then it's easy to see that this $x$ satisfies our goal
>5. therefore, $\text{span}(U) \subset \text{range}(A)$

* 所以，在这个简化情况下，我们有 $\text{span}(AZ) = \text{span}(U)$。
* 因此，令 $X$ 是一个矩阵，其列向量是标准正交的，并且张成 $\text{span}(AZ)$（也就是张成 $\text{span}(U)$）。

* 那么，使用子空间 $\text{span}(X)$ 对矩阵 $AA^T$ 应用**瑞利-里兹过程 (Rayleigh-Ritz procedure)**，将能得到前 $k$ 个左奇异向量（以及前 $k$ 个奇异值的平方）。
    * **符号提醒**：这里的 $X$ 扮演了我们之前讨论子空间迭代时 $V$ (迭代基矩阵) 的角色！（现在符号 $V$ 保留给右奇异向量使用。）
    * 具体来说，这里我们必须构造 $k \times k$ 矩阵 $B := X^T AA^T X = (X^T A)(X^T A)^T$。我们通过谱定理将其对角化为 $B = \tilde{U} \tilde{\Lambda} \tilde{U}^T$ （其中 $\tilde{\Lambda}$ 包含 $B$ 的特征值 $\approx \sigma_i^2$，按非增顺序排列）。
    * 然后恢复 $U = X \tilde{U}$，并且可以通过 $\Sigma = \sqrt{\tilde{\Lambda}}$ （取对角元素的正平方根）恢复奇异值。

>[!note]
>Note on $B$: 这里的 $B$ is similar to the $\tilde{A}$ we talked about before, just the projection of the map $AA'$ in subspace $\text{span}(X)$

* 类似的过程可以应用于 $A^T$ 来推导出 $V$，因为 $\text{rank}(A^T) = \text{rank}(A) = k$：
    * 令 $W = [w_1, \dots, w_k] \in \mathbb{R}^{m \times k}$ 的列向量是随机的。
    * 计算 $A^T W$ 并将其列向量标准正交化得到 $Y$。（因此 $\text{span}(Y) = \text{range}(A^T) = \text{span}(V)$）。
    * 构造 $C := Y^T A^T A Y = (AY)^T (AY)$。（这是将 $A^T A$ 投影到 $\text{span}(Y)$ 上的 $k \times k$ 矩阵）。
    * 通过谱定理将其对角化为 $C = \tilde{V} \tilde{\Lambda} \tilde{V}^T$ （按非增顺序排列，这里的 $\tilde{\Lambda}$ 理论上应与上面 $B$ 分解得到的相同）。
    * 恢复 $V = Y \tilde{V}$。

* 但是，有一种方法可以**同时完成**左右两边的步骤！
    * 观察到 $XX^T A = A$。
        * 原因是 $P_X := XX^T$ 是到 $\text{span}(X)$ 的正交投影矩阵，而 $\text{span}(X) = \text{range}(A)$。因此，对于 $A$ 的任何列 $a_i$（都在 $\text{range}(A)$ 中），$P_X a_i = a_i$。所以 $P_X A = A$。
    * 类似地，$YY^T A^T = A^T$（因为 $YY^T$ 是到 $\text{range}(A^T)$ 的投影），两边取转置得到 $AYY^T = A$。
    * 因此，$A = XX^T A = XX^T (AYY^T) = X(X^T A Y)Y^T$。

* **更简洁/紧凑的表述（合并方法）：**
    * 令 $Z = [z_1, \dots, z_k] \in \mathbb{R}^{n \times k}$ 和 $W = [w_1, \dots, w_k] \in \mathbb{R}^{m \times k}$ 的列向量是随机的。
    * 计算 $AZ$ 和 $A^T W$，并将它们的列向量分别标准正交化得到 $X$ 和 $Y$。 ($\text{span}(X) = \text{range}(A) = \text{span}(U)$, $\text{span}(Y) = \text{range}(A^T) = \text{span}(V)$).
    * 构造 $\tilde{A} := X^T A Y$ （注意：这通常**不是对称**矩阵！），并对其进行**完全 SVD** 分解得到 $\tilde{A} = \tilde{U} \tilde{\Sigma} \tilde{V}^T$，其中所有因子 $\tilde{U}, \tilde{\Sigma}, \tilde{V}$ 都是 $k \times k$ 的。
    * 然后恢复 $U = X \tilde{U}$，$V = Y \tilde{V}$，以及 $\Sigma = \tilde{\Sigma}$。


* **为什么这个合并方法能得到相同的结果？**
    * 注意 $$\tilde{A} \tilde{A}^T = (X^T A Y)(Y^T A^T X) = X^T A (YY^T) A^T X$$。因为 $AYY^T = A$，所以 $$\tilde{A} \tilde{A}^T = X^T A A^T X = B$$。根据 SVD 的性质，$\tilde{A}$ 的左奇异向量（即 $\tilde{U}$ 的列）就是 $\tilde{A}\tilde{A}^T$ 的特征向量，也就是 $B$ 的特征向量。
        * 所以我们两种方法（单独 R-R 和合并 SVD）得到的 $\tilde{U}$ 是一致的，因此 $U = X\tilde{U}$ 的计算结果一致。
    * 同时，$\tilde{A}^T \tilde{A} = (Y^T A^T X)(X^T A Y) = Y^T A^T (XX^T) A Y$。因为 $XX^T A = A$，所以 $\tilde{A}^T \tilde{A} = Y^T A^T A Y = C$。$\tilde{A}$ 的右奇异向量（即 $\tilde{V}$ 的列）就是 $\tilde{A}^T\tilde{A}$ 的特征向量，也就是 $C$ 的特征向量。
        * 所以我们两种方法得到的 $\tilde{V}$ 是一致的，因此 $V = Y\tilde{V}$ 的计算结果一致。
    * 并且，$\tilde{A}$ 的奇异值 $\tilde{\Sigma}$ 是 $\tilde{A}\tilde{A}^T = B$ 或 $\tilde{A}^T\tilde{A} = C$ 的特征值的平方根，这也与单独方法一致。


## 40.2 超出秩 k 的情况

* 更一般的算法是类似的，除了我们允许使用 $\tilde{k} \ge k$ 个随机向量进行乘法，其中 $\tilde{k}$ 是一个需要设置的参数（称为**过采样参数**, oversampling parameter）。
    * 通过选取 $Z \in \mathbb{R}^{n \times \tilde{k}}$ 和 $W \in \mathbb{R}^{m \times \tilde{k}}$，并且取足够大的 $\tilde{k}$，我们仍可以期望 $\text{span}(AZ)$ 和 $\text{span}(A^T W)$ 分别**近似地包含** $A$ 的值域 $\text{range}(A)$ 和 $A^T$ 的值域 $\text{range}(A^T)$（也就是 $\text{span}(U)$ 和 $\text{span}(V)$）。
    * 因此，通过如上定义 $X = \text{orth}(AZ) \in \mathbb{R}^{m \times \tilde{k}}$ 和 $Y = \text{orth}(A^T W) \in \mathbb{R}^{n \times \tilde{k}}$，我们仍然可以期望近似 $A \approx XX^T A \approx XX^T A YY^T = X(X^T A Y)Y^T = X \tilde{A} Y^T$ 成立，其中 $\tilde{A} = X^T A Y \in \mathbb{R}^{\tilde{k} \times \tilde{k}}$ 现在是 $\tilde{k} \times \tilde{k}$ 维的（可能比 $k \times k$ 更大）。
* 这个直觉得到了以下技术性定理的支撑（该定理超出了本课程范围）。特别地，我们现在假设 $Z$（和 $W$）的元素是**独立同分布 (i.i.d.) 的标准正态分布**（高斯分布）随机变量。（在 Matlab 中可以用 `randn` 函数生成。）

    **定理 1**: 设 $\delta > 0$ 为失败概率。设 $A \in \mathbb{R}^{m \times n}$，并令 $X = \text{orth}(AZ)$，其中 $Z \in \mathbb{R}^{n \times \tilde{k}}$ 具有独立同分布的标准正态项。存在一个通用常数 $C$ 使得如果 $\tilde{k} \ge C (k + \log(1/\delta))$，那么以至少 $1 - \delta$ 的概率，有
     $$||XX^T A||_F \le 2 \sum_{i>k} \sigma_i^2$$，其中 $\sigma_i$ 表示 $A$ 的奇异值。

* 因此，如果 $A$ 具有 $k$ 阶的“**数值秩 (numerical rank)**”，即 $\sum_{i>k} \sigma_i^2$（尾部奇异值平方和）小到可以忽略不计，那么通过取 $\tilde{k}$ 为比 $k$ 稍大一些（例如 $\tilde{k} = k + p$，其中 $p$ 是小的过采样数，如 $p=5$ 或 $p=10$），随机 SVD 将能以很高的概率保证准确工作。

## 40.3 实际算法

* **给定**:
    * 能执行 $A$ 和 $A^T$ 的矩阵向量乘积的能力。
    * 目标秩 $k$。
    * 随机向量的数量 $\tilde{k} \ge k$（过采样后的维度）。
* **算法步骤**:
    1. 令 $Z \in \mathbb{R}^{n \times \tilde{k}}$ 和 $W \in \mathbb{R}^{m \times \tilde{k}}$ 的元素为独立同分布的标准正态（高斯）随机变量。
    2. 计算 $AZ$ 和 $A^T W$，并将它们的列向量分别**标准正交化 (orthonormalize)** 得到 $X \in \mathbb{R}^{m \times \tilde{k}}$ 和 $Y \in \mathbb{R}^{n \times \tilde{k}}$。
    3. 构造 $\tilde{A} := X^T A Y \in \mathbb{R}^{\tilde{k} \times \tilde{k}}$ （注意：通常不对称！），并对其进行**完全 SVD** 分解得到 $\tilde{A} = \tilde{U} \tilde{\Sigma} \tilde{V}^T$，其中所有因子 $\tilde{U}, \tilde{\Sigma}, \tilde{V}$ 都是 $\tilde{k} \times \tilde{k}$ 的。
    4. 然后恢复并**截断 (truncate)** 至秩 $k$：
        * $\check{U} = [X \tilde{U}]_{:, 1:k} \in \mathbb{R}^{m \times k}$ （取 $X\tilde{U}$ 的前 $k$ 列）
        * $\check{V} = [Y \tilde{V}]_{:, 1:k} \in \mathbb{R}^{n \times k}$ （取 $Y\tilde{V}$ 的前 $k$ 列）
        * $\check{\Sigma} = [\tilde{\Sigma}]_{1:k, 1:k} \in \mathbb{R}^{k \times k}$ （取 $\tilde{\Sigma}$ 左上角的 $k \times k$ 子矩阵）
* **输出**:
    * 那么，$A \approx \check{U} \check{\Sigma} \check{V}^T$ 就构成了 $A$ 的一个近似秩 $k$ 截断 SVD。


# 41 谱聚类 (Spectral Clustering)

## 41.1 从数据构造加权图

* 假设我们给定一组数据点 $x_1, \dots, x_n \in \mathbb{R}^m$。我们将利用这些数据点来创建一个**加权图 (weighted graph)**。
* 同时给定一个**相似性核函数 (similarity kernel)** $K(x, y) \ge 0$，它定义了任意两个数据点 $x, y \in \mathbb{R}^m$ 之间的相似度。该核函数满足对称性：对于所有的 $x, y$，都有 $K(x, y) = K(y, x)$。
    * 一个常用的选择是**高斯相似性核函数 (Gaussian similarity kernel)**（也称为径向基函数核，RBF kernel），它有一个宽度参数 $\sigma > 0$：
        $$ K(x, y) = \exp\left(-\frac{\|x-y\|_2^2}{2\sigma^2}\right) $$
* 利用该核函数可以构建图的**加权邻接矩阵 (weighted adjacency matrix)** $A \in \mathbb{R}^{n \times n}$。矩阵中的元素 $A_{ij}$ 表示第 $i$ 个数据点（对应 $x_i$）和第 $j$ 个数据点（对应 $x_j$）之间的边的权重（即它们的相似度）：
    $$ A_{ij} = K(x_i, x_j) $$
    由于核函数是对称的 ($K(x, y) = K(y, x)$)，因此邻接矩阵 $A$ 也是对称的，即 $A^T = A$。（注意：对于高斯核，通常 $A_{ii} = K(x_i, x_i) = 1$，但有时也会将对角线元素设为 0）。

## 41.2 图拉普拉斯算子 (Graph Laplacians)

* 然后，可以使用加权邻接矩阵 $A$ 来构造相应的**图拉普拉斯矩阵 (Graph Laplacian)** $L \in \mathbb{R}^{n \times n}$。它也是一个对称矩阵，定义为 $L = D - A$，其中 $D$ 是**度矩阵 (degree matrix)**，一个对角矩阵，其对角元素 $D_{ii} = \sum_{j=1}^n A_{ij}$（节点 $i$ 的度，即与节点 $i$ 相连的所有边的权重之和）。简写为 $D = \text{diag}(A\mathbf{1}_n)$（其中 $\mathbf{1}_n$ 是全 1 向量）。
    * 注意，从元素上看，$L_{ij} = \delta_{ij} D_{ii} - A_{ij}$（其中 $\delta_{ij}$ 是克罗内克 δ）。即对角元素 $L_{ii} = D_{ii} - A_{ii}$，非对角元素 $L_{ij} = -A_{ij}$ ($i \neq j$)。

* **补充说明**：图拉普拉斯算子的一种直观理解来自于考虑**左归一化图拉普拉斯算子 (left normalized graph Laplacian)** $\tilde{L} = D^{-1} L = I - D^{-1} A$，注意它通常是**不对称的**！
    * 从元素上看，$\tilde{L}_{ij} = \delta_{ij} - A_{ij} / D_{ii}$。
    * 那么对于任意向量 $v \in \mathbb{R}^n$，乘积向量 $[\tilde{L}v]$ 的第 $i$ 个元素是：
        $$ [\tilde{L}v]_i = v_i - \frac{\sum_{j=1}^n A_{ij} v_j}{\sum_{j=1}^n A_{ij}} $$
        (这里假设 $D_{ii} = \sum_j A_{ij} \neq 0$)
    * 因此，如果我们将向量 $v$ 看作图上的一个“函数”（将节点 $i$ 映射到值 $v_i$），那么 $\tilde{L}v$ 就对应这样一个函数：它测量了节点 $i$ 上的函数值 $v_i$ 与其**邻居节点值的加权平均值**之间的**差值**。

* 关于 $L$ 的两个性质（课堂上的证明在此略去，作为练习）：
    * **性质 1**: $L\mathbf{1}_n = 0$。这意味着 0 是 $L$ 的一个特征值，全 1 向量 $\mathbf{1}_n$ 是对应的特征向量。
    * **性质 2**: $L$ 是（弱）**对角占优 (diagonally dominant)** 的，即对于所有 $i=1, \dots, n$，有 $|L_{ii}| \ge \sum_{j \neq i} |L_{ij}|$。（如果 $A_{ij} \ge 0$ 且 $A_{ii}=0$, 则 $L_{ii} = \sum_{j \neq i} A_{ij} = \sum_{j \neq i} |L_{ij}|$，即行和为零）。

>[!proof]
>Let's now prove the propertis: By definition, we have 
> $$
(L1_{n})_{i} = \sum_{j=1}^{n} L_{ij}(1_{n})_{j} = \sum_{j=1}^{n} L_{ij}= L_{ii} + \sum_{j\neq i} L_{ij}
>$$
>By definition, we have $L_{ii} = D_{ii} -A_{ii}$ and $L_{ij} = -A_{ij}$, so $(L1_{n})_{i}=D_{ii} - \sum_{j=1}^{n}A_{ij}=D_{ii} -D_{ii} =0$
>Then let's prove $L$ is weakly diagonally dominant: still by definition, we have $\sum_{j\neq i}\lvert L_{ij} \rvert=\sum_{j\neq i}\lvert -A_{ij} \rvert=\sum_{j\neq i}\lvert A_{ij} \rvert$
>For the LHS, we know $\lvert L_{ii} \rvert= \lvert D_{ii} - A_{ii} \rvert=\left\lvert  \sum A_{ij} - A_{ii}  \right\rvert=\underbrace{ \left\lvert  \sum_{j\neq i}A_{ij}  \right\rvert=\sum_{j\neq i}\lvert A_{ij} \rvert }_{ \text{given }A_{ij}\geq 0 }$

* 由于 $L$ 是对角占优且对角元素非负（因为 $D_{ii} = \sum_j A_{ij} \ge A_{ii}$ 如果 $A_{ij} \ge 0$），可以推导出第三个性质（证明略去）——
    * **性质 3**: $L$ 是**半正定 (positive semidefinite)** 的（即 $L$ 的所有特征值都 $\ge 0$）。
* 实际上，谱嵌入/聚类通常使用**对称归一化图拉普拉斯算子 (symmetric normalized graph Laplacian)** $$\hat{L} := D^{-1/2} L D^{-1/2} = I - D^{-1/2} A D^{-1/2}$$。其元素为 $$\hat{L}_{ij} = \delta_{ij} - \frac{A_{ij}}{\sqrt{D_{ii} D_{jj}}}$$。

>[!Degree Matrix]
>The matrix $D$ here is called the degree matrix, where $D=\text{diag}(\left\{ D_{ii} \right\}_{i=1}^{n})$ such that $D_{ii}=\sum_{j=1}^{n}A_{ij}$. We call $D_{ii}$ to be the degree of each node $i$

* 我们以最后一条性质结束讨论：
* **性质 4**: $\hat{L}$ (*和* $\tilde{L}$)的所有特征值都位于区间 $[0, 2]$ 内。
    * **证明概要** [课堂讲授中略过]：
        * 首先，$\hat{L}$ 是半正定的。这是因为它可以通过 $\hat{L} = (D^{-1/2}) L (D^{-1/2})^T$ 构建（因为 $D^{-1/2}$ 对称），并且 $L$ 是半正定的（性质 3）。因此 $\hat{L}$ 的特征值都 $\ge 0$。
        > by simply verify $y'\hat{L}y\geq 0$ for arbitrary $y \in \mathbb{R}^{n}$
        * 注意到 $\hat{L}$ 和 $\tilde{L}$ 是**相似 (similar)** 的，它们之间通过 $\tilde{L} = D^{1/2} \hat{L} D^{-1/2}$ 相关联（或者 $\hat{L} = D^{-1/2} \tilde{L} D^{1/2}$）。相似矩阵拥有相同的特征值。
        * 所以，只需要证明 $\tilde{L}$ 的谱半径 $\rho(\tilde{L}) \le 2$ 即可。
        * 根据 Gerschgorin 圆盘定理或范数理论，证明 $\|\tilde{L}\|_\infty \le 2$ （最大行绝对值和范数）就足够了。
        >for any induced matrix norm, we have $\rho(M)\leq \lVert M \rVert$
        * 我们可以界定 $\tilde{L}$ 的任意一行的绝对值之和（假设 $A_{ij} \ge 0$，这是相似性核函数的通常情况）：
            $$ \sum_{j=1}^n |\tilde{L}_{ij}| = \sum_{j=1}^n |\delta_{ij} - \frac{A_{ij}}{D_{ii}}| \le \sum_{j=1}^n |\delta_{ij}| + \sum_{j=1}^n |\frac{-A_{ij}}{D_{ii}}| = 1 + \frac{1}{D_{ii}} \sum_{j=1}^n A_{ij} = 1 + \frac{D_{ii}}{D_{ii}} = 2 $$
            *(这个界限使用了三角不等式和 $A_{ij} \ge 0$)*。
        * 因此，$\tilde{L}$ 的所有行的绝对值和都以 2 为界，这意味着 $\|\tilde{L}\|_\infty \le 2$，从而 $\rho(\tilde{L}) \le 2$。
        * 结合特征值非负，可知 $\hat{L}$ (和 $\tilde{L}$) 的特征值都在 $[0, 2]$ 区间内。证毕。
