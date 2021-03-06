# 《深度学习》阅读笔记

## Chap4 (Pages 57-58)

1. Hessian矩阵是实对称的，可以将其分解为一组实特征值和一组特征向量的正交基，在特定方向d上的二阶导数可以写成d'Hd，当d是H的一个特征向量时，这个方向的二阶导数就是对应的特征值。对于其他方向d，方向二阶导数是所有特征值的加权平均，权重在0-1之间，且与d夹角越小的特征向量权重越大。最大特征值确定最大二阶导数，最小特征值确定最小二阶导数；
2. 通过泰勒近似，得到使得近似泰勒级数下降最多的最优步长为：$\epsilon^* = \frac{ \Vg^\Tsp \Vg}{ \Vg^\Tsp \MH  \Vg}$，最坏的情况下，g与H最大特征值对应的特征向量对齐，则最优步长为1/lambda_max，因此Hessian的特征值决定了学习率的量级；
3. 二阶导数能够用来判断局部极大、极小点以及鞍点；
4. 在临界点处，Hessian是正定的，代表是局部极小点，Hessian是负定的（所有特征值都是负的），代表是局部极大点。
