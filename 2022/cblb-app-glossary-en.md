# Cblb.app Glossary

<!-- MarkdownTOC -->

- [Permanent liquidity](#permanent-liquidity)
- [Check-in cost](#check-in-cost)
- [Check-in to get CBLB amount](#check-in-to-get-cblb-amount)
- [Check-in cost ratio](#check-in-cost-ratio)
- [Developer](#developer)

<!-- /MarkdownTOC -->

<a id="permanent-liquidity"></a>

## Permanent liquidity

> Update date@2022/3/3

CBLB permanent liquidity consists of two parts

- [Quickswap CBLB/MATIC](https://info.quickswap.exchange/#/pair/0xe99d5f930048ae3006205c87d2ddafa397014012)
- [Quickswap CBLB/WETH](https://info.quickswap.exchange/#/pair/0x8b6734217e1c5914cb729780fa9557629ff5b427)
- [Quickswap CBLB/USDC](https://info.quickswap.exchange/#/pair/0x7d760ba1df7ec334a2942b5e057b82fa0a5cab5d)

Developers use the MATIC accumulated in the check-in contract to conduct Quickswap CBLB/MATIC trading pairs, CBLB/WETH trading pairs and CBLB/USDC trading pairs to add liquidity to the liquidity pool and transfer the corresponding LP tokens to the CBLB token permanent liquidity pool formed by the permanent lock-in contract

<a id="check-in-cost"></a>

## Check-in cost

> Update date@2022/2/22

CBLB check-in cost is the MATIC amount for each check-in, including

- Check-in fixed fee `0.113145539906103286`MATIC for developers to buy CBLB, WETH and add permanent liquidity
- Check-in contract interaction gas cost, about `0.0054`MATIC

The cost of each check-in is about `0.11854`MATIC

The check-in fixed fee can be viewed by calling the Cblb check-in contract function `getCheckinFee`

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/2022/imgs/cblb-glossary-getCheckinFee.png)

<a id="check-in-to-get-cblb-amount"></a>

## Check-in to get CBLB amount

> Update date@2022/1/20

The amount of CBLB obtained for each check-in is controlled by the mathematical model of Torricelli trumpet in the Cblb Check-in contract, which satisfies the formula

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/2022/imgs/check-in-to-get-cblb-amount-en.png)

For example, the amount of CBLB earned for the 20000th check-in is

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/2022/imgs/check-in-to-get-cblb-amount-res-en.png)

It can be viewed by calling the Cblb sign-in contract function `getCblbIssueAmount()`

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/2022/imgs/cblb-glossary-getCblbIssueAmount.png)

<a id="check-in-cost-ratio"></a>

## Check-in cost ratio

> Update date@2022/2/22

The check-in cost ratio is the check-in cost divided by the number of CBLBs obtained per check-in

Since the number of CBLBs obtained for each check-in is related to the total number of check-ins, which is non-linearly decreasing, the conversion ratio of check-in cost is a non-linear growth trend.

The calculation formula is

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/2022/imgs/check-in-cost-ratio-en.png)

<a id="developer"></a>

## Developer

The developer completes the deployment of all contracts in cblb.app, and obtains the MATIC accumulated by user sign-in for permanent liquidity CBLB/MATIC and CBLB/WETH addition

Wallet address: `0xe75Dc9d66eae386e76370bfcB4BbD5AdC7BeE6db`
