# 多项式插值与逼近

M. Lindsey

## 目录

1.  拉格朗日插值
    1.1 构造与唯一性
    1.2 误差界限
2.  切比雪夫多项式
3.  正交多项式与高斯求积
    3.1 正交多项式
    3.2 三项递推关系
    3.3 正交多项式的零点
    3.4 高斯求积

# 1. 拉格朗日插值

令 $t_0 < \ldots < t_m \in \mathbb{R}$ (不必均匀间隔)，并令 $y_0, \ldots, y_m \in \mathbb{R}$。我们的目标是找到一个多项式 $P(t)$ 使得对于 $i=0, \ldots, m$，有 $P(t_i) = y_i$。 [cite: 3] 通常，我们需要考虑一个至少为 m 阶的多项式才能一般地做到这一点，事实上，存在一个唯一的 m 阶插值多项式，有时称为拉格朗日（插值）多项式。 [cite: 4]

通常我们设想的场景是，存在一个“真实”函数 g，使得对所有的 i 都有 $g(t_i) = y_i$，我们希望插值数据点 $(t_i, y_i)$（$i=0, \ldots, m$）的多项式 P 是对 g 的一个良好逼近。 [cite: 5]

一般而言，拉格朗日插值是一件极其危险的事情，因为即使数据集的大小 m 增加，真实函数 g 和插值 P 之间也可能存在显著差异，这是由龙格现象（Runge's phenomenon）造成的。 [cite: 6] 然而，如果 g 足够光滑，插值点数 m 固定，并且区间 $[t_0, t_m]$ 缩小，那么实际上 P 会以点态 $O(|t_m - t_0|^{m+1})$ 的误差逼近 g，而与插值点 $t_i$ 的选择无关。 [cite: 7] 首先我们讨论如何构造 P，然后我们给出这个误差界的证明。如果 $t_i$ 被选为区间 $[t_0, t_m]$ 上的切比雪夫节点，则可以避免这种病态情况。 [cite: 8] 但总的来说，例如对于等距网格，需要小心。 [cite: 9]

## 1.1 构造与唯一性

考虑从属于插值点选择 $t = (t_0, \ldots, t_m)$ 的拉格朗日基多项式：
$$l_j(t; t) := \prod_{i \in \{0, \ldots, m\} \setminus \{j\}} \frac{t - t_i}{t_j - t_i}, \quad j=0, \ldots, m.$$
由于插值点将是固定的，我们将省略对 t 的依赖。 [cite: 10] 注意到 $l_j$ 是一个 m 阶多项式，并且观察到：
$$l_j(t_i) = \delta_{ij}$$
其中 $\delta_{ij}$ 是克罗内克 δ 函数。 [cite: 11, 12] 因此，如果我们简单地通过以下方式定义拉格朗日插值多项式 $l: \mathbb{R} \rightarrow \mathbb{R}$：
$$l = \sum_{j=0}^{m} y_j l_j,$$
那么根据构造，$l(t_i) = \sum_{j=0}^{m} y_j \delta_{ij} = y_i$，从而达到了所需的插值性质。 [cite: 12]

注意，δ 性质 (1.2) 意味着 $l_j$ 作为函数是线性无关的，因此构成了 m 阶多项式空间的一个基。 [cite: 13] (事实上，假设 $\sum_{j=0}^{m} c_j l_j \equiv 0$ 是零多项式。那么特别地，将 $t_i$ 代入两边，我们得到对所有 $i=0, \ldots, m$ 都有 $c_i=0$。这保证了线性无关性。) [cite: 14]

事实上，基的性质意味着 $l$ 是唯一的 m 阶多项式插值，即唯一的 m 阶多项式 P 使得对所有 $i=0, \ldots, m$ 都有 $P(t_i) = y_i$。确实，任何这样的 P 都可以根据 $l_j$ 的基性质写成 $P = \sum_{j=0}^{m} z_j l_j$，其中 $z_j \in \mathbb{R}$。 [cite: 14] 然后将 $t_i$ 代入两边，我们看到 $P(t_i) = z_i$，但根据插值性质 $P(t_i) = y_i$，所以实际上 $P = \sum_{j=0}^{m} y_j l_j = l$。这就如所声称的那样建立了唯一性。 [cite: 15]

**定理 1.** 给定不同的插值点 $t_0, \ldots, t_m \in \mathbb{R}$，如 (1.1) 中定义的拉格朗日基多项式 $l_j(\cdot; t)$ 构成了 m 阶多项式空间的一个基。 [cite: 16] 此外，给定 $y_0, \ldots, y_m \in \mathbb{R}$，拉格朗日插值多项式
$$l(t) := \sum_{j=0}^{m} y_j l_j(t; t)$$
是**唯一**的 m 阶多项式，使得对于 $i=0, \ldots, m$ 有 $l(t_i) = y_i$。 [cite: 17]

## 1.2 误差界限

接下来我们建立对我们有用的逼近性质。

**定理 2.** 假设 $g \in C^{m+1}([a,b])$，并且令 $t_0, \ldots, t_m \in [a,b]$ 是不同的插值点。 [cite: 19] 令 $y_i = g(t_i)$ 对于 $i=0, \ldots, m$，并令 l 表示数据 $(t_i, y_i)$（$i=0, \ldots, m$）的拉格朗日插值多项式，如定理 1 的陈述。那么对于每个 $t \in [a,b]$，存在 $\xi = \xi(t) \in [a,b]$ 使得：
$$g(t) - l(t) = \frac{g^{(m+1)}(\xi)}{(m+1)!} \prod_{i=0}^{m} (t - t_i).$$

**证明：** 定义余项 $R := g - l$。 [cite: 21] 我们知道 R 在 $t_0, \ldots, t_m$ 处有零点，我们想将其与具有相同零点的 $(m+1)$ 次多项式 P 进行“比较”，即：
$$P(t) := \prod_{i=0}^{m} (t - t_i).$$
R 和 P 都在 $t_i$ 处有零点，因此它们的任何线性组合也如此。 [cite: 22] 但对于任意固定的 $t \in [a,b] \setminus \{t_0, \ldots, t_m\}$，我们可以找到 R 和 P 的一个线性组合，使得它在 t 处有额外的零点，即函数：
$$h_t(s) := R(s) - \frac{R(t)}{P(t)}P(s).$$
那么 $h_t(s)$ 在 $[a,b]$ 上至少有 $m+2$ 个零点，因此根据罗尔定理，$h_t'(s)$ 在此区间上有 $m+1$ 个零点，通过重复应用罗尔定理，我们看到 $h_t^{(m+1)}(s)$ 在 $[a,b]$ 上有一个零点，我们称之为 $\xi = \xi(t)$。 [cite: 23] 那么根据构造：
$$0 = h_t^{(m+1)}(\xi) = g^{(m+1)}(\xi) - \frac{R(t)}{P(t)}(m+1)!,$$
最后一个等式是因为 $P^{(m+1)} \equiv (m+1)!$（因为 P 是一个首项系数为1的 $m+1$ 次多项式）并且 $l^{(m+1)} \equiv 0$（因为 l 是一个 m 次多项式）。 [cite: 24] 解出余项，我们得到：
$$R(t) = \frac{g^{(m+1)}(\xi)}{(m+1)!}P(t),$$
证毕。 [cite: 25] (注意，对于 $t \in \{t_0, \ldots, t_m\}$，该定理显然成立。) [cite: 26]

前面的定理立即暗示了拉格朗日插值多项式的所需 $O(|t_m - t_0|^{m+1})$ 逼近性质。我们转而证明这个界的精确表述。

**推论 3.** 假设 $g \in C^{m+1}([a,b])$，并令 $a = t_0 < \ldots < t_m = b$ 是不同的插值点。令 $y_i = g(t_i)$ 对于 $i=0, \ldots, m$，并令 l 表示数据 $(t_i, y_i)$（$i=0, \ldots, m$）的拉格朗日插值多项式，如定理 1 的陈述。进一步定义
$$\Delta := \max_{i=0, \ldots, m-1} |t_{i+1} - t_i|$$
为相邻插值点之间的最大距离，并令 $||| \cdot |||$ 表示在 $[a,b]$ 上的均匀范数 $|||h||| := \sup_{t \in [a,b]} |h(t)|$。那么
$$|||g - l||| \le \frac{|||g^{(m+1)}|||}{4(m+1)} \Delta^{m+1}.$$
**证明：** 令 $t \in [a,b]$。根据前面的定理，我们知道存在 $\xi \in [a,b]$ 使得： [cite: 26]
$$g(t) - l(t) = \frac{g^{(m+1)}(\xi)}{(m+1)!} \prod_{i=0}^{m} (t - t_i).$$
那么我们只需要证明： [cite: 28]
$$\prod_{i=0}^{m} |t - t_i| \le \frac{m!}{4} \Delta^{m+1}.$$
注意，对于任何 $t \in [a,b] \setminus \{t_0, \ldots, t_m\}$，存在 j 使得 $t \in [t_j, t_{j+1}]$。 [cite: 28] 这些值 $t_j, t_{j+1}$ 是 $t_i$ 中距离给定 t 最近的点。 [cite: 29] 下一个最近的值必须在 $2\Delta$ 的距离内，再下一个最近的值在 $3\Delta$ 的距离内，依此类推，最远的值在 $m\Delta$ 的距离内。 [cite: 30] 此外，乘积 $(t-t_j)(t_{j+1}-t)$ 在 $[t_j, t_{j+1}]$ 的中点 $(t_j+t_{j+1})/2$ 处最大化，因此其界为 $\Delta^2/4$。因此所有距离的乘积的界为：
$$\prod_{i=0}^{m} |t - t_i| \le (\Delta^2/4)(2\Delta)(3\Delta)\cdots(m\Delta) = \frac{m!}{4}\Delta^{m+1},$$
证毕。 [cite: 31]

# 2. 切比雪夫多项式

切比雪夫多项式由于其在区间 $[-1, 1]$上的等波振荡性质，在数值分析中是一个非常有用的工具，该性质可以通过适当的平移和缩放转移到任意区间。 [cite: 31]
第 n 阶切比雪夫多项式对于 $t \in [-1, 1]$ 定义为：
$$T_n(t) = \cos(n \cos^{-1}(t)).$$
从定义上看，$T_n$ 实际上是一个多项式并非立即显而易见！ [cite: 32] 然而，这个事实由三项递推关系保证：
$$T_{n+1}(t) = 2tT_n(t) - T_{n-1}(t),$$
以及明显的恒等式 $T_0 \equiv 1$ 和 $T_1(t) = t$。 [cite: 33]

要证明 (2.1)，我们使用经典的三角恒等式：
$$\cos(a+b) = \cos(a)\cos(b) - \sin(a)\sin(b).$$
将 b 替换为 -b 并将两个恒等式相加得到另一个恒等式：
$$\cos(a+b) + \cos(a-b) = 2\cos(a)\cos(b),$$
或者
$$\cos(a+b) = 2\cos(a)\cos(b) - \cos(a-b).$$
然后我们可以计算：
$$T_{n+1}(t) = \cos(n\cos^{-1}(t) + \cos^{-1}(t))$$
$$= 2\cos(n\cos^{-1}(t))\cos(\cos^{-1}(t)) - \cos((n-1)\cos^{-1}(t))$$
$$= 2tT_n(t) - T_{n-1}(t),$$
从而验证了 (2.1)。 [cite: 33]
对我们来说，术语“切比雪夫多项式”将始终指“第一类切比雪夫多项式”，除非另有说明。 [cite: 34]

注意到 $T_n$ 的零点（称为切比雪夫节点）因此是：
$$\cos\left(\frac{2j-1}{2n}\pi\right), \quad j=1, \ldots, n,$$
并且，
$$|T_n(t)| \le 1, \quad t \in [-1, 1].$$
此外，$T_n$ 的局部极值点，在
$$\cos\left(\frac{j\pi}{n}\right), \quad j=1, \ldots, n-1$$
处达到，均为 $\pm 1$（区间端点 -1 和 1 处的值也是如此）。 [cite: 35] 这就是等波振荡性质。 [cite: 36]

那么我们有定理 1 的以下推论，它阐明了在拉格朗日插值中使用切比雪夫节点（而不是等距点）作为插值点的优势。 [cite: 36]

**定理 4.** 假设 $g \in C^{m+1}([-1,1])$。令 $t_0, \ldots, t_m$ 为 $m+1$ 阶切比雪夫多项式的零点，即：
$$t_i = \cos\left(\frac{2i+1}{2m+2}\pi\right), \quad i=0, \ldots, m.$$
令 $x_i = g(t_i)$。 [cite: 37] 那么如定理 1 中的拉格朗日插值多项式 l 满足：
$$|||g - l||| \le 2^{-m} \frac{|||g^{(m+1)}|||}{(m+1)!},$$
其中 $||| \cdot |||$ 表示区间 $[-1,1]$ 上的均匀范数。 [cite: 38]

**证明：** 注意到多项式 $P(t) = \prod_{i=0}^{m} (t - t_i)$ 必定与 $T_{m+1}$ 的一个标量倍数一致（根据代数基本定理）。 [cite: 39] 三项递推关系 (2.1) 表明，对于所有 $n \ge 1$，$T_n$ 的 n 次项是 $2^{n-1}t^n$。 [cite: 40] 因此：
$$\prod_{i=0}^{m} (t - t_i) = \frac{1}{2^m} T_{m+1}(t).$$
但是 $|T_{m+1}(t)| \le 1$ 在 $[-1,1]$ 上，所以结果由定理 2 得出。 [cite: 40]

下一个推论通过平移和缩放插值区间简单得出。

**定理 5.** 假设 $g \in C^{m+1}(I)$，其中 $I := [c-r, c+r]$，$c \in \mathbb{R}$ 且 $r > 0$。定义插值点：
$$t_i = c + r \cos\left(\frac{2i+1}{2m+2}\pi\right), \quad i=0, \ldots, m$$
并令 $x_i = g(t_i)$。那么如定理 1 中的拉格朗日插值多项式 l 满足：
$$|||g - l||| \le \frac{r^{m+1}}{2^m} \frac{|||g^{(m+1)}|||}{(m+1)!},$$
其中 $||| \cdot |||$ 表示区间 I 上的均匀范数。 [cite: 41]

# 3. 正交多项式与高斯求积

给定一个区间 $[a,b]$（可能 $a = -\infty, b = +\infty$）和一个权函数 $w: [a,b] \rightarrow [0, \infty)$，高斯求积关注的是估计以下形式的积分：
$$\int_a^b g(t)w(t)dt$$
使用以下形式的求积法则：
$$\sum_{i=1}^m b_i g(t_i).$$
我们将要求一个积分法则，当 g 是多项式时，它能精确到我们能达到的任意阶数。 [cite: 42] 注意，如果区间是无限或半无限的，我们必须要求权函数 $w(t)$ 具有足够的衰减性。 [cite: 43] 例如，对于区间 $(-\infty, \infty)$ 选择 $w(t) = e^{-t^2/2}$ 将导出所谓的高斯-埃尔米特求积。 [cite: 44] 同时，高斯-勒让德求积由在区间 $[-1,1]$ 上选择 $w \equiv 1$ 导出，高斯-切比雪夫求积由在区间 $[-1,1]$ 上选择 $w(t) = \frac{1}{\sqrt{1-t^2}}$ 导出。 [cite: 45]

## 3.1 正交多项式

高斯求积与正交多项式理论密切相关。 [cite: 46] 对于给定的区间和权函数，正交多项式被定义为一个多项式序列 $p_k$，其阶数递增 $k=0, 1, 2, \ldots$（通常通过它们是首项系数为1的约束唯一确定），这些多项式关于加权内积是正交的：
$$\langle g, h \rangle = \int_a^b g(t)h(t)w(t)dt.$$
在我们的讨论中，我们将固定我们的正交多项式序列为唯一的首项系数为1的正交多项式序列。 [cite: 47] 原则上，$p_k = p_k(t)$ 可以通过对单项式序列 $1, t, t^2, t^3, \ldots$ 应用格拉姆-施密特过程来构造，即通过以下方式递归构造它们：
$$p_k(t) = t^k - \sum_{l=0}^{k-1} \frac{\langle t^k, p_l \rangle}{\langle p_l, p_l \rangle} p_l(t).$$
根据构造，很明显 $p_k$ 是首项系数为1的正交多项式。 [cite: 48] 此外，注意到作为阶数递增的首项系数为1的多项式，$p_0, \ldots, p_k$ 构成了 k 次多项式集合 $\mathbb{P}_k$ 的一个基，对于任何 k。 [cite: 49]

## 3.2 三项递推关系

正交多项式序列的一个重要特征（我们实际上并不真正需要）是三项递推关系，它总是允许稳定地计算正交多项式。 [cite: 50] 三项递推关系的推导来自于注意到 $tp_k(t)$ 是一个 $k+1$ 阶多项式，因此可以在正交基 $p_0, \ldots, p_{k+1}$ 中展开。 [cite: 51] 因此我们可以写：
$$tp_k(t) = \sum_{l=0}^{k+1} \frac{\langle tp_k, p_l \rangle}{\langle p_l, p_l \rangle} p_l(t).$$
[cite: 52]然而，有趣的是，许多这些项都消失了，我们可以计算：
$$\langle tp_k, p_l \rangle = \int_a^b p_k(t) [tp_l(t)] w(t)dt.$$
当 $l < k-1$ 时，$p_k$ 与 $\mathbb{P}_{l+1}$ 的一个基正交，因此与所有 $\mathbb{P}_{l+1}$ 中的多项式正交，这些项就消失了，得到：
$$\frac{\langle tp_k, p_{k+1} \rangle}{\langle p_{k+1}, p_{k+1} \rangle} p_{k+1}(t) = \left(t - \frac{\langle tp_k, p_k \rangle}{\langle p_k, p_k \rangle}\right)p_k(t) - \frac{\langle tp_k, p_{k-1} \rangle}{\langle p_{k-1}, p_{k-1} \rangle}p_{k-1}(t),$$
经过适当的项整理后。 [cite: 53] 注意到 $tp_k - p_{k+1} \in \mathbb{P}_k$，因此利用正交性：
$$\langle tp_k, p_{k+1} \rangle = \langle p_{k+1} + (tp_k - p_{k+1}), p_{k+1} \rangle = \langle p_{k+1}, p_{k+1} \rangle,$$
类似地 $\langle tp_k, p_{k-1} \rangle = \langle t p_{k-1}, p_k \rangle = \langle p_k, p_k \rangle + \langle (tp_{k-1}-p_k), p_k \rangle = \langle p_k, p_k \rangle$，进而我们有：
$$p_{k+1}(t) = \left(t - \frac{\langle tp_k, p_k \rangle}{\langle p_k, p_k \rangle}\right)p_k(t) - \frac{\langle p_k, p_k \rangle}{\langle p_{k-1}, p_{k-1} \rangle}p_{k-1}(t),$$
或者
$$p_{k+1}(t) = (t - \alpha_k)p_k(t) - \beta_k p_{k-1}(t),$$
其中
$$\alpha_k := \frac{\langle tp_k, p_k \rangle}{\langle p_k, p_k \rangle}, \quad \beta_k := \frac{\langle p_k, p_k \rangle}{\langle p_{k-1}, p_{k-1} \rangle} > 0.$$
这是经典的三项递推关系，事实上，任何由序列 $\alpha_k \in \mathbb{R}$ 和 $\beta_k > 0$ （原文为 $\beta_k \ge 0$，但对于首项系数为1的正交多项式通常 $\beta_k > 0$）指定的三项递推关系都对应于一个权函数，并且在某种意义上，$\mathbb{R}$ 上的测度等价于这样的序列。 [cite: 54] (这是法瓦尔定理的内容。) [cite: 55]

## 3.3 正交多项式的零点

在上一小节中，我们基本上证明了一个有用的引理，我们现在正式陈述它：

**引理 6.** 对于任何 $l < k$，$p_k$ 与 $\mathbb{P}_l$ 中的每个多项式正交。 [cite: 55]

事实上，正交多项式的零点将是高斯求积节点。 [cite: 56] 以下引理描述了它们的一些关键性质： [cite: 57]

**引理 7.** $p_m$ 的所有 m 个零点都是单根，因此是不同的，并且位于 $(a,b)$ 内。 [cite: 57]

**证明：** 我们只需要考虑 $m \ge 1$。在这种情况下：
$$\langle p_m, 1 \rangle = \int_a^b p_m(t)w(t)dt = 0,$$
所以我们知道 $p_m$ 在 $(a,b)$ 内至少改变一次符号。 [cite: 58] 令 $\tau_1, \ldots, \tau_k$ 表示 $p_m$ 在 $(a,b)$ 内改变符号的不同点。假设 $k < m$ 导致矛盾，并定义：
$$q(t) := \prod_{j=1}^k (t - \tau_j) \in \mathbb{P}_k.$$
[cite: 59]由于 $p_m$ 和 q 都在 $\tau_j$ 处改变符号，因此 $p_m q$ 在 $(a,b)$ 上从不改变符号，由此可知：
$$\langle p_m, q \rangle = \int_a^b p_m(t)q(t)w(t)dt \ne 0.$$
但是 $p_m \perp \mathbb{P}_k$，所以这是一个矛盾。 [cite: 60] 我们得出结论，$p_m$ 在 $(a,b)$ 内至少有 m 个零点。 [cite: 61] 由于 $p_m$ 的次数是 m，根据根的计数，它们都必须是单根，并且 $p_m$ 不能在 $(a,b)$ 之外有任何零点。 [cite: 62]

## 3.4 高斯求积

在某节中，给定节点 $c_1, \ldots, c_s$，我们解释了如何选择权重 $b_1, \ldots, b_s$，使得求积法则：
$$\int_0^1 \xi(u)du \approx \sum_{i=1}^s b_i \xi(c_i)$$
对于多项式 $\xi \in \mathbb{P}_{s-1}$ 是精确的。 [cite: 63] 权重是通过精确积分数据 $(c_i, \xi(c_i))$（$i=1, \ldots, s$）的拉格朗日插值得到的，从而得到精确公式：
$$b_i := \int_0^1 l_i(u; c)du \quad \text{对于 } i=1, \ldots, m.$$
给定 $t=(t_1, \ldots, t_m)$，完全相同的过程更一般地产生一个求积法则：
$$\int_a^b g(t)w(t)dt \approx \sum_{i=1}^m b_i g(t_i)$$
对于多项式 $g \in \mathbb{P}_{m-1}$ 是精确的，权重定义为：
$$b_i := \int_a^b l_i(t; t)w(t)dt \quad \text{对于 } i=1, \ldots, m.$$
（注意：这里我们对插值点使用从1开始的索引约定，与附录1中在线性多步法（LMMs）上下文中讨论插值时使用的从0开始的索引约定相反。）[cite: 64]

值得注意的是，如果 $t_1, \ldots, t_m \in (a,b)$ 是关于区间 $[a,b]$ 上的权函数 w 的第 m 个正交多项式 $p_m$ 的零点，那么事实上这个求积法则对于所有多项式 $g \in \mathbb{P}_{2m-1}$ 都是精确的。 [cite: 64, 65]

**定理 8.** 令 $a < t_1 < \ldots < t_m < b$ 为关于区间 $[a,b]$ 上的权函数 w 的第 m 个正交多项式 $p_m$ 的零点，并令 $t=(t_1, \ldots, t_m)$。 [cite: 65] 定义权重：
$$b_i := \int_a^b l_i(t; t)w(t)dt \quad \text{对于 } i=1, \ldots, m.$$
那么对于所有 $g \in \mathbb{P}_{2m-1}$：
$$\int_a^b g(t)w(t)dt = \sum_{i=1}^m b_i g(t_i).$$
[cite: 66]
**证明：** 令 $g \in \mathbb{P}_{2m-1}$。由于 $p_m$ 的次数是 m，通过多项式长除法我们可以写出：
$$g = p_m q + r,$$
其中 $q \in \mathbb{P}_{m-1}$，并且 $\text{deg}(r) < \text{deg}(p_m)$ （原文为 $\text{deg}(r) < \text{deg}(q)$，根据上下文应为 $\text{deg}(r) < \text{deg}(p_m)$ 或 $r \in \mathbb{P}_{m-1}$），因此 $r \in \mathbb{P}_{m-1}$。 [cite: 67] 那么：
$$\sum_{i=1}^m b_i g(t_i) = \sum_{i=1}^m b_i p_m(t_i)q(t_i) + \sum_{i=1}^m b_i r(t_i).$$
但是对于所有 $i=1, \ldots, m$，$p_m(t_i) = 0$，所以事实上： [cite: 68]
$$\sum_{i=1}^m b_i g(t_i) = \sum_{i=1}^m b_i r(t_i).$$
但是由于 r 是一个次数最多为 $m-1$ 的多项式，由权重 $b_i$ 和求积点 $t_i$ 定义的求积法则是精确的，事实上我们已经证明了：
$$\sum_{i=1}^m b_i g(t_i) = \int_a^b r(t)w(t)dt. \quad (3.1)$$
同时，我们可以计算：
$$\int_a^b g(t)w(t)dt = \int_a^b p_m(t)q(t)w(t)dt + \int_a^b r(t)w(t)dt$$
$$= \langle p_m, q \rangle + \sum_{i=1}^m b_i g(t_i)$$
$$= \sum_{i=1}^m b_i g(t_i),$$
这里我们使用了 (3.1) 以及 $p_m \perp \mathbb{P}_{m-1}$ 的事实。