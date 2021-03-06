#### Thinking 1：关联规则中的支持度、置信度和提升度代表的什么，如何计算

支持度：某个商品组合出现的次数 / 样本总数，支持度越高代表出现频率越大

置信度：买商品A的同时，买商品B的概率， P(B|A)

提升度：A对B的提升度 = A对B的置信度 / 支持(B)



#### Thinking 2：关联规则与协同过滤的区别

关联规则：基于订单交易内容计算频率、频次、或概率等

协同过滤：基于用户偏好的分析（用户评分）



#### Thinking 3：为什么我们需要多种推荐算法

不同算法考虑的场景不一样，当考虑当前的需求的时候，那就只需要短期的行为记录，而需要考虑用户长期偏好的时候则需要对历史行为进行挖掘分析。通过多维的视觉综合起来的结果进行混合推荐，效果会更好。



#### Thinking 4：关联规则中的最小支持度、最小置信度该如何确定

最小支持度和最小置信度都是通过实验得出的。

最小支持度可能是0.01到0.5之间，最小置信度可能是0.5到1之间，可以从高到低输出前20个项集的支持度作为参考



#### Thinking 5：如何通过可视化的方式探索特征之间的相关性

非欧数据可以通过图的方式寻找邻近关系；分类特征可以进行groupby后查看与连续变量之间的关系（方差分析求组间差异系数），两分类变量之间可以进行相关性分析（卡方分布？）



#### （ppt）Thinking 5：TFIDF的思想

如果某个term在一篇文档中出现的次数很高（TF），但是在别的文档中出现的次数很低（IDF），那么这个term就具有比较好的分类能力进行文档的区分。