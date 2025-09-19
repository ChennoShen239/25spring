# 社会与经济网络导论  
**Lecture 2: 基本性质 —— 微观度量（中心性）**  
邢亦青  
xingyq@nsd.pku.edu.cn  
课程参考资料，未经允许请勿传播。

---

## 应关注的度量/性质（Measures/Properties to Look At）

- **宏观（整体，聚合）Macro (global, aggregate)**
  - 距离/直径（Distance/Diameter）
  - 连通分量（Components）

- **微观（个体）Micro (individual)**
  - 度（Degree，链接数 # of links）
  - 中心性（Centrality，若干定义）
  - 聚类——共同朋友（Clustering - common friends，next class）

---

## 网络的表示（Representing Networks）

**回顾……网络 $(N,g)$（Recall… Network $(N,g)$）**

- $N=\{1,\ldots,n\}$：节点（或顶点、参与者、代理人等；nodes or vertices, players, agents…）
- $g \in \{0,1\}^{n\times n}$：邻接矩阵（无权，可能有向；unweighted, possibly directed）
- $g_{ij}=1$：表示节点 $i$ 与 $j$ 之间存在一条连接/关系/边（a link, tie, or edge between $i$ and $j$）
- 另一种记法：若 $i$ 与 $j$ 之间存在连接，则记作 $ij \in g$（Alternative notation: $ij \in g$ if link between $i$ and $j$）


## 2.1 度（Degree）

- **邻域（Neighborhood）：**  
  $N_i(g) = \{\, j \mid ij \in g \,\}$  
  （通常约定：$ii \notin g$）

- **度（Degree）：**  
  $d_i = \#\,N_i(g)$  
  – 节点 $i$ 的度 = $i$ 的链接数（# of $i$’s links）

---

### 平均度（Average Degree）

- HS Friendships (CJP 09)：6.5  
- Romances (BMS 03)：0.8  
- Borrowing (BCDJ 12)：3.2  
- Co-authors (Newman 01, GLM 06)：  
  - Bio：15.5  
  - Econ：1.7  
  - Math：3.9  
  - Physics：9.3  
- Facebook (Marlow 09)：120  

---

### 平均度（Average Degree）

- Q: 这两个例子的平均度是多少？  
- ![[Pasted image 20250919225229.png]]
- **平均值只反映部分信息**  
  – 因此，考察**度的分布**是有用的（下节课）


## 2.2：中心性度量——导论

### 中心性：节点的“重要性”
- 思考：你如何定义某个人（节点）的“重要性”？

### 中心性：可以度量的不同方面
- **度（Degree）** —— 连接性（connectedness）
- **接近度/衰减型接近度（Closeness, Decay）** —— 触达其他节点的难易程度
- **中介中心性（Betweenness）** —— 作为中间人、连接者的角色
- **影响力、声望、特征向量（Influence, Prestige, Eigenvectors）** —— *“重要的不只是你知道什么，而是你认识谁……”*
- 以及更多……（Bloch–Jackson–Tebaldi 2017）  
  https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2749124

---

### 度中心性（Degree Centrality）
- 一个节点有多“连通”？  
- **度**刻画连通性  
- （有时按 $n-1$ 进行归一化）

![[Pasted image 20250919225410.png]]

---

### Padgett & Ansell（1993）数据  
**佛罗伦萨婚姻网络，1430 年代（Florentine Marriages, 1430’s）**
![[Pasted image 20250919225612.png]]

- Node 3 is considered as `central`  as 1 and 2

> [!remark]
> ### 为什么说 “Node 3 is considered as **central** as 1 and 2”？
> 
> 这句话是**在“度中心性（degree centrality）”的语境下**说的。  
> 度中心性只看一个节点的**直接邻居数量**：$C_D(i)=d_i$（或归一化为 $d_i/(n-1)$）。  
> 在图中，1、2、3 号节点的度都相同（都连着 3 条边），因此
> $$C_D(1)=C_D(2)=C_D(3)$$
> 按“度中心性”它们**同样中心**。
> 
> 直觉上：
> - 节点 1：连着左侧链条、右上支、以及节点 2（度=3）  
> - 节点 2：连着节点 1、右侧支、下方支（度=3）  
> - 节点 3：连着左侧三角里的两个点和右侧链条的一个点（度=3）
> 
> ---
> 
> ### 但这只是一种“局部”中心性
> 
> 虽然度数一样，节点 1 与 2 明显处在**桥接**位置，连接不同子群；  
> 节点 3 更偏局部（在一个三角里）。如果用**接近度**或**中介中心性**衡量：
> 
> - **接近度（closeness）**：$C_C(i)=\dfrac{n-1}{\sum_j \ell(i,j)}$  
>   1、2 的到全网的平均距离更短，$C_C(1),C_C(2)$ 会 **大于** $C_C(3)$。
> - **中介中心性（betweenness）**：统计经过节点的最短路比例  
>   1、2 落在跨群最短路上更频繁，因而远高于 3。
> 
> **结论**：  
> “Node 3 与 1、2 一样中心”仅在**度中心性**下成立；若考虑更“全局”的中心性（接近度/中介等），1、2 会比 3 更中心。这也说明度中心性虽简单，但可能**忽略桥接作用**与网络位置差异。


## 2.3 接近度（Closeness）

**Closeness centrality:**  
$$
\frac{n-1}{\sum_j l(i,j)}
$$

- 相对于其他节点的**相对距离**  
- 与距离**成反比**缩放——距离加倍，则接近度减半（“twice as far is half as central”）

> [!note]
> ### 解释：接近度中心性（Closeness Centrality）
> 
> 给定节点总数为 $n$ 的网络，节点 $i$ 的接近度中心性定义为
> $$
> C(i)\;=\;\frac{n-1}{\sum_{j\ne i} \, \ell(i,j)}\,,
> $$
> 其中：
> - $\ell(i,j)$ 表示从 $i$ 到 $j$ 的**最短路径长度**（也称测地距离，通常以“跳数”计数；若是加权网络，则为最小权重和）。
> - 分子 $n-1$ 是**归一化因子**：在完全图中，每个节点到其他所有节点的距离都是 $1$，于是 $C(i)=1$。
> 
> **直观含义：**  
> $C(i)$ 等于“$i$ 到其他节点的**平均距离**的倒数”乘上一个常数。具体地，
> $$
> \text{AvgDist}(i)\;=\;\frac{1}{n-1}\sum_{j\ne i}\ell(i,j)
> \quad\Longrightarrow\quad
> C(i)\;=\;\frac{1}{\text{AvgDist}(i)}.
> $$
> 因此，$i$ 越**靠近**全网其它节点（平均距离越小），$C(i)$ 就越大。距离**加倍**，$C(i)$ 就会**减半**（“twice as far is half as central”）。
> 
> ---
> 
> ### 例子与对比
> 
> - **星形图（star）**：中心到其余 $n-1$ 个叶子的距离都为 $1$，  
>   $$
>   C(\text{中心})=\frac{n-1}{(n-1)\cdot 1}=1;\qquad
>   C(\text{叶子})=\frac{n-1}{1+2(n-2)}=\frac{n-1}{2n-3}\approx \tfrac{1}{2}.
>   $$
>   中心比叶子“更接近”全网。
> 
> - **路径图（line/path）**（以 $n=5$ 为例）：  
>   中心节点的距离和为 $2+1+1+2=6$，$C=\frac{4}{6}\approx0.667$；  
>   端点的距离和为 $1+2+3+4=10$，$C=\frac{4}{10}=0.4$。  
>   位于中间的位置更“居中”，因此接近度更大。
> 
> ---
> 
> ### 实务细节与变体
> 
> - **非连通图**：若 $i$ 无法到达某些节点，则 $\ell(i,j)=\infty$，$C(i)$ 形式上变为 $0$。常见处理：
>   1) 仅在 $i$ 所在的连通分量上计算；  
>   2) 使用**谐和接近度（harmonic closeness）**：$\sum_{j\ne i} \frac{1}{\ell(i,j)}$，并约定不可达时取 $0$。  
> 
> - **有向/加权网络**：将 $\ell(i,j)$ 替换为有向最短路/加权最短路距离即可。
> 
> - **尺度**：$C(i)$ 的量纲是“距离的倒数”（如 $1/$跳数），便于跨网络比较（在采用相同归一化时）。


![[Pasted image 20250919230224.png]]

## 2.4 衰减中心性（Decay Centrality）

$$
C_i^{\delta}(g) \;=\; \sum_{j\ne i} \delta^{\,\ell(i,j)}
$$

- $0<\delta<1$
- 当 $\delta$ 接近 $1$ 时，度量趋近于**连通分量的规模**（component size）
- 当 $\delta$ 接近 $0$ 时，度量趋近于**度**（degree）
- 介于两者之间时，这是**随距离衰减**的度量 —— 对更远的节点赋予**指数级**更小的权重

---

### 规范化：衰减中心性（Normalize: Decay Centrality）

**Normalized version:**
$$
\tilde{C}_i^{\delta}(g)
\;=\;
\frac{\sum_{j\ne i}\delta^{\,\ell(i,j)}}{(n-1)\,\delta}
$$

- $(n-1)\,\delta$ 是**最低可能的衰减**。
![[Pasted image 20250919230455.png]]
## 2.5 介数（Freeman）中心性

- $P_{j,k}$：节点 $j$ 与 $k$ 之间的**测地线**条数  
- $P_i(j,k)$：节点 $j$ 与 $k$ 之间**经过 $i$** 的测地线条数

**介数中心性：**
$$
C_i^{B}(g)\;=\;\sum_{\substack{j<k\\ j,k\neq i}}
\frac{P_i(j,k)}{P_{j,k}} \, .
$$

**归一化（Normalized）介数中心性：**
$$
C_i^{B,\mathrm{norm}}(g)\;=\;
\frac{2}{(n-1)(n-2)}\,
\sum_{\substack{j<k\\ j,k\neq i}}
\frac{P_i(j,k)}{P_{j,k}} \, .
$$

*Betweenness Centrality*

> [!remark]
> ### 直观理解 Freeman（介数）中心性
> 
> **定义回顾**  
> 对每个与节点 $i$ 不同的无序节点对 $(j,k)$，设
> - $P_{j,k}$：$j$ 与 $k$ 之间**所有最短路径（测地线）**的条数；
> - $P_i(j,k)$：其中**经过 $i$** 的最短路径条数。
> 
> 则
> $$
> C_i^{B}(g)=\sum_{\substack{j<k\\ j,k\ne i}}\frac{P_i(j,k)}{P_{j,k}},
> \qquad
> C_i^{B,\text{norm}}(g)=\frac{2}{(n-1)(n-2)}\,
> \sum_{\substack{j<k\\ j,k\ne i}}\frac{P_i(j,k)}{P_{j,k}}.
> $$
> 
> **直觉**  
> 把“信息/流量”想像为沿**最短路**传播：谁被更多最短路“踩过”，谁就**更像中间人/经纪人**，能控制跨群沟通的“要道”。  
> 若某对 $(j,k)$ 存在多条等长最短路，$i$ 只拿**其中一部分的“学分”**，即按 $P_i(j,k)/P_{j,k}$ 平分。
> 
> ---
> 
> ### 三个一眼就懂的例子
> 
> 1) **星形图（star），中心为 $c$**  
>    所有叶子对的最短路都必须走 $c$，所以
>    $$
>    C_c^{B}=\binom{n-1}{2},\quad
>    C_c^{B,\text{norm}}=1;\qquad
>    \text{任一叶子的介数}=0.
>    $$
>    *中心是“唯一桥梁”，权力最大。*
> 
> 2) **路径图（line），$n=5$，节点依次 $1$–$2$–$3$–$4$–$5$**  
>    看 $i=3$。其他节点集合 $\{1,2,4,5\}$ 有 $\binom{4}{2}=6$ 对：  
>    $(1,4),(1,5),(2,4),(2,5)$ 的最短路都经过 3，而 $(1,2)$、$(4,5)$ 不经过。  
>    $$
>    C_3^{B}=4,\qquad
>    C_3^{B,\text{norm}}=\frac{2\cdot 4}{(5-1)(5-2)}=\frac{8}{12}=\frac{2}{3}.
>    $$
>    *处在“中间”的节点，介数更高。*
> 
> 3) **四环（cycle $C_4$）$1$–$2$–$3$–$4$–$1$**，看 $i=2$  
>    需要它的只有对 $(1,3)$，且有两条等长最短路：$1$–$2$–$3$ 与 $1$–$4$–$3$，  
>    因而贡献为 $1/2$；总和 $C_2^{B}=1/2$，归一化 $C_2^{B,\text{norm}}= \frac{2}{3\cdot 2}\cdot\frac{1}{2}= \frac{1}{6}$.  
>    *有“替代路径”时，介数被分摊。*
> 
> ---
> 
> ### 该指标在说什么（与不说什么）
> 
> - **在说**：一个节点对跨群最短通信的**控制力/桥接作用**。  
> - **不在说**：所有可能路径的流量（它只看最短路）、节点的直接人脉多少（那是**度**），或到全网的平均距离（那是**接近度**）。
> 
> 小贴士：非连通时，通常只对连通的 $(j,k)$ 计数；有向/加权网络则把“最短路”改为有向/加权最短路。


![[Pasted image 20250919231012.png]]

![[Pasted image 20250919231021.png]]