# ESL: pp 121 - 130

### Logistic Regression

K 个类别，用 $k-1$ 个 log-odds $\log\frac{\Pr(G=k|X=x)}{\Pr(G=K|X=x)}=\beta_{k0}+\beta_{k}^Tx$ 来确定。虽然模型采用最后一类来作为 odds-ratios 的分母，但分母的选择其实是任意的。

$\Pr(G=k|X=x)=\frac{\exp(\beta_{k0}+\beta_k^Tx)}{1+\sum_{\ell=1}^{K-1}\exp(\beta_{\ell 0}+\beta_\ell^T x)},k=1,\cdots, K-1$

$\Pr(G=K|X=x)=\frac{1}{1+\sum_{\ell = 1}^{K-1}\exp(\beta_{\ell 0}+\beta_{\ell}^Tx)}$.

- 参数集：$\theta = \{\beta_{10}, \beta_1^T,\cdots,\beta_{(K-1)0},\beta_{K-1}^T\}$
- 分到 $k$ 类别的概率为 $p_k(x,\theta)$



- PRML里面定义 $\Pr(G=k|X=x)=\frac{\exp(\beta_k^Tx)}{\sum_{\ell}\exp(\beta_{\ell}^Tx)}$，有 $K$ 个系数向量，多一个。



#### Fitting Logistic Regression Models

N 个观测的对数似然是：$\ell(\theta)=\sum_{i=1}^N \log p_{g_i}(x_i;\theta)$

二分类简化：$p_1(x;\theta)=p(x;\theta)$, $p_2(x;\theta)=1-p(x;\theta)$

=> $p(x;\theta)= \frac{e^{\beta^T x}}{1+e^{\beta^Tx}}$

$\ell(\beta)=\sum_{i=1}^N\{y_i\log p(x_i;\beta) + (1-y_i)\log(1-p(x_i;\beta))\}\\
=\sum_{i=1}^N\{y_i\beta^Tx_i-\log(1+e^{\beta^Tx_i})\}$

- $\beta = \{\beta_{10}, \beta_{1}\}$



=> 为了最大化对数似然，令微分为0: $\frac{\partial \ell(\beta)}{\partial \beta}=\sum_{i=1}^N x_i(y_i-p(x_i;\beta)) = 0$

- 其中 $\frac{\partial \log(1+e^{\beta^Tx})}{\partial \beta}=\frac{xe^{\beta^Tx}}{e^{\beta^T x}+1}$



为了求解上式，采用 Newton-Raphson 算法，需要Hessian矩阵：

$\frac{\partial^2 \ell(\beta)}{\partial\beta\ \partial\beta^T}=-\sum_{i=1}^Nx_ix_i^Tp(x_i;\beta)(1-p(x_i;\beta))$

$\beta^{new}=\beta^{old}-(\frac{\partial^2\ell(\beta)}{\partial\beta\ \partial \beta^T})^{-1}\frac{\partial \ell(\beta)}{\partial\beta}$



记 $W$ 是第 $i$ 个对角元为 $p(x_i;\beta^{old})(1-p(x_i;\beta^{old})) $ 的 $N\times N$ 的对角矩阵，我们有

​	$\frac{\partial\ell(\beta)}{\partial\beta}=X^T(y-p)$

​	$\frac{\partial^2\ell(\beta)}{\partial\beta\partial\beta^T}=-X^TWX$

- 牛顿迭代 =>

  $\beta^{new}&=&\beta^{old}+(X^TWX)^{-1}X^T(y-p)\\
  &=&(X^TWX)^{-1}X^TW(X\beta^{old}+W^{-1}(y-p))\\
  &=&(X^TWX)^{-1}X^TWz$

- 最小二乘迭代，响应变量为 $z=X\beta^{old}+W^{-1}(y-p)$

- 每一次迭代时，$p$ 改变，因此 $W$ 和 $z$ 也改变

- 这个算法被称作 **加权迭代最小二乘 (iteratively reweighted least squares)** 或者 IRLS

- 每次迭代求解加权最小二乘问题：

  $\beta^{new}\gets \arg\min_{\beta} (z-X\beta)^TW(z-X\beta)$

  - $\beta=0$ 是一个好的初始值，尽管不会保证收敛。
  -  步长折半 (step size halving) 会保证收敛

  

#### Example: South African Heart Disease

- 用Z-score 去判断该因素显不显著，绝对值 > 2 表明在 5% 的水平下是显著的

方法一：

删掉显著性最低的系数然后重新拟合模型，可以重复做下去直到没有更多的项可以从模型中剔除

方法二：（更好）

对每一个剔除一个变量后的模型进行重新拟合，然后进行 **偏差分析 (analysis of deviance)** 确定哪个变量需要剔除。



#### Quadratic Approximations and Inference

略



#### $L_1$ Regularized Logistic Regresson

$\max_{\beta_0,\beta}\{\sum_{i=1}^N [y_i(\beta_0+\beta^Tx_i)-\log(1+e^{\beta_0+\beta^Tx_i})-\lambda\sum_{j=1}^p|\beta_j|]\}$

- 运用非线性规划方法可以找到一个解
- 运用 Netwon 算法的二次逼近，我们可以通过重复应用加权的 lasso 算法求解





#### Logistic Regression or LDA?

考虑$K$个类别，LDA对类别的概率密度函数做了**正态分布**假设以及**协方差相等**的假设。

LDA：

- $\log\frac{\Pr(G=k|X=x)}{\Pr(G=K|X=x)}=\log \frac{\pi_k}{\pi_K}-\frac{1}{2}(\mu_k+\mu_K)^T\Sigma^{-1}(\mu_k-\mu_K)=\alpha_{k0}-\alpha_k^Tx$.

- 最大化联合概率 $\Pr(X,G)$ 来估计参数。

Logistic regression:

- $\log\frac{\Pr(G=k|X=x)}{\Pr(G=K|X=x)}=\beta_{k0}+\beta_k^Tx$.

- 最大化条件概率 $\Pr(G|X)$ 来估计参数。



当有许多的边界点时，LDA 不够robust。一般感觉逻辑斯蒂回归更加安全，因为它依赖更少的假设。从经验来看，即便不恰当地运用 LDA，比如说对定性预测变量应用 LDA，两个模型都会得到非常相似的结果。

