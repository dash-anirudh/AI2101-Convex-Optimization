# Convex Optimization Assignment 1 Solutions

## General Instructions

The following document contains the solutions to the questions for Assignment 1. Please note that the solutions provided may not be the only possible way to solve the questions. They indicate only one of the many (possibly) valid solutions. The solutions provided are relatively crisp and do not include all the steps that you must have. Your solution should be logical and contain all supporting arguments. Feel free to contact any of the TAs via email in case of any discrepancy you find in the solutions provided.

## Question 1

There's only 3 possible cases in the Bisection Search Method, for a unimodal function with a minima. 
#### Case 1: 
Considering $f'(x)=0$ In this case, $x^{(k)}=x^*$ 

#### Case 2:
Considering $f'(x)>0$. If the slope is greater than zero, the point $x^{(k)}$ must lie to the right of the minima $x^*$. The search space is reduced to $\left[l^{(k)}, x^{(k)}\right)$. Now, $x^{(k+1)}=\displaystyle \frac{l^{(k)} + x^{(k)}}{2}$

#### Case 3:
Considering $f'(x)<0$. If the slope is lesser than zero, the point $x^{(k)}$ must lie to the left of the minima $x^*$. The search space is reduced to $\left[x^{(k)}, r^{(k)}\right)$. Now, $x^{(k+1)}=\displaystyle\frac{r^k + x^k}{2}$

Thus, at the $k^{th}$ iteration, either $x^{(k)}=x^*$, or the search space reduces by a factor of $2$ for the next iteration. In fact, after $k$ steps, the search space has been reduced by a factor of $2^k$. Thus, the width of the search space after $k$ iterations, if the original width search space was $\left(r^{(0)}-l^{(0)}\right)=c$  ,which is finite according to the initial condition of the algorithm, is given by:

$$
\begin{align*}
w^{(k)} &= \frac{c}{2^k} \\
\lim_{{k \to \infty}} w^{(k)} &= \lim_{{k \to \infty}}\left(\frac{c}{2^k}\right) = 0
\end{align*}
$$

Therefore, $x^{(k)}$ eventually converges to $x^*$.

## Question 2

Let the initial interval's size be $w^{(0)}$

In Golden Section Search, the size of the interval after the first iteration i.e. $w^{(1)}$ is given by,

$$
\begin{align*}
    w^{(1)} &= w^{(0)} - \rho w^{(0)} \\
     &= (1 - \rho)w^{(0)}
\end{align*}
$$

Similarly, after the second iteration, the size of the interval i.e. $w^{(2)}$ is given by,

$$
\begin{align*}
    w^{(2)} &= (1 - \rho)w^{(0)}\\
    &= (1 - \rho)(1 - \rho)w^{(0)}\\
    &= (1 - \rho)^2w^{(0)}
\end{align*}
$$

So, after the $k^{th}$ iteration, the size of the interval i.e $w^{(k)}$ is given by,

$$
\begin{align*}
    w^{(k)} &= (1 - \rho)^kw^{(0)}
\end{align*}
$$

So, the size of the interval during the $k^{th}$ iteration decreases by,

$$
\begin{align*}
    \Delta_k &= w^{(k-1)}-w^{(k)}\\
    &=(1-\rho)^{k-1}w^{(0)}-(1-\rho)^kw^{(0)}\\
    &=(1-\rho)^{k-1}w^{(0)}[1-(1-\rho)]\\
    &=\rho(1-\rho)^{k-1}w^{(0)}
\end{align*}
$$

Thus, in the $k^{th}$ iteration the size of the initial interval i.e $w_0$ decreases by a factor of $\rho(1-\rho)^{k-1} \approx (0.382)(0.618)^{k-1}$.

## Question 3
Given a convex objective function, we need to how many number of iterations we'll need to find a result which is $\varepsilon$−close to the minima of the function.

### Using Bisection Search

Assume you're given the interval $[a,b]$ to find the given minima for the function.

* Bisection Search Algorithm, basically after every iteration decreases the width of our search space in half.
* To be $\varepsilon$-close to the minima, we'll need the width of our interval to be less than $\varepsilon$.
* So after n iterations, the width would come down to 

$$
\begin{align*}
W_n = \frac{|b-a|}{2^n}
\end{align*}
$$

* So we get the equation -

$$
\begin{align*}
\frac{|b-a|}{2^n} \leq \varepsilon
\end{align*}
$$

* Solving for $n$, we get - 

$$
\begin{align*}
n \le \log_2\left(\frac{b-a}{\varepsilon}\right)
\end{align*}
$$

Thus, the algorithm runs in $\mathcal O(\log\left(\frac{1}{\varepsilon}\right))$ iterations.

### Using Golden Section Search

Assume you're given the interval $[a,b]$ to find the given minima for the function. 

Golden Section Search, after every iteration, the width decreases by a factor of $1$/$\varphi$ where $\varphi$ is the golden ratio. To be $\varepsilon$-close to the minima, we'll need the width of our interval to be less than $\varepsilon$. Thus, after $n$ iterations, the width would become:

$$
\begin{align*}
W_n = \frac{|b-a|}{\varphi^n}
\end{align*}
$$

So we get the equation

$$
\begin{align*}
\frac{|b-a|}{\varphi^n} \leq \varepsilon
\end{align*}
$$

Solving for $n$, we get

$$
\begin{align*}
n \le \log_{\varphi}\left(\frac{b-a}{\varepsilon}\right)
\end{align*}
$$

Thus, the algorithm runs in $\mathcal O(\log\left(\frac{1}{\varepsilon}\right))$ iterations.

Let us compare which method requires less number of iterations. Taking the worst case scenario, we can compare the number of iterations required in both the methods.

$$
\begin{align*}
\frac{n_{\text{Bisection}}}{n_{\text{Golden}}} = \frac{\log_2\left(\frac{b-a}{\varepsilon}\right)}{\log_{\varphi}\left(\frac{b-a}{\varepsilon}\right)} \approx 0.69
\end{align*}
$$

Even though the number of iterations are of the same order, the Bisection Method requires less number of iterations than the Golden Section Search because of the constant factor. 

Therefore, the Bisection Method seems to be the better method in terms of rate of convergence.

## Question 4

$a)$ Given the set $\mathbb{A}$ as:

$$
\begin{align*}
\mathbb{A}&= \left\\{\begin{bmatrix}
    5 \\
    9 \\
    3 \\
\end{bmatrix},
\begin{bmatrix}
    2 \\
    1 \\
    4 \\
\end{bmatrix}\right\\}
\end{align*}
$$

Notice, $\mathbb{A}$ contains two 3 dimensional vectors. Thus, its span will be a 2-dimensional plane in 3-dimensional space. The plane's equation can be found too. A similar procedure can be repeated for

$$
\begin{align*}
\mathbb{B}&= \left\\{\begin{bmatrix}
    7 \\
    1 \\
    7 \\
\end{bmatrix},
\begin{bmatrix}
    3 \\
    8 \\
    -1 \\
\end{bmatrix}\right\\}
\end{align*}
$$

However, the equations may not be immediately identical because a plane is given by $\hat{\mathbf{n}}\cdot(\mathbf{r-r_0})=0$ . Thus, there is variation in the equation with $\mathbf{r_0}$. Therefore, we opt for a different approach. To compare the subspace spanned, we need some form of row space/column space. That is, if we can somehow figure out the space spanned by the rows/columns by the matrices formed by these vectors, we are done.

Thus, firstly, express the vectors in the sets as matrices:

$$
\begin{align*}
\mathbf{A_1}&= \begin{bmatrix}
    5 & 9 & 3\\
    2 & 1 & 4 \\
\end{bmatrix} \\
\mathbf{B_1}&= \begin{bmatrix}
    7 & 1 & 7\\
    3 & 8 & -1 \\
\end{bmatrix}
\end{align*}
$$

Perform elementary row operations to try to match at least $1$ row of $\mathbf{A_1}$ to that of $\mathbf{B_1}$. Remember, these operations do not change the row or column space. (Proved later) 

$$
\begin{align*}
\mathcal{R_2}\leftarrow \mathcal{R_1}-\mathcal{R_2} 
\end{align*}
$$

$$
\begin{align*}
\implies \mathbf{A_1'}&= \begin{bmatrix}
    5 & 9 & 3\\
    3 & 8 & -1 \\
\end{bmatrix}
\end{align*}
$$

Beyond this, to check whether a row operation can be performed to reach $\mathbf{B_1}$, simply seek the solutions for the linear equation $\alpha \mathbf{a'_1}+\beta \mathbf{a'_2}=\mathbf{b_1}$. In this case, such a solution does not exist.

$b)$
Again, we are given the sets $\mathbb{A}$ and $\mathbb{B}$ as:

$$
\begin{align*}
\mathbb{A}&= \left\\{\begin{bmatrix}
    1 \\
    2 \\
    3 \\
\end{bmatrix},
\begin{bmatrix}
    6 \\
    5 \\
    4 \\
\end{bmatrix}\right\\}
\end{align*}
$$

$$
\begin{align*}
\mathbb{B}&= \left\\{\begin{bmatrix}
    8 \\
    9 \\
    10 \\
\end{bmatrix},
\begin{bmatrix}
    5 \\
    3 \\
    1 \\
\end{bmatrix}\right\\}
\end{align*}
$$

Express the vectors in the sets as matrices:

$$
\begin{align*}
\mathbf{A_2}&= \begin{bmatrix}
    1 & 2 & 3\\
    6 & 5 & 4 \\
\end{bmatrix} \\
\mathbf{B_2}&= \begin{bmatrix}
    8 & 9 & 10\\
    5 & 3 & 1 \\
\end{bmatrix}
\end{align*}
$$

Perform elementary row operations to try to match at least 1 row of $\mathbf{A_2}$ to that of $\mathbf{B_2}$.

$$
\begin{align*}
\mathcal{R_2}\leftarrow\mathcal{R_2}-\mathcal{R_1} \\
\end{align*}
$$

$$
\begin{align*}
\implies \mathbf{A_2'}&= \begin{bmatrix}
    1 & 2 & 3\\
    5 & 3 & 1 \\
\end{bmatrix} \\
\end{align*}
$$

$$
\begin{align*}
\mathcal{R_1}\leftarrow3\mathcal{R_1}+\mathcal{R_2} 
\end{align*}
$$

$$
\begin{align*}
\implies \mathbf{A_2'}&= \begin{bmatrix}
    8 & 9 & 10\\
    5 & 3 & 1 \\
\end{bmatrix} = \mathbf{B_2'}\
\end{align*}
$$

Thus, both sets span the same subspace.

Proving that elementary Row Operations Do Not Change Row Space. Let $\left\\{\mathbf{a_1},\mathbf{a_2}, \cdots \mathbf{a_m}\right\\}$ be the row vectors of a matrix $\mathbf{A}$ and let $\left\\{\mathbf{b_1},\mathbf{b_2}, \cdots \mathbf{b_m}\right\\}$ be the row vectors of a matrix $\mathbf{B}$. Let $\mathbf{B}$ be such that it has been obtained from elementary row operations on $\mathbf{A}$. Thus, $\mathbf{b_i}=\mathbf{a_i}+c\mathbf{a_j}$ \
Repeat the same procedure for $\mathbf{a_i}$ in terms of $\mathbf{b_i}$ and $\mathbf{b_j}$. Thus:

$$
\begin{align*}
\mathrm{span}\left(\left\\{\mathbf{a_1}, \mathbf{a_2} \cdots \mathbf{a_m}\right\\}\right) \subseteq \mathrm{span}\left(\left\\{\mathbf{b_1}, \mathbf{b_2} \cdots \mathbf{b_m}\right\\}\right) \\
\mathrm{span}\left(\left\\{\mathbf{b_1}, \mathbf{b_2} \cdots \mathbf{b_m}\right\\}\right) \subseteq \mathrm{span}\left(\left\\{\mathbf{a_1}, \mathbf{a_2} \cdots \mathbf{a_m}\right\\}\right)
\end{align*}
$$

In other words, their spans are equal. Thus, both have the same row space.



