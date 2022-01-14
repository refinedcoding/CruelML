# 《深度学习》阅读笔记

## Chap4 (Pages 58-62)

1. 仅仅使用梯度信息的优化算法称为一阶优化算法，例如梯度下降；使用Hessian矩阵的优化算法称为二阶最优化算法，例如牛顿法；
2. 深度学习背景下，限制函数满足Lipschitz连续或者其导数Lipschitz连续可以获得一些保证。Lipschitz连续函数的变化速度以Lipschitz常数L为界；
3. 凸优化只对凸函数适用，即Hessian处处半正定的函数，这些函数没有鞍点而且所有局部极小点必然是全局最小点；
4. 约束优化：KKT方法（Karush-Kuhn-Tucker），为每个约束引入新的变量：KKT乘子，$L(\Vx, \Vlambda, \Valpha) = f(\Vx) + \sum_i \lambda_i g^{(i)}(\Vx)  + \sum_j \alpha_j h^{(j)}(\Vx)$；
