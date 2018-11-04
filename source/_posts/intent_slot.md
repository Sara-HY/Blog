---
title: Review on Intent Classification and Slot Filling
date: 2018-11-02 10:41:02
tags: Research
---

自然语言理解（Natural Language Understanding, NLU）是NLP领域的一个分支，在自然语言理解的过程中，首先就是对意图（Intent）分类，然后接着对槽位（Slot）填充。

<!--more-->

意图分类时一个典型的文本分类的问题，常用的方法如下：
- 基于规则的方法
 用户人工定义一些匹配规则进行分类。
- 机器学习的方法
 SVM, Decision Tree等等。
- 深度学习的方法
 目前更加推崇使用 End-to-End 的网络进行分类。

最近收集了一些关于意图分类以及槽填充的相关的数据集以及对应的测试指标。

## 中文数据集

### [NLPCC 2018 Task4](http://tcci.ccf.org.cn/conference/2018/taskdata.php) - Spoken Language Understanding in Task-Oriented Dialogue Systems

#### 数据描述
这个数据集来源于某车载产品的真实日志数据，主要涉及音乐，导航以及打电话等等领域，11种意图以及15种槽值类型。其中包括 **5.8K** 次会话，总共有 **26K** 次叙述（Utterance）。特别地，这个数据集仅仅包含了用户的输入（没有系统的回复），并且针对错误的槽值进行了修正，如将“什话”修正为“神话”。

 - 训练集：4705次会话, 21352次叙述。
 - 验证集：1177次会话, 5350次叙述。 （训练集：验证集 约 4:1）

数据格式
``` bash
session ID    用户query              意图                       语义槽标注
    1           打电话	   phone_call.make_a_phone_call	        打电话
    1	      我想听美观	        music.play	          我想听<song>美观</song>
    1	      我想听什话	        music.play	          我想听<song>什话||神话</song>
```

#### 评估方法
这个比赛主要有两个评估方法:

- 意图分类，评估方法为F1值，具体的计算方法如下：
<div align=center>
	<img src="/images/intent_f1.png" width = "500"/>
</div>

- 意图分类以及槽填充，评估方法是准确度。即意图分类以及所有的槽位都完全正确。

#### 主要算法
总共有16个队伍参加了这个比赛，但是只有两个队伍开源了他们的方法，分别是HLSTM-SLU模型和Sogou团队的模型。具体结果如下：
<div align=center>
	<img src="/images/intent_results.png" width = "500" align=center/>
</div>

##### HLSTM-SLU [1]
这个可以看做是深度学习的方法和传统的机器学习方法相结合。模型结构如下：
<div align=center>
	<img src="/images/intent_hlstm.png" width = "500" align=center/>
</div>

这个模型主要由三个LSTM组成，两个双向LSTM处理输入和输出，一个单向LSTM处理一个会话中的多个叙述。

- 输入Bi-LSTM
 输入：Character Embedding + POS + Domain 
 其中POS表示对每个字进行词性标注，并用类似于BI的方法进行编码；Domain表示不同领域的词，也用BI的方法进行编码，具体事例如下：

<div align=center>
	<img src="/images/intent_input.png" width = "500" align=center/>
</div>

- Session LSTM
 输入：一次对话中的每轮的描述经过输入Bi-LSTM的输出经过最大池化之后的结果。
 输出：**意图的类别**

- 输出Bi-LSTM
 输入：Session LSTM + 输入Bi-LSTM
 输出：**槽位标注**

注：并没有直接使用LSTM的结果作为最终的结果，而是根据 **CRF** 预测最优的序列。

**Trick**: 使用 **over sampling** 解决意图类别中的样本不均衡的问题，并在过程中使用规则识别了一部分小样本的意图。

**结果**：这个模型在两个评估方法的结果最终为94.19%，90.84%。

##### Sogou [2]
这个模型没有使用深度学习的方法，而是使用传统的机器学习中的序列标注方法。首先，他们认为用户的query可以根据是否有显性的意图词分为两类（这一部分主要根据实体词匹配算法得到）。对于有显性意图词语的query，采用**基于规则**的处理的方法进行标注；剩下的部分采用**基于模型**的方法，具体的模型方法分为5步：

1. 对query进行分词和词性标注（POS）。

2. 寻找槽边界：先对处理后的query使用character embedding + word embedding; 根据BILOU原则，使用CRF对其进行序列标注。

3. 槽分类：根据槽边界检测结果的character embedding + word embedding以及词性标注结果POS，通过逻辑回归的方式（Logistic Regression）进行分类。

4. 槽修正：若槽类别预测错误，则根据词之间的相似性寻找真实槽类别中的所有的值与之进行相似度比较，进而修正结果。

5. 意图分类：使用**XGBoost**的方法，根据word embedding，query长度，槽类别进行意图分类。

注：由于训练样本比较少，针对模型预测错误的数据，他们根据比较query与Sogou语音中最匹配的进行替换，最终针对意图分类增加了500个数据，槽填充增加了1000个数据。

**结果**：这个模型在两个评估方法的结果最终为96.11%，94.49%。

## 英文数据集

### Frame

#### 数据描述
这个数据集主要针对航班和酒店预订，来源于基于Wizard-of-Oz(WOz)设定的人机对话的过程（实际上是一个人假扮机器）。其中包括 **1369** 个对话, 总共有 **19986** 轮。

**数据格式**
每一次叙述都包含 'author', 'text', 'labels', 'timestamp', 'frames'('frame id', 'frame parent id', 'requests, binary questions, compare requests', 'info'), 'db'字段。其中 'labels'记录当前的active_frame以及对话过程中的Act(包括act名称以及对应的slot类型和值)， 'info'字段主要为了标注对于槽位值是否为否定的。

**Act类型**：inform, offer, request, switch frame, suggest, no result, thankyou, goodbye.....


#### 评估方法
微软在提出这个数据集的同时，也定义了一个任务Frame Tracking，这个任务与State Tracking不同的是，它可以同时追踪一个frame与之前几轮相关的frame，以及由一个frame转变到多个frame，例如用户要求系统可以推荐4个符合条件的旅行，如下图所示：
<div align=center>
	<img src="/images/intent_frame.png" width = "300" align=center/>
</div>

这个任务就是需要预测是否有新的frame生成。如果有，则预测其目的Act，限制条件Ref Labels以及之前相关的Frame ID，如果预测结果完全匹配，则认为预测正确，最后计算准确度。同时计算总的预测有新的frame生成的叙述个数，计算其识别新frame生成的准确度。

#### 主要算法

##### Baseline [3]
由下图可知模型结构，针对叙述中的每个词，将其表示为trigrams的形式，然后通过一个embedding层，tanh激活层。针对Act分类和Slot分类，分别用一个双向的GRU实现，输入为每个词在激活层的输出。最后经由一个softmax分类层得到最终的类别。
<div align=center>
	<img src="/images/intent_frame_baseline.png" width = "300" align=center/>
</div>

**结果**：这个模型在两个评估方法的结果最终为：frame识别准确度0.24 ± 0.02, frame新建识别准确度为0.49 ± 0.03。

<!-- ##### Frame Tracking Model for Memory-Enhanced Dialogue Systems [4]
微软的团队随后提出了一个新的模型来处理这个问题。

<div align=center>
	<img src="/images/intent_frame_model.png" width = "400" align=center/>
</div>

首先是对输入的预处理：
- Token Encoding

	

**结果**：这个模型在基于槽分类的准确度为76.43 ± 4.49，基于行动Act分类的准确度为95.66 ± 2.34。



### DSTC

#### 数据描述

#### 评估方法

#### 主要算法

##### lala -->


[1] Learning Dialogue History for Spoken Language Understanding.
[2] The Sogou Spoken Language Understanding System for the NLPCC 2018 Evaluation.
[3] Frames: A Corpus for Adding Memory to Goal-Oriented Dialogue Systems.
<!-- [4] A Frame Tracking Model for Memory-Enhanced Dialogue Systems -->





























