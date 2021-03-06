# Cblb developer wallet operation record

> Single source: [CBLB check-in gameplay introduction](https://github.com/cblb-app/cblb-articles/blob/master/2022/mannual-cblbcheckin-en.md)

- Developer wallet address: [0xe75Dc9d66eae386e76370bfcB4BbD5AdC7BeE6db](https://polygonscan.com/address/0xe75Dc9d66eae386e76370bfcB4BbD5AdC7BeE6db)

Developer Wallet Address Code of Conduct

- Unique account to deploy all [cblb.app](https://cblb.app/) contracts
- Routinely perform [CBLB check-in smart contract](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88) check-in action to receive CBLB
- Buy CBLB via Dex([Quickswap](https://quickswap.exchange/#/swap?inputCurrency=ETH&outputCurrency=0x7a45922F95C845Ff9bE01112AfCF207968a9cA0B))
- Extract the MATIC accumulated by the user's check-in from the [Cblb check-in smart contract](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)
- Add [Quickswap CBLB/MATIC liquidity pool](https://polygonscan.com/address/0xe99d5f930048ae3006205c87d2ddafa397014012) using CBLB received by check-in, purchased CBLB and acquired MATIC, and lock [liquidity LP tokens](https://polygonscan.com/token/0xe99d5f930048ae3006205c87d2ddafa397014012) into [CBLB check-in smart contract](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88) to become permanent CBLB/MATIC liquidity
- Add [Quickswap CBLB/WETH liquidity pool](https://polygonscan.com/address/0x8b6734217e1c5914cb729780fa9557629ff5b427) using CBLB received by check-in, purchased CBLB and WETH, and lock [liquidity LP tokens](https://polygonscan.com/token/0x8b6734217e1c5914cb729780fa9557629ff5b427) into [CBLB check-in smart contract](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88) to become permanent CBLB/WETH liquidity
- **Prohibition** Sell CBLB

## Deploy contract record

- Deploy the [CblbCheckin contract](https://polygonscan.com/tx/0xdda6622ac2cea5cc3e7ac5e21526487c35e51724660949364595f4f0797cf794) @2022/1/20
- Deploy [CBLB Token Contract](https://polygonscan.com/tx/0xbec5289b7dd1dbb71a8550cd9ccbff6f782ace6490907468c29ad3a01f980632) @2022/1/9

## Lock Quickswap CBLB/MATIC liquidity to Cblb check-in contract record

- Check-in contract address: [0x15942E96becA7fA6081740dFB74D7702ec2C3B88](https://polygonscan.com/address/0x15942e96beca7fa6081740dfb74d7702ec2c3b88)
- Quickswap CBLB/MATIC LP token address: [0xe99D5F930048AE3006205c87d2dDAfa397014012](https://polygonscan.com/address/0xe99d5f930048ae3006205c87d2ddafa397014012)

- Developer [locks CBLB/MATIC liquidity records](https://polygonscan.com/token/0xe99d5f930048ae3006205c87d2ddafa397014012?a=0x15942e96beca7fa6081740dfb74d7702ec2c3b88) on Polygonscan

## Lock Quickswap CBLB/WETH liquidity to Cblb check-in contract record

- Check-in contract address: [0x15942E96becA7fA6081740dFB74D7702ec2C3B88](https://polygonscan.com/address/0x15942e96beca7fa6081740dfb74d7702ec2c3b88)
- Quickswap CBLB/WETH LP token address: [0x8B6734217e1c5914CB729780fA9557629fF5B427](https://polygonscan.com/address/0x8B6734217e1c5914CB729780fA9557629fF5B427)

- Developer [locks CBLB/WETH liquidity records](https://polygonscan.com/token/0x8B6734217e1c5914CB729780fA9557629fF5B427?a=0x15942e96beca7fa6081740dfb74d7702ec2c3b88) on Polygonscan

## Extract the accumulated MATIC record of user check-in from the Cblb check-in smart contract

- [CblbCheckin contract send MATIC to developer history](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88#internaltx)
