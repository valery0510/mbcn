# 第9章 竞争币、竞争块链和应用程序

比特币是20多年的分布式系统和货币研究的结果，是一项具有革命性的新技术：一种基于工作量证明的去中心化的一致性机制。这项比特币的核心发明引领了一场包括货币体系、金融服务、经济学、分布式系统、投票系统、联合监管和合同体系在内的创新浪潮。

本章将探讨比特币和区块链的发明的衍生物：2009年比特币诞生以来所涌现出来的竞争币、竞争块链和应用程序。大部分篇幅将要探讨竞争币（alt coin），这些电子货币有着与比特币相似的的构建模式出来的，但它们完全独立地运行在自己的网络和块链系统之上。

除了我们将在本章讨论到的竞争币以外，至少还有50种以上的竞争币未能论及，这或许会引来这些竞争币的创造者或粉丝们的不满。但这一章节的目的并不是为了给提到的竞争币背书，讨论到的竞争币也不是作者根据主观判断选择的。相反，这一章节讨论的是每一种不同的创新性的竞争币里的代表币种，以此来展现整个竞争币生态系统的宏大和多样。从货币的角度考虑，有些很有趣的竞争币实际上是完全失败的，从而让这些例子研究起来变得更有趣，同时也表明本章所讲并非投资建议。

由于每天都会有新的竞争币出现，因此我们的讨论难免会有遗漏，甚至漏掉的就是改变历史的币种。目前这个领域的创新速度快得令人兴奋，同时也预示着，从本书发布之日起，这一章的讨论就将不再有时效性和完备性。

## 9.1 竞争币和竞争块链的分类

比特币是一个开源项目，其源代码也作为其他的一些软件项目的基础。由比特币衍生出来的最常见的形式，就是替代性去中心化货币，简称“竞争币”，这类货币使用跟比特币同样的创建块链的方式来实现自己的电子货币系统。

在比特币的块链上层，可以实现一系列的协议层。元币、元块链或者块链应用程序以块链为平台，或通过增加协议层的方式扩展比特币协议。如彩色币，万事达币以及合约币。

下一部分我们将介绍一些值得注意的竞争币，比如Litecoin, Dogecoin, Freicoin, Primecoin, Peercoin,Darkcoin和Zerocoin。之所以提到这些，并不是因为它们是最好的或是市值最高的竞争币，而是因为他们是历史上某种竞争币创新的典型代表。

除了竞争币，还有一些关于块链其他实现，他们并不是“币”，可以称之为“竞争块链”（alt chains）。竞争块链通过实现一致性和分布式账簿机制来给诸如合同、名字注册和其他一些应用提供服务。竞争块链使用的是和比特币一样的创建块的机制，有时也会采用货币或代币的支付机制，但它们的主要目的不是为了维持一个货币系统。我们后续将探讨竞争块链的典型代表：域名币、以太坊和 NXT。

除了比特币系统使用的基于工作量证明的一致性机制这种协议以外，还有基于资源证明或发布证明的一些试验性协议。后续将探讨以Maidsafe和Twister为代表的这类协议。

最后，有一些比特币的竞争者，比如Ripple等，也提供电子货币和交易网络，但并没有像比特币一样使用分布式账簿或者一致性机制。这些不基于块链技术的电子货币系统不在本书的讨论范畴，故不会在本章节出现。

## 9.2 元币平台

元币和元块链是在比特币之上实现的软件层，也可以认为是覆盖在比特币系统之上的平台/协议，或者是在一个币中币的实现。这些功能层拓展了核心比特币协议，使得在比特币交易和比特币地址中编码附加信息成为可能。元币的第一个实现利用了大量的 hack 技巧把元数据添加到比特币块链中，比如使用比特币地址编码数据，或者利用空白的交易字段存放新协议层增加的这些元数据。自从交易脚本操作码问世之后，元币得以直接将信息存放在块链之中。

### 9.2.1 染色币

染色币是一种在少量比特币上存储信息的一种元协议。一个“被染色的”币，是一定数额的重新用于表达另一种资产的比特币。想象一下，在一张一美金的纸币上盖上写有一行“这是Acme公司的一份股权的证明”的印章。现在这张一美金的纸币就有了两层意义，它既是流通的货币，同时又是一份股权证明。由于它作为一份股权证明的价值更大一些，因此你肯定不大会用它来购买糖果吃了（而是保留着），这也让这张纸币不再具有货币的流通属性。染色币也是这个工作原理，通过将一笔数额不大的具体比特币交易转化为某种证明来指征另外一笔财产。所谓“染色”也仅仅是一种隐喻，并非字面意思，而是指增加属性（比如给个颜色）的方式。因此，染色币并没有颜色。

染色币由特殊的钱包管理，这类钱包存储和解析依附在染色币上的元信息。用户在使用这类钱包的时候，可以通过增加有着某种特殊含义的标签的方式，将一般的比特币“染色”为染色币。比如说，这种标签的内容可以表示股票证明、优惠券信息、实际财产、商品或者可收集的代币等等。如何书写和解读这类标签，完全取决于给这枚比特币“染色”的人，他可以决定附着在这部分比特币上的元信息属性。比如信息类型、能不能再分割、某种符号或描述，或者其他的相关信息。这部分比特币一旦被染色，这些币可以用来交易、分割、合并和获取利息等。被染色的比特币也可用通过删除附着信息的方式，也能将“被染色的”比特币恢复为普通比特币。

如例9-1所示，为了演示染色币的使用，我们创建了20单位带有元信息“MasterBTC”的染色币，其中“MasterBTC”代表了可以获取本书免费拷贝的兑换码。每一单位的这种染色币，都可以被出售或赠予给任何装有兼容染色币协议钱包的人，拥有这种染色币的人可以继续转手或者用它来兑换本书的免费拷贝。[染色币的例子](https://cpr.sm/FoykwrH6UY)如下。

**例9-1 The metadata profile of the colored coins recorded as a coupon for a free copy of the book** 

```
{
  "source_addresses": [
    "3NpZmvSPLmN2cVFw1pY7gxEAVPCVfnWfVD"
  ],
  "contract_url": "https://www.coinprism.info/asset/ 3NpZmvSPLmN2cVFw1pY7gxEAVPCVfnWfVD",
  "name_short": "MasterBTC",
  "name": "Free copy of \"Mastering Bitcoin\"",
  "issuer": "Andreas M. Antonopoulos",
  "description": "This token is redeemable for a free copy of the book \"Mastering
Bitcoin\"",
  "description_mime": "text/x-markdown; charset=UTF-8",
  "type": "Other", 
  "divisibility": 0, 
  "link_to_website": false, 
  "icon_url": null, 
  "image_url": null, 
  "version": "1.0"
}
```

### 9.2.2 万事达币

万事达币是另一个建立在比特币之上的协议，该协议支持多个平台对比特币系统的扩展。万事达币使用名为MST的代币来指导交易，但它并不是一种通货。相反的，它服务于其他应用平台，比如用户货币，智能财产代币，去中心化的财产交易和合约系统等等。就像HTTP协议是TCP协议的应用层一样，Mastercoin是比特币协议的应用层协议。

类似HTTP协议利用TCP协议的80端口和其他协议的TCP流量加以区别，万事达币通过一个名为“exodus”的比特币地址（1EXoDusjGwvnjZUyKkxZ4UHEf77z6A5S4P）的进出交易机制来维持协议的运行。万事达币协议正从利用“exodus”地址和多方签名的机制转向利用OP_RETURN比特币操作符来编码信息。

### 9.2.3 合约币

合约币是另一个建立在比特币系统之上的协议层。合约币拥有用户货币、可交易代币、金融手段、去中心化财产交易和其他一些功能。合约币利用比特币脚本语言中的OP_RETURE操作符记录元信息来增加比特币交易的额外信息。合约币使用名为XCP的代币维持整个系统的运行。

### 9.3 竞争币/山寨币

绝大多数的山寨币都来自比特币源代码的克隆，少数则没有使用比特币的任何源码，仅仅是借鉴了块链的模型后自己实现。竞争币或竞争块链（下一节会讲到）都是运行在自己块链上的独立的块链实现。之所以以命名区分，主要是因为竞争币主要用做货币，而竞争块链则不是。

严格意义上讲，比特币的第一个克隆并不是一个竞争币而是一个名为Namecoin的竞争块链，我们将在下一节讨论。

从发布时间来看，第一款竞争币名为IXCoin，出现于2011年8月。IXCoin更改了比特币的一些参数，尤其是通过调整每个新块的奖励为96个币，从而增加了货币的发行量。

2011年9月，Tenebrix发布。Tenebrix是第一款使用了其他工作量证明算法（script）的加密货币，这种算法起初是为了防止密码遭暴力破解而设计的。Tenebrix的目标是通过使用这种消耗内存的算法来实现一种不依赖GPU和ASIC芯片的电子货币。

除了使用这种算法，莱特币还把新块产生的时间从比特币的10分钟缩短为2分半钟。如果把比特币看作电子货币中的金币的话，那么莱特币的愿景就是当电子货币系统中的银币，谋求成为比特币的一种轻量的替代货币。考虑到莱特币8,400万的货币总量和相对更快的确认速度，很多莱特币的拥趸相信与比特币相比，莱特币更适合零售业的交易。

以比特币和莱特币为基础的竞争币数量在2011和2012年呈持续增长状态。到了2013年，有20种竞争币在市场中谋求一席之地。到2013年年底，这个数字增至200种，2013年也因此被誉为“竞争币之年”。竞争币的增长在2014年依然没有放缓，截至本书截稿，市场上的竞争币数量已经达到了500种以上，其中超过一半的竞争币克隆自莱特币。

之所以市面上的竞争币有超过500种之多，是因为创造一种新的竞争币非常简单。因此，大多数的竞争币跟比特币区别非常小，并没有多少研究价值。但在这些通过毫无创意的抄袭和圈钱模式产生的竞争币中间，依然有一些值得一提的非常重要的创新。这些特殊的竞争币，要么采用完全不同的实现方式，要么在比特币现有的设计模式上加入了重大的创新。下面所列出的就是这些竞争币区别于比特币的三点主要不同：

▷ 货币策略不同
<br>▷ 基于工作量证明的一致性机制不同
<br>▷ 一些特殊的功能，比如更强的匿名性等等

For more information, see this [graphical timeline of alt coins and alt chains](http://mapofcoins.com/).

### 9.3.1 评估竞争币的价值 

市面上这么多竞争币，该如何决定关注哪些呢？一些竞争币旨在成为广泛流通的主流货币，还有一些是实验室项目，仅仅是为了测试不同的特性和货币模型，更多的仅仅是那些发起者们创富的手段。我一般通过某款竞争币的决定性特性和市场规模来对其进行价值评估。

以下是关于竞争币和比特币的不同之处的几个问题：
    
▷ 这款竞争币有没有引入重大的创新？
<br>▷ 如果有，那么这项创新是不是足够吸引使用比特币的用户转移过来？
<br>▷ 这款竞争币是不是致力于某一细分领域或应用？
<br>▷这款竞争币可以吸引到足够多的矿工来抵御一致性攻击吗？

还有一些有关关键财务和市场指标的问题：

▷ 这款竞争币的市场总值是多少？
<br>▷ 整个系统的用户/钱包规模大概是多少？
<br>▷ 接受其支付的商家有多少？
<br>▷ 整个系统每日的交易数是多少？
<br>▷ 交易总量是多少？
    
本节，我们将主要在技术和创新层面上就上述第一组的四个问题进行讨论。

### 9.3.2 货币属性不同于比特币的竞争币：莱特币、狗狗币和Freicoin

比特币本身所具有的一些货币属性令其成为总额固定并且不通货膨胀的货币。比如，比特币的总量为固定的2,100万枚，新币的生成速度随时间递减，块生成速度为十分钟一块，这个频率也控制了整个比特币系统交易的确认速度和新币的生成。很多竞争币通过对这些货币属性的微调，来达到实现不同的货币政策的目的。在这类竞争币中，值得一提的有以下几种。

#### 莱特币

莱特币是最早的一批竞争币中的一员，自2011年发布至今，已经成为继比特币之后的第二成功的电子货币。它的主要创新在于两点，一是使用了scrypt作为工作量证明算法（继承自前文提到的Tenebrix），二是更快的货币参数。

▷ 出块速度：2分半
<br>▷ 货币总量：到2140年达到8,400万
<br>▷ 一致性算法：scrypt
<br>▷ 市场总值：1亿6,000万美金（截至2014年年中）

#### 狗狗币

狗狗币是基于莱特币的一款竞争币，于2013年12月发布。狗狗币之所以值得一提，主要是因为其飞快的出块速度和惊人的货币总量，其目的也是为了鼓励用户交易和给小费等。狗狗币始于一个玩笑，在其2014年快速衰退之前，一经发布就风行于巨大而活跃的用户社区。下面是 狗狗币的一些特性：

▷ 出块速度：60秒
<br>▷ 货币总量：到2015年达到100,000,000,000（1,000亿）
<br>▷ 一致性算法：scrypt
<br>▷ 市场总值：1,200 万美金（截至2014年年中）

#### Freicoin

Freicoin于2012年7月发布。它是一种滞留性通货，可以理解为存在钱包中的货币的利率为负数。为了鼓励用户消费和减少储蓄，Freicoin拟定了一个4.5%的APR fee。Freicoin值得一提的原因是它的货币策略跟比特币的通货紧缩策略恰恰相反。作为货币，Freicoin并不是非常成功，但它是竞争币所能表现的多样性货币策略的生动体现。

▷ 出块速度：10分钟
<br>▷ 货币总量：到2140年达到1亿
<br>▷ 一致性算法：SHA256
<br>▷ 市场总值：13万美金（截至2014年年中）

### 9.3.3 一致性机制创新：peercoin，Myriad，Blackcoin，vericoin 和 NXT

比特币的一致性机制建立在基于SHA256算法的工作量证明之上。第一款引入scrypt算法作为一致性机制的竞争币是为了便于CPU挖矿，避免ASIC矿机可能导致的算力集中化的问题。在那之后，对于一致性机制的创新一直很活跃。诸多竞争币陆续引进了包括scrypt，scrypt-N, Skein, Groestl, SHA3, X11, Blake 在内的算法来实现工作量证明的一致性机制。而在2013年，作为工作量证明的一种替代机制——权益证明的出现，成为现代竞争币的基础。

权益证明系统中，货币的所有人可以将自己的通货做利息抵押。类似于存款证明(CD)，参与者可以保有他们货币的一部分，通过利息和矿工费的方式获取回报。

#### Peercoin

Peercoin于2012年8月发布，是首款工作量证明和权益证明混用的竞争币。

▷ 出块速度：10分钟
<br>▷ 货币总量：没有上限
<br>▷ 一致性算法：工作量证明和权益证明混用
<br>▷ 市场总值：140万美金（截至2014年年中）

#### Myriad

Myriad于2014年2月发布，值得一提的是，它同时使用5种工作量证明算法（HA256d, Scrypt, Qubit, Skein, or Myriad-Groestl），根据参与矿工的情况动态选择。这是为了让整个Myriad系统不受集中化的ASIC矿机的影响，同时也加强了其抵御一致性攻击的能力。

▷ 出块速度：平均30秒
<br>▷ 货币总量：到2024年达到 20 亿
<br>▷ 一致性算法：多重算法的工作量证明机制
<br>▷ 市场总值：12万美金（截至2014年中）

#### Blackcoin

Blackcoin发布于2014年2月，使用的是权益证明的一致性机制。同时，它引入的可以根据受益自动切换到不同竞争币的“多矿池”机制也值得一提。

▷ 出块速度：1分钟
<br>▷ 货币总量：没有上限
<br>▷ 一致性算法：权益证明机制
<br>▷ 市场总值：370万美金（截至2014年年中）

#### VeriCoin

VeriCoin于2014年5月发布。它使用了权益证明机制，并辅以随着市场供需关系动态调整的利率。它也是首款可以直接在钱包中兑换比特币支付的竞争币。

▷ 出块速度：1分钟
<br>▷ 货币总量：没有上限
<br>▷ 一致性算法：权益证明机制
<br>▷ 市场总值：110万美金（截至2014年年中）

#### NXT

NXT（发音同Next）是一种“纯”权益证明的竞争币，它甚至不采用工作量证明的挖矿机制。NXT是一款完全自己实现的加密货币，并非衍生自比特币或其他竞争币。NXT具有很多先进的功能，包括名字注册、去中心化资产交易、、集成的去中心化加密信息和权益委托。NXT的拥趸称NXT为新一代加密货币或者或者加密货币2.0。

▷ 出块速度：1分钟
<br>▷ 货币总量：没有上限
<br>▷ 一致性算法：权益证明机制
<br>▷ 市场总值：3,000万美金（截至2014年年年中）

### 9.3.4 多目的挖矿创新：Primecoin, Curecoin, Gridcoin

比特币的工作量证明机制只有一个目的：维护比特币系统的安全。跟维护一个传统货币系统比起来，挖矿的成本并不高。然而，某些批评者认为某些批评者认为挖矿这一行为是一种浪费。新一代的加密货币试图解决这个争议。多目的挖矿算法就是为了解决工作量证明导致的“浪费”问题而出现的。多目的挖矿在为货币系统的安全加入额外需求的同时，也为该系统的供需关系加入了额外的变量。

#### Primecoin

Primecoin是在2013年7月发布的。它它的工作量证明算法可以搜索质数，计算孪生素数表。素数在科研领域有广泛的应用。Primecoin的块链中包含其发现的质数，因此Primecoin的块链在用于维护公共交易账簿的同时，还会产生一份公开的科学发现（素数表）。

▷ 出块速度：1分钟
<br>▷ 货币总量：没有上限
<br>▷ 一致性算法：含有素数计算功能的工作量证明算法
<br>▷ 市场总值：130万美金（截至2014年年中）

#### Curecoin

Curecoin于2013年5月发布。通过Folding@Home项目，它将SHA256工作量证明算法和蛋白质褶皱结构的研究结合了起来。蛋白质褶皱研究需要对蛋白质进行生化反应的模拟，用于发现治愈疾病的新药，但这一过程需要大量的计算资源。

▷ 出块速度：10分钟
<br>▷ 货币总量：没有上限
<br>▷ 一致性算法：含有蛋白质结构研究功能的工作量证明算法
<br>▷ 市场总值：6.8万美金（截至2014年年中）

#### Gridcoin

Gridcoin是2013年10月对外发布的。它结合了以scrypt为基础的工作量证明算法和参与BOINC计算项目的补贴机制。BOINC——伯克利开发网络计算系统——是一项用于科学研究网格计算的开放协议。Gridcoin网络输出算力给BOINC这个计算平台，而不是自己直接用算力去解决某一个具体的科学问题。

▷ 出块速度：150秒
<br>▷ 货币总量：没有上限
<br>▷ 一致性算法：整合了BOINC网格计算的工作量证明算法
<br>▷ 市场总值：12.2万美金（截至2014年年中）

### 9.3.5 致力于匿名性的竞争币：CryptoNote, Bytecoin, Monero, Zerocash/Zerocoin, Darkcoin

比特币一直被误解为匿名货币。事实上，将个人和比特币地址关联起来，是一件相对容易的事情。利用大数据分析可以很容易地得到某一比特币地址的消费习惯。一些竞争币试图通过增强匿名性来解决这个问题。最初尝试的是Zerocoin，它是一种建立在比特币协议之上的元币协议，最早发布于2013 IEEE安全隐私讨论会上。截至本书完稿时，基于这个协议的Zerocash的竞争币系统还在开发当中。匿名性的另一种实现名为CryptoNote，初见于2013年10月的一篇论文。CryptoNote是一种由多个竞争币一起实现的基础技术，稍后将重点讨论。除了上述两种实现之外，还有一些其他的独立的匿名币，比如利用影子地址和交易混淆来达到匿名性目的的Darkcoin。

#### Zerocoin/Zerocash

Zerocoin是 2013 年由Johns Hopkins发表的电子货币匿名性的一种理论实现。截至本书完稿时，基于这一理论的Zerocash的竞争币系统还在开发当中。

#### CryptoNote

CryptoNote是一种提供了电子货币基础的匿名性的参考实现，于2013年10月发布。它可以被克隆继而衍生出其他实现，并且内建了一个周期性的重置机制使其不能用作货币。很多竞争币是基于CryptoNote实现的。比如Bytecoin (BCN), Aeon (AEON), Boolberry (BBR), duckNote (DUCK), Fantomcoin (FCN), Monero (XMR), MonetaVerde (MCN), 和Quazarcoin(QCN)。值得指出的是，CryptoNote是一个没有借鉴比特币的完全独立的实现。

#### Bytecoin

Bytecoin是CryptoNote的第一个实现，基于CryptoNote技术提供切实可行的匿名货币方案。Bytecoin于2012年发布。这里要留意一下，在基于CryptoNote的Bytecoin发布之前，有一个名字同样为Bytecoin的电子货币，货币符号为BTE，而基础CryptoNote的Bytecoin的货币符号为BCN。Bytecoin使用了基于Cryptonight的工作量证明机制，每个实例需要至少2MB的RAM，这使得GPU和ASIC矿机无法在Bytecoin网络中运行。Bytecoin继承了CryptoNote的环签名、不可链接交易和块链抗分析匿名性等机制。

▷ 出块速度：2分钟
<br>▷ 货币总量：1,840亿BCN
<br>▷ 一致性算法：基于Cryptonight的工作量证明机制
<br>▷ 市场总值：300 万美金（截至2014年年中）

#### Monero
Monero是CryptoNote的另一个实现。其货币曲线比Bytecoin稍显平缓，在系统运行的最开始四年发行 80% 的货币。它提供一些基于 CryptoNote 的匿名性特性。

▷ 出块速度：1分钟
<br>▷ 货币总量：1,840万XMR
<br>▷ 一致性算法：基于Cryptonight的工作量证明机制
<br>▷ 市场总值：500万美金（截至2014年年中）

#### Darkcoin

Darkcoin在2014年1月发布。Darkcoin通过一个名为DarkSend的混淆协议来实现匿名货币。值得一提的是，Darkcoin在工作量证明算法中使用了11轮不同的哈希函数（blake, bmw, groestl, jh, keccak, skein, luffa, cubehash, shavite, simd, echo）

▷ 出块速度：2.5分钟
<br>▷ 货币总量：最高2,200万DRK
<br>▷ 一致性算法：基于多轮哈希的工作量证明算法
<br>▷ 市场总值：1,900万美金（截至2014年年中）

    
## 9.4 非货币型竞争区块链

非货币型竞争币区块链是区块链设计模式的另类实现，并不主要作为货币使用。当然不少这种区块链的确含有货币，只不过它们的货币仅是一种象征，用于分配其他东西，比如一种资源或者一份合约。换句话说，货币并不是非货币型竞争币区块链的要点，仅仅是一种次要特征。

### 9.4.1 域名币
域名币是比特币源代码的首个克隆产物，它是一种使用区块链的去中心化平台，用来注册和转让键－值对。域名币支持全球的域－名注册，类似因特网上的域－名注册系统。目前域名币作为根域名.bit的替代性域名服务（DNS）使用。域名币也可以用来注册其他命名空间下的名称和键－值对，例如存储邮件地址、密钥、SSL证书、文件签名、投票系统和股票凭证之类，以及许多其他应用。

域名币系统也有它自己的货币（符号为NMC），用于支付域名注册及转让的交易费用。依照当前价格（2014年8月），注册一个域名的费用是0.01NMC，大约相当于1美分。与比特币类似，这些费用支付给域名币的矿工。

域名币的基本参数与比特币相同：

▷ 出块速度：10分钟
<br>▷ 货币总量：2140年将达2,100万NMC
<br>▷ 共识算法：SHA256工作量证明法
<br>▷ 市场总值：1,000万美元（截至2014年年中）

域名币的命名空间不受限制，任何人都可以以任意方式使用任意命名空间。不过，一些特定的命名空间因为有着一致认可的规范，因此当从区块链读取它们的时候，应用层的软件知道如何进行后续操作。无论使用何种软件，假如区块链遭到篡改，读取这个特定命名空间的软件都会报错。域名币一些流行的命名空间有：

▷ d/ 是 .bit 域名的域－名命名空间
<br>▷ id/ 是存储诸如邮件地址、PDP 密钥等个人身份验证的命名空间
<br>▷ u/ 是一个补充性的、更加结构化的存储身份的规范（基于公开规范）

域名币的客户端与比特币核心十分类似，因为前者的代码是从后者衍生而来的。在安装过程中，域名币客户端会下载其区块链的完整拷贝，下载完成之后便可进行查询和注册域名了。域名币客户端有3条可用命令：

`name_new`
查询并提前注册一个域名

`name_firstupdate`
公开注册一个域名

`name_update`
改变域名的信息或刷新域名

例如，注册mastering-bitcoin.bit这个域名，需使用按如下方法使用name_new指令：

```
$ namecoind name_new d/mastering-bitcoin
[
    "21cbab5b1241c6d1a6ad70a2416b3124eb883ac38e423e5ff591d1968eb6664a",
    "a05555e0fc56c023"
]
```

`name_new`通过给该域名创建一个哈希数和一个随机密钥来册一个对域名的声明。命令执行完毕后返回的两个字符串分别是哈希数和随机密钥（上例中的a05555e0fc56c023），二者可用于公开此次域名注册。一旦上述声明记录于域名币的区块链上，该声明便可转换为一个公开的注册。使用`name_firstupdate`命令便可达到此目的，当然，要提供随机密钥：

```
$ namecoind name_firstupdate d/mastering-bitcoin a05555e0fc56c023 "{"map": {"www": {"ip":"1.2.3.4"}}}}"
b7a2e59c0a26e5e2664948946ebeca1260985c2f616ba579e6bc7f35ec234b01
```

这个例子将会把域名 www.mastering-bitcoin.bit 映射到1.2.3.4这个IP地址上，返回的哈希数则是交易ID，能够用于追踪此次注册。你可以运行name_list命令来查看自己名下注册了哪些域名：

```
$ namecoind name_list
[
    {
        "name" : "d/mastering-bitcoin",
        "value" : "{map: {www: {ip:1.2.3.4}}}}",
        "address" : "NCccBXrRUahAGrisBA1BLPWQfSrups8Geh",
        "expires_in" : 35929
    }
]
```

每生成36,000个区块（大约200到250天），域名币上的注册就需要更新一次。不过name_update命令不收取费用，因此续约域名是免费的。也有第三方提供商提供一个网页界面来帮助处理注册、自动续约及更新等事宜，当然，这要花费你少许费用。使用第三方提供商的好处是你不需要运行一个域名币客户端了，坏处是你失去了对域名币提供去中心化的域名注册服务的自主控制。

### 9.4.2 Bitmessage

Bitmessage是一个实现了去中心化安全消息服务的比特币竞争币区块链，其本质上是一个无服务器的加密电子邮件系统。Bitmessage可以让用户通过一个Bitmessage地址来编写和发送消息。这些消息的运作方式与比特币交易大致相同，但区别在于消息是短暂瞬态的——如果超过两天还没被传送至目的节点，消息将会丢失。发送方和接收方都是假名，除了一个bitmessage地址外，他们没有其他的身份标识。但发送方和接收方有严格的身份验证，这意味着不会出现“欺骗”消息。Bitmessage都是经加密再发送给接收方，Bitmessage网络也因此可以抵御全面监视。除非网络偷听者破坏了接收方的设备，否则他们无法截取邮件消息。

### 9.4.3 以太坊

以太坊是一种图灵完备的平台，基于区块链账簿，用于合约的处理和执行。它不是比特币的一个克隆，而是完完全全独立的一种设计和实现。以太坊内置一种叫做ether的货币，该货币是付合约执行之费用所必须的。以太坊区块链记录的东西叫做合约，所谓合约，就是一种低级二进制码，也是一种图灵完备语言。本质上，合约其实是运行在以太坊系统中各个节点上的程序。这些程序可以存储数据、支付及收取、存储ether 以及执行无穷范围（因此才叫图灵完备）的计算行为，在系统中充当去中心化的自治软件代理。

以太坊能够实现一些颇为复杂的系统，这些系统甚至还能自我实现为其他的竞争币区块链。举例来说，下面就是一个类域名币的域名注册合约，使用以太坊代码编写（或者更准确地说，使用一种可编译为以太坊代码的高级代码编写）：

```
if !contract.storage[msg.data[0]]: # Is the key not yet taken? 
    # Then take it!
    contract.storage[msg.data[0]] = msg.data[1]
    return(1) 
else:

    return(0) // Otherwise do nothing
```

## 9.5 加密货币的未来

总体来看，加密货币的未来甚至比比特币还要光明。这是因为，比特币引入了这样一种全新的形式，那就是去中心化的组织和共识，而且这种形式已经催生了大量不可思议的创新。这些创新很有可能影响到社会中相当广泛的行业，从分布式系统科学到金融、经济、货币、中央银行以及企业管理，不一而足。在以前，很多人类活动都需要一个中心化的机构或组织来实现权威或可信控制点的功能，现在，这些都可以去中心化了。区块链和共识系统的发明，还会显著降低大型系统在组织及协调上的花销，同时也将消除权力攫取、腐败及管制俘获的可趁之机。

