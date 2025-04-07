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
