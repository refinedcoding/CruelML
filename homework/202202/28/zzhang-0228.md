## Linear Regression: Review 3

针对线性回归假设的检验方法：

1. 违反 误差项相互独立 => 自相关性：Autocorrelation 

   - 检验方法：Durbin-Watson (DW) Statistic

   - $d=\frac{\sum_{t=2}^T(e_t-e_{t-1})^2}{\sum_{t=1}^Te_t^2}$，$e_t$ 是 $t$ 时段的残差

   - 检验子相关是否在$\alpha$ 显著水平下为正，将$d$与关键值 $d_{L,a}$ 和 $d_{U,\alpha}$ 比较：

     - $d\le d_{L,\alpha}$: 误差项自相关为正
     - $d \ge d_{U,\alpha}$: 不拒绝，无自相关
     - $d_{L,\alpha} < d < d_{U,\alpha}$: 无法确认

   - 检验子相关是否在$\alpha$ 显著水平下为负，将$(4-d)$与关键值 $d_{L,a}$ 和 $d_{U,\alpha}$ 比较:

     - $(4-d)\le d_{L,\alpha}$: 误差项自相关为负

     - $(4-d) \ge d_{U,\alpha}$: 不拒绝，无自相关

     - $d_{L,\alpha} < (4-d) < d_{U,\alpha}$: 无法确认

       

2. 违反 自变量间相互独立 => 多重共线性：multicollinearity

   - 检验方法：Variance Inflation Factor (VIF) 

   - 回归模型 $Y=\beta_0+\beta_1X_1+\cdots+\beta_kX_k+\epsilon$

   - 系数的方差：$\hat{\text{Var}}(\hat{\beta}_j)=\frac{s^2}{(n-1)\hat{\text{Var}}{X_j}}\cdot\frac{1}{1-R_j^2}$. 

   - $R^2=1-\frac{SS_{res}}{SS_{tot}}$, $SS_{res}=\sum_i(y_i-f_i)^2=\sum_ie_i^2$ 残差平方和 ，  $SS_{tot}=\sum_i(y_i-\bar{y})^2$ 和数据variance成正比。

   - $\frac{1}{1-R_j^2}$ 为VIF，反映了影响系数估计不确定性的所有其他因素。VIF值越接近1，多重共线性越轻

     

3. 违反 误差项的方差为常数 => 异方差性：Heteroskedasticity

   - 检验方法：Breusch-Pagan (BP) test, White test

   - TODO

      

   

