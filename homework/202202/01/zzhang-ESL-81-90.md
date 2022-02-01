# ESL: pp 81-90

(79-80)

 ##### Methods Using Derived Input Directions

解决输入变量相关性很强的问题：

- 产生较少的 输入变量$X_j$的线性组合 $Z_m$，用$Z_m$ 作为回归的输入。

##### Principal Components Regression (PCR) 主成分回归

Derived: $z_m=Xv_m$, 然后在 $z_1,\cdots,z_M$, $M\le p$ 上回归 $y$。其中 $z_m$ 正交。

$\hat{y}=\bar{y}\mathbf{1} + \sum_{m=1}^{M}\hat\theta_{m}z_m$, $\hat\theta_m=\langle z_m,y\rangle/\langle z_m,z_m \rangle$

M = p 就是最小二乘估计

M < p 降维的regression，丢掉 p − M 个最小的特征值分量。

 ##### Partial Least Squares (PLS) 偏最小二乘

假设每个$x_j$ 标准化使得均值为0，方差为1. 

$\hat\varphi_{1j}=\langle x_j,y\rangle$, $z_1=\sum_j \hat\varphi_{1j}x_j$. 这是第一偏最小二乘方向。在每个 $z_m$ 的构造中，输入变量通过判断其在 $y$上的单变量影响强度来加权。

算法步骤 m = 1, 2, ..., p

1. $z_m=\sum_{j=1}^p \hat\varphi_{mj}x_j^{(m-1)}$, $\hat\varphi_{mj}=\langle x_j^{(m-1)},y\rangle$
2. $\hat\theta_m=\langle z_m,y\rangle/\langle z_m,z_m\rangle$
3. $\hat{y}^{(m)}=\hat{y}^{(m-1)}+\hat\theta_mz_m$.
4. Orthogonalize each $x_j^{(m-1)}$ : $x_j^{(m)}=x_j^{(m-1)}-[\langle z_m,x_j^{m-1}\rangle / \langle z_m,z_m\rangle]z_m$

如果输入矩阵 $X$ 是正交的，则偏最小二乘会经过 $m=1$ 步找到最小二乘估计。当 $m>1$ 时，$\hat\varphi_{mj}=0$.

偏最小二乘寻找**有高方差**以及**和响应变量有高相关性**的方向，而与之相对的主成分分析回归只重视高方差


---

##### Discussion: A comparison of the selection and shrinkage methods

岭回归和 lasso 的惩罚参数在一个连续的区域内变化，而最优子集，PLS 和 PCR 只要两个离散的步骤便达到了最小二乘解。

参数的相关系数为正时：

- 从零点开始，岭回归整体收缩参数直到最后收缩到最小二乘。尽管 PLS 和 PCR 是离散的且更加极端，但它们显示了类似岭回归的行为。最优子集超出解然后回溯。lasso 的行为是其他方法的过渡。

参数的相关系数为负时：

- PLS 和 PCR 大致地跟随岭回归的路径，而所有的方法都更加相似。



Ridge 岭回归：对所有方向都有收缩但在低方差方向收缩程度更厉害。

PCR 主成分回归：将 MM 个高方差的方向单独取出来，然后丢掉剩下的。

PLS 偏最小二乘回归：趋向于收缩低方差的方向，但是实际上会使得某些高方差方向膨胀。不太稳定，因此相比于岭回归会有较大的预测误差。



🌟🌟 对于最小化预测误差 prediction error，ridge 岭回归一般比变量子集选择 subset selection、主成分回归 PCR 和偏最小二乘 PCR 更好。然而，相对于后两种方法的提高只是很小的。

总的来说，PLS，PCR 以及岭回归趋向于表现一致，但岭回归更好，收缩得很光滑，不像离散步骤中一样。Lasso 介于岭回归和最优子集回归中间，并且有两者的部分性质。



#### Multiple Outcome shrinkage and selection

多重输出：

$Y_k=f(X)+\epsilon_k$, $Y_\ell=f(X)+\epsilon_{\ell}$. 有相同的模型结构 $f(X)$ => 应该合并 $Y_k$ 和 $Y_\ell$ 来估计共同的 $f$.

合并响应变量 => **CCA (canonical correlation analysis) ** 典则相关分析

- 寻找 $x_j$ 的一列不相关的线性组合 $Xv_{m},m=1,\cdots,M$ 以及对应的响应变量 $y_k$ 的不相关的线性组合 $Yu_m$，使得相关系数 $Corr^2(Yu_m,Xv_m)$ 相继最大。

具体方法如 reduced-rank regression 略。

#### More on the lasso and related path algorithms

##### Incremental forward stagewise regression

- 通过重复更新与当前残差最相关的变量的系数（乘以一个小量 $\epsilon$）得到系数曲线
- $\epsilon$ 相当于 step size.

算法细节：

1. Intialization: normalize predictors. residual $r = y$.
2. find the predictor $x_j$ most correlated with residual $r$
3. Update $\beta_j\gets \beta_j+\delta_j$, $\delta_j=\epsilon\cdot \text{sign}[\langle x_j,r\rangle]$. $r\gets r - \delta_jx_j$.
4. 重复2-3，直到 residual are uncorrelated with all the predictors

$\epsilon\to 0$ 的时候叫做 **无穷小的向前逐渐回归 (infinitesimal forward stagewise regression)** ，和LASSO的路径差不多。在非线性、自适应方法中有着很重要的作用，比如 boosting。

- 全 $FS_0$ 路径可以通过 LAR 算法非常有效地计算出来。

- $FS_0$ 系数曲线是微分方程的一个解。

- LASSO在降低系数向量 $\beta$ 的 $L_1$ 范数的 单位残差平方和 增长方面实现了最优化；但 $FS_0$ 在沿着系数路径的 $L_1$ 弧长的单位增长是最优的，因此它的系数曲线不会经常改变方向。？？？

- $FS_0$ 比 LASSO的约束更强。$FS_0$ 可能在 $p\gg N$ 情形下很有用，它的系数曲线会更加的光滑，因此比LASSO有更小的方差。

  

##### Piecewise-linear path algorithms

略

##### The dantzig selector

$\min_{\beta}\|\beta\|_1$ subject to $\|X^T(y-X\beta)\|_{\infty} \le s$

可以等价地写成

$\min_{\beta} \|X^T(y-X\beta)\|_\infty$ subject to $\|\beta\|_1\le t$.



$L_\infty$ 范数：该向量中绝对值最大的组分

类似 LASSO，用梯度绝对值的最大值替换平方误差损失。当 $t$ 变大，如果 $N < p$，则两个过程都会得到最小二乘解。如果 $p\ge N$，它们都得到最小的 $L_1$ 范数的最小二乘解。

DS 可能得到非常不稳定的系数曲线，不太好，略。
