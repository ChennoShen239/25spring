### Euler's Method
The problem is now $$
\frac{ \partial y }{ \partial t }  = f(t,y),t\in[a,b],y(a)= \alpha
$$
so what we do is to choose a positive integer $N$, and select **mesh points** (grid points)$$
t_{j} = a +  jh ,j=0,1,\dots,N
$$
where $h = \frac{b-a}{N}$.
![[Screenshot 2025-04-02 at 15.40.23.png]]

- For each $j$, do 2-term Taylor expansion $$
y(t_{j+1}) = y(t_{j}) + h y'(t_{j}) + \frac{h^{2}}{2}y''(\xi_{j})
$$
- since $y(t)$ satisfies the ODE, we then substitute it into $$
\underbrace{ y(t_{j+1}) }_{ w_{j+1} } = y(t_{j}) + hf(t_{j},\underbrace{ y(t_{j}) }_{ w_{j} })+\frac{h^{2}}{2}y''(\xi_{j})
$$
- ignore the error term, we set $w_{0}= \alpha$, so we have $$
w_{j+1} = w_{j} + hf(t_{j},w_{j}),j=0,1,2\dots,N-1
$$
 **Theorem**: suppose that in the initial value ODE $$
\frac{ \partial y }{ \partial t } = f(t,y),t\in[a,b],y(a)=\alpha
$$
- $f(t,y)$ is continuous
- $f(t,y)$ satisfies Lipschitz condition, i.e. $$
\left| f(t,y_{1})-f(t,y_{2}) \right| \leq L \left| y_{1}-y_{2} \right| ,D=[a,b] \times \mathbb{R}
$$then let $\left\{ w_{i} \right\}_{i=0}^{N}$ be the approximations generated by Euler's method for some positive integer $N$, then for each $j\leq N$, we have $$
\left| y(t_{j})-w_{j} \right| \leq \frac{hM}{2L} (\exp(L(t_{j}-a))-1)
$$where $M = \max_{t\in[a,b]}\left| y''(t) \right|$



**Good news**: the Euler's method indeed converges: $$
\lim_{  N\to \infty } \frac{hM}{2L} (\exp(L(t_{j}-a))-1) = 0
$$
**Bad news**: $N$ is likely too big for numerical convergence
**Worse**: Any numerical solution can be hopeless for chaotic solutions.

**Proof**: we mesh points as in the theorem
- for each $j$, we have 2-term Taylor expansion and then the euler's method $$
w_{j+1} = w_{j} + hf(t_{j},w_{j})
$$
- for the original expansion, we have $$
\underbrace{ y(t_{j+1}) }_{ w_{j+1} } = y(t_{j}) + hf(t_{j},\underbrace{ y(t_{j}) }_{ w_{j} })+\frac{h^{2}}{2}y''(\xi_{j})
$$
- then we subtract the 2, which gives $$
y(t_{j+1}) -w_{j+1} = y(t_{j}) -w_{j} +h[f(t_{j},y(t_{j}))-f(t_{j},w_{j})] + \frac{h^{2}}{2}y''(\xi_{j})
$$
 - by triangle inequality and Lipschitz condition, we have $$
\left| y-w \right| _{j+1} \leq \left| y-w \right|_{j} + hL\left| y-w \right| _{j} +\frac{h^{2}}{2}M
$$
- which can be further simplified to $$
\left| y-w \right| _{j+1} \leq \left| y-w \right| _{j}(1+hL) + \frac{h^{2}}{2}M
$$
- then recursively $$
\begin{aligned}
\underbrace{ |y(t_{j+1})-w_{j+1}|+\frac{hM}{2L} }_{ p_{j+1} }\leq\quad(1+hL)\left|y(t_j)-w_j\right|+\frac{h^2}{2}M+\frac{hM}{2L} \\
=\quad(1+hL)\left(\underbrace{ |y(t_j)-w_j|+\frac{hM}{2L} }_{ p_{j} }\right).
\end{aligned}
$$
i.e. $p_{j+1}\leq (1+hL)p_{j}$, then it's trivial to see $p_{j+1}\leq \left( 1+hL \right)^{j+1}p_{0} = \frac{\left( 1+hL \right)^{j+1}hM}{2L}$ , then $$
\left| y(t_{j+1})-w_{j+1} \right| \leq \underbrace{ \frac{hM}{2L} ((1+hL)^{j+1}-1) \leq \frac{hM}{2L}(\exp(L(t_{j+1}-a))-1) }_{ (j+1) \ln(1+hL) \leq (j+1)hL =L(t_{j+1}-a) }
$$
### Euler's method in finite precision
- still the same mesh points and the same expansion
- in Euler's method, we have $$
u_{j+1} = u_{j} +hf(t_{j},u_{j}) + \delta_{j+1}
$$ where $\left| \delta_{j+1} \right|\leq\delta$.
- do the subtraction $$
y(t_{j+1})-u_{j+1}=y(t_{j})-u_{j}+h\left(f(t_{j},y(t_{j}))-f(t_{j},u_{j})\right)+\frac{h^{2}}{2}y^{\prime\prime}(\xi_{j})-\delta_{j+1}.
$$
- so again we have the recursion $$
\begin{aligned}
|y(t_{j+1})-u_{j+1}| & \leq\left|y(t_j)–u_j\right|+h\left|f(t_j,y(t_j))–f(t_j,u_j)\right|+\frac{h^2}{2}\left|y^{\prime\prime}(\xi_j)\right|+\left|\delta_{j+1}\right| \\
 & \leq\quad\left|y(t_{j})-u_{j}\right|+hL\left|y(t_{j})-u_{j}\right|+\frac{h^{2}}{2}M+\delta
 \\
& =(1+hL)\left|y(t_{j})-u_{j}\right|+\frac{h^{2}}{2}M+\delta.
\end{aligned}
$$
- then by recursion, it's easy to see $$
\underbrace{ \left| y-u \right| _{j+1} +\frac{hM}{2L} + \frac{\delta}{hL} }_{ p_{j+1} } \leq \left(\underbrace{ \left| y-u \right| _{j} + \frac{hM}{2L} + \frac{\delta}{hL}  }_{ p_{j} }  \right) (1+hL)
$$
- the key is just to divide $hL$ to the remained terms 
- then we'll get the upper bound as $$
p_{j+1} \leq (1+hL)^{j+1} \left( \underbrace{ \delta }_{ \text{assume }\left| y-u \right| _{0}\leq\delta }+ \frac{hM}{2L} + \frac{\delta}{hL} \right)
$$
i.e. the error bound in finite precision $$
\left| y-u \right| _{j+1}  \leq \left( \delta + \frac{hM}{2L} + \frac{\delta}{hL} \right)(\exp(L(t_{j+1}-a))-1)
$$
**Optimal step size** $h$ for accuracy only : $$
h_{opt} = \sqrt{ \frac{2\delta}{M} } = O(\sqrt{ \delta })
$$
### Local truncation error for a general difference method
Still the Euler's method settings, the only difference is 
$$
w_{j+1} = w_{j} + h \phi(t_{j},w_{j})
$$
We define the truncation error as $$
\begin{align}
\tau_{j+1}(h)  & = \frac{y(t_{j+1})-(y(t_{j})+h\phi(t_{j},y(t_{j})))}{h} \\
 & = \frac{y(t_{j+1})-y(t_{j})}{h} - \phi(t_{j},y(t_{j}))
\end{align}
$$
then let's substitute $f$ back to $\phi$ again, then we'll get the **LTE** being $$
\tau_{j+1}(h) = \frac{y_{j+1}-y_{j}}{h} - \underbrace{ f(t_{j},y(t_{j})) }_{ y'(t_{j}) } = \frac{h}{2}y''(\xi_{j}),\xi_{j} \in(t_{j},t_{j+1})
$$
so this implies that $$
\left| \tau_{j+1}(h) \right| \leq \frac{h}{2} \max_{t\in[a,b]}\left| y''(t) \right | = \frac{hM}{2}
$$
which is a first order method.


### 2nd order Taylor method

$$\frac{dy}{dt} = f(t, y), \quad a \leq t \leq b, \quad y(a) = \alpha. \tag{1} $$


-  **3-term Taylor expansion**

$$
y(t_{j+1}) = y(t_j) + h y'(t_j) + \frac{h^2}{2} y''(t_j) + \frac{h^3}{3!} y^{(3)}(\xi_j) \tag{2}
$$

- **On the other hand, (1) implies in (2)**

$$
y'(t_j) = f(t_j, y(t_j)), \quad y''(t_j) = f'(t_j, y(t_j)) \tag{3}
$$

$$
\boxed{
\begin{aligned}
&\text{2-nd order Taylor method} \\
&w_0 = \alpha, \\
&w_{j+1} = w_j + h T^{(2)}(t_j, w_j), \quad j = 0, 1, \cdots, N - 1, \\
&\text{where} \quad T^{(2)}(t_j, w_j) = f(t_j, w_j) + \frac{h}{2} f'(t_j, w_j) \quad \text{\small nasty!}
\end{aligned}
}
$$
-  **$f'(t, y(t))$ is total derivative**

$$
\begin{aligned}
f'(t, y(t)) &= \frac{d}{dt} f(t, y(t)) \\
&= \frac{\partial f}{\partial t}(t, y(t)) + \frac{\partial f}{\partial y}(t, y(t)) \cdot y'(t) \\
&= \frac{\partial f}{\partial t}(t, y(t)) + \frac{\partial f}{\partial y}(t, y(t)) \cdot f(t, y(t)) \\
f'(t, w) &\coloneqq \frac{\partial f}{\partial t}(t, w) + \frac{\partial f}{\partial y}(t, w) \cdot f(t, w) \quad \text{⟵ two partial derivatives}
\end{aligned}
$$
- **But LTE is 2-nd order**

$$
\begin{aligned}
\tau_{j+1}(h) &\overset{\text{def}}{=} \frac{y(t_{j+1}) - y(t_j)}{h} - T^{(2)}(t_j, y(t_j)) \\
&\overset{(3)}{=} \frac{y(t_{j+1}) - y(t_j)}{h} - \left( y'(t_j) + \frac{h}{2} y''(t_j) \right) \\
&\overset{(2)}{=} \frac{h^{2}}{3!} y^{(3)}(\xi_j)
\end{aligned}
$$
> the key term here is we expand the 3rd order Taylor series, but for calculating truncation error we must divide a $h$ here, therefore making LTE 2nd order.
### Example 
Let $\frac{ \partial t }{ \partial y } =f(t,y)=y-t^{2}+1$, and $t\in[0,2],y(0)=0.5$
We then imply the 2nd order Taylor method as $$
w_{0}=0.5,w_{j+1}=w_{j}+h\mathrm{T}^{(2)}(t_{j},w_{j}),j=0,1,\dots ,N-1
$$
where $$
\mathrm{\mathbf{T}}^{(2)}(t_{j},w_{j})= f(t,w)+ \frac{h}{2}\left( \frac{ \partial f }{ \partial t } (t,w)+\frac{ \partial f }{ \partial y } (t,w)f(t,w)  \right)
$$
in this case, we have $$
\frac{ \partial f }{ \partial t }  = -2t,\frac{ \partial f }{ \partial y } =1
$$
so we have then $$
\mathrm{\mathbf{T}}^{(2)}(t,w)= (w-t^{2}+1) + \frac{h}{2} \left(-2t+(w-t^{2}+1)  \right) 
$$
and the recursive formula is now $$
\begin{align}
 w_{j+1}  & = w_{j}+ h\left( (w-t^{2}+1) + \frac{h}{2} \left(-2t+(w-t^{2}+1)  \right)  \right) \\
 & =\left( 1 + h + \frac{h^{2}}{2}  \right)w_{j} - \left( h + \frac{h^{2}}{2} \right)t_{j}^{2} -h^{2}t_{j} + h + \frac{h^{2}}{2}
\end{align}
$$

### *n*-th Order Taylor Methods:

$$
\frac{dy}{dt} = f(t, y), \quad a \leq t \leq b, \quad y(a) = \alpha. \tag{1}
$$
-  **$(n+1)$-term Taylor expansion**

$$
y(t_{j+1}) = y(t_j) + h y'(t_j) + \frac{h^2}{2} y''(t_j) + \cdots + \frac{h^n}{n!} y^{(n)}(t_j) + \frac{h^{n+1}}{(n+1)!} y^{(n+1)}(\xi_j) \tag{2}
$$
- **On the other hand, (1) implies in (2)**

$$
y'(t_j) = f(t_j, y(t_j)), \quad y''(t_j) = f'(t_j, y(t_j)), \quad y^{(n)}(t_j) = f^{(n-1)}(t_j, y(t_j)) \tag{3}
$$

$$
\boxed{
\begin{aligned}
&\text{n-th order Taylor method} \\
&w_0 = \alpha, \\
&w_{j+1} = w_j + h T^{(n)}(t_j, w_j), \quad j = 0, 1, \cdots \\
&\text{where} \quad T^{(n)}(t_j, w_j) = f(t_j, w_j) + \frac{h}{2} f'(t_j, w_j) + \cdots + \frac{h^{n-1}}{n!} f^{(n-1)}(t_j, w_j)
\end{aligned}
}
$$
-  **$f'(t, y(t)), \dots, f^{(n-1)}(t, y(t))$ are total derivatives** ⟵ *even more nasty*
- **But LTE is $n$-th order**

$$
\begin{aligned}
\tau_{j+1}(h) &\overset{\text{def}}{=} \frac{y(t_{j+1}) - y(t_j)}{h} - T^{(n)}(t_j, y(t_j)) \\
&\overset{(3)}{=} \frac{y(t_{j+1}) - y(t_j)}{h} - \left( y'(t_j) + \frac{h}{2} y''(t_j) + \cdots + \frac{h^{n-1}}{n!} y^{(n)}(t_j) \right) \\
&\overset{(2)}{=} \frac{h^{2}}{(n+1)!} y^{(n+1)}(\xi_j)
\end{aligned}
$$
> always lower 1 order than the Taylor expansion used.

### First order Taylor Expansion in 2 variables
Suppose that $f(t,y)$ and all its partial derivatives are continuous on $$
D= [a,b]\times[c,d]
$$
**Theorem**: Let $(t_{0},y_{0}) \in D$, $\Delta_{t } = t-t_{0},\Delta_{y}=y-y_{0}$,. Then $$
f(t,y) = P_{1}(t,y) + R_{1}(t,y)
$$
where for some $(\xi,\mu)\in D$: $$
\begin{align}
P_{1}(t,y)  & =f(t_{0},y_{0}) + \Delta_{t}\frac{ \partial f }{ \partial t } (t_{0},y_{0}) + \Delta_{y}\frac{ \partial f }{ \partial y } (t_{0},y_{0} ) \\
R_{1}(t,y) & = \frac{\Delta_{t}^{2}}{2}\frac{ \partial^{2} f }{ \partial t^{2}  }(\xi,\mu) + \Delta_{t}\Delta_{y} \frac{ \partial^{2}f }{ \partial t \partial y }  (\xi,\mu) + \frac{\Delta_{y}^{2}}{2}\frac{ \partial^{2}f }{ \partial y ^{2}  }(\xi,\mu) 
\end{align}
$$
**Reverse Theorem**:
$$
P_{1}(t,y) \approx f(t,y)
$$
### 2nd Order Runge-Kutta Method

$$
\frac{dy}{dt} = f(t, y), \quad a \leq t \leq b, \quad y(a) = \alpha.
$$

$$
\boxed{
\begin{aligned}
&\text{2-nd order Taylor method} \\
&w_0 = \alpha, \\
&w_{j+1} = w_j + h T^{(2)}(t_j, w_j), \quad j = 0, 1, \cdots, N - 1
\end{aligned}
}
$$
$$
\begin{aligned}
\text{where} \quad T^{(2)}(t, y) &= f(t, y) + \frac{h}{2} f'(t, y) \\&= f(t, y) + \frac{h}{2} \left( \frac{\partial f}{\partial t}(t, y) + \frac{\partial f}{\partial y}(t, y) \frac{dy}{dt} \right) \\
&= f(t, y) + \underbrace{ \frac{h}{2} \left( \frac{\partial f}{\partial t}(t, y) + \frac{\partial f}{\partial y}(t, y) f(t, y) \right) }_{ \left( \Delta_t = \frac{h}{2}, \ \Delta_y = \frac{h}{2} f(t, y) \right)  }
\\
&= f\left(t + \frac{h}{2}, \ y + \frac{h}{2} f(t, y) \right) - R_1\left(t + \frac{h}{2}, \ y + \frac{h}{2} f(t, y) \right)
\end{aligned}
$$

- **From first order Taylor expansion,**

$$
\begin{aligned}
R_1\left(t + \frac{h}{2}, y + \frac{h}{2} f(t, y) \right)
&= \frac{h^2}{8} \frac{\partial^2 f}{\partial t^2}(\xi, \mu)
+ \frac{h^2 f(t, y)}{4} \frac{\partial^2 f}{\partial t \partial y}(\xi, \mu)
+ \frac{h^2 f^2(t, y)}{8} \frac{\partial^2 f}{\partial y^2}(\xi, \mu) \\
&= \mathcal{O}(h^2)
\end{aligned}
$$
- **Method remains second order** after dropping 
$R_1\left(t + \frac{h}{2}, y + \frac{h}{2} f(t, y)\right)$

> Better just to memorize this

- **Only two function evaluations** to approximate $T^{(2)}(t_j, w_j)$
**In conclusion**: the 2-nd order Runge - Kutta method ( mid point method)
let $w_{0} = \alpha$, then recursively $$
w_{j+1}  = w_{j}  + hf\left( t_{j}+\frac{h}{2},w_{j}+ \frac{h}{2}f(t_{j},w_{j}) \right)
$$
> Remain second order
> 2 function evaluations per step
> No need for derivative calculations

Let's forget about those expansion things:
1. calculate $k_{1} = f(t_{j},w_{j})$
2. then calculate $k_{2} = f\left( t_{j}+ \frac{h}{2},w_{j} + \frac{h}{2} k_{1} \right)$
3. then finally the update is $$
w_{j+1} = w_{j} + hk_{2}
$$
### 3rd Order Runge-Kutta Method

$$
w_0 = \alpha; \quad \text{for } j = 0, 1, \cdots, N - 1,
$$
$$
\begin{align} 
w_{j+1}  & = w_j + \frac{h}{4} \left( f(t_j, w_j) + 3 f\left( t_j + \frac{2h}{3}, w_j + \frac{2h}{3} f\left( t_j + \frac{h}{3}, w_j + \frac{h}{3} f(t_j, w_j) \right) \right) \right) \\

 & \overset{\text{def}}{=} w_j + h \, \phi(t_j, w_j)
\end{align}

$$

> 📌 **3 function evaluations per step**

> Let's break this down so you can better get the idea behind this:

In this RK3 method:
1. $k_{1} = f(t_{j},w_{j})$
2. $k_{2} =f\left( t_{j}+\frac{h}{3} ,w_{j}+\frac{h}{3}k_{1}\right)$
3. $k_{3}=f\left( t_{j}+\frac{2}{3}h ,w_{j} + \frac{2}{3}hk_{2} \right)$
4. Then finally we update the $$w_{j+1} = w_{j } + \frac{h}{4}(k_{1}+3k_{3})$$
RK3 has an LTE of  $O(h^{3})$ 
### 4th Order Runge-Kutta Method (RK4)

$$
w_0 = \alpha; \quad \text{for } j = 0, 1, \cdots, N - 1,
$$

$$
\begin{aligned}
k_1 &=  f(t_j, w_j), \\
k_2 &=  f\left( t_j + \frac{h}{2}, w_j + \frac{h}{2} k_1 \right), \\
k_3 &=  f\left( t_j + \frac{h}{2}, w_j + \frac{h}{2} k_2 \right), \\
k_4 &=  f\left( t_j + h, w_j + hk_3 \right), \\
w_{j+1} &= w_j + \frac{h}{6} \left( k_1 + 2k_2 + 2k_3 + k_4 \right)
\end{aligned}
$$

> 📌 **4 function evaluations per step**

It's like we update the slope by $\frac{h}{2}k_{1}, \frac{h}{2}k_{2},hk_{3}$, then summarize as $$
\frac{h}{6} (k_{1} + 2k_{2}  + 2k_{3} + k_{4})
$$

### **Crying baby Principle** in adaptive algorithms

**More points in regions of inadequate accuracy**

#### **`crying babies get more candies`**

**Numerical accuracy adequate unless detected otherwise**
Lots of numerical inaccuracies _can_ go _undetected_.




### Adaptive Error Control
still the same setup
We consider a variable-step method with a well-chosen function $\phi(t,w,h)$: 
- $w_{0}=\alpha$
- for $j=0,1,\dots$:
	- choose step-size $h_{j} =t_{j+1}- t_{j}$	
	- set $w_{j+1} =w_{j}+h_{j}\phi(t_{j},w_{j},h_{j})$
> the key is to adaptively choose step-size to satisfy given tolerance

Given an **order-$n$** method:
- $w_{0}=\alpha$
- for $j=0,1,\dots$:$$
w_{j+1} = w_{j} + h \phi(t_{j},w_{j},h)
$$
- local truncation error (LTE)$$
\tau_{j+1} (h) = \underbrace{ \frac{y(t_{j+1})-y(t_{j})}{h} }_{ \text{real slope} }-\underbrace{ \phi(t_{j},y(t_{j}),h) }_{ \text{estimated slope} } = O(h^{n})
$$
> you can treat the LTE as the error to the slopes

- **Given tolerance** $\tau > 0$, we would like to estimate **largest** step-size $h$ for which
$$
|\tau_{j+1}(h)| \lesssim \tau.
$$
> **Approach:** Estimate $\tau_{j+1}(h)$ with **order-$(n + 1)$ method**
$$
\widetilde{w}_{j+1} = \widetilde{w}_j + h \, \widetilde{\phi}(t_j, \widetilde{w}_j, h), \quad \text{for } j \geq 0.
$$

- **Assume** $w_j \approx y(t_j), \quad \widetilde{w}_j \approx y(t_j)$  (only estimating **LTE**)
-  $\phi(t, w, h)$ is order-$n$ method

$$
\begin{align}
\tau_{j+1}(h)  \overset{\text{def}}{=}  & \frac{y(t_{j+1}) - y(t_j)}{h} - \phi(t_j, y(t_j), h) \\
 \overset{w_j \approx y(t_j)}{\approx}  & \frac{y(t_{j+1}) - \left(w_j + h \, \phi(t_j, w_j, h)\right)}{h} \\
= &  \frac{y(t_{j+1}) - w_{j+1}}{h} = \mathcal{O}(h^n)
\end{align}

$$

-  $\widetilde{\phi}(t, w, h)$ is order-$(n+1)$ method

$$
\begin{align}
\widetilde{\tau}_{j+1}(h) \overset{\text{def}}{=}  & \frac{y(t_{j+1}) - y(t_j)}{h} - \widetilde{\phi}(t_j, y(t_j), h) \\
\overset{\widetilde{w}_j \approx y(t_j)}{\approx}  & \frac{y(t_{j+1}) - \left(\widetilde{w}_j + h \, \widetilde{\phi}(t_j, \widetilde{w}_j, h)\right)}{h} \\
=  & \frac{y(t_{j+1}) - \widetilde{w}_{j+1}}{h} = \mathcal{O}(h^{n+1})
\end{align}

$$

- therefore:
	$$
\begin{aligned}
\tau_{j+1}(h) & \approx\quad\underbrace{ \frac{y(t_{j+1})-\widetilde{w}_{j+1}}{h} }_{ O(h^{n+1}) }+\frac{\widetilde{w}_{j+1}-w_{j+1}}{h} \\
 & =\quad O\left(h^{n+1}\right)+\frac{\widetilde{w}_{j+1}-w_{j+1}}{h}=O\left(h^n\right).
\end{aligned}
$$
**LTE estimate**: $$
\tau_{j+1}(h) \approx \frac{\tilde{w}_{j+1}-w_{j+1}}{h}
$$
### Step-size selection
Given this estimate, since $\tau_{j+1}(h) =O(h^{n})$, assume $$
\tau_{j+1}(h) \approx Kh^{n}
$$where $K$ is independent of $h$ 
- Assume LTE for new step-size $qh$ satisfies given tolerance $\epsilon$: $$
\lvert \tau_{j+1}(qh) \rvert \leq \epsilon
$$
- Our goal is to estimate $q$
- Assume LTE satisfies given tolerance $\epsilon$: $$
\lvert \tau_{j+1}(qh) \rvert \approx \lvert K(qh)^{n} \rvert \approx q^{n}\left\lvert  \frac{\tilde{w}_{j+1}-w_{j+1}}{h}  \right\rvert  \leq \epsilon
$$
- therefore the new step-size estimate is $$
qh \lesssim \left\lvert  \frac{\epsilon h}{\tilde{w}_{j+1}-w_{j+1}}  \right\rvert ^{1/n} h
$$
in other words: $$
qh\lesssim\left|\frac{\epsilon h}{\widetilde{w}_{j+1}-w_{j+1}}\right|^{\large\frac{1}{n}}h=\left|\frac{\epsilon}{\widetilde{\phi}\left(t_{j},w_{j},h\right)-\phi\left(t_{j},w_{j},h\right)}\right|^{\large\frac{1}{n}}h.


$$
### Runge–Kutta–Fehlberg: step-size selection procedure

>用两个不同阶数的方法（如 4 阶和 5 阶）计算同一个点，利用它们的差来估计误差，再据此动态调整步长。

1. **compute a conservative value for** $q$:
$$
q = \left| \frac{\epsilon h}{2 (\widetilde{w}_{j+1} - w_{j+1})} \right|^{\frac{1}{4}}
$$
2. **make restricted step-size change:**
$$
h =
\begin{cases}
0.1\, h, & \text{if } q \leq 0.1, \\
4\, h, & \text{if } q \geq 4.
\end{cases}
$$
3. **step-size can’t be too big:**

$$
h = \min(h, h_{\max})
$$
4. **step-size can’t be too small:**

$$
\textbf{if } \quad h < h_{\min} \quad \textbf{then} \quad \textit{declare failure}.
$$
|     步骤      |    目的     |
| :---------: | :-------: |
| 估计误差（两个解之差） |   获取误差量   |
| 构造比例因子 $q$  | 判断步长是否合适  |
|  限制步长变化范围   |  保证数值稳定性  |
|  限制最大最小步长   | 避免跳过/死循环  |
|   动态调整步长    | 提高效率、保证精度 |

```python
while t < T:
    # Step 1: compute both w and w_tilde
    w, w_tilde = rkf45_step(t, y, h)
    
    # Step 2: estimate error
    error = abs(w_tilde - w)
    
    # Step 3: compute q
    q = (epsilon * h / (2 * error)) ** 0.25
    
    # Step 4: check accept/reject
    if error < epsilon:
        # accept the step
        t += h
        y = w
    else:
        # reject the step
        pass
    
    # Step 5: update h
    if q <= 0.1:
        h = 0.1 * h
    elif q >= 4:
        h = 4 * h
    else:
        h = q * h
    
    # Step 6: enforce limits
    h = min(h, h_max)
    if h < h_min:
        raise Exception("Step size too small — method failed")

```