# MATH 104: MidTerm-1 Practice

## Exam Information

**Name**:  Cheney Gao

### Instructions

- You have 50 minutes to answer the questions.
- Use of electronic devices is not allowed. You can use one side of a cheat sheet.
- Answer the questions in the spaces provided on the question sheets. If you run out of room for an answer, continue on the back of the page.
- Only use results that have been stated in class, the textbook, or homework. In writing proofs, please indicate clearly which theorem, if any, is being used.
- In questions with multiple parts, to get partial credit, you can assume that you have solved the earlier parts if it helps with the subsequent parts.

### Points Allocation

| Question | Points | Score |
|----------|--------|-------|
| 1        | 10     |       |
| 2        | 10     |       |
| 3        | 10     |       |
| 4        | 20     |       |
| **Total** | **50** |       |

---

## Question 1 (10 points)

**Problem**: Suppose that $(x_n)$ is an increasing sequence with a convergent subsequence. Prove that $(x_n)$ is a convergent sequence.

**Answer**:

Assume the subsequence $\{x_{n_k}\}$ converges to the limit $c$. Then, for any $\epsilon > 0$, there exists $K > 0$ such that for any $k > K$:
$$
|x_{n_k} - c| \leq \epsilon. \quad \text{(2 points)}
$$

Since $(x_{n_k})$ is increasing, the above inequality implies:
$$
-\epsilon < x_{n_k} - c < 0. \quad \text{(2 points)}
$$

Also, when $n > n_K$, since $(x_n)$ is increasing, we have $x_{n_k} \leq x_n < c$, so:
$$
-\epsilon < x_{n_k} - c \leq x_n - c < 0, \quad \text{(2 points)}
$$
which implies:
$$
|x_n - c| \leq \epsilon. \quad \text{(2 points)}
$$

This proves:
$$
\lim_{n \to \infty} x_n = c. \quad \text{(2 points)}
$$

---

## Question 2 (10 points)

**Problem**: Given $x \in \mathbb{R}$, prove:
$$
\inf \{ n > x \mid n \in \mathbb{Z} \} \in \mathbb{Z}.
$$
**Hint**: You can use the following claim: For any $x \in \mathbb{R}$, there exists a unique $n \in \mathbb{Z}$ such that $x < n \leq 1 + x$.

**Answer**:

Let $n^*$ be the integer that satisfies $x < n^* \leq 1 + x$. We show $n^* = \min \{ n \mid n > x, n \in \mathbb{Z} \}$, thus $n^* = \inf \{ n \mid n > x, n \in \mathbb{Z} \}$. (2 points)

First, because $n^*$ is an integer and $n^* > x$, we have $n^* \in \{ n \mid n > x, n \in \mathbb{Z} \}$. (2 points)
> This is to show that $n^*$ is in the desired set

For any $n \in \{ n \mid n > x, n \in \mathbb{Z} \}$, since $n^*$ is the unique integer such that $x < n^* \leq 1 + x$, 
- if $n \leq x + 1$, then $n \leq n^*$ by uniqueness. 
- If $n > x + 1$, then $n > n^*$ since $n^* \leq x + 1$. 
- Thus, $n \geq n^*$. (4 points)

According to the definition of minimal elements, we have $n^* = \min \{ n \mid n > x, n \in \mathbb{Z} \}$, and **since the infimum of a set of integers that is bounded below is its minimum,** $n^* = \inf \{ n \mid n > x, n \in \mathbb{Z} \}$, which is an integer. (2 points)

---

## Question 3 (10 points)

**Problem**: Given a sequence $(x_n)$ and a finite number $x \in \mathbb{R}$, assume $x_n < x$ for all $n \in \mathbb{N}$ and $\limsup_{n \to \infty} x_n < x$. Prove: $\sup \{ x_n \mid n \in \mathbb{N} \} < x$.

**Answer**:

To prove $\sup \{ x_n \mid n \in \mathbb{N} \} < x$, it suffices to find an upper bound $M$ of $x_n$ such that $M < x$.

Let $y = \limsup_{n \to \infty} x_n$. Since $y < x$, choose an intermediate value $(y + x)/2$ such that $y < (y + x)/2 < x$. By the definition of $\limsup$, there exists $N_1 \in \mathbb{N}$ such that for all $n > N_1$:
$$
x_n < \frac{y + x}{2} < x. \quad \text{(4 points)}
$$

Define $M' = \max \{ x_1, x_2, x_3, \dots, x_{N_1} \}$. Since $x_n < x$ for all $n$, we have $M' < x$. (3 points)

Define:
$$
M = \max \left\{ x_1, x_2, x_3, \dots, x_{N_1}, \frac{y + x}{2} \right\} = \max \left[M', \frac{y+x}{2}\right]      
$$

Since $M' < x$ and $\frac{y + x}{2} < x$, we have $M < x$. Moreover, $M$ is an upper bound for $x_n$ because:
- For $n \leq N_1$, $x_n \leq M' \leq M$,
- For $n > N_1$, $x_n < (y + x)/2 \leq M$.

Thus, $M$ is an upper bound of $x_n$ and $M < x$, so $\sup \{ x_n \mid n \in \mathbb{N} \} \leq M < x$. This completes the proof. (3 points)

---
### **Part (a): Prove $x_n = 2^n - 3^{n-1}$ for $n \in \mathbb{N}$**

Use strong induction.  
- **Base cases**:  
  - $n = 1$: $x_1 = 1$, $2^1 - 3^{0} = 2 - 1 = 1$.  
  - $n = 2$: $x_2 = 1$, $2^2 - 3^{1} = 4 - 3 = 1$.  
- **Inductive hypothesis**: $x_m = 2^m - 3^{m-1}$ for $m \leq k$, $k \geq 2$.  
- **Inductive step**:  
  $$x_{k+1} = 5 x_k - 6 x_{k-1} = 5 (2^k - 3^{k-1}) - 6 (2^{k-1} - 3^{k-2}).$$

  Simplify: $5 \cdot 2^k - 6 \cdot 2^{k-1} = 2^{k+1}$, $-5 \cdot 3^{k-1} + 6 \cdot 3^{k-2} = -3^k$, so $x_{k+1} = 2^{k+1} - 3^k$.  
- **Conclusion**: By induction, $x_n = 2^n - 3^{n-1}$ for all $n \in \mathbb{N}$.

### **Part (b): Prove $\lim_{n \to \infty} x_n = -\infty$**

Rewrite: $x_n = 3^n \left( \left( \frac{2}{3} \right)^n - \frac{1}{3} \right)$. As $n \to \infty$, $\left( \frac{2}{3} \right)^n \to 0$, so $x_n \approx 3^n \cdot (-\frac{1}{3}) = -\frac{1}{3} \cdot 3^n \to -\infty$. For $M < 0$, choose $N > \log_3 (-3M)$; then for $n > N$, $x_n < M$, hence $\lim_{n \to \infty} x_n = -\infty$.