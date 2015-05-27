# 附录２ 比特币改进协议

比特币改进协议（Bitcoin improvement proposals 简称BIP）是为比特币社区提供规范，完善比特币及其运行进程和外部环境特性的设计指导文件。
依据 BIP0001协议即比特币改进协议的目的与指南，比特币改进协议有以下三种类型：

**标准协议（Standard BIP）**
<br>描述任何影响大多或全部比特币应用的变化，比如网络协议、交易有效性规则的变化，或者任何影响使用比特币交互操作性的变化或补充。

**信息补充协议（Informational BIP）**
<br>描述比特币的设计事项而不是为其提供新特性，或者为比特币社区提供一般性的指南或信息。信息补充型协议 不一定需要比特币社区达成共识或推荐，因此用户和开发人员可以选择忽略或者接受信息补充型协议的建议。

**开发指导协议（Process BIP）**
<br>描述比特币进程，或者提议更改进程或事项。Process BIP与Standard BIP 相似，但是也可以应用于除比特币协议以外的领域。在普遍达成共识的情况下，它可以向比特币以外的代码库提出改进建议。与Informational BIP不同，Process BIP 是强制性的，用户必须遵守。例如针对决策进程的过程、指南、改变，在比特币开发过程中使用的工具、环境的改变。任何meta-BIP也应被认为是Process BIP。
比特币改进协议在 GitHub 中更新版本。

表B-1为比特币改进协议一览表（更新至2014年底） 。需要有关目前 BIP 内容的最新信息，请参考官方版本。

**表B-1 BIP一览表**

| BIP# | 链接 | 标题 | 作者 | 类型 | 状态 |
| -- | -- | -- | -- | -- | -- |
| 1 | [https://github.com/bitcoin/bips/blob/ master/bip-0001.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0001.mediawiki ) | BIP Purpose and Guidelines | Amir Taaki | Standard | Active |
| 10 | [https://github.com/bitcoin/bips/blob/ master/bip-0010.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0010.mediawiki) | Multi-Sig Transaction Distribution | Alan Reiner | Informational | Draft |
| 11 | [https://github.com/bitcoin/bips/blob/ master/bip-0011.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0011.mediawiki) | M-of-N Standard Transactions | Gavin Andresen | Standard | Accepted |
| 12 |[https://github.com/bitcoin/bips/blob/ master/bip-0012.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0012.mediawiki)| OP_EVAL | Gavin Andresen | Standard | Withdrawn |
| 13 | [https://github.com/bitcoin/bips/blob/ master/bip-0013.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0013.mediawiki)| Address Format for pay-to- script-hash |Gavin Andresen | Standard | Final |
| 14 | [https://github.com/bitcoin/bips/blob/ master/bip-0014.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0014.mediawiki) |Protocol Version and User Agent | Amir Taaki, Patrick | Standard |Accepted |
| 15 | [https://github.com/bitcoin/bips/blob/ master/bip-0015.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0015.mediawiki) | Aliases |Amir Taaki | Standard | Withdrawn |
| 16 |[https://github.com/bitcoin/bips/blob/ master/bip-0016.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0016.mediawiki) |Pay To Script Hash |Gavin Andresen | Standard | Accepted |
| 17 | [https://github.com/bitcoin/bips/blob/ master/bip-0017.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0017.mediawiki) | OP_CHECKHASHVERIFY (CHV) | Luke Dashjr | Withdrawn | Draft |
| 18 | [https://github.com/bitcoin/bips/blob/ master/bip-0018.mediawikilink:](https://github.com/bitcoin/bips/blob/ master/bip-0018.mediawikilink:) | hashScriptCheck | Luke Dashjr | Standard | Draft |
| 19 |  [https://github.com/bitcoin/bips/blob/ master/bip-0019.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0019.mediawiki)| M-of-N Standard Transactions (Low SigOp) | Luke Dashjr | Standard | Draft |
| 20 | [https://github.com/bitcoin/bips/blob/ master/bip-0020.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0020.mediawiki) | URI Scheme |Luke Dashjr | Standard | Replaced |
| 21 | [https://github.com/bitcoin/bips/blob/ master/bip-0021.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0021.mediawiki) | URI Scheme | Nils Schneider, Matt Corallo | Standard | Accepted |
| 22 | [https://github.com/bitcoin/bips/blob/ master/bip-0022.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0022.mediawiki) | getblocktemplate - Fundamentals | Luke Dashjr | Standard |Accepted|
| 23|  [https://github.com/bitcoin/bips/blob/ master/bip-0023.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0023.mediawiki) | getblocktemplate - Pooled Mining | Luke Dashjr | Standard | Accepted |
| 30|  [https://github.com/bitcoin/bips/blob/ master/bip-0030.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0030.mediawiki) | Duplicate transactions| Pieter Wuille | Standard | Accepted |
| 31|  [https://github.com/bitcoin/bips/blob/ master/bip-0031.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0031.mediawiki) | Pong message | Mike Hearn | Standard | Accepted |
| 32 |  [https://github.com/bitcoin/bips/blob/ master/bip-0032.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0032.mediawiki) | Hierarchical Deterministic Wallets |Pieter Wuille | Informational | Accepted |
| 33 | [https://github.com/bitcoin/bips/blob/ master/bip-0033.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0033.mediawiki) | Stratized Nodes | Amir Taaki | Standard | Draft |
| 34 | [https://github.com/bitcoin/bips/blob/ master/bip-0034.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0034.mediawiki) | Block v2, Height in coinbase |Gavin Andresen | Standard | Accepted |
| 35 |  [https://github.com/bitcoin/bips/blob/ master/bip-0035.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0035.mediawiki) | mempool message| Jeff Garzik | Standard | Accepted |
| 36 | [https://github.com/bitcoin/bips/blob/ master/bip-0036.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0036.mediawiki)  | Custom Services |Stefan Thomas |Standard | Draft|
| 37 |  [https://github.com/bitcoin/bips/blob/ master/bip-0037.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0037.mediawiki) | Bloom filtering | Mike Hearn and Matt Corallo | Standard | Accepted |
| 38 |  [https://github.com/bitcoin/bips/blob/ master/bip-0038.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0038.mediawiki) | Passphrase-protected private key | Mike Caldwell| Standard |Draft |
| 39 | [https://github.com/bitcoin/bips/blob/ master/bip-0039.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0039.mediawiki)| Mnemonic code for generating deterministic keys |Slush | Standard |Draft|
| 40 | -  | Stratum wire protocol | Slush | Standard |BIP number allocated |
| 41| - | Stratum mining protocol |Slush| Standard | BIP number allocated |
| 42 |  [https://github.com/bitcoin/bips/blob/ master/bip-0042.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0042.mediawiki)|A finite monetary supply for bitcoin | Pieter Wuille | Standard | Draft |
| 43 |  [https://github.com/bitcoin/bips/blob/ master/bip-0043.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0043.mediawiki) | Purpose Field for Deterministic Wallets | Slush | Standard |Draft |
| 44 |  [https://github.com/bitcoin/bips/blob/ master/bip-0044.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0044.mediawiki) | Multi-Account Hierarchy for Deterministic Wallets | Slush | Standard| Draft |
| 50 | [https://github.com/bitcoin/bips/blob/ master/bip-0050.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0050.mediawiki)| March 2013 Chain Fork Post- Mortem |Gavin Andresen | Informational |Draft |
| 60 |  [https://github.com/bitcoin/bips/blob/ master/bip-0060.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0060.mediawiki) | Fixed Length “version” Message (Relay-Transactions Field) | Amir Taaki | Standard | Draft |
| 61 |  [https://github.com/bitcoin/bips/blob/ master/bip-0061.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0061.mediawiki) | “reject” P2P message | Gavin Andresen | Standard | Draft |
| 62 |  [https://github.com/bitcoin/bips/blob/ master/bip-0062.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0062.mediawiki) | Dealing with malleability | Pieter Wuille | Standard | Draft |
| 63 |  - | Stealth Addresses | Peter Todd | Standard | BIP number allocated |
| 64 |  [https://github.com/bitcoin/bips/blob/master/bip-0064.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0064.mediawiki) |getutxos message | Mike Hearn| Standard |  Draft |
| 70 |  [https://github.com/bitcoin/bips/blob/ master/bip-0070.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0070.mediawiki) | Payment protocol | Gavin Andresen | Standard |  Draft |
| 71 |  [https://github.com/bitcoin/bips/blob/ master/bip-0071.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0071.mediawiki) | Payment protocol MIME types| Gavin Andresen | Standard| Draft |
| 72 | [https://github.com/bitcoin/bips/blob/ master/bip-0072.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0072.mediawiki) | Payment protocol URIs | Gavin Andresen| Standard |  Draft |
| 73 |  [https://github.com/bitcoin/bips/blob/ master/bip-0073.mediawiki](https://github.com/bitcoin/bips/blob/ master/bip-0073.mediawiki) | Use “Accept” header with Payment Request URLs | Stephen Pair | Standard |  Draft |



