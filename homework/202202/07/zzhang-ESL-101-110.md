# ESL: pp 101-110

## Linear Methods for Classification

#### Introduction

判别边界 decision boundaries

- 第 $k$ 类和第 $l$ 类的判别边界是满足 $\hat f_k(x)=\hat f_\ell (x)$ 的点的集合 $\{x:(\hat\beta_{k0}-\hat\beta_{\ell0})+(\hat\beta_k-\hat\beta_\ell)^Tx=0\}$ 超平面。

- 输入空间被分块超平面判别边界分成了若干个类别区域

- 回归方法对每个类别建立 判别函数 (discriminant function) $\delta_k(x)$，将 $x$ 分到取最大的判别函数所在类别中。

只要$\delta_k(x)$ 是关于$x$ 线性的，则判别边界也将是线性的。



#### Linear Regression of an Indicator Matrix

$K$ 个类别，$Y_k\in\{0,1\}$.

$N$ 个 training sample

$Y\in\{0,1\}^{N\times K}$: indicator response matrix

对 $Y$ 的每一列同时用线性回归模型做拟合得到：

- $\hat{Y}=X(X^TX)^{-1}X^TY$
- 对每一个预测变量 $Y_k$ 有系数矩阵$\hat B=(X^TX)^{-1}X^TY$. $X$ 有 p + 1列，p个输入加截距1.



对$x$ 进行分类：

1. 计算拟合值$\hat f(x)^T=(1,x^T)\hat B$

2. 确定分类 $\hat G(x)=\arg\max_{k\in\mathcal{G}}\hat f_k(x)$

- $\hat f_k(x)$  可以是负数或者比 1 大 (线性回归刚性本质 (ridge nature) )





#### LDA: Linear Discriminant Analysis 🌟🌟

TODO
