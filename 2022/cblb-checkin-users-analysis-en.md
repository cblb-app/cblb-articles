# Cblb.app check-in gameplay and user analysis

<!-- MarkdownTOC -->

- [1. Overview](#1-overview)
- [2. Basic data](#2-basic-data)
- [3. Check-in in-game character decheck](#3-check-in-in-game-character-decheck)
- [4. Introduction to the check-in gameplay mechanism](#4-introduction-to-the-check-in-gameplay-mechanism)
- [5. The number of characters after the online check-in gameplay is increased](#5-the-number-of-characters-after-the-online-check-in-gameplay-is-increased)
  - [5.1 Behavior analysis of robot arbitrageurs](#51-behavior-analysis-of-robot-arbitrageurs)
  - [5.2 Participant Behavior Analysis](#52-participant-behavior-analysis)
- [6. Character analysis after the cold start of the check-in gameplay](#6-character-analysis-after-the-cold-start-of-the-check-in-gameplay)
  - [6.1 Contributions and constraints of four roles other than contracts to the CBLB Web3 economic system](#61-contributions-and-constraints-of-four-roles-other-than-contracts-to-the-cblb-web3-economic-system)
  - [6.2 Analysis of Risk from Developers](#62-analysis-of-risk-from-developers)
- [7. Permanent liquidity CBLB/MATIC analysis](#7-permanent-liquidity-cblbmatic-analysis)
- [8. Give participation suggestions through CBLB related exchange ratio parameters](#8-give-participation-suggestions-through-cblb-related-exchange-ratio-parameters)
- [9. Summary](#9-summary)

<!-- /MarkdownTOC -->

<a id="1-overview"></a>

## 1. Overview

cblb.app is a dApp on Polygon after deploying the Cblb check-in contract and the CBLB token contract. As of January 29, 2022, a total of 1,266 people have checked in. Obtaining such data without any publicity highlights the charm of Web3.

It also proves the activeness of Web3 from the side, especially the users with development ability occupy a large proportion.

<a id="2-basic-data"></a>

## 2. Basic data

- CBLB token contract is deployed on January 9, 2022, [Transaction hash](https://polygonscan.com/tx/0xbec5289b7dd1dbb71a8550cd9ccbff6f782ace6490907468c29ad3a01f980632)
- Cblb check-in contract is deployed on January 20, 2022, [Transaction hash](https://polygonscan.com/tx/0xdda6622ac2cea5cc3e7ac5e21526487c35e51724660949364595f4f0797cf794)

The above two smart contract codes have been verified by Polygonscan, and the development project has been open sourced

- [CBLB Token Contract Polygonscan](https://polygonscan.com/address/0x7a45922F95C845Ff9bE01112AfCF207968a9cA0B#code)
- [Cblb check in contract Polygonscan](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88#code)
- [Open source engineering Github repository](https://github.com/cblb-app/cblb-token-checkin-contracts)

<a id="3-check-in-in-game-character-decheck"></a>

## 3. Check-in in-game character decheck

The check-in gameplay consists of four elements

- [CBLB Check-in Contract](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)
- [CBLB Token Contract](https://polygonscan.com/token/0x7a45922F95C845Ff9bE01112AfCF207968a9cA0B)
- [Developer](https://polygonscan.com/address/0xe75Dc9d66eae386e76370bfcB4BbD5AdC7BeE6db)
- [Maintainer](https://polygonscan.com/address/0xf9e4b03a592152cbF2362222d7465f25ba627f9C)

<a id="4-introduction-to-the-check-in-gameplay-mechanism"></a>

## 4. Introduction to the check-in gameplay mechanism

For details, see [CBLB Check-in Game Introduction](https://cblb.app/supervise/cblb-check-in)

- CBLB token is an ERC20 standard Mintable token issued on Polygon, with an initial issuance of 0 and no upper limit
- The `owner()` of the CBLB token is the Cblb check-in contract
- The issuance of CBLB tokens can only be done by calling the `checkin()` method of the Cblb check-in contract. The corresponding UI interface is the [cblb.app Prologue](https://cblb.app/prologue).The amount of Mint per time is calculated by [the mathematical model of the Torricelli trumpet in the Cblb check-in contract](https://cblb.app/supervise/cblb-token-model). The number of CBLB `mint()` is only related to the total number of check-ins. The more the total number of check-ins, the less CBLB tokens will be issued each time the Cblb check-in contract `mint()`
- For each check-in, the user needs to pay a fixed payment of about `0.113146` MATIC to increase the guaranteed price of CBLB tokens. The same wallet address can only check-in once in 24 hours
- Developers can receive the MATIC accumulated in the Cblb check-in smart contract by calling the Cblb check-in contract function `devWithdrawAcquiredFee()`.
- Any user can call the Cblb check-in contract function `sendAcquireFeeToDev()` to send the MATIC accumulated in the Cblb check-in contract to the developer wallet
- Developers receive the MATIC collected in the Cblb check-in contract for: buying CBLB, adding [Quickswap CBLB/MATIC liquidity](https://info.quickswap.exchange/#/pair/0xe99d5f930048ae3006205c87d2ddafa397014012), locking [CBLB/MATIC LP tokens](https://polygonscan.com/token/0xe99d5f930048ae3006205c87d2ddafa397014012) to the Cblb check-in contract to constitute the permanent liquidity of the system
- The developer initially provides some MATIC to start the check-in game: buy CBLB tokens, add [Quickswap CBLB/MATIC liquidity](https://info.quickswap.exchange/#/pair/0xe99d5f930048ae3006205c87d2ddafa397014012), lock [CBLB/MATIC LP tokens](https://polygonscan.com/token/0xe99d5f930048ae3006205c87d2ddafa397014012) to the Cblb check-in contract to constitute the permanent liquidity of the system
- The maintainer initially provides some MATIC for: establishing liquidity that can earn income (currently [Uniswap v3 CBLB/USDC](https://app.uniswap.org/#/pool/27318?chain=polygon)), buying and selling CBLB tokens to increase CBLB activity, making profits through liquidity pool fees, selling CBLB to gain profit

<a id="5-the-number-of-characters-after-the-online-check-in-gameplay-is-increased"></a>

## 5. The number of characters after the online check-in gameplay is increased

After completing the deployment of CBLB token contract and Cblb check-in contract, developers provide initial liquidity, maintainers establish liquidity pools, and new roles from Web3 quickly appeared in the whole system, namely:

- Robot arbitrageur
- Participant

<a id="51-behavior-analysis-of-robot-arbitrageurs"></a>

### 5.1 Behavior analysis of robot arbitrageurs

Robot arbitrageurs appeared because the developers initially provided the exchange ratio of the CBLB/MATIC liquidity pool and there was an arbitrage space between the **check-in cost**. Surprisingly, the CBLB check-in game was launched and harvested without any announcement. After thousands of check-ins, a simple conclusion can be drawn:

- **In the defi section of the Polygon blockchain, the discovery and execution of robo-arbitrage opportunities is well established**

This is due to the advantages of Polygon's low interaction fees and blockchain confirmation speed blocks.

For the Cblb check-in contract, the CBLB acquisition cost for the bot arbitrageur is

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/2022/imgs/cblb-price-base-en.png)

In actual operation, the mode adopted by the robot arbitrageur is to check in with dozens of wallet addresses, and collect them into one address to complete the swap, then the check-in cost is

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/2022/imgs/cblb-price-average-en.png)

For the Cblb check-in game, the number of CBLB tokens obtained by each check-in decreases with the number of check-ins, and it can be concluded that:

- **Robot arbitrageurs will intervene when the price of CBLB in the Quickswap permanent liquidity pool is too high relative to the check-in cost, complete the arbitrage and suppress the price of CBLB**

<a id="52-participant-behavior-analysis"></a>

### 5.2 Participant Behavior Analysis

The behavior patterns of participants include: check in to receive CBLB, sell CBLB, and buy CBLB. It is the behavior pattern of most defi users, which can be summarized as "digging", "withdrawing", and "selling" to make a profit, or "hoarding coins" and "selling" to make a profit.

<a id="6-character-analysis-after-the-cold-start-of-the-check-in-gameplay"></a>

## 6. Character analysis after the cold start of the check-in gameplay

To sum up, there are six roles in the check-in gameplay system, which are:

- [CBLB Check-in Contract](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)
- [CBLB Token Contract](https://polygonscan.com/token/0x7a45922F95C845Ff9bE01112AfCF207968a9cA0B)
- [Developer](https://polygonscan.com/address/0xe75Dc9d66eae386e76370bfcB4BbD5AdC7BeE6db)
- [Maintainer](https://polygonscan.com/address/0xf9e4b03a592152cbF2362222d7465f25ba627f9C)
- Robot arbitrageur
- Participant

Analysis can be drawn from the contribution of different roles in the system to the price of CBLB

- Cblb check-in contract: form the bottoming condition of CBLB price, and generate **CBLB check-in cost price**
- Developer: Execute the three steps of CBLB price bottoming: "receive MATIC", provide CBLB/MATIC liquidity, "lock in liquidity LP tokens to check-in contract", generate CBLB issuance volume and Cblb check-in contract to collect the balance between MATIC Exchange relationship, called **CBLB expected exchange ratio**
- Robot arbitrageur: Completing CBLB price suppression can prevent the unhealthy rise of CBLB in any situation of issuance and price, and avoid huge losses for large investors and ordinary participants

<a id="61-contributions-and-constraints-of-four-roles-other-than-contracts-to-the-cblb-web3-economic-system"></a>

### 6.1 Contributions and constraints of four roles other than contracts to the CBLB Web3 economic system

At this point we have a small metaverse economic system, which we prefer to call a small Web3 economic system.

This small Web3 economic system with upper bound and bottom constraints is the basis for a dApp to carry all other subsequent functions, as well as a space for value balance

- Participants: Check in to push up the bottoming price of CBLB tokens **(contribution)**, sell CBLB for profit **(constraint)**
- Developer: Check in pushes up the bottom price of CBLB tokens, providing permanent liquidity **(contribution)**
- Maintainer: Check in to push up the bottom price of CBLB tokens, sell CBLB for profit through self-built liquidity arbitrage **(constraint)**
- Robot arbitrageur: check-in pushes up the bottoming price of CBLB tokens **(contribution)**, and uses the difference between the CBLB check-in cost conversion ratio and the current CBLB conversion ratio to arbitrage **(constraint)**

conclusion can be made

- **The four human factors in the system provide three kinds of contributions and three kinds of constraints, ensuring the long-term stability and sustainable development of the CBLB Web3 economic system**

<a id="62-analysis-of-risk-from-developers"></a>

### 6.2 Analysis of Risk from Developers

Based on the above introduction and analysis, the most intuitive risk point comes from **whether developers continue to add permanent liquidity**.

From the perspective of decentralization, the risk of developers' behavior patterns is also the risk of cblb.app itself. This risk point cannot be eliminated for cblb.app, but the advantage of decentralized apps is that all behaviors can be checked on the chain, which is convenient for users to view and supervise.

Therefore, from the perspective of the stability of a system, even if the developer's wallet address does not perform subsequent permanent liquidity addition, it is limited to the value other than the current permanent liquidity, and once the behavior constraints are not observed, it will be reflected on the chain immediately. As long as the developer's wallet address has content beyond the behavioral constraints, the credit of cblb.app itself will also disappear.

conclusion can be made

- **The risk monitoring of cblb.app is in a real-time state, and the data on the chain is completely open, which is in line with the idea of ​​dApp opening and open source**

<a id="7-permanent-liquidity-cblbmatic-analysis"></a>

## 7. Permanent liquidity CBLB/MATIC analysis

The above analysis is based on the supremacy of two assumptions

- MATIC price unchanged
- There is always a user to check in

After the introduction of these two variables, it can be concluded that the introduction of these two variables is more of a contribution to the role of the CBLB Web3 economic system.

From the perspective of liquidity, the permanent liquidity pool is CBLB/MATIC, and the liquidity pool established by the maintainer is CBLB/USDC. Then, as the price of MATIC fluctuates, these two pools will generate natural arbitrage space, and the existence of robot arbitrageurs will smooth the price difference between the two pools, thus bringing the continuous fluctuation power of the CBLB Web3 economic system.

The generation of this fluctuation power provides arbitrage space for maintainers and participants to meet the needs of the stable development of the CBLB Web3 economic system. At the same time, the permanent liquidity pool on [Quickswap will continue to accumulate 0.3%](https://quickswap-layer2.medium.com/welcome-to-quickswap-exchange-93d47e057633) of the value of the transaction volume to itself, completing the continuous growth of the value of the CBLB Web3 economic system

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/2022/imgs/quickswap-fee.png)

From the check-in point of view, if there is no user check-in, then the system can also gain momentum from the price fluctuation of MATIC, and the check-in behavior only affects the speed of the growth rate of the CBLB Web3 economic system.

<a id="8-give-participation-suggestions-through-cblb-related-exchange-ratio-parameters"></a>

## 8. Give participation suggestions through CBLB related exchange ratio parameters

The three CBLB price points mentioned above are

- CBLB check-in cost conversion ratio
- CBLB expected exchange rate
- Quickswap permanent liquidity current CBLB conversion ratio

The data points have been shown in [cblb.app/supervise/cblb-token-info](https://cblb.app/supervise/cblb-token-info), since the number of CBLB issuances and the number of check-ins are uniquely correlated, when the 1266th checking in

- The 1266th check-in to receive CBLB amount is: `105.9` CBLB
- Check-in requires payment of MATIC: `0.113146` MATIC
- **CBLB check-in cost conversion ratio** can be calculated: `0.113146 / 105.9 = 0.001068` CBLB/MATIC
- The total amount of CBLB issued is: `378723.9` CBLB
- The amount of MATIC accumulated in the **Cblb check-in contract**: `143.2` MATIC
- **CBLB expected exchange ratio** can be calculated: `143.2 / 378723.9 = 0.000378` CBLB/MATIC
- Quickswap permanent liquidity at the 1266th check-in **Current CBLB exchange ratio**: `0.002771` CBLB/MATIC

At this time, the **robot arbitrageur** did not continue to suppress the price of CBLB, which can be regarded as a short-term stability, and the price relationship can be obtained.

```
CBLB expected exchange rate < CBLB check-in cost exchange rate < current CBLB exchange rate
```

Suggestions for participation

- For **robot arbitrageurs**: you should pay attention to the difference between **CBLB check-in cost conversion ratio** and **current CBLB conversion ratio**, if the difference expands, you can make arbitrage
- For **participants**: if you plan to **buys**, you need to control the buying volume, if the buying volume is too large, and the **current CBLB exchange rate** is much higher than the **CBLB check-in cost exchange rate**, thus creating arbitrage space for **robot arbitrageurs**, resulting in short-term losses
- For **participants**: plan to check in, no need to pay attention to the ratio

<a id="9-summary"></a>

## 9. Summary

After a relatively stable CBLB Web3 economic system is established after a cold start, the next step is to enter the function superposition stage of cblb.app

The above is for reference only, DYOR
