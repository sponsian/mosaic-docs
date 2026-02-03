# 概述

### **Mosaic是什么？**

Mosaic是一种基于Reef Chain的去中心化借贷协议，允许您用REEF作[抵押](borrowing.md#what-do-you-mean-by-collateral)提取[无息贷款](borrowing.md)。贷款以MEUR（一种与欧元挂钩的稳定币）的形式支付，并要求110%的[最低抵押率](borrowing.md#what-is-the-minimum-collateral-ratio-mcr-and-the-recommended-collateral-ratio)。

除了用户的抵押外，Mosaic的贷款还由一个MEUR的[稳定池](stability-pool-and-liquidations.md#what-is-the-stability-pool)和所有借款人集体作为最后担保人提供担保。您可以在我们关于[清算](stability-pool-and-liquidations.md#what-are-liquidations)的说明文件中了解有关这些机制的更多信息。

作为一个协议，Mosaic是非保管性的，不可改变的且无治理的。

### **Mosaic背后的动机是什么？**

具有稳定价值的资产是区块链应用的重要组成部分，并且已经发展成为一个价值数百亿美元的资产类别。

然而，绝大部分的这类资产是以法币作抵押的稳定币形式出现的，如Tether和USDC。去中心化稳定币仅占稳定币总供应量的一小部分，这意味着绝大多数稳定币都是中心化的。此外，大多数稳定币与美元挂钩，使欧洲用户面临汇率波动的风险。

通过在Reef Chain上创建一种更具资本效率、更容易使用的借入欧元挂钩稳定币的方式，Mosaic解决了这个问题。此外，Mosaic是无治理的，可确保协议保持去中心化。

### **Mosaic的强项是什么？**

Mosaic的主要优势包括：

* [利率为0％](borrowing.md#how-can-the-protocol-offer-interest-free-borrowing)——作为借款人，您无需担心不断产生新的债务。
* 110％的[最低抵押率](borrowing.md#what-is-the-minimum-collateral-ratio-mcr-and-the-recommended-collateral-ratio)——更有效地利用储蓄的REEF。
* 无治理——所有操作都是算法化的和自动化的，并且在协议部署时就已经设置好了协议参数。
* [可直接赎回](meur-redemptions.md#what-are-redemptions)——MEUR可以随时按面值赎回相关抵押品。
* 完全去中心化——Mosaic协议没有管理密钥，从而使其不受审查。

### **Mosaic是否可以升级或更改？**

不可以。Mosaic没有管理员密钥。没有人可以以任何方式更改系统规则。智能合约的代码是完全不变的。

### **如何使用Mosaic？**

您可以通过官方前端 [mosaic.markets](https://mosaic.markets) 访问Mosaic。

### Mosaic的主要应用案例有哪些？

1. 通过打开[金库](borrowing.md#what-is-a-trove)，用REEF作抵押借入MEUR
2. 通过向[稳定池](stability-pool-and-liquidations.md#what-is-the-stability-pool)提供MEUR来换取奖励，以确保Mosaic的安全性
3. 质押MSIC以赚取其他用户借入或赎回MEUR所支付的费用收入
4. 当MEUR价格低于€1时，用1 MEUR兑换价值€1的REEF

### MEUR和MSIC是什么？

MEUR是与欧元挂钩的稳定币，可以用于偿还Mosaic协议里的贷款。您在任何时候都可以按面值赎回[抵押品](borrowing.md#what-do-you-mean-by-collateral)。在[此处](meur-redemptions.md)了解有关稳定机制的更多信息。

MSIC是Mosaic发行的辅助令牌。它捕获了系统产生的费用收入，并激励早期用户。MSIC的总供应量上限为100,000,000个代币。有关更多信息，请参阅[MSIC奖励和分配](msic-distribution-and-rewards.md)。

### 使用Mosaic有什么条件？

要借入MEUR，您所需要的只是一个钱包（如Klever）和足够的REEF以开设[金库](borrowing.md#what-is-a-trove)并支付交易费。

要想在稳定池中存款或者质押MSIC，您需要拥有MEUR和/或MSIC代币。您可以通过开设金库借入MEUR，而MSIC可以通过在稳定池中存款来赚取。您还可以使用ReefSwap或其他去中心化交易所在公开市场上购买代币。

### Mosaic是否收取任何费用？

每当借入MEUR以及赎回MEUR时，都必须支付一笔一次性的费用：

* 对于借款人，贷款的借款费占实际借款的一定比例（以MEUR为单位）。
* 对于赎回者，将MEUR兑换为REEF时，系统会收取赎回费（以REEF为单位）。请注意，赎回与偿还您作为借款人的贷款是分开的，后者是免费的。

两种费用都取决于赎回的数量。它们随每次赎回而增加，但如果没有新的赎回发生就随时间推移而递减。这样做的目的是用较高的费用限制大量的赎回，并在大量赎回后直接限制借入。随着时间的流逝，费用的减少使得在赎回量很低的时候对借款人和赎回者的收费"降温"。费用不得低于0.5％（在[恢复模式](recovery-mode.md#what-are-the-fees-during-recovery-mode)下除外），这可以保护赎回工具免于被套利交易者抢先使用。借款费用的上限为5％，即使在大量赎回导致货币收缩时，该系统也对借款人保持吸引力。

### 如何使用Mosaic赚钱？

使用Mosaic有两种不同的创收方式：

* 将MEUR存入[稳定池](stability-pool-and-liquidations.md#what-is-the-stability-pool)，并获得清算收益（以REEF为单位）和MSIC奖励。
* [质押](staking.md)MSIC，并从借入和赎回费中赚取MEUR和REEF收入。

### 我会亏本吗？

作为非保管性的系统，发送给协议的所有令牌都将通过算法进行保存和管理，不会受到任何人或机构的干扰。这意味着您的资金将仅受智能合约代码中规定的规则约束。

在以下两种情况下，您可能会损失一部分资金：

* 您是借款人（金库所有者），您的REEF抵押品已被[清算](stability-pool-and-liquidations.md#what-are-liquidations)。您将保留您借入的MEUR，但您的金库已经被关闭，而您的抵押品将用于补偿[稳定池](stability-pool-and-liquidations.md#what-is-the-stability-pool)的存款者。
* 您是稳定池的存款人，您所存的MEUR用于偿还被清算的借款人的债务。通常只要借款人的抵押率跌到110％以下就会触发清算，所以您很有可能获得更多REEF的回报。但是，如果REEF价格持续下跌并且您维持仓位，您可能会损失一部分稳定池存款的价值。

请注意，MEUR并非完美地与欧元挂钩，在某些市场条件下可能会略有偏差。

尽管我们对系统进行了非常认真的设计，但我们无法完全排除黑客或系统漏洞导致的用户损失。
