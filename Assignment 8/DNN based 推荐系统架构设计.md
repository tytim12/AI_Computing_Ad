DNN based 推荐系统：

1. 召回阶段：使用LBS或协同过滤类召回策略，先召回 Top N 目标
2. 排序模型：
   1. 提取 user 和 item 特征，分别输入 FM 和 GBDT 层，输入FM和GBDT的数据集一样，初步共享输入
   2. FM层和DeepFM处理方法一样
   3. GBDT层与GBDT+LR前半段的方式一样，提取GBDT结果的树节点参数数据（不是预测结果）
   4. GBDT结果进入DNN单元
   5. 最后FM结果和DNN单元结果共同经过输出单元（sigmoid）



![DNN模型图](/DNN模型图.jpg)