> This is my lecture note for math 104 [[Ch5.pdf]], please read it with the pdf file.

> [!PDF|yellow] [[Ch5.pdf#page=1&selection=171,6,171,19&color=yellow|Ch5, p.1]]
> > isolated poin
> 
> for a review, $x \in S$ is an isolated point if there exists an open set $U$ such that $x \in U$ and $U \cap S = \{ x \}$.

> [!PDF|red] [[Ch5.pdf#page=1&selection=257,1,272,1&color=red|Ch5, p.1]]
> > →c f (x) = f (c),
> 
> only when $c$ is an accumulation point  can we say that $$
\lim_{ x \to c } f(x) = f(c)
$$

> [!PDF|yellow] [[Ch5.pdf#page=2&selection=0,0,1,0&color=yellow|Ch5, p.2]]
> > Example 1.2.
> 
> make sure you handle all the accumulation points and then the boundary points correct.

> [!PDF|red] [[Ch5.pdf#page=2&selection=231,0,232,1&color=red|Ch5, p.2]]
> > Theorem 1.1. 
> 
> Here's the proof

Proof of Theorem 1.1
1. we first prove the "if" part: (from "all $\left\{ x_{k} \right\} \to c,f(x_{k})\to f(c)$" to "$f(x)$ is continuous at $c$")
	1. if $f$ is discontinuous at $c$, then there exists $\epsilon_{0}>0$ such that $\forall \delta>0$, there exists $x \in A$ such that $$
|x-c|<\delta,|f(x)-f(c)|\geq\epsilon_{0}
$$
	2. then for every $n \in \mathbb{N}$, let $\delta = \frac{1}{n}$, then we have a sequence $(x_{n})$ such that $$
|x_{n}-c|< \frac{1}{n},|f(x_{n})-f(c)|\geq \epsilon_{0}
$$
	3. by squeeze theorem, $x_{n} \to c$ but $f(x_{n})$ doesn't converge to $f(c)$. Then it contradicts the hypothesis
2. Then we prove the "only if part": (from "$f$ is continuous at $c$ " to "all $\left\{ x_{n} \right\}\to c,f(x_{n})\to f(c)$")
	1. if $f$ is continuous at $c$, then for any $\epsilon>0$, there exists $\delta >0$ such that $$
\forall x \in(c-\delta ,c+\delta),|f(x)-f(c)|<\epsilon
$$
	2. then for any convergent sequence $(x_{n})\to c$ , we have that there exists a $N \in \mathbb{N}$ such that $$
\forall n>N,|x_{n}-c|<\delta
$$
	3. and this implies that $$
\forall n>N, |f(x_{n})-f(c)|<\epsilon
$$
	4. i.e. $(f(x_{n}))\to f(c)$.

> [!PDF|red] [[Ch5.pdf#page=4&selection=393,3,395,7&color=red|Ch5, p.4]]
> > he Thomae function is continuous at 0 and every irrational number and discontinuous at every nonzero rational number.
> 
> A proof of sketch:

3. $f$ is continuous at $0$: when $x \to 0$, no matter for rational numbers or irrational numbers the function value approaches $0$
4. $f$ is continuous at all **irrational numbers**: for every $c \in \mathbb{R} \setminus \mathbb{Q}$ , and for any neighborhood $U$ of $c$, for any $x \in \mathbb{Q} \cap U$, as $q$ is getting bigger, $f(x) \to 0$, i.e. continuous at $c$
> for a more detailed proof, see the pdf file for it!
5. $f$ is **discontinuous** at all **rational numbers**: for every $c \in \mathbb{Q}$,  there are infinite many irrational numbers $(x_{n}),\forall x_{n} \in \mathbb{R} \setminus\mathbb{Q}$  and the sequence $(f(x_{n}))\to_{0} \ne \frac{1}{q}$.

> [!PDF|yellow] [[Ch5.pdf#page=7&selection=0,0,2,12&color=yellow|Ch5, p.7]]
> > Example 2.4. The function
> 
> Here don' t forget to discuss the continuity at $x =0$.

> [!PDF|yellow] [[Ch5.pdf#page=7&selection=92,3,92,23&color=yellow|Ch5, p.7]]
> > uniformly continuous
> 
> The concept of uniformly continuous analog to that of Cauchy sequences

> [!PDF|red] [[Ch5.pdf#page=7&selection=168,2,169,21&color=red|Ch5, p.7]]
> > but the converse is not true.
> 
> This means that **Uniformly Continuous** $\to$ Continuity on $A$, and that only.

> [!PDF|red] [[Ch5.pdf#page=7&selection=303,24,310,1&color=red|Ch5, p.7]]
> >  every c ∈ A.
> 
> For this statement, the critical part is to realize that $c \in A$ here actually refer to the $y$ in the definition of uniformly continuity.

> [!PDF|yellow] [[Ch5.pdf#page=7&selection=319,0,320,0&color=yellow|Ch5, p.7]]
> > Proposition 3.1.
> 
> In other words, the sequences $(x_{n}),(y_{n})$ converge to the same limit but there function value don't.

> [!PDF|note] [[Ch5.pdf#page=8&selection=0,12,2,0&color=note|Ch5, p.8]]
> > Example 3.1. 
> 
> See?  The key here is to construct the relationship between $|f(x)-f(y)|$ and $|x-y|$.



> [!PDF|red] [[Ch5.pdf#page=9&selection=171,0,172,56&color=red|Ch5, p.9]]
> > It isn’t a coincidence that these examples of non-uniformly continuous functions have domains that are either unbounded or not clos
> > 
> All these **Continuous but not uniformly continuous** functions have domains that are **Either unbounded or not closed**

> [!PDF|red] [[Ch5.pdf#page=9&selection=197,0,198,1&color=red|Ch5, p.9]]
> > Theorem 4.1. 
> 
> Proof or Theorem 4.1

6. $\Rightarrow$: 
	1. since $A$ is bounded, the sequence $(x_{n})$ defined on $A$ is also bounded
	2. By Bolzano-Weierstrass theorem, $(x_{n})$ has a convergent subsequence $(x_{n_{k}})$ 
	3. since $A$ is closed, all convergent sequences' limits (including $(x_{n_{k}})$) is in $A$, therefore it's **sequentially compact**
7. $\Leftarrow$:
	1. We first prove $A$ is bounded:
		1. assume $A$ is not bounded
		2. then we can construct $(x_{n})$ such that $$
||x_{n}-0||>n
$$
		3. then $(x_{n})$ is unbounded, therefore doesn't have a limit $a \in A$
	2. Then we prove $A$ is closed:
		1. assume $A$ is not closed
		2. then there exists a limit point $a \not\in A$
		3. since $a$ is a limit point, there exists such sequence $(x_{n})  \subseteq A,x_{n} \to a$
		4. by sequential compactness, $(x_{n})$ must have a convergent subsequence $(x_{n_{k}})$ such that $x_{n_{k}}\to b \in A$.
		5. then we must have $a=b$, which contradicts $a \not\in A$.
> [!PDF|yellow] [[Ch5.pdf#page=9&selection=284,0,284,11&color=yellow|Ch5, p.9]]
> > Theorem 4.2
> 
> For proof of this, just use the definition and verify **Sequential Compactness**

> [!PDF|] [[Ch5.pdf#page=11&selection=141,32,141,75|Ch5, p.11]]
> >  it needn’t attain its supremum or infimum.
> 
> The key is that you can't get the maximum or minimum in $\mathbf{K}$

> [!PDF|yellow] [[Ch5.pdf#page=11&selection=351,0,352,1&color=yellow|Ch5, p.11]]
> > Theorem 4.4. 
> 
> Uniformly continuous $f$ given $K \subset \mathbb{R}$ is compact

![[Screenshot 2025-04-10 at 5.59.35 PM.png]]
> so it's likely you may need this

The main idea of the proof is just to construct 2 different sequences $\left\{ x_{n} \right\}_{n=1}^{\infty}, \left\{ y_{n} \right\}_{n=1}^{\infty}$ so that they share the same limit, then we prove they can't have different image limits.

> [!PDF|yellow] [[Ch5.pdf#page=12&selection=362,0,366,0&color=yellow|Ch5, p.12]]
> > Theorem 5.1 (Intermediate value).
> 
> The proof is pretty simple, just define $c= \sup{E}\in[a,b]$ and prove $f(c) =0$

> [!PDF|red] [[Ch5.pdf#page=14&selection=92,0,97,0&color=red|Ch5, p.14]]
> > Theorem 5.2 (Intermediate value theorem VERY IMPORTANT!). 
> 
> Here we have several requirements:
> 1. $[a,b]$ is closed and bounded
> 2. $d \in(f(a),f(b))$
> 3. $c \in(a,b)$ such that $f(c)=d$

> [!PDF|yellow] [[Ch5.pdf#page=14&selection=289,0,290,0&color=yellow|Ch5, p.14]]
> > Theorem 5.3.
> 
> This is like the special case for Theorem 4.2

> [!PDF|yellow] [[Ch5.pdf#page=15&selection=321,0,322,1&color=yellow|Ch5, p.15]]
> > Theorem 6.1. 
> 
> we first construct an interval $E$ here, then we prove the
>  $$\lim_{ x \to c^{-} } f(x) = \sup{E}$$
> result
> we care about the least upper bound of $E$, so it's enough to give an upper bound for proving the existence of $\sup{E}$.
> 


> [!PDF|yellow] [[Ch5.pdf#page=16&selection=223,0,223,36&color=yellow|Ch5, p.16]]
> > We leave the details as an exercise.
> 
> Let's do this!

1. Since $c\in I$ is an interior point of $I$, so the set $$
\mathbf{F} = \left\{ f(x): x \in I ,x>c \right\} 
$$is non-empty
2. since $f$ is monotonically increasing, we have $f(x)\geq f(c)$ for all $x>c$, then $F$ has an lower bound $f(c)$.
3. by the completeness of $\mathbb{R}$, we know $R = \inf{\mathbf{F}}$ exists, we now try to prove $$
\lim_{ x \to c^{+} } f(x) = R
$$
4. let $\epsilon>0$ be arbitrary positive number, since $R$ is the infimum of $\mathbf{F}$, so there exists $y_{0} \in \mathbf{F}$ such that $R\leq y_{0}<R+\epsilon$. 
5. Since $y_{0} \in \mathbf{F}$, we know there exists a $x_{0}>c$ such that $f(x_{0})=y_{0}$, then let $\delta = x_{0}-c>0$ , for any $x \in(c,c+\delta)\cap I$, we know  $$
R\leq f(x) \leq f(x_{0} )<R+\epsilon
$$
6. that is, $\forall x \in(c,c+\delta)$, we have $f(x) \in[R,R+\epsilon)$
7. that is, $$
\lim_{ x \to c^+ } f(x) = R = \inf{\mathbf{F}}
$$



