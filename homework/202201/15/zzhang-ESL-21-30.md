# ESL: pp 21-30

(2.4 continue)

相似地去解决 categorical variable $G$.

1. $$EPE=E_X\sum_{k}^K L[\mathcal{G}_k, \hat{G}(X)] Pr(\mathcal{G_k}|X)$$. 

- L[A, B]: 把 A 错误地分到 B 的Loss

2. minimize EPE pointwise

如果用 *zero-one* loss function (all misclassifcations are charged a single unit) 得到 ***Bayes classifier***

- $$\hat{G}(x)=\arg\min_{g\in\mathcal{G}}[1-Pr(g|X=x)]$$
  - 解释：给定 x，把它分到最有可能的那个category去
- The error rate of the bayes classifier is called the ***Bayes rate***.

- 其实k-NN approximate了这一个过程，只不过用了neighborhood的majority vote。



### 2.5 Local Methods in High Dimensions

*curse of dimensionality*: 

- $p$-dimensional unit hypercube, capture a fraction $r$ of the observation
  - To capture 1% - 10% of the data, we must cover 63% or 80% of the range of each input variable.
  - Most data points are closer to the boundary of the sample space. Prediction is much more difficult near the edges of the training sample.
- sampling density is proportional to $N^{1/p}$. Too sparse!



*bias-variance*

Example 1: 1-nn rule to predict $y_0$ at the test-point $x_0=0$ with training set $\mathcal{T}$.  $f(x)=e^{-8\|x\|^2}$ is the real relationship. $x$ is sampled uniformly on $[-1,1]^p$.

- Expected prediction error (*bias-variance decomposition*)

  ​	$$MSE&=&E_\mathcal{T}[f(x_0)-\hat{y}_0]^2\\
  &=&E_{\mathcal{T}}[\hat{y}_0-E_{\mathcal{T}}(\hat{y}_0)]^2+[E_{\mathcal{T}}(\hat{y}_0)-f(x_0)]^2\\
  &=& \mbox{Var}_{\mathcal{T}}(\hat{y}_0) + \mbox{Bias}^2(\hat{y}_0)$$

- Variance: sampling variance of the 1-nearest neighbor

- x=0 的时候 y 实际取得最大值1，所以预测的值只有biased downward。
- 如果dimension $p$ 很小，bias 和 variance 都很小；如果dimension p很大，99% of the samples 都sample到了离origin至少0.5远的地方，所以estimate tends to 0。Bias最多只有1，variance 变得很小（因为都选0去了）。



Example 2: fitting $Y=X^T\beta+\epsilon$, $\epsilon\sim N(0,\sigma^2)$.

TODO



### 2.6 Statistical Models, Supervised Learning and Function Approximation

k-NN：direct estimates of the conditional expectation $f(x)=E(Y|X=x)$, fail when

- high dimensional input space, knn need not be close to the target point => large errors
- if special structure is known to exist, this can be used to reduce both the bias and the variance of the estimates. 



2.6.1 TODO



2.6.2 Supervised learning

- *learn by example*: modify the input/output relationship $\hat{f}$ in response to differences $y_i-\hat{f}(x_i)$ between the original and generated outputs.



2.6.3 Function Approximation

Machine Learning：

- data pairs $\{x_i,y_i\}$ are vied as points in a $(p+1)$-dimensional Euclidean space. The function $f(x)$ has domain equal to the $p$-dimensional input subspace.
- The goal is to obtain a useful approximation to $f(x)$ for all $x$ in some region of $\mathbb{R}^p$, given representations in $\mathcal{T}$.

To approximate with parameter $\theta$:

- linear basis expansions: $f_\theta(x)=\sum_{k=1}^K h_k(x)\theta_k$. 
  - $h_k$ : transformation such as $x_1^2$, $x_1x_2^2$, $cos(x_1)$ , sigmoid transformation.

Minimize residual sum-of-squares $RSS(\theta)=\sum_{i=1}^N(y_i-f_\theta(x_i))^2$.

- parameterized function => surface in $p+1$ space. What we observe are noisy realizations from it.



