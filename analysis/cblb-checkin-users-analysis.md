# Cblb 签到玩法和使用者分析

<!-- MarkdownTOC -->

- [1. 综述](#1-综述)
- [2. 基本数据](#2-基本数据)
- [3. 签到玩法内角色设计](#3-签到玩法内角色设计)
- [4. 签到玩法机制简介](#4-签到玩法机制简介)
- [5. 上线签到玩法后的角色增加](#5-上线签到玩法后的角色增加)
  - [5.1 机器人套利者行为分析](#51-机器人套利者行为分析)
  - [5.2 参与者行为分析](#52-参与者行为分析)
- [6. 签到玩法冷启动之后的角色分析](#6-签到玩法冷启动之后的角色分析)
  - [6.1 除合约外的四个角色对于 CBLB Web3 经济系统的贡献和约束](#61-除合约外的四个角色对于cblb-web3经济系统的贡献和约束)
  - [6.2 来自开发者风险的分析](#62-来自开发者风险的分析)
- [7. 永久流动性 CBLB/MATIC 分析](#7-永久流动性cblbmatic分析)
- [8. 通过 CBLB 相关兑换比例参数给出参与建议](#8-通过cblb相关兑换比例参数给出参与建议)
- [9. 总结](#9-总结)

<!-- /MarkdownTOC -->

<a id="1-综述"></a>

## 1. 综述

[cblb.app](https://cblb.app/supervise/cblb-token-info)是一个 Polygon 上的 dApp，在部署**Cblb 签到合约**和**CBLB 代币合约**之后。截止 2022 年 1 月 29 日，签到共计[1266 人次](https://polygonscan.com/tx/0x15721e4e874ccc9d867851e36917db3d5302e418000e8d9fd65e04e6d187f076)，在没有任何宣发情况下取得这样的数据突显了 Web3 的魅力。

也从侧面证明了 Web3 的活跃，尤其是具有开发能力的使用者占有不小比例。

<a id="2-基本数据"></a>

## 2. 基本数据

- **CBLB 代币合约**部署于 2022 年 1 月 9 日，[Transaction hash](https://polygonscan.com/tx/0xbec5289b7dd1dbb71a8550cd9ccbff6f782ace6490907468c29ad3a01f980632)
- **Cblb 签到合约**部署于 2022 年 1 月 20 日，[Transaction hash](https://polygonscan.com/tx/0xdda6622ac2cea5cc3e7ac5e21526487c35e51724660949364595f4f0797cf794)

上述两个智能合约代码已于 Polygonscan 验证，并且开源了开发工程

- [CBLB 代币合约 Polygonscan](https://polygonscan.com/address/0x7a45922F95C845Ff9bE01112AfCF207968a9cA0B#code)
- [Cblb 签到合约 Polygonscan](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88#code)
- [开源工程 Github 仓库](https://github.com/cblb-app/cblb-token-checkin-contracts)

<a id="3-签到玩法内角色设计"></a>

## 3. 签到玩法内角色设计

签到玩法包含四个元素

- [CBLB 签到合约](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)
- [CBLB 代币合约](https://polygonscan.com/token/0x7a45922F95C845Ff9bE01112AfCF207968a9cA0B)
- [开发者](https://polygonscan.com/address/0xe75Dc9d66eae386e76370bfcB4BbD5AdC7BeE6db)
- [维护者](https://polygonscan.com/address/0xf9e4b03a592152cbF2362222d7465f25ba627f9C)

<a id="4-签到玩法机制简介"></a>

## 4. 签到玩法机制简介

具体信息见[CBLB 签到玩法介绍](https://cblb.app/supervise/cblb-check-in)

- **CBLB 代币**是发行在 Polygon 上的 ERC20 标准的 Mintable 代币，初始发行量 0，无上限
- **CBLB 代币**的`owner()`是**Cblb 签到合约**
- **CBLB 代币**的发行只能通过调用**Cblb 签到合约**的`checkin()`方法，对应 UI 界面为[cblb.app 序章](https://cblb.app/prologue)，每次 Mint 数量被**Cblb 签到合约**中的[托里拆利小号数学模型](https://cblb.app/supervise/cblb-token-model)计算得出，每次 CBLB `mint()`数量只与**签到总人次**有关。**签到总人次**越多，每次被**Cblb 签到合约**Mint 出的 CBLB 代币越少
- 每次签到，用户需要固定支付约`0.113146` MATIC，用来抬升 CBLB 代币的保底价格，同一用户钱包地址 24 小时只能签到一次
- **开发者**可以通过调用**Cblb 签到合约**函数`devWithdrawAcquiredFee()`领取 Cblb 签到智能合约内积累的 MATIC
- 任何用户可以调用**Cblb 签到合约**函数`sendAcquireFeeToDev()`发送**Cblb 签到合约**内积累的 MATIC 到**开发者**钱包
- **开发者**需要在领取签到合约内汇集的 MATIC，执行买入 CBLB，添加[Quickswap CBLB/MATIC 流动性](https://info.quickswap.exchange/#/pair/0xe99d5f930048ae3006205c87d2ddafa397014012)，锁定[CBLB/MATIC LP 代币](https://polygonscan.com/token/0xe99d5f930048ae3006205c87d2ddafa397014012)到**Cblb 签到合约**中
- **开发者**在初始阶段提供一些 MATIC，用于启动签到玩法，购买 CBLB 代币，添加[Quickswap CBLB/MATIC 流动性](https://info.quickswap.exchange/#/pair/0xe99d5f930048ae3006205c87d2ddafa397014012)，锁定[CBLB/MATIC LP 代币](https://polygonscan.com/token/0xe99d5f930048ae3006205c87d2ddafa397014012)到**Cblb 签到合约**中，构成系统的**永久流动性**
- **维护者**在初始阶段提供一些 MATIC，用于买入 CBLB，建立可获得收益的流动性（当前为[Uniswap v3 CBLB/USDC](https://app.uniswap.org/#/pool/27318?chain=polygon)），执行购买、卖出 CBLB 代币，提升 CBLB 活跃度，通过交易量流动性池分红，卖出 CBLB 获利

<a id="5-上线签到玩法后的角色增加"></a>

## 5. 上线签到玩法后的角色增加

完成**CBLB 代币合约**部署，**Cblb 签到合约**部署，**开发者**提供初始流动性，**维护者**建立流动性池，整个系统内迅速出现了来自 web3 的新角色，分别为

- **机器人套利者**
- **参与者**

<a id="51-机器人套利者行为分析"></a>

### 5.1 机器人套利者行为分析

**机器人套利者**之所以出现，是因为**开发者**初始提供**CBLB/MATIC 流动池**的兑换比例和**签到成本**之间存在套利空间，十分惊喜的是，CBLB 签到玩法是在完全没有宣发的情况下上线的，可以得出简单结论：

- **在 Polygon 区块链的 defi 板块，机器人套利机会的发现和执行已非常完善**

这得益于 Polygon 交互费用低廉，区块链确认速度块等优点。

对于 Cblb 签到合约，机器人套利者的 CBLB 获取成本为

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/analysis/imgs/cblb-price-base.png)

实际运行中，机器人套利者采用的模式是数十个钱包地址进行签到，汇集到一个地址完成 swap，那么签到成本为

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/analysis/imgs/cblb-price-average.png)

对于 Cblb 签到玩法，每次签到获得的 CBLB 代币数量随着签到次数递减，可以得出结论：

- **机器人套利者会在 Quickswap 流动池价格相对于签到成本过高时候介入，完成 CBLB 价格的压制动作**  
  <a id="52-参与者行为分析"></a>

### 5.2 参与者行为分析

参与者为直接参与签到或囤积 CBLB 代币的用户

<a id="6-签到玩法冷启动之后的角色分析"></a>

## 6. 签到玩法冷启动之后的角色分析

综上，签到玩法的系统中拥有六种角色，分别是：

- [CBLB 签到智能合约](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)
- [CBLB 代币合约](https://polygonscan.com/token/0x7a45922F95C845Ff9bE01112AfCF207968a9cA0B)
- [开发者](https://polygonscan.com/address/0xe75Dc9d66eae386e76370bfcB4BbD5AdC7BeE6db)
- [维护者](https://polygonscan.com/address/0xf9e4b03a592152cbF2362222d7465f25ba627f9C)
- 机器人套利者
- 参与者

从系统中不同角色对于 CBLB 价格的贡献作用可得出分析

- **Cblb 签到合约**：完成 CBLB 代币价格的筑底，产生**CBLB 签到成本价格**
- **开发者**：完成 CBLB 代币的价格驻底，CBLB 发行量和 Cblb 签到合约汇集 MATIC 之间的兑换关系，称为**CBLB 期望兑换比例**
- **机器人套利者**：完成 CBLB 价格压制，可以保证 CBLB 在任何发行量、价格情况下的价格非健康上涨，避免造成大额投资者、普通参与者巨额亏损的可能

<a id="61-除合约外的四个角色对于cblb-web3经济系统的贡献和约束"></a>

### 6.1 除合约外的四个角色对于 CBLB Web3 经济系统的贡献和约束

到这里我们拥有了一个小型的**元宇宙经济系统**，我们更愿意称之为小型**Web3 经济系统**。

这个有上限约束和筑底约束的小型 Web3 经济系统是一个 dApp 承载其它所有后续功能的基础，以及价值均衡的空间

- 参与者：签到推高 CBLB 代币筑底价格（贡献），卖出 CBLB 获利（约束）
- 开发者：签到推高 CBLB 代币筑底价格，提供永久流动性（贡献）
- 维护者：签到推高 CBLB 代币筑底价格，通过自建流动性套利，卖出 CBLB 获利（约束）
- 机器人套利者：签到推高 CBLB 代币筑底价格（贡献），利用**CBLB 签到成本兑换比例**和**当前 CBLB 兑换比例**差额套利（约束）

<a id="62-来自开发者风险的分析"></a>

### 6.2 来自开发者风险的分析

综上介绍和分析，最直观的风险点来自于开发者是否持续执行**永久流动性**的添加。

从去中心化角度来看，**开发者**的行为模式风险同样也是 cblb.app 本身的风险。这个风险点对于 cblb.app 来说不可消除，但去中心化 App 的优势是所有行为链上可查，方便用户查看和监督。

所以从一个系统的稳定程度来看，即使开发者钱包地址没有执行后续永久流动性添加，也仅限于[当前永久流动性](https://polygonscan.com/token/0xe99d5f930048ae3006205c87d2ddafa397014012?a=0x15942e96beca7fa6081740dfb74d7702ec2c3b88)之外的价值，并且一旦没有遵守行为约束，所有活动均为链上可查信息。只要开发者钱包地址出现行为约束里没有提到的内容，那么 cblb.app 本身的信用也会随之消失。

从这个角度来看，cblb.app 的风险监控处于实时状态，链上数据完全公开，符合 dApp 开放、开源的思路。

<a id="7-永久流动性cblbmatic分析"></a>

## 7. 永久流动性 CBLB/MATIC 分析

上面的分析，建立在两个假设至上

- MATIC 价格不变
- 始终有用户进行签到动作

引入这两个变量之后，再次纵观可得出这两个变量的引入对于 CBLB Web3 经济系统的作用更多的是贡献。

从流动性角度，**永久流动池**为 CBLB/MATIC，**维护者**建立的流动池为 CBLB/USDC。那么随着 MATIC 价格波动，这两个池子会产生天然的套利空间，那么**机器人套利者**的存在会抹平两个池子之间的差价，从而带来 CBLB Web3 经济系统的持续波动动力。

这个波动动力的产生，给**维护者**和**参与者**提供了套利空间，满足 CBLB Web3 经济系统稳定发展的需要。与此同时 Quickswap 上的**永久流动池**会不断积累[交易量价值的 0.3%](https://quickswap-layer2.medium.com/welcome-to-quickswap-exchange-93d47e057633)到自身，完成 CBLB Web3 经济系统价值的不断增长

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/analysis/imgs/quickswap-fee.png)

从签到的角度，如果没有用户签到，那么系统同样可以获得来自 MATIC 价格波动的动力，签到行为仅作用于 CBLB Web3 经济系统的增速快慢。

<a id="8-通过cblb相关兑换比例参数给出参与建议"></a>

## 8. 通过 CBLB 相关兑换比例参数给出参与建议

上面提到的三个 CBLB 价格点分别为

- CBLB 签到成本兑换比例
- CBLB 期望兑换比例
- Quickswap 永久流动性当前 CBLB 兑换比例

数据点已展示在[cblb.app](https://cblb.app/supervise/cblb-token-info)，由于 CBLB 发行数量和签到次数唯一相关，当第 1266 次签到时

- CBLB 发行总量为：`378723.9` CBLB
- **Cblb 签到合约**内积累的 MATIC 数量：`143.2` MATIC
- 可计算得出**CBLB 期望兑换比例**：`143.2 / 378723.9 = 0.000378` CBLB/MATIC
- 当前签到领取 CBLB 数量为：`105.9` CBLB
- 当前签到须付出 MATIC：`0.113147` MATIC
- 拟合**CBLB 签到成本兑换比例**：`0.113147 / 105.9 = 0.001068` CBLB/MATIC
- Quickswap 永久流动性**当前 CBLB 兑换比例**：`0.002771` CBLB/MATIC

这时候**机器人套利者**没有继续压制 CBLB 价格，可视为短暂稳定，可得到价格关系

```
CBLB期望兑换比例 < CBLB签到成本兑换比例 < 当前CBLB兑换比例
```

综上可得出参与建议

- 对于**机器人套利者**：应当关注**CBLB 签到成本兑换比例**和**当前 CBLB 兑换比例**差值，如果差值扩大，可以进行套利
- 对于**参与者**：计划进行**买入**，则需要控制买入量，因为买入量过大会造成**当前 CBLB 兑换比例**远高于**CBLB 签到成本兑换比例**，从而给**机器人套利者**制造套利空间，造成短期亏损
- 对于**参与者**：计划进行签到，无需关注该比例

<a id="9-总结"></a>

## 9. 总结

经过冷启动建立相对稳定的 CBLB Web3 经济系统后，下一步进入 cblb.app 的功能叠加阶段

综上仅作参考，DYOR
