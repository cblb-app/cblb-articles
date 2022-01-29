# CBLB 签到玩法介绍

CBLB 签到包含了四个元素：

- [CBLB 签到智能合约](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)
- [CBLB 代币合约](https://polygonscan.com/token/0x7a45922F95C845Ff9bE01112AfCF207968a9cA0B)
- [开发者钱包地址](https://polygonscan.com/address/0xe75Dc9d66eae386e76370bfcB4BbD5AdC7BeE6db)
- [维护者钱包地址](https://polygonscan.com/address/0xf9e4b03a592152cbF2362222d7465f25ba627f9C)

以上四个元素构成了 CBLB 签到玩法，以上元素均部署在 Polygon

## CBLB 签到合约

- CBLB 签到智能合约：[0x15942E96becA7fA6081740dFB74D7702ec2C3B88](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)

用户通过[签到](https://cblb.app/prologue)行为

- 用户将**付出**少量 MATIC
- 用户将**得到**不定数量的 CBLB

用户每次签到需要付出的 MATIC 数量固定，约为`0.113147`MATIC。  
用户每次签到得到的 CBLB 数量从 1460 个开始递减，和`总签到人次`相关，满足公式

```
cblbAmount = 144600 / (index + 100)
```

其中

- `cblbAmount`：每次签到用户可以获得的 CBLB 数量
- `index`:总签到人次

具体信息见[CBLB 代币模型](https://cblb.app/supervise/cblb-token-model)

随着签到人数的增多，从签到合约的视角来看

- [CBLB 签到合约](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)**得到**用户签到付出的 MATIC
- [CBLB 签到合约](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)**付出**了 CBLB 代币

CBLB 代币为可 Mintable ERC20 代币，owner 已被设置为[CBLB 签到合约地址](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)，意味着每次签到行为对应的 CBLB 产生量被[CBLB 代币模型](https://cblb.app/supervise/cblb-token-model)公式严格控制，随着总签到人次增加，每次签到行为可获得的 CBLB 不断减少

为了防止高频签到造成 CBLB 被单一大户控制，对较晚参与签到玩法的用户造成**签到劣势**，[CBLB 签到合约](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)内设置了规则：同一钱包地址每 24 小时只能进行一次签到的约束

随着签到总人次的增加，可以得到一个 MATIC 获得量和 CBLB 发行量之间的关系，称之为**期望兑换比例**，该比例描述了一个 CBLB 对应的 MATIC 数量，计算公式

```
expectRatio = maticAcquired / cblbMinted
```

其中

- `expectRatio`：期望兑换比例，是 CBLB 保底兑换比例，单位 CBLB/MATIC
- `maticAcuired`：签到合约收到的 MATIC 总量

签到人次和 CBLB 发行数量对应关系，具体参考[CBLB 代币模型](https://cblb.app/supervise/cblb-token-model)

![](https://raw.githubusercontent.com/cblb-app/cblb-articles/master/introductions/imgs/cblb-checkin-issue-amout-table.png)

## CBLB 代币

- CBLB 代币合约：[0x7a45922F95C845Ff9bE01112AfCF207968a9cA0B](https://polygonscan.com/token/0x7a45922F95C845Ff9bE01112AfCF207968a9cA0B)

一个没有初始 Mint 的 Mintable ERC20 代币，每次签到会由[CBLB 签到智能合约](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)Mint 并发送 CBLB 给签到用户，发行数量被[CBLB 签到智能合约](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)里的[托里拆利小号模型](https://cblb.app/supervise/cblb-token-model)控制，随着签到人数增加，每次发行数量非比例性递减

## 开发者钱包

- 开发者钱包地址： [0xe75Dc9d66eae386e76370bfcB4BbD5AdC7BeE6db](https://polygonscan.com/address/0xe75Dc9d66eae386e76370bfcB4BbD5AdC7BeE6db)

开发者钱包地址行为规范

- 部署所有[cblb.app](https://cblb.app/)合约的唯一账户
- 例行执行[CBLB 签到智能合约](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)签到动作领取 CBLB
- 通过 Dex([Quickswap](https://quickswap.exchange/#/swap?inputCurrency=ETH&outputCurrency=0x7a45922F95C845Ff9bE01112AfCF207968a9cA0B))买入 CBLB
- 从[CBLB 签到智能合约](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)提取用户签到积累的 MATIC
- 利用签到领取到的 CBLB 、买入的 CBLB 和获取的 MATIC 添加[Quickswap CBLB/MATIC 流动性池](https://polygonscan.com/address/0xe99d5f930048ae3006205c87d2ddafa397014012)，并把[流动性 LP 代币](https://polygonscan.com/token/0xe99d5f930048ae3006205c87d2ddafa397014012)锁入[CBLB 签到智能合约](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)成为永久 CBLB/MATIC 流动性
- 【禁止】卖出 CBLB

## 维护者钱包

- 维护者钱包地址：[0xf9e4b03a592152cbF2362222d7465f25ba627f9C](https://polygonscan.com/address/0xf9e4b03a592152cbF2362222d7465f25ba627f9C)

维护者钱包地址行为规范

- 例行执行[CBLB 签到智能合约](https://polygonscan.com/address/0x15942E96becA7fA6081740dFB74D7702ec2C3B88)签到动作领取 CBLB
- 创建 Polygon 上[Uniswap v3 CBLB/MATIC 流动性](https://app.uniswap.org/#/pool/23854)，[Uniswap v3 CBLB/USDC 流动性](https://app.uniswap.org/#/pool/27318?chain=polygon)，Uniswap v3 流动性收益可自由支配
- 执行买入 CBLB 和卖出 CBLB 动作
- 可以囤积 CBLB 获利

综上仅作参考，DYOR
