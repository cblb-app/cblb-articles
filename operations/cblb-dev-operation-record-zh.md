# Cblb 开发者钱包操作记录

> Single source: [CBLB 签到玩法介绍](https://github.com/cblb-app/cblb-articles/blob/master/2022/mannual-cblbcheckin-zh.md)

- 开发者钱包地址： [0xe75Dc9d66eae386e76370bfcB4BbD5AdC7BeE6db](https://polygonscan.com/address/0xe75Dc9d66eae386e76370bfcB4BbD5AdC7BeE6db)

开发者钱包地址行为规范

- 部署所有[cblb.app](https://cblb.app/)合约的唯一账户
- 例行执行[CBLB 签到智能合约](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)签到动作领取 CBLB
- 通过 Dex([Quickswap](https://quickswap.exchange/#/swap?inputCurrency=ETH&outputCurrency=0x7a45922F95C845Ff9bE01112AfCF207968a9cA0B))买入 CBLB
- 从[Cblb 签到智能合约](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)提取用户签到积累的 MATIC
- 利用签到领取到的 CBLB 、买入的 CBLB 和获取的 MATIC 添加[Quickswap CBLB/MATIC 流动性池](https://polygonscan.com/address/0xe99d5f930048ae3006205c87d2ddafa397014012)，并把[流动性 LP 代币](https://polygonscan.com/token/0xe99d5f930048ae3006205c87d2ddafa397014012)锁入[CBLB 签到智能合约](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)成为永久 CBLB/MATIC 流动性
- 利用签到领取到的 CBLB 、买入的 CBLB 和 WETH 添加[Quickswap CBLB/WETH 流动性池](https://polygonscan.com/address/0x8b6734217e1c5914cb729780fa9557629ff5b427)，并把[流动性 LP 代币](https://polygonscan.com/token/0x8b6734217e1c5914cb729780fa9557629ff5b427)锁入[CBLB 签到智能合约](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)成为永久 CBLB/WETH 流动性
- 【禁止】卖出 CBLB

## 部署合约记录

- [部署 CblbCheckin 合约](https://polygonscan.com/tx/0xdda6622ac2cea5cc3e7ac5e21526487c35e51724660949364595f4f0797cf794) @2022/1/20
- [部署 CBLB 代币合约](https://polygonscan.com/tx/0xbec5289b7dd1dbb71a8550cd9ccbff6f782ace6490907468c29ad3a01f980632) @2022/1/9

## 锁定 Quickswap CBLB/MATIC 流动性 LP 代币到 Cblb 签到合约记录

签到合约地址: [0x15942E96becA7fA6081740dFB74D7702ec2C3B88](https://polygonscan.com/address/0x15942e96beca7fa6081740dfb74d7702ec2c3b88)  
Quickswap CBLB/MATIC LP 代币地址: [0xe99D5F930048AE3006205c87d2dDAfa397014012](https://polygonscan.com/address/0xe99d5f930048ae3006205c87d2ddafa397014012)

- 开发者[ 锁定 CBLB/MATIC 流动性 LP 代币记录](https://polygonscan.com/token/0xe99d5f930048ae3006205c87d2ddafa397014012?a=0x15942e96beca7fa6081740dfb74d7702ec2c3b88)

## 锁定 Quickswap CBLB/WETH 流动性 LP 代币到 Cblb 签到合约记录

签到合约地址: [0x15942E96becA7fA6081740dFB74D7702ec2C3B88](https://polygonscan.com/address/0x15942e96beca7fa6081740dfb74d7702ec2c3b88)  
Quickswap CBLB/WETH LP 代币地址: [0x8b6734217e1c5914cb729780fa9557629ff5b427](https://polygonscan.com/address/0x8b6734217e1c5914cb729780fa9557629ff5b427)

- 开发者[ 锁定 CBLB/WETH 流动性 LP 代币记录](https://polygonscan.com/token/0x8b6734217e1c5914cb729780fa9557629ff5b427?a=0x15942e96beca7fa6081740dfb74d7702ec2c3b88)

## 从 Cblb 签到智能合约提取用户签到积累的 MATIC 记录

- [CblbCheckin 签到智能合约发送 MATIC 给开发者历史记录](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88#internaltx)
