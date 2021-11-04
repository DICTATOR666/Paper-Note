# Title：Go and no-go learning in reward and punishment: Interactions between affect and effect

[https://doi.org/10.1016/j.neuroimage.2012.04.024](https://doi.org/10.1016/j.neuroimage.2012.04.024)

## 实验目的

受试者在学习奖励条件下的主动选择和惩罚条件下的被动选择方面要成功得多。利用计算性强化学习模型，我们把在学习过程中观察到的不对称性的产生，从所谓的工具性和巴甫洛夫成分中分离出来。

## 前言

最佳决策要求：最大化奖励和最小化惩罚。动物为做出最佳决策衍生出两大类机制：Pavlovian，instrumental。二者通常倾向相同选择，但在二者矛盾时，基本工作原则被次优性揭示。<br />次优性的一个来源——两个逻辑上独立的行为控制轴实质性相互依赖。<br />实验设计中行动和价值完全正交。<br />研究巴甫洛夫对去和不去选择的工具性学习的影响，以使收益最大化和损失最小。<br />假设：最佳行动选择（去或不去）的学习会受到选择结果价值的影响。<br />神经基础：纹状体和SN/VTA激活强度。

## 被试

47名被试，17名在室外实验，30名在扫描仪内实验。均为右撇子，视力正常。

## 实验设计和任务

每个试次由三个事件组成：分形线索、目标检测任务、概率结果。<br />每个试次中，被试看到四个抽象分形线索（提示被试该做的正确反应）中的一个，时间为1000ms。之后间隔250~2500ms后，进行目标检测任务。目标在屏幕一侧显示圆形，持续1500ms，被试有1000ms进行反应，选择了正确的一面被归类为“go”，反之为“nogo”。<br />圆形消失后1000ms，被试会看到结果，结果显示1000ms，绿色向上箭头表示赢1英镑，红色向下箭头表示输1英镑，黄色横线表示没有赢也没有输。<br />

![](https://cdn.nlark.com/yuque/0/2021/jpeg/22171666/1635956404173-1ce5b597-2c0a-41ef-a199-ddf5f69e513a.jpeg#clientId=u48d48205-688e-4&from=drop&id=u6afa49e8&margin=%5Bobject%20Object%5D&name=Guitart%202012%20Figure1.jpg&originHeight=594&originWidth=814&originalType=binary&ratio=1&size=76873&status=done&style=none&taskId=u696c8a5d-83d3-4bfe-bdaf-a87a51af19b)

## 行为数据分析

三因素重复测量方差分析：时间、行为反应（go/nogo）、效价（win/lose）。

## 强化学习模型

主要目的是求得action weight即$W\left(a_{t},s_{t}\right)$的值。<br />代入下式求得某个动作的概率：

$$
p\left(a_{t} \mid s_{t}\right)=\left[\frac{\exp \left(W\left(a_{t} \mid s_{t}\right)\right.}{\sum_{a^{\prime}} \exp \left(W\left(a^{\prime} \mid s_{t}\right)\right)}\right](1-\xi)+\frac{\xi}{2}
$$


在上述公式中，$\xi$是噪音，在RW模型里是0，其他模型里是自由参数。

模型的一个区分是action weight如何得出，在RW和RW + noise里，$W \left(a,s \right) = Q\left(a,s \right)$，$Q$的更新通过类Rescorla-Wagner更新公式得出：

$$
Q_{t-1} \left(a_{t}, s_{t} \right) + 
\xi \left(\rho r_{t} - 
Q_{t-1} \left(a_{t}, s_{t} \right) \right)
$$


在上述公式中，$\xi$是学习率，$r_{t} \in \left\{-1,0,1 \right\}$是该试次得到的奖励，$\rho$是被试对于奖励感知的自由参数。

在RW（rew/pun） + noise + bias模型里，参数$\rho$在获得奖励或者收到惩罚的试次中可以不同，但是在其他模型里，每个被试对应一个$\rho$值，这表明其他模型将失去奖励与得到惩罚等价。
