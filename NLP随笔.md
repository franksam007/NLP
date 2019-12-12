# NLP随笔

此处记录从网上搜集的一些NLP相关知识，以备后查。

## 定义

自然语言处理，即 Natural Language Processing，简称 NLP ，是一门旨在利用计算机技术来理解并运用自然语言的学科。在不同的场景下，有时候也称之为计算语言学(Computational Linguistics, CL)或者自然语言理解(Natural Language Understanding, NLU)。

要点：
1. NLP 主要通过计算机技术来进行

    在底层理论层面，NLP 会涉及数学、语言学、认知科学等多个学科，但在最后一般是通过计算机技术来承载这些理论知识并发挥效果的。

    看起来好像是废话，但仍然要在此进行强调，计算机和人脑不同，它有其优点也有其缺点，而 NLP 技术也会受到现在计算机技术优缺点的影响。因此不要用我们人脑处理自然语言的过程和效果来要求 NLP 技术 —— 对我们中的绝大部分人来说，使用语言是很自然、很简单的，但不要因此就觉得用计算机来处理也会很简单。

2. NLP 要理解和运用的，是自然语言

    所谓「自然语言」是指在我们的世界中自然地演变出来的语言，比如说英语、汉语、法语……之所以称之为「自然语言」，是为了和程序设计语言（如 C 语言、Java 语言、Python 语言等）等人造的语言进行区分。

    程序设计语言是有非常明确的、固定的语法的，用程序设计语言写出来的每一个句子，都会有唯一确定的含义，因此计算机只需要按照语法规则对其进行解析并执行就好了。

    自然语言则不同，它有相对稳定的语法规则，但这些语法规则都会存在例外而且一直在演变，加上其他一些特性，经常会出现歧义。处理歧义是 NLP 中非常核心的一部分内容。

3. NLP 试图理解自然语言，但何谓「理解」其实并没有一个确定的标准

   理想意义上的「理解」自然语言，是要求 NLP 可以像人脑一样理解自然语言，然而现在脑科学研究上对于我们在使用语言时大脑是如何运作的，并没有一个系统的、全面的认识。因此这也就不能称之为一个标准，实际上在现有的技术框架下，用计算机做到完全理解自然语言，是不可能的。

   退而求其次的，我们一般认为只要在特定的场景中，机器能对我们用自然语言表达的要求进行正确的响应，就是理解了自然语言。
   
   注意这里有几个前提

   *「在特定的场景中」：一般我们认为，在限制了场景后，人们的目的以及语言的表达也会受到限制，因此能把语言表达的多样性降低，这样理解才具备可能性
   *「进行了正确的响应」：我们认为机器的行为符合预期就是理解了，并不关心这中间的过程是否和人脑的运作机制是否一致、是否真正意义上的理解了语言的内涵
当然，这只是现在实际的 NLP 系统所遵循的标准，事实上还是有人从语言学、脑科学等不同角度尝试确定「理解」的过程和标准，让我们保持关注、期待未来吧。

4. NLP 在理解自然语言之后还有加以运用，因此凡是有用计算机来处理、分析自然语言的应用，我们都可以说它是一个 NLP 过程 —— 当然有可能不止是 NLP。

## 主要难点
自然语言自身的一些特性，给计算机理解自然语言这件事情带来了非常多的困难。

第一个特性是自然语言中普遍地存在歧义现象，这种歧义体现在多个层面：

1. 在语言的最小单元也就是词语的级别，存在多义词、同义词等现象

    比较经典的是 20 世纪 60 年代一位早期的机器翻译研究者给出的经典例子

    `The box is in the pen.`
    
    虽然可能不太清楚 pen 的另外一个含义是「围栏」，但肯定能意识到这句话中 pen 的含义不是「笔」。这个 badcase 从提出到现在已经有 50 多年了，但我们可以看到，仍然没有翻译系统能够在不加特殊处理的情况下解决这个问题（换言之这个 badcase 是可以通过特殊而丑陋的手段来解决的）。

    * Google 翻译 --> 盒子在笔中
    * 百度翻译 --> 盒子在钢笔里
    * 搜狗翻译 --> 盒子在钢笔里
    
    与之相对的，中文里有一个例子是「意思」这个词的多义性

    他说：“她这个人真有意思(funny)。”她说：“他这个人怪有意思(funny)的。”于是人们认为他们有了意思(wish)，并让他向她意思意思(express)。他火了：“我根本没有那个意思(thought)！”她也生气了：“你们这么说是什么意思(intention)？”事后有人说：“真有意思(funny)。”也有人说：“真没意思(nosense)”。（原文见《生活报》1994.11.13 第六版）

    当然，上述两个例子都是经过人为设计的精巧例子，大部分人们日常活动中使用的语言，并不会这么复杂。

    多义词之外，同义词也是非常普遍的语言现象，如：词语的缩写（如「人影办」之于「人工影响天气办公室」）、专有名词的别名（如「感冒」之于「上呼吸道感染」）、网络用语（如「蓝瘦」之于「难受」）、方言（如「包谷」之于「玉米」）、口语和书面语（如「脑袋」之于「头部」）……在 NLP 应用中，对同义词的辨别和处理工作也是非常多的，如：搜索引擎会通过查询改写(Query Rewrite)来将用户的搜索改写为同样含义但表述更为精准的语句；知识图谱里的实体链接技术本质上就是将实体名称（如人名、地名）的不同形式的表达和标准的表达对应起来；智能对话里可以通过同义词来更好地理解用户的问题……

    而在多义词、同义词理解上，目前 NLP 领域并没有一劳永逸的解决办法，有靠人工构建的小规模高质量知识库如 WordNet、HowNet、同义词词林，也有靠机器学习方法从大量语料中学习到词语的向量表示来隐式地反映词义 —— 量大但并不足够精确。前者往往质量很好但只能覆盖人们实际语言中很小的一部分，后者依赖于语料的数量、质量和领域，对于语料中较少出现的一些词往往就会得到莫名其妙的结果。

2. 在句子乃至更高层的语言单元如段落、篇章里，又存在结构性歧义的现象

    以句子为例，它是由词组成的，词和词之间有些是有关联的、有些是没有关联的，因此整体会形成一个结构，也就是我们在学习语言时了解到的「语法」。

    理想的情况下，任意给定一个句子，如果它的语法结构是唯一、确定的，那么我们只需要把它这个语法结构计算出来，然后再把前面提到的同义词、多义词的问题也解决了，那么这个句子的含义就能确定了。但实际情况是，自然语言的语法规则并不是一个非常严格的规则，在句子比较复杂的时候，往往会造成句子可以有多种不同但都合理的解释。

   举一些例子

    * “喜欢乡下的孩子” 可以有下面两种解释
      * [喜欢/乡下]的/孩子: “喜欢乡下的”作为定语修饰“孩子”
      *喜欢[乡下/的/孩子]: “乡下的孩子”作为“喜欢”的宾语
    * “他背着总经理和副总经理偷偷地把钱存进了银行” 可以有下面 2 种解释
      * 他[背着/总经理/和/副总经理]偷偷地/把/钱/存进/了/银行: “他”独自存钱
      * 他[背着/总经理]和/副总经理/偷偷地/把/钱/存进/了/银行: “他”和“副总经理”一起存钱
    * “放弃美丽的女人让人心碎” 可以有下面 2 种解释
      * [放弃/美丽/的]女人/让/人/心碎: “女人”让人心碎
      * [放弃/美丽/的/女人]让/人/心碎: “放弃”让人心碎
    再看英文的一个经典例句: "Put the block in the box on the table"。它可以有两种解释:

    * Put the block [in the box on the table]: "on the table" 修饰 "box"
    * Put [the block in the box] on the table: "on the table" 限定 "block"

   如果再加上一个介词短语 "in the kitchen"，那么它可以有 5 种不同的解释；再增加一个的话，将会得到 14 种不同的解释。就这个介词短语导致歧义的情况来说，可能的歧义结构数量基本上是随着介词短语数量的增加而呈指数级上升。「指数级上升」是什么概念？那意味着想要靠枚举所有的可能性来解决歧义是非常低效甚至不可能的。

上述两种情况互相组合，又会造成更多、更复杂的歧义情况。

正如前文所说，如何处理歧义并排除歧义，是 NLP 中非常主要的一部分内容，而且是非常困难的一部分，这是因为造成语言歧义的原因多种多样。

造成词语歧义的原因，前面已经说过了一部分，也就是缩写、别名、网络用语、方言、口头语和书面语这几个；除此以外，比喻、拟人、谐音等手法也会使已有的词产生新的含义或和原来不相关的词产生同义；还有省略、指代等依赖上下文的情况也容易造成歧义……总之造成词语歧义的情况是非常多的。

在词义消歧这个问题上，除了造成歧义的情况多种多样外，还有一个困难是消歧经常依赖于文本之外的、海量的「常识」，比如说前面那个机器翻译的例子「The box is in the pen」，我们为什么能判断「pen」的含义不是「笔」，是因为我们具备这些知识

* 盒子是有体积的
* 笔不是一个容器
* 相对盒子，笔一般都更小

并由此推理出：盒子在笔中是不合理的。但是抱歉，这种我们认为是常识的知识，计算机并不具备，它是无法作出这种推理的。我们说的机器学习、深度学习，本质上还是依赖于数据，也就是说，要见过相同的或者相近的数据，它才能理解，对于知识本身则基本没有学习到。

在 NLP 发展历程中，也有人耗费巨大精力和金钱来将我们说的知识和规则整理成计算机可操作的数据，如 Cyc、DBpedia、Freebase，并演变成我们现在所说的知识图谱（其实以前就叫「知识库(Knowledge Base)」的，「Knowledge Graph」最早是 Google 的一个知识库的名字），但在 NLP 任务比如说词义消歧中，如何使用这些知识，仍然是一个很大的问题。

至于结构歧义或者说语法歧义，其原因也可能有几方面

1. 当其中的词语有歧义时，这个词的不同词义可能具有不同的语法功能，而造成最终的语法结构不同，如前文的例句「放弃美丽的女人让人心碎」的两个不同解释中，「美丽」一词分别作为名词和形容词，而造成了不同的语法解析结果

2. 自然语言语法本身并不是确定性的，即存在一些情况，哪怕其中每个词的词性、词义都是确定无疑的，可以得到的合理的语法解析结果也会有多个，前面那个「他背着总经理和副总经理偷偷地把钱存进了银行」的例句和那个英文例句就是这种情况

再加上语言一直在演变，新的语法规则不断出现，比如原来认为是错误的语法因为被普遍使用而被接受为新的语法规则，比如原有的语法规则被简化称为更简单的语法规则。这就导致很多语法规则都会有例外，而很多例外逐渐又成为了新的语法规则，就造成了「所有规则都有例外，所有例外都是规则」的现象。这就导致如果我们如果想靠语法规则来完成任务的话，最终就会陷入不停补充新的语法规则（或说例外）的境地里。

前面说了*歧义*这个自然语言的特性，而自然语言还有一个很重要的特性，就是前面提到的语言的动态演变。除了它给带来的歧义现象，更重要的是，由于语言的动态演变，新的知识、语言现象一直在出现，如何捕获、学习到这些新的知识和语言规则，对 NLP 来说，同样是非常大的一个挑战，因为如果不能学习到新的语言知识，那么建立在旧数据上的 NLP 模型，往往连基本的分析都做不到，更别谈去解决歧义并理解了。

此外，对中文、日文等一些语言来说，还有特殊的一点，就是在文字中，词和词不是天然就分隔开的。出于效果和效率等多方面的考虑，现有的 NLP 方法基本都建立在词的基础上，所以对中文这些语言来说，还需要对文字进行额外的、确定词和词之间边界的处理，也就是我们常说的「分词(Word Segmentaion)」。而分词这个过程本身，又存在不确定性，即同一个句子，可能的分词结果不一定是唯一的。

先看看这些例子

1. “梁启超生前住在这里” 可能有两种分词结果
   * 梁启超/生前/住/在/这里
   * 梁启/超生/前/住/在/这里
2. “武汉市长江大桥” 可能有两种分词结果
   * 武汉/市长/江大桥
   * 武汉市/长江/大桥
3. “阿拉斯加遭强暴风雪袭击致多人死亡” 可能有两种分词结果
   * 阿拉斯加/遭/强/暴风雪/袭击/致/多人/死亡
   * 阿拉斯加/遭/强暴/风雪/袭击/致/多人/死亡
4. “已取得文凭的和尚未取得文凭的干部” 可能有两种分词结果
   * 已/取得/文凭/的/和/尚未/取得/文凭/的/干部
   * 已/取得/文凭/的/和尚/未/取得/文凭/的/干部
5. “今后三年中将翻两番” 可能有两种分词结果
   * 今后/三年/中将/翻/两番
   * 今后/三年/中/将/翻/两番

可以看到，仅仅是分错一两个词，整个句子的含义就完全不一样了。中文分词的困难在于，如果要正确地进行分词，就要对句子的语义有正确的理解；另一方面，要正确理解句子的语义，又需要正确的分词结果。于是就出现了一个先有鸡还是现有蛋的问题。

虽然有上述诸多困难，但 NLP 领域也形成了相应的应对方法，不过也只能说是「应对」而非「解决」，因为这些方法的目的都是追求解决上述问题在实际应用中常见的一部分，使对应的 NLP 系统能在受限场景中正确处理绝大部分比如 80% 或者 90% 的自然语言；而剩下未能处理的部分，则可以通过系统、产品上的一些设计，根据用户行为把它们找出来，加以研究并更新技术，如此逐渐迭代，来让 NLP 系统逐渐达到令人满意的效果。

## 主要应用和关键技术
一些比较成体系的 NLP 应用，有

1. 机器翻译: 将一种自然语言的文字转换成另外一种自然语言的文字
2. 信息检索: 从海量的文档里检索出我们需要的信息，搜索引擎如 Google/Bing/Baidu 就是非常典型的信息检索系统
3. 文本摘要: 从较长的文档或文章中生成篇幅更小但内容完整的摘要
4. 智能对话: 通过对话的形式直接自动回答用户的问题或者执行特定的行为
5. 垃圾邮件过滤: 将垃圾邮件筛选出来并进行标记
6. 與情分析: 检测民众对公共事件的意见、态度、情感等倾向

当然实际上 NLP 的应用是非常多的，限于篇幅这里只讨论一下上述比较主要的应用。

上面六个 NLP 应用，其实可以划分成两类，一类是需要理解文本的完整语义并作出响应，如机器翻译、文本摘要和智能对话；另一类只需要理解文本中特定的信息就可以，对于文本的完整语义并不太关心，比如信息检索、垃圾邮件过滤和與情分析。当然这样划分并不太严格，比如说搜索引擎里也会有人用自然语言去描述自己的问题并期望得到正确的结果，而垃圾邮件过滤和與情分析有时候也需要在理解完整语义的基础上再去提炼「特定信息」，但大部分情况下这样划分是没有问题的。

在第一类即机器翻译、文本摘要和智能对话中，前两者都有明确的目标和评估标准，比如机器翻译有 BLEU 指标，文本摘要有 ROUGE 指标，而智能对话至今仍没有一个通用的评估标准，要么是借用一下机器翻译的 BLEU，要么是在特定的对话形式和对话任务里制定特殊的标准 —— 比如任务型对话里的槽填充率、检索型问答里的命中率和召回率。一个真正可用的智能对话系统，必然是一个融合系统，既有任务型问答也有检索型问答，说不定还会有开放域闲聊，那么在这样一个融合的系统里，各扫自家门前雪肯定是不行的，所以就现在来说，智能对话会比机器翻译和文本摘要要难一点 —— 倒不是说技术上难，而是难在确定目标和评估标准上。

在第二类即信息检索、垃圾邮件过滤、與情分析这三者中，與情分析除了要分析出情感、态度倾向，还要确定这种倾向针对的是什么对象，所以相比信息检索和垃圾邮件过滤，又会更难一点。

总的来说，在大部分情况下，对于 NLP 的应用，可以按照下面的原则来判断其难易程度

* 需要理解完整语义的任务，要比只需理解部分信息的任务更难
* 有确定目标和评估标准的任务，要比没有的更容易
* 要做复杂分析的任务，要比只做简单分析的任务更难

在技术方面，各个应用会涉及的更底层的关键 NLP 技术如下：

* 早期基于规则的翻译系统: 句法分析
* 统计机器翻译: 语言模型，隐马尔可夫模型(HMM，早期被广泛用于序列标注)
* 神经网络机器翻译: seq2seq，注意力模型
* 信息检索: 大量的文本预处理，实体抽取，主题模型，文本相似度量，知识图谱
* 检索型的问答系统: 同信息检索，但还需要进行指代消解、省略消解
* 任务型的问答系统: 意图识别，实体抽取，指代消解，省略消解，对话状态管理，自然语言生成
* 垃圾邮件过滤: 文本分类
* 與情分析: 观点词抽取，情感分析，关系抽取，意见挖掘
* 文本摘要: (这个不太清楚，略过)

虽然各个应用的目标都不一样，但最后会发现它们用到的很多方法都是共通或者干脆是一样的。

最基础的，各个应用在开始前都需要对文本做预处理，不过预处理是一个很宽泛的概念，并没有一个或一套特定的方法，因为处理的都是汉语，所以基本上都会做简繁统一转换，会把全角字符转成半角字符，会做标点的归一化处理(例如，希腊字母里的问号在外形上和英文的分号一个样子)，会去除一些无效的字符(比如说不可见的零宽度的空白符)；英文里则会做词干提取、词形还原。很多讲 NLP 的文章说到预处理都会说停用词(stopwords)去除 —— 所谓停用词是指在特定领域里使用频率很高且往往不表达语义的词，如「了」、「的」，但实际上不是所有的应用上都需要去停用词、都可以去停用词的，比如说在作者身份鉴别这个应用上，是重度依赖虚词、介词等所谓功能词的，而在 NLP 里，虚词、介词这种词一般都会被视作停用词。

预处理的目的是让文本变得更「干净」，少一些「脏东西」，同时尽量更加地规范，所以有时候也会把预处理形象地称为「清洗」。好的预处理能减少干扰信息，并且保留重要信息，同时一些规范化处理(如繁简统一转换、标点归一化处理、英语的词干提取和词形还原)还能够减少后续步骤需要处理的信息量。

在做完预处理后，一般就是变着花样从文本里提取信息出来，以机器学习的角度来讲就是特征提取。根据不同的应用，这一步可能会非常简单，也可能会非常复杂。

最初始的一个处理，就是从文本里，把词都提取出来，这一步对英文等语言来说很自然，按空格和标点分一下就好了，而对中文来说则需要专门做中文分词，这个是前面提到过的。从计算语言学的角度来讲，分词是「词法分析」的一部分，所谓「词法分析」除了确定词和词之间的边界，还需要确定词性(一个词是动词、名词还是别的什么)、词义(「苹果」是一种水果还是一种电子产品)，通俗一点来说，就是要解决: 哪些是词，有哪些词，各个词都是什么意思。

分词的方法有多种，简单的如准备好一个超大的词表，然后在这个词表里找可能拼成当前这句话的词，然后在多种可能的组合里确定一个最有可能的，看着很粗暴但其实也还可以。不过现在主流上都是将分词当作序列标注问题来处理。所谓序列标注是说，给一个序列，模型能给这个序列上每一个元素都标注成为一个特殊的记号，对分词而言，要标注的记号可以有三种: 是不是词的第一个字，是不是词的最后一个字，是不是词中间的字。

序列标注问题并不是 NLP 中特有的，但有不少 NLP 任务或技术都和序列标注有关，刚才说到的分词和词性标注(确定词性)，基本上都是当作序列标注问题来处理。除此以外，实体抽取或者更复杂的信息抽取，也被视为序列标注问题。所以如果是作为一个 NLP 从业人员，序列标注问题的相关方法，是必须要掌握的，建议 HMM、CRF、RNN 的原理摸熟吃透，掌握一两个好用的序列标注工具，囤点序列标注问题的数据集打磨一下自己的感觉。

虽然说主流的方法都是将分词当作序列标注问题来做，但在实践中，囤点词典还是有益无害的，比如说做做新词挖掘、同义词挖掘、领域实体词的积累等等。至于怎么做这些挖掘、积累，各个应用有各个应用的做法，比如说搜索引擎靠 query 点击日志能把同义词或近义词找出来，原理就是类似两个人用了不同的词去搜索，但最后都点击了同一个链接这种思路；没有搜索引擎这样比较方便的用户反馈的，可以通过一些无监督或半监督的方法来做，会更难一些但总之是有方法的。

做完词法分析后，一般会有一些不同的后续处理

1. 区分哪些词是重要的，哪些词是不重要的，可能涉及到关键词提取、实体抽取、停用词去除等
2. 分析哪些词之间是有关联的，哪些词之间是没有关联的，可能涉及到短语抽取、关系抽取、句法分析等
3. 基于词对整个文本进行分类得到一个高度抽象的结果，可能涉及情感分析、意图识别、主题分类等

实体抽取前面说了，可以当作序列标注问题来做。停用词去除没什么好说的，一般就是在通用的一个停用词表的基础上，统计一下数据中高频的词加进去而已。关键词提取我觉得是很重要的一件事情，不过大部分情况下用 TFIDF 就能提取出不错的关键词来了，在此基础上辅以之前词法分析的一些结果如词性基本上就能把关键词捋得差不多，基本上名词、动词、形容词、实体词拿出来做关键词就差不多了。

这里说到了 TFIDF，这个也是 NLP 里非常经典非常重要的一个技术，思路是很简单的，就是说对一个词，用两个数值来反映其在某篇文档或者某个句子里的重要程度，第一个是所谓词频(Term Frequency, TF)，即这个词在当前文档/句子中出现的次数；第二个是所谓逆文档频率(Inverse Document Frequency, IDF)，指出现过这个词的文档/句子的数量的倒数。通俗来说，就是，一个词在其他文档/句子里越少出现(IDF 值比较大)，在当前文档/句子中越多出现，那么它在当前文档/句子中就越重要。很朴素的思想，实际上这个思路最终是可以用信息熵来解释的，总之很实用。

短语抽取、关系抽取和句法分析都是为了得到文本中的层次结构以更好地理解语义。其中短语抽取较简单，因为只需要看前后两个词是否有关系就好了，而关系抽取和句法分析都需要分析不相邻的词之间是否存在关联。这块不太熟，只是用过相关工具。句法分析是理解语义非常核心非常重要的一件事情，一个好的句法分析系统或工具，能够大大提高整个系统的效果。

然后是情感分析、意图识别、主题分类这些技术，其实大部分情况下都是文本分类在不同应用场景里的别名而已。文本分类是一个相对简单但应用非常广泛的技术，也是一块值得花精力去好好掌握的内容，逻辑回归、支持向量机、GBDT，然后是深度学习常见的分类模型结构，把这些都好好掌握一下，并且在实际数据中熟练掌握好预处理、特征提取、特征选择的流程和技巧，受用无穷。至于说深度学习不用特征的都是傻蛋，我分类的时候用深度学习一样能把特征加上去，就是比你不加好，爱调不调。

上述技术，基本上就能把任务相关的「理解」做得差不多了。在理解之后，一般还会有涉及应用的更具体的响应处理，如机器翻译、文本摘要、智能对话中会有自然语言生成，信息检索及检索型问答系统会有文本相似度量。

其中自然语言生成(Natural Language Generation, NLG)至今仍然是一个很困难的问题，在技术上，有基于统计语言模型的生成方法，也有基于神经网络语言模型的生成方法，近几年的变分自编码器(Variational Auto-Encoder, VAE)和基于强化学习的生成方法使用得也越来越多了。但这里说的 NLG 多是在特定任务中，基于前面已经有的分析结果来生成较短的文本，至于生成小说什么的，看看都没有媒体和公司去吹就知道是多么难的一件事情了。

这里提到了语言模型，也是一块可以好好掌握一下的内容。

然后就是文本相似度量，也是非常重要的一项 NLP 技能。某种意义上来说，它和 NLP 的终极目标是等价的。如果任意给定两个句子，一个 NLP 系统能够准确地判断这两个句子是相似还是不相似，那么它就已经是一个完全理解自然语言的系统了。以机器翻译为例，其 BLEU 指标，就是判断翻译出来的句子，和给定的标准翻译是否相似，但实际上其计算方法很简单只是计算了表面相似，所以 BLEU 指标也并不是非常准确，在实际应用中还是要靠人来评估实际效果，但是这么多年了学术界和业界也并没有找到比 BLEU 更好多少的指标，所以将就用着，倒是也有 AMBER 和 METEOR 这种不光看表面相似的评估标准，但是计算太复杂了，所以并没有成为公认的标准。假如有一天有更好的评估标准能和人为评估效果更加接近，那才是机器翻译的大突破。

文本相似的困难对很多非技术人员或者非 NLP 领域人员来说也经常难以理解，“这两个句子就是一个意思为什么就不理解呢”这样的话也是经常能听到的。理解一下，它真的很难。

简单的、传统的相似度量有 LCS 相似度、Jaccard 系数、余弦相似度等，都是久经考验非常实用的方法，应对一些简单的任务措措有余，当然这些方法基本上都是看表面相似，所以泛化性会差一些，需要不断补充特征才能提高效果。如果有足够数据的话，一些基于深度学习的匹配模型会有非常不错的效果，这个不错不光是指其在固定的测试集上的效果，在集外数据的泛化性上都会很不错，当然前提是要有米。

文本相似度量的应用也是很多的，在机器翻译和文本摘要里可以用来评估系统效果，在信息检索和智能对话里可以用来匹配正确的文档或问题，甚至有些时候一些分类任务也可以用文本相似度量来解决(有 A 类数据 1000 条 B 类数据 1000 条，判断下和 A 类数据更像还是和 B 类数据更像)。

另外一方面，除了给定两个句子判断其相似程度外，相似句子的挖掘和生成，也是很有意思的一件事情。生成相似问题这件事情，专业的说法叫做「复述(Paraphrase)」，它和相似度量是互相促进的，相似度量做的好，那么就可以挖掘出更多的相似句子来做训练复述生成模型；复述生成做的话，反过来又可以给相似度量模型提供训练数据。

对于深度学习在 NLP 中的应用，比较核心的技术有

1. word embedding，也就是我们俗称的词向量，通过大量数据无监督(不需要标注)训练，可以用一个向量来表示一个词的词义，理想情况下如词性、词义、情感、主题等各种信息都可以在这个向量中得到表达 —— 当然这只是一个感性认识，目前对于这个向量实际的含义和解释，我们并不太关心，好用就对了。此外 word embedding 因为能比较好地反映词义，还可以用来做关键词、同义词挖掘，在各项深度学习相关的 NLP 任务中，基本也是标配了
2. 序列标注方面，BiLSTM+CRF 已经是很主流的做法
3. seq2seq 和 attention，这两个技术都是在神经网络机器翻译的研究中被提出来的，然后也被广泛用到如智能问答、文本摘要等重要 NLP 应用上。这两者一般是一起出现的，现在已经演变成了一种计算框架，具体的方法和细节则已经有了很多的变化
4. 自然语言生成方面前面提到过 VAE 和强化学习，近一年内生成对抗网络(Generative Adversarial Nets, GAN)也开始有在这方面的应用

深度学习相关的技术一般都会需要比较多的数据，但我们会发现在实际的任务中，可能并没有那么多数据来让我们上深度学习，或者数据太多但却包含了太多噪音数据。土豪的办法是用金钱来为所欲为顺便创造点特殊岗位造福社会。比较经济的做法是先使用前面提到的传统的、经典的方法，同时在产品、系统的上设计好良好的反馈渠道，在冷启动后不断进行迭代优化，同时有意识地从日志、用户反馈中积累数据，到达一定的量后开始上深度学习来解决传统模型泛化性不够好的问题。

## Unicode 简介
所有的数据，在计算机上都是以数字（严格来说是二进制）的形式存在的，文字也是如此，只不过咱们的编辑器、浏览器对这些数字做了特殊处理，将其对应的形状展示出来了而已。在这个基础上，不同的操作系统、平台、应用为了能够正常地交流，就必须约定一个统一的「计算机中的数字」到「实际文字」的对应关系（即编码标准），比方说数字 97 对应小写英文字母「a」、33528 对应「言」字之类的 —— 没错，所谓的编码标准，就相当于一个大的索引表，每个文字在这个索引表里都有一个对应的索引号（也就是我们刚才说到的数字）。

在计算机系统发展早期，其实是并没有这样一个统一的编码系统的，美国一开始就用了 0-127 的值来编码，包括了大小写字母、数字、标点符号以及一些特殊符号，这就是“美国信息交换标准代码(American Standard Code for Information Interchange, ASCII)”。显然 ASCII 是不适用于中文的，所以后来我国推出过 GB2312 标准，收录了 6763 个汉字，并在之后经过扩展有了 GBK 和 GB18030 多个编码标准；另外一方面，港澳台地区又独立发展出了繁体的 BIG5 编码……这些编码都是互相不兼容的，这就会导致使用编码 A 的网站，被使用编码 B 的计算机访问后显示为乱码的状况，而这里只提到了中英文的编码体系，实际上很多国家都有过自己的标准，而且很多是还在使用的。

基于这种状况，后来计算机领域产生了一个叫做 Unicode 的统一编码，又称「万国码」，收录了世界上各个国家大部分的文字，并且仍然在不断增修，今年六月份发布了第十一个正式版本。目前使用最广泛的是 Unicode 实现是 UTF-8 编码。

## Unicode 在 NLP 中的应用
Unicode 这个标准，并不是单纯做好所有文字的索引，它还对文字分门别类做了很多的整理，比如说同一个语系的文字会放在索引表的邻近区域，而一个文字是否是数字或标点、数学符号这些信息也都在 Unicode 标准中有记录，并且所有这些数据都是公开的。如果能善加利用这些信息的话，能帮助到咱们在 NLP 工作中对文字进行处理的部分。

这里不准备对 Unicode 数据做系统、全面的说明，如有兴趣，可以前往 http://unicode.org/charts/ 查看完整的 Unicode 数据，这里就以几个例子来讲解几个应用。

### 根据 Unihan 数据来从文本中筛选中文字符
Unicode 中中文数据的部分被称为「Unihan 数据库」，在<a href="http://unicode.org/charts/unihangridindex.html">这个页面</a>可以看到 Unihan 中数据的范围。根据 Unihan 数据，可以得知在 Unicode 编码里，中文的索引值的范围包括以下几部分:

* U+3400 - U+4DB5: 「U+」表示这是 Unicode 编码，3400 是十六进制表示，换算成十进制是 13312，下同
* U+4E00 - U+9FCC
* U+F900 - U+FAD9
* U+20000 - U+2A6D6
* U+2A700 - U+2B734
* U+2B740 - U+2B81D
* U+2B820 - U+2CEA1
* U+2F800 - U+2FA1D

根据这个我们能很容易地写出一个检查某个字符是不是中文字符的方法来，如下
```python
def is_chinese_char(char):
    char_idx = ord(char)
    if 0x3400 <= char_idx <= 0x4DB5 or \
       0xF900 <= char_idx <= 0xFAD9 or \
       0x4E00 <= char_idx <= 0x9FCC or \
       0x20000 <= char_idx <= 0x2A6D6 or \
       0x2A700 <= char_idx <= 0x2B734 or \
       0x2B740 <= char_idx <= 0x2B81D or \
       0x2B820 <= char_idx <= 0x2CEA1 or \
       0x2F800 <= char_idx <= 0x2FA1D:
        return True

    return False
```

或者写个正则
```python
import re

CHINESE_CHAR_PAT = re.compile(
    r'[\u3400-\u4DB5\u4E00-\u9FCC\uF900-\uFAD9'
    r'\u20000-\u2A6D6\u2A700-\u2B734\u2B740-\u2B81D'
    r'\u2B820-\u2CEA1\u2F800-\u2FA1D]'
)

def is_chinese_char(char):
    return bool(CHINESE_CHAR_PAT.match(char))
```

以上都是笨办法，因为实际上并不需要去记中文的编码范围，而且由于 Unicode 是在扩展的，如果将来扩充了，那么扩充进来的新的字可能就没有办法用上面的方法检查了。前面提到，Unicode 标准做了多方面的整理，而这些整理结果都作为属性附加到每个 Unicode 字符上了。

首先，每个 Unicode 字符都会被赋予一个名字，下面是一部分对照表

|Unicode|Name|
|---|---|
|a|LATIN SMALL LETTER A|
|9|DIGIT NINE|
|我|CJK UNIFIED IDEOGRAPH-6211|
|α|GREEK SMALL LETTER ALPHA|

对于中文，只要取其 name，然后判断是否包含 CJK 这个关键词就行了。要怎么获取 Unicode 字符的 name 呢？用 Python 标准库里的 unicodedata 模块即可
```python
import unicodedata

def is_chinese(char):
    return unicodedata.name(char).startswith('CJK')
```

而除了 name，Unicode 字符还有 block 和 script 两个属性：block 其实就是我们前面提到的连续编码区域，不过会有一个名字；script 是指每个文字的书写体系，可能会包含多个 block，详情见<a href="https://www.unicode.org/standard/supported.html">文档</a>。

前面提到的汉字的编码区域和 block 名称的对应关系如下表所示

Block Name	|Block Range
---|---
CJK Unified Ideographs Extension A	|U+3400 - U+4DB5
CJK Unified Ideographs	|U+4E00 - U+9FCC
CJK Compatibility Ideographs	|U+F900 - U+FAD9
CJK Unified Ideographs Extension B	|U+20000 - U+2A6D6
CJK Unified Ideographs Extension C	|U+2A700 - U+2B734
CJK Unified Ideographs Extension D	|U+2B740 - U+2B81D
CJK Unified Ideographs Extension E	|U+2B820 - U+2CEA1
CJK Compatibility Ideographs Supplement	|U+2F800 - U+2FA1D

汉字对应的 script 名字是 Han，直接包括了上述所有 block。使用 Python 的 regex 这个工具，可以直接在正则表达式中使用 block 和 script。仍以汉字判断为例，可以这么写
```python
import regex

def is_chinese_char(char):
    return bool(regex.match(r'\p{script=han}', char))
```
可惜在标准库 unicodedata 中并没有访问 Unicode 字符的 block、script 等属性的方法。

对于其他语言的文字，将上述方法中的参数（编码区域、script 等）稍作修改也是可行的，不再赘述。

### 用 category 属性判断标点、数字、货币单位等

Unicode 数据中，每个 Unicode 字符还有一个叫做 category 的属性，这个属性和字从属的语言无关。category 一共有 Letter、Mark、Number、Punctuation、Symbol、Seperator、Other 七大类，然后每个大类下还有一些小类，总体上是一个二级分类结构。因此在 Unicode 中有两个字母来组合表示一个 Unicode 字符的类型信息，我们可以用 unicodedata.category 来得到这个信息
```python
import unicodedata

for char in '1天。':
    print(char, unicodedata.category(char))
```

结果为
```
1 Nd
天 Lo
。 Po
```

类型码和分类信息的对照表如下

类型码	|类型信息
---|---
Lu	|Letter, uppercase
Ll	|Letter, lowercase
Lt	|Letter, titlecase
Lm	|Letter, modifier
Lo	|Letter, other
Mn	|Mark, nonspacing
Mc	|Mark, spacing combining
Me	|Mark, enclosing
Nd	|Number, decimal digit
Nl	|Number, letter
No	|Number, other
Pc	|Punctuation, connector
Pd	|Punctuation, dash
Ps	|Punctuation, open
Pe	|Punctuation, close
Pi	|Punctuation, initial quote (may behave like Ps or Pe depending on usage)
Pf	|Punctuation, final quote (may behave like Ps or Pe depending on usage)
Po	|Punctuation, other
Sm	|Symbol, math
Sc	|Symbol, currency
Sk	|Symbol, modifier
So	|Symbol, other
Zs	|Separator, space
Zl	|Separator, line
Zp	|Separator, paragraph
Cc	|Other, control
Cf	|Other, format
Cs	|Other, surrogate
Co	|Other, private use
Cn	|Other, not assigned (including noncharacters)

如上，标点符号的类型码都是 P 开头的，根据这个就能把标点筛出来了
```python
import unicodedata

def is_punctuation_char(char):
    return unicodedata.category(char).startswith('P')
```
类似的，货币单位符号的类型码为 Sc，可以直接判断
```python
import unicodedata

def is_currency_char(char):
    return unicodedata.category(char) == 'Sc'
```
类型码 N 开头的是数字字符，除了我们常见的十个阿拉伯数字外，像罗马数字、带圆圈的数字序号等都被涵盖在内。

此外类型信息也可以在 regex 这个工具里使用，例如

* 找到文本中所有数字
```python
regex.findall(r'\p{N}', '第⑩项')
```
结果
```
['⑩']
```
* 找到各种括号表示开始的那一个
```python
regex.findall(r'\p{Ps}', '「Unicode」（又名万国码）见《标准》')
```
结果
```
['「', '（', '《']
```
或找到表示结束那一个
```python
regex.findall(r'\p{Pe}', '「Unicode」（又名万国码）见《标准》')
```
结果
```
['」', '）', '》']
```
根据这张类型表，也可以写出一个用于文本预处理的简单清洗函数来，用来把一些奇奇怪怪的字符都从文本里去掉
```python
import regex

def clean_text(text):
    # 去除明确无意义的字符
    # 1. Zl: Separator, line
    # 2. Zp: Separator, paragraph
    # 3. Cc, Cf, Cs, Co, Cn
    text = regex.sub(r'[\p{Zl}\p{Zp}\p{C}]', '', text)

    # 将空白符归一化
    text = regex.sub(r'\p{Zs}', ' ', text)
    return text
```
还可以根据数字类型 Unicode 字符的 name 来将其归一化到阿拉伯数字上，先看看数字类型的 Unicode 字符的 name 吧
```python
import unicodedata

chars = ['⑩', '1', 'Ⅲ', '〹', '⒗']
for char in chars:
    print('{}: {}'.format(char, unicodedata.name(char)))
```
结果
```
⑩: CIRCLED NUMBER TEN
1: DIGIT ONE
Ⅲ: ROMAN NUMERAL THREE
〹: HANGZHOU NUMERAL TWENTY
⒗: NUMBER SIXTEEN FULL STOP
```
可以看到，在 NUMBER/DIGIT/NUMERAL 后面的那个单词，就是对应数值的英文单词，只要把这个英文单词提取出来就得到了一个统一的表示，然后再将其转换成阿拉伯数字即可。

## 关于文本分类
所谓的文本分类，是机器学习中分类问题在 NLP 领域中的应用，它的理论相对简单、工具成熟、上手简单，大家基本上是把它当作一个「理论上已经解决」的问题来看待，但其实在实际场景中处理文本分类任务时还是会遇到不少问题的，加上文本分类又是 NLP 领域中最常见的任务之一。

关于文本分类
所谓的文本分类，其实就是机器学习中分类问题在 NLP 领域中的应用，它的理论相对简单、工具成熟、上手简单，大家基本上是把它当作一个「理论上已经解决」的问题来看待，但其实在实际场景中处理文本分类任务时还是会遇到不少问题的，加上文本分类又是 NLP 领域中最常见的任务之一，我想把自己在这方面的一些经验和学习成果慢慢地整理出来。

2017 年的时候，为了提高做文本分类任务的效率，将 sklearn 中的文本分类功能做了一些封装，后来断断续续地优化，产出了一个我自己用起来很顺手的文本分类工具。在我开始写《NLP 哪里跑》这个系列的博客后，我计划是把自己在 NLP 方面的经验进行系统地梳理，第一块就是文本分类 —— 这一块当然有很多很多想讲的东西和想做的事情，一篇文章是写不完的，所以最初的想法是先看一下工具方面的情况。我对我在公司维护的文本分类工具还是挺满意的，但也会想自己会不会对一些先进的工具认识不够，所以就去了解了很多其他的同类工具，本篇文章就是对这些工具的一个简单的罗列，不涉及分类模型的理论，也不涉及某个分类模型的具体实现的优劣评价，仅仅是一个非常工具向、实用向的整理记录。

在挑选文本分类工具时是有一些标准的，不是非常严格，但大概能分成以下几点：

* 工程化程度良好的，能提供易用的编程接口或命令行接口
* 以 Python 生态内的工具为主 —— 在大数据及AI时代，Python已经成熟No. 1的变成语言

### 一些不建议使用的工具
本节中列举的工具，建议不要浪费时间在上面。（参考网上经验）

#### 腾讯的 NeuralClassifier

[【开源公告】NeuralNLP-NeuralClassifier - 深度学习文本分类工具 - 云+社区 - 腾讯云](https://cloud.tencent.com/developer/article/1459733)

项目地址：https://github.com/Tencent/NeuralNLP-NeuralClassifier

* 作为一个 Python 项目，没有发布到 pypi，连 setup.py 也没有，无法安装，项目组织也没眼看，只能像个原始人一样拷贝代码到自己的目录跑跑脚本，很难想象是一个大厂的项目
* 训练需要使用一个格式复杂的 json 格式的配置文件，然后这个配置的文档太过简略，不少细节藏在项目提供的脚本里……

#### 无人维护的 keras-text
项目地址：https://github.com/raghakot/keras-text

这个项目蛮可惜的，从文档和实际使用来看，作者在代码结构和使用流程上是做了一些用心的设计的，但是有些关键模块没有完成，在很多细节上存在令人难以忍受的小问题。

项目已经两年没有更新了，可以参考它的代码，但不建议作为一个正经的工具在实际任务中使用。

#### 差强人意的 text-classification-keras
项目地址：https://github.com/jfilter/text-classification-keras

该项目是对 keras-text 项目的改进，总体上来说是一个可用的项目，但存在以下问题：

* 使用文档不齐全
* 代码上仍然有一些致命伤，比如
  * 将文本转成特征向量后，先存了一个文件，然后从文件中加载后再喂给模型……意义不明……
  * 每次调用的时候都要把 spaCy 的模型重新加载一遍，慢得要死

作者应该是从 keras-text 项目 fork 过来然后改成能用的状态的，也挺不容易的，但不管怎么说这不是一个合格的工具。

### 可用的文本分类工具及其使用方法
#### 使用 NLTK 进行文本分类
安装: `pip install nltk`

文档: `https://www.nltk.org/api/nltk.classify.html`

NLTK 提供了大量的文本处理方法，同时提供了通用的分类器接口，组合起来就能进行文本分类了。

以其中的朴素贝叶斯 NaiveBayesClassifier 为例，可以这样来进行文本分类

* 实现一个方法，将文本转成 dict 形式的特征

以英文为例，可以直接用 NLTK 中的分词方法，需要的话还可以加上 stemming 或者 lemmatization。
```python
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize

def extract_feature(text):
    feature = {}
    for word in word_tokenize(text):
        if word not in stopwords:
            feature[word] = 1

    return feature
```
中文的话可以换成 jieba 或者其他中文分词工具。

* 训练
```python
from nltk.classify import NaiveBayesClassifier


train_texts = [
    # ...
]
train_labels = [
    # ...
]

train_features = [extract_feature(text) for text in train_texts]
train_samples = list(zip(train_features, train_labels))
classifier = NaiveBayesClassifier.train(train_samples)
```
* 评估
```python
from nltk.classify import accuracy

test_texts = [
    # ...
]
test_labels = [
    # ...
]

test_features = [extract_feature(text) for text in test_texts]
test_samples = list(zip(test_features, test_labels))
acc = accuracy(classifier, test_samples)
```
* 预测

用 classify 方法直接预测最可能的类别
```python
text = "blablabla"              # 待预测的文本
feature = extract_feature(text)
pred_label = classifier.classify(feature)
```
用 prob_classify 方法获得所有可能类别的预测分数
```python
text = "blablabla"              # 待预测的文本
feature = extract_feature(text)
prob = classifier.prob_classify(feature)
```
* 模型保存和读取

可以直接用 pickle 保存、读取训练好的模型

保存：
```python
import pickle

with open('model.pkl', 'wb') as f:
    pickle.dump(classifier, f)
```
读取：
```python
import pickle

classifier = None
with open('model.pkl', 'rb') as f:
    classifier = pickle.load(f)
```
NLTK 中还有其他分类器，使用方法和 NaiveBayesClassifier 大同小异。

#### 使用 TextBlob 进行文本分类
注意：TextBlob 仅支持英文

安装: `pip install textblob`

文档: `https://textblob.readthedocs.io/en/dev/classifiers.html`

TextBlob 是一个基于 NLTK 的文本处理工具，其中的文本分类功能也是建立在 NLTK 中分类器的基础上的。

* 训练
```python
from textblob.classifiers import NaiveBayesClassifier

train_texts = [
    # ...
]
train_labels = [
    # ...
]
train_samples = list(zip(train_texts, train_labels))
classifier = NaiveBayesClassifier(train_samples)
```
* 评估
```python
test_texts = [
    # ...
]
test_labels = [
    # ...
]
test_samples = list(zip(test_texts, test_labels))
acc = classifier.accuracy(test_samples)
```
* 预测

只有一个 classify 接口预测得到最有可能的类别
```python
label = classifier.classify("this is a sentence to be classified")
```
* 模型保存和读取

同 NLTK。

相比 NLTK 中原来的文本分类，TextBlob 的封装隐藏了一些细节，简化了接口，用起来还是挺方便的。不好的一点是，TextBlob 里强制依赖了 NLTK 里的 word_tokenize，虽然说 word_tokenize 可以通过 language 参数设置语言，但在 TextBlob 里没有提供传递这个参数的机会，这就导致 TextBlob 只能对英文进行分类。

#### 使用 TextGrocery 进行文本分类
注意：TextGrocery 仅支持 Python2

安装: `pip install tgrocery`

文档: `https://github.com/2shou/TextGrocery/blob/master/README_CN.md`

* 初始化

需要给分类器指定一个名字
```python
from tgrocery import Grocery

classifier = Grocery('test')
```
默认使用 jieba 作为分词器，但也支持在初始化分类器的时候通过 custom_tokenize 参数来自定义分词器
```python
classifier = Grocery('test', custom_tokenize=list)
```
要求 custom_tokenize 的参数值是一个 python 的函数。

* 训练

支持传入 python 数据进行训练：
```python
train_src = [
    ('education', '名师指导托福语法技巧：名词的复数形式'),
    ('education', '中国高考成绩海外认可 是“狼来了”吗？'),
    ('sports', '图文：法网孟菲尔斯苦战进16强 孟菲尔斯怒吼'),
    ('sports', '四川丹棱举行全国长距登山挑战赛 近万人参与')
]
classifier.train(train_src)
```
也支持从文件中读取训练数据然后训练，要求文件中一行是一个数据，且行中有一个分隔符把文本和文本的类别标签分隔开，如用竖线分隔：
```
education|名师指导托福语法技巧：名词的复数形式
education|中国高考成绩海外认可 是“狼来了”吗？
sports|图文：法网孟菲尔斯苦战进16强 孟菲尔斯怒吼
sports|四川丹棱举行全国长距登山挑战赛 近万人参与
```
假设上面的内容存储在 train.txt 中，则将 train.txt 作为 train 的参数，同时要用 delimiter 参数指明分隔符
```python
classifier.train('train.txt', delimiter='|')
```
* 评估
```python
test_src = [
    ('education', '福建春季公务员考试报名18日截止 2月6日考试'),
    ('sports', '意甲首轮补赛交战记录:米兰客场8战不败国米10年连胜'),
]
report = classifier.test(test_src)
report.show_result()
```
上述代码会输出如下内容：
```
               accuracy       recall
education      50.00%         100.00%
sports         0.00%          0.00%
```
也可以从文件中读取数据进行评估，文件的要求同训练
```python
report = classifier.test('test.txt', delimiter='|')
report.show_result()
```
* 预测

使用 predict 接口来进行预测
```python
preds = classifier.predict('意甲首轮补赛交战记录:米兰客场8战不败国米10年连胜')
print preds.dec_values         # => {'education': 0.00604235155848336, 'sports': -0.006042351558483356}
print preds.predicted_y        # => education
print str(preds)               # => education
```
* 模型保存和读取

用 save 方法来保存模型
```python
classifier.save()
```
保存模型时会用分类器初始化时给的名字来创建一个目录，比如最开始给的名字是 test，所保存的模型会在 test 目录下，如下所示：
```
test
├── converter
│   ├── class_map.config.pickle
│   ├── feat_gen.config.pickle
│   └── text_prep.config.pickle
├── id
└── learner
    ├── idf.pickle
    ├── liblinear_model
    └── options.pickle
```
用相同的名字创建一个分类器，然后执行 load 方法来读取模型
```python
classifier = Grocery('test', custom_tokenize=list)
classifier.load()
```
这里需要注意的是，保存模型的时候，自定义的分词器是没有被保存下来的，所以在读取的时候，还需要重新设置一下分词器。

TextGrocery 是一个基于 liblinear 的小巧的文本分类实现，可惜作者已经放弃维护了，目前只能在 Python2 环境里面使用。

#### 使用 sklearn 进行文本分类
安装: `pip install scikit-learn`

文档: `https://scikit-learn.org/stable/tutorial/text_analytics/working_with_text_data.html#training-a-classifier`

sklearn 中实现了很多的分类器，并且提供了统一的接口，比较友好。

* 训练

首先创建一个 vectorizer 用来将文本编码成向量，最常用的可能是 TfidfVectorizer 了
```python
from sklearn.feature_extraction.text import TfidfVectorizer

vectorizer = TfidfVectorizer()
```
默认会按空格来分词，如果需要自定义分词器，可以通过 tokenizer 参数来传入一个函数，比如
```python
import jieba

def jieba_tokenize(text):
    return jieba.lcut(text)

vectorizer = TfidfVectorizer(tokenizer=jieba_tokenize)
```
注意：由于 jieba 中加了线程锁，将 jieba.lcut 直接传入，会导致模型无法保存

这个 vectorizer 是需要训练的
```python
texts = [
    '名师指导托福语法技巧',
    '中国高考成绩海外认可',
    '法网孟菲尔斯苦战进16强',
    '四川丹棱举行登山挑战赛',
]
vectorizer.fit(texts)
```
一旦训练后，对任意一个文本，会产生一个固定长度的向量，比如：
```python
print(vectorizer.transform(['名师指导托福语法技巧']).toarray())
```
上面的代码会输出
```
[[0.        0.        0.        0.        0.4472136 0.        0.
  0.        0.        0.4472136 0.4472136 0.4472136 0.        0.
  0.        0.        0.        0.        0.        0.4472136 0.
  0.       ]]
```
向量化还有其他方法，如下：
```python
from sklearn.feature_extraction.text import (
    TfidfVectorizer,
    CountVectorizer,
    HashingVectorizer,
)
from sklearn.feature_extraction import DictVectorizer
```
创建一个分类器，比如 SVM
```python
from sklearn.svm import LinearSVC

classifier = LinearSVC()
````
如果想使用 GBDT 分类器的话，可以执行 pip install xgboost 安装 XGBoost 这个包，它提供了符合 sklearn 规范的接口，可以直接使用并像 sklearn 的分类器一样用在后面的训练、预测过程中：
```python
from xgboost import XGBClassifier

classifier = XGBClassifier()
```
首先用 vectorizer 将训练数据中的文本转成矩阵，然后喂给分类器进行训练
```python
train_texts = [
    # blablabla
]
train_labels = [
    # blablabla
]
train_feats = vectorizer.transform(train_texts)
classifier.fit(train_feats, train_labels)
```
* 评估

用分类器的 score 方法可以计算测试集的 accuracy
```python
test_texts = [
    # ...
]
test_labels = [
    # ...
]
test_feats = vectorizer.transform(test_texts)
acc = classifier.score(test_feats, test_labels)
```
这个方法其实是调用了 accuracy_score 这个函数，所以也可以自己来计算
```python
from sklearn.metrics import accuracy_score

pred_labels = classifier.predict(test_feats)
acc = accuracy_score(test_labels, pred_labels)
```
还可以用 classification_report 这个函数来得到更详细的评估报告
```python
from sklearn.metrics import classification_report

pred_labels = classifier.predict(test_feats)
print(classification_report(test_labels, pred_labels))
```
输出结果是下面这个样子的：
```
              precision    recall  f1-score   support

     class 0       0.50      1.00      0.67         1
     class 1       0.00      0.00      0.00         1
     class 2       1.00      0.67      0.80         3

    accuracy                           0.60         5
   macro avg       0.50      0.56      0.49         5
weighted avg       0.70      0.60      0.61         5
```
有时候我们还需要输出分类的混淆矩阵，虽然 sklearn 提供了 sklearn.metrics.confusion_matrix 这个方法来计算混淆矩阵，但它的输出不够直观，pandas.crosstab更加方便
```python
import pandas

pred_labels = classifier.predict(test_feats)
cnf_matrix = pandas.crosstab(
    pandas.Series(test_labels), pandas.Series(pred_labels),
    rownames=['targets'], colnames=['preds']
)
```
输入结果是下面这个样子：
```
preds     negative  positive

targets
negative       590       126
positive       383       901
```
* 预测

用 predict 方法来预测最可能的类别，或用 predict_proba 方法来获得所预测类别的分数
```python
texts = ['text1', 'text2', 'text3']
feats = vectorizer.transform(texts)
labels = classifier.predict(feats) # labels: ['label1', 'label2', 'label3']
# or
prob_list = classifier.predict_proba(feats)
# prob_list:
# [
#     {'label1': 0.1, 'label2': 0.3, 'label3': 0.6},
#     {'label1': 0.1, 'label2': 0.3, 'label3': 0.6},
#     {'label1': 0.1, 'label2': 0.3, 'label3': 0.6},
# ]
```
注意 sklearn 中的 predict/predict_proba 都被设计为批量预测，没有单个数据预测的接口。

* 模型保存和读取

保存模型用 pickle 或者 joblib 都可以，注意要把 vectorizer 和 classifier 一起保存。
```python
import pickle
from sklearn.externals import joblib

with open('model.pkl', 'wb') as f:
    data = [vectorizer, classifier]
    pickle.dump(data, f)

# or
data = [vectorizer, classifier]
joblib.dump(data, 'model.pkl')
```
如果使用 pickle.dump 保存的模型，则用 pickle.load 来读取；如果是用 joblib.dump 保存的则用 joblib.load 读取
```python
vectorizer, classifier = None, None
with open('model.pkl', 'rb') as f:
    vectorizer, classifier = pickle.load(f)

# or
vectorizer, classifier = joblib.load('model.pkl')
```
除了上面这样先创建 vectorizer 再创建 classifier 的方法，sklearn 还提供了 Pipeline 这个类来简化这个过程，非常推荐使用。

创建 vectorizer 和 classifier 后，用 Pipeline 把它们组合起来：
```python
from sklearn.pipeline import Pipeline

vectorizer = TfidfVectorizer()
classifier = LinearSVC()
pipeline = Pipeline([('vec', vectorizer), ('model', classifier)])
```
然后可以直接将文本喂给 pipeline，不用自己再去调用 vectorizer.fit 和 vectorizer.transform 来将文本编码成向量了！
```python
train_texts = [
    # blablabla
]
train_labels = [
    # blablabla
]
pipeline.fit(train_texts, train_labels)
```
评估、预测和非 pipeline 方式的差不多，都是可以省略掉将文本转成向量的这个步骤；模型保存时只需要将 pipeline 保存成文件即可。

#### 使用 FastText 进行文本分类
安装: `pip install fasttext`

文档: `https://fasttext.cc/docs/en/python-module.html#text-classification-model`

* 数据格式

fasttext 的训练和评估都只能从文件中读取数据，而不能直接传入 Python 的值，而且对文件的格式是有要求的

1. 文件中一行一个样本
2. 每行用制表符分隔，第一列是标签，第二列是文本
3. 第一列的标签要有 __label__ 前缀
4. 第二列的文本必须是用空格分隔的词序列，对中文来说，意味着需要先分好词

文件内容示例如下：
```
__label__education	名师 指导 托福 语法 技巧 ： 名词 的 复数 形式
__label__education	中国 高考 成绩 海外 认可 是 “ 狼 来了 ” 吗 ？
__label__sports	图文 ： 法网 孟菲尔斯 苦战 进 16强 孟菲尔斯 怒吼
__label__sports	四川 丹棱 举行 全国 长距 登山 挑战赛 近 万人 参与
```

* 训练

假设训练数据按照前面的要求写在了 train_data.txt 里，则用下面的代码来训练：
```python
import fasttext

model = fasttext.train_supervised('train_data.txt')
```
* 评估

假设测试数据在 test_data.txt 中，使用 test 方法来评估模型效果，它会返回数据集中的样本数量，以及 precesion 和 recall 值：
```python
num, precesion, recall = model.test('test_data.txt')
```
也可以用 test_label 方法获得每个类别的 precesion、recall 和 f1 值：
```python
print(model.test_label('test_data.txt'))
```
输出结果是下面这个样子的：
```
{
    '__label__education': {
        'precision': 0.8830022075055187,
        'recall': 0.8784773060029283,
        'f1score': 0.8807339449541285
    },
    '__label__sports': {
        'precision': 0.883881230116649,
        'recall': 0.853121801432958,
        'f1score': 0.8682291666666667
    }
}
```
* 预测

用 predict 接口来对单条文本进行预测，同样要求文本是用空格分隔的、分好词的
```
top3_labels, top3_scores = model.predict('土豆网 拟 明年 登陆 纳市 募资 1.5 亿美元', k=3)
```

* 模型保存和读取

保存
```python
model.save_model('model.bin')
```
读取
```python
import fasttext
model = fasttext.load_model('model.bin')
```
#### 使用 Kashgari 进行文本分类
安装: `pip install kashgari-tf tensorflow==1.14.0`

文档: `https://kashgari.bmio.net/`

Kashgari 是一个基于神经网络模型的 NLP 工具，内部实现大多数常用的神经网络模型，也支持了最新的 BERT，使用体验挺不错的。

##### 进行常规的文本分类
* 训练

Kashgari 要求输入的文本是分好词的，把分词的事情留给用户自己处理。不过分好词就能直接输入到模型中了，不需要像 sklearn 一样通过 vectorizer 转成向量：
```python
from kashgari.tasks.classification.models import CNN_Model

train_x = [['Hello', 'world'], ['Hello', 'Kashgari']]
train_y = ['a', 'b']

model = CNN_Model()
model.fit(train_x, train_y)
```
训练时还可以设置校验集
```python
val_x = [['Hello', 'world'], ['Hello', 'Kashgari']]
val_y = ['a', 'b']

model.fit(val_x, val_y)
```
* 评估
```python
test_x = [['Hello', 'world'], ['Hello', 'Kashgari']]
test_y = ['a', 'b']
model.evaluate(test_x, test_y)
```
会打印测试结果到标准输出，其内容是下面这个格式的：
```
              precision    recall  f1-score   support

      sports     1.0000    1.0000    1.0000      1000
   education     1.0000    0.9980    0.9990      1000
  technology     0.9930    1.0000    0.9965      1000

    accuracy                         0.9985     10000
   macro avg     0.9985    0.9985    0.9985     10000
weighted avg     0.9985    0.9985    0.9985     10000
```
* 预测

使用 predict 方法来预测最可能的类别
```python
tokens = ['姚明', '：', '对', '奥尼尔', '不得', '不服']
model.predict([tokens])          # => ['sports']
```
或者用 predict_top_k_class 来获取 topk 的预测结果及分数
```python
print(model.predict_top_k_class([tokens], top_k=3))
```
结果
```
[
    {
        'label': 'sports',
        'confidence': 0.50483656,
        'candidates': [
            {'label': 'education', 'confidence': 0.057417843},
            {'label': 'technology', 'confidence': 0.048766118},
        ]
    }
]
```
* 模型保存和读取
保存

使用 save 方法将模型保存到 test 目录中，目录不存在会创建
```python
model.save('test')
```
目录中会有一个描述模型结构的 model_info.json 和记录模型参数的 model_weights.h5
```
test
├── model_info.json
└── model_weights.h5

0 directories, 2 files
```
读取

使用 kashgari.utils.d_model 来读取模型
```python
from kashgari.utils import load_model

model = load_model('test')
```
##### 基于 BERT 进行文本分类
先下载 BERT 模型。

中文的话可以用 Google 开放的: https://storage.googleapis.com/bert_models/2018_11_03/chinese_L-12_H-768_A-12.zip

中文模型下载后解压得到 chinese_L-12_H-768_A-12 这个目录

然后创建基于 BERT 的分类器
```python
from kashgari.embeddings import BERTEmbedding
from kashgari.tasks.classification.models import CNN_Model

embedding = BERTEmbedding('chinese_L-12_H-768_A-12/', task=kashgari.CLASSIFICATION)
model = CNN_Model(embedding)
```
之后的训练、评估、预测，都和非 BERT 的模型一样。

默认情况下 BERTEmbedding 被设置为不可训练，如果需要对 BERT 进行 finetuning 的话，那么按如下设置：
```python
embedding = BERTEmbedding('chinese_L-12_H-768_A-12/', task=kashgari.CLASSIFICATION, trainable=True)
```
#### 使用 AllenNLP 进行文本分类
安装: `pip install allennlp`

文档: `https://allennlp.org/tutorials`

##### 进行常规的文本分类
AllenNLP 完全通过配置文件来对数据处理、模型结果和训练过程进行设置，最简单的情况下可以一行代码不写就把一个文本分类模型训练出来。下面是一个配置文件示例：
```
{
    "dataset_reader": {
        "type": "text_classification_json",
        "tokenizer": {
            "type": "word",
            "word_splitter": {
                "type": "jieba",
            }
        }
    },
    "train_data_path": "allen.data.train",
    "test_data_path": "allen.data.test",
    "evaluate_on_test": true,
    "model": {
        "type": "basic_classifier",
        "text_field_embedder": {
            "tokens": {
                "type": "embedding",
                "embedding_dim": 100,
                "trainable": true
            }
        },
        "seq2vec_encoder": {
            "type": "cnn",
            "embedding_dim": 100,
            "num_filters": 1,
            "ngram_filter_sizes": [2, 3, 4]
        }
    },
    "iterator": {
        "type": "bucket",
        "sorting_keys": [["tokens", "num_tokens"]],
        "batch_size": 64
    },
    "trainer": {
        "num_epochs": 40,
        "patience": 3,
        "cuda_device": -1,
        "grad_clipping": 5.0,
        "validation_metric": "+accuracy",
        "optimizer": {
            "type": "adam"
        }
    }
}
```
配置文件中的内容可以分成

* 数据部分: 包括 dataset_reader/train_data_path/test_data_path 这几个 key 及其 value
* 模型部分: 就是 model 这个 key 的内容
* 训练部分: 包括 evaluate_on_test/iterator/trainer 这几个 key 及其 value
下面对这些配置做简要说明，详细内容可查看文档。

* 数据部分

   train_data_path 和 test_data_path 比较好理解，它们指定了训练数据和测试数据的文件路径；而 data_reader 则限定了数据文件的格式。

   data_reader 中的配置，会被用来构建一个 DatasetReader 的子类的对象，用来读取数据并转换成一个个 Instance 对象。

   * 内置的可用来读取分类数据的 DataReader 是 TextClassificationJsonReader ，所以配置中有
   ```
   "type": "text_classification_json"
   ```
   这个 type 的值是 TextClassificationJsonReader 这个类实现的时候注册上的，去看代码会看到有这样的片段
   ```
   @DatasetReader.register("text_classification_json")
   class TextClassificationJsonReader(DatasetReader):
   ```
   这个 TextClassificationJsonReader 要求的数据文件是一行一个 json 数据，如下：
   ```
   {"label": "education", "text": "名师指导托福语法技巧：名词的复数形式"}
  {"label": "education", "text": "中国高考成绩海外认可是“狼来了”吗？"}
  {"label": "sports, "text": "图文：法网孟菲尔斯苦战进16强孟菲尔斯怒吼"}
  {"label": "sports, "text": "四川丹棱举行全国长距登山挑战赛近万人参与"}
   ```
   DataReader 通过配置中 tokenizer 部分会创建一个分词器，用来将文本转换为词序列
   ```
   "tokenizer": {
       "type": "word",
       "word_splitter": {
           "type": "jieba",
       }
   }
   ```
   type 的值设置为 word，这没什么好说的。

   tokenizer 中的 word_splitter 指定的才是真正的分词器（比较绕）。

   如果是英文的数据，那么 word_splitter 的配置可以不写，默认就是支持英文分词的。

   但如果是用于中文处理的话，有一个 SpacyWordSplitter 可以用于中文分类，但是现有的中文 spaCy 模型仅支持 spaCy 2.0.x，和 AllenNLP 中 spaCy 要求的版本不兼容，这个是比较坑的。

   好在 AllenNLP 提供了加载自定义模块的方法，按照如下方法来处理这个问题
   ```
   mkdir allen_ext/
   touch allen_ext/__init__.py
   touch allen_ext/word_splitter.py
   ```
   然后在 allen_ext/word_splitter.py 中写入如下内容
   ```python
from typing import List

import jieba
from overrides import overrides
from allennlp.data.tokenizers.token import Token
from allennlp.data.tokenizers.word_splitter import WordSplitter


@WordSplitter.register('jieba')
class JiebaWordSplitter(WordSplitter):

    def __init__(self):
        pass

    @overrides
    def split_words(self, sentence: str) -> List[Token]:
        offset = 0
        tokens = []
        for word in jieba.lcut(sentence):
            word = word.strip()
            if not word:
                continue

            start = sentence.find(word, offset)
            tokens.append(Token(word, start))

            offset = start + len(word)

        return tokens
    ```
   使用 WordSplitter.register('jieba') 后就可以在配置中 word_splitter 部分写上 "type": "jieba" 来启用。

   在 allen_ext/__init__.py 中写入如下内容
   ```python
from .word_splitter import JiebaWordSplitter

__all__ = ['JiebaWordSplitter']
   ```
   自定义了 JiebaWordSplitter 后在训练的时候还要加载 allen_ext 这个目录才能生效，这个之后再说。

* 模型部分

   因为是做文本分类，所以 type 设置为 basic_classifier。

   这个分类器需要 text_field_embedder 和 seq2vec_encoder 两个参数：

   * text_field_embedder 用来定义 word embedding，这个配置应该还好理解
   ```python
   "text_field_embedder": {
       "tokens": {
           "type": "embedding",
           "embedding_dim": 100,
           "trainable": true
       }
   }
   ```
   seq2vec_encoder 则用来产生句子的编码向量用于分类，这里选择了 CNN
   ```
   "seq2vec_encoder": {
    "type": "cnn",
    "embedding_dim": 100,
    "num_filters": 1,
    "ngram_filter_sizes": [2, 3, 4]
   }
   ```
* 训练部分：略

配置文件写好后，假设配置文件为 config.json，直接执行下面的命令来训练即可
```
allennlp train config.json -s model_save_dir --include-package allen_ext
```
选项 --include-package allen_ext 用来来加载自定义的模块。

最终会在 save_dir 目录下产生一个 model.tar.gz 文件，就是模型参数，然后目录下还会产生 tensorboard 能读取的 log，这个挺方便的。

评估用 evaluate 命令
```
allennlp evaluate model_save_dir/model.tar.gz test.jsonl --include-package allen_ext
```
比较麻烦的是，预测需要一个 Predictor，而 AllenNLP 中内置的 TextClassifierPredictor 要求的输入是 {"sentence": "xxx"} ，这个和 TextClassificationJsonReader 的要求不一样……

如果是在代码里进行预测，那么是没有问题的，可以这样
```python
from allen_ext import *         # noqa
from allennlp.models.archival import load_archive
from allennlp.predictors.predictor import Predictor

archive = load_archive('model_save_dir/model.tar.gz')
predictor = Predictor.from_archive(archive)

inputs = {"sentence": "名师指导托福语法技巧：名词的复数形式"}
result = predictor.predict_json(inputs)
```
得到的 result 是这样的结构
```
{
    'label': 'education',
    'logits': [
        15.88630199432373,
        0.7209644317626953,
        7.292031764984131,
        5.195938587188721,
        5.073373317718506,
        -35.6490478515625,
        -7.7982988357543945,
        -35.44648742675781,
        -18.14293098449707,
        -14.513381004333496
    ],
    'probs': [
        0.999771773815155,
        2.592259420453047e-07,
        0.0001851213601185009,
        2.2758060367777944e-05,
        2.013285666180309e-05,
        4.153195524896307e-23,
        5.1737975015342386e-11,
        5.085729773519049e-23,
        1.6641527142180782e-15,
        6.273159211056881e-14
    ],
}
```
这个输出结构完全是由 TextClassifierPredictor 决定的。

如果要自定义 Predictor，可以参考文档。

#####　基于 BERT 进行文本分类
AllenNLP 是基于 pytorch 实现的，所以 Google 提供的 BERT 模型在它这里没法用，需要下载它自己提供的模型，以中文模型为例：
```
mkdir chinese_bert_torch && cd chinese_bert_torch
wget https://s3.amazonaws.com/models.huggingface.co/bert/bert-base-chinese-pytorch_model.bin -O pytorch_model.bin
wget https://s3.amazonaws.com/models.huggingface.co/bert/bert-base-chinese-config.json -O config.json
wget https://s3.amazonaws.com/models.huggingface.co/bert/bert-base-chinese-vocab.txt -O vocab.txt
```
然后 config.json 中 data_reader 部分这样写
```
{
    "dataset_reader": {
        "type": "text_classification_json",
        "tokenizer": {
            "type": "word",
            "word_splitter": {
                "type": "bert-basic",
            }
        },
        "token_indexers": {
            "bert": {
                "type": "bert-pretrained",
                "pretrained_model": "./chinese_bert_torch/vocab.txt"
            }
        }
    }
}
```
model 部分这么写
```
{
    "model": {
        "type": "bert_for_classification",
        "bert_model": "./chinese_bert_torch",
        "trainable": false
    }
}
```
这里 trainable 设置成 false 的话 BERT 就只是充当一个 encoder，不参与训练；如果要进行 finetuning 的话将其改为 true。

完整的配置是这个样子的
```
{
    "dataset_reader": {
        "type": "text_classification_json",
        "tokenizer": {
            "type": "word",
            "word_splitter": {
                "type": "bert-basic",
            }
        },
        "token_indexers": {
            "bert": {
                "type": "bert-pretrained",
                "pretrained_model": "./chinese_bert_torch/vocab.txt"
            }
        }
    },
    "train_data_path": "allen.data.train",
    "test_data_path": "allen.data.test",
    "evaluate_on_test": true,
    "model": {
        "type": "bert_for_classification",
        "bert_model": "./chinese_bert_torch",
        "trainable": false
    },
    "iterator": {
        "type": "bucket",
        "sorting_keys": [["tokens", "num_tokens"]],
        "batch_size": 64
    },
    "trainer": {
        "num_epochs": 5,
        "patience": 3,
        "cuda_device": -1,
        "grad_clipping": 5.0,
        "validation_metric": "+accuracy",
        "optimizer": {
            "type": "adam"
        }
    }
}
```
训练、评估、预测等操作同未使用 BERT 的时候一样。
