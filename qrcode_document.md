## 概述
本文档是对TokenPocket钱包常用二维码格式说明

转账二维码格式：
### EOS 系列底层
~~~
{
  "address":"xxxxxxxxxxxx" //收款账号
  "amount":"1" //数目
  "symbol":"EOS" //代币名字
  "contract":"eosio.token" //合约
  "precision":4 //精度
  "blockchain":"eos" //底层标识 enu bos等
  "action":"tokenTransfer" //转账操作标识
}
~~~

### 以太坊
~~~
{
  "address":"0x40e5A542087FA4b966209707177b103d158Fd3A4"
  "amount":"0.001"
  "contract":"" 
  "symbol":"ETH"
  "decimal":18
  "blockchain":"eth"
  "action":"tokenTransfer"
}
~~~

### 创建账号
~~~
{
  "account":"targetaccount"
  "owner":"Nnv8Mfx3ZfwJeR6daU9YBsSsJHeSvLJ8fr3ouUj1H34"
  "active":"Nnv8Mfx3ZfwJeR6daU9YBsSsJHeSvLJ8fr3ouUj1H34"
  "blockchain":"eos"
  "action":"createAccount"
}
~~~

### 冷钱包扫描观察钱包二维码
~~~
{
  "blockchain":"enu"
  "action":"coldWalletSign"
  "sign":"cf057bbfb72640471fd910bcb67639c22df9f92470936cddc1ade0e2f2e7dc4f5c00785cd839c41c1e0b00000000010000980ad20cf454000000572d3ccdcd01701533d348ea305500000000a8ed323221701533d348ea3055905436894a491132e80300000000000004454e550000000000000000000000000000000000000000000000000000000000000000000000000000"
  "isHash":0 //scatter 需要 如果需要signHash 则为1 否则为0
}
~~~

### 观察钱包扫描冷钱包签名后的数据
~~~
  SIG_K1_Kda4FjEawxZNT5yCrKbpy2WzSQtzt8HUr9oykDbjgpTMHPCBzDBeufa1bGXUJRja15m2RZzR99TG1U4gaL7rYZHbRnwiXJ
~~~

### IM 群二维码
~~~
{
  "type":23
  "teamId":"1603508625"
  "name":"team name"
}
~~~
