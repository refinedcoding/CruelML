# ESL: pp 111-120

### LDA

$f_k(x)$: class-conditional density of X in class G = k

$\pi_k$: prior probability of class $k$, $\sum_{k=1}^K\pi=1$



Bayes theorem得

$\Pr(G=k|X=x)=\frac{f_k(x)\pi_k}{\sum_{\ell=1}^K f_\ell(x)\pi_\ell}$

就判别能力(ability to classify)而言 ，知道 $f_k(x)$ 等于知道概率 $\Pr(G=k|X=x)$



假设每个类别密度用多元高斯分布来建模，则

$f_k(x)=\frac{1}{(2\pi)^{p/2}|\Sigma_k|^{1/2}}exp\{-\frac{1}{2}(x-\mu_k)^T\Sigma_k^{-1}(x-\mu_k)\}$.



假设类别有相同的协方差矩阵 $\Sigma_k=\Sigma$，得到LDA，比较两个类别时，比较 log-ratio：

$\log\frac{\Pr(G=k|X=x)}{\Pr(G=\ell|X=x)}=\log\frac{f_k(x)}{f_{\ell}(x)} + \log\frac{\pi_k}{\pi_\ell}\\
=-\frac{1}{2}(\mu_k+\mu_l)^T\Sigma^{-1}(\mu_k-\mu_l)+x^{T}\Sigma^{-1}(\mu_k-\mu_\ell)+\log\frac{\pi_k}{\pi_\ell}$



实际中，我们不知道高斯分布的参数，需要用训练数据去估计它们：

- $\hat\pi_k=N_k/N$: $N_k$ 是第 k 类观测值的个数
- $\hat\mu_k=\sum_{g_i=k}x_i/N_k$
- $\hat\Sigma=\sum_{k=1}^K\sum_{g_i=k}(x_i-\hat\mu_k)(x_i-\hat\mu_k)^T/(N-K)$



如果满足

$x^T\hat\Sigma^{-1}(\hat\mu_2-\hat\mu_1)>\frac{1}{2}(\hat\mu_2+\hat\mu_1)^T\hat\Sigma^{-1}(\hat\mu_2-\hat\mu_1)-\log(N_2/N_1)$

则分给第二类，否则分给第一类



- 通过最小二乘得到的 LDA 方向不需要对特征做高斯分布的假设，它的应用可以不局限于高斯分布的数据。



如果没有假设$\Sigma_k$ 相等，则关于x的平方项保留，得到平方判别函数QDA

$\delta_k=-\frac{1}{2}\log|\Sigma_k|-\frac{1}{2}(x-\mu_k)^T\Sigma_k^{-1}(x-\mu_k)+\log\pi_k$.

细节略

LDA 和 QDA 在非常大以及离散的数据集的分类上面表现得很好 。

```
为什么 LDA 和 QDA 有那么好的效果？

原因[不可能]是数据近似服从高斯分布，对于 LDA 协方差矩阵也不可能近似相等．

很可能的一个原因是数据仅仅可以支持简单的判别边界比如线性和二次，并且通过高斯模型给出的估计是[稳定]的，这是一个偏差与方差之间的权衡——我们[可以忍受线性判别边界的偏差]因为它可以通过用比其它方法[更低的方差]来弥补
```

TODO


