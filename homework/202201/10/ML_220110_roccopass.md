# 论文阅读笔记

《Hierarchical Adaptive Temporal-Relational Modeling for Stock Trend Prediction》

https://www.ijcai.org/proceedings/2021/0508.pdf

## Highlights:

1. 两个模块用来预测，第一个是传统的量价数据（开高低收），第二个是股票间的关系（图神经网络，例如个股行业概念、控股股东关系等）；
2. 对于开高低收等量价数据，先使用了attention算法，后续对stock_ID进行embedding也是亮点，其中Multi-Scale Temporal Representation用来挖掘因子在时序上不同时间长度的信息（例如日频、周频、月频等），Hawkes process用来挖掘时间尺度上的信息，做到了time和scale两个维度上的dual attention； 
3. 图神经网络这块没有太多亮点，就是比较常见的diffusion graph convolution。
