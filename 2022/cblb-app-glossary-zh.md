# cblb.app 名词解释

## 永久流动性

> 更新日期@2022/2/22

CBLB 永久流动性由两部分组成

- Quickswap CBLB/MATIC
- Quickswap CBLB/WETH

开发者使用签到合约内积累的 MATIC 进行 Quickswap CBLB/MATIC 交易对和 CBLB/WETH 交易对流动池添加流动性并把对应 LP 代币转入签到合约永久锁定所形成的 CBLB 代币永久流动池

## 签到成本

> 更新日期@2022/2/22

CBLB 签到成本为每次签到需付出 MATIC 数量，其中包含

- 签到固定费用`0.113145539906103286`MATIC，用于开发者购买 CBLB，WETH 并添加永久流动性
- 签到合约交互费用，约`0.0054`MATIC

每次签到成本约`0.11854`MATIC

## 签到成本兑换比例

> 更新日期@2022/2/22

签到成本兑换比例为签到成本除以每次签到得到的 CBLB 数量

由于每次签到得到的 CBLB 数量和签到总人次有关，呈非线性递减，签到成本兑换比例为非线性增长趋势。

计算公式为

$ 签到成本兑换比例\, =\, \frac {签到成本} {签到得到 CBLB 数量} $

## 签到获得 CBLB 数量

> 更新日期@2022/1/20

每次签到获得 CBLB 数量被 Cblb 签到合约内托里拆利小号数学模型控制，满足公式

$ 签到获得 CBLB 数量\, =\, \frac {144600} {签到总人次\, +\, 100} $

例如，第 20000 次签到获得的 CBLB 数量为

$ 签到获得 CBLB 数量\, =\, \frac {144600} {20000\, +\, 100}=7.19402985\, CBLB $

可通过调用 Cblb 签到合约函数`getCblbIssueAmoun()`查看

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/2022/imgs/cblb-explain-getCblbIssueAmount.png)
