### Adaptive Error Control
Let's consider this $$
\frac{dy}{dt} = f(t,y(t)),t\in[a,b],y(a) = \alpha
$$
given tolerance $\epsilon$ and a method $\phi(t,w,h)$ so that $$
w_{j+1} = w_{j} + h_{j} \phi(t_{j},w_{j},h_{j})
		$$**we want to adaptively choose $h_j$ to satisfy $\epsilon$**
we only consider LTE $$
\tau_{j+1}(h) = \frac{y(t_{j+1})-y(t_{j})}{h} - \phi(t_{j},y(t_{j}),h) = O(h^{n})
$$
- estimate largest $h$ for which $$
\lvert \tau_{j+1}(h) \rvert \leq \epsilon
$$
## LTE Estimation

Assume (only for estimating LTE):  
$w_j \approx y(t_j), \quad \widetilde{w}_j \approx y(t_j)$ &nbsp;&nbsp;&nbsp;&nbsp;(1)

Let $\phi(t, w, h)$ be an order-$n$ method. The local truncation error (LTE) is defined as:
$$
\tau_{j+1}(h) \coloneqq \frac{y(t_{j+1}) - y(t_j)}{h} - \phi(t_j, y(t_j), h)
$$
Since $w_j \approx y(t_j)$, we have:
$$
\frac{y(t_{j+1}) - \left(w_j + h \phi(t_j, w_j, h)\right)}{h} = O(h^n)
$$

Let $\widetilde{\phi}(t, w, h)$ be an order-$(n+1)$ method. Then:
$$
\widetilde{\tau}_{j+1}(h) \coloneqq \frac{y(t_{j+1}) - y(t_j)}{h} - \widetilde{\phi}(t_j, y(t_j), h)
$$
$$
\frac{y(t_{j+1}) - \left(\widetilde{w}_j + h \widetilde{\phi}(t_j, \widetilde{w}_j, h)\right)}{h} = O(h^{n+1})
$$

Therefore, under assumption (1), we approximate:
$$
w_{j+1} \approx y(t_j) + h \phi(t_j, y(t_j), h)
$$

Hence,
$$
\tau_{j+1}(h) \approx \frac{y(t_{j+1}) - w_{j+1}}{h} = \frac{y(t_{j+1}) - \widetilde{w}_{j+1}}{h} + \frac{\widetilde{w}_{j+1} - w_{j+1}}{h}
$$
$$
= O(h^{n+1}) + O(h^n)
$$

**LTE estimate:**
$$
\tau_{j+1}(h) \approx \frac{\widetilde{w}_{j+1} - w_{j+1}}{h}
$$
## Step-Size Selection

**LTE estimate:**
$$
\tau_{j+1}(h) \approx \frac{\widetilde{w}_{j+1} - w_{j+1}}{h}
$$

Since $\tau_{j+1}(h) = O(h^n)$, assume
$$
\tau_{j+1}(h) \approx K h^n \quad \text{where } K \text{ is independent of } h.
$$

$K$ should satisfy:
$$
K h^n \approx \frac{\widetilde{w}_{j+1} - w_{j+1}}{h} \tag{1}
$$

Choose new step-size $q h$ so that the LTE satisfies a given tolerance $\epsilon$:
$$
\left|\tau_{j+1}(q h)\right| \leq \epsilon
$$

Equation (1) implies:
$$
\left|q^n \frac{\widetilde{w}_{j+1} - w_{j+1}}{h}\right| \approx \left|K (q h)^n\right| \approx \left|\tau_{j+1}(q h)\right| \lesssim \epsilon
$$

Thus, compute a **conservative** value for $q$:
$$
q = \left|\frac{\epsilon h}{2 \left(\widetilde{w}_{j+1} - w_{j+1}\right)}\right|^{\frac{1}{n}}
$$

Decision rule:
- If $q < 1$, reject the current $w_{j+1}$.
- If $q \geq 1$, accept it and set $j = j + 1$.

Make a **restricted step-size change**:
$$
h = \begin{cases}
0.1 h, & \text{if } q \leq 0.1, \\
4 h,   & \text{if } q \geq 4, \\
q h,   & \text{if } 0.1 < q < 4.
\end{cases}
$$

Additional constraints:
- Step-size can't be too big: $h = \min(h, h_{\max})$
- Step-size can't be too small:  
  If $h < h_{\min}$, then **declare failure**.

![[Pasted image 20250416152223.png]]
## §5.6 Multistep Methods

We consider the initial value problem:
$$
\frac{dy}{dt} = f(t, y), \quad a \leq t \leq b, \quad y(a) = \alpha.
$$
Choose a positive integer $N$, and define the mesh points:
$$
t_j = a + j h, \quad \text{for} \quad j = 0, 1, 2, \dots, N, \quad \text{where} \; h = \frac{b - a}{N}.
$$
For each $0 \leq j \leq N - 1$, integrate the ODE:
$$
y(t_{j+1}) - y(t_j) = \int_{t_j}^{t_{j+1}} \left( \frac{dy}{dt} \right) dt = \int_{t_j}^{t_{j+1}} f(t, y(t)) \, dt.
$$

We approximate the integral on the right-hand side using quadrature rules based on previously computed values of $f$:
- $f(t_{j+1}, y(t_{j+1}))$
- $f(t_j, y(t_j))$
- $f(t_{j-1}, y(t_{j-1}))$
- $\vdots$

## Examples: Constant Approximations

Assume we approximate $f(t, y(t))$ using a **constant value at the left endpoint**:
$$
f(t, y(t)) \approx f(t_j, y(t_j)),
$$
so
$$
y(t_{j+1}) - y(t_j) = \int_{t_j}^{t_{j+1}} f(t, y(t)) \, dt \approx h f(t_j, y(t_j)),
$$
which leads to **Euler's method (explicit)**:
$$
w_{j+1} = w_j + h f(t_j, w_j), \quad \text{for} \quad j = 0, 1, \dots
$$

Alternatively, approximate using the **right endpoint:**
$$
f(t, y(t)) \approx f(t_{j+1}, y(t_{j+1})),
$$
so
$$
y(t_{j+1}) - y(t_j) = \int_{t_j}^{t_{j+1}} f(t, y(t)) \, dt \approx h f(t_{j+1}, y(t_{j+1})),
$$
which gives the **backward Euler method (implicit)**:
$$
w_{j+1} = w_j + h f(t_{j+1}, w_{j+1}), \quad \text{for} \quad j = 0, 1, \dots
$$

Both are **first-order methods**, but the **implicit** one (backward Euler) generally requires solving a nonlinear equation at each step, making it **computationally more expensive**.
## Examples: Linear Approximations

Using the two points $f(t_j, y(t_j))$ and $f(t_{j-1}, y(t_{j-1}))$, approximate $f(t, y(t))$ linearly:
$$
f(t, y(t)) \approx \frac{(t - t_{j-1}) f(t_j, y(t_j)) + (t_j - t) f(t_{j-1}, y(t_{j-1}))}{h}
$$
![[output (2).png]]
>This is just to take the linear combination of $f(t_{j-1},y(t_{j-1}))$ and $f(t_{j},y(t_{j}))$


Then,
$$
y(t_{j+1}) - y(t_j) = \int_{t_j}^{t_{j+1}} f(t, y(t)) \, dt \approx \frac{h}{2} \left( 3f(t_j, y(t_j)) - f(t_{j-1}, y(t_{j-1})) \right)
$$

This leads to the **Adams-Bashforth two-step explicit method**:
$$
w_{j+1} = w_j + \frac{h}{2} \left( 3f(t_j, w_j) - f(t_{j-1}, w_{j-1}) \right), \quad \text{for } j = 1, 2, \dots
$$

---

Using the points $f(t_j, y(t_j))$ and $f(t_{j+1}, y(t_{j+1}))$, approximate $f(t, y(t))$ as:
$$
f(t, y(t)) \approx \frac{(t - t_j) f(t_{j+1}, y(t_{j+1})) + (t_{j+1} - t) f(t_j, y(t_j))}{h}
$$

Then,
$$
y(t_{j+1}) - y(t_j) = \int_{t_j}^{t_{j+1}} f(t, y(t)) \, dt \approx \frac{h}{2} \left( f(t_j, y(t_j)) + f(t_{j+1}, y(t_{j+1})) \right)
$$

This yields the **mid-point method (one-step implicit)**:
$$
w_{j+1} = w_j + \frac{h}{2} \left( f(t_j, w_j) + f(t_{j+1}, w_{j+1}) \right), \quad \text{for } j = 1, 2, \dots
$$
> This is different by using $t_{j+1}$ instead of $t_{j}$
---

Both are **second-order methods**, but the implicit method (mid-point) generally requires solving an equation at each step, making it **computationally more expensive**.

## $m$-th Order Methods

### Explicit $m$-step Method

Let $P(t)$ interpolate $f(t, y(t))$ at the points:
$$
f(t_j, y(t_j)),\quad f(t_{j-1}, y(t_{j-1})),\quad \dots,\quad f(t_{j-m+1}, y(t_{j-m+1}))
$$
Then,
$$
y(t_{j+1}) - y(t_j) = \int_{t_j}^{t_{j+1}} f(t, y(t))\, dt \approx \int_{t_j}^{t_{j+1}} P(t)\, dt
$$
defined as
$$
\int_{t_j}^{t_{j+1}} P(t)\, dt \coloneqq h\left( b_{m-1} f(t_j, y(t_j)) + b_{m-2} f(t_{j-1}, y(t_{j-1})) + \cdots + b_0 f(t_{j-m+1}, y(t_{j-m+1})) \right)
$$

This leads to the **explicit $m$-point method**, for $j = m-1, m, m+1, \dots$:
$$
w_{j+1} = w_j + h\left( b_{m-1} f(t_j, w_j) + b_{m-2} f(t_{j-1}, w_{j-1}) + \cdots + b_0 f(t_{j-m+1}, w_{j-m+1}) \right)
$$

---

### Implicit $(m-1)$-step Method

Let $P(t)$ interpolate $f(t, y(t))$ at the points:
$$
f(t_{j+1}, y(t_{j+1})),\quad f(t_j, y(t_j)),\quad \dots,\quad f(t_{j-m+2}, y(t_{j-m+2}))
$$

Then,
$$
y(t_{j+1}) - y(t_j) = \int_{t_j}^{t_{j+1}} f(t, y(t))\, dt \approx \int_{t_j}^{t_{j+1}} P(t)\, dt
$$
defined as
$$
\int_{t_j}^{t_{j+1}} P(t)\, dt \coloneqq h\left( b_m f(t_{j+1}, y(t_{j+1})) + b_{m-1} f(t_j, y(t_j)) + \cdots + b_0 f(t_{j-m+2}, y(t_{j-m+2})) \right)
$$

This leads to the **implicit $(m-1)$-point method**, for $j = m-1, m, m+1, \dots$:
$$
w_{j+1} = w_j + h\left( b_{m} f(t_{j+1}, w_{j+1}) + b_{m-1} f(t_j, w_j) + b_{m-2} f(t_{j-1}, w_{j-1}) + \cdots + b_0 f(t_{j-m+2}, w_{j-m+2}) \right)
$$

---
###  4th-order Adams-Bashforth Method (explicit, 4-step)

$$
w_{j+1} = w_j + \frac{h}{24} \left( 55 f(t_j, w_j) - 59 f(t_{j-1}, w_{j-1}) + 37 f(t_{j-2}, w_{j-2}) - 9 f(t_{j-3}, w_{j-3}) \right)
$$
### 隐式：4阶 Adams-Moulton 方法（隐式 3 步）

$$

w_{j+1} = w_j + \frac{h}{24} \left( 9 f_{j+1} + 19 f_j - 5 f_{j-1} + f_{j-2} \right)

$$

含 $f_{j+1} = f(t_{j+1}, w_{j+1})$，需解方程。

> **显式法**更快但更容易发散，**隐式法**更稳但每步都要多解一个（可能是非线性）方程。

## $m$-th Order Methods and Local Truncation Error (LTE)

### Explicit $m$-step Method

Let $P(t)$ interpolate $f(t, y(t))$ at the points:
$$
f(t_j, y(t_j)),\quad f(t_{j-1}, y(t_{j-1})),\quad \dots,\quad f(t_{j-m+1}, y(t_{j-m+1}))
$$

Then,
$$
f(t, y(t)) = P(t) + R(t)
$$
with the remainder term:
$$
R(t) = \frac{f^{(m)}(\xi_t, y(\xi_t))}{m!} \prod_{k=j-m+1}^{j} (t - t_k)
$$
>In total $m$ terms

Integrating from $t_j$ to $t_{j+1}$:
$$
y(t_{j+1}) - y(t_j) = \int_{t_j}^{t_{j+1}} (P(t) + R(t)) \, dt
$$
Define the quadrature approximation:
$$
= h \left( b_{m-1} f(t_j, y(t_j)) + b_{m-2} f(t_{j-1}, y(t_{j-1})) + \cdots + b_0 f(t_{j-m+1}, y(t_{j-m+1})) \right) + \int_{t_j}^{t_{j+1}} R(t) \, dt
$$

The local truncation error (LTE) is defined as:
$$
\tau_{j+1}(h) = \frac{1}{h} \int_{t_j}^{t_{j+1}} R(t) \, dt
$$
which gives
$$
\tau_{j+1}(h) = \frac{1}{m! \, h} \int_{t_j}^{t_{j+1}} f^{(m)}(\xi_t, y(\xi_t)) \prod_{k=j-m+1}^{j} (t - t_k) \, dt
$$
From the textbook simplification:
$$
\tau_{j+1}(h) = \frac{f^{(m)}(\xi, y(\xi))}{m! \, h} \int_{t_j}^{t_{j+1}} \prod_{k=j-m+1}^{j} (t - t_k) \, dt
$$

---

### Implicit $(m-1)$-step Method

Let $P(t)$ interpolate $f(t, y(t))$ at the points:
$$
f(t_{j+1}, y(t_{j+1})),\quad f(t_j, y(t_j)),\quad \dots,\quad f(t_{j-m+2}, y(t_{j-m+2}))
$$

Then,
$$
f(t, y(t)) = P(t) + R(t)
$$
with
$$
R(t) = \frac{f^{(m)}(\xi_t, y(\xi_t))}{m!} \prod_{k=j-m+2}^{j+1} (t - t_k)
$$

Integrating from $t_j$ to $t_{j+1}$:
$$
y(t_{j+1}) - y(t_j) = \int_{t_j}^{t_{j+1}} (P(t) + R(t)) \, dt
$$
Define the quadrature approximation:
$$
= h \left( b_{m-1} f(t_{j+1}, y(t_{j+1})) + b_{m-2} f(t_j, y(t_j)) + \cdots + b_0 f(t_{j-m+2}, y(t_{j-m+2})) \right) + \int_{t_j}^{t_{j+1}} R(t) \, dt
$$

The local truncation error (LTE) is:
$$
\tau_{j+1}(h) = \frac{1}{h} \int_{t_j}^{t_{j+1}} R(t) \, dt
$$
which gives
$$
\tau_{j+1}(h) = \frac{1}{m! \, h} \int_{t_j}^{t_{j+1}} f^{(m)}(\xi_t, y(\xi_t)) \prod_{k=j-m+2}^{j+1} (t - t_k) \, dt
$$
Simplified:
$$
\tau_{j+1}(h) = \frac{f^{(m)}(\xi, y(\xi))}{m! \, h} \int_{t_j}^{t_{j+1}} \prod_{k=j-m+2}^{j+1} (t - t_k) \, dt
$$
## 4th-order Methods

### 4th-order Adams-Bashforth Method (explicit, 4-step)

The update formula is:
$$
w_{j+1} = w_j + \frac{h}{24} \left( 55f(t_j, w_j) - 59f(t_{j-1}, w_{j-1}) + 37f(t_{j-2}, w_{j-2}) - 9f(t_{j-3}, w_{j-3}) \right)
$$

### 4th-order Adams-Moulton Method (implicit, 3-step)

The update formula is:
$$
w_{j+1} = w_j + \frac{h}{24} \left( 9f(t_{j+1}, w_{j+1}) + 19f(t_j, w_j) - 5f(t_{j-1}, w_{j-1}) + f(t_{j-2}, w_{j-2}) \right)
$$

---

### Local Truncation Error (LTE)

#### Adams-Bashforth

The local truncation error is defined as:
$$
\tau_{j+1}(h) = \frac{f^{(4)}(\xi, y(\xi))}{4! \, h} \int_{t_j}^{t_{j+1}} \prod_{k=j-3}^j (t - t_k) \, dt
$$

Change of variable $t = s + t_j$, so $t_k = t_j - (j - k)h$, and the integral becomes:
$$
= \frac{f^{(4)}(\xi, y(\xi))}{4! \, h} \int_0^h s (s + h) (s + 2h) (s + 3h) \, ds
$$
which evaluates to:
$$
= \boxed{\frac{251}{720}} f^{(4)}(\xi, y(\xi)) \, h^4
$$

#### Adams-Moulton

The local truncation error is:
$$
\tau_{j+1}(h) = \frac{f^{(4)}(\xi, y(\xi))}{4! \, h} \int_{t_j}^{t_{j+1}} \prod_{k=j-2}^{j+1} (t - t_k) \, dt
$$

Using change of variable $t = s + t_j$, the integral becomes:
$$
= \frac{f^{(4)}(\xi, y(\xi))}{4! \, h} \int_0^h (s - h) s (s + h) (s + 2h) \, ds
$$
which evaluates to:
$$
= -\boxed{\frac{19}{720}} f^{(4)}(\xi, y(\xi)) \, h^4
$$
## §5.7 Predictor-Corrector Methods

### 4th-order Adams-Bashforth Method (explicit, less accurate)

$$
w_{j+1} = w_j + \frac{h}{24} \left( 55f(t_j, w_j) - 59f(t_{j-1}, w_{j-1}) + 37f(t_{j-2}, w_{j-2}) - 9f(t_{j-3}, w_{j-3}) \right)
$$

### 4th-order Adams-Moulton Method (implicit, more accurate)

$$
w_{j+1} = w_j + \frac{h}{24} \left( 9f(t_{j+1}, w_{j+1}) + 19f(t_j, w_j) - 5f(t_{j-1}, w_{j-1}) + f(t_{j-2}, w_{j-2}) \right)
$$

---

### Predictor-Corrector (PC) Scheme

**Definition:**
$$
\text{Adams4PC} \coloneqq \text{One fixed-point iteration on Moulton, with Bashforth initial guess}
$$

**Initialization:** Use 3 steps of the 4th-order Runge-Kutta method to obtain $w_0, w_1, w_2, w_3$.

---

### Adams-Bashforth Predictor

Predict a preliminary value $w_{j+1}^{\text{p}}$ using the explicit method:
$$
w_{j+1}^\text{p} \coloneqq w_j + \frac{h}{24} \left( 55f(t_j, w_j) - 59f(t_{j-1}, w_{j-1}) + 37f(t_{j-2}, w_{j-2}) - 9f(t_{j-3}, w_{j-3}) \right)
$$

### Adams-Moulton Corrector

Correct using the predicted value $w_{j+1}^\text{p}$ in the implicit formula:
$$
w_{j+1} \coloneqq w_j + \frac{h}{24} \left( 9f(t_{j+1}, w_{j+1}^\text{p}) + 19f(t_j, w_j) - 5f(t_{j-1}, w_{j-1}) + f(t_{j-2}, w_{j-2}) \right)
$$
预测-修正法是一种结合了**显式方法的计算效率**与**隐式方法的高精度**的策略。它的核心思想是：

> 用一个“预测器”（显式方法）先估算解的下一步值，再用一个“修正器”（隐式方法）对该预测值进行修正。

1. 先用 Adams-Bashforth 做预测，得 $w_{j+1}^{\text{p}}$；
2. 用预测值代入 Adams-Moulton，得到修正后的 $w_{j+1}$；
3. 更新数据，继续迭代。

```matlab
function adams4pc_demo()
    % 参数设置
    f = @(t, y) -y + sin(t);         % 可更换为任意 f(t, y)
    y0 = 1;                          % 初始值
    t0 = 0; t_end = 10;              % 时间区间
    N = 100;                         % 网格点数
    h = (t_end - t0) / N;

    % 初始化变量
    t = t0:h:t_end;
    w = zeros(1, N+1);
    w(1) = y0;

    % 用 RK4 初始化前三步
    for j = 1:3
        k1 = f(t(j), w(j));
        k2 = f(t(j) + h/2, w(j) + h*k1/2);
        k3 = f(t(j) + h/2, w(j) + h*k2/2);
        k4 = f(t(j) + h, w(j) + h*k3);
        w(j+1) = w(j) + h*(k1 + 2*k2 + 2*k3 + k4)/6;
    end

    % Adams4 Predictor-Corrector
    for j = 4:N
        % predictor: Adams-Bashforth 4-step
        fp = f(t(j), w(j));
        f1 = f(t(j-1), w(j-1));
        f2 = f(t(j-2), w(j-2));
        f3 = f(t(j-3), w(j-3));
        wp = w(j) + h/24 * (55*fp - 59*f1 + 37*f2 - 9*f3);   % predictor

        % corrector: Adams-Moulton 3-step (one fixed-point iteration)
        f_corr = f(t(j+1), wp);
        w(j+1) = w(j) + h/24 * (9*f_corr + 19*fp - 5*f1 + f2); % corrector
    end

    % 可视化结果
    plot(t, w, 'b.-', 'LineWidth', 1.2);
    hold on;
    y_true = @(t) (3/2)*exp(-t) + 0.5*(sin(t) - cos(t)); % 精确解（仅本例）
    plot(t, y_true(t), 'r--', 'LineWidth', 1);
    legend('Adams4PC 解', '精确解');
    xlabel('t'); ylabel('y');
    title('Adams-Bashforth-Moulton Predictor-Corrector 方法');
    grid on;
end

```
![[untitled.jpg]]
## Adaptive Error Control (I)

Consider the initial value problem:
$$
\frac{dy}{dt} = f(t, y(t)), \quad a \leq t \leq b, \quad y(a) = \alpha
$$

We use a **variable-step method** based on the **Adams-Bashforth-Moulton predictor-corrector (Adams4PC)** method.

### Assumptions

- A tolerance $\tau > 0$ is given.
- The numerical solution satisfies: $w_i \approx y(t_i)$ for all $i \leq j$.

### Goal

Ensure that the **local truncation error (LTE)** remains below the tolerance:
$$
|\tau_{j+1}(h_{j+1})| \lesssim \tau
$$

### Approach

For each time step $j = 0, 1, \dots$:

1. **Runge-Kutta Initialization**  
   Use a fixed-step **4th-order Runge-Kutta** method initially or *whenever the step-size is reset.*

2. **Step-size Adjustment**  
   Reset the step-size $h_j = t_{j+1} - t_j$ based on the estimated LTE and the given tolerance $\tau$.

3. **Prediction-Correction**  
   Compute $w_{j+1}$ using the **Adams4PC method**, i.e.,
	   - Predict with Adams-Bashforth,
	   - Correct with Adams-Moulton using the predicted value,
	   - Optionally adjust $h$ if error is too large or small.

## Adaptive Error Control (II)

We use both the **4th-order Adams-Bashforth method** (predictor) and the **4th-order Adams-Moulton method** (corrector) to estimate the local truncation error (LTE), which in turn guides adaptive step-size control.

### 4th-order Adams-Bashforth Predictor

$$
w_{j+1}^{\mathrm{p}} = w_j + \frac{h}{24} \left( 55f(t_j, w_j) - 59f(t_{j-1}, w_{j-1}) + 37f(t_{j-2}, w_{j-2}) - 9f(t_{j-3}, w_{j-3}) \right)
$$

This predictor approximates the true solution with:
$$
w_{j+1}^{\mathrm{p}} \approx y_{j+1} - \frac{251}{720} f^{(4)}(\xi, y(\xi)) h^5
$$

### 4th-order Adams-Moulton Corrector

$$
w_{j+1} = w_j + \frac{h}{24} \left( 9f(t_{j+1}, w_{j+1}^{\mathrm{p}}) + 19f(t_j, w_j) - 5f(t_{j-1}, w_{j-1}) + f(t_{j-2}, w_{j-2}) \right)
$$

This corrector approximates the true solution with:
$$
w_{j+1} \approx y_{j+1} + \frac{19}{720} f^{(4)}(\widetilde{\xi}, y(\widetilde{\xi})) h^5
$$

### Error Estimation via Difference

Assuming
$$
h^5 f^{(4)}(\xi, y(\xi)) \approx h^5 f^{(4)}(\widetilde{\xi}, y(\widetilde{\xi}))
$$

We estimate the error using the difference between corrector and predictor:
$$
\frac{w_{j+1} - w_{j+1}^{\mathrm{p}}}{h} \approx \frac{270}{720} f^{(4)}(\widetilde{\xi}, y(\widetilde{\xi})) h^4
$$

So:
$$
\frac{19}{720} f^{(4)}(\widetilde{\xi}, y(\widetilde{\xi})) h^4 \approx \frac{19}{270} \cdot \frac{w_{j+1} - w_{j+1}^{\mathrm{p}}}{h}
$$

### Final Approximation of LTE

Hence, the local truncation error is approximated by:
$$
\tau_{j+1}(h) = \frac{y_{j+1} - w_{j+1}}{h} \approx -\frac{19}{270} \cdot \frac{w_{j+1} - w_{j+1}^{\mathrm{p}}}{h}
$$

## Step-size Selection

We use the LTE estimate derived from Adams4PC:

$$
\tau_{j+1}(h) = \frac{y_{j+1} - w_{j+1}}{h} \approx -\frac{19}{270} \cdot \frac{w_{j+1} - w_{j+1}^{\text{p}}}{h}
$$

Since the local truncation error is of order $O(h^4)$, we assume:
$$
\tau_{j+1}(h) \approx K h^4 \quad \text{where } K \text{ is independent of } h.
$$

From the expression above, $K$ approximately satisfies:
$$
K h^4 \approx -\frac{19}{270} \cdot \frac{w_{j+1} - w_{j+1}^{\text{p}}}{h} \tag{1}
$$

---

### Goal

Select a new step-size $q h$ such that:
$$
|\tau_{j+1}(q h)| \leq \epsilon
$$

Substituting Equation (1) into this inequality gives:
$$
\left|q^4 \cdot \frac{19}{270} \cdot \frac{w_{j+1} - w_{j+1}^{\text{p}}}{h}\right| \approx |K (q h)^4| \lesssim \epsilon
$$

---

### Compute a conservative step-size scaling factor:

$$
q = 1.5 \left( \frac{\epsilon h}{|w_{j+1} - w_{j+1}^{\text{p}}|} \right)^{\frac{1}{4}}
$$

Decision rule:

- If $q < 1$, **reject** the current step and recompute;
- If $q \geq 1$, **accept** the current value and proceed with $j \gets j + 1$.

---

### Apply a restricted step-size update:

$$
h =
\begin{cases}
\max(q, 0.1) \cdot h, & \text{if } q < 1 \\
\min(q, 4) \cdot h, & \text{if } q > 2 \\
h, & \text{if } 1 \leq q \leq 2
\end{cases}
$$
![[output (3).png]]
Apply hard bounds to ensure numerical safety:

- Maximum step-size: $h = \min(h, h_{\text{max}})$  
- Minimum step-size: if $h < h_{\text{min}}$, then **declare failure** and stop integration.

---

> 💡 **Note**  
> This is analogous to adaptive control in embedded Runge-Kutta methods.  
> **PLEASE HANDLE WITH CARE — fragile — THANK YOU.**

## Multistep vs. Runge-Kutta

- **Multistep methods are cheaper** than Runge-Kutta.  
  They reuse previously computed function values and require fewer evaluations per step.

- **Multistep methods require Runge-Kutta** for *every* step-size change.  
  Because they rely on multiple past values, a step-size change invalidates the previous history, and a **single-step method** like Runge-Kutta must be used to reinitialize.

---

**`OdeDemo`**: Matlab code available on *bcourses* for running different ODE solvers.

## §5.9 Predator and Prey Model

### Notation

- $x\overset{\text{def}}{=}$ prey population  
- $y \overset{\text{def}}{=}$ predator population

### Dynamics (Lotka–Volterra equations)

$$
\begin{aligned}
x' &= \alpha x - \beta x y \\
y' &= -\gamma y + \delta x y
\end{aligned}
$$

### Interpretation

- Prey population $x$ increases when **alone**, decreases when predator $y$ is present.
- Predator population $y$ **increases** when prey $x$ is available, **decreases** **without** prey.

---
## System of ODEs

We begin with a single initial value problem:

### Single ODE:
$$
\frac{dy}{dt} = f(t, y), \quad a \leq t \leq b, \quad y(a) = \alpha
$$

---
### Generalization: System of $m$ First-Order ODEs

We now consider a system:
$$
\frac{du_1}{dt} = f_1(t, u_1, u_2, \dots, u_m),
$$
$$
\frac{du_2}{dt} = f_2(t, u_1, u_2, \dots, u_m),
$$
$$
\vdots
$$
$$
\frac{du_m}{dt} = f_m(t, u_1, u_2, \dots, u_m), \quad a \leq t \leq b
$$

Each equation is coupled to the others through the variables $u_1, u_2, \dots, u_m$.

---

### Initial Conditions:

To solve the system, we require $m$ initial conditions:
$$
u_1(a) = \alpha_1, \quad u_2(a) = \alpha_2, \quad \dots, \quad u_m(a) = \alpha_m
$$

## Systems of ODEs in Vector Form

We define the vector of dependent variables:
$$
\mathbf{u} \overset{\text{def}}{=} 
\begin{pmatrix}
u_1 \\
u_2 \\
\vdots \\
u_m
\end{pmatrix}, 
\quad
\boldsymbol{\alpha} \overset{\text{def}}{=}
\begin{pmatrix}
\alpha_1 \\
\alpha_2 \\
\vdots \\
\alpha_m
\end{pmatrix}
$$

---

## Higher-Order ODEs as First-Order Systems

Consider a single $m$-th order ODE:
$$
y^{(m)} = f(t, y, y', \dots, y^{(m-1)}), \quad a \leq t \leq b \tag{3}
$$

with initial conditions:
$$
y(a) = \alpha, \quad y'(a) = \alpha', \quad \dots, \quad y^{(m-1)}(a) = \alpha^{(m-1)} \tag{4}
$$

---

### The "Magic" Reduction:

We convert this higher-order equation into a system of first-order equations.

Define:
$$
\mathbf{u} =
\begin{pmatrix}
u_1 \\
u_2 \\
\vdots \\
u_m
\end{pmatrix}
\overset{\text{def}}{=}
\begin{pmatrix}
y \\
y' \\
\vdots \\
y^{(m-1)}
\end{pmatrix}, 
\quad
\boldsymbol{\alpha} =
\begin{pmatrix}
\alpha \\
\alpha' \\
\vdots \\
\alpha^{(m-1)}
\end{pmatrix}
$$

Then the system becomes:
$$
\frac{d\mathbf{u}}{dt} = \mathbf{f}(t, \mathbf{u}), \quad a \leq t \leq b \tag{1}
$$

with initial condition:
$$
\mathbf{u}(a) = \boldsymbol{\alpha} \tag{2}
$$

Specifically,
$$
\frac{d\mathbf{u}}{dt} =
\begin{pmatrix}
y' \\
y'' \\
\vdots \\
y^{(m)}
\end{pmatrix}
=
\begin{pmatrix}
u_2 \\
u_3 \\
\vdots \\
f(t, u_1, u_2, \dots, u_{m})
\end{pmatrix}
=
\mathbf{f}(t, \mathbf{u})
$$

Thus:
$$
\mathbf{u}(a) = \boldsymbol{\alpha}
$$

---

## Conclusion

>**Every higher-order ODE can be rewritten as a first-order ODE system.**  

## Example: Rewriting a Second-Order ODE System as a First-Order System

We begin with a second-order system of coupled ODEs:
$$
\begin{aligned}
x'' &= \alpha y - \beta x y \\
y'' &= -\gamma x + \delta x y
\end{aligned}
$$

---

### Define the state vector:

We reduce this to a first-order system by defining a 4-dimensional vector:
$$
\mathbf{u} \overset{\text{def}}{=} 
\begin{pmatrix}
u_1 \\
u_2 \\
u_3 \\
u_4
\end{pmatrix}
\equiv
\begin{pmatrix}
x \\
x' \\
y \\
y'
\end{pmatrix}
$$

---

### Compute the derivative $\dfrac{d\mathbf{u}}{dt}$:

Taking the time derivative:
$$
\frac{d\mathbf{u}}{dt} =
\begin{pmatrix}
x' \\
x'' \\
y' \\
y''
\end{pmatrix}
=
\begin{pmatrix}
u_2 \\
\alpha u_3 - \beta u_1 u_3 \\
u_4 \\
-\gamma u_1 + \delta u_1 u_3
\end{pmatrix}
\overset{\text{def}}{=} \mathbf{f}(t, \mathbf{u})
$$

---
## Vector Lipschitz Condition (I)

### Definition

Let the function $f(t, \mathbf{u})$ be defined for:
$$
\mathbf{u} =
\begin{pmatrix}
u_1 \\
u_2 \\
\vdots \\
u_m
\end{pmatrix}
\in \mathbb{R}^m
$$

on the domain:
$$
\mathcal{D} \overset{\text{def}}{=}
\left\{ (t, \mathbf{u}) \,\middle|\, a \leq t \leq b,\quad -\infty < u_j < \infty,\quad 1 \leq j \leq m \right\}
$$

We say that **$f$ satisfies a Lipschitz condition** on $\mathcal{D}$ if there exists a constant $L > 0$ such that:
$$
\left| f(t, \mathbf{u}) - f(t, \mathbf{z}) \right| \leq L \sum_{j=1}^{m} \left| u_j - z_j \right|
$$

for all vectors:
$$
\mathbf{z} =
\begin{pmatrix}
z_1 \\
z_2 \\
\vdots \\
z_m
\end{pmatrix}
\quad \text{and} \quad
(t, \mathbf{u}), (t, \mathbf{z}) \in \mathcal{D}
$$

---
## Vector Lipschitz Condition (II) and Existence Theorem

### Domain Definition

We consider a domain:
$$
\mathcal{D} \overset{\text{def}}{=}
\left\{ (t, \mathbf{u}) \,\middle|\, a \leq t \leq b, \; -\infty < u_j < \infty, \; 1 \leq j \leq m \right\}
$$

### System of First-Order ODEs

Let $\mathbf{u}(t)$ be a vector of $m$ unknown functions governed by:
$$
\frac{d\mathbf{u}}{dt} = \mathbf{f}(t, \mathbf{u}), \quad a \leq t \leq b, \quad \text{with} \quad \mathbf{u}(a) = \boldsymbol{\alpha}
$$

---

### Theorem (Existence and Uniqueness)

Suppose that for each component $f_j(t, \mathbf{u})$, the function satisfies a **Lipschitz condition** with constant $L$ on $\mathcal{D}$, i.e.,
$$
\left| \frac{\partial f}{\partial u_j}(t, \mathbf{u}) \right| \leq L, \quad \text{for } j = 1, 2, \dots, m
$$

Then the initial value problem:
$$
\frac{d\mathbf{u}}{dt} = \mathbf{f}(t, \mathbf{u}), \quad \mathbf{u}(a) = \boldsymbol{\alpha}
$$
has a **unique solution** $\mathbf{u}(t)$ for all $t \in [a, b]$.

---

### Remarks

- This is a **sufficient condition** for uniqueness, derived from **Picard-Lindelöf theorem**.
- In practice, verifying the **boundedness of partial derivatives** is often easier than checking the full Lipschitz inequality.

## Scalar vs. Vector ODE Methods: Identical Runge-Kutta Form

We begin with the standard scalar initial value problem:
$$
\frac{dy}{dt} = f(t, y), \quad a \leq t \leq b, \quad y(a) = \alpha
$$

This generalizes to the vector-valued initial value problem:
$$
\frac{d\mathbf{u}}{dt} = \mathbf{f}(t, \mathbf{u}), \quad a \leq t \leq b, \quad \mathbf{u}(a) = \alpha
$$

---
### 4th-Order Runge-Kutta for Scalar or Vector ODEs

In both the scalar and vector cases, the **Runge-Kutta method of order 4** takes the same **form**:
#### Initialization
$$
\mathbf{w}_0 = \alpha
$$
#### Iteration (for $j = 0, 1, \dots$):
$$
\begin{aligned}
\mathbf{k}_1 &= h \mathbf{f}(t_j, \mathbf{w}_j) \\
\mathbf{k}_2 &= h \mathbf{f}\left(t_j + \frac{h}{2}, \mathbf{w}_j + \frac{1}{2} \mathbf{k}_1 \right) \\
\mathbf{k}_3 &= h \mathbf{f}\left(t_j + \frac{h}{2}, \mathbf{w}_j + \frac{1}{2} \mathbf{k}_2 \right) \\
\mathbf{k}_4 &= h \mathbf{f}(t_{j+1}, \mathbf{w}_j + \mathbf{k}_3) \\
\mathbf{w}_{j+1} &= \mathbf{w}_j + \frac{1}{6} \left( \mathbf{k}_1 + 2\mathbf{k}_2 + 2\mathbf{k}_3 + \mathbf{k}_4 \right)
\end{aligned}
$$

---

### Key Insight

> **Identical appearance!**  
> Whether you're solving a scalar equation or a system (vector equation), the 4th-order Runge-Kutta algorithm **looks exactly the same** — only the data type of $\mathbf{f}$ and $\mathbf{w}_j$ changes (scalar vs. vector).

## Example: Lotka–Volterra Predator-Prey Model

### ODE System

The model describes interactions between prey $x(t)$ and predator $y(t)$:
$$
\begin{aligned}
x' &= x - 0.01 \cdot x y \\
y' &= -y + 0.02 \cdot x y
\end{aligned}
$$

- Prey $x$ grows exponentially when left alone.
- Predator $y$ declines without prey.
- Interaction terms $\pm xy$ couple their dynamics.

```matlab
[t, y] = ode45(@lotka, [0, 40], [2, 1]); % initial: x=2, y=1
```
![[combined_log_plots.png]]
## §5.10 Stability Analysis for One-Step Methods

We consider the scalar initial value problem:
$$
\frac{dy}{dt} = f(t, y), \quad a \leq t \leq b, \quad y(a) = \alpha
$$

---

### One-Step Method

The general form of a one-step numerical method is:
- Initialization:  
  $$
  w_0 = \alpha
  $$
- Iteration for $j = 0, 1, 2, \dots$:
  $$
  w_{j+1} = w_j + h \cdot \phi(t_j, w_j, h)
  $$

Here, $\phi(t_j, w_j, h)$ is the numerical approximation to $f(t_j, y(t_j))$.

---

### Local Truncation Error (LTE)

The local truncation error at step $j$ is defined by:
$$
\tau_j(h) = \frac{y(t_{j+1}) - y(t_j)}{h} - \phi(t_j, y(t_j), h)
$$

This measures how well the method approximates the differential equation over a **single step**, assuming **exact data input**.

---

### Definition: Consistency

A method is said to be **consistent** if:
$$
\lim_{h \to 0} \max_{0 \leq j \leq N} |\tau_j(h)| = 0, \quad \text{with } x_j = a + jh
$$

That is, the local error vanishes uniformly as the step-size $h \to 0$.

Consistency is the **least requirement** for a method to be valid for solving ODEs.

---

### Definition: Convergence

A numerical method is **convergent** if:
$$
\lim_{h \to 0} \max_{0 \leq j \leq N} |y(t_j) - w_j| = 0
$$

That is, the **numerical solution** $w_j$ approaches the **true solution** $y(t_j)$ uniformly as $h \to 0$ over the interval $[a, b]$.

> ✅ Consistency + Stability ⇒ Convergence (Lax equivalence principle for ODEs)

## Review: Convergence Analysis for Euler Method

### Initial Value Problem
$$
\frac{dy}{dt} = f(t, y), \quad a \leq t \leq b, \quad y(a) = \alpha \tag{1}
$$

---

### Euler Method
Let $h = \frac{b - a}{N}$, $t_j = a + jh$, and define:
$$
w_0 = \alpha, \quad w_{j+1} = w_j + h f(t_j, w_j)
$$
This corresponds to $\phi(t_j, w_j, h) = f(t_j, w_j)$.

---
### Local Truncation Error (LTE)
$$
|\tau_j(h)| = \left| \frac{y(t_{j+1}) - y(t_j)}{h} - f(t_j, y(t_j)) \right|
= \frac{h}{2} \left| \frac{df}{dt}(\tilde{t}_j, y(\tilde{t}_j)) \right| \xrightarrow{h \to 0} 0
$$

→ **Euler method is consistent**.

---

### Theorem I: Convergence

Assume:
- $f(t, y)$ is continuous,
- Lipschitz in $y$:
  $$
  |f(t, y_1) - f(t, y_2)| \leq L |y_1 - y_2|
  $$

Then for $j = 0, 1, \dots, N$:
$$
|y(t_j) - w_j| \leq \frac{h M}{2L} \left(e^{L(t_j - a)} - 1\right) \xrightarrow{h \to 0} 0
$$

where $M = \max_{t \in [a, b]} |y''(t)|$.

→ **Euler method is convergent**.

---

### Definition: Well-posedness

An ODE is **well-posed** if:
- A unique solution exists,
- Small changes to ODE → small changes to solution.

**Theorem II**: If $f$ satisfies Theorem I, then problem (1) is well-posed.

---

### Definition: Stability (Numerical)

A numerical method is **stable** if:
- Small changes in data or model → small changes in computed solution.

## **Theorem**: Stability and Convergence of One-Step Methods

### Initial Value Problem
$$
\frac{dy}{dt} = f(t, y), \quad a \leq t \leq b, \quad y(a) = \alpha
$$

---

### One-Step Method
Let $w_0 = \alpha$ and iterate:
$$
w_{j+1} = w_j + h \cdot \phi(t_j, w_j, h), \quad j = 0, 1, \dots
$$

---

### Assumptions
Assume the function $\phi(t, w, h)$ satisfies:
- $\phi$ is continuous on the domain$$
  \mathcal{D} \overset{\text{def}}{=} \left\{ (t, w, h) \,\middle|\, a \leq t \leq b, \; -\infty < w < \infty, \; 0 < h < h_0 \right\}
  $$
- $\phi$ is Lipschitz in $w$ with constant $L > 0$ (uniformly in $h$), for $0 < h < h_0$

---

### Then:
- The method is **stable** (small perturbations lead to small deviations)
- The method is **convergent ⇔ consistent**, and consistency means:
  $$
  \phi(t, y, 0) = f(t, y), \quad \text{for all } a \leq t \leq b
  $$

---

### Error Bound
Define the local truncation error maximum:
$$
\tau(h) \overset{\text{def}}{=} \max_{0 \leq j \leq N} |\tau_j(h)|
$$

Then the **global error** satisfies:
$$
|y(t_j) - w_j| \leq \frac{\tau(h)}{L} \cdot e^{L(t_j - a)}
$$

> ✅ This shows:  
> Consistency + Lipschitz ⇒ Convergence (with exponential error growth in $t$)

## Example: Modified Euler's Method and Lipschitz Constant

Assume the scalar IVP:
$$
\frac{dy}{dt} = f(t, y), \quad y(a) = \alpha, \quad \text{and} \quad \left| \frac{\partial f}{\partial y} \right| \leq \widehat{L}
$$

---

### Modified Euler’s Method (a 2nd-order Runge-Kutta method)
Initialize:
$$
w_0 = \alpha
$$

Iterate for $j = 0, 1, \dots$:
$$
w_{j+1} = w_j + \frac{h}{2} \left[ f(t_j, w_j) + f(t_{j+1}, w_j + h f(t_j, w_j)) \right]
$$
>remember this function form!

---

### Corresponding One-Step Function $\phi$

Define:
$$
\phi(t, w, h) = \frac{1}{2} \left[ f(t, w) + f(t + h, w + h f(t, w)) \right]
$$

Now compare two values $w$ and $\widehat{w}$:
$$
\begin{aligned}
\phi(t, w, h) - \phi(t, \widehat{w}, h) 
&= \frac{1}{2} \left[ f(t, w) - f(t, \widehat{w}) \right] \\
& + \frac{1}{2} \left[ f(t + h, w + h f(t, w)) - f(t + h, \widehat{w} + h f(t, \widehat{w})) \right]
\end{aligned}
$$

---

### Lipschitz Estimate

Using the assumption $|\partial f / \partial y| \leq \widehat{L}$:

$$
|\phi(t, w, h) - \phi(t, \widehat{w}, h)| 
\leq \frac{\widehat{L}}{2} |w - \widehat{w}| 
+ \frac{\widehat{L}}{2} \left| w + h f(t, w) - \widehat{w} - h f(t, \widehat{w}) \right|
$$

Now estimate the second term:
$$
\left| w + h f(t, w) - \widehat{w} - h f(t, \widehat{w}) \right| 
\leq |w - \widehat{w}| + h \widehat{L} |w - \widehat{w}|
= (1 + h \widehat{L}) |w - \widehat{w}|
$$

Thus:
$$
|\phi(t, w, h) - \phi(t, \widehat{w}, h)| 
\leq \left( \widehat{L} + \frac{1}{2} h \widehat{L}^2 \right) |w - \widehat{w}| 
\overset{\text{def}}{=} L |w - \widehat{w}|
$$

1. **写出差值公式**：先写出 $\phi$ 的差值：
$$

\phi(t, w, h) - \phi(t, \widehat{w}, h) =

\frac{1}{2} \left[ f(t, w) - f(t, \widehat{w}) \right]

+ \frac{1}{2} \left[ f(t+h, w + h f(t, w)) - f(t+h, \widehat{w} + h f(t, \widehat{w})) \right]

$$
	我们希望估计它的模长，即：
$$

|\phi(t, w, h) - \phi(t, \widehat{w}, h)|

\leq \frac{1}{2} \left| f(t, w) - f(t, \widehat{w}) \right|

+ \frac{1}{2} \left| f(t+h, w + h f(t, w)) - f(t+h, \widehat{w} + h f(t, \widehat{w})) \right|

$$

2. **使用 Lipschitz 假设**：你假设对所有 $t$，$f$ 对 $y$ 是 Lipschitz 的，即：
$$

\left| f(t, y_1) - f(t, y_2) \right| \leq \widehat{L} |y_1 - y_2|

$$
	于是：
	- 第一项直接使用 Lipschitz 条件：
	$$
	
	\left| f(t, w) - f(t, \widehat{w}) \right| \leq \widehat{L} |w - \widehat{w}|
	
	$$
	- 第二项中的 $f(t+h, \cdot)$ 对它的参数也是 Lipschitz，因此：
$$

\left| f(t+h, w + h f(t, w)) - f(t+h, \widehat{w} + h f(t, \widehat{w})) \right|

\leq \widehat{L} \left| w + h f(t, w) - \widehat{w} - h f(t, \widehat{w}) \right|

$$
3. **代入两个估计**，你得到：
$$

|\phi(t, w, h) - \phi(t, \widehat{w}, h)|

\leq \frac{\widehat{L}}{2} |w - \widehat{w}|

+ \frac{\widehat{L}}{2} \left| w + h f(t, w) - \widehat{w} - h f(t, \widehat{w}) \right|

$$
---
### Conclusion

> ✅ Modified Euler’s method satisfies a **Lipschitz condition in $w$**,  
> with step-size–dependent constant $L = \widehat{L} + \frac{1}{2} h \widehat{L}^2$.

## Stability Analysis: Multistep Methods (I)

### Initial Value Problem

$$
\frac{dy}{dt} = f(t, y), \quad a \leq t \leq b, \quad y(a) = \alpha
$$

---

### General Multistep Method

Given initial values:
$$
w_0 = \alpha, \quad w_1 = \alpha_1, \dots, \quad w_{m-1} = \alpha_{m-1}
$$

Then for $j = m-1, m, m+1, \dots$:
$$
\begin{aligned}
w_{j+1} &= a_{m-1} w_j + a_{m-2} w_{j-1} + \cdots + a_0 w_{j+1-m} \\
&+ h F(t_j, w_{j+1}, w_j, \dots, w_{j+1-m}), \quad x_j = a + jh
\end{aligned}
$$

---

### Local Truncation Error (LTE)

Defined as:
$$
\tau_{j+1}(h) \overset{\text{def}}{=} 
\frac{1}{h} \left[ y(t_{j+1}) - \sum_{k=0}^{m-1} a_k y(t_{j+1 - (m - k)}) \right]
- F(t_j, y(t_{j+1}), \dots, y(t_{j+1 - m}))
$$

---

### Assumptions on $F$

- If $f \equiv 0$ $⇒$ $F \equiv 0$
- Lipschitz in all arguments:
  $$
  \left| F(t_j, u_{j+1}, \dots, u_{j+1 - m}) 
  - F(t_j, \widehat{u}_{j+1}, \dots, \widehat{u}_{j+1 - m}) \right| 
  \leq L \sum_{k=0}^m |u_{j+1 - k} - \widehat{u}_{j+1 - k}|
  $$

---

## Stability Analysis: Multistep Methods (II)

### Definition: Consistency

A multistep method is **consistent** if:
$$
\lim_{h \to 0} \max_{m \leq j \leq N} |\tau_j(h)| = 0
\quad \text{and} \quad 
\lim_{h \to 0} \max_{0 \leq j \leq m-1} |y(t_j) - \alpha_j| = 0
$$

---

### Definition: Convergence

A multistep method is **convergent** if:
$$
\lim_{h \to 0} \max_{0 \leq j \leq N} |y(t_j) - w_j| = 0
$$

> ✅ Both conditions resemble the single-step case.  
> ⚠️ But **stability** will be very different and a much bigger issue in multistep methods.

---

## Stability Analysis: Multistep Methods (III)

### Constant Solution Test

Consider the special case:
$$
\frac{dy}{dt} = f(t, y) = 0, \quad \text{so } y(t) \equiv \alpha
$$

Apply the multistep method:
$$
w_{j+1} = a_{m-1} w_j + a_{m-2} w_{j-1} + \cdots + a_0 w_{j+1 - m}, \quad \text{since } F \equiv 0
$$

---

### Minimum Requirements for Stability

Assume:
$$
\alpha = \alpha_1 = \dots = \alpha_{m-1}
$$

Then the method must satisfy:
- $w_j \equiv \alpha$ for all $j$ (constant solution preserved),
- $w_j$ remains **close to** $\alpha$ in finite precision arithmetic

> ✅ These are the **minimum stability conditions**.
> **最小稳定条件确保：当真实解是常数时，多步法必须也能稳定地维持常数解。**

这既是对多步法最基本的**正确性**要求，也为后续更强的稳定性条件（如根条件）打下基础。

## Finite Recurrence Relations

---

### General Recurrence Setup

Given initial values:
$$
w_0 = \alpha_0, \quad w_1 = \alpha_1, \dots, \quad w_{m-1} = \alpha_{m-1}
$$

A linear $m$-step recurrence relation:
$$
w_{j+1} = a_{m-1} w_j + a_{m-2} w_{j-1} + \cdots + a_0 w_{j+1 - m} \tag{1}
$$

---

### Characteristic Polynomial

Assume a geometric solution $w_j = \mu^j$, i.e.,
$$
\frac{w_{j+1}}{w_j} = \lambda \Rightarrow \mu = \lambda
$$

Substitute into (1), yields the **characteristic polynomial**:
$$
P(\mu) = \mu^m - (a_{m-1} \mu^{m-1} + a_{m-2} \mu^{m-2} + \cdots + a_0)
$$

> ✅ For the constant solution $w_j \equiv 1$ to satisfy (1), we must have $P(1) = 0$.

---

### General Solution (Distinct Roots)

If $P(\mu)$ has $m$ distinct roots $\mu_1, \dots, \mu_m$, the general solution is:
$$
w_j = c_1 \mu_1^j + c_2 \mu_2^j + \cdots + c_m \mu_m^j, \quad j = 0, 1, \dots
$$

The constants $c_1, \dots, c_m$ are determined by the initial conditions:
$$
w_0, w_1, \dots, w_{m-1}
$$

---

## Examples

---

### Example 1: Distinct Roots

Given:
$$
w_{j+1} = 3w_j - 2w_{j-1}, \quad m = 2
$$

Characteristic polynomial:
$$
P(\mu) = \mu^2 - 3\mu + 2 = (\mu - 1)(\mu - 2)
$$

General solution:
$$
w_j = c_1 + c_2 \cdot 2^j
$$

Solve constants from:
$$
w_0 = c_1 + c_2, \quad w_1 = c_1 + 2c_2 \\
\Rightarrow \quad c_2 = w_1 - w_0, \quad c_1 = 2w_0 - w_1
$$

---

### Example 2: Repeated Roots

Given:
$$
w_{j+1} = 2w_j - w_{j-1}, \quad m = 2
$$

Characteristic polynomial:
$$
P(\mu) = \mu^2 - 2\mu + 1 = (\mu - 1)^2
$$

General solution:
$$
w_j = c_1 + j c_2
$$

Determine constants from:
$$
w_0 = c_1, \quad w_1 = c_1 + c_2 \Rightarrow c_2 = w_1 - w_0
$$
## Root Conditions

Consider a multistep method with initial values:
$$
w_0 = \alpha, \quad w_1 = \alpha_1, \quad \dots, \quad w_{m-1} = \alpha_{m-1}
$$

For $j = m - 1, m, m + 1, \dots$, the method updates via:
$$
\begin{aligned}
w_{j+1} &= a_{m-1} w_j + a_{m-2} w_{j-1} + \cdots + a_0 w_{j+1 - m} \\
&\quad + h F(t_j, w_{j+1}, w_j, \dots, w_{j+1 - m})
\end{aligned}
$$

The corresponding characteristic polynomial is:
$$
P(\mu) = \mu^m - \left(a_{m-1} \mu^{m-1} + a_{m-2} \mu^{m-2} + \cdots + a_0\right)
$$

---

### Root Condition

A multistep method is **zero-stable** if every root $\mu_i$ of $P(\mu)$ satisfies:
$$
|\mu_i| \leq 1
$$

---

### Classification of Stability

Assuming the root condition holds:

- **Strongly stable**:  
  $\mu = 1$ is a root of $P(\mu)$ and it is the **only** root on the unit circle (i.e., $|\mu| = 1$).

- **Weakly stable**:  
  $P(\mu)$ has **more than one** distinct root with $|\mu| = 1$.

- **Unstable**:  
  Any root $\mu_i$ of $P(\mu)$ satisfies $|\mu_i| > 1$.

---

### Stability Implications

>Strong stability implies the method resists numerical growth due to roundoff or perturbations.  

>Weak stability may lead to **numerical oscillations** in the presence of rounding errors.  

>Violating the root condition implies **instability** and divergence.

## Convergence Theorem for Multistep Methods

Consider the initial value problem:
$$
\frac{dy}{dt} = f(t, y), \quad a \leq t \leq b, \quad y(a) = \alpha
$$

Assume the multistep method is defined with:
$$
w_0 = \alpha, \quad w_1 = \alpha_1, \quad \dots, \quad w_{m-1} = \alpha_{m-1}
$$

and for $j = m - 1, m, m + 1, \dots$:
$$
\begin{aligned}
w_{j+1} &= a_{m-1} w_j + a_{m-2} w_{j-1} + \cdots + a_0 w_{j+1 - m} \\
&\quad + h F(t_j, w_{j+1}, w_j, \dots, w_{j+1 - m})
\end{aligned}
$$

---

### Theorem

If the method is **consistent**, then the following are equivalent:

- The method is **stable**
- The method satisfies the **root condition**
- The method is **convergent**

## Example: Fourth-Order Methods

---

### 4-Step Adams–Bashforth Method

Update formula:
$$
w_{j+1} = w_j + h \cdot F(t_j, w_j, w_{j-1}, w_{j-2}, w_{j-3})
$$

where:
$$
F(t_j, w_j, w_{j-1}, w_{j-2}, w_{j-3}) =
\frac{h}{24} \left( 55f(t_j, w_j) - 59f(t_{j-1}, w_{j-1}) + 37f(t_{j-2}, w_{j-2}) - 9f(t_{j-3}, w_{j-3}) \right)
$$

---

### 4-Step Milne's Method

Update formula:
$$
w_{j+1} = w_{j-3} + h \cdot \widehat{F}(t_j, w_j, w_{j-1}, w_{j-2}, w_{j-3})
$$

where:
$$
\widehat{F}(t_j, w_j, w_{j-1}, w_{j-2}, w_{j-3}) =
\frac{4h}{3} \left( 2f(t_j, w_j) - f(t_{j-1}, w_{j-1}) + 2f(t_{j-2}, w_{j-2}) \right)
$$

---

### Root Conditions

#### 4-Step Adams–Bashforth

Characteristic polynomial:
$$
P(\mu) = \mu^4 - \mu^3 = \mu^3(\mu - 1)
$$

Roots of $P(\mu)$: $0, 0, 0, 1$

- Satisfies root condition
- **Strongly stable**: only one root on unit circle

---

#### Milne's Method

Characteristic polynomial:
$$
P(\mu) = \mu^4 - 1 = (\mu - 1)(\mu + 1)(\mu - \sqrt{-1})(\mu + \sqrt{-1})
$$

Roots of $P(\mu)$: $\pm 1$, $\pm i$

- Satisfies root condition
- **Weakly stable**: all roots lie on unit circle
---

我们考虑一个通用的 $m$ 步法，其递推公式如下：

$$

w_{j+1} = a_{m-1} w_j + a_{m-2} w_{j-1} + \cdots + a_0 w_{j+1 - m} + h F(\cdots)

$$

在分析稳定性时，我们忽略右边的 $h F(\cdots)$，也就是忽略非齐次项，只看**齐次递推关系**：

$$

w_{j+1} = a_{m-1} w_j + a_{m-2} w_{j-1} + \cdots + a_0 w_{j+1 - m}

$$

我们假设解是指数形式 $w_j = \mu^j$，带入递推关系中：

$$

\mu^{j+1} = a_{m-1} \mu^j + a_{m-2} \mu^{j-1} + \cdots + a_0 \mu^{j+1 - m}

$$

两边除以 $\mu^{j+1}$ 得：

$$

1 = a_{m-1} \mu^{-1} + a_{m-2} \mu^{-2} + \cdots + a_0 \mu^{-m}

$$

再乘回 $\mu^m$ 得到所谓的**特征多项式**：

$$

P(\mu) = \mu^m - a_{m-1} \mu^{m-1} - \cdots - a_0

$$

---

## ✅ 例子1：4步 Adams–Bashforth 方法

它的公式为：
$$

w_{j+1} = w_j + \frac{h}{24} \left(55 f_j - 59 f_{j-1} + 37 f_{j-2} - 9 f_{j-3}\right)

$$

注意，更新只用到了 $w_j$，其他项是函数 $f$ 的组合，不影响齐次递推的系数。所以对应的齐次关系其实就是：
$$

w_{j+1} = w_j

$$

但这是一个 4 步法，所以我们默认其他项的系数为 0，即：
$$

w_{j+1} = 1 \cdot w_j + 0 \cdot w_{j-1} + 0 \cdot w_{j-2} + 0 \cdot w_{j-3}

$$

对应特征多项式：

$$

P(\mu) = \mu^4 - \mu^3 = \mu^3(\mu - 1)

$$

其根为：$0, 0, 0, 1$

满足根条件（模长 $\leq 1$），只有一个在单位圆上，**强稳定**。

---

## ✅ 例子2：4步 Milne 方法

Milne 方法形式为：
$$

w_{j+1} = w_{j-3} + \text{(function terms)}

$$
即只与 $w_{j-3}$ 有直接关系，其他的 $w_j, w_{j-1}, w_{j-2}$ 只出现在 $f$ 中，不参与线性组合。因此齐次递推关系为：

$$

w_{j+1} = w_{j-3}

$$写成标准形式：

$$

w_{j+1} - w_{j-3} = 0

$$
出特征多项式：

$$

P(\mu) = \mu^4 - 1 = (\mu - 1)(\mu + 1)(\mu - i)(\mu + i)

$$

其根为：$\pm 1, \pm i$，都在单位圆上

**弱稳定**（模长 = 1 的根不唯一）
![[characteristic_roots_latex_highres.png]]