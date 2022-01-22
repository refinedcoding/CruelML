# ESL: pp 51 - 60

#### The Gauss-Markov Theorem

The least squares estimates of the parameter $\beta$ have the smallest variance among all linear unbiased estimates

=> Restriction to unbiased estimate is not necessarily a wise one.



Consider linear combination of param, $\theta=a^T\beta$.

Prediction: $f(x_0)=x_0^T\beta$

Then $\hat{\theta}=a^T\hat\beta=a^T(X^TX)^{-1}X^Ty$

If the linear model is correct, then $a^T\hat\beta$ is unbiased. 

$E(a^T\hat\beta)=E(a^T\hat\beta=a^T(X^TX)^{-1}X^Ty) = a^T(X^TX)^{-1}X^TX\beta=a^T\beta$.

**Gauss-Markov Theorem**

- 如果$a^T\beta$ 存在其他无偏估计  $\hat{\theta}=c^Ty$ ，即 $E(c^Ty)=a^T\beta$, 则
  - $Var(a^T\hat\beta)\le Var(c^Ty)$.



Mean squared error of an estimator $\tilde\theta$:

- $MSE(\tilde\theta)=E(\tilde{\theta}-\theta)^2=Var(\tilde{\theta})+[E(\tilde{\theta})-\theta]^2$.
- Least square estimate 保证的是在无偏的情况下，有最小的MSE，但是其实存在着 trade a little bias for a larger reduction in variance 的情况。

- 任何收缩或者将最小二乘的一些参数设为 0 的方法都可能导致有偏估计



TODO 

#### Multiple Regression from Simple Univariate Regression

#### Multiple Outputs



### Subset Selection

有时不选最小二乘法的原因

- prediction accuracy: low bias but large variance. 有时可以通过shrink或者令某些系数为0 来提高准确性。
- interpretation: 可解释性。有大量predictor的时候，通常只选择少部分。



#### Best-Subset Selection

对于每个 $k\in\{0,1,...,p\}$ ，要找出residual sum of squares of subset with size k。算法 *leaps and bounds* 可以支持 p到 30-40。residual sum of squares必然随着k增大而降低，所以怎么选 k涉及 bias 和 variance的trade-off.



#### Forward- and Backward-Stepwise Slection

Forward-stepwise selection:

- 从截距开始，向模型中依次添加最大程度提升拟合效果的预测变量

- 相当于一个Greedy算法
- 计算快，可能有更低的方差，但或许有更大的bias

Backward-step selection:

- 从整个模型开始，并且逐步删掉对拟合影响最低的预测变量。要删掉的候选变量是 Z 分数最低的变量。

- converge得快

