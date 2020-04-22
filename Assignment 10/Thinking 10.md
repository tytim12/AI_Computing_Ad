#### Thinking 1：电商定向广告和搜索广告有怎样的区别，算法模型是否有差别

| 区别项       | 电商定向广告                                     | 搜索广告                   |
| ------------ | ------------------------------------------------ | -------------------------- |
| 用户意图     | 没有明确意图                                     | 主动搜索                   |
| 用户目标     | 没有明确目标                                     | 有明确目标                 |
| 算法模型差别 | 通过历史行为进行推荐                             | 更关注搜索排序，关键词匹配 |
| 算法模型举例 | LR -> GBDT+LR -> MLR -> DNN(DIN -> DIEN -> DSIN) | 也有LR，GBDT+LR, PageRank  |



#### Thinking 2：定向广告有哪些常见的使用模型，包括Attention机制模型

一般公司初期会通过 LR、MLR、GBDT + LR、DNN 模型等方式进行定向广告

近几年阿里则是结合了 DNN 和 Attention机制，推出了 DIN、DIEN 和 DSIN 进行定向推广。





#### Thinking 3：DIN中的Attention机制思想和原理是怎样的

**Attention的思想**是在pooling的时候，与 candidate Ad 相关的商品权重就设置大一些，不相关的就设置小一些。

**执行机制**是把用户的历史行为特征进行 embedding 操作，视为用户的兴趣表示，然后通过 attention unit 对每个兴趣进行赋权。

**场景描述：**

在预测多兴趣用户的时候，用户对大部分的兴趣和 candidate Ad 都是没有关系的，所以预测时候应该考虑和商品相关的局部兴趣。受到 Attention 机制的启发，DIN网络引入了局部兴趣激活单元，捕捉用户的局部兴趣，然后通过 embedding 和根据历史行为计算不同的权重，最后通过加权sum pooling的方式得到跟candidate ad相关的兴趣表达向量



#### Thinking 4：DIEN相比于DIN有哪些创新

考虑到了用户兴趣的动态变化性，DIEN 增加了兴趣抽取层（interest extractor layer），用于从用户的历史行为序列中捕捉短期的兴趣点，同时增加了辅助损失函数auxiliary loss，用来额外监督学习的每一步兴趣点抽取（用下一时刻的行为监督当前时刻兴趣的学习，使GRU在提炼兴趣表达上更准确）。



#### Thinking 5：DSIN关于Session的洞察是怎样的，如何对Session兴趣进行表达

DSIN把用户的行为切分的更细，按照 session 的视角洞察用户行为。论文认为从 session 的角度看，组内行为是类似，而组间是存在差异。DSIN 通过对行为序列进行切片成为session，然后使用带有 bias encoding 的 self-attention 机制提取用户向量，再通过Bi-LSTM对session之间的交互进行建模，输出带有上下文信息的兴趣的session向量，最后再利用 activation unit 自适应地学习各种绘画兴趣对目标item的影响



#### Thinking 6：如果你来设计淘宝定向广告，会有哪些future work（即下一个阶段的idea）

DSIN考虑到的session是按照固定时间进行行为序列的切片，那么很有可能在切片的时候会使不同session间的兴趣有一定程度的混合。如果要对session进行优化，可能可以考虑怎么把session内的方差缩小、session间的方差增大表现差异性。也就是尝试让捕捉兴趣演化的过程更精确。

针对session以外：

1. 方向1：可以考虑尝试模型的横向扩展，比如激活兴趣表示向量后，喂到GBDT之类的树模型中抽取特征，再喂到MLP中。
2. 方向2：结合GCN类的图模型，提取浏览行为的长中短期特征进行进一步的结合分析，喂进模型中。