# §6.2 带部分主元的高斯消去法 (Gaussian Elimination with partial pivoting)

## 定义与初始设置

给定线性方程组 $Ax = b$，其中：

$$A=\begin{pmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ a_{21} & a_{22} & \cdots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{n1} & a_{n2} & \cdots & a_{nn} \end{pmatrix}, \quad b=\begin{pmatrix} b_{1} \\ b_{2} \\ \vdots \\ b_{n} \end{pmatrix}, \quad x=\begin{pmatrix} x_{1} \\ x_{2} \\ \vdots \\ x_{n} \end{pmatrix}$$

* 方程 $E_j$ 对应于矩阵 A 的第 j 行。
* 变量 $x_1$ 对应于矩阵 A 的第一列 $\begin{pmatrix} a_{11} \\ a_{21} \\ \vdots \\ a_{n1} \end{pmatrix}$。

**主元选择 (Pivoting):** 选择绝对值最大的元素作为主元。

$$piv \stackrel{def}{=} \text{argmax}_{1 \le j \le n} |a_{j1}|$$
即
$$|a_{piv,1}| = \max_{1 \le j \le n} |a_{j1}|$$

交换方程 $E_1$ 和 $E_{piv}$ (记作 $E_1 \leftrightarrow E_{piv}$)。

## 消元过程

### 步骤 1: 消去 $x_1$

从方程 $E_2$ 到 $E_n$ 中消去 $x_1$：

$$(E_j - \frac{a_{j1}}{a_{11}}E_1) \rightarrow (E_j) \quad \text{，其中 } 2 \le j \le n$$

* 由于进行了主元选择，我们有 $|\frac{a_{j1}}{a_{11}}| \le 1$，$2 \le j \le n$。
* 新的A矩阵的第j行变为：
    $$(\begin{matrix} 0 & a_{j2} - \frac{a_{j1}}{a_{11}}a_{12} & \cdots & a_{jn} - \frac{a_{j1}}{a_{11}}a_{1n} \end{matrix}) \quad ，2 \le j \le n$$
* 新的b向量的第j个分量变为：
    $$b_j - \frac{a_{j1}}{a_{11}}b_1$$

覆盖更新后的A矩阵和b向量：

新的
$$A = \begin{pmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ 0 & a_{22} & \cdots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ 0 & a_{n2} & \cdots & a_{nn} \end{pmatrix}$$
其中
$$a_{jk} = a_{jk} - \frac{a_{j1}}{a_{11}}a_{1k} \quad ，2 \le j \le n, 2 \le k \le n$$

新的
$$b = \begin{pmatrix} b_{1} \\ b_{2} \\ \vdots \\ b_{n} \end{pmatrix}$$
其中
$$b_j = b_j - \frac{a_{j1}}{a_{11}}b_1 \quad ，2 \le j \le n$$

### 后续步骤: 对 $E_s$ ($s=2, \ldots, n-1$) 重复操作

对子问题重复相同的过程：

$$A=\begin{pmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ 0 & a_{22} & \cdots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ 0 & a_{n2} & \cdots & a_{nn} \end{pmatrix}, \quad b=\begin{pmatrix} b_{1} \\ b_{2} \\ \vdots \\ b_{n} \end{pmatrix}$$

**主元选择:** 对于当前的第 $s$ 列，选择绝对值最大的元素。

$$piv = \text{argmax}_{s \le j \le n} |a_{js}|$$
即
$$|a_{piv,s}| = \max_{s \le j \le n} |a_{js}|$$

交换方程 $E_s$ 和 $E_{piv}$ ($E_s \leftrightarrow E_{piv}$)。

**消元:** 从 $E_{s+1}$ 到 $E_n$ 中消去 $x_s$。

$$(E_j - \frac{a_{js}}{a_{ss}}E_s) \rightarrow (E_j) \quad ，s+1 \le j \le n$$

更新系数：
$$a_{jk} = a_{jk} - \frac{a_{js}}{a_{ss}}a_{sk} \quad ，s+1 \le j \le n, s+1 \le k \le n$$
$$b_j = b_j - \frac{a_{js}}{a_{ss}}b_s \quad ，s+1 \le j \le n$$

## 带部分主元的高斯消去法总结

对于 $s = 1, 2, \ldots, n-1$：

1.  **主元选择:**
    $$piv = \text{argmax}_{s \le j \le n} |a_{js}|$$
    交换 $E_s \leftrightarrow E_{piv}$。
2.  **消元:** 从 $E_{s+1}$ 到 $E_n$ 消去 $x_s$：
    $$a_{jk} = a_{jk} - \frac{a_{js}}{a_{ss}}a_{sk} \quad \text{(覆盖 } a_{jk} \text{)}，s+1 \le j \le n, s+1 \le k \le n$$
    $$b_j = b_j - \frac{a_{js}}{a_{ss}}b_s \quad \text{(覆盖 } b_j \text{)}，s+1 \le j \le n$$

## 高斯消元后的方程与回代法

经过高斯消元后，矩阵 A 变为上三角矩阵：

$$A=\begin{pmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ 0 & a_{22} & \cdots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & a_{nn} \end{pmatrix}, \quad b=\begin{pmatrix} b_{1} \\ b_{2} \\ \vdots \\ b_{n} \end{pmatrix}$$

**回代法 (Backward Substitution):**

对于 $s = n, n-1, \ldots, 1$：
$$x_s = \frac{b_s - \sum_{k=s+1}^{n} a_{sk}x_k}{a_{ss}}$$

MATLAB 命令： `x = A\b`

## 高斯消元法成本分析

对于 $s=1, 2, \ldots, n-1$：

* **主元选择:** $(n-s+1)$ 次比较。
    总比较次数: $$\sum_{s=1}^{n-1}(n-s+1) = \frac{n(n+1)}{2} - 1$$
* **消元 $x_s$:**
    * 计算比率 $\{\frac{a_{js}}{a_{ss}}\}$ 的总成本: $$\sum_{s=1}^{n-1}(n-s) = \frac{n(n-1)}{2} \quad \text{次除法}$$
    * 计算 $\{a_{jk}\}$ 的总成本: $$\sum_{s=1}^{n-1}2(n-s)^2 = \frac{n(n-1)(2n-1)}{3} \quad \text{次乘法和减法}$$
    * 计算 $\{b_j\}$ 的总成本: $$\sum_{s=1}^{n-1}2(n-s) = n(n-1) \quad \text{次乘法和减法}$$

**总计 ($n^3$ 项):** 约为 $\frac{2}{3}n^3$ 次加法和乘法。

*不计算整数运算和内存成本。*

## §6.3 矩阵代数 (Matrix Algebra)

### 定义：矩阵的线性组合

设 $A = (a_{ij}) \in \mathcal{R}^{n \times m}$，$B = (b_{ij}) \in \mathcal{R}^{n \times m}$，则
$C = \alpha A + \beta B \in \mathcal{R}^{n \times m}$ 定义为：
$$C = \begin{pmatrix} \alpha a_{11} + \beta b_{11} & \alpha a_{12} + \beta b_{12} & \cdots & \alpha a_{1m} + \beta b_{1m} \\ \alpha a_{21} + \beta b_{21} & \alpha a_{22} + \beta b_{22} & \cdots & \alpha a_{2m} + \beta b_{2m} \\ \vdots & \vdots & \ddots & \vdots \\ \alpha a_{n1} + \beta b_{n1} & \alpha a_{n2} + \beta b_{n2} & \cdots & \alpha a_{nm} + \beta b_{nm} \end{pmatrix}$$

**例子:**
设 $A = \begin{pmatrix} 2 & -1 & 7 \\ 3 & 1 & 0 \end{pmatrix}$, $B = \begin{pmatrix} 4 & 2 & -8 \\ 0 & 1 & 6 \end{pmatrix} \in \mathcal{R}^{2 \times 3}$，则
$$C \stackrel{def}{=} A - 2B = \begin{pmatrix} -6 & -5 & 23 \\ 3 & -1 & -12 \end{pmatrix} \in \mathcal{R}^{2 \times 3}$$

### 矩阵向量乘积，线性方程组和点积

线性方程组：
$$a_{11}x_1 + a_{12}x_2 + \cdots + a_{1n}x_n = b_1$$
$$a_{21}x_1 + a_{22}x_2 + \cdots + a_{2n}x_n = b_2$$
$$\vdots$$
$$a_{n1}x_1 + a_{n2}x_2 + \cdots + a_{nn}x_n = b_n$$

可以表示为 $Ax = b$，其中
$$A=\begin{pmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ a_{21} & a_{22} & \cdots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{n1} & a_{n2} & \cdots & a_{nn} \end{pmatrix}, \quad x=\begin{pmatrix} x_{1} \\ x_{2} \\ \vdots \\ x_{n} \end{pmatrix}, \quad b=\begin{pmatrix} b_{1} \\ b_{2} \\ \vdots \\ b_{n} \end{pmatrix}$$

矩阵向量乘积 $Ax$ 定义为：
$$Ax \stackrel{def}{=} \begin{pmatrix} a_{11}x_1 + a_{12}x_2 + \cdots + a_{1n}x_n \\ a_{21}x_1 + a_{22}x_2 + \cdots + a_{2n}x_n \\ \vdots \\ a_{n1}x_1 + a_{n2}x_2 + \cdots + a_{nn}x_n \end{pmatrix}$$
对于任何 $A \in \mathcal{R}^{n \times m}, x \in \mathcal{R}^{m}$。
$Ax$ 中的每个分量 $(Ax)_j$ 是 A 的第 j 行与向量 x 的点积：
$$(Ax)_j = (a_{j1}x_1 + a_{j2}x_2 + \cdots + a_{jm}x_m) = \begin{pmatrix} a_{j1} & a_{j2} & \cdots & a_{jm} \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \\ \vdots \\ x_m \end{pmatrix}$$

**例子:**
$$A = \begin{pmatrix} 3 & 2 \\ -1 & 1 \\ 6 & 4 \end{pmatrix}, \quad u = \begin{pmatrix} 3 \\ -1 \end{pmatrix}$$
$$Au = \begin{pmatrix} 3 & 2 \\ -1 & 1 \\ 6 & 4 \end{pmatrix} \begin{pmatrix} 3 \\ -1 \end{pmatrix} = \begin{pmatrix} 7 \\ -4 \\ 14 \end{pmatrix}$$

### 矩阵-矩阵乘积

设 $A = (a_{ij}) \in \mathcal{R}^{n \times m}$，$B = (b_{ij}) \in \mathcal{R}^{m \times p}$。

**列划分 (Column partition):**
$B = \begin{pmatrix} b_1 & b_2 & \cdots & b_p \end{pmatrix}$，其中 $b_j \stackrel{def}{=} \begin{pmatrix} b_{1j} \\ b_{2j} \\ \vdots \\ b_{mj} \end{pmatrix} \in \mathcal{R}^m$，$j=1, \ldots, p$。

**定义:**
$$AB = A \begin{pmatrix} b_1 & b_2 & \cdots & b_p \end{pmatrix} \stackrel{def}{=} \begin{pmatrix} Ab_1 & Ab_2 & \cdots & Ab_p \end{pmatrix} \in \mathcal{R}^{n \times p}$$

**元素公式 (Entry-wise formula):**
$$(AB)_{jk} = (Ab_k)_j = \begin{pmatrix} a_{j1} & a_{j2} & \cdots & a_{jm} \end{pmatrix} b_k = \sum_{i=1}^{m} a_{ji}b_{ik}$$

**例子:**
设 $A = \begin{pmatrix} 3 & 2 \\ -1 & 1 \\ 1 & 4 \end{pmatrix} \in \mathcal{R}^{3 \times 2}$, $B = \begin{pmatrix} 2 & 1 & -1 \\ 3 & 1 & 2 \end{pmatrix} \in \mathcal{R}^{2 \times 3}$。
$$C = AB = \begin{pmatrix} 12 & 5 & 1 \\ 1 & 0 & 3 \\ 14 & 5 & 7 \end{pmatrix} \in \mathcal{R}^{3 \times 3}$$

**定理：矩阵乘法的结合律**
设 $A \in \mathcal{R}^{n \times m}$，$B \in \mathcal{R}^{m \times p}$，$C \in \mathcal{R}^{p \times k}$。则 $A(BC) = (AB)C$。
证明：
$$(A(BC))_{st} = \sum_{i=1}^{m} a_{si}(BC)_{it} = \sum_{i=1}^{m} a_{si} (\sum_{j=1}^{p} b_{ij}c_{jt})$$
$$= \sum_{j=1}^{p} (\sum_{i=1}^{m} a_{si}b_{ij}) c_{jt} = \sum_{j=1}^{p} (AB)_{sj}c_{jt} = ((AB)C)_{st}$$

## 特殊矩阵和MATLAB命令

| 矩阵类型                            | 定义                                                                                                                                           | MATLAB 命令 |
| ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| 方阵 (Square matrix)              | $A \in \mathcal{R}^{n \times n}$                                                                                                             |           |
| 对角矩阵 (Diagonal matrix)          | $$D = \begin{pmatrix} d_1 & & \\ & d_2 & \\ & & \ddots \\ & & & d_n \end{pmatrix}$$                                                          | `diag(D)` |
| 单位矩阵 (Identity matrix)          | $$I = \begin{pmatrix} 1 & & \\ & 1 & \\ & & \ddots \\ & & & 1 \end{pmatrix}$$                                                                | `eye(n)`  |
| 上三角矩阵 (Upper-triangular matrix) | $$U = \begin{pmatrix} u_{11} & u_{12} & \cdots & u_{1n} \\ & u_{22} & \cdots & u_{2n} \\ & & \ddots & \vdots \\ & & & u_{nn} \end{pmatrix}$$ | `triu(A)` |
| 下三角矩阵 (Lower-triangular matrix) | $$L = \begin{pmatrix} l_{11} & & \\ l_{21} & l_{22} & \\ \vdots & \vdots & \ddots \\ l_{n1} & l_{n2} & \cdots & l_{nn} \end{pmatrix}$$       | `tril(A)` |

## 逆矩阵 (Inverse Matrices)

如果一个方阵 $A \in \mathcal{R}^{n \times n}$ 存在一个矩阵 $B \in \mathcal{R}^{n \times n}$ 使得 $AB = BA = I$，则称 A 是**非奇异的 (non-singular)**。
矩阵 B 称为 A 的**逆矩阵 (inverse)**，记作 $A^{-1}$。
没有逆矩阵的方阵称为**奇异的 (singular)**。

**例子:**
$$A = \begin{pmatrix} 2 & -1 \\ 1 & 2 \end{pmatrix}, \quad A^{-1} = \frac{1}{5}\begin{pmatrix} 2 & 1 \\ -1 & 2 \end{pmatrix} \quad \text{，A 是非奇异的。}$$
$$C = \begin{pmatrix} 2 & -1 \\ 0 & 0 \end{pmatrix} \quad \text{，C 是奇异的。}$$

### 使用逆矩阵求解 $Ax=b$

如果 $A^{-1}$ 已知，则 $$x = Ix = (A^{-1}A)x = A^{-1}(Ax) = A^{-1}b$$

**例子:**
$$A = \begin{pmatrix} 1 & 2 & -1 \\ 2 & 1 & 0 \\ -1 & 1 & 2 \end{pmatrix}, \quad A^{-1} = \frac{1}{9}\begin{pmatrix} -2 & 5 & -1 \\ 4 & -1 & 2 \\ -3 & 3 & 3 \end{pmatrix}$$
对于 $b \in \mathcal{R}^3$，解为 $$x = \frac{1}{9}\begin{pmatrix} -2 & 5 & -1 \\ 4 & -1 & 2 \\ -3 & 3 & 3 \end{pmatrix} b$$

**注意:** $A^{-1}$ 很少直接获得，计算 $A^{-1}$ 通常比直接求解 x 更困难。

### 关于 $A^{-1}$ 的事实

假设 $A^{-1}$ 存在：
1.  $A^{-1}$ 是唯一的。
2.  $(A^{-1})^{-1} = A$。
3.  如果 $B^{-1}$ 也存在 (A, $B \in \mathcal{R}^{n \times n}$)，则 $(AB)^{-1} = B^{-1}A^{-1}$。

### 计算 $A^{-1}$

计算 $A^{-1}$ 等价于求解矩阵方程 $AX=I$，其中 $X \in \mathcal{R}^{n \times n}$。
将 X 和 I 按列划分： $X = \begin{pmatrix} x_1 & x_2 & \cdots & x_n \end{pmatrix}$，$I = \begin{pmatrix} e_1 & e_2 & \cdots & e_n \end{pmatrix}$ (其中 $e_j$ 是第j个标准单位向量)。
则 $AX=I \leftrightarrow A\begin{pmatrix} x_1 & x_2 & \cdots & x_n \end{pmatrix} = \begin{pmatrix} e_1 & e_2 & \cdots & e_n \end{pmatrix} \leftrightarrow Ax_j = e_j$，对于 $j=1, \ldots, n$。
因此，计算 $A^{-1}$ 就是求解 n 个具有相同系数矩阵 A 的线性方程组。

## 回顾: GEPP 求解 $Ax=b$

**消元阶段:**
对于 $s=1, 2, \ldots, n-1$:
1.  **主元选择:** 选取绝对值最大的元素 $piv = \text{argmax}_{s \le j \le n} |a_{js}|$，$E_s \leftrightarrow E_{piv}$。
2.  **消元 $x_s$:**
    $$a_{jk} = a_{jk} - \frac{a_{js}}{a_{ss}}a_{sk} \quad \text{(覆盖 } a_{jk} \text{)}，s+1 \le j, k \le n \quad (1)$$
    $$b_j = b_j - \frac{a_{js}}{a_{ss}}b_s \quad \text{(覆盖 } b_j \text{)}，s+1 \le j \le n \quad (2)$$

**回代阶段:**
对于 $s=n, n-1, \ldots, 1$:
$$x_s = \frac{b_s - \sum_{k=s+1}^{n} a_{sk}x_k}{a_{ss}} \quad (3)$$

当 b 变成一个矩阵 B 时，只有方程 (2) 和 (3) 发生变化。

## GEPP 求解 $AX=B$

其中 $$B = \begin{pmatrix} b_{11} & b_{12} & \cdots & b_{1n} \\ b_{21} & b_{22} & \cdots & b_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ b_{n1} & b_{n2} & \cdots & b_{nn} \end{pmatrix}$$

**消元阶段:**
对于 $s=1, 2, \ldots, n-1$:
1.  **主元选择:** $piv = \text{argmax}_{s \le j \le n} |a_{js}|$，$E_s \leftrightarrow E_{piv}$。
2.  **消元 $x_s$:**
    $$a_{jk} = a_{jk} - \frac{a_{js}}{a_{ss}}a_{sk} \quad \text{(覆盖 } a_{jk} \text{)}，s+1 \le j, k \le n \quad (1)$$
    $$b_{jk} = b_{jk} - \frac{a_{js}}{a_{ss}}b_{sk} \quad \text{(覆盖 } b_{jk} \text{)}，s+1 \le j, k \le n \quad (2)$$

**成本分析:**
* 方程 (1) 的成本: $$\sum_{s=1}^{n-1} 2(n-s)^2 \approx \frac{2}{3}n^3$$
* 方程 (2) 的成本: $$\sum_{s=1}^{n-1} 2(n-s)^2 \approx \frac{2}{3}n^3$$

**回代阶段:**
对于 $s=n, n-1, \ldots, 1$:
$$x_{sj} = \frac{b_{sj} - \sum_{k=s+1}^{n} a_{sk}x_{kj}}{a_{ss}} \quad ，j=1, \ldots, n \quad (3)$$
* 方程 (3) 的成本: $$\sum_{s,j=1}^{n} 2(n-s) \approx n^3$$

**总成本 (方程 (1) + (2) + (3)):** $$\approx \frac{2}{3}n^3 + \frac{2}{3}n^3 + n^3 = \frac{7}{3}n^3$$

## 矩阵转置 (Matrix Transpose): $A^T$

如果 $A = (a_{ij}) \in \mathcal{R}^{m \times n}$，则其转置 $A^T = (a_{ji}) \in \mathcal{R}^{n \times m}$。
$$A = \begin{pmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ a_{21} & a_{22} & \cdots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{m1} & a_{m2} & \cdots & a_{mn} \end{pmatrix} \implies A^T \stackrel{def}{=} \begin{pmatrix} a_{11} & a_{21} & \cdots & a_{m1} \\ a_{12} & a_{22} & \cdots & a_{m2} \\ \vdots & \vdots & \ddots & \vdots \\ a_{1n} & a_{2n} & \cdots & a_{mn} \end{pmatrix}$$

**例子:**
$$A = \begin{pmatrix} 2 & 4 & 7 & 1 \\ 2 & -9 & -1 & 2 \end{pmatrix} \in \mathcal{R}^{2 \times 4}, \quad A^T = \begin{pmatrix} 2 & 2 \\ 4 & -9 \\ 7 & -1 \\ 1 & 2 \end{pmatrix} \in \mathcal{R}^{4 \times 2}$$

**定理:**
1.  $(A^T)^T = A$
2.  $(AB)^T = B^T A^T$
3.  如果 $A^{-1}$ 存在，则 $(A^{-1})^T = (A^T)^{-1}$

## 行列式 (Determinant) for $A \in \mathcal{R}^{n \times n}$

$$\det(A) = \begin{vmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ a_{21} & a_{22} & \cdots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{n1} & a_{n2} & \cdots & a_{nn} \end{vmatrix}$$
行列式可以沿任何行或列展开。例如，沿第一列展开：
$$\det(A) = a_{11} C_{11} - a_{21} C_{21} + \cdots + (-1)^{n+1}a_{n1}C_{n1}$$
其中 $C_{ij}$ 是相应的余子式。

### 行列式的性质

* $\det(A^T) = \det(A)$
* 如果 $A^{-1}$ 存在，则 $\det(A^{-1}) = (\det(A))^{-1}$
* 如果 $B \in \mathcal{R}^{n \times n}$，则 $\det(AB) = \det(A)\det(B)$
* $\det(A) \ne 0 \iff Ax=b$ 有唯一解。

**GEPP 可用于计算 $\det(A)$:**
* 如果 $A_e$ 是通过初等行变换 $(E_i) \leftrightarrow (E_j)$ ($i \ne j$) 从 A 得到的，则 $\det(A_e) = -\det(A)$ (行交换改变行列式的符号)。
* 如果 $A_e$ 是通过初等行变换 $(E_i + \lambda E_j) \rightarrow (E_i)$ ($i \ne j$) 从 A 得到的，则 $\det(A_e) = \det(A)$ (消元操作不改变行列式的值)。
* 如果 A 是上三角矩阵，则 $$\det(A) = \prod_{j=1}^{n} a_{jj}$$

### 使用 GEPP 计算 $\det(A)$

1.  **主元选择:** 选择绝对值最大的元素 $$piv \stackrel{def}{=} \text{argmax}_{1 \le j \le n} |a_{j1}|$$，即 $$|a_{piv,1}| = \max_{1 \le j \le n} |a_{j1}|$$
2.  交换行 $E_1$ 和 $E_{piv}$ ($E_1 \leftrightarrow E_{piv}$)。如果 $piv \ne 1$，则 $\det(A)$ 变号。
3.  **消元:** 从 $E_2$ 到 $E_n$ 消去 $x_1$: $$(E_j - \frac{a_{j1}}{a_{11}}E_1) \rightarrow (E_j) \quad ，2 \le j \le n$$ $\det(A)$ 不变。
4.  重复以上过程，直到 A 变为上三角矩阵 $$U = \begin{pmatrix} u_{11} & u_{12} & \cdots & u_{1n} \\ 0 & u_{22} & \cdots & u_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & u_{nn} \end{pmatrix}$$
5.  原始矩阵 A 的行列式为：$$(-1)^{\text{\# of row swaps}} \prod_{j=1}^{n} u_{jj}$$

## §6.5 一般线性方程组 (General linear equations)

$$E_1: a_{11}x_1 + a_{12}x_2 + \cdots + a_{1n}x_n = b_1$$
$$E_2: a_{21}x_1 + a_{22}x_2 + \cdots + a_{2n}x_n = b_2$$
$$\vdots$$
$$E_n: a_{n1}x_1 + a_{n2}x_2 + \cdots + a_{nn}x_n = b_n$$

$$A \stackrel{def}{=} \begin{pmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ a_{21} & a_{22} & \cdots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{n1} & a_{n2} & \cdots & a_{nn} \end{pmatrix}, \quad b \stackrel{def}{=} \begin{pmatrix} b_1 \\ b_2 \\ \vdots \\ b_n \end{pmatrix}, \quad x \stackrel{def}{=} \begin{pmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \end{pmatrix}$$

* 方程 $E_j$ 对应于 A 的第 j 行: $(a_{j1}, a_{j2}, \ldots, a_{jn})$，$1 \le j \le n$。
* 变量 $x_k$ 对应于 A 的第 k 列: $$\begin{pmatrix} a_{1k} \\ a_{2k} \\ \vdots \\ a_{nk} \end{pmatrix} \quad ，1 \le k \le n$$
* 关注消元过程以提高算法效率。

### 矩阵代数中的事实 (用于 §6.5-6.6)

对于分块矩阵的乘法，公式同样适用：
设 $$A = \begin{pmatrix} A_{11} & A_{12} \\ A_{21} & A_{22} \end{pmatrix}, \quad B = \begin{pmatrix} B_{11} & B_{12} \\ B_{21} & B_{22} \end{pmatrix}$$，则
$$A \cdot B = \begin{pmatrix} A_{11}B_{11} + A_{12}B_{21} & A_{11}B_{12} + A_{12}B_{22} \\ A_{21}B_{11} + A_{22}B_{21} & A_{21}B_{12} + A_{22}B_{22} \end{pmatrix}$$

特别地，对于 $$A = \begin{pmatrix} A_{11} & 0 \\ A_{21} & I \end{pmatrix}, \quad B = \begin{pmatrix} B_{11} & B_{12} \\ 0 & L \cdot U \end{pmatrix}$$:
$$A \cdot B = \begin{pmatrix} A_{11}B_{11} & A_{11}B_{12} \\ A_{21}B_{11} & A_{21}B_{12} + L \cdot U \end{pmatrix} = \begin{pmatrix} A_{11} & 0 \\ A_{21} & L \end{pmatrix} \cdot \begin{pmatrix} B_{11} & B_{12} \\ 0 & U \end{pmatrix}$$

### 高斯消元的 LU 分解视角 (假设 $a_{11} \ne 0$)

第一步消元：
$$l_{j1} \stackrel{def}{=} \frac{a_{j1}}{a_{11}}, \quad (E_j - l_{j1}E_1) \rightarrow (E_j), \quad 2 \le j \le n$$
新的 $a_{jk} = a_{jk} - l_{j1}a_{1k}$，对于 $j,k = 2, \ldots, n$。
这可以表示为矩阵乘积：
$$A = \begin{pmatrix} 1 & & & \\ l_{21} & 1 & & \\ \vdots & & \ddots & \\ l_{n1} & & & 1 \end{pmatrix} \begin{pmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ 0 & a'_{22} & \cdots & a'_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ 0 & a'_{n2} & \cdots & a'_{nn} \end{pmatrix}$$ (此处 $a'_{jk}$ 表示更新后的值)

第二步消元 (假设 $a'_{22} \ne 0$) 作用于子矩阵：
$$\begin{pmatrix} a'_{22} & \cdots & a'_{2n} \\ \vdots & \ddots & \vdots \\ a'_{n2} & \cdots & a'_{nn} \end{pmatrix} = \begin{pmatrix} 1 & & \\ l'_{32} & 1 & \\ \vdots & & \ddots \\ l'_{n2} & & & 1 \end{pmatrix} \begin{pmatrix} a'_{22} & a'_{23} & \cdots & a'_{2n} \\ 0 & a''_{33} & \cdots & a''_{3n} \\ \vdots & \vdots & \ddots & \vdots \\ 0 & a''_{n3} & \cdots & a''_{nn} \end{pmatrix}$$

重复这个过程，可以得到 $A = LU$ 分解：
$$A = \begin{pmatrix} 1 & & & \\ l_{21} & 1 & & \\ l_{31} & l_{32} & 1 & \\ \vdots & \vdots & & \ddots \\ l_{n1} & l_{n2} & \cdots & l_{n,n-1} & 1 \end{pmatrix} \begin{pmatrix} u_{11} & u_{12} & \cdots & u_{1n} \\ & u_{22} & \cdots & u_{2n} \\ & & \ddots & \vdots \\ & & & u_{nn} \end{pmatrix}$$

**高斯消元即 LU 分解:**
对于 $s = 1, \ldots, n-1$:
$$l_{js} = \frac{a_{js}}{a_{ss}}, \quad s+1 \le j \le n$$
$$a_{jk} = a_{jk} - l_{js}a_{sk} \quad \text{(覆盖 } a_{jk} \text{)}，s+1 \le j, k \le n$$

GE后，A 变为上三角矩阵 U。
$$U = \begin{pmatrix} u_{11} & u_{12} & \cdots & u_{1n} \\ & u_{22} & \cdots & u_{2n} \\ & & \ddots & \vdots \\ & & & u_{nn} \end{pmatrix}$$
L 是单位下三角矩阵，其元素为消元过程中的乘数 $l_{js}$。
$$L = \begin{pmatrix} 1 & & & \\ l_{21} & 1 & & \\ \vdots & \vdots & \ddots & \\ l_{n1} & l_{n2} & \cdots & 1 \end{pmatrix}$$

**例子:**
$$A = \begin{pmatrix} 1 & 1 & 0 & 3 \\ 2 & 1 & -1 & 1 \\ 3 & -1 & -1 & 2 \\ 1 & 4 & 3 & 5 \end{pmatrix} \in \mathcal{R}^{4 \times 4}$$
可以分解为
$$L = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 2 & 1 & 0 & 0 \\ 3 & 4 & 1 & 0 \\ 1 & -3 & 0 & 1 \end{pmatrix}, \quad U = \begin{pmatrix} 1 & 1 & 0 & 3 \\ 0 & -1 & -1 & -5 \\ 0 & 0 & 3 & 13 \\ 0 & 0 & 0 & -13 \end{pmatrix}$$

## 行交换与置换矩阵 (Permutation Matrix)

**定义:** 置换矩阵 P 是通过重排单位矩阵 $I_n$ 的行得到的矩阵。
**$3 \times 3$ 例子:**
$$P_{2,3} = \begin{pmatrix} 1 & 0 & 0 \\ 0 & 0 & 1 \\ 0 & 1 & 0 \end{pmatrix} \quad \text{(交换 } I_3 \text{ 的第2行和第3行)}$$
如果 $$A = \begin{pmatrix} a_{11} & a_{12} & a_{13} \\ a_{21} & a_{22} & a_{23} \\ a_{31} & a_{32} & a_{33} \end{pmatrix}$$, 则 $$P_{2,3}A = \begin{pmatrix} a_{11} & a_{12} & a_{13} \\ a_{31} & a_{32} & a_{33} \\ a_{21} & a_{22} & a_{23} \end{pmatrix} \quad \text{(A的第2行和第3行交换)}$$

设 $P_{k,s}$ 是交换 $I_n$ 的第 k 行和第 s 行得到的置换矩阵。对于任何 $A \in \mathcal{R}^{n \times n}$，$P_{k,s}A$ 的结果是 A 的第 k 行和第 s 行互换。
如果 P 是一个置换矩阵，则 $P \cdot P_{k,s}$ 也是一个置换矩阵。

## GEPP 作为 LU 分解 (带行交换)

回顾 GEPP 过程：
对于 $s = 1, 2, \ldots, n-1$:
1.  **主元选择:** $$piv_s \stackrel{def}{=} \text{argmax}_{s \le j \le n} |a_{js}| \quad ，E_s \leftrightarrow E_{piv_s} \quad \text{(行交换，对应一个置换矩阵)}$$
2.  **消元:** $$l_{js} = \frac{a_{js}}{a_{ss}}, \quad s+1 \le j \le n$$ $$a_{jk} = a_{jk} - l_{js}a_{sk}, \quad s+1 \le j, k \le n$$

**定理:** 设 $A = (a_{ij}) \in \mathcal{R}^{n \times n}$ 是非奇异的。则 GEPP 计算出一个 LU 分解，使得存在一个置换矩阵 P，满足：
$$PA = LU$$

**例子:**
$$A = \begin{pmatrix} 0 & 0 & -1 & 1 \\ 1 & 1 & -1 & 2 \\ -1 & -1 & 2 & 0 \\ 1 & 2 & 0 & 2 \end{pmatrix}$$
经过一系列的行交换 (由P表示) 和消元步骤，可以得到：
$$P = \begin{pmatrix} 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 1 & 0 & 0 & 0 \\ 0 & 0 & 1 & 0 \end{pmatrix}, \quad L = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 1 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ -1 & 0 & -1 & 1 \end{pmatrix}, \quad U = \begin{pmatrix} 1 & 1 & -1 & 2 \\ 0 & 1 & 1 & 0 \\ 0 & 0 & -1 & 1 \\ 0 & 0 & 0 & 3 \end{pmatrix}$$
使得 $PA = LU$。

**$PA = LU$ 证明 (归纳法):**
* **n=2 基例:**
    $$A = \begin{pmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{pmatrix}$$
    主元选择：$piv_1 = \text{argmax}_{1 \le j \le 2} |a_{j1}|$，$P = I$ (如果 $piv_1=1$) 或 $P=P_{1,2}$ (如果 $piv_1=2$)。
    消元后，$PA=LU$ 成立。
* **n ≥ 3 归纳步骤:**
    主元选择：$piv_1 = \text{argmax}_{1 \le j \le n} |a_{j1}|$，$P_1$ (初始置换)。
    消元：$$P_1 A = \begin{pmatrix} 1 & 0 \\ l & I_{n-1} \end{pmatrix} \begin{pmatrix} a'_{11} & a'_{12 \ldots 1n} \\ 0 & A' \end{pmatrix}$$，其中 $A'$ 是 $(n-1) \times (n-1)$ 矩阵。
    归纳假设：对于 $A'$，存在 $P_b A' = L_b U_b$。
    组合起来：
    $$\begin{pmatrix} 1 & 0 \\ 0 & P_b \end{pmatrix} P_1 A = \begin{pmatrix} 1 & 0 \\ 0 & P_b \end{pmatrix} \begin{pmatrix} 1 & 0 \\ l & I_{n-1} \end{pmatrix} \begin{pmatrix} a'_{11} & a'_{12 \ldots 1n} \\ 0 & A' \end{pmatrix}$$
    $$= \begin{pmatrix} 1 & 0 \\ P_b l & I_{n-1} \end{pmatrix} \begin{pmatrix} a'_{11} & a'_{12 \ldots 1n} \\ 0 & P_b A' \end{pmatrix}$$ (这里 $P_b l$ 表示 $P_b$ 作用于 $l$ 的相应行)
    $$= \begin{pmatrix} 1 & 0 \\ P_b l & L_b \end{pmatrix} \begin{pmatrix} a'_{11} & a'_{12 \ldots 1n} \\ 0 & U_b \end{pmatrix}$$
    令 $$P = \begin{pmatrix} 1 & 0 \\ 0 & P_b \end{pmatrix} P_1$$，则 $PA = LU$。

**如果A是奇异的?** GEPP 仍然可以进行，但U中会出现零主元 (除非在选择主元时所有可选元素都为零)。

## 使用 GEPP 求解一般线性方程组

已知 $Ax=b$ 和 $PA=LU$。
1.  **变换 b:** $$P(Ax) = Pb \implies (LU)x = Pb$$
2.  **求解:** $$x = (LU)^{-1}(Pb) = U^{-1}L^{-1}(Pb)$$
    这分两步：
    * 解 $Ly = Pb$ (前向替换)
    * 解 $Ux = y$ (后向替换)

**成本分析:**
* 计算 $PA=LU$: 约 $\frac{2}{3}n^3$ 次运算。
* 前向和后向替换: 约 $2n^2$ 次运算。
* 最重要的是高效计算 $PA=LU$。