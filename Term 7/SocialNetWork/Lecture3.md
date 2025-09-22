- 要玩大航海
- 中欧专列，北极航线试运行

# Measures/Properties
- Micro 
	- Degree
	- Centrality
	- Clustering - common friends
- Macro
	- Distance
	- Diameter
	- Components
## Another Centrality
- Influence, prestige, eigenvectors
	- not what you know but who you know.
- So what's that "prestige"
> Image that you know 2 person, that's Alice and Bob and there is one guy who knows 2 person, Laoda and DT.

# Eigenvector Centrality — Rigorous Definition

## Setup
Let $G=(V,E)$ be a (possibly weighted) graph with $|V|=n$.  
Let $A\in\mathbb{R}^{n\times n}$ be its **adjacency matrix** with non-negative entries:
- **Undirected**: $A$ is symmetric, $A_{ij}=A_{ji}\ge 0$.
- **Directed**: $A_{ij}\ge 0$ is the weight of the edge $i\to j$.

Assume $A\ge 0$ (entrywise) and at least one edge exists.

## Core idea (fixed-point relation)
A node is important if it is linked **to important nodes**. Formally, a centrality vector
$$
x=\begin{bmatrix}x_1&\cdots&x_n\end{bmatrix}^\top\in\mathbb{R}_{\ge 0}^n\setminus\{0\}
$$
satisfies
$$
x_i \;\propto\; \sum_{j=1}^n A_{ij}\,x_j\quad\text{for all }i,
$$
i.e.
$$
A x \;=\; \lambda x
$$
for some scalar $\lambda>0$.

## Rigorous definition (Perron eigenvector)
Let $\rho(A)$ denote the spectral radius of $A$. An **eigenvector-centrality vector** is any
$$
x \in \mathbb{R}_{\ge 0}^n\setminus\{0\}\quad\text{s.t.}\quad A x \;=\; \rho(A)\,x,
$$
with a chosen normalization, e.g. $\|x\|_1=1$ or $\|x\|_2=1$.

### Existence and uniqueness (Perron–Frobenius)
- If $A$ is **irreducible** (e.g., $G$ is connected for undirected graphs; strongly connected for directed graphs), then:
  1. $\rho(A)>0$ is a **simple** eigenvalue;
  2. There exists a unique (up to positive scaling) **strictly positive** eigenvector $x\gg 0$ with $A x=\rho(A)x$.
- If $A$ is **reducible** (graph not connected / not strongly connected), any nonnegative solution of $A x=\rho(A)x$ has support contained in the union of strongly connected components whose **local** spectral radius equals $\rho(A)$. Nodes outside these components receive centrality $0$ under this definition.

## Directed graphs (in/out versions)
For a directed graph, two common choices are:
- **Incoming (authority-style)**: $A^\top x=\rho(A^\top)x$ (note $\rho(A^\top)=\rho(A)$).
- **Outgoing (hub-style)**: $A x=\rho(A)x$.

(Eigenvector centrality typically fixes one orientation and uses the Perron eigenvector accordingly; HITS separates hubs/authorities.)

## Computation (power iteration)
If $A$ is **primitive** (irreducible and aperiodic), the **power method** converges to the Perron vector:
$$
x^{(t+1)} \;=\; \frac{A\,x^{(t)}}{\|A\,x^{(t)}\|_p},\qquad t=0,1,2,\dots
$$
for any $x^{(0)}\gg 0$ and norm $p\in\{1,2\}$. The limit is the normalized eigenvector $x$ with $A x=\rho(A)x$.

## Normalizations
Common normalizations enforce comparability:
- $\|x\|_1=1$ (sum to one),
- $\|x\|_2=1$ (unit Euclidean norm),
- $\max_i x_i=1$.

## Notes and variants
- **Weights**: *Any nonnegative weights are allowed; negative edges violate Perron–Frobenius assumptions.*
- **Disconnection sensitivity**: Nodes not in the dominant (strongly) connected component of maximal spectral radius obtain $x_i=0$.
- **Katz centrality** (regularized variant): solves $x=\alpha A x + \beta \mathbf{1}$ with $0<\alpha<1/\rho(A)$; as $\beta\to 0^+$ and $\alpha\uparrow 1/\rho(A)$, Katz centrality approaches the Perron vector (up to scaling).

