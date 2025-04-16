> This is a note for my MATH 104, which should be used together with the note provided by the professor in [[Ch7.pdf]]

# sequences and series of functions

> [!PDF|yellow] [[Ch7.pdf#page=1&selection=29,0,104,1&color=yellow|Ch7, p.1]]
> > Definition 1.1. Suppose that (fn) is a sequence of functions fn : A → R and f : A → R. Then fn → f pointwise on A if fn(x) → f (x) as n → ∞ for every x ∈ A.
> 
> Note the way we call this as "$f_{n} \to f$ pointwise on $A$"

> [!PDF|red] [[Ch7.pdf#page=2&selection=75,0,154,15&color=red|Ch7, p.2]]
> > Example 1.2. Suppose that fn : [0, 1] → R is defined by fn(x) = xn. If 0 ≤ x < 1, then xn → 0 as n → ∞, while if x = 1, then xn → 1 as n → ∞. So fn → f pointwise where
> 
> We use this case to prove the **point-wise convergence** doesn't preserve continuity
> 

> [!PDF|red] [[Ch7.pdf#page=2&selection=205,0,292,1&color=red|Ch7, p.2]]
> > Example 1.3. Define fn : R → R by fn(x) = sin nx n . Then fn → 0 pointwise on R. The sequence (f ′ n) of derivatives f ′ n(x) = cos nx does not converge pointwise on R; for example, f ′ n(π) = (−1)n does not converge as n → ∞. 
> 
> This case shows that we don't expect to differentiate a pointwise convergent sequence.

> [!PDF|yellow] [[Ch7.pdf#page=2&selection=305,0,395,1&color=yellow|Ch7, p.2]]
> > Definition 2.1. Suppose that (fn) is a sequence of functions fn : A → R and f : A → R. Then fn → f uniformly on A if, for every ϵ > 0, there exists N ∈ N such that n > N implies that |fn(x) − f (x)| < ϵ for all x ∈ A.
> 
> The way we describe **uniform convergent** is that "$f_{n} \to f$  uniformly on $A$", with a definition in $N-\epsilon$ language.

> [!PDF|red] [[Ch7.pdf#page=3&selection=18,1,32,2&color=red|Ch7, p.3]]
> > N depends only on ϵ and not on x ∈ A, 
> 
> remember this to see the difference

> [!PDF|red] [[Ch7.pdf#page=3&selection=44,0,45,38&color=red|Ch7, p.3]]
> > A uniformly convergent sequence is always pointwise convergent (to the same limit), but the converse is not true. 
> 
> we can say that uniformly convergent $>$ pointwise convergent

> [!PDF|yellow] [[Ch7.pdf#page=3&selection=311,0,383,1&color=yellow|Ch7, p.3]]
> > Definition 3.1. A sequence (fn) of functions fn : A → R is uniformly Cauchy on A if for every ϵ > 0 there exists N ∈ N such that m, n > N implies that |fm(x) − fn(x)| < ϵ for all x ∈ A.
> 
> Basically you just need to memorize $f_{n},f_{m}$ as the previous $x_{n},x_{m}$

> [!PDF|red] [[Ch7.pdf#page=3&selection=385,0,415,1&color=red|Ch7, p.3]]
> > Theorem 3.1. A sequence (fn) of functions fn : A → R converges uniformly on A if and only if it is uniformly Cauchy on A.
> 
> Again, uniformly convergent $\iff$ Cauchy convergent

Let's go over this proof just for review.
we first prove the $\Rightarrow$ part:
1. suppose $(f_{n})$ converges uniformly on $A$ to $f$, so given any $\epsilon>0$, there exists $N \in \mathbb{N}$ such that $$
	\lvert f_{n}(x) - f(x) \rvert < \frac{\epsilon}{2}
$$
2. then for any $m,n>N$, we have $$
\lvert f_{m}-f_{n} \rvert \leq \lvert f_{m} -f \rvert +\lvert f_{n} -f \rvert \leq \frac{\epsilon}{2} + \frac{\epsilon}{2}  =\epsilon
$$
3. this proves $(f_{n})$ is uniformly Cauchy
Then we do the $\Leftarrow$ part:
4. suppose $(f_{n})$ is uniformly Cauchy. then for each $x \in A$, we have sequence $(f_{n}(x))$ is Cauchy, so it converges. we then define $f : A\to \mathbb{R}$ by $$
f(x) = \lim_{ n \to \infty } f_{n}(x)
$$
it's easy to see $f_{n} \to f$ pointwise
5. then let $\epsilon >0$, then we have $N \in \mathbb{N}$ such that $$
\lvert f_{m} - f_{n} \rvert < \frac{\epsilon}{2}
$$
6. let $n>N,x \in A$, then we have $$
\lvert f_{n} (x) - f(x) \rvert \leq \lvert f_{n} - f_{m} \rvert  + \lvert f_{m} -f \rvert < \frac{\epsilon}{2} + \lvert f_{m} -f \rvert 
$$holds for every $m >N$ 
then given $f_{n} \to f$ pointwise, we know $f_{m}(x) \to f(x)$, so there exists a $N_{1} \in \mathbb{N}$ such that $\lvert f_{m}(x) -f(x) \rvert< \frac{\epsilon}{2}$ for all $m > N_{1}$, so it follows that $$
\lvert f_{n} - f \rvert < \epsilon 
$$
> Recall how we get the $m$, it's from 2 conditions: 1. it's bigger than $N$, 2. it can let the $\lvert f_{m} -f \rvert$ be small enough. 
> In other words, once we find the $N$, even $f_{n}$ is far alway from $f$ itself, we can always find a $f_{m}$ with sufficiently large $m$ to be close enough to $f$, but also close enough to $f_{n}$, it doesn't matter how we choose $m$, it only matters that we know there always be this $m$.

then finally we can say that $\forall x \in A,$ there exists an $N \in \mathbb{N}$ such that $$
\lvert f_{n} - f \rvert < \epsilon
$$
在本节中，我们将证明，与逐点收敛不同，一致收敛能够保持有界性和连续性。然而，一致收敛在保持可导性方面并不比逐点收敛更强。尽管如此，我们仍给出一个可以对收敛函数列进行求导的结果，其关键假设是导数列**一致收敛**。

> [!PDF|yellow] [[Ch7.pdf#page=5&selection=6,0,60,1&color=yellow|Ch7, p.5]]
> > Theorem 4.1. Suppose that fn : A → R is bounded on A for every n ∈ N and fn → f uniformly on A. Then f : A → R is bounded on A.
> 
> Given the sequence $(f_{n})$ is bounded, this tells you that the limit $f$ is also bounded.

> [!PDF|yellow] [[Ch7.pdf#page=5&selection=213,0,262,1&color=yellow|Ch7, p.5]]
> > Theorem 4.2. If a sequence (fn) of continuous functions fn : A → R converges uniformly on A ⊂ R to f : A → R, then f is continuous on A.
> 
> This part is similar

> [!PDF|note] [[Ch7.pdf#page=6&selection=36,0,82,1&color=note|Ch7, p.6]]
> > Exercise 1. Prove lim n→∞ lim x→c fn(x) = lim x→c lim n→∞ fn(x). if fn uniformly converges to f .
> 
> Now let's prove this

we suppose $f_{n} \to f$ uniformly, then we suppose $\lim_{ x \to c }f_{n}(x)$ exists and let the limit be $L_{n}$
since $f_{n} \to f$ uniformly, then $$
\lim_{ n \to \infty } f_{n}(x) = f(x)
$$
so $$
\lim_{ x \to c }  \lim_{ n \to \infty } f_{n}(x) = \lim_{ x \to c } f(x) \tag{RHS}
$$
also we can see that $$
\lvert \lim_{ x \to c } f_{n}(x) - \lim_{ x \to c } f(x) \rvert \leq \sup_{x \in A} \lvert f_{n}(x) - f(x) \rvert \to 0
$$
so $$
\lim_{ n \to \infty } \lim_{ x \to c }  f_{n}(x) = \lim_{ x \to c } f(x) \tag{LHS}
$$
then we know the $\lim_{ n \to \infty }$ and $\lim_{ x  \to c }$ can be exchanged

---
可微函数的一致收敛**通常并不意味着**其导数的收敛性，或其极限函数的可导性（例如见例 2.2）。然而，如果我们加强假设，要求导数**一致收敛**（而不仅仅是逐点收敛），则可以得到一个有用的结论。

---
> [!PDF|yellow] [[Ch7.pdf#page=6&selection=94,0,171,1&color=yellow|Ch7, p.6]]
> > Theorem 4.3. Suppose that (fn) is a sequence of differentiable functions fn : (a, b) → R such that fn → f pointwise and f ′ n → g uniformly for some f, g : (a, b) → R. Then f is differentiable on (a, b) and f ′ = g.
> 
> ![[Pasted image 20250414183520.png]]
> Note that $(f_{n})$ can be only **pointwise convergent** but $(f'_{n})$ has to be **uniformly convergent**.

We go through the proof now.
The key thought is to split this into 3 parts and prove them to be close to $0$ by $\frac{\epsilon}{3}$

> [!PDF|note] [[Ch7.pdf#page=7&selection=397,0,399,22&color=note|Ch7, p.7]]
> > Exercise 2. Prove the above claim.
> 
> 
> **Exercise 2.**  
> Prove that under the conditions of Theorem 4.3, the following exchange of limits holds:
> 
> $$
> \lim_{n \to \infty} \lim_{x \to c} \frac{f_n(x) - f_n(c)}{x - c} = \lim_{x \to c} \lim_{n \to \infty} \frac{f_n(x) - f_n(c)}{x - c}.
> $$

**Proof.**  
Suppose $(f_n)$ is a sequence of differentiable functions on $(a, b)$, and that:

- $f_n \to f$ pointwise,
- $f_n' \to g$ uniformly,

where $f$ and $g$ are real-valued functions on $(a, b)$. From Theorem 4.3, we know that $f$ is differentiable and $f' = g$. We analyze the two sides of the equation.

**Left-hand side:**
Since $f_n$ is differentiable, we have:

$$
\lim_{x \to c} \frac{f_n(x) - f_n(c)}{x - c} = f_n'(c),
$$

so:

$$
\lim_{n \to \infty} \lim_{x \to c} \frac{f_n(x) - f_n(c)}{x - c} = \lim_{n \to \infty} f_n'(c).
$$

Given that $f_n' \to g$ uniformly, we have:

$$
\lim_{n \to \infty} f_n'(c) = g(c).
$$

**Right-hand side:**

From Theorem 4.3 again, $f$ is differentiable at $c$, and:
$$
f'(c) = \lim_{x \to c} \frac{f(x) - f(c)}{x - c}.
$$

Since $f = \lim_{n \to \infty} f_n$ pointwise, we consider:

$$
\lim_{n \to \infty} \frac{f_n(x) - f_n(c)}{x - c} = \frac{f(x) - f(c)}{x - c},
$$

and then:

$$
\lim_{x \to c} \lim_{n \to \infty} \frac{f_n(x) - f_n(c)}{x - c} = \lim_{x \to c} \frac{f(x) - f(c)}{x - c} = f'(c) = g(c).
$$

**Conclusion:**
Both sides equal $g(c)$, so the limits can be exchanged:
$$
\lim_{n \to \infty} \lim_{x \to c} \frac{f_n(x) - f_n(c)}{x - c} = \lim_{x \to c} \lim_{n \to \infty} \frac{f_n(x) - f_n(c)}{x - c}.
$$

> Just try to prove the LHS and RHS to be the same formula.

> [!PDF|yellow] [[Ch7.pdf#page=8&selection=238,0,254,1&color=yellow|Ch7, p.8]]
> > The series does, however, converge uniformly on [−ρ, ρ] for every 0 ≤ ρ < 1.
> 
> Did you see the difference? Once you set the $\rho$, you can say it's uniformly convergent. You can't do that to $(-1,1)$!


> [!PDF|yellow] [[Ch7.pdf#page=9&selection=0,0,81,1&color=yellow|Ch7, p.9]]
> > Theorem 5.1. Let (fn) be a sequence of functions fn : A → R. The series ∞X n=1 fn converges uniformly on A if and only if for every ϵ > 0 there exists N ∈ N such that nX k=m+1 fk(x) < ϵ for all x ∈ A and all n > m > N .
> 
> Just treat this as the given $n>m$, the $\lvert S_{m} - S_{n} \rvert<\epsilon$ holds.

> [!PDF|yellow] [[Ch7.pdf#page=9&selection=253,14,253,26&color=yellow|Ch7, p.9]]
> > "majorants,"
> 
> 主控函数

> [!PDF|yellow] [[Ch7.pdf#page=9&selection=255,0,354,1&color=yellow|Ch7, p.9]]
> > Theorem 5.2 (Weierstrass M -test). Let (fn) be a sequence of functions fn : A → R, and suppose that for every n ∈ N there exists a constant Mn ≥ 0 such that |fn(x)| ≤ Mn for all x ∈ A, ∞X n=1 Mn < ∞. Then ∞X n=1 fn(x). converges uniformly on A.
> 
> It's like finding a convergent upper bound, the proof will use the Cauchy of the $M_{n}$ sequence



