## 开胃小菜：幂法
- **幂法 (Power method)**：计算特征向量（特别是主特征向量）的最简单迭代方法。
    - 迭代意味着特征向量是作为一个收敛向量序列的极限来构造的。
- 它也可以被看作是最简单的免矩阵 (matrix-free) 方法。
    - 回顾：免矩阵意味着我们只依赖于矩阵向量乘法（*不一定需要构造完整的矩阵 $A$*）。
    - 回顾：有时，实现矩阵向量乘法比构建整个矩阵 $A$ 并进行完整的矩阵向量乘法更经济。
        * 例如，$A$ 是稀疏矩阵 + 低秩矩阵。
- 在实践中，人们通常只需要一个或几个（即 $O(1)$）关键的特征对。
    - 重要的例子将在后面介绍。
    - 如果矩阵向量乘法的成本是 $O(n)$，那么就有可能在 $O(n)$ 时间内实现这一目标。
    - 这远比完全对角化要好，后者总是 $O(n^3)$。
- 从任意初始向量 $x \in \mathbb{R}^n$ (或 $\mathbb{C}^n$) 开始。
    - 考虑序列 $Ax, A^2x, A^3x, \ldots$
    - 这个序列会收敛到什么？
        - 这是一个陷阱问题：通常不收敛，或者收敛到零向量。
    - 但是如果我们“适当地规范化”这个序列，它会收敛到什么？（为简单起见，假设 $A$ 是可对角化的）
        * 主特征向量（如果存在），即*其特征值的绝对值最大的特征向量*。

### 可对角化的等价条件（Equivalent Conditions for Diagonalizability）

设 $A \in \mathbb{R}^{n \times n}$ 或 $A \in \mathbb{C}^{n \times n}$，下列条件等价：

1. $A$ 有 $n$ 个线性无关的特征向量。  
   $A$ has $n$ linearly independent eigenvectors.

2. 所有特征空间维数之和为 $n$：
   $$
   \sum_{\lambda \in \text{spec}(A)} \dim \ker(A - \lambda I) = n
   $$
   The sum of dimensions of all eigenspaces equals $n$.

3. 对每个特征值 $\lambda$，几何重数等于代数重数：
   $$
   \dim \ker(A - \lambda I) = \text{algebraic multiplicity of } \lambda
   $$

4. 存在可逆矩阵 $P$，使得 $P^{-1} A P$ 是对角矩阵。  
   There exists an invertible matrix $P$ such that $P^{-1} A P$ is diagonal.

---

### 简单的充分条件（Sufficient Conditions）

- 若 $A$ 有 $n$ 个**互不相同**的特征值，则 $A$ 一定可对角化。  
  If $A$ has $n$ distinct eigenvalues, then $A$ is diagonalizable.

- 若所有特征值的几何重数等于其代数重数，则 $A$ 可对角化。  
  *If all eigenvalues have equal geometric and algebraic multiplicity, then $A$ is diagonalizable.*

---

### 不可对角化的典型情形（Non-diagonalizable Cases）

- 存在特征值 $\lambda$ 满足：
  $$
  \dim \ker(A - \lambda I) < \text{algebraic multiplicity of } \lambda
  $$
  即几何重数小于代数重数时，$A$ 不可对角化。

- 例如：
  $$
  A = \begin{pmatrix}
  2 & 1 \\
  0 & 2
  \end{pmatrix}, \quad \text{只有一个特征向量，不可对角化}
  $$

---

### 实用判断步骤（Practical Steps）

1. 求特征多项式 $\det(A - \lambda I) = 0$，解出所有特征值，记下其代数重数；
2. 对每个特征值 $\lambda$，求解 $\ker(A - \lambda I)$ 的维数（几何重数）；
3. 若所有特征值都满足 $\text{几何重数} = \text{代数重数}$，则 $A$ 可对角化。
---
- 事实上，假设 $A$ 有一个（严格的）主特征对 $(\lambda_1, v_1)$ 并且 $A$ 是可对角化的。
    - 特别地，$\lambda_1 \neq 0$。
    - 注意，如果 $A$ 是实矩阵，由于所有复特征值都以共轭对的形式出现，任何主特征值也必须是实数。
    - 那么将 $x$ 写成 $x = \sum_{i=1}^{n} c_i v_i$，其中 $v_2, \ldots, v_n$ 与 $v_1$ 一起构成一个特征向量基。
    - 那么 $A^k x = \sum_{i=1}^{n} c_i \lambda_i^k v_i$。
    - 所以 $\lambda_1^{-k} A^k x = \sum_{i=1}^{n} c_i \left(\frac{\lambda_i}{\lambda_1}\right)^k v_i$。
    - 但是对于 $i > 1$，有 $\left|\frac{\lambda_i}{\lambda_1}\right| < 1$，所以 $\left(\frac{\lambda_i}{\lambda_1}\right)^k \to 0$。
    - 因此 $\lambda_1^{-k} A^k x \to c_1 v_1$。
    - 注意，如果 $c_1 = 0$，我们就会遇到麻烦。我们稍后会回到这个问题。
- 在实践中，我们不知道 $\lambda_1$，所以我们无法构造序列 $\{\lambda_1^{-k} A^k x\}_{k=0}^\infty$。
- 知道 $\lambda_1$ 并不重要，我们只需要规范化迭代向量，以防止它们坍缩到零或发散到无穷大。

定义
$$u^{(k)} := \frac{A^k x}{\|A^k x\|}$$

这里我们暂时采用2-范数作为我们的范数，并未在符号中特别注明。
> 我认为这里 $x$ 是任意选取的，但我们必须有 $c_1 \neq 0$，否则算法无法学习到正确的方向。

- 注意，当 $k \to \infty$ 时，只要 $c_1 \neq 0$，我们有

$$u^{(k)} = \underbrace{ \frac{\sum_{i=1}^n c_i \lambda_i^k v_i}{\|\sum_{i=1}^n c_i \lambda_i^k v_i\|} \approx \frac{c_1 \lambda_1^k v_1}{|c_1\lambda_1^k |\|v_1\|} }_{\text{因为 } \lambda_1 \text{ 是最大的}} = \underbrace{ \frac{c_1}{|c_1|}\left(\frac{\lambda_1}{|\lambda_1|}\right)^k }_{=:z^{(k)}} \frac{v_1}{\|v_1\|} = z^{(k)} u_1$$
其中 $|z^{(k)}| = 1$。因此，在实数情况下，$z^{(k)} = \pm 1$。

- 这意味着以下结论。
- **定理**：在上述符号下，存在一个复单位 $z^{(k)}$（在实数情况下为 $\pm 1$）使得 $$\lim_{k \to \infty} \frac{u^{(k)}}{z^{(k)}} = \frac{v_1}{\|v_1\|}$$
- 这提出了一个收敛到 $v_1$（在缩放意义下）的算法，但是如何终止呢？

    - 给定一个猜测值 $u^{(k)}$，我们希望考虑一个基于“相对残差范数”的停止准则：
$$\frac{\|Au^{(k)} - \lambda_1 u^{(k)}\|}{\lambda_1}.$$
    - 然而，我们不知道 $\lambda_1$，所以我们需要为它想出一个迭代的猜测值……

- 如何根据特征向量的猜测值来估计特征值？
    - 注意，如果 $Au = \lambda u$，那么 $u \cdot (Au) = \lambda \|u\|^2$，因此 $\lambda = \frac{u^\dagger Au}{\|u\|^2}$。
    - 如果 $u$ 是规范化的，那么我们有 $\lambda = u \cdot (Au) = u^\dagger Au$。
    > 这就是你估计和更新 $\lambda$ 猜测值的方法。
    - 因此，猜测 $\lambda_1^{(k)} = u^{(k)} \cdot (Au^{(k)})$，并将相对残差范数估计为：
$$\frac{\|Au^{(k)} - \lambda_1^{(k)} u^{(k)}\|}{\lambda_1^{(k)}}.$$

- 这提出了实用的算法（**幂法**）：
    - 给定初始猜测向量 $x^{(0)} \in \mathbb{R}^n$，最大迭代次数 $m$，执行矩阵 $A$ 的矩阵向量乘法的能力，以及容差 $\epsilon$。

    - 对于 $k = 0, \ldots, m$:
        * 令 $u^{(k)} = x^{(k)} / \|x^{(k)}\|$。
        * 令 $x^{(k+1)} = Au^{(k)}$。
        * 令 $\lambda_1^{(k)} = u^{(k)} \cdot x^{(k+1)}$。
        * 如果 $\|x^{(k+1)} - \lambda_1^{(k)} u^{(k)}\| / \lambda_1^{(k)} \le \epsilon$:
            - 终止循环 (BREAK)。
    - 返回 $(\lambda_1^{(k)}, u^{(k)})$。

- 即使 $A$ 不可对角化，只要存在一个严格的主特征向量，幂法仍然有效。
    - 证明更为微妙，依赖于若尔当标准型。
- 可以推广到寻找 $k \ge 1$ 个最主要特征向量的问题（**子空间迭代 (subspace iteration)**）。

## 马尔可夫链 (Markov Chain)
- 设想一个有 $n$ 个不同状态的系统，标记为 $1, \ldots, n$。
    - 我们对在离散时间步长下状态之间的随机转换感兴趣。
    - 具体来说，假设对于每个状态 $j$，我们给定一个概率列向量 $p_j := (p_{1j}, \ldots, p_{nj})^\top$。
    - 给定在时间 $t$ 我们处于状态 $j$，则 *$p_{ij}$ 表示在时间 $t+1$ 我们转移到状态 $i$ 的概率*。
    - 转移概率仅取决于当前状态（马尔可夫性质）。
    - 为了确保概率解释，我们必须有：
        - 对于所有的 $i,j$，有 $p_{ij} \geq 0$。
        - 对于所有的 $j$，有 $\sum_{i=1}^{n} p_{ij} = 1$。
        - 也可以写成对于所有的 $j$，有 $\mathbf{1}^\top p_j = 1$，其中 $\mathbf{1}$ 是全为1的向量。
        > 第三个基本上是第二个性质的矩阵形式。

    - 满足这两个性质的矩阵 $P = (p_{ij})$ 被称为**（列）随机矩阵 (column stochastic matrix)**。
        - 第二个性质可以简明地改写为 $P^\top \mathbf{1} = \mathbf{1}$。
        - 可以用 $P \geq 0$ 来表示逐项非负。
    - 如果对于所有的 $i,j$ 都有 $p_{ij} > 0$，则 $P$ 另外是**正的 (positive)**，在这种情况下我们可以写成 $P > 0$。
        - 为简单起见，我们稍后将假设其为正。

- 注意，如果对于所有的 $i$ 都有 $\pi_i \geq 0$ 并且 $\sum_{i=1}^{n} \pi_i = 1$，则 $\pi \in \mathbb{R}^n$ 定义了在 $\{1, \ldots, n\}$ 上的一个**概率分布 (probability distribution)**。（我们可以将这些性质另外写为 $\pi \geq 0$ 和 $\mathbf{1}^\top \pi = 1$。）

- 令 $X_t \in \{1, \ldots, n\}$ 为表示我们在时间 $t$ 所处状态的随机变量。
    - **断言**：如果 $\pi = (\pi_1, \ldots, \pi_n)^\top$ 是在时间 $t$ 时 $X_t$ 的概率分布，那么在时间 $t+1$ 时的概率分布 $\pi'$ 是 $P\pi$。
        * 检验：
        $$
        \begin{aligned}
        \pi'_i &= \mathbf{P}(X_{t+1} = i) \\
                &= \sum_{j=1}^{n} \mathbf{P}(X_{t+1} = i \mid X_t = j) \mathbf{P}(X_t = j) \\
                &= \sum_{j=1}^{n} p_{ij} \pi_j \\
                &= [P\pi]_i
        \end{aligned}
        $$

    - 因此，我们状态的概率分布的演化可以纯粹通过随机矩阵 $P$ 的重复应用来理解。
- 注意，如果 $\mathbf{1}^\top \pi = 1$，那么
    $$\mathbf{1}^\top (P\pi) = (P^\top \mathbf{1})^\top \pi = \mathbf{1}^\top \pi = 1$$

    - 此外，如果 $\pi \geq 0$（逐项），那么 $P\pi \geq 0$ 也成立。
    - 这很好，因为它证实了 $P$ 将概率分布映射到概率分布，正如我们所怀疑的那样。

- 对于任意初始分布 $\pi$，我们对极限感兴趣：
$$\pi_\infty = \lim_{k \to \infty} P^k \pi$$
    - 如果它存在，$\pi_\infty$ 也应该是一个概率向量。
    - 如果 $\pi_\infty$ 存在，那么通过对 $\pi_{k+1} = P(\pi_k)$ 的两边取极限，我们得到：
$$\pi_\infty = P\pi_\infty.$$
- 如果极限存在，$\pi_\infty$ 被称为**平衡分布 / 不变分布 (equilibrium / invariant distribution)**。
    - 因此引出问题：幂法的条件是否满足？
    - 如果是这样，那么 $\pi_\infty$ 就是 $P$ 的（适当规范化的）主特征向量。

- **佩龙-弗罗贝尼乌斯定理 (Perron-Frobenius Theorem)**：令 $P$ 为一个正随机矩阵。那么 $P$ 拥有一个特征值为 1 的主特征向量。
    - 该定理的更精细版本在较弱的假设下也可用。

## 子应用：PageRank
- 互联网……是一个有向图。

    - 再次给定一个状态（网页）的集合，索引为 $1, \ldots, n$。
    - 有向图是边 $(i,j)$（顺序很重要）的集合 $E$。
        * 表示从页面 $i$ 到页面 $j$ 的一个超链接。
- 有向图等价地由邻接矩阵 $A$ 指定，定义为：
$$A_{ij} =
    \begin{cases}
        1, & (i,j) \in E \\
        0, & (i,j) \notin E
    \end{cases}$$
- 希望根据某种分数对页面进行排序。
    * 分数应该衡量网页的“中心性”。
        * 仅仅衡量有多少页面链接到它并不能真正令人满意（为什么？）。
    - PageRank 提供了这样一种分数，是特征向量中心性度量的一个例子。
- 我们将从邻接矩阵 $A$ 构建一个马尔可夫链（随机矩阵）。

    - 事实上，这是从非负矩阵生成随机矩阵的一般方法的例子。
    - 只需适当地规范化每一列，使其总和为1。
        * 假设每一列都有一个非零项，即每个页面都有指向它的链接。
        * 否则，如果存在一个没有页面链接到的页面，我们可以将其丢弃。
    - 公式：通过 $\tilde{P}^T = \text{diag}(A\mathbf{1})^{-1}A$ 定义随机矩阵 $\tilde{P}$，或者
$$\tilde{P}_{ji}=\begin{cases}
        \frac{1}{\text{deg}^{+}(i)}, & (i,j) \in E \\
        0, & (i,j) \notin E,
    \end{cases}$$
    其中 $\text{deg}^{+}(i)$ 是页面 $i$ 的“出度”
    - **概率解释**：网页上的马尔可夫链，在每个时间步从当前页面中均匀随机选择一个超链接并点击它。
    - 目前还不完全令人满意……
        - *幂法收敛可能非常缓慢*，正如你将在作业中探索的那样。通过稍微改变问题，我们可以确保它总是快速收敛。
- 引入阻尼因子 $\tau \in (0,1)$。
    - 不再是点击一个随机链接，而是执行以下操作：
        * 以概率 $\tau$，从当前页面中均匀随机选择一个链接并点击它。
        * 以概率 $1-\tau$，跳转到从整个网页集合中均匀随机选择的一个网页。
    - 这对应于定义一个新的马尔可夫链：
$$P = \tau \tilde{P} + (1-\tau) \frac{1}{n} \mathbf{1}\mathbf{1}^T$$
    （注意 $\mathbf{1}\mathbf{1}^T$ 就是全1矩阵）。

    - 注意 $P$ 是随机的且是正的。
    - 因此（根据佩龙-弗罗贝尼乌斯定理）可以令 $\pi^{(*)}$ 为其主特征向量，并进行缩放使得 $\pi^{(*)} \geq 0$ 且 $\mathbf{1}^{\top}\pi^{(*)} = 1$。
        * $\pi_i^{(*)}$ 是网页 $i$ 的 PageRank 分数。
        * 对应于我们的马尔可夫链在长时间极限下停留在状态 $i$ 的时间比例。
    - 可以用幂法计算。
- **PageRank 算法**随后就只是将幂法应用于这个矩阵 $P$，甚至更简单：我们不需要在每次迭代中进行规范化（因为主特征值恰好是1）。
    - 确实，如果我们从一个作为概率分布的初始猜测 $\pi^{(0)}$ 开始，然后对所有 $k = 0, 1, 2, \ldots$ 定义 $\pi^{(k+1)} = P\pi^{(k)}$，那么可以保证在每次迭代中 $\pi^{(k)}$ 都是一个概率分布，并且 $\lim_{k \to \infty} \pi^{(k)} = \pi^{(*)}$。

## 线性代数回顾
- 回顾内容：
    - 特征值 (eigenvalues)
    - 对角化 (diagonalization)
    - 对称矩阵的谱定理 (spectral theorem for symmetric matrices)
    - 将矩阵分解视为秩一矩阵之和 (viewing matrix factorizations as sums of rank-one matrices)
    - 正交矩阵 (orthogonal matrices)
    - 正交投影算子 (orthogonal projectors)
    - 奇异值分解 (SVD) (完全、瘦、紧凑、截断)
    - SVD 与谱定理之间的关系

### 特征值和特征向量 (Eigenvalues and Eigenvectors)

令 $A \in \mathbb{R}^{n \times n}$。一个标量 $\lambda \in \mathbb{C}$ 是 $A$ 的一个**特征值**，如果存在一个非零向量 $v \in \mathbb{C}^n$ 使得：
$$Av = \lambda v$$

- $v$ 是对应的**特征向量**。
- **具体做法/等价条件**：
    - 上述定义是判断 $\lambda$ 和 $v$ 是否为特征值和特征向量的基本方法。
    - 等价地，$\lambda$ 是特征值当且仅当 $(A - \lambda I)v = 0$ 有非零解 $v$，这意味着矩阵 $A - \lambda I$ 是奇异的。
    - 因此，可以通过求解特征方程 $\det(A - \lambda I) = 0$ 来找到所有的特征值 $\lambda$。这是一个关于 $\lambda$ 的 n 次多项式方程。
    - 一旦找到特征值 $\lambda$，就可以通过求解线性方程组 $(A - \lambda I)v = 0$ 来找到对应的特征向量 $v$（即找到 $A - \lambda I$ 的零空间中的非零向量）。

### 对角化 (Diagonalization)

一个矩阵 $A \in \mathbb{R}^{n \times n}$ 是**可对角化的 (diagonalizable)**，如果它可以被分解为：
$$A = VDV^{-1}$$

- $D$ 是一个对角矩阵，其对角线上的元素是 $A$ 的特征值 $\lambda_1, \dots, \lambda_n$。
- $V$ 的列是与 $D$ 中特征值顺序对应的特征向量。
- **具体做法/条件**：
    - 一个 $n \times n$ 矩阵 $A$ 可对角化，当且仅当 $A$ 有 $n$ 个线性无关的特征向量。这些特征向量可以构成 $\mathbb{R}^n$ (或 $\mathbb{C}^n$) 的一个基。
    - 这也等价于对于 $A$ 的每一个特征值，其几何重数（对应特征空间的维数）等于其代数重数（作为特征多项式根的重数）。
    - **步骤**：
        1. 求解特征方程 $\det(A - \lambda I) = 0$ 找到所有特征值 $\lambda_i$。
        2. 对于每个特征值 $\lambda_i$，求解 $(A - \lambda_i I)v_i = 0$ 找到对应的特征向量 $v_i$（或特征子空间的一个基）。
        3. 如果找到了 $n$ 个线性无关的特征向量 $v_1, \ldots, v_n$，则 $A$ 可对角化。
        4. 构造矩阵 $V = [v_1 | v_2 | \ldots | v_n]$。
        5. 构造对角矩阵 $D = \text{diag}(\lambda_1, \lambda_2, \ldots, \lambda_n)$，其中 $\lambda_i$ 的顺序与 $V$ 中 $v_i$ 的顺序对应。
        6. 那么 $A = VDV^{-1}$。

### 谱定理 (对称矩阵) (Spectral Theorem (Symmetric Matrices))

令 $A \in \mathbb{R}^{n \times n}$ 是**对称的 (symmetric)**：$A = A^\top$。

那么：
$$A = Q \Lambda Q^\top$$

- $Q$ 是**正交矩阵** ($Q^\top Q = I$，因此 $Q^{-1} = Q^\top$)，其列是 $A$ 的标准正交特征向量。
- $\Lambda$ (通常也用 $D$ 表示) 是一个对角矩阵，其对角线上的元素是 $A$ 的实数特征值。
- 这被称为**正交对角化 (orthogonal diagonalization)**。
- **具体做法/性质**：
    1. **实数特征值**：对称矩阵的所有特征值都是实数。
    2. **特征向量正交性**：对应于不同特征值的特征向量是正交的。
    3. **总能正交对角化**：任何实对称矩阵总是可以被正交对角化的。这意味着总能找到一组 $n$ 个标准正交的特征向量。
    - **步骤**：
        1. 求解 $\det(A - \lambda I) = 0$ 找到所有实数特征值 $\lambda_i$。
        2. 对于每个特征值 $\lambda_i$，求解 $(A - \lambda_i I)v = 0$ 找到对应的特征向量（或特征子空间的一个基）。
        3. 如果一个特征值有重根（代数重数大于1），其对应的特征子空间维数（几何重数）等于代数重数。在该特征子空间内，可以使用格拉姆-施密特正交化过程来获得一组标准正交的特征向量。
        4. 对于不同特征值对应的特征向量，它们已经是正交的。将所有找到的特征向量进行归一化，得到一组 $n$ 个标准正交的特征向量 $q_1, \ldots, q_n$。
        5. 构造正交矩阵 $Q = [q_1 | q_2 | \ldots | q_n]$。
        6. 构造对角矩阵 $\Lambda = \text{diag}(\lambda_1, \lambda_2, \ldots, \lambda_n)$，其中 $\lambda_i$ 是与 $q_i$ 对应的特征值。
        7. 那么 $A = Q \Lambda Q^\top$。

### 矩阵分解作为秩一矩阵之和 (Matrix Factorizations as Sums of Rank-One Matrices)

任何可对角化的 $A \in \mathbb{R}^{n \times n}$（特别是对称矩阵，因为它们总是可正交对角化的）可以写成：
$$A = \sum_{i=1}^n \lambda_i v_i v_i^\top$$

- $\lambda_i$ 是特征值。
- $v_i$ 是**标准正交**的特征向量（这主要适用于对称矩阵的情况，其中特征向量可以被选择为标准正交的。对于一般的可对角化矩阵，如果特征向量 $v_i$ 不构成标准正交基，而是构成 $V$ 的列，其逆矩阵的行向量为 $w_i^\top$ (即 $V^{-1}$ 的行)，则分解形式为 $A = \sum_{i=1}^n \lambda_i v_i w_i^\top$。原文这里可能特指了对称矩阵的情况，因为提到了 $v_i$ 是标准正交的）。
- 每一项 $\lambda_i v_i v_i^\top$ 是一个**秩一矩阵 (rank-one matrix)**。
- **具体做法/解释**：
    - 对于对称矩阵 $A = Q \Lambda Q^\top$，其中 $Q = [q_1 | \ldots | q_n]$ 且 $\Lambda = \text{diag}(\lambda_1, \ldots, \lambda_n)$：
    $$A = Q \Lambda Q^\top = [q_1 | \ldots | q_n] \begin{pmatrix} \lambda_1 & & \\ & \ddots & \\ & & \lambda_n \end{pmatrix} \begin{pmatrix} q_1^\top \\ \vdots \\ q_n^\top \end{pmatrix}$$
    $$= [ \lambda_1 q_1 | \ldots | \lambda_n q_n ] \begin{pmatrix} q_1^\top \\ \vdots \\ q_n^\top \end{pmatrix} = \lambda_1 q_1 q_1^\top + \lambda_2 q_2 q_2^\top + \ldots + \lambda_n q_n q_n^\top$$
    - 其中 $q_i$ 是列向量，$q_i^\top$ 是行向量，所以 $q_i q_i^\top$ 是一个 $n \times n$ 的外积矩阵，其秩为1（假设 $q_i \neq 0$）。

### 正交矩阵 (Orthogonal Matrices)

一个矩阵 $Q \in \mathbb{R}^{n \times n}$ 是**正交的 (orthogonal)**，如果：
$$Q^\top Q = I \quad \text{或者} \quad Q^{-1} = Q^\top$$
- $Q$ 的列（和行）构成一个标准正交基 (orthonormal basis)。
- $\|Qx\| = \|x\|$：正交矩阵保持向量的内积和范数（长度和角度不变）。
- **具体做法/性质**：
    - 要检验一个矩阵是否是正交的，可以计算 $Q^\top Q$。如果结果是单位矩阵 $I$，则 $Q$ 是正交的。
    - 正交矩阵的行列式值为 $+1$ 或 $-1$。
    - 正交矩阵的例子包括旋转矩阵和反射矩阵。

### 正交投影算子 (Orthogonal Projectors)

令 $V \in \mathbb{R}^{n \times k}$ 的列是标准正交的。那么：
$$P = VV^\top$$
是到 $V$ 的列空间 (column space of $V$, $\text{Col}(V)$) 上的**正交投影算子 (orthogonal projector)**。
- **性质**：
    - $P^2 = P$ (**幂等性, idempotent**)
    - $P^\top = P$ (**对称性, symmetric**)
    - 对于任何 $v \in \text{Col}(V)$，有 $Pv = v$ (子空间内的向量投影后不变)。
    - 对于任何垂直于 $\text{Col}(V)$ 的向量 $w$ (即 $w \in (\text{Col}(V))^\perp$)，有 $Pw = 0$。
    - $P^2 = P \implies$ 投影算子的特征值只能是 $0$ 或 $1$。
- **具体做法**：
    1. 给定一个子空间 $W \subseteq \mathbb{R}^n$。
    2. 找到 $W$ 的一组标准正交基 $\{v_1, \ldots, v_k\}$。
    3. 构造矩阵 $V = [v_1 | \ldots | v_k]$。
    4. 正交投影到 $W$ 上的投影矩阵是 $P = VV^\top$。
    - 对于任意向量 $x \in \mathbb{R}^n$，$Px = VV^\top x$ 是 $x$ 在子空间 $W$ 上的正交投影。
    - 如果 $V$ 的列是线性无关但不一定是标准正交的，则投影矩阵是 $P = V(V^\top V)^{-1}V^\top$。

### 奇异值分解 (Singular Value Decomposition, SVD)

对于任意 $A \in \mathbb{R}^{m \times n}$，存在一个分解：
$$A = U \Sigma V^\top$$

- $U \in \mathbb{R}^{m \times m}$，是正交矩阵，其列称为**左奇异向量 (left singular vectors)**。
- $V \in \mathbb{R}^{n \times n}$，是正交矩阵，其列称为**右奇异向量 (right singular vectors)**。
- $\Sigma \in \mathbb{R}^{m \times n}$，是一个“对角”矩阵（只有主对角线上的元素可能非零），其对角线上的元素 $\sigma_1 \ge \sigma_2 \ge \cdots \ge \sigma_r > 0$ 是**奇异值 (singular values)**，$r = \text{rank}(A)$。其余奇异值为0。$\Sigma$ 的形式取决于 $m$ 和 $n$ 的关系：
    - 如果 $m=n$, $\Sigma = \text{diag}(\sigma_1, \ldots, \sigma_n)$。
    - 如果 $m>n$, $\Sigma = \begin{pmatrix} \text{diag}(\sigma_1, \ldots, \sigma_n) \\ 0 \end{pmatrix}$。
    - 如果 $m<n$, $\Sigma = \begin{pmatrix} \text{diag}(\sigma_1, \ldots, \sigma_m) & 0 \end{pmatrix}$。
    (更准确地说，$\Sigma_{ii} = \sigma_i$ for $i=1,\dots,r$, and all other entries are zero)

**变体 (Variants)：**
- **完全 SVD (Full SVD)**：如上所述，$U$ 是 $m \times m$，$V$ 是 $n \times n$。
    - **具体做法**：$U$ 的列是 $AA^\top$ 的标准正交特征向量。$V$ 的列是 $A^\top A$ 的标准正交特征向量。$\Sigma$ 的对角元素是 $A^\top A$ (或 $AA^\top$) 的非零特征值的平方根。
- **瘦 SVD (Thin SVD)**：$A = U_r \Sigma_r V_r^\top$，其中
    - $U_r \in \mathbb{R}^{m \times r}$ (包含与 $r$ 个非零奇异值对应的 $U$ 的前 $r$ 列)。
    - $\Sigma_r \in \mathbb{R}^{r \times r}$ (是一个包含 $r$ 个非零奇异值的对角矩阵 $\text{diag}(\sigma_1, \ldots, \sigma_r)$)。
    - $V_r \in \mathbb{R}^{n \times r}$ (包含与 $r$ 个非零奇异值对应的 $V$ 的前 $r$ 列)。
    - **具体做法**：计算出完全 SVD 后，取其对应非零奇异值的部分。当 $m > n$ 时，这通常更有用，此时 $U_r$ 是 $m \times n$，$\Sigma_r$ 是 $n \times n$，$V_r$ (即 $V$) 是 $n \times n$ (假设 $r=n$)。更一般的瘦 SVD 是指 $U$ 矩阵的列数等于 $\Sigma$ 矩阵的行数，V 矩阵的列数等于 $\Sigma$ 矩阵的列数，而 $\Sigma$ 矩阵的大小为 $\min(m,n) \times \min(m,n)$。
- **紧凑 SVD (Compact SVD)**：与瘦 SVD 基本相同，但明确指出只存储非零的奇异值 $\sigma_i$ 及其对应的左右奇异向量。因此 $U_r$ 是 $m \times r$, $\Sigma_r$ 是 $r \times r$, $V_r$ 是 $n \times r$。
    - $A = \sum_{i=1}^r \sigma_i u_i v_i^\top$ (秩一矩阵之和的形式)。
- **截断 SVD (Truncated SVD)**：保留前 $k < r$ 个最大的奇异值及其对应的奇异向量，用于低秩逼近：
    $$A_k = U_k \Sigma_k V_k^\top = \sum_{i=1}^k \sigma_i u_i v_i^\top$$
    其中 $U_k$ 是 $U$ 的前 $k$ 列，$\Sigma_k$ 是 $\Sigma$ 的左上角 $k \times k$ 对角块，$V_k$ 是 $V$ 的前 $k$ 列。$A_k$ 是在弗罗贝尼乌斯范数和谱范数意义下，秩为 $k$ 的矩阵中对 $A$ 的最佳逼近 (Eckart-Young-Mirsky 定理)。

### SVD 与谱定理之间的关系 (Relation Between SVD and Spectral Theorem)

对于一个**对称**矩阵 $A \in \mathbb{R}^{n \times n}$：
- SVD 和特征值分解（谱分解）是一致的（或者说非常相似）：
    $$A = Q \Lambda Q^\top \quad \text{(谱定理)}$$
    如果我们将 SVD 写为 $A = U \Sigma V^\top$，那么对于对称矩阵：
    - $U$ 和 $V$ 可以选择为相同的正交矩阵 $Q$（或者 $U = Q \cdot \text{Sign}(\Lambda)$ 且 $V=Q$）。
    - 奇异值 $\sigma_i$ 是特征值 $\lambda_i$ 的绝对值，即 $\sigma_i = |\lambda_i|$。
    - 所以 $\Sigma = |\Lambda|$（对角元素取绝对值）。
    - 如果所有特征值非负 ($A$ 是对称半正定)，则 $U=V=Q$ 且 $\Sigma = \Lambda$，SVD 和谱分解完全相同。
    - 如果有负特征值，例如 $A = Q \text{diag}(\lambda_1, \ldots, \lambda_n) Q^\top$。其 SVD 可以是 $A = U \text{diag}(|\lambda_1|, \ldots, |\lambda_n|) Q^\top$，其中 $U$ 的第 $i$ 列 $u_i = \text{sgn}(\lambda_i)q_i$ (如果 $\lambda_i \neq 0$) 或 $u_i=q_i$ (如果 $\lambda_i = 0$)。

对于一般的矩阵 $A$ (不一定对称或方阵)，我们有：
- $A^\top A = (U \Sigma V^\top)^\top (U \Sigma V^\top) = V \Sigma^\top U^\top U \Sigma V^\top = V (\Sigma^\top \Sigma) V^\top$。
- $A A^\top = (U \Sigma V^\top) (U \Sigma V^\top)^\top = U \Sigma V^\top V \Sigma^\top U^\top = U (\Sigma \Sigma^\top) U^\top$。

注意到 $A^\top A$ (大小 $n \times n$) 和 $AA^\top$ (大小 $m \times m$) 都是对称且半正定的矩阵。
- $V$ 的列是 $A^\top A$ 的标准正交特征向量。
- $U$ 的列是 $AA^\top$ 的标准正交特征向量。
- $A^\top A$ 和 $AA^\top$ 的非零特征值是相同的，它们等于 $\sigma_i^2$ (奇异值的平方)。

所以，SVD 与应用于 $A^\top A$ 和 $AA^\top$ 的**谱定理**密切相关。
- **具体做法**：
    1. 计算 $A^\top A$ (对称半正定)。
    2. 对 $A^\top A$ 进行谱分解：$A^\top A = V \Lambda_{V} V^\top$。$\Lambda_V$ 的对角元素 $\lambda_i(A^\top A) = \sigma_i^2 \ge 0$ 是 $A^\top A$ 的特征值。$V$ 的列是 $A^\top A$ 的标准正交特征向量。
    3. 奇异值 $\sigma_i = \sqrt{\lambda_i(A^\top A)}$。构造 $\Sigma$ 矩阵。
    4. 计算 $AA^\top$ (对称半正定)。
    5. 对 $AA^\top$ 进行谱分解：$AA^\top = U \Lambda_{U} U^\top$。$\Lambda_U$ 的对角元素 $\lambda_i(AA^\top) = \sigma_i^2 \ge 0$ 是 $AA^\top$ 的特征值。$U$ 的列是 $AA^\top$ 的标准正交特征向量。
    6. 确保 $U, \Sigma, V$ 的对应关系正确（例如通过 $Av_i = \sigma_i u_i$ 和 $A^\top u_i = \sigma_i v_i$ 来调整 $u_i$ 或 $v_i$ 的符号）。
    7. 得到 $A = U \Sigma V^\top$。

这种通过构造 $A^\top A$ 或 $AA^\top$ 的方法在数值上可能不稳定（特别是当 $A$ 的条件数很大时），实际的 SVD 算法（如基于 QR 分解的迭代方法）通常更稳健。
## PCA (主成分分析)

- 假设我们有一组“数据点” $x_j \in \mathbb{R}^m$，其中 $j = 1, \dots, n$。
    - $m$ 是数据空间的维度，$n$ 是数据点的数量。
- 目标：希望找到一个维度为 $k$（给定）的**子空间**，能够尽可能好地“捕捉”数据。
    - 用统计学的术语来说，即找到能够“**解释尽可能多方差**”的子空间。
- 假设数据的经验均值为零，即 $\frac{1}{n} \sum_{i=1}^n x_i = 0$。
    - 这总是可以通过用 $x_i \leftarrow x_i - \frac{1}{n} \sum_{j=1}^n x_j$ 替换 $x_i$ 来实现。
    - 这被称为**数据去均值 (de-meaning the data)**。
- 可以构建数据矩阵 $X = [x_1 | \dots | x_n] \in \mathbb{R}^{m \times n}$ (这里将每个数据点作为一列)。
    - 补充说明：$\frac{1}{n} XX^T = \frac{1}{n} \sum_i x_i x_i^T$ 被称为*经验协方差矩阵 (empirical covariance matrix)*。
- 需要将其量化为一个优化问题。
    - 希望优化 $q_1, \dots, q_k$（它们构成最佳子空间的一组标准正交基）。
    - 令 $Q = [q_1 | \dots | q_k]$，因此可以转而优化满足 $Q^T Q = I_k$ 的矩阵 $Q \in \mathbb{R}^{m \times k}$。
    - 对于满足 $Q^T Q = I_k$ 的矩阵，并没有一个完全标准的名称，但我们可以说这样的 $Q$ 是**部分正交的 (partially orthogonal)** 或者简单地说它**具有标准正交的列 (has orthonormal columns)**。
    - 注意：$P_Q := QQ^T$ 是到 $\text{span}(Q) = \text{col}(Q)$（$Q$的列空间）上的正交投影算子。

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
    这可以用矩阵形式简洁地表示为： $Q^T (x - P_Q x) = \mathbf{0}$ (零向量)。
    我们来计算：
    $$\begin{align}
    Q^T (x - P_Q x)  &= Q^T (x - QQ^T x)  \\
                     &= Q^T x - \underbrace{Q^T (QQ^T x)}_{\text{括号结合}} \\
                     &= Q^T x - (Q^T Q)Q^T x \\
                     &= Q^T x - I_k Q^T x \quad (\text{因为 } Q^T Q = I_k) \\
                     &= Q^T x - Q^T x \\
                     &= \mathbf{0}
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

- 需要**最小化**的目标函数是：
$$f(Q) := \sum_{i=1}^n \|x_i - P_Q x_i\|^2$$
    - 它衡量了每个数据点 $x_i$ 与其在该子空间上的正交投影（即子空间中离 $x_i$ 最近的点）之间的偏差的平方和。
    - 显然，如果所有 $x_i \in \text{span}(Q)$（即所有数据都位于该子空间内），则该值为零。
    - 该函数衡量了与这种理想情况的偏差。
- 符号说明：“span”一个矩阵指的是其**列向量的张成空间 (span of its columns)**。它与列空间 (column space) 完全相同。
- 计算：
$$ f(Q) = \sum_{i=1}^n \|x_i - P_Q x_i\|^2 = \sum_{i=1}^n \|(I - QQ^T)x_i\|^2 $$
    - 注意：$(I - QQ^T)x_i$ 是矩阵 $(I - QQ^T)X = X - QQ^T X$ 的第 $i$ 列，而弗罗贝尼乌斯范数的平方等于各列范数平方之和。
    - 因此 $f(Q) = \|X - QQ^T X\|_F^2$。
    > 这是根据弗罗贝尼乌斯范数的定义。
- 令 $X = U \Sigma V^T = \sum_{i=1}^r \sigma_i u_i v_i^T$ 为 $X$ 的**紧凑 SVD (compact SVD)**，其中 $r := \text{rank}(X)$。
    - 这里 $U = [u_1 | \dots | u_r]$ ($m \times r$)，$V = [v_1 | \dots | v_r]$ ($n \times r$)。
- 令 $\tilde{X} = \tilde{U} \tilde{\Sigma} \tilde{V}^T = \sum_{i=1}^k \sigma_i u_i v_i^T$ 为**截断 SVD (truncated SVD)** (截断到秩 $k$)。
    - 这里 $\tilde{U} = [u_1 | \dots | u_k]$ ($m \times k$)，$\tilde{V} = [v_1 | \dots | v_k]$ ($n \times k$)。
- 注意到 $\text{rank}(QQ^T X) \le k$，因此我们从截断SVD的“最佳秩-$k$逼近”性质得知，如果我们能选择 $Q$ 使得 $QQ^T X = \tilde{U} \tilde{\Sigma} \tilde{V}^T$，那将是最优的。

根据 **Eckart-Young-Mirsky 定理**，这个 $\tilde{X}$ 是所有秩不超过 $k$ 的矩阵中，与原矩阵 X 在弗罗贝尼乌斯范数意义下**最接近**的矩阵。也就是说，$\|X-B\|_F^2$ 的最小值在 $B = \tilde{X}$ 时取到，对于所有 $\text{rank}(B) \le k$。

- 那么只需选择 $Q = \tilde{U}$，所以：
$$ QQ^T X = (\tilde{U}\tilde{U}^T) X = \tilde{U}\tilde{U}^T \left(\sum_{i=1}^r \sigma_i u_i v_i^T\right) $$
  考虑到 $\tilde{U}^T u_i$ 的性质：
    - 如果 $1 \le i \le k$，则 $u_i$ 是 $\tilde{U}$ 的一列（第 $i$ 列），由于 $\tilde{U}$ 的列是标准正交的，$\tilde{U}^T u_i = e_i$ (第 $i$ 个标准单位向量)。那么 $\tilde{U}(\tilde{U}^T u_i) = \tilde{U}e_i = u_i$。
    - 如果 $i > k$，则 $u_i$ 与 $\tilde{U}$ 的所有列（即 $u_1, \dots, u_k$）正交，因此 $\tilde{U}^T u_i = \mathbf{0}$ (零向量)。那么 $\tilde{U}(\tilde{U}^T u_i) = \mathbf{0}$。
  所以：
$$ QQ^T X = \sum_{i=1}^k \sigma_i (\tilde{U}\tilde{U}^T u_i) v_i^T + \sum_{i=k+1}^r \sigma_i (\tilde{U}\tilde{U}^T u_i) v_i^T = \sum_{i=1}^k \sigma_i u_i v_i^T + \sum_{i=k+1}^r \sigma_i \cdot \mathbf{0} \cdot v_i^T = \sum_{i=1}^k \sigma_i u_i v_i^T = \tilde{X} $$
  （原文 $QQ^T X = \sum_{i=1}^r \tilde{U} \tilde{U}^T \sigma_i u_i v_i^T = \sum_{i=1}^k \sigma_i u_i v_i^T = \tilde{U} \tilde{\Sigma} \tilde{V}^T$ 的表述可以这样理解）


- 总结来说，最优子空间由（**去均值后的**）数据矩阵 $X$ 的前 $k$ 个左**奇异向量 (singular vectors)** 的张成空间给出。
    - 或者说，它由经验协方差矩阵 $\frac{1}{n} XX^T$ 的前 $k$ 个主特征向量的张成空间给出。
- 对于一个数据点 $x_j$，它在第 $i$ 个奇异向量方向上的分量 $u_i \cdot x_j$ (即 $u_i^T x_j$) 被称为数据的第 $i$ 个**主成分 (principal component)**。
    - 因此，矩阵 $Q^T X \in \mathbb{R}^{k \times n}$ 的第 $j$ 列是 $(u_1^T x_j, \dots, u_k^T x_j)^T \in \mathbb{R}^k$，它是由第 $j$ 个数据点的前 $k$ 个主成分组成的向量。

- 我们可以使用 PCA 进行降维 (dimensionality reduction)：
    - $Y := Q^T X$ 的列向量 $y_j$ 是数据点 $x_j$ 在线性变换 $Q^T$（该变换将向量从 $\mathbb{R}^m$ 映射到 $\mathbb{R}^k$）下的像。
    - 因此，映射 $Q^T$ 可以被认为是“*压缩 (compressing)*”我们的数据集。
    - 要从压缩后的数据集中近似地*恢复 (recover)* 原始数据集，我们可以构造 $\tilde{X} = QY = QQ^T X$。
        - 回想一下，$Q$ 是为了最小化恢复误差 $\| \tilde{X} - X \|_F$ 而优化的。
        - 因此，尽管这种压缩是“有损的 (lossy)”，但考虑到我们将数据压缩到 $k$ 维，它是**尽可能忠实的 (as faithful as possible)**。
    > 这个 $\tilde{X}$ 是 $X$ 在 $\text{col}(Q)$ 上的正交投影。
# 39 子空间迭代 (Subspace iteration)

## 39.1 基本算法

* 令 $A \in \mathbb{R}^{n \times n}$ 是可对角化的（为简单起见）。令 $\lambda_1, \dots, \lambda_n$ 表示其特征值（可能根据重数重复），并按如下顺序排列：
    $$|\lambda_1| \ge \dots \ge \underbrace{ |\lambda_k| > |\lambda_{k+1}| }_{\text{谱间隙 (spectral gap)} > 0} \ge \dots \ge |\lambda_n|$$
* 令 $u_1, \dots, u_n$ 表示对应的特征向量组成的一个基，并令 $U = [u_1 | \dots | u_k] \in \mathbb{R}^{n \times k}$。
    * 目前我们不假设 $A$ 是对称的，所以这些特征向量不一定是标准正交的！

* 我们想在某种意义上找到子空间 $\text{span}(U)$。
* 令 $W = [w_1 | \dots | w_k] \in \mathbb{R}^{n \times k}$。（初始猜测矩阵）
* **定理：** 对于“*泛型 (generic)*”的初始猜测矩阵 $W \in \mathbb{R}^{n \times k}$，存在一个合适的可逆矩阵序列 $C_l \in \mathbb{R}^{k \times k}$，$l = 0, 1, 2, \dots$，使得：
    $$\lim_{l \to \infty} A^l W C_l = U$$
    * 在证明中，我们将说明“*泛型*”的含义（推广幂法的条件），并且我们将构造序列 $C_l$。
* **含义：** 当 $l \to \infty$ 时，$A^l W = A(A(A(\dots AW) \dots )))$ 并非严格“收敛”到 $U$，但其张成的子空间“收敛”到作为子空间的 $\text{span}(U)$。
    * 然而，如果我们直接计算 $A^l W$ 且 $l$ 很大，将会遇到数值上溢/下溢的问题。
    * 因此，实际的实用算法将包含一个**推广的规范化过程 (generalization of the normalization procedure)**，类似于幂法中使用的那样。

* 这提出了实用的算法（**子空间迭代 (subspace iteration)**），我们暂时不给出停止准则：
    * 给定泛型的初始猜测矩阵 $W \in \mathbb{R}^{n \times k}$，最大迭代次数 $m$，以及执行与 $A$ 进行矩阵向量乘法的能力。
    * 令 $V$ 的列向量是标准正交的，并且其张成的空间与 $W$ 的列向量张成的空间相同。（这可以通过格拉姆-施密特过程实现，或者等价地，通过对 $W$ 进行QR分解 $W=VR$ 来实现。Matlab 函数 `orth` 也可以使用。）
        * **具体做法 (初始化 $V$)**: 对 $W$ 进行 QR 分解，$W = Q_{QR}R_{QR}$。令 $V = Q_{QR}$（取 $Q_{QR}$ 的前 $k$ 列，如果 $W$ 的秩小于 $k$，则可能需要特殊处理，但通常假设 $W$ 的列是线性无关的，或者取其张成空间的一个标准正交基）。
    * 对于 $j = 0, 1, \dots, m$：
        * 令 $W \leftarrow AV$。（注意这需要 $k$ 次与 $A$的矩阵向量乘法，每列一次。）
        * 令 $V$ 的列向量是**标准正交的 (orthonormal)**，并且其张成的空间与 $W$ 的列向量张成的空间相同。(*再次进行 QR 分解*)
            * **具体做法 (更新 $V$)**: 对上一步得到的新的 $W$ 进行 QR 分解，$W = Q_{QR}R_{QR}$。令 $V = Q_{QR}$。
    * 返回 $V$。

* 注意，每次迭代的主要工作量包括 (1) $k$ 次与 $A$ 的矩阵向量乘法 和 (2) 对 $W$ 的 $k$ 个列向量进行标准正交化。
    * 标准正交化的成本是 $O(nk^2)$，这可以通过计算格拉姆-施密特过程中的运算次数来验证。
    * 例如，如果 $A$ 是稀疏矩阵，有 $O(n)$ 个非零元素，那么每次迭代中矩阵向量乘法的成本是 $O(nk)$。如果 $A$ 是完全稠密的（最坏情况），每次迭代的成本也只有 $O(n^2 k)$。
    * 与完全**对角化 (diagonalization)** 的成本 $O(n^3)$ 相比！
    > 子空间迭代的成本大约是 $m \times O(nk + nk^2)$ 或 $m \times O(n^2 k + nk^2)$。
* 如果迭代次数 $m$ **足够**大，那么最终输出的 $V$ 的列向量将构成一个*标准正交基*，其张成的子空间非常接近 $\text{span}(U)$。
* 稍后我们将改进该算法，以包含一个当算法收敛到指定容差内时停止的准则。然而，这比幂法的情况需要更仔细的处理。
* 我们稍后还将解释如何从恢复的子空间 $\text{span}(V)$ 中恢复实际的特征对。

## 39.2 收敛性证明

* **证明 (定理的证明):**
    * 我们将在下面构造 $C_l$，并用***粗斜体***给出对 $W$ 的*泛型性*条件。
    * 首先令 $P$ 的列向量为 $u_1, \dots, u_n$，所以
        $$P = [U | V_{rest}]$$
        其中 $U=[u_1 | \dots | u_k]$，$V_{rest}=[u_{k+1} | \dots | u_n]$。（注意：这里 $V_{rest}$ 与算法迭代中的 $V$ 不同，仅为表示方便）
        > * （注意，由于未假设 $A$ 是对称的，列向量 $u_i$ 不一定是正交的。）
        > * 需要说明的是，这个 $P$ 来自于 $A = P\Lambda P^{-1}$，我们想要获取 $A$ 的信息（前 $k$ 个不变子空间）。

    * 那么 $A = P \Lambda P^{-1}$，其中 $\Lambda = \text{diag}(\lambda_1, \dots, \lambda_n)$。我们将 $\Lambda$ 与 $P$ 进行分块：
        $$ \Lambda = \begin{pmatrix} \Lambda_1 & 0 \\ 0 & \Lambda_2 \end{pmatrix} $$
        其中左上角块 $\Lambda_1 = \text{diag}(\lambda_1, \dots, \lambda_k)$ 是 $k \times k$ 的，$\Lambda_2 = \text{diag}(\lambda_{k+1}, \dots, \lambda_n)$ 是 $(n-k) \times (n-k)$ 的。*注意对角矩阵 $\Lambda_1$ 是可逆的，因为 $|\lambda_1| \ge \dots \ge |\lambda_k| > |\lambda_{k+1}| \ge 0$，这意味着 $\lambda_1, \dots, \lambda_k$ 都非零。*
    * 令 $Y = P^{-1} W$。我们将 $Y$ 进行分块：
        $$ Y = \begin{pmatrix} Y_1 \\ Y_2 \end{pmatrix} $$
        其中上块 $Y_1$ 是 $k \times k$ 的，$Y_2$ 是 $(n-k) \times k$ 的。我们假设 $W$ 满足*泛型性*条件，这等价于：***$Y_1$ 具有满秩，即可逆***。
    * 在这种情况下，令 $C_l = Y_1^{-1} \Lambda_1^{-l}$。由于 $Y_1$ 和 $\Lambda_1$ 是可逆的，$C_l$ 也是可逆的。现在我们来考察极限：
        $$ A^l W C_l = (P \Lambda P^{-1})^l W C_l = P \Lambda^l P^{-1} W C_l = P \Lambda^l Y C_l $$
    * 代入分块形式和 $C_l$ 的定义：
        $$ A^l W C_l = P \begin{pmatrix} \Lambda_1^l & 0 \\ 0 & \Lambda_2^l \end{pmatrix} \begin{pmatrix} Y_1 \\ Y_2 \end{pmatrix} (Y_1^{-1} \Lambda_1^{-l}) = P \begin{pmatrix} \Lambda_1^l Y_1 \\ \Lambda_2^l Y_2 \end{pmatrix} (Y_1^{-1} \Lambda_1^{-l}) $$
        $$ = P \begin{pmatrix} \Lambda_1^l Y_1 Y_1^{-1} \Lambda_1^{-l} \\ \Lambda_2^l Y_2 Y_1^{-1} \Lambda_1^{-l} \end{pmatrix} = P \begin{pmatrix} I_k \\ \Lambda_2^l Y_2 Y_1^{-1} \Lambda_1^{-l} \end{pmatrix} $$
    * 我们断言，上式中整个下块 $\Lambda_2^l Y_2 Y_1^{-1} \Lambda_1^{-l}$ 当 $l \to \infty$ 时*收敛到零矩阵*。
        * 要理解这一点，令 $B := Y_2 Y_1^{-1}$（一个常数 $(n-k) \times k$ 矩阵）。我们需要证明当 $l \to \infty$ 时 $M_l := \Lambda_2^l B \Lambda_1^{-l} \to 0$。
        * $M_l$ 的 $(i, j)$ 项由下式给出：
            $$ (M_l)_{ij} = (\lambda_{k+i})^l B_{ij} (\lambda_j)^{-l} = \left( \frac{\lambda_{k+i}}{\lambda_j} \right)^l B_{ij} $$
            对于 $i = 1, \dots, n-k$ 和 $j = 1, \dots, k$。
        * 根据特征值的排序，我们知道对于 $i \ge 1$，有 $|\lambda_{k+i}| < |\lambda_k|$；对于 $j \le k$，有 $|\lambda_j| \ge |\lambda_k|$。因此，
            $$ \left| \frac{\lambda_{k+i}}{\lambda_j} \right| \le \frac{|\lambda_{k+i}|}{|\lambda_k|} < 1 $$
            由于幂的*底数*的绝对值*严格*小于1，所以当 $l \to \infty$ 时，每一项 $(M_l)_{ij} \to 0$。因此，矩阵 $M_l$ 收敛到零矩阵。
    * 因此，当 $l \to \infty$ 时取极限：
        $$ \lim_{l \to \infty} A^l W C_l = P \begin{pmatrix} I_k \\ 0 \end{pmatrix} = [U | V_{rest}] \begin{pmatrix} I_k \\ 0 \end{pmatrix} = U I_k + V_{rest} 0 = U $$
        证毕。

## 39.3 子空间之间的距离

* 我们需要一个条件来判断子空间迭代是否已在期望的容差范围内收敛。
* 这样做有些棘手，因为我们希望将子空间迭代视为提供一个子空间序列。**我们如何衡量两个子空间之间的距离？**
* 衡量两个子空间之间距离的一种方法是*计算它们对应的正交投影矩阵之间的矩阵范数距离*。
* 考虑两个子空间 $\text{span}(V)$ 和 $\text{span}(\tilde{V})$，其中 $V \in \mathbb{R}^{n \times k}$ 和 $\tilde{V} \in \mathbb{R}^{n \times k}$ 的列向量是标准正交的（即 $V^T V = I_k$ 和 $\tilde{V}^T \tilde{V} = I_k$）。
    * 那么 $P := VV^T$ 和 $Q := \tilde{V}\tilde{V}^T$ 分别是到这两个子空间上的 $n \times n$ 正交投影矩阵。
    * **我们将计算弗罗贝尼乌斯范数的平方距离** $\|P - Q\|_F^2$。

* 需要用到涉及矩阵**迹 (trace)** $\text{Tr}[B]$（也记作 $\text{tr}(B)$ 或 $\text{trace}(B)$）的两个性质，迹是方阵 $B$ 对角元素之和。
    * **性质 1：** 对于任意矩阵 $A$（不一定是方阵），
        $$\|A\|_F^2 = \text{Tr}[A^T A] = \text{Tr}[AA^T]$$
    * **性质 2：** 对于任意矩阵 $B$ ($m \times n$) 和 $C$ ($n \times m$)，$\text{Tr}[BC] = \text{Tr}[CB]$ (迹的循环性质)。
    * 我们在课堂上验证过，但你自己尝试也是一个很好的练习！
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

* **计算过程：**
    * 首先，注意 $P$ 和 $Q$ 是对称的（$P^T=P, Q^T=Q$）且是幂等的（$P^2=P, Q^2=Q$）。使用性质 1 展开：
        $$\begin{align}
        \|P - Q\|_F^2  &= \text{Tr}[(P - Q)^T (P - Q)]  \\
                         &= \text{Tr}[(P - Q)(P - Q)] \quad (\text{因为 } P-Q \text{ 是对称的}) \\
                         &= \text{Tr}[P^2 - QP - PQ + Q^2]
        \end{align} $$
    * 利用幂等性（$P^2=P, Q^2=Q$）和性质 2（$\text{Tr}[QP] = \text{Tr}[PQ]$）：
        $$ \|P - Q\|_F^2 = \text{Tr}[P] + \text{Tr}[Q] - 2\text{Tr}[PQ] $$
    * 代入 $P=VV^T$ 和 $Q=\tilde{V}\tilde{V}^T$：
        $$ \|P - Q\|_F^2 = \text{Tr}[VV^T] + \text{Tr}[\tilde{V}\tilde{V}^T] - 2\text{Tr}[VV^T \tilde{V}\tilde{V}^T] $$
    * 现在使用性质 2（循环性质）来重新排列迹内的矩阵。同时使用 $V^T V = I_k$ 和 $\tilde{V}^T \tilde{V} = I_k$：
        > 因为我们假设 $V$ 和 $\tilde{V}$ 的列是标准正交的。
        $$ \text{Tr}[VV^T] = \text{Tr}[V^T V] = \text{Tr}[I_k] = k $$
        $$ \text{Tr}[\tilde{V}\tilde{V}^T] = \text{Tr}[\tilde{V}^T \tilde{V}] = \text{Tr}[I_k] = k $$
        $$ \text{Tr}[VV^T \tilde{V}\tilde{V}^T] = \text{Tr}[\tilde{V}^T (VV^T) \tilde{V}] = \text{Tr}[\underbrace{ (\tilde{V}^T V) }_{ X^T } \underbrace{ (V^T \tilde{V}) }_{ X }] $$
        (原文此处 $X'$ 和 $X$ 的定义与标准 $X^T X$ 略有不同，但结果是相同的，令 $X = V^T \tilde{V}$，则 $\tilde{V}^T V = X^T$)
    * 令 $X = V^T \tilde{V}$ (一个 $k \times k$ 矩阵)。最后一个迹项变为 $\text{Tr}[X^T X]$。根据性质 1，$\text{Tr}[X^T X] = \|X\|_F^2 = \|V^T \tilde{V}\|_F^2$。
    * 将这些代回：
        $$ \|P - Q\|_F^2 = k + k - 2\|V^T \tilde{V}\|_F^2 = 2k - 2\|V^T \tilde{V}\|_F^2 $$
    * 同样有用的是注意到 $\|P\|_F^2 = \text{Tr}[P^T P] = \text{Tr}[P^2] = \text{Tr}[P] = k$。所以“相对距离”可以计算为：
        $$ \frac{\|P - Q\|_F}{\|P\|_F} = \frac{\sqrt{2k - 2\|V^T \tilde{V}\|_F^2}}{\sqrt{k}} = \sqrt{\frac{2(k - \|V^T \tilde{V}\|_F^2)}{k}} = \sqrt{2 \left( 1 - \frac{\|V^T \tilde{V}\|_F^2}{k} \right)} $$
* **定理：** 如果 $V$ 和 $\tilde{V}$ 是具有标准正交列的 $n \times k$ 矩阵，并且 $P=VV^T$ 和 $Q=\tilde{V}\tilde{V}^T$ 分别是到 $\text{span}(V)$ 和 $\text{span}(\tilde{V})$ 上的正交投影矩阵，则
    $$ \|P - Q\|_F^2 = 2 ( k - \|V^T \tilde{V}\|_F^2 ) $$
    且
    $$ \frac{\|P - Q\|_F}{\|P\|_F} = \sqrt{2 \left( 1 - \frac{1}{k} \|V^T \tilde{V}\|_F^2 \right)} . $$
* 关键点在于，我们可以使用涉及 $\|V^T \tilde{V}\|_F^2$ 的公式来计算弗罗贝尼乌斯范数距离 $\|P - Q\|_F$（或其平方），而**无需显式地构建 $n \times n$ 的投影矩阵 $P$ 和 $Q$**。直接构建 $P=VV^T$ 或 $Q=\tilde{V}\tilde{V}^T$ 大约需要 $O(n^2 k)$ 次运算，对于大的 $n$ 来说非常昂贵。
    * 相反，成本主要由构建 $k \times k$ 矩阵 $X = V^T \tilde{V}$ 决定。
    * 这个矩阵乘法需要 $O(nk^2)$ 次浮点运算。
    * 从 $X$ 计算 $\|X\|_F^2$ 只需要 $O(k^2)$ 次运算。
    * 因此，使用这个公式评估距离的总成本仅为 $O(nk^2)$，效率高得多。

## 39.4 完整的伪代码

* 如果在子空间迭代中 $V$ 是我们当前的猜测（标准正交基矩阵），$\tilde{V}$ 是下一次迭代得到的基矩阵，那么**我们可以使用它们张成空间上的正交投影矩阵之间的相对弗罗贝尼乌斯范数距离**，
    $$ \frac{\|VV^T - \tilde{V}\tilde{V}^T\|_F}{\|VV^T\|_F} = \sqrt{2 \left( 1 - \frac{1}{k} \|V^T \tilde{V}\|_F^2 \right)} $$
    作为收敛的度量。

* 这提出了以下子空间迭代的伪代码，现在包含了停止准则：

    * **输入：**
        * 泛型的初始猜测矩阵 $W \in \mathbb{R}^{n \times k}$。
        * 最大迭代次数 $m$。
        * 执行与 $A$ 进行矩阵向量乘法的能力。
        * 收敛容差 $\epsilon > 0$。

    * **初始化：**
        * 计算 $V \in \mathbb{R}^{n \times k}$，使其列向量是标准正交的，并且 $\text{span}(V) = \text{span}(W)$。（例如，使用 $W$ 的 QR 分解，或 `orth(W)`）。

    * **迭代循环：**
        * 对于 $j = 0, 1, \dots, m$：
            * **幂步 (Power Step)：** 计算 $W_{next} \leftarrow AV$。（需要 $k$ 次矩阵向量乘积）。
            * **标准正交化 (Orthonormalization)：** 计算 $\tilde{V} \in \mathbb{R}^{n \times k}$，使其列向量是标准正交的，并且 $\text{span}(\tilde{V}) = \text{span}(W_{next})$。（例如，使用 $W_{next}$ 的 QR 分解，或 `orth(W_{next})`）。
            * **收敛性检查 (Convergence Check)：** 计算当前子空间（span $V$）和下一个子空间（span $\tilde{V}$）之间的相对距离度量：
                $$ \delta := \sqrt{2 \left( 1 - \frac{1}{k} \|V^T \tilde{V}\|_F^2 \right)} $$
                *（注意：此计算需要 $O(nk^2)$ 次运算，主要由计算 $V^T \tilde{V}$ 决定）*。
            * **更新 (Update)：** 令 $V \leftarrow \tilde{V}$。
            * **检查并停止 (Check & Stop)：** 如果 $\delta < \epsilon$，则 BREAK （退出循环）。

    * **输出：** 返回最终矩阵 $V$。

* 输出 $V$ 包含一个标准正交基，使得 $\text{span}(V)$ 近似等于目标主不变子空间 $\text{span}(U)$。

## 39.5 通过瑞利-里兹过程恢复特征对 (Recovering eigenpairs via Rayleigh-Ritz)

* **在本节中，我们将假设 $A$ 是对称的。**
* 子空间迭代（为简单起见，假设我们已经完全收敛）提供了一个矩阵 $V \in \mathbb{R}^{n \times k}$，其列向量构成了 $A$ 的前 $k$ 个主特征向量的张成空间 $\text{span}(U)$ 的一个标准正交基。因此，
    $$\text{span}(U) = \text{span}(V)$$
    * 由于 $A$ 是对称的，根据**谱定理 (spectral theorem)**，我们知道特征向量 $u_1, \dots, u_n$ 可以被选择为构成一个标准正交基。因此，构成 $U$ 的列向量（真正的主特征向量）$u_1, \dots, u_k$ 可以被假设为标准正交的，即 $U^T U = I_k$。

> **谱定理（针对实对称矩阵 $A \in \mathbb{R}^{n \times n}$, $A^T = A$）的主要内容：**
> 1.  **所有特征值都是实数**: 对称矩阵 $A$ 的所有特征值 $\lambda_1, \dots, \lambda_n$ 都是实数。
> 2.  **可对角化**: 对称矩阵 $A$ 总是可以被对角化。
> 3.  **特征向量的正交性**:
>     * 对应于**不同**特征值的特征向量是**相互正交 (orthogonal)** 的。
>     * 更强的是：**存在**一个由 $A$ 的特征向量组成的 $\mathbb{R}^n$ 的**标准正交基 (orthonormal basis)**。这意味着我们可以找到 $n$ 个特征向量 $q_1, \dots, q_n$，它们不仅两两正交 ($q_i^T q_j = 0$ for $i \neq j$)，而且每个向量的长度都为 1 ($q_i^T q_i = 1$)。
> 4.  **正交对角化 (Orthogonal Diagonalization)**: 上述性质保证了对称矩阵 $A$ 可以被**正交对角化**。也就是说，存在一个**正交矩阵 (orthogonal matrix)** $Q$ 和一个**实对角矩阵 (real diagonal matrix)** $\Lambda$，使得：
>
>     $$ A = Q \Lambda Q^T $$
>
>     其中：
>     * $Q$ 是一个 $n \times n$ 的正交矩阵 ($Q^T Q = QQ^T = I_n$)。$Q$ 的列向量 $(q_1, \dots, q_n)$ 就是 $A$ 的那组标准正交的特征向量。
>     * $\Lambda$ 是一个 $n \times n$ 的对角矩阵，其对角线上的元素 $(\lambda_1, \dots, \lambda_n)$ 是 $A$ 的对应特征值。

* 然而，子空间迭代算法本身只返回基 $V$；我们实际上并没有恢复**特征对 (eigenpairs)**（特征值 $\lambda_j$ 和特征向量 $u_j$）。
    * 在恢复构成 $U$ 的“那些”特定的特征向量 $u_1, \dots, u_k$ 这项任务中存在一些模糊性。
    * 这是由于特征向量的任意符号（或复相位，尽管实对称矩阵具有实特征向量）以及如果在主特征值组 $\lambda_1, \dots, \lambda_k$ 中存在重复特征值时可能存在的非唯一性。
    * 因此，我们不能期望恢复我们理论上可能定义的精确矩阵 $U$。
* 相反，我们的目标是恢复：
    * 主特征值 $\lambda_1, \dots, \lambda_k$（如果某些相等，则可能需要置换）。
    * 一组对应的标准正交特征向量 $q_1, \dots, q_k$，使得 $\text{span}(q_1, \dots, q_k) = \text{span}(U)$ 并且它们满足特征向量方程 $Aq_j = \lambda_j q_j$，对于 $j = 1, \dots, k$。
* 注意到特征向量方程 $Au_j = \lambda_j u_j$ 对于 $j = 1, \dots, k$，可以被重新组合成单个矩阵方程 $AU = U \Lambda_1$，其中 $\Lambda_1 = \text{diag}(\lambda_1, \dots, \lambda_k)$ 是主特征值的 $k \times k$ 对角矩阵（如收敛性证明中所用）。
* **因此，类似地，我们寻求一个具有标准正交列的 $n \times k$ 矩阵 $Q = [q_1 | \dots | q_k]$ ($Q^T Q = I_k$) 使得 $AQ = Q\Lambda_1$。**
* **瑞利-里兹过程 (Rayleigh-Ritz procedure)**，应用于从子空间迭代获得的基 $V$，提供了一种实现这一目标的方法：
    * **步骤 1：** 构建 $k \times k$ 矩阵 $\tilde{A} = V^T A V$。由于 $A$ 是对称的，$\tilde{A}$ 也是对称的。（$\tilde{A}^T = (V^T A V)^T = V^T A^T (V^T)^T = V^T A V = \tilde{A}$）。
    > **关于 $\tilde{A}$ 的理解:**
    > 1. 让 $V$ 的各个列向量作为子空间 $S = \text{span}(V)$ 的一个标准正交基。
    > 2. 对于所有 $x \in S$，我们有 $x = Vy$，其中 $y \in \mathbb{R}^k$，$y = V^T x$ 是 $x$ 在这个基下的坐标。
    > 3. 当我们将线性算子 $A$ 作用在 $x$ 上时，$Ax$ 可能不完全落在子空间 $S$ 内。
    > 4. 于是我们想到去找 $Ax$ 在 $S$ 上的正交投影，即 $P_S (Ax) = VV^T (Ax)$。
    > 5. 这个投影向量在基 $V$ 下的坐标是 $y_{proj} = V^T (P_S (Ax)) = V^T (VV^T Ax) = (V^T V)V^T Ax = I_k V^T Ax = V^T Ax$。
    > 6. 如果我们将原始向量 $x$ 的坐标 $y$ 代入，即 $x=Vy$，那么投影后的坐标变为 $y_{proj} = V^T A (Vy) = (V^T A V)y = \tilde{A}y$。
    > 7. 换句话说，$\tilde{A} = V^T A V$ 是原线性算子 $A$ 先作用再投影到子空间 $S$ 后，在子空间 $S$ 的标准正交基 $V$ 下的矩阵表示。它也被称为 $A$ 在子空间 $\text{span}(V)$ 上的瑞利商矩阵。

    * **步骤 2：** 对这个小的 $k \times k$ 对称矩阵 $\tilde{A}$ 执行完全的特征分解（对角化）：
        * 找到一个 $k \times k$ 的正交矩阵 $\tilde{U}$（$\tilde{U}^T \tilde{U} = I_k$）和一个 $k \times k$ 的对角矩阵 $\tilde{\Lambda}$，使得 $\tilde{A} = \tilde{U} \tilde{\Lambda} \tilde{U}^T$。
        * $\tilde{\Lambda}$ 的对角元素是 $\tilde{A}$ 的特征值（称为**里兹值 (Ritz values)**），$\tilde{U}$ 的列是对应的标准正交特征向量。
        * **根据对称矩阵的谱定理，这样的分解总是存在的。**
        * 计算它涉及到求解一个标准的 $k \times k$ 特征值问题，通常需要 $O(k^3)$ 次运算（*与原始的大维度 $n$ 无关*）。
    * **步骤 3：** 构建 $A$ 的近似特征向量（称为**里兹向量 (Ritz vectors)**）为 $Q = V \tilde{U}$。
    > 我们在这里恢复 $Q = V \tilde{U}$，从而达到将 $\tilde{A}$ 的特征向量（它们是 $\mathbb{R}^k$ 中的坐标向量）转换回原始 $\mathbb{R}^n$ 空间中的近似特征向量的目的。

* 关于这个过程有两个断言：
    * **断言 1：** 从 $\tilde{A}$ 获得的特征值对角矩阵 $\tilde{\Lambda}$ 等于包含 $A$ 的**真正主特征值**的对角矩阵 $\Lambda_1$。（$\tilde{\Lambda} = \Lambda_1$，如果特征值有重复，则可能需要置换）。
    * **断言 2：** 构建的矩阵 $Q = V \tilde{U}$ 具有标准正交列（$Q^T Q = I_k$）
        * 并且满足期望的矩阵特征向量方程 $AQ = Q\Lambda_1$（使用真正的 $\Lambda_1$，根据断言1，它等于 $\tilde{\Lambda}$）。

* **断言的证明：** 我们从一个关联计算出的基 $V$ 和真实的基 $U$ 的子断言开始。
    * **子断言：** $V = U O$，对于某个 $k \times k$ 的正交矩阵 $O$。具体来说，我们可以证明 $O = U^T V$ 是可行的。
        * **证明 $V=U(U^T V)$：** 令 $O=U^T V$。我们计算 $UO = U(U^T V) = (UU^T)V$。由于 $A$ 是对称的，$U$ 具有标准正交列（$U^T U = I_k$），所以 $P_U = UU^T$ 是到 $\text{span}(U)$ 上的正交投影矩阵。由于子空间迭代完全收敛，我们有 $\text{span}(V) = \text{span}(U)$。将 $V$ 的列向量（它们已经在 $\text{span}(U)$ 中）投影到 $\text{span}(U)$ 上使它们保持不变。因此，$P_U V = (UU^T)V = V$。于是，$V = UO$。
        * **证明 $O=U^T V$ 是正交的：** 我们计算 $O^T O = (U^T V)^T (U^T V) = (V^T U^{TT}) (U^T V) = V^T U U^T V$。再次，由于 $UU^T = P_U$ 并且 $P_U V = V$，我们有 $O^T O = V^T (UU^T V) = V^T (P_U V) = V^T V$。由于 $V$ 的列向量是标准正交的（子空间迭代的输出），$V^T V = I_k$。因此，$O^T O = I_k$，这意味着 $O$ 是一个正交矩阵。
        * 这完成了子断言的证明（$V=UO$，其中 $O$ 是正交的）。
* **断言 1 的证明 ($\tilde{\Lambda} = \Lambda_1$)：**
    * 使用子断言 $V=UO$，代入 $\tilde{A}$ 的定义：
        $$ \tilde{A} = V^T A V = (UO)^T A (UO) = O^T U^T A U O $$
    * 现在使用矩阵特征向量方程 $AU = U\Lambda_1$：
        $$ \tilde{A} = O^T U^T (U \Lambda_1) O = O^T (U^T U) \Lambda_1 O $$
    * 由于 $U^T U = I_k$：
        $$ \tilde{A} = O^T I_k \Lambda_1 O = O^T \Lambda_1 O $$
    * 方程 $\tilde{A} = O^T \Lambda_1 O$ 表明 $\tilde{A}$ 通过一个**正交相似变换 (orthogonal similarity transformation)** 与对角矩阵 $\Lambda_1$ 相关联（因为 $O$ 是正交的，$O^T = O^{-1}$）。这意味着 $\tilde{A}$ 和 $\Lambda_1$ 具有相同的特征值。$\Lambda_1$ 的特征值是 $\lambda_1, \dots, \lambda_k$。$\tilde{A}$ 的特征值是来自特征分解 $\tilde{A} = \tilde{U} \tilde{\Lambda} \tilde{U}^T$ 的 $\tilde{\Lambda}$ 的对角元素。因此，$\tilde{\Lambda}$ 的对角元素必定是 $\lambda_1, \dots, \lambda_k$，如果某些 $\lambda_j$ 相等，则顺序可能不同。假设一个一致的排序（例如，非递增），我们有 $\tilde{\Lambda} = \Lambda_1$。断言 1 成立。
* **断言 2 的证明 ($AQ = Q\Lambda_1$ 且 $Q^T Q = I_k$)：**
    * 首先，检查 $Q=V\tilde{U}$ 是否具有标准正交列：
        $$ Q^T Q = (V\tilde{U})^T (V\tilde{U}) = (\tilde{U}^T V^T) (V \tilde{U}) = \tilde{U}^T (V^T V) \tilde{U} $$
        由于 $V^T V = I_k$ 且 $\tilde{U}$ 是正交的（$\tilde{U}^T \tilde{U} = I_k$）：
        $$ Q^T Q = \tilde{U}^T I_k \tilde{U} = \tilde{U}^T \tilde{U} = I_k $$
        所以 $Q$ 确实具有标准正交列。
    * 现在，我们验证 $AQ = Q\Lambda_1$。从 $AQ$ 开始并代入 $Q = V\tilde{U}$：
        $$ AQ = A(V\tilde{U}) $$
    * 代入 $V=UO$：
        $$ AQ = A(UO\tilde{U}) = (AU)O\tilde{U} $$
    * 使用 $AU = U\Lambda_1$：
        $$ AQ = (U\Lambda_1)O\tilde{U} = U\Lambda_1 O\tilde{U} $$
    * 插入 $I_k = OO^T$ (因为 $O$ 是正交的，原文此处可能有笔误，应该是 $I_k = O O^T$ 或 $O^T O$，这里用 $O^T O$ 更自然，但为了与 $O^T \Lambda_1 O = \tilde{A}$ 衔接，可能是指 $O$ 左乘 $\Lambda_1$ 再右乘 $O^T$ 得到 $\tilde{A}$ 的相似变换，但 $\tilde{A} = O^T \Lambda_1 O$。我们保持 $U \Lambda_1 O \tilde{U}$ 的形式，并利用 $\tilde{A}$ 的定义。)
        更直接的推导：
        我们有 $\tilde{A} = V^T A V$ 和 $\tilde{A} \tilde{U} = \tilde{U} \tilde{\Lambda}$ (因为 $\tilde{U}$ 的列是 $\tilde{A}$ 的特征向量，$\tilde{\Lambda}$ 是对应的特征值)。
        $$ AQ = A(V\tilde{U}) $$
        我们想证明它等于 $Q\Lambda_1 = (V\tilde{U})\Lambda_1 = V(\tilde{U}\Lambda_1)$。
        考虑 $V^T A Q = V^T A V \tilde{U} = \tilde{A} \tilde{U}$。
        又因为 $\tilde{A} \tilde{U} = \tilde{U} \tilde{\Lambda}$。
        所以 $V^T A Q = \tilde{U} \tilde{\Lambda}$。
        左乘 $V$：$V V^T A Q = V \tilde{U} \tilde{\Lambda}$。
        $P_V A Q = Q \tilde{\Lambda}$。
        由于 $Q$ 的列在 $\text{span}(V)$ 中（因为 $Q=V\tilde{U}$），并且我们假设子空间迭代已经收敛，所以 $A$ 作用于 $\text{span}(V)$ 中的向量（近似特征向量）大约还是在 $\text{span}(V)$ 中（如果是 $A$ 的不变子空间）。
        更严谨的证明回到原文的思路：
        $$ AQ = U\Lambda_1 O\tilde{U} $$
        我们知道 $\tilde{A} = O^T \Lambda_1 O$，所以 $\Lambda_1 = O \tilde{A} O^T = O (\tilde{U} \tilde{\Lambda} \tilde{U}^T) O^T$。
        代入 $AQ = U (O \tilde{U} \tilde{\Lambda} \tilde{U}^T O^T) O \tilde{U}$。这变得复杂。

        让我们重新审视原文的推导步骤，从 $AQ = V \tilde{A} \tilde{U}$ 开始（这是正确的，因为 $AQ = AV\tilde{U}$，而 $V\tilde{A}\tilde{U}$ 是目标 $Q\tilde{\Lambda}$ 的一种形式）。
        从 $AQ = (UO) \tilde{A} \tilde{U}$（因为 $V=UO$）
        我们有 $\tilde{A} = \tilde{U} \tilde{\Lambda} \tilde{U}^T$。
        所以 $AQ = (UO) (\tilde{U} \tilde{\Lambda} \tilde{U}^T) \tilde{U} = UO \tilde{U} \tilde{\Lambda} (\tilde{U}^T \tilde{U})$
        由于 $\tilde{U}^T \tilde{U} = I_k$：
        $$ AQ = UO \tilde{U} \tilde{\Lambda} $$
        我们想要证明 $UO\tilde{U} = Q = V\tilde{U}$。这是恒成立的。
        所以 $AQ = Q \tilde{\Lambda}$。
    * 最后，使用断言 1 ($\tilde{\Lambda} = \Lambda_1$)：
        $$ AQ = Q \Lambda_1 $$
    * 这建立了断言 2。

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
## 41.3 谱嵌入 (Spectral Embedding)

* **谱嵌入 (Spectral embedding)** 是一种**图嵌入 (graph embedding)** 技术。
	* 它定义了一个映射 $\Phi : \{1, \dots, n\} \to \mathbb{R}^d$，使得 $\Phi(i)$ 是图中第 $i$ 个顶点（对应于第 $i$ 个原始数据点 $x_i$）在该嵌入下的“像”或坐标。
	* 这里的 $d$ 通常远小于原始数据的维度 $m$ 或数据点个数 $n$。
* 嵌入之后，我们可以通过令 $y_i = \Phi(i)$ 定义一个新的数据集 $y_1, \dots, y_n \in \mathbb{R}^d$。
	* 这个新数据集就是原始数据在 $d$ 维嵌入空间中的表示，希望它能更好地揭示数据的内在结构（如簇）。
* 为了定义这个嵌入 $\Phi$，令 $U = [u_1, \dots, u_d] \in \mathbb{R}^{n \times d}$ 是一个矩阵，其列向量是**对称归一化拉普拉斯算子 $\hat{L}$ 的 $d$ 个最小特征值**（通常包括特征值 0 及其对应的特征向量，如果需要 $d > 1$）所对应的**特征向量**。
    * 这些特征向量可以通过**子空间迭代**来计算。因为子空间迭代找的是绝对值最大的特征值，而我们想要 $\hat{L}$ 最小的 $d$ 个特征值
    * （根据性质 4，它们在 $[0, 2]$ 区间内），我们可以将子空间迭代应用于矩阵 $M = cI - \hat{L}$（其中 $c$ 是一个常数，例如 $c=2$，使得 $M$ 的最大特征值对应 $\hat{L}$ 的最小特征值）。
    * 例如，当 $c=2$ 时，矩阵 $(2I - \hat{L})$ 的特征值是 $2 - \lambda_i(\hat{L})$。$(2I - \hat{L})$ 最大的 $d$ 个特征值就对应 $\hat{L}$ 最小的 $d$ 个特征值。
	    * 因此，对 $(2I - \hat{L})$ 使用子空间迭代可以找到所需的 $u_1, \dots, u_d$。
* 然后，我们将第 $i$ 个顶点的嵌入坐标定义为矩阵 $U$ 的**第 $i$ 行**（并将其视为一个 $d$ 维列向量）：
    $$ \Phi(i) = [U_{i,:}]^T \in \mathbb{R}^d $$
    也就是说，新的数据点 $y_i$ 就是由 $U$ 的第 $i$ 行构成的向量。这个 $y_i$ 就代表了原始数据点 $x_i$ 在 $d$ 维空间中的新坐标。

>[!Why do we need the embeddings?]
>- 是一种强大的**非线性降维**方法。
> - 能有效地处理**非凸、任意形状**的簇结构。
> - 通过利用数据的**图结构和连通性**信息，将数据变换到更适合聚类的低维空间。
> - 使得后续应用简单的聚类算法（如 k-均值）也能获得好的效果，尤其是在复杂数据集上。
## 41.4 聚类 (Clustering)

* 给定一个数据集 $x_1, \dots, x_n \in \mathbb{R}^m$，我们将描述如何将其划分 (partition) 为 $k$ 个**簇 (clusters)**。
    * **请注意**：我们描述的聚类算法既可以应用于本节开头提到的**原始数据集** $x_1, \dots, x_n \in \mathbb{R}^m$，也可以应用于通过**谱嵌入 (spectral embedding)** 得到的**新数据集** $y_1, \dots, y_n \in \mathbb{R}^d$。对不同的数据集应用该算法，通常会得到不同的聚类结果！

* 实现这种聚类的标准算法称为 **k-均值聚类 (k-means clustering)**。
    * 在 k-均值聚类中，会定义 $k$ 个“**簇质心 (cluster centroids)**”，记为 $z_1, \dots, z_k \in \mathbb{R}^m$（或 $\mathbb{R}^d$，取决于应用的数据集）。
    * 此外，还会定义一个**簇分配映射 (cluster assignment map)** $c : \{1, \dots, n\} \to \{1, \dots, k\}$。对于每个数据点的索引 $i$，$c(i)$ 的值表示该数据点被分配到的簇的索引（编号）。

* k-均值聚类的目标是**优化（最小化）** 以下目标函数 $F(z_1, \dots, z_k, c)$：
    $$ F(z_1, \dots, z_k, c) = \sum_{j=1}^k \sum_{i : c(i)=j} \|x_i - z_j\|_2^2 $$
    这个函数计算的是**每个数据点到其所属簇的质心之间的平方欧几里得距离的总和** (sum of squared distances)。优化的变量包括簇质心 $z_1, \dots, z_k$ 和簇分配 $c$ 本身！
    
* 这个优化问题通常通过 **劳埃德算法 (Lloyd's algorithm)** 来求解，这是一种迭代算法，它通过**交替优化 (alternating optimization)** 来更新簇质心和簇分配：
    1. 固定当前的簇分配 $c$，选择最优的簇质心 $z_1, \dots, z_k$ 来最小化目标函数 $F$。
    2. 固定当前的簇质心 $z_1, \dots, z_k$，选择最优的簇分配 $c$ 来最小化目标函数 $F$。
    
* 实际上，这两个步骤都有简单的**闭式解 (closed form)**：
    1.  **（更新质心）** 对于每个簇 $j = 1, \dots, k$，将质心 $z_j$ 设置为所有分配给该簇的数据点 $x_i$ 的**均值 (mean)**：
        $$ z_j \leftarrow \frac{\sum_{i : c(i)=j} x_i}{|\{i : c(i)=j\}|} $$
        其中 $|\{i : c(i)=j\}|$ 是分配给簇 $j$ 的数据点的数量。
    2.  **（更新分配）** 对于每个数据点 $i = 1, \dots, n$，将其分配给距离它**最近的质心**所对应的簇：
        $$ c(i) \leftarrow \underset{j=1,\dots,k}{\operatorname{argmin}} \|x_i - z_j\|_2^2 $$
* 通常，算法以**随机选择的初始簇质心**开始，但需要注意，k-均值算法**不保证收敛到全局最优解 (global optimum)**！
    * 事实上，算法经常会陷入**局部最优解 (local optimum)**，因此实践中常常使用**多次随机重启 (multiple random restarts)** 的策略（即多次使用不同的随机初始质心运行算法，选择最终目标函数值最小的结果）。
    * 但是，该算法保证目标函数 $F$ 的值在迭代过程中**永不增加**（非递增），因此算法最终会收敛（到某个局部最优解或稳定状态）。****
