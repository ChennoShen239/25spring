> This note has to be working with [[Ch4.pdf]] and I'll skip the writing of existing part in the pdf file but only containing my own thinkings.

# Limits of Functions

> [!PDF|yellow] [[Math 104/Ch4.pdf#page=1&selection=23,0,25,1&color=yellow|Ch4, p.1]]
> > (accumulation point). 
> 
> This is the definition, notice we only need the $a \in A$ exists 


> [!PDF|yellow] [[Math 104/Ch4.pdf#page=1&selection=108,18,120,0&color=yellow|Ch4, p.1]]
> >  c ∈ R is an accumulation point of A
> 
> here we have by definition, $\forall \varepsilon>0,\exists x \in A$ such that $\left| c-x \right|<\varepsilon$.
> > i.e. the function $f$ is defined around $c$


> [!PDF|red] [[Math 104/Ch4.pdf#page=1&selection=249,4,253,22&color=red|Ch4, p.1]]
> > a function needn’t be defined at c for its limit to exist
> 
> We don't care about whether $f$ has definition on the limit point $c$

> [!PDF|yellow] [[Math 104/Ch4.pdf#page=2&selection=152,0,193,0&color=yellow|Ch4, p.2]]
> > Thus, if δ = 3ϵ, then x ∈ A and |x − 9| < δ implies that |f (x) − 6| < ϵ
> 
> If we gotta prove by definition, one important thing is that we finally want the $\left| f(x)-L \right|$ be something like $\left| x-c \right|$ so that we can then choose the **neighborhood**.

> [!PDF|yellow] [[Math 104/Ch4.pdf#page=2&selection=199,25,199,31&color=yellow|Ch4, p.2]]
> > unique
> 
> By contradiction just let there be $2$ limits.

> [!PDF|red] [[Math 104/Ch4.pdf#page=2&selection=478,0,479,1&color=red|Ch4, p.2]]
> > Theorem 1.1. 
> 
> For this theorem, the most important part is that the sequence $\implies$ limit part holds for **all** $(x_{n})\in A$ such that $\lim_{ n \to \infty }x_{n} = c$

> [!PDF|yellow] [[Math 104/Ch4.pdf#page=3&selection=389,6,389,23&color=yellow|Ch4, p.3]]
> > accumulation point
> 
> Just for review, a point $x$ is an accumulation point of $S$ if for every neighborhood $U$ of $x$, the intersection $U \cap \{ S \setminus \{ x \} \}$ is non-empty

> [!PDF|yellow] [[Math 104/Ch4.pdf#page=3&selection=367,0,368,0&color=yellow|Ch4, p.3]]
> > Corollary 1.1.
> 
> convergent $\{ x \}$ but divergent $(f(x_{n}))$

> [!PDF|yellow] [[Math 104/Ch4.pdf#page=5&selection=135,0,135,15&color=yellow|Ch4, p.5]]
> > Proposition 2.1
> 
> The limit $\to$ LR limits is trivial. For the other side, just take the minimum $\delta$.


> [!PDF|red] [[Math 104/Ch4.pdf#page=6&selection=62,0,137,28&color=red|Ch4, p.6]]
> > Exercise 1. Given f : R → R, prove lim x→∞ f (x) = lim t→0+ f  1 t  , lim x→−∞ f (x) = lim t→0− f  1 t  . (assume all the limits exist
> 
> Here's the proof

Proof. of Ex 1
We first prove the positive case:
1. $\lim_{ x \to \infty }f(x) = L \implies \lim_{ t \to 0^{+} }f(t)= L$:
	1. by definition, for all $\epsilon > 0$, there exists $M > 0$ such that $\forall x>M$, $|f(x)-L|<\epsilon$. Then we can let $\delta = | \frac{1}{{M}}|>0$, then $\forall t\in(0,\delta)$, we have $\frac{1}{t}>{M}$, and therefore $|f\left( \frac{1}{t} \right)-L|< \epsilon$.
2. $\lim_{ t \to 0^{+} }f\left( \frac{1}{t} \right) = L \implies \lim_{ x \to \infty }f(x) = L$:
	1. by definition, for all $\epsilon >0$, there exists $\delta>0$ such that $\forall \frac{1}{t} \in(0,\delta),|f\left( \frac{1}{t} \right)-L|<\epsilon$. Then we can let $M = \frac{1}{\delta}$, then for all $x > M$, we have equivalently $\frac{1}{x}<\delta$, so $|f(x) -L|<\epsilon$

Similarly we can get the result for the negative case.

> [!PDF|red] [[Math 104/Ch4.pdf#page=6&selection=360,18,360,54&color=red|Ch4, p.6]]
> > ; it does not mean that the limit ex
> 
> $\lim_{ x \to c }f(x) = \pm \infty$ doesn't mean the limit exists.

> [!PDF|red] [[Math 104/Ch4.pdf#page=8&selection=3,0,4,0&color=red|Ch4, p.8]]
> > Theorem 3.2.
> 
> Here's the proof

Proof of squeeze Theorem:
1. since the limit of $f$ and $h$ exists, for any $\epsilon>0$, there exists $\delta_{1} >0$ such that $\forall x \in(c-\delta_{1},c+\delta_{1})$, $|f(x)-L|<\epsilon$ and there exists $\delta_{2}>0$ such that $\forall x \in(c-\delta_{2},c+\delta_{2})$, $|h(x)-L|<\epsilon$
2. let $\delta = \min \{ \delta_{1},\delta_{2} \}$, then for all $x \in (c-\delta,c+\delta)$, we have $$
L - \epsilon < f(x) \leq g(x) \leq h(x) < L + \epsilon
$$
	i.e.$|g(x)-L|< \epsilon$. 

