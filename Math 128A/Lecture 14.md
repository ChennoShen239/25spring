# 回顾：高斯消元法的 LU 分解

对于 $s=1, \ldots, n-1$：
$$l_{js} = \frac{a_{js}}{a_{ss}}, \quad 1+s \le j \le n$$
$$a_{jk} \leftarrow a_{jk} - l_{js}a_{sk}, \quad 1+s \le j, k \le n$$

经过高斯消元（GE）后，矩阵 A 变成上三角矩阵：
$$A \xrightarrow{GE} U \stackrel{def}{=} \begin{pmatrix} u_{11} & u_{12} & \cdots & u_{1n} \\ & u_{22} & \cdots & u_{2n} \\ & & \ddots & \vdots \\ & & & u_{nn} \end{pmatrix}$$

LU 分解：$A = LU$，其中
$$L \stackrel{def}{=} \begin{pmatrix} 1 & & & \\ l_{21} & 1 & & \\ \vdots & \vdots & \ddots & \\ l_{n1} & l_{n2} & \cdots & 1 \end{pmatrix}$$

**例子：**
$$A = \begin{pmatrix} 1 & 1 & 0 & 3 \\ 2 & 1 & -1 & 1 \\ 3 & -1 & -1 & 2 \\ 1 & 4 & 3 & 5 \end{pmatrix} \in \mathcal{R}^{4 \times 4}$$
分解为：
$$L = \begin{pmatrix} 1 & & & \\ 2 & 1 & & \\ 3 & 4 & 1 & \\ 1 & -3 & 0 & 1 \end{pmatrix}, \quad U = \begin{pmatrix} 1 & 1 & 0 & 3 \\ & -1 & -1 & -5 \\ & & 3 & 13 \\ & & & -13 \end{pmatrix}$$

# 行交换与置换矩阵

**定义：** 置换矩阵 $P=(p_{ij})$ 是通过重排单位矩阵 $I_n$ 的行得到的矩阵。

**$3 \times 3$ 例子：**
$$P_{2,3} = \begin{pmatrix} 1 & 0 & 0 \\ 0 & 0 & 1 \\ 0 & 1 & 0 \end{pmatrix}, \quad A = \begin{pmatrix} a_{11} & a_{12} & a_{13} \\ a_{21} & a_{22} & a_{23} \\ a_{31} & a_{32} & a_{33} \end{pmatrix}$$
$P_{2,3} \cdot A$ 是将 A 的行进行交换：
$$P_{2,3} \cdot A = \begin{pmatrix} a_{11} & a_{12} & a_{13} \\ a_{31} & a_{32} & a_{33} \\ a_{21} & a_{22} & a_{23} \end{pmatrix}$$
例如，对于
$$A = \begin{pmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9 \end{pmatrix}$$
我们有
$$P_{2,3} \cdot A = \begin{pmatrix} 1 & 2 & 3 \\ 7 & 8 & 9 \\ 4 & 5 & 6 \end{pmatrix}$$

令 $P_{k,s}$ 为交换 $I_n$ 的第 k 行和第 s 行得到的置换矩阵。
对于任意 $A=(a_{ij}) \in \mathcal{R}^{n \times n}$，$P_{k,s} \cdot A$ 的结果是 A 的第 k 行和第 s 行互换。
令 P 为一个置换矩阵，则 $P \cdot P_{k,s}$ 也是一个置换矩阵。

# GEPP (带部分主元的高斯消元法) 作为 LU 分解

给定矩阵 A：
$$A = \begin{pmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ a_{21} & a_{22} & \cdots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{n1} & a_{n2} & \cdots & a_{nn} \end{pmatrix}$$
对于 $s=1, 2, \ldots, n-1$：
1.  **主元选择：** 选择绝对值最大的元素作为主元。
    $$piv_s \stackrel{def}{=} \text{argmax}_{s \le j \le n} |a_{js}|$$
    交换方程 $E_s \leftrightarrow E_{piv_s}$ (行交换)。
2.  **消元 $x_s$：** 从 $E_{s+1}$ 到 $E_n$ 消去 $x_s$。
    $$l_{js} = \frac{a_{js}}{a_{ss}}, \quad s+1 \le j \le n$$
    $$a_{jk} \leftarrow a_{jk} - l_{js}a_{sk}, \quad s+1 \le j, k \le n$$

**定理：GEPP**
对于一个非奇异矩阵 A，GEPP 计算出一个置换矩阵 P，一个单位下三角矩阵 L 和一个上三角矩阵 U，使得：
$$P \cdot A = L \cdot U$$

**例子：**
$$A = \begin{pmatrix} 0 & 0 & -1 & 1 \\ 1 & 1 & -1 & 2 \\ -1 & -1 & 2 & 0 \\ 1 & 2 & 0 & 2 \end{pmatrix} \in \mathcal{R}^{4 \times 4}$$
经过 GEPP 后，我们可能得到 (具体的 P, L, U 取决于主元选择的实现细节)：
$$P = \begin{pmatrix} 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 1 & 0 & 0 & 0 \\ 0 & 0 & 1 & 0 \end{pmatrix}, \quad L = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 1 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ -1 & 0 & -1 & 1 \end{pmatrix}, \quad U = \begin{pmatrix} 1 & 1 & -1 & 2 \\ 0 & 1 & 1 & 0 \\ 0 & 0 & -1 & 1 \\ 0 & 0 & 0 & 3 \end{pmatrix}$$

**证明 (归纳法概要)：**
* **n=2 基例：**
    $$A = \begin{pmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{pmatrix}$$
    主元选择：$piv_1 \stackrel{def}{=} \text{argmax}_{1 \le j \le 2} |a_{j1}|$，$P = I$ (如果 $piv_1=1$) 或 $P=P_{1,2}$ (如果 $piv_1=2$)。
    消元后，$P \cdot A = L \cdot U$ 成立。
* **n ≥ 3 归纳步骤：**
    假设对于 $(n-1) \times (n-1)$ 矩阵该定理成立。
    对于 n 阶矩阵 A，第一步主元选择得到 $P_1$，消元得到：
    $$P_1 A = \begin{pmatrix} 1 & \\ l & I_{n-1} \end{pmatrix} \begin{pmatrix} a'_{11} & a'_{1 \ldots n} \\ 0 & \hat{A} \end{pmatrix}$$
    其中 $\hat{A}$ 是一个 $(n-1) \times (n-1)$ 矩阵。根据归纳假设，存在 $\hat{P}$，$\hat{L}$，$\hat{U}$ 使得 $\hat{P}\hat{A} = \hat{L}\hat{U}$。
    整合后，令 $P = \begin{pmatrix} 1 & \\ & \hat{P} \end{pmatrix} P_1$，则
    $$P A = \begin{pmatrix} 1 & \\ \hat{P}l & \hat{L} \end{pmatrix} \begin{pmatrix} a'_{11} & a'_{1 \ldots n} \\ & \hat{U} \end{pmatrix} = LU$$
    即使 A 是奇异的，此过程（分解）仍然有效。

# 使用 GEPP 求解一般线性方程组

给定 $Ax=b$ 和 GEPP 分解 $P \cdot A = L \cdot U$。
1.  **变换右端项 b：**
    $P \cdot (Ax) = (P \cdot b) \implies (L \cdot U)x = (P \cdot b)$
2.  **通过前向和后向替换求解：**
    令 $y = Ux$，则 $Ly = Pb$。首先解出 $y$ (前向替换)，然后解 $Ux=y$ 得到 $x$ (后向替换)。
    $$x = (L \cdot U)^{-1}(P \cdot b) = U^{-1}(L^{-1}(P \cdot b))$$

**成本分析：**
* 计算 $P \cdot A = L \cdot U$：大约 $\frac{2}{3}n^3$ 次运算。
* 前向和后向替换：大约 $2n^2$ 次运算。
* 最重要的是高效地计算 $P \cdot A = L \cdot U$。

# §6.6 严格对角占优 (SDD) 矩阵

**定义：** 矩阵 $A=(a_{ij}) \in \mathcal{R}^{n \times n}$ 是严格对角占优 (Strictly Diagonally Dominant, SDD) 的，如果对于每一行 $i=1, 2, \ldots, n$：
$$|a_{ii}| > \sum_{j=1, j \ne i}^{n} |a_{ij}|$$

**例 I：** 矩阵 $A = \begin{pmatrix} 7 & 2 & 0 \\ 3 & 5 & -1 \\ 0 & 5 & -6 \end{pmatrix}$ 是 SDD。
$|7| > |2| + |0|$
$|5| > |3| + |-1|$
$|-6| > |0| + |5|$

**例 II：** 矩阵 $B = \begin{pmatrix} 7 & 5 & 0 \\ 3 & 5 & -1 \\ 0 & -3 & 3 \end{pmatrix}$ 不是 SDD。
因为对于第三行：$|3| \not> |0| + |-3|$ (即 $3 \not> 3$)。

## SDD 矩阵的高斯消元：无需主元选择即可成功

令 $A=(a_{ij}) \in \mathcal{R}^{n \times n}$ 为 SDD。则 $|a_{11}| > \sum_{j=1, j \ne 1}^{n} |a_{1j}| \ge 0$，因此 $a_{11} \ne 0$。
进行一步消元：
$$A = \begin{pmatrix} 1 & & \\ l_{21} & 1 & \\ \vdots & & \ddots \\ l_{n1} & & & 1 \end{pmatrix} \begin{pmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ 0 & \hat{a}_{22} & \cdots & \hat{a}_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ 0 & \hat{a}_{n2} & \cdots & \hat{a}_{nn} \end{pmatrix}$$
其中 $l_{j1} = \frac{a_{j1}}{a_{11}}$，$\hat{a}_{jk} = a_{jk} - \frac{a_{j1}}{a_{11}}a_{1k}$ 对于 $2 \le j, k \le n$。
只需证明子矩阵 $\hat{A} \stackrel{def}{=} (\hat{a}_{ij})_{i,j=2}^n$ 仍然是 SDD。

对于 $i=2, \ldots, n$：
$$\sum_{j=2, j \ne i}^{n} |\hat{a}_{ij}| = \sum_{j=2, j \ne i}^{n} |a_{ij} - \frac{a_{i1}}{a_{11}}a_{1j}| \le \sum_{j=2, j \ne i}^{n} |a_{ij}| + \left|\frac{a_{i1}}{a_{11}}\right| \sum_{j=2, j \ne i}^{n} |a_{1j}|$$
使用原始矩阵 A 的 SDD 条件：
$\sum_{j=2, j \ne i}^{n} |a_{ij}| < |a_{ii}| - |a_{i1}|$
$\sum_{j=2, j \ne i}^{n} |a_{1j}| < |a_{11}| - |a_{1i}|$ (如果 $i \ne 1$)
代入后可证明：
$$\sum_{j=2, j \ne i}^{n} |\hat{a}_{ij}| < |a_{ii}| - \left|\frac{a_{i1}}{a_{11}}\right||a_{1i}| \le \left|a_{ii} - \frac{a_{i1}}{a_{11}}a_{1i}\right| = |\hat{a}_{ii}|$$
因此 $\hat{A}$ 也是 SDD。

**例子：**
$$A = \begin{pmatrix} 7 & 2 & 0 \\ 3 & 5 & -1 \\ 0 & 5 & -6 \end{pmatrix}$$
第一步消元：
$$A = \begin{pmatrix} 1 & & \\ \frac{3}{7} & 1 & \\ 0 & & 1 \end{pmatrix} \begin{pmatrix} 7 & 2 & 0 \\ 0 & \frac{29}{7} & -1 \\ 0 & 5 & -6 \end{pmatrix}$$
子矩阵 $\begin{pmatrix} \frac{29}{7} & -1 \\ 5 & -6 \end{pmatrix}$ 也是 SDD ($|\frac{29}{7}| > |-1|$, $|-6| > |5|$)。
继续分解：
$$A = \begin{pmatrix} 1 & & \\ \frac{3}{7} & 1 & \\ 0 & \frac{35}{29} & 1 \end{pmatrix} \begin{pmatrix} 7 & 2 & 0 \\ 0 & \frac{29}{7} & -1 \\ 0 & 0 & -\frac{139}{29} \end{pmatrix}$$

# 对称正定 (SPD) 矩阵

**定义：** 矩阵 $A=(a_{ij}) \in \mathcal{R}^{n \times n}$ 是对称正定 (Symmetric Positive Definite, SPD) 的，如果：
1.  $A = A^T$ (对称性)
2.  对于任意非零向量 $x \in \mathcal{R}^n$，$x^T A x > 0$ (正定性)

**例 I：** 矩阵 $\hat{A} = \begin{pmatrix} 0 & -1 & 0 \\ -1 & 2 & -1 \\ 0 & -1 & 2 \end{pmatrix} = \hat{A}^T$ 不是 SPD。
因为，令 $x = \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix}$，则 $x^T \hat{A} x = 0$，不满足正定性。

**例 II：** 矩阵 $A = \begin{pmatrix} 2 & -1 & 0 \\ -1 & 2 & -1 \\ 0 & -1 & 2 \end{pmatrix} = A^T$ 是 SPD。
证明：令 $x = \begin{pmatrix} x_1 \\ x_2 \\ x_3 \end{pmatrix} \ne 0$。
$$x^T A x = \begin{pmatrix} x_1 & x_2 & x_3 \end{pmatrix} \begin{pmatrix} 2 & -1 & 0 \\ -1 & 2 & -1 \\ 0 & -1 & 2 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \\ x_3 \end{pmatrix}$$
$$= \begin{pmatrix} x_1 & x_2 & x_3 \end{pmatrix} \begin{pmatrix} 2x_1 - x_2 \\ -x_1 + 2x_2 - x_3 \\ -x_2 + 2x_3 \end{pmatrix} = 2x_1^2 - 2x_1x_2 + 2x_2^2 - 2x_2x_3 + 2x_3^2$$
整理得：
$$x^T A x = x_1^2 + (x_1^2 - 2x_1x_2 + x_2^2) + (x_2^2 - 2x_2x_3 + x_3^2) + x_3^2$$
$$= x_1^2 + (x_1 - x_2)^2 + (x_2 - x_3)^2 + x_3^2 > 0 \quad (\text{因为 } x \ne 0)$$

## SPD 矩阵的高斯消元：更快且无需主元选择

令 $A=(a_{ij}) \in \mathcal{R}^{n \times n}$ 为 SPD。
则 $A^T = A$，所以 $a_{jk} = a_{kj}$。
$a_{11} = \begin{pmatrix} 1 & 0 & \cdots & 0 \end{pmatrix} A \begin{pmatrix} 1 \\ 0 \\ \vdots \\ 0 \end{pmatrix} > 0$。
因此 $a_{11} \ne 0$，无需主元选择。
第一步高斯消元：
$$A = \begin{pmatrix} 1 & & \\ l_1 & I \end{pmatrix} \begin{pmatrix} a_{11} & a_{11}l_1^T \\ 0 & \hat{A} \end{pmatrix}$$
其中 $l_1 = \begin{pmatrix} l_{21} \\ \vdots \\ l_{n1} \end{pmatrix}$，$l_{j1} = \frac{a_{j1}}{a_{11}}$。$\hat{A}$ 是消元后的 $(n-1) \times (n-1)$ 子矩阵。
由于 A 的对称性，可以写成：
$$A = \begin{pmatrix} 1 & \\ l_1 & I \end{pmatrix} \begin{pmatrix} a_{11} & \\ & \hat{A} \end{pmatrix} \begin{pmatrix} 1 & l_1^T \\ & I \end{pmatrix}$$
下一步：证明 $\hat{A}$ 仍然是 SPD。
已知 $\hat{A}^T = \hat{A}$ (对称性保持)。
令 $\hat{x} \in \mathcal{R}^{n-1}$ 为任意非零向量。我们需要证明 $\hat{x}^T \hat{A} \hat{x} > 0$。
构造 $x = \begin{pmatrix} -l_1^T \hat{x} \\ \hat{x} \end{pmatrix} \in \mathcal{R}^n$。如果 $\hat{x} \ne 0$，则 $x \ne 0$。
可以证明：
$$\hat{x}^T \hat{A} \hat{x} = x^T A x > 0$$
因此 $\hat{A}$ 是 SPD。

## SPD 矩阵的 Cholesky 分解：$A = LDL^T$

**Cholesky for n=2：**
$$A = \begin{pmatrix} a_{11} & a_{21} \\ a_{21} & a_{22} \end{pmatrix} = \begin{pmatrix} 1 & \\ l_{21} & 1 \end{pmatrix} \begin{pmatrix} a_{11} & \\ & \hat{a}_{22} \end{pmatrix} \begin{pmatrix} 1 & l_{21} \\ & 1 \end{pmatrix}$$
其中 $l_{21} = \frac{a_{21}}{a_{11}}$，$\hat{a}_{22} = a_{22} - l_{21}a_{12} = a_{22} - \frac{a_{21}^2}{a_{11}}$。
这可以写成 $A = LDL^T$，其中 $D = \begin{pmatrix} a_{11} & \\ & \hat{a}_{22} \end{pmatrix}$。

**Cholesky for n ≥ 3 (归纳法)：**
$$A = \begin{pmatrix} a_{11} & a_{11}l_1^T \\ a_{11}l_1 & A_{22} \end{pmatrix} = \begin{pmatrix} 1 & \\ l_1 & I \end{pmatrix} \begin{pmatrix} a_{11} & \\ & \hat{A} \end{pmatrix} \begin{pmatrix} 1 & l_1^T \\ & I \end{pmatrix}$$
其中 $\hat{A} = A_{22} - a_{11}l_1 l_1^T$。
归纳假设：$\hat{A} = \hat{L}\hat{D}\hat{L}^T$。
则：
$$A = \begin{pmatrix} 1 & \\ l_1 & I \end{pmatrix} \begin{pmatrix} a_{11} & \\ & \hat{L}\hat{D}\hat{L}^T \end{pmatrix} \begin{pmatrix} 1 & l_1^T \\ & I \end{pmatrix}$$
$$= \begin{pmatrix} 1 & \\ l_1 & \hat{L} \end{pmatrix} \begin{pmatrix} a_{11} & \\ & \hat{D} \end{pmatrix} \begin{pmatrix} 1 & l_1^T \\ & \hat{L}^T \end{pmatrix} \stackrel{def}{=} L D L^T$$

**例子：**
$$A = \begin{pmatrix} 4 & -1 & 1 \\ -1 & 4.25 & 2.75 \\ 1 & 2.75 & 3.5 \end{pmatrix}$$
分解为 $A = LDL^T$：
$$L = \begin{pmatrix} 1 & & \\ -1/4 & 1 & \\ 1/4 & 3/4 & 1 \end{pmatrix}, \quad D = \begin{pmatrix} 4 & & \\ & 4 & \\ & & 1 \end{pmatrix}$$

## Cholesky 分解是特殊的 LU 分解

$A = LDL^T = LU$，其中 $U = DL^T$。
只需要计算 L 和 D，节省了因子分解中大约一半的工作量。
**总成本：** 大约 $\frac{1}{3}n^3$ 次运算。

**“但是 Cholesky 分解不应该有 D...”**
我们可以将 D 分解为 $(D^{1/2})^2$：
$$D = \begin{pmatrix} d_1 & & \\ & \ddots & \\ & & d_n \end{pmatrix} = (D^{1/2})^2, \quad \text{其中 } D^{1/2} \stackrel{def}{=} \begin{pmatrix} \sqrt{d_1} & & \\ & \ddots & \\ & & \sqrt{d_n} \end{pmatrix}$$
则 $$A = L D^{1/2} D^{1/2} L^T = (L D^{1/2}) (L D^{1/2})^T = \tilde{L} \tilde{L}^T$$
其中 $\tilde{L} = L D^{1/2}$ 是一个下三角矩阵 (但不一定是单位下三角)。

**例子（续）：**
$$\tilde{L} = \begin{pmatrix} 1 & & \\ -1/4 & 1 & \\ 1/4 & 3/4 & 1 \end{pmatrix} \begin{pmatrix} 2 & & \\ & 2 & \\ & & 1 \end{pmatrix} = \begin{pmatrix} 2 & & \\ -1/2 & 2 & \\ 1/2 & 3/2 & 1 \end{pmatrix}$$
所以 $$A = \begin{pmatrix} 2 & & \\ -1/2 & 2 & \\ 1/2 & 3/2 & 1 \end{pmatrix} \begin{pmatrix} 2 & -1/2 & 1/2 \\ & 2 & 3/2 \\ & & 1 \end{pmatrix}$$

# 回顾：自然样条曲线方程的矩阵形式

样条系数 $\{c_j\}_{j=1}^{n-1}$ 的方程：
$$A \cdot \begin{pmatrix} c_1 \\ c_2 \\ \vdots \\ c_{n-2} \\ c_{n-1} \end{pmatrix} = \text{rhs}$$
其中
$$A \stackrel{def}{=} \begin{pmatrix} 2(h_0+h_1) & h_1 & & & \\ h_1 & 2(h_1+h_2) & h_2 & & \\ & \ddots & \ddots & \ddots & \\ & & h_{n-3} & 2(h_{n-3}+h_{n-2}) & h_{n-2} \\ & & & h_{n-2} & 2(h_{n-2}+h_{n-1}) \end{pmatrix}$$
矩阵 A 是 SDD，SPD 和三对角的。

**定义：** $A \in \mathcal{R}^{n \times n}$ 是三对角的，如果 $a_{ij}=0$ 当 $|i-j|>1$。
$$A = \begin{pmatrix} a_{11} & a_{12} & & & \\ a_{21} & a_{22} & a_{23} & & \\ & \ddots & \ddots & \ddots & \\ & & a_{n-1,n-2} & a_{n-1,n-1} & a_{n-1,n} \\ & & & a_{n,n-1} & a_{n,n} \end{pmatrix}$$
由于 A 中有许多零元素，LU 分解应该大大简化。

# 三对角矩阵的 LU 分解 (假设 $a_{jj} \ne 0$)

$$A = \begin{pmatrix} a_{11} & a_{12} & & \\ a_{21} & a_{22} & a_{23} & \\ & \ddots & \ddots & \ddots \\ & & a_{n,n-1} & a_{n,n} \end{pmatrix}$$
第一步消元：令 $l_{21} = \frac{a_{21}}{a_{11}}$ 并且 $a_{22} \leftarrow a_{22} - l_{21}a_{12}$。
$$A = \begin{pmatrix} 1 & & & \\ l_{21} & 1 & & \\ & & \ddots & \\ & & & 1 \end{pmatrix} \begin{pmatrix} a_{11} & a_{12} & & \\ 0 & a'_{22} & a_{23} & \\ & a_{32} & a_{33} & \ddots \\ & & \ddots & \end{pmatrix}$$
消元过程仅计算 $l_{21}$ 和新的 $a_{22}$ (3 次运算)。剩余矩阵仍然是三对角的。
递归地对所有剩余子矩阵进行操作，得到：
$$A = \begin{pmatrix} 1 & & & \\ l_{21} & 1 & & \\ & l_{32} & 1 & \\ & & \ddots & \\ & & & l_{n,n-1} & 1 \end{pmatrix} \begin{pmatrix} u_{11} & u_{12} & & \\ & u_{22} & u_{23} & \\ & & \ddots & \ddots \\ & & & u_{n,n} \end{pmatrix}$$
其中 $u_{jj}$ 是消元过程中更新的对角元素。
对于 $j=1, \ldots, n-1$：
$l_{j+1,j} = \frac{a_{j+1,j}}{a_{jj}}$ (这里 $a_{jj}$ 是更新后的值)
$a_{j+1,j+1} \leftarrow a_{j+1,j+1} - l_{j+1,j}a_{j,j+1}$
总共：大约 $3n$ 次运算 (如果所有 $a_{jj} \ne 0$)。

# (非奇异) 三对角矩阵带部分主元的 LU 分解

* **情况 1：$|a_{11}| \ge |a_{21}|$ (无需交换)**
    令 $l_{21} = \frac{a_{21}}{a_{11}}$ 且 $a_{22} \leftarrow a_{22} - l_{21}a_{12}$。
    $$A = \begin{pmatrix} 1 & & \\ l_{21} & 1 & \\ & & \ddots \end{pmatrix} \begin{pmatrix} a_{11} & a_{12} & \\ 0 & a'_{22} & a_{23} \\ & & \ddots \end{pmatrix}$$
    消元仅计算 $l_{21}$ 和 $a'_{22}$。剩余矩阵是三对角的。
* **情况 2：$|a_{21}| > |a_{11}|$ (需要交换)**
    交换第1行和第2行 ($P_{1,2}A$)。
    令 $l'_{21} = \frac{a_{11}}{a_{21}}$ (使用交换后的元素，这里 $a_{11}$ 是原 $a_{21}$，$a_{21}$ 是原 $a_{11}$)。
    更新第二行的元素：$(a'_{22}, a'_{23}) = (a_{12} - l'_{21}a_{22}, -l'_{21}a_{23})$ (使用交换后的元素)。
    $$P_{1,2}A = \begin{pmatrix} 1 & & \\ l'_{21} & 1 & \\ & & \ddots \end{pmatrix} \begin{pmatrix} \text{new } a_{11} & \text{new } a_{12} & \text{new } a_{13} \\ 0 & a'_{22} & a'_{23} \\ & & \ddots \end{pmatrix}$$
    消元计算 $l'_{21}$，$a'_{22}$ 和 $a'_{23}$ (约 4 次运算)。剩余矩阵是三对角的。

**总结与递归：**
第一步（可能带主元选择）后：
$$P_1 A = L_1 U_1'$$
其中 $L_1$ 是简单的下三角矩阵， $U_1'$ 的第一行已确定，其右下角的子矩阵 $A'$ 仍然是（或经过变换后是）三对角（或带宽有限）。
递归地：$\hat{P}A' = \hat{L}\hat{U}$。
$\hat{U}$ 是上三角矩阵，带宽最多为 3 (因为行交换可能引入元素到 $u_{i,i+2}$)。
$\hat{L}$ 是单位下三角矩阵，每列对角线下方最多只有一个非零元素。
最终：
$$P A = L U$$
总成本：最多 $4n$ 次运算和 $n$ 次比较。
$U$ 的带宽可能从2增加到3，因为行交换可能会将 $a_{i+1,i+2}$ 这样的元素移到 $a_{i,i+2}$ 的位置。 L 仍然保持每列只有一个非零的 $l_{ij}$。