# 论文阅读笔记

《DoubleEnsemble: A New Ensemble Method Based on Sample Reweighting and Feature Selection for Financial Data Analysis》

https://arxiv.org/pdf/2010.01265.pdf

## Highlights:

1. 每个ML模型作为子模型，通过样本重赋权与因子选择，来迭代子模型，最后各个子模型分配权重求平均；
2. 因子选择思路：对于一般的机器学习模型，例如树模型与神经网络，如果改变因子的输入维度（改变因子个数，通过直接删去该因子方式实现），需要重新训练，如果简单改变因子的数值（例如全部填0或者平均数或者中位数），改变了分布，不符合实际。作者提出了shuffle方法，将每一天的某一个因子值重新permutation，打散多次取平均值，理论上削弱了该因子的影响；
3. 样本重赋权思路：根据损失函数变化的曲线，将样本分为简单样本、困难样本与噪声样本，目标是给困难样本赋予更高的权重，给简单样本与噪声样本赋予更低的权重，一定程度上解决了金融数据信噪比较低的痛点。
