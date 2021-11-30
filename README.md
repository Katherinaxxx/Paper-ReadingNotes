[TOC]

## Bilingual Alignment Pre-Training for Zero-Shot Cross-Lingual Transfer (MRQA 2021)
* 论文地址：https://arxiv.org/abs/2106.01732
* 主要内容：多语言预训练模型在跨语言任务上取得了惊人的效果。在这类任务中，模型利用源语言的训练集训练，在目标语言的测试集上测试。在预训练阶段即便不借助平行语料，而仅通过MLM自监督训练，模型也可习得跨语言zero-shot能力。而如果使用双语平行语料，跨语言zero-shot效果能得到进一步的提升。本次分享将先回顾现有的双语平行语料预训练对齐技术，然后介绍我们提出的双语对齐预训练模型 Word- Exchange Aligning Model (WEAM)：**使用统计对齐信息作为先验知识，训练模型使用一种语言的上下文表示预测另一种语言中的token**。实验表明，WEAM不仅在下游任务上提升了跨语言迁移性能，从多语言词向量相似度的角度看其词向量表示也优于baseline。

* 多语言预训练模型
模型结构相同，训练数据多个语言语料
  * 特点
    * **跨语言能力**
    * 减少开发维护
  * setting
    * supervised：与单语言类似
    * **zero-shot**：在一种语言上训练，在其他语言上测试
    * few-shot
  * mbert
    跨语言能力研究结论：1）每层有区分语言的能力；2）更容易泛化到相似语法的语言

* 双语预训练模型
  * XLM’： +TLM（平行句对，随机mask任一词）
  * infoXLM： +TLM +XLCo（平行句子表示拉近，非平行句子表示拉远）
  * ERNIE-M： +TLM +CAMLM +BTMLM

* 多语言预训练模型中的对齐
  * 拉近翻译词对的表示（相似度）+ 与为对齐模型做正则化（防止学成同一个词的表示）
  * 隐式vs显式
  * 动态（hidden）vs静态（embedding）
  * 预训练vs微调

* Bilingual Alignment Pre-Training for Zero-Shot Cross-Lingual Transfer (MRQA 2021)
**WEAM**
![](figs/WEAM.jpg)




## 中文拼写纠错最新进展

### 任务
* 错字：字形
* 别字：字音字形字义

### 研究切入点
* 模型
  * 编码：pretrain阶段引入额外信息、模型结构
  * 解码：混淆集
* 数据：高质量伪数据

### 生成对抗样本

### 半监督课程学习

由易到难，选择困难样本加入训练

### global attention decoder （GAD）

解决相邻字错误导致中间的错误改不了 - GAD（候选做attention）

### spellbert


## Masked Autoencoders Are Scalable Vision Learners [by何恺明]

* motivation

AE用在nlp效果不好：
1）cnn对mask token和position embedding的处理不好
2）mask用在图像上，可以较容易从周围点推理出来

* method

![MAE](figs/MAE.png)

encoder：（有position embedding）随机打乱（无序）mask大量（eg.后75%）,对没有mask的部分编码。

decoder：还原回去

损失：重构损失mse

* thoughts

用在图像领域效率还是存在问题的吧
