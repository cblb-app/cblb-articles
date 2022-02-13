# Cblb.app check-in gameplay, character refinement and room for improvement

After more than 20 days of operation, the CBLB economic system has entered a relatively stable state, which includes relatively stable liquidity and relatively stable number of check-ins.

All data in this article are as of Polygon block [24895721](https://polygonscan.com/tx/0xde82e0cc153d8e436f4139f30e86fc3b7613ff5e7adc22aaeb11a3a0947bd476), corresponding to `2641` Cblb check-in times.

## Robot arbitrageur role refinement

Through the article "Cblb Check-in Gameplay and User Analysis", the fifth section "Character Increase after Online Check-in Gameplay", the role of robot arbitrageur appeared at the beginning of the CBLB economic system.

By analyzing the 2641 check-in data, we can refine the **robot arbitrageur** into two roles

- Check-in bot users
- CBLB/MATIC liquidity pool and CBLB/USDC liquidity pool arbitrageurs

The robot arbitrageur at the beginning of the CBLB economic system is a combination of these two roles. It not only uses the check-in robot for check-in, but also performs arbitrage by monitoring the Quickswap permanent liquidity pool and the CBLB price in the CBLB/USDC liquidity pool.

## Why did the user of the check-in robot not continue to check in?

First of all, we analyze the motivation of the check-in robot users to continue to check in. The analysis has been done in "Cblb Check-in Gameplay and User Analysis". There are two key CBLB price indicators to determine whether the robot arbitrageur performs arbitrage actions.

- Check-in cost conversion ratio
- Quickswap exchange rate

**The conclusion is thrown first**: When the Quickswap exchange ratio is greater than the check-in cost exchange ratio and there is enough profit margin, the machine check-in robot user will operate multiple accounts to check in to obtain CBLB and sell it in Quickswap to complete the profit.

### Check-in cost analysis

The calculation method of the check-in cost conversion ratio is as follows: the fee for each wallet account to perform the check-in action includes, Cblb check-in fee (about `0.1131455` MATIC) + check-in gas fee (about `0.0054` MATIC) + Quickswap selling gas fee ( About `0.008` MATIC), if you consider multi-wallet batch check-in, it also includes the transfer CBLB fee for each wallet account (about `0.0001`MATIC)

Then the check-in cost of 100 wallet accounts is: 100 \* (0.1131455 + 0.0054 + 0.0001) + 0.008 = 11.832 MATIC

100 accounts have checked in from the Polygon block `24895721`, and a total of 2641 people have checked in at present, then the number of CBLB that can be obtained for the first check-in can be calculated by the mathematical model of Torricelli trumpet in the check-in contract, which is about `52.754` CBLB. 100 check-ins can be recursively added, and the total amount of CBLB that can be obtained is `5182.42` CBLB

It can be calculated that the CBLB acquisition cost of using 100 wallet addresses to complete 100 check-ins after 2,641 check-in robot users is: total CBLB acquisition / total MATIC consumption = 11.832 /5182.42 = 0.002283 CBLB/MATIC

In block `24895721`, the Quickswap permanent liquidity pool contains 950.95 MATIC, 295184 CBLB, and the exchange ratio can be calculated as: 950.95 / 295184 = 0.00322 CBLB/MATIC

### Robot arbitrageur profit

Then simply calculate if the robot arbitrageur controls 100 wallet accounts from block `24895721` to check in and sell CBLB (assuming the price of the Quickswap liquidity pool remains unchanged, which is actually less than the profit), the profit can be: (0.00322 - 0.002283 ) \* 5182.42 = 4.85 MATIC, at block `24895721`, the price of MATIC is about `1.67$`, then the estimated total profit is about `8$`. In fact, because Quickswap uses the AMM model, the actual profit is less than `8$` about is `7.5$`. In the steady state, it can be seen that the profit threshold for the robot model of the CBLB arbitrageur is set around `8$`.

**Conclusion**: As long as the current CBLB price of the Quickswap permanent liquidity pool is higher than the check-in cost and has a profit margin higher than the threshold, the robot arbitrageur has the incentive to use the robot to control multiple wallets to check in in batches and sell CBLB for profit.

## Why does the flow cell enter a steady state?

After the above analysis, due to the small arbitrage space, the users of the check-in robot have no power to operate the check-in robot to perform batch check-in to suppress the CBLB price, and the MATIC price fluctuation is in a normal state, double-pool arbitrage (here refers to the CBLB/MATIC flow pool of the quickswap flow pool) and Uniswap v3 CBLB/USDC liquidity pool) are also moderate, which in turn explains the relative stability of the liquidity pool.

## Next upgrade point of cblb.app

List flow cell data first

- The quickswap liquidity pool CBLB/MATIC created by the developer, the liquidity LP tokens are permanently locked in the check-in contract, the liquidity `950.95` MATIC, `295184` CBLB
- Liquidity CBLB/USDC for uniswap v3 created by maintainers, price range `0.00014094` - `0.015493 `, liquidity `986.6` USDC, `85940` CBLB

Summarize

- The total value of liquidity is about $3000, and the capacity of the liquidity pool is relatively small
- The check-in cost is about `0.002283` CBLB/MATIC, and the Quickswap liquidity pool price is `0.00322` CBLB/MATIC. The check-in cost is slightly less than the liquidity pool price, which is on the verge of being triggered by robot arbitrageurs. For large capital users, if they buy CBLB directly, they will directly give the robot Arbitrageurs form arbitrage space, causing large capital users to lose money
- Insufficient new check-in users

It is not difficult to see that if cblb.app wants to carry participants with a larger amount of funds, make it convenient for participants without technical ability to obtain more CBLB, and let the check-in advantage of check-in robot users is eliminated.

- Develop an easy-to-use batch check-in robot (operating 100 wallet accounts or more at the same time) and open source
- Developers, maintainers and participants use check-in robots to push up the check-in cost CBLB/MATIC price, creating space for large-capital participants to buy CBLB
- Developers continue to add Quickswap liquidity and lock it as permanent liquidity, increasing liquidity capacity
- Maintainers add more CBLB trading pair liquidity pools to create benign arbitrage space between liquidity pools and increase transaction activity

Written at the end, citing the [Transaction](https://polygonscan.com/tx/0xc1f5fd9c97046504c555375bd9cd78cc2969cc2116037b67945b6b5ba47c5682) of a check-in robot user , if you see this article, you can optimize the check-in fee of the bot, the exact value is `0.1131455399061032`(The calculation process can refer to the [CblbCheckin contract code](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88#code), function `getCheckinFee()`), no need to use `0.113147`, saving some is always good.

The above is for reference only, DYOR
