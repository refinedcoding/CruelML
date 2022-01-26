# ESL: pp 61-70

Subset selection

- 得到一个可解释的、预测误差可能比全模型低
- 离散的过程（变量保留或丢弃）=> high variance => 没有降低全模型的预测误差



## Shrinkage methods



#### Ridge Regression

The ridge coefficients minimize a penalized residual sum of squares

$\hat{\beta}^{\text{ridge}}=\arg\min_{\beta}\{\sum_{i=1}^N (y_i-\beta_0-\sum_{j=1}^p x_{ij}\beta_j)^2+\lambda\sum_{j=1}^p \beta_j^2\}$

$\lambda$ 值越大，收缩的程度越大．每个系数都向零收缩



相当于求解

$\text{minimize} \sum_{i=1}^N (y_i-\beta_0-\sum_{j=1}^p x_{ij}\beta_j)^2$

$\text{subject to}\sum_{j=1}^{p}\beta_j^2\le t$



对输入按比例进行缩放时，岭回归的解不相等，因此求解之前需要对输入进行标准化。constraint与 $\beta_0$ 无关，所以可以对输入进行中心化。用$\bar{y}=\frac{1}{N}\sum_{i=1}^Ny_i$ 来估计 $\beta_0$。假设中心化已经完成，输入矩阵 $X$ 有p列。



写成矩阵形式：$\text{RSS}(\lambda)=(y-X\beta)^T(y-X\beta)+\lambda\beta^T\beta$

得到解 $\hat{\beta}^{\text{ridge}}=(X^TX+\lambda I)^{-1}X^Ty$

岭回归的解仍是 $y$ 的线性函数。在求逆之前对角元上加上 $\lambda$，即使 $X^TX$不是full rank，加上之后也是非奇异的。



---

🌟🌟

当给定一个合适的先验分布，岭回归也可以从后验分布的均值或众数得到。

假设 $y_i\sim N(\beta_0+x_i^T\beta, \sigma^2)$. 参数 $\beta_j\sim N(0,\tau^2)$ 且相互独立。当$\tau^2$ 和 $\sigma^2$ 的值已知时， $\beta$ 后验分布密度函数的绝对值（的负数）和 $\{\sum_{i=1}^N (y_i-\beta_0-\sum_{j=1}^p x_{ij}\beta_j)^2+\lambda\sum_{j=1}^p \beta_j^2\}$ 成比例 且 $\lambda=\frac{\sigma^2}{\tau^2}$.

因此岭回归估计是后验分布的众数；又因分布为高斯分布，则也是后验分布的均值．

---

利用奇异值分解（$$X=UDV^T$$）我们可以把最小二乘拟合向量写成

$X\hat\beta^{\text{ls}}=X(X^TX)^{-1}X^Ty=UU^Ty$. $U^Ty$ 是$y$ 正交基 $U$下的坐标。

$\hat\beta=R^{-1}Q^Ty$, $\hat{y}=QQ^Ty$

$Q$ 和 $U$ 是 $X$ 列空间的两个不同的正交基。

岭回归的解为 

- $X\hat{\beta}^{\text{ridge}}=X(X^TX+\lambda I)^{-1}X^Ty = UD(D^2+\lambda I)^{-1}DU^Ty=\sum_{j=1}^p u_j\frac{d_j^2}{d_j^2+\lambda}u_j^Ty$

- $u_j$  是 $U$ 的列向量
- $\frac{d_j^2}{d_j^2+\lambda}<1$.岭回归计算 $y$ 关于 正交基 $U$ 的坐标，通过因子 $\frac{d_j^2}{d_j^2+\lambda}<1$ 收缩坐标。更小的 $d_j^2$ 会更大程度上收缩基向量的坐标。

- 因此越小的奇异值 $d_j$ 对应 $X$ 列空间中方差越小的方向，并且岭回归在这些方向上收缩得最厉害。

$df(\lambda)=tr[X(X^TX+\lambda I)^{-1}X^T]=tr(H_\lambda)=\sum_{j=1}^p\frac{d_j^2}{d_j^2+\lambda}$

- This monotone decreasing function of $\lambda$ is the *effective degress of freedom* of  the ridge regression fit. 岭回归拟合的 **有效自由度 (effective degrees of freedom)**
- 当 $\lambda = 0$, $df(\lambda)=p$. 当 $\lambda \to \infty$，$df(\lambda)\to 0$



### Lasso

Lasso estimate 定义如下

$\hat{\beta}^{\text{lasso}} = \arg\min_{\beta} \sum_{i=1}^N (y_i-\beta_0-\sum_{j=1}^p x_{ij}\beta_j)^2$

$\text{subject to}\sum_{j=1}^{p}|\beta_j|\le t$

=> (Lagrangian form)

$\hat{\beta}^{\text{lasso}}=\arg\min_{\beta}\{\sum_{i=1}^N (y_i-\beta_0-\sum_{j=1}^p x_{ij}\beta_j)^2+\lambda\sum_{j=1}^p |\beta_j|\}$

计算 lasso 的解是一个二次规划问题。令 $t$ 充分小会造成一些参数恰恰等于0，因此Lasso完成一个温和的连续子集选择。

