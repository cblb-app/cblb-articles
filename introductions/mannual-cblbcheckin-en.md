# CBLB check-in gameplay introduction

The CBLB check-in game is the entrance to the CBLB Web3 economic system based on smart contracts. Both the [Cblb check-in contract](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88) and the [CBLB token contract](https://polygonscan.com/token/0x7a45922F95C845Ff9bE01112AfCF207968a9cA0B) are deployed in Polygon.

A CBLB check-in consists of four elements:

- [CBLB check-in smart contract](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)
- [CBLB Token Contract](https://polygonscan.com/token/0x7a45922F95C845Ff9bE01112AfCF207968a9cA0B)
- [Developer wallet address](https://polygonscan.com/address/0xe75Dc9d66eae386e76370bfcB4BbD5AdC7BeE6db)
- [Maintainer wallet address](https://polygonscan.com/address/0xf9e4b03a592152cbF2362222d7465f25ba627f9C)

The above four elements constitute the CBLB check-in gameplay, and the above elements are all deployed in Polygon

## CBLB check-in contract

- CBLB check-in smart contract: [0x15942E96becA7fA6081740dFB74D7702ec2C3B88](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)

User check-in behavior

- Users will pay a small amount of MATIC
- Users will get a variable amount of CBLB

The amount of MATIC that users need to pay for each check-in is fixed, about `0.113146`MATIC.

The number of CBLBs obtained by the user for each check-in starts to decrease from 1460, which is related to the `total number of check-ins` and satisfies the formula

```
cblbAmount = 144600 / (index + 100)
```

What's more

- `cblbAmount`: The amount of CBLB a user can get per check-in
- `index`: total check-ins

For details, see [CBLB Token Model](https://cblb.app/supervise/cblb-token-model)

As the number of check-ins increases, from the perspective of check-in contracts

- The [CBLB check-in contract](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88) **gets** the MATIC paid by the user for check-in
- [CBLB check-in contract](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88) **pays** CBLB tokens

The CBLB token is a Mintable ERC20 token, and the owner has been set as the [CBLB check-in contract address](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88), which means that the CBLB generation corresponding to each check-in behavior is strictly controlled by the [CBLB token model formula](https://cblb.app/supervise/cblb-token-model). CBLB available to behavior is decreasing

In order to prevent CBLB from being controlled by a single large account due to high-frequency check-in, which will cause a **check-in disadvantage** for users who participate in the check-in game later, the [CBLB check-in contract](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88) sets a rule: the same wallet address can only be checked in once every 24 hours.

With the increase of the total number of check-ins, a relationship between the amount of MATIC obtained and the amount of CBLB issued can be obtained, which is called the **expected exchange ratio**. This ratio describes the amount of MATIC corresponding to a CBLB. The calculation formula

```
expectRatio = maticAcquired / cblbMinted
```

What's more

- `expectRatio`: Expected exchange ratio, which is the guaranteed exchange ratio of CBLB, in CBLB/MATIC
- `maticAcuired`: The total amount of MATIC received by the check-in contract

The corresponding relationship between the number of check-ins and the number of CBLB issuance, please refer to the CBLB token model for details

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/introductions/imgs/cblb-checkin-issue-amout-table-en.png)

## CBLB token

- CBLB token contract: [0xe75Dc9d66eae386e76370bfcB4BbD5AdC7BeE6db](https://polygonscan.com/address/0xe75Dc9d66eae386e76370bfcB4BbD5AdC7BeE6db)

A Mintable ERC20 token without initial Mint, each time a check-in will be made by CBLB to check in the smart contract Mint and send CBLB to the check-in user. The number of issuances is controlled by [the Torricelli trumpet model](https://cblb.app/supervise/cblb-token-model) in the CBLB check-in smart contract, and as the number of check-ins increases , the number of each issuance decreases non-proportionally

## Developer wallet

- Developer wallet address: [0xe75Dc9d66eae386e76370bfcB4BbD5AdC7BeE6db](https://polygonscan.com/address/0xe75Dc9d66eae386e76370bfcB4BbD5AdC7BeE6db)

Developer Wallet Address Code of Conduct

- Unique account to deploy all [cblb.app](https://cblb.app/) contracts
- Routinely perform [CBLB check-in smart contract](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88) check-in action to receive CBLB
- Buy CBLB via Dex([Quickswap](https://quickswap.exchange/#/swap?inputCurrency=ETH&outputCurrency=0x7a45922F95C845Ff9bE01112AfCF207968a9cA0B))
- Extract the MATIC accumulated by the user's check-in from the [CBLB check-in smart contract](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)
- Add [Quickswap CBLB/MATIC liquidity pool](https://polygonscan.com/address/0xe99d5f930048ae3006205c87d2ddafa397014012) using CBLB received by check-in, purchased CBLB and acquired MATIC, and lock [liquidity LP tokens](https://polygonscan.com/token/0xe99d5f930048ae3006205c87d2ddafa397014012) into [CBLB check-in smart contract](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88) to become permanent CBLB/MATIC liquidity
- **Prohibition** Sell CBLB

## Maintainer wallet

- Maintainer wallet address: [0xf9e4b03a592152cbF2362222d7465f25ba627f9C](https://polygonscan.com/address/0xf9e4b03a592152cbF2362222d7465f25ba627f9C)

Maintainer Wallet Address Code of Conduct

- Routinely perform CBLB sign-in smart contract sign-in action to receive CBLB
- Create [Uniswap v3 CBLB/MATIC liquidity](https://app.uniswap.org/#/pool/23854) on Polygon, [Uniswap v3 CBLB/USDC liquidity](https://app.uniswap.org/#/pool/27318?chain=polygon), Uniswap v3 liquidity income is discretionary
- Execute buy CBLB and sell CBLB actions
- Can hoard CBLB for profit

The above is for reference only, DYOR
