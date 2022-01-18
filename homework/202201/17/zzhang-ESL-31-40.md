# ESL: pp 31 - 40

(2.6 continue)

*Maximum likelihood estimation*:

- Suppose we have a random sample $y_i$, $i=1,...,N$ from a density $Pr_\theta(y)$ indexed by some parameters $\theta$. 
- The log-probability of the observed sample is $L(\theta)=\sum_{i=1}^Nlog Pr_{\theta}(y_i)$.

Example 1: $Y=f_{\theta}(X)+\epsilon$, $\epsilon\sim N(0,\sigma^2)$. 

- Least squares for it is same to maximum likelihood using the conditional likelihood 

  - $Pr(Y|X,\theta)=N(f_{\theta}(X), \sigma^2)$.
  - Then log-likelihood is $L(\theta)=-\frac{N}{2}log(2\pi)-Nlog\sigma-\frac{1}{2\sigma^2}\sum_{i=1}^N(y_i-f_{\theta}(x_i))^2$.

  - Only last term contains $\theta$, so maximize $L(\theta)$ is the same as minimize RSS($\theta$)

Example 2: quanlitative output => cross-entropy

- $L(\theta)=\sum_{i=1}^N log\ p_{g_i,\theta}(x_i)$.



### Structured Regression Models

Minimizing $RSS(f)=\sum_{i=1}^N(y_i-f(x_i))^2$  leads to infinitely many solutions of $\hat{f}$.

=> Add restrictions (encoded via the parametric representation $f_{\theta}$ or may be build into the learning method itself implicitly or explicitly).



The strength of the constant is dictated by the neighborhood size

-  larger the neighborhood size, stronger the constraint
- Directly: kernel and local regression, tree-based methods
- Implicitly: splines, neural networks, basis-function methods



### Classes of Restricted Estimators

- *smoothing* parameters: control the effective size of the local neighborhood



#### Roughness Penalty and Bayesian Methods

$PRSS(f;\lambda)=RSS(f)+\lambda J(f)$.

- $J(f)$: large for function f that vary too rapidly over small regions of input space

Example J(f): *cubic smoothing spline* for one-dim inputs

- $PRSS(f;\lambda)=\sum_{i=1}^N(y_i-f(x_i))^2+\lambda\int[f''(x)]^2dx$.

Interpretation：

- Penalty function (regularization) express our prior belif that the type of functions we seek exhibit a certain type of smooth behavior. The penalty $J$ corresponds to a log-prior, and $PRSS(f;\lambda)$ amounts to finding the posterior mode.



#### Kernel Methods and Local Regression

Idea: explicitly provide estimates of the regression function or conditional expectation by specifying the nature of the local neighborhood. *Fitted locally*

*kernel function* $K_\lambda(x_0,x)$ => assigns weights to points $x$ in a region around $x_0$.

- Example: Gaussian density function $K_\lambda(x_0,x)=\frac{1}{\lambda}exp[-\frac{\|x-x_0\|^2}{2\lambda}]$.
  - $\lambda$: variance of the Gaussian density, controls the width of the neighbohood.

*kernel estimate*: 

- Example: Nadaraya-Watson weighted average:
  - $\hat{f}(x_0)=\frac{\sum_{i=1}^NK_\lambda(x_0,x_i)y_i}{\sum_{i=1}^NK_\lambda(x_0,x_i)}$

Local regression estimate $f_{\hat{\theta}}(x_0)$of $f(x_0)$ :

- $\hat{\theta}= \arg\min_\theta RSS(f_{\theta},x_0)=\sum_{i=1}^N K_\lambda(x_0,x_i)(y_i-f_{\theta}(x_i))^2$,
  - $f_{\theta}(x) = \theta_0$ Constant function. => Nadaraya-Watson estimate
  - $f_{\theta}(x)=\theta_0+\theta_1x$ => local linear regression method



k-NN can be regarded as kernel methods having a more data-dependent meytric

- $K_k(x,x_0)=I(\|x-x_0\|\le \|x_{(k)}-x_0\|)$
  - $I(\cdot)$ Indicator function
  - $x_{(k)}$: training observation ranked $k$-th in distance from $x_0$
- 相当于，kernel是去选择 k 近邻



#### Basis Functions and Dictionary Methods

Model for $f$ is a linear expansion of basis functions

- $f_{\theta}(x) = \sum_{m=1}^M \theta_mh_{m}(x)$

Example 1: Radial basis function

- $f_\theta(x)=\sum_{m=1}^MK_{\lambda_m}(\mu_{m},x)\theta_m$
- symmetric $p$-dimensional kernels located at particular centroids

Example 2: single-layer feed-forward neural network

- $f_\theta(x)=\sum_{m=1}^M\beta_m\sigma(\alpha_m^Tx+b_m)$
- $\sigma(\cdot)$ activation function. 



Adaptively chosen basis function methods is *dictionary* methods

- One has available a possibly infinite set of dictionary $\mathcal{D}$ of candidate basis functions. Models are built up by employing some kind of search mechanism.

  

### Model Selection and the Bias-Variance Tradeoff

Bias-variace tradeoff



Suppose the data arise from a model $Y=f(X)+\epsilon$, with $E(\epsilon)=0$ and $Var(\epsilon) =\sigma^2$.



The expected prediction error (generalization error) at $x_0$:

$EPE_k(x_0)=E[(\hat{Y}-\hat{f}_k(x_0))^2|X=x_0]$



TODO
