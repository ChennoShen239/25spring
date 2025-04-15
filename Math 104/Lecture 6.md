> This is the course note together with [[Ch6.pdf]], please refer to the original doc to see the whole note.

> [!PDF|yellow] [[Ch6.pdf#page=1&selection=35,0,36,1&color=yellow|Ch6, p.1]]
> > Definition 1.1. 
> 
> The key is to get the domain where $c \in(a,b)$  that let this limit exist.

> [!PDF|red] [[Ch6.pdf#page=4&selection=55,0,85,0&color=red|Ch6, p.4]]
> > a3 − b3 = (a − b) a2 + ab + b2 
> 
> Basic Algebra! Keep in mind you silly boy!

> [!PDF|yellow] [[Ch6.pdf#page=5&selection=339,0,348,25&color=yellow|Ch6, p.5]]
> > A function is differentiable at a < c < b if and only if the left and right derivatives at c both exist and are equal.
> 
> So you will have to check 2 properties:
> 1. left and right limit exist
> 2. They are equal.

> [!PDF|yellow] [[Ch6.pdf#page=6&selection=194,0,225,1&color=yellow|Ch6, p.6]]
> > Theorem 2.1. If f : (a, b) → R is differentiable at at c ∈ (a, b), then f is continuous at c.
> 
> Differentiable $\to$ continuous


> [!PDF|yellow] [[Ch6.pdf#page=7&selection=0,15,51,11&color=yellow|Ch6, p.7]]
> > Definition 2.1. A function f : (a, b) → R is continuously differentiable on (a, b), written f ∈ C1(a, b), if it is differentiable on (a, b) and f ′ : (a, b) → R is continuous.
> 
> For this, you need to memorize 4 points:
> 1. Written as $C^{1}(a,b)$
> 2. $f$ is differentiable
> 3. $f'$ is continuous
> 4. It's always a open interval

> [!PDF|yellow] [[Ch6.pdf#page=8&selection=77,0,81,0&color=yellow|Ch6, p.8]]
> > Theorem 2.3 (Chain rule).
> 
> The new points:
> 1. we need $c$ to be an interior point

> [!PDF|yellow] [[Ch6.pdf#page=8&selection=270,0,274,1&color=yellow|Ch6, p.8]]
> > Theorem 3.1 (Rolle). 
> 
> Rolle's theorem requires f to be on $[a,b]$ but differentiable on $(a,b)$ and finally $f(a) = f(b)$.

> [!PDF|note] [[Ch6.pdf#page=8&selection=329,0,332,1&color=note|Ch6, p.8]]
> > Theorem 3.2 (Extreme point has zero derivative).
> 
> Let's prove this

Let's say $f$ is defined on $I$, $x_{0} \in I$ and $f$ is differentiable at $x_{0}$. we suppose $f$ has a supremum at $x_{0}$, then there exists a $\delta$ such that for all $x \in I$, $\lvert x-x_{0} \rvert\leq \delta$, we have $$
f(x) \leq f(x_{0})
$$
then we have $$
\lim_{ h \to 0^+ } \frac{f(x_{0}+h)-f(x_{0})}{h} \leq 0
$$
and $$
\lim_{ h \to 0^- } \frac{f(x_{0}+h)-f(x_{0})}{h}  \geq 0
$$
> Note that $h <0$ .

And since $f$ is differentiable at $x_{0}$, we must have $$
\lim_{ h \to 0^+ } \frac{f(x_{0}+h)-f(x_{0})}{h} = \lim_{ h \to 0^- } \frac{f(x_{0}+h)-f(x_{0})}{h}  =0
		$$
If $x_{0}$ is the infimum point, then we just switch all the inequalities and the theorem still holds.

> [!PDF|yellow] [[Ch6.pdf#page=9&selection=250,0,292,1&color=yellow|Ch6, p.9]]
> > Theorem 3.4. If f : (a, b) → R is differentiable on (a, b) and f ′(x) = 0 for every a < x < b, then f is constant on (a, b).
> 
> The proof is basically try to find a $x_{0}$ that is not the constant value and use MVT to find some point $c$ that $f'(x) \neq 0$.

> [!PDF|yellow] [[Ch6.pdf#page=9&selection=485,0,583,23&color=yellow|Ch6, p.9]]
> > Theorem 3.5. Suppose that f : (a, b) → R is differentiable on (a, b). Then f is increasing if and only if f ′(x) ≥ 0 for every a < x < b, and decreasing if and only if f ′(x) ≤ 0 for every a < x < b. Furthermore, if f ′(x) > 0 for every a < x < b then f is strictly increasing, and if f ′(x) < 0 for every a < x < b then f is strictly decreasing.
> 
> You'll need MVT to strictly prove this.

> [!PDF|red] [[Ch6.pdf#page=10&selection=196,0,224,1&color=red|Ch6, p.10]]
> > Note that although f ′ > 0 implies that f is strictly increasing, f is strictly increasing does not imply that f ′ > 0.
> 
> We only have the $f' \to \uparrow$ side and we don't have the other direction

> [!PDF|yellow] [[Ch6.pdf#page=10&selection=316,0,317,1&color=yellow|Ch6, p.10]]
> > Example 3.2. 
> 
> 即使函数在某点的导数为正，如果导数在该点**不连续**，那么函数在该点附近**也不一定是严格递增的**，从而也**不一定存在局部反函数**。

> [!PDF|note] [[Ch6.pdf#page=10&selection=468,0,468,11&color=note|Ch6, p.10]]
> > Theorem 3.6
> 
> Here is the proof

Define $g(x) = f(x) - cx$, it's easy to see that $g$ is differentiable on $(a,b)$, then $g' =f'-c$ . Note that 
- $g'(x_{1}) = f'(x_{1})-c$
- $g'(x_{2}) = f'(x_{2})-c$
We suppose that $c \in(x_{1},x_{2})$, then we have $g'(x_{1})<0, g'(x_{2})>0$. Then by IVT, there exists a $x \in(x_{1},x_{2})$ such that $g'(x)=0$ i.e. $f'(x) =c$.

> [!PDF|yellow] [[Ch6.pdf#page=11&selection=32,0,190,1&color=yellow|Ch6, p.11]]
> > Proposition 4.1. Suppose that f : A → R is a one-to-one function on A ⊂ R with inverse f −1 : B → R where B = f (A). Assume that f is differentiable at an interior point c ∈ A and f −1 is differentiable at f (c), where f (c) is an interior point of B. Then f ′(c)̸ = 0 and f −1′ (f (c)) = 1 f ′(c) . (equivalent to f −1′ (y) = 1 f ′(f −1(y)) .)
> 
> 1. First, note that we need $f$ to be one-to-one function.
> 2. Then we need $f$ to be differentiable at $c$ and $f^{-1}$ be differentiable at $f(c)$
> 3. They're both interior points
> 

> [!PDF|yellow] [[Ch6.pdf#page=11&selection=366,0,368,20&color=yellow|Ch6, p.11]]
> > Theorem 4.1. (Inverse function). 
> 
> We need a few conditions here:
> 1. $f$ is $\mathbb{R} \to \mathbb{R}$
> 2. $f$ is differentiable in a neighborhood of $c$
> 3. $f'(c) \neq{0}$
> 4. $f'$ is continuous at $c$

> [!PDF|red] [[Ch6.pdf#page=11&selection=511,0,515,17&color=red|Ch6, p.11]]
> > Since we only consider local invertibility, we don’t need f to be one-to-one.
> 
> This is crucial!!

> [!PDF|red] [[Ch6.pdf#page=12&selection=91,1,104,23&color=red|Ch6, p.12]]
> >  |U : U → V is one-to-one and onto,
> 
> And later the local function $f|_{U}:U\to V$ is required to be one-to-one and onto.

> [!PDF|yellow] [[Ch6.pdf#page=13&selection=79,0,83,1&color=yellow|Ch6, p.13]]
> > Theorem 5.1 (Cauchy mean value). 
> 
> This one is strange and weird, you need to memorize this as like MVT but with 2 symmetric functions $f,g$. 

The proof of this is basically just construct a function $h$ that satisfies the Rolle's Theorem.

> [!PDF|yellow] [[Ch6.pdf#page=13&selection=320,0,440,2&color=yellow|Ch6, p.13]]
> > Theorem 5.2 (L’Hospital’s rule). Suppose that f, g : (a, b) → R are differentiable functions on a bounded open interval (a, b) such that g′(x)̸ = 0 for x ∈ (a, b) and lim x→a+ f (x) = 0, lim x→a+ g(x) = 0. Then lim x→a+ f ′(x) g′(x) = L implies that lim x→a+ f (x) g(x) = L.
> 
> Note that the traditional L'Hospital's rule is not directly the equal. It's from $\lim_{ x \to a^{+} } \frac{f'}{g'} = \lim_{ x \to a^{+}f } \frac{f}{g}$
> And we require the right derivative of $f$ and $g$ both exist

> [!PDF|yellow] [[Ch6.pdf#page=14&selection=517,0,534,1&color=yellow|Ch6, p.14]]
> > lim x→a+ |g(x)| = ∞.
> 
> This condition is to guarantee the origin limit won't be $\frac{\infty}{0}$

> [!PDF|yellow] [[Ch6.pdf#page=17&selection=421,0,471,9&color=yellow|Ch6, p.17]]
> > Theorem 6.1 (Taylor with Lagrange Remainder). Suppose that f : (a, b) → R has n + 1 derivatives on (a, b) and let a < c < b. For every a < x < b, there exists ξ between c and x such that
> 
> Note that we need the $f$ to have $n+1$ derivatives now.

The proof need 2 aux functions, $g$ as the residual and $h$ for the Rolle's Theorem. $$
h(t) = g(t)  - \left( \frac{x-t}{x-c}  \right)^{n+1}g(c)
$$
After the Rolle's theorem, we can easily get to the point.

> [!PDF|red] [[Ch6.pdf#page=20&selection=537,3,537,20&color=red|Ch6, p.20]]
> >  Critical points 
> 
> A new definition!




