# 《深度学习》阅读笔记

## Chap1-3 (Pages 1-51)

1. **logistic sigmoid**函数：$\sigma(x) = \frac{1}{1+\exp(-x)}$ 可以用来产生伯努利分布中的参数$\phi$;
2. **softplus**函数：$\zeta(x) = \log(1+\exp(x))$ 可以用来产生正态分布中的参数$\sigma$;
3. 上面这两个函数的一些导数关系，太难记了，见花书P44 P45；
4. 定义一个事件$x=x$的自信息为$I(x) = -\log P(x)$，自信息只处理单个输出，用香农熵来对整个概率分布中的不确定性进行量化：$H(\RSx) = \SetE_{\RSx \sim P}[I(x)] = -\SetE_{\RSx \sim P}[\log P(x)]$，即是自信息的期望；
5. 用KL散度来衡量两个分布的差异：$D_{\text{KL}}(P||Q) = \SetE_{\RSx \sim P} \left [  \log \frac{P(x)}{Q(x)} \right ] = \SetE_{\RSx \sim P} [\log P(x) - \log Q(x)]$, 即为自信息差的期望，注意到KL散度是不对称的
6. KL散度非负，当KL散度为0，说明两个分布在离散型情况下是相同的，或者在连续型情况下是几乎处处相同，KL散度去掉左边项即为交叉熵：$H(P, Q) = -\SetE_{\RSx\sim P} \log Q(x)$;
7. 结构化概率模型用有向图或者无向图来解释。
