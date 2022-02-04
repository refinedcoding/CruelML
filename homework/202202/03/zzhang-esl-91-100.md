# ESL: pp 91 - 100

##### Further Properties of the LASSO

- Relaxed lasso: 采用 lasso 来选择非零预测变量，接着再次运用 lasso，但是从第一步开始便只用选择出的变量。

- 修改 lasso 惩罚函数使得更大的系数收缩得不要太剧烈 => **平稳削减绝对偏差法 (smoothly clipped absolute deviation, SCAD)** 。不是凸的，很难算～
- Adaptive lasso: $w_j|\beta_j|$ 加权。$w_j=1/|\hat{\beta_j}|^v$. $\hat\beta_j$ 是一般最小二乘估计并且 ν > 0. adaptive lasso 在保证 lasso 吸引人的凸性基础上还得到了参数的一致估计

##### Pathwise Coordinate Optimization

在固定Lagrangian 中 $\lambda$ ，控制其他参数固定不变时，相继优化每一个参数

$\hat\beta^{lasso}=\arg\min_\beta \{\sum_{i=1}^N(y_i-\beta_0-\sum_{j=1}^px_{ij}\beta_j)^2+\lambda\sum_{j=1}^p |\beta_j|\}$.

假设预测变量都经过标准化得到 0 均值和单位范数，$\tilde\beta_k(\lambda)$ 表示惩罚参数为 $\lambda$ 时对$\beta_k$ 的当前估计，可以分离出上式的 $\beta_j$：

$R(\tilde\beta(\lambda), \beta_j)=\frac{1}{2}\sum_{i=1}^N (y_i-\sum_{k\neq j}x_{ik}\tilde\beta_k(\lambda)-x_{ij}\beta_j)^2 + \lambda\sum_{k\neq j}|\tilde\beta_k(\lambda)|+\lambda|\beta_j|$.

这个可以看成是响应变量为部分残差：$y_i-\tilde y_i = y_i - \sum_{k\neq j}x_{ik}\tilde\beta_k(\lambda)$。

=> $\tilde\beta_j\gets S(\sum_{i=1}^N x_{ij}(y_i-\tilde{y}_i^{(j)}), \lambda)$

where $S(t,\lambda)=sign(t)(|t|-\lambda)_+$.

我们从使得 $\hat\beta(\lambda_{max})=0$ 的最小 $\lambda_{max}$ 开始，每次降低一点点来循环考虑每个变量直到收敛．采用前一个解作为 $\lambda$ 新值的“warm start”，$\lambda$ 再一次降低，并且重复该过程



总结：

TODO
