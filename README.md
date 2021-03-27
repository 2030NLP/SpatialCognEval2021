# 空间认知能力评测2021



---

#### 关键信息

> 这部分内容是用于CCL2021评测总览页面的简要介绍。

- **任务名称**：空间认知能力评测——中文空间语义的正误判别与归因
- **任务简介**：
  - 语言交际中存在大量的空间信息，理解这些信息是非常重要的。对文本中空间信息的理解，不仅需要掌握句段中字词的语义，还需要具备一定的常识或世界知识，甚至是超出语言范畴的空间想象等认知能力。对机器进行空间认知能力的评测，需要系统化的考察。为此，北京大学与复旦大学的研究团队组织了此次“中文空间语义的正误判别与归因”评测任务，作为对机器“空间认知能力评测”的初步尝试。
  - 如果机器具备了空间认知能力，那么它不仅要能够识别常规、正确的空间信息，还应该能够识别异常、错误的空间信息。这些异常包括：跟空间语义理解有关的词语搭配问题、上下文信息冲突问题、与常识冲突的问题等。对于不同层面的异常原因，可能需要进行不同的后续处理，因而在识别异常之后，对于异常原因的解释也很重要。基于上述观点，本次评测设置了三个任务来考察计算机的空间认知能力，分别是：
    - 子任务1，中文空间语义正误判断。 
    - 子任务2，中文空间语义异常归因合理性判断。
    - 子任务3，中文空间语义判断与归因联合任务。
- **委员会**
  - 单位：北京大学，复旦大学
  - 主席：詹卫东，穗志方（北京大学）；邱锡鹏（复旦大学）
  - 委员：孙春晖，唐乾桐，秦梓巍，董青秀（北京大学）；李孝男（复旦大学）等
- **联系方式**：sc_eval@163.com
- **总奖金**：40000元（华为公司赞助）
- **任务网址**：https://github.com/2030NLP/SpatialCognEval2021

---

#### 一、任务简介

语言交际中存在大量的空间语义信息，理解这些信息是非常重要的。著名认知语言学家Jackendoff在其概念语义学理论中也指出空间结构是语言系统的四种基本结构之一（其余三个层面：语音、句法、概念语义）<sup>**`1`**</sup>。

通常认为，对文本中空间信息的理解，不仅需要掌握句段中字词的语义，还需要具备一定的常识或世界知识，甚至是超出语言范畴的空间想象等认知能力。那么，对于机器的空间认知能力，应该如何评估？这一问题需要系统化的考察。为此，北京大学与复旦大学的研究团队组织了此次“中文空间语义的正误判别与归因”评测任务，作为对机器“空间认知能力评测”的初步尝试。

如果机器具备了空间认知能力，那么它不仅要能够识别常规、正确的空间信息，还应该能够识别异常、错误的空间信息。如对于“在四面签一个名字”，人类能够意识到其中存在异常，因为“一个名字”通常不会签在“四面”；又如对于“走过火车下”，人类能够清楚地知道通常不会有人在火车的“下”方走路。可以看出，这些异常是多种多样的，具体包括：跟空间语义理解有关的词语搭配问题、上下文信息冲突问题、与常识冲突的问题等。对于不同层面的异常原因，可能需要进行不同的后续处理，因而在识别异常之后，对于异常原因的解释也很重要。

基于上述观点，本次评测试图考察计算机的以下能力：（1）计算机能否正确区分正常与错误的空间语义表达；（2）计算机能否解释空间语义表达错误的原因；（3）计算机处理上述两个任务的综合能力。对应为如下三个任务：

**子任务1，中文空间语义正误判断**：要求参赛系统对给定的中文文本中是否存在空间关系异常加以判断。

**子任务2，中文空间语义异常归因合理性判断**：要求参赛系统判断给定的归因是否可以用来解释给定的中文文本中所存在的空间关系异常。这些异常被分为词语搭配问题、语义问题、语境问题、常识问题以及其他问题（详情请看后文介绍）。

**子任务3，中文空间语义判断与归因联合任务**：参赛系统首先需要判断给定的中文文本中是否存在空间关系异常，如果存在异常，则再判断所给定的归因是否可以用来解释这一异常。

---

#### 二、数据介绍

数据以json格式发布（参见后附数据样例），各个字段说明如表1所示。

> **表1    数据字段说明**
>
> | 字段      | 类型   | 说明                                                         |
> | --------- | ------ | ------------------------------------------------------------ |
> | `qID`     | int    | 试题编号。                                                   |
> | `context` | string | 文本材料。                                                   |
> | `reason`  | string | 子任务2及子任务3中，对文本材料中空间关系异常的归因。         |
> | `judge1`  | bool   | 子任务1中，对文本是否存在空间异常的判断。`true`表示句子成立，无异常；`false`表示句子不成立，有异常。 |
> | `judge2`  | bool   | 子任务2及子任务3中，对归因是否能够解释材料的空间关系异常的判断。`true`表示归因成立；`false`表示归因不成立。 |

评测任务中的语料主要来源于CCL语料库，涵盖小说、散文、词典等文体。需注意实际使用的文本材料是在原始语料的基础上，替换了具有空间方位意义的词语之后，再进行人工标注和检验后得到的。最终得到7782段有效文本材料，合计86万字。各段材料字数的平均值为110.52，标准差为53.00。这些材料根据性质和任务需要被划分至评测的三个任务的不同数据集中，具体分布情况如表2所示<sup>**`2`**</sup>。

> **表2    各子任务的数据集分布情况**
>
> | 子任务                            | 训练集 | 验证集 | 测试集 | 总计  | 备注                                                         |
> | --------------------------------- | ------ | ------ | ------ | ----- | ------------------------------------------------------------ |
> | 1、中文空间语义正误判断           | 4k+    | 800~   | 800~   | 5.6k+ | 三个数据集之间，所使用的原始语料没有交集，下同。             |
> | 2、中文空间语义异常归因合理性判断 | 8k+    | 2.5k+  | 2.5k+  | 14k+  | (1)任一数据集所使用的`context`与子任务1的验证集和测试集无交集。(2)训练集使用的`context`与子任务1的训练集有交集。 |
> | 3、中文空间语义判断与归因联合任务 | 0      | 1k+    | 1k+    | 2.5k~ | (1)不提供训练集。(2)验证集和测试集中使用的`context`与子任务1的相应数据集相同。 |

在子任务2及子任务3中，使用了多种归因类型。类型之间并不完全独立，每段材料可能对应多种归因类型。参赛系统不需要在归因类型之中做选择，而只需要判断所提供的类型是否适合用来解释材料中的错误。各类型的简介及其在子任务2中的数量如表3所示。每种类型的具体数据样例请看文后附加材料。

> **表3    归因类型说明**
>
> | 类型     | 内部编号 | 描述                                                         | 形式（例）                                 | 在子任务2中的数量 |
> | -------- | -------- | ------------------------------------------------------------ | ------------------------------------------ | ----------------- |
> | 搭配问题 | A        | `text1`、`text2`不能搭配，主要是因为语法、韵律、习惯等因素，通常不会这样说，而不是因为它们语义不兼容。 | “`[text1]`”和“`[text2]`”不宜搭配           | 5000+             |
> | 语义问题 | B        | `text1`、`text2`通常不一起使用，主要是因为它们语义通常不兼容，而不是因为语法、韵律、习惯等因素。 | “`[text1]`”和“`[text2]`”语义冲突           | 4300+             |
> | 语境问题 | C        | `text1`、`text2`之间存在冲突，主要是因为在当前语境中，具体信息存在冲突，而不是因为二者语义不兼容。 | “`[text1]`”与上下文“`[text2]`”存在信息冲突 | 2200+             |
> | 常识问题 | D        | `text1`所描述的内容不符合常识，这个常识由`commonsense`描述。 | “`[text1]`”与常识不符[：`[commonsense]`]   | 2000+             |

---

#### 三、评价标准

对于**子任务一**和**子任务二**，使用准确率（Acc，Accuracy）作为评价指标。

```
Acc = 命中正确答案的题数 / 题目总数
```

对于**子任务3**，使用F1值作为评价指标。公式如下，其中 *P* 、 *R* 分别代表准确率（Precision）和召回率（Recall）：


$F_1=\frac{2 * P * R}{P+R}$

*P* 和 *R* 的计算公式如下，其中 *TP* 、 *TN* 、 *FP* 、 *FN* 分别代表命中数量、正确拒绝数量、误报数量、漏报数量，下标表示`judge`所属的步骤。


$P=\frac{TP_2}{TN_1 + FN_1}$


$R=\frac{TP_2}{TN_1 + FP_1}$



注意上面公式中 *TP_2* 只计算`judge1`判断为`false`，且`judge1`和`judge2`都判断正确的情况。

**最终排名**：在所有参赛队伍的评测结果产生之后，计算每个任务下各个队伍的标准分数（Z-score），对三个任务的标准分数取平均，作为最终排名的依据。标准分数计算公式如下，其中 *X̄* 为平均数， *s* 为标准差：

$Z = \frac{(X - \overline{x})}{s}$




##### 基线系统

我们将提供一个基线系统供参赛队伍参考，该系统将于4月5日发布。

---

#### 四、预计赛程

- 评测开始（2021年4月1日）
  - 发布报名系统，开放报名
  - 发布训练集以及不带答案的验证集
  - 发布排行榜页面、结果提交页面
- 第一阶段（2021年4月5日—2021年6月18日，近3个月）：
  - 发布基线系统
  - 参赛者需要提交验证集结果，排行榜按验证集成绩排序
  - 参赛者每周可提交3次模型，排行榜每天更新
  - 此阶段可以不提交模型
- 第二阶段（2021年6月19日—2021年7月16日，约1个月）：
  - 此阶段开始的同时，报名截止
  - 发布验证集的答案以及不带答案的测试集
  - 参赛者需要提交测试集结果，排行榜按测试集成绩排序
  - 参赛者每周可提交3次模型，排行榜每天更新
  - 此阶段不提交模型视为弃权
- 第三阶段（2021年7月16日—2021年7月20日，共5天）：
  - 参赛者选择1个模型作为最终参赛模型提交
  - 此阶段不提交模型视为弃权
- 总结回顾阶段（2021年7月23日—2021年8月15日）
  - 公布结果并邀请优秀评测单位撰写技术报告（2021年7月23日）
  - 技术报告收取截止（2021年7月23日）
  - CCL 2021评测研讨会（2021年8月13日—2021年8月15日）

---

#### 五、报名方式

请填写在线报名表： [点击此链接填写报名表](https://docs.qq.com/form/page/DRGFXVmVEUG9DbnV0) 。

请注意：

1. 报名时间：2021年4月1日至2020年6月19日；
2. 一个团队只需由负责人或联系人填写一次报名表单即可；
3. 主办方会在每个工作日检查新的报名队伍并通过邮件发送回执；
4. 如有其他问题，请直接联系评测委员会：sc_eval@163.com 。



#### 六、奖项设置

**评测奖金由华为公司赞助**，奖池共计40000元：

一等奖（1名），奖金15000元；

二等奖（2名），各奖8000元；

三等奖（3名），各奖3000元。



#### 七、评测委员会

单位：北京大学，复旦大学

主席：詹卫东教授，穗志方（北京大学）；邱锡鹏（复旦大学）

委员：孙春晖，唐乾桐，秦梓巍，董青秀（北京大学）；李孝男（复旦大学）等

联系方式：sc_eval@163.com

---

#### 附：数据样例

（1）各任务数据样例如下：

```javascript
// 子任务1 正例
  {
    "qID": 12,
    "context": "我下了车，站在铁板上。船身并不小，甲板上铺着铁轨，火车就躺在铁轨上喘气。左边有卖饮食的货摊，许多人围在这里谈笑。我一面走，一面看。我走过火车头前面，到了右边。",
    "judge1": true // `true`表示句子成立，无异常。
  }

//子任务1 负例
  {
    "qID": 13,
    "context": "船身并不小，甲板上铺着铁轨，火车就躺在铁轨上喘气。左边有卖饮食的货摊，许多人围在那里谈笑。我一面走，一面看。我走过火车头下面，到了右边。",
    "judge1": false // `false`表示句子不成立，有异常。
  }

// 子任务2 正例
  {
    "qID": 213,
    "context": "在城门口经过一阵可怕的拥挤后，我终于到了郊外。在那里耽搁了两个多钟头，和几个朋友在一起，还在草地上吃了他们带上去的午餐。警报解除后，我回来，打开锁，推开园门，迎面扑来的仍然是一个园子的静寂。",
    "reason": "“郊外”和“带上去”语义冲突",
    "judge2": true // `true`表示归因成立。
  }

// 子任务2 负例
  {
    "qID": 214,
    "context": "在城门口经过一阵可怕的拥挤后，我终于到了郊外。在那里耽搁了两个多钟头，和几个朋友在一起，还在草地上吃了他们带回来的午餐。警报解除后，我回来，打开锁，推开园门，迎面扑来的仍然是一个园子的静寂。",
    "reason": "“带”和“回来”不宜搭配",
    "judge2": false // `false`表示归因不成立。
  }
    
// 子任务3 例子
  {
    "qID": 9,
    "context": "他耷拉着脑袋走近小庙，打眼角往后边瞅。庙门开着，院子里，佛堂里都没个人影儿。他走到庙门旁边，想买股香拿着，象个求神讨签的样子。",
    "reason": "“往后边瞅”与上下文“庙门开着，院子里，佛堂里都没个人影儿”不和谐",
    "judge1": false, // 首先判断句子是否成立。
    "judge2": true // 然后判断归因是否成立。
  }
```

（2）各归因类型的数据样例如下：

```javascript
// A类，搭配问题，正负例
  {
    "qID": 629,
    "context": "再上去百余步是归云洞。洞口有危石横亘，像要坠落上来的样子，我低着头，弯着腰才能走进去。里面石罅离立，像用斧头划开，天光从上面漏下来，正射在两个大碑上。碑是宋治平年杜符卿题诗刻石，字径八寸，洞口“归云”两字，款署双溪。",
    "reason": "“坠落”和“上来”不宜搭配",
    "judge2": true
  },
  {
    "qID": 947,
    "context": "当晚两人便在茅屋后歇宿。李文秀找些枯草，在厅上做了个睡铺，睡梦之中接连惊醒了几次，不是梦到突然给强人捉住，便是见到血淋淋的恶鬼来向自己索命。",
    "reason": "“茅屋”和“后”不宜搭配",
    "judge2": false
  },

// B类，语义问题，正负例
  {
    "qID": 773,
    "context": "他十几年前在德国一个拍卖场上发现一本精装的早期出版的《浮士德》，里面有异常精美的十帧插图，这本书曾经许多名人阅读过，老威廉皇帝读完之后在四面签了一个名字。",
    "reason": "“四面”和“签一个名字”语义冲突",
    "judge2": true
  },
  {
    "qID": 951,
    "context": "当晚两人便在茅屋后歇宿。李文秀找些枯草，在厅上做了个睡铺，睡梦之中接连惊醒了几次，不是梦到突然给强人捉住，便是见到血淋淋的恶鬼来向自己索命。",
    "reason": "“茅屋后”和“睡梦之中”语义冲突",
    "judge2": false
  },

// C类，语境问题，正负例
  {
    "qID": 4015,
    "context": "过了好一会，只听得脚步细碎，两个中年妇人从花径上走到凉亭外，略略躬身，微笑道：“请新官人进内堂更衣。”石破天不知是什么意思，猜测要他进内堂去，便随着二人向外走去。",
    "reason": "“猜测要他进内堂去”与上下文“便随着二人向外走去”存在信息冲突",
    "judge2": true
  },
  {
    "qID": 4016,
    "context": "过了好一会，只听得脚步细碎，两个中年妇人从花径上走到凉亭外，略略躬身，微笑道：“请新官人进内堂更衣。”石破天不知是什么意思，猜测要他进内堂去，便随着二人向外走去。",
    "reason": "“猜测要他进内堂去”与上下文“只听得脚步细碎”存在信息冲突",
    "judge2": false
  },

// D类，常识问题，正负例
  {
    "qID": 1402,
    "context": "我回到房间，回到书桌里面，打开玻璃窗，在继续执笔前还看看窗外。树上，地上，满个园子都是阳光。墙角一丛观音竹微微地在飘动它们的尖叶。一只大苍蝇带着嗡嗡声从开着的窗飞进房来，在我的头上盘旋。",
    "reason": "“回到书桌里面”与常识“人不能回到书桌里面”有一定冲突",
    "judge2": true
  },
  {
    "qID": 2546,
    "context": "她想站起身来扬长而去，走出这间洋溢着冷气令人汗毛孔闭锁的陌生房间，回到她的车床上。她轻车熟路，手艺不错，车出来的活计像她的衣服一样清洁合体。",
    "reason": "“回到她的车床上”与常识“人不能进入车床中”有一定冲突",
    "judge2": false
  }
```

---

> **脚注**
>
> `1` 参看 Jackendoff（2002）著作《Foundations of language: Brain, meaning, grammar, evolution》第1.2、1.5节。
>
> `2` 每段材料配合不同归因将会形成不同题目，因此题目数量大于材料数量。
