## Question 2
Since the goal is to estimate the model parameters a and e using measurements of r at n different values of t, the optimisation problem at hand can be stated as 

$$
\min \sum_{i=1}^{n} (r_i- r(t_i))^2 
$$

This can be restated as follows

$$ 
\min \lVert \mathbf{r} - \mathbf{f}(a,e) \rVert^{2} 
$$

where $\mathbf{r} = [r_1, \ r_2, \ \cdots, \ r_n]^T$ 
and 

$$ 
\mathbf{f}(a,e) = \begin{bmatrix} a(1-e \cos (\theta(t_1)))^2 \\\ a(1-e \cos (\theta(t_2)))^2 \\\ \vdots \\\ a(1-e \cos (\theta(t_n)))^2 \end{bmatrix} 
$$

$a)$ The state vector $\mathbf{x}$ is clearly $[a,\ e]^T$

The affine approximation to $\mathbf{f}(a,e) $ defined above at $\mathbf{x_0} = [a_0,\  e_0]^T$ is given by   

$$
\mathbf{l}(\mathbf{x}) = \mathbf{f}(\mathbf{x_0}) + D(\mathbf{f}(\mathbf{x_0}))(\mathbf{x}-\mathbf{x_0})
$$

where $D(\mathbf{f}(\mathbf{x_0}))$ is the derivative matrix of $\mathbf{f}(a,e) $ wrt  $[a,\ e]^T $ at $[a_0,\ e_0]^T $ and it is given by,

$$
\begin{align*}
D(\mathbf{f}(\mathbf{x_0})) &= D(\mathbf{f}(a_0,e_0))\\
&=\begin{bmatrix} (1-e_0 \cos (\theta(t_1)))^2, -2a_0\cos (\theta(t_1))(1-e_0 \cos (\theta(t_1))) \\\ (1-e_0 \cos (\theta(t_2)))^2, -2a_0\cos (\theta(t_2))(1-e_0 \cos (\theta(t_2))) \\\ \vdots \\\ (1-e_0 \cos (\theta(t_n)))^2, -2a_0\cos (\theta(t_n))(1-e_0 \cos (\theta(t_n))) \end{bmatrix} 
\end{align*} 
$$

$b)$ In Gaussian-Newton Method, the following optimisation problem is solved

$$ 
\min \quad \lVert \mathbf{r} - \mathbf{l}(\mathbf{x}) \rVert^{2} 
$$

where $\mathbf{l}(\mathbf{x})$ is as defined in part $(a)$ and $\mathbf{r}$ is as defined in the premise above part $(a)$

$c)$ According to Gaussian-Newton Method, the update equation after k iterations is given by,

$$
\mathbf{x_{k+1}} = \mathbf{x_{k}} + \Delta \mathbf{x}
$$

$$
(J^TJ)\Delta \mathbf{x} = J^T(\mathbf{r}-\mathbf{f}(\mathbf{x_k})) 
$$

where $\mathbf{x_k} = [a_k,\ e_k]^T$ and 

$$
J = \begin{bmatrix} (1-e_k \cos (\theta(t_1)))^2, -2a_k\cos (\theta(t_1))(1-e_k \cos (\theta(t_1)))\\\ (1-e_k \cos (\theta(t_2)))^2, -2a_k\cos (\theta(t_2))(1-e_k \cos (\theta(t_2))) \\\ \vdots \\\ (1-e_k \cos (\theta(t_n)))^2, -2a_k\cos (\theta(t_n))(1-e_k \cos (\theta(t_n))) \end{bmatrix}
$$
