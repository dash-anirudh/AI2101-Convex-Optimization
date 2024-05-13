# Convex Optimization Assignment 6 Solutions

## General Instructions

The following document contains the solutions to the questions for Assignment 6. Please note that the solutions provided may not be the only possible way to solve the questions. They indicate only one of the many (possibly) valid solutions. The solutions provided are relatively crisp and do not include all the steps that you must have. Your solution should be logical and contain all supporting arguments. Feel free to contact any of the TAs via email in case of any discrepancy you find in the solutions provided.

## Question 2
$f(\mathbf{w})$ can be written as 

$$
f(\mathbf{w}) = - \sum _ {i=1}^{N}\left(y_{i}\log(\hat{y} _ {i})  + ( 1-y_{i})  \log( 1-\hat{y}_{i})\right)
$$

where $\hat{y} _ {i}  =\sigma (z_{i}) =\frac{1}{1+e^{-z}}$ and  $z_{i} =\mathbf{w}^{T}\mathbf{x}_{i} \quad \forall  i \in \\{1,2,..., N\\}$

$a)$ The gradient of $f(\mathbf{w})$ with respect to $w$ can be computed as follows:

$$
\nabla f(\mathbf{w}) = \begin{bmatrix} \frac{\partial f}{\partial w_1} \\\ \\\ \frac{\partial f}{\partial w_2} \\\ \\\ \vdots \\\ \\\ \frac{\partial f}{\partial w_n} \end{bmatrix}
$$

Where $\frac{\partial f}{\partial w_i}$ represents the partial derivative of $f(\mathbf{w})$ with respect to the $i$-th component of $w$.

Using the chain rule, we have:

$$
\frac{\partial f(\mathbf{w})}{\partial \mathbf{w}}  = \sum _ {i=1}^{N}\frac{\partial f(\mathbf{w})}{\partial \hat{y} _ {i}}\frac{\partial \hat{y} _ {i}}{\partial z_{i}}\frac{\partial z_{i}}{\partial \mathbf{w}}
$$

Solving for each term individually 

$$
{\frac{\partial f(\mathbf{w})}{\partial \hat{y} _ {i}}  = -\left(\frac{y_{i}}{\hat{y} _ {i}} -\frac{1-y_{i}}{1-\hat{y} _ {i}}\right) =\frac{\hat{y} _ {i} -y_{i}}{\hat{y} _ {i}( 1-\hat{y}_{i})}}
$$

$$
{\frac{\partial \hat{y} _ {i}}{\partial z_{i}} =\frac{\partial \left(\frac{1}{1+e^{-z_{i}}}\right)}{\partial z_{i}} =\hat{y} _ {i}( 1-\hat{y}_{i})}
$$

$$
{\frac{\partial z_{i}}{\partial \mathbf{w}} =\mathbf{x}_{i}}
$$

Therefore, 

$$
{\frac{\partial f(\mathbf{w})}{\partial \mathbf{w}} = \sum _ {i=1}^{N}(\hat{y} _ {i} -y_{i})\mathbf{x} _ {i}}\\
\implies \nabla f(\mathbf{w}) = \sum _ {i=1}^{N}( \sigma \left(\mathbf{w}^{T}\mathbf{x} _ {i}\right) -y_{i})\mathbf{x}_{i}\\
\implies \nabla f(\mathbf{w}) = \mathbf{Xd}
$$

where $\mathbf X = [\mathbf x_1, \ \mathbf x_2, \ \cdots, \ \mathbf x_N]$ and $\mathbf d$ is a vector with the $i$-th entry as $d_i = \sigma \left(\mathbf{w}^{T}\mathbf{x}_{i}\right) - y_i$

Calculating the Hessian matrix of $f(\mathbf{w})$:

$$
\nabla^2(\mathbf{w}) = \begin{bmatrix} \frac{\partial^2 f}{\partial w_1^2} & \frac{\partial^2 f}{\partial w_1 \partial w_2} & \cdots & \frac{\partial^2 f}{\partial w_1 \partial w_n} \\\ \frac{\partial^2 f}{\partial w_2 \partial w_1} & \frac{\partial^2 f}{\partial w_2^2} & \cdots & \frac{\partial^2 f}{\partial w_2 \partial w_n} \\\ \vdots & \vdots & \ddots & \vdots \\\ \frac{\partial^2 f}{\partial w_n \partial w_1} & \frac{\partial^2 f}{\partial w_n \partial w_2} & \cdots & \frac{\partial^2 f}{\partial w_n^2} \end{bmatrix} 
$$

Where $\frac{\partial^2 f}{\partial w_i \partial w_j}$ represents the second-order partial derivative of $f(\mathbf{w})$ with respect to the $j$-th and $k$-th components of $w$.

The second-order partial derivatives can be computed as follows:

$$
\frac{\partial^2 f}{\partial w_j \partial w_k} = \sum_{i=1}^{N} \sigma(\mathbf{w^T} \mathbf{x_i}) \left( 1 - \sigma(\mathbf{w}^T\mathbf{x} _ i) \right) x_{ij} x_{ik}
$$

where $x_{ij}$ and $x_{ik}$ denote the $j$-th and $k$-th components of the $i$-th data point $x_i$.

Writing the above equation in matrix form, we get:

$$
\begin{align*}
\nabla^{2} f(\mathbf{w}) &=\sum _ {i=1}^{N} \mathbf{x} _ {i}\mathbf{x} _ {i}^{T} \sigma \left(\mathbf{w}^{T}\mathbf{x} _ {i}\right) \left( 1-\sigma \left(\mathbf{w}^{T}\mathbf{x}_{i}\right)\right)\\
\implies \nabla ^{2} f(\mathbf{w}) &=\mathbf{XDX}^{T}
\end{align*}
$$

where $\mathbf X = [\mathbf x_1, \ \mathbf x_2, \ \cdots, \ \mathbf x_N]$ and $D$ is a diagonal matrix with ${D_{ii} = \sigma \left(\mathbf{w}^{T}\mathbf{x} _ {i}\right)\left( 1-\sigma \left(\mathbf{w}^{T}\mathbf{x}_{i}\right)\right)}$

Writing the update equation for Newton-Raphson's method:

$$
w^{(k+1)} = w^{(k)} - \left( \nabla^2 f(w^{(k)}) \right)^{-1} \nabla f(w^{(k)}) 
$$

Where $w^{(k)}$ denotes the current estimate of the minimum, and $w^{(k+1)}$ denotes the updated estimate.

Substituting the values of $\nabla^2 f(\mathbf{w})$ and $\nabla f(\mathbf{w})$ in the above equation, we get:

$$
\begin{align*}
w^{(k+1)} &= w^{(k)} - \left(\left( \mathbf{XDX}^{T} \right)^{-1} \mathbf{Xd}\right)\bigg|_{w^{(k)}} \\
\end{align*}
$$

where $|_{w^{(k)}}$ denotes the evaluation of the expression at $w^{(k)}$.

$$
\begin{align*}
w^{(k+1)} &= w^{(k)} - \left(\mathbf{X^{-T}D^{-1}d}\right)\bigg|_{w^{(k)}} \\
&= w^{(k)} - X^{-T}t^{(k)}
\end{align*}
$$

where $t^{(k)}$ is defined as 

$$
\begin{align*}
t^{(k)} &= D^{-1}d \big| _ {w^{(k)}} \\
\implies t^{(k)} _ i &= \frac{\sigma\left(\mathbf{x} _ i^T\mathbf{w}^{(k)}\right)-y_i}{\sigma \left(\mathbf{x} _ {i}^T\mathbf{w}^{(k)}\right)\left( 1-\sigma \left(\mathbf{x}_{i}^T\mathbf{w}^{(k)}\right)\right)}
\end{align*}
$$

$b)$ Let $\mathbf{p}$ be a vector such that $\mathbf{p} \in \mathbb{R}^n$. Then,

$$
\begin{align*}
\mathbf{p}^T\nabla^2 f(\mathbf{w})\mathbf{p} &= \mathbf{p}^T\mathbf{XDX}^{T}\mathbf{p}\\
&=  (\mathbf{X}^T\mathbf{p})^T\mathbf{D}(\mathbf{X}^T\mathbf{p}) \\
&=  (\mathbf{X}^T\mathbf{p})^T\mathbf{D}^{1\over 2}\mathbf{D}^{1\over 2}(\mathbf{X}^T\mathbf{p}) \\
\end{align*}
$$

We can split the matrix $\mathbf{D} = \mathbf{D}^{1\over 2}\mathbf{D}^{1\over 2}$ as $D$ is a diagonal matrix with all positive values. Therefore, $\mathbf{D}^{1\over 2}$ will be the square root of the diagonal elements of $\mathbf{D}$.

$$
\begin{align*}
\mathbf{p}^T\nabla^2 f(\mathbf{w})\mathbf{d} &=  \left(\mathbf{D}^{1\over 2}\mathbf{X}^T\mathbf{p}\right)^T(\mathbf{D}^{1\over 2}\mathbf{X}^T\mathbf{p}) \\
&= \Vert\mathbf{D}^{1\over 2}\mathbf{X}^T\mathbf{p}\rVert^2\ge 0
\end{align*}
$$

So, we can see that $\nabla^2 f(\mathbf{w})$ will be Positive Semi-Definite, and therefore $f(\mathbf{w})$ will be convex. 

Therefore, we can conclude that Newton-Raphson will converge to a local minima, and the local minima might coincide with the global minima in some cases.

## Question 3
Let's define the noisy signal ${f(t)}$ as the corrupted signal, modeled as ${f(t) = g(t) + n(t)}$, where ${n(t)}$ represents the noise component. The minimization problem is formulated as follows:

$$
{\min_{a_0, a_1, \ldots, a_m} \sum_{i=1}^{N} (f(t_i) - g(t_i))^2}
$$

where: ${a_0, a_1, \ldots, a_m}$ are the coefficients of the polynomial ${g(t)}$. ${t_i}$ are the given data points and ${N}$ is the number of data points.

Now, let's propose a numerical optimization algorithm using Newton's Method to minimize the function with respect to $t = [t_1, \ t_2,\ \cdots, \ t_N]$.

### Algorithm:

1. Initialize the vector of data points ${ t }$.
2. Compute the noisy signal ${ f(t) }$ using the given data points and the polynomial ${ g(t) }$.
3. Define the objective function to be minimized:

$$
{ \displaystyle \mathcal L(t) = \sum_{i=1}^{N} (f(t_i) - g(t_i))^2 }
$$

4. Compute the gradient vector ${\nabla \mathcal L(t)}$ and the Hessian matrix ${H(t)}$ of ${\mathcal L(t)}$.
5. Update the vector of data points using Newton's Method:

$$
{t^{(k+1)} = t^{(k)} - \left(H\left(t^{(k)}\right)\right)^{-1} \nabla \mathcal L(t^{(k)}) }
$$

6. Repeat steps $2-5$ until convergence criteria are met (defined below).

### Convergence Criteria:

You can define convergence criteria based on the change in the objective function value or the norm of the gradient vector. For example, one can terminate the algorithm when the norm of the gradient vector falls below a certain threshold as gradient norm approaching to a zero value indicates that the iterator $t^{(k)}$ is close to a critical point.
