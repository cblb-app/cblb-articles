# Cblb.app 名词解释

<!-- MarkdownTOC -->

- [永久流动性](#永久流动性)
- [签到成本](#签到成本)
- [签到获得 CBLB 数量](#签到获得-cblb-数量)
- [签到成本兑换比例](#签到成本兑换比例)
- [闪崩兑换比例](#闪崩兑换比例)
- [期望兑换比例](#期望兑换比例)
- [开发者](#开发者)

<!-- /MarkdownTOC -->

<a id="永久流动性"></a>

## 永久流动性

> 更新日期@2022/3/3

CBLB 永久流动性由两部分组成

- [Quickswap CBLB/MATIC](https://info.quickswap.exchange/#/pair/0xe99d5f930048ae3006205c87d2ddafa397014012)
- [Quickswap CBLB/WETH](https://info.quickswap.exchange/#/pair/0x8b6734217e1c5914cb729780fa9557629ff5b427)
- [Quickswap CBLB/USDC](https://info.quickswap.exchange/#/pair/0x7d760ba1df7ec334a2942b5e057b82fa0a5cab5d)

开发者使用签到合约内积累的 MATIC 进行 Quickswap CBLB/MATIC 交易对、Quickswap CBLB/WETH 交易对和 CBLB/USDC 交易对流动池添加流动性并把对应 LP 代币转入签到合约永久锁定所形成的 CBLB 代币永久流动池

<a id="签到成本"></a>

## 签到成本

> 更新日期@2022/2/22

CBLB 签到成本为每次签到需付出 MATIC 数量，其中包含

- 签到固定费用`0.113145539906103286`MATIC，用于开发者购买 CBLB，WETH 并添加永久流动性
- 签到合约交互 gas 费用，约`0.0054`MATIC

每次签到成本约`0.11854`MATIC

签到固定费用可通过调用 Cblb 签到合约函数`getCheckinFee`查看

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/2022/imgs/cblb-glossary-getCheckinFee.png)

<a id="签到获得-cblb-数量"></a>

## 签到获得 CBLB 数量

> 更新日期@2022/1/20

每次签到获得 CBLB 数量被 Cblb 签到合约内托里拆利小号数学模型控制，满足公式

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/2022/imgs/check-in-to-get-cblb-amount-zh.png)

例如，第 20000 次签到获得的 CBLB 数量为

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/2022/imgs/check-in-to-get-cblb-amount-res-zh.png)

可通过调用 Cblb 签到合约函数`getCblbIssueAmount()`查看

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/2022/imgs/cblb-glossary-getCblbIssueAmount.png)

<a id="签到成本兑换比例"></a>

## 签到成本兑换比例

> 更新日期@2022/2/22

签到成本兑换比例为签到成本除以每次签到得到的 CBLB 数量

由于每次签到得到的 CBLB 数量和签到总人次有关，呈非线性递减，签到成本兑换比例为非线性增长趋势。

计算公式为

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/2022/imgs/check-in-cost-ratio-zh.png)

<a id="闪崩兑换比例"></a>

## 闪崩兑换比例

> 更新日期@2022/3/3

闪崩兑换比例为市场上所有可卖出的 CBLB 瞬时全部卖出后的 CBLB/MATIC 兑换比例，由于 CBLB 包含符合 AMM 自动做市的永久流动性池，`constant = CBLB数量 * MATIC数量`，计算公式为

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/2022/imgs/rug_pull_ratio_zh.png)

<a id="期望兑换比例"></a>

## 期望兑换比例

> 更新日期@2022/3/3

期望兑换比例为 Cblb 签到合约内部由用户签到积累的 MATIC 总数除以 CBLB 总发行量，期望兑换比例可认为是 CBLB 代币从发行到当下兑换 MATIC 比例的平均值，是不可能达到的最低兑换比例。不可能达到该比例由于由永久流动池的存在。期望兑换比例随着签到人次增加，不断增长。

<a id="开发者"></a>

## 开发者

> 更新日期@2022/1/20

开发者完成 cblb.app 所有合约部署，获取用户签到积累的 MATIC 进行永久流动性 CBLB/MATIC 和 CBLB/WETH 添加

钱包地址：`0xe75Dc9d66eae386e76370bfcB4BbD5AdC7BeE6db`
