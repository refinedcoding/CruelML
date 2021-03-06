# ESL: pp 71-80



## Subset Selection, Ridge and Lasso

在**正交**输入矩阵的情况下，三种过程都有显式解。每种方法对最小二乘估计 $\hat{\beta}_j$ 进行简单的变换：

| Estimator            | Formula                                                      |
| -------------------- | ------------------------------------------------------------ |
| Best subset (size M) | $\hat{\beta}_j \cdot \mathbb{1}(|\hat{\beta}_j|\ge|\hat{\beta}_{(M)}|)$ |
| Ridge                | $\hat{\beta}_j / (1+\lambda)$                                |
| Lasso                | $\text{sign}(\hat{\beta}_j)(|\hat{\beta}_j-\lambda|)_+$      |

岭回归做等比例的收缩．lasso 通过常数因子 $\lambda$ 变换每个系数，在 0 处截去。

**非正交**时，画图可得到：

- 残差平方和为椭圆形的等高线，以全最小二乘估计为中心
- 二维：Ridge的约束区域为圆形 $\beta_1^2+\beta_2^2\le t$. Lasso 为菱形 $|\beta_1+\beta_2|\le t$。两种方式都寻找当椭圆等高线达到约束区域的第一个点。
- 菱形有角，因此如果解出现在角上，则有一个参数 $\beta_j=0$。当 $p>2$ ，菱形变成了偏菱形 (rhomboid)，而且有许多角，平坦的边和面，有更多的参数估计可能为0.



一般化 $L_p$ regularizer后，可以看成是贝叶斯估计：

$\tilde{\beta}=\arg\min_{\beta}\{\sum_{i=1}^N(y_i-\beta_0-\sum_{j=1}^px_{ij}\beta_j)^2+\lambda\sum_{j=1}^p|\beta_j|^q\}$

$q=0$: 变量子集选择

$q=1$: lasso => **使得约束区域为凸的最小 q 值**。 非凸约束区域使得优化问题很困难!

$q=2$: ridge 

$q\le1$ 时：先验在各方向上不是均匀的，而是更多地集中在坐标方向上。

lasso、岭回归和最优子集选择是有着不同先验分布的贝叶斯估计。注意到它们取自后验分布的众数，即最大化后验分布。在贝叶斯估计中使用后验分布的均值更加常见。岭回归同样是**后验分布的均值**，但是 lasso 和最优子集选择不是。



当 $q>1$ 时，尽管$|\beta_j|^q$ 在0处可导，但并没有Lasso令系数恰好为0的性质。

弹性惩罚：

- $\lambda \sum_{j=1}^p (\alpha\beta_j^2+(1-\alpha)|\beta_j|)$
- 像 lasso 一样选择变量，同时像岭回归一样收缩相关变量的系数
- $\alpha=0.2$ 和 $q=1.2$ 时的轮廓线很像，但是用弹性惩罚会有尖角，而q=1.2时不会有尖角。



## Least Angle Regression

**最小角回归 (LAR)** 

算法：

第一步它确定与响应变量最相关的变量：不是完全的拟合该变量，LAR 使得该变量的系数向最小二乘值连续变化（使得它与进化的残差之间的相关系数绝对值降低）。只要其他变量与残差的相关性与该变量和残差的相关性相等，则该过程暂停．第二个变量加入活跃集，然后它们的系数一起以保持相关性相等并降低的方式变化．这个过程一直继续直到所有的变量都在模型中，然后在全最小二乘拟合处停止。



（略）



## Methods Using Derived Input Directions

解决输入变量相关性很强的问题：

- 产生较少的 输入变量$X_j$的线性组合 $Z_m$，用$Z_m$ 作为回归的输入。



### Principal Components Regression

TODO



