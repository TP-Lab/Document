# 该文档以EOS转账为例描述了EOS资源代付签名基本流程
# This document uses EOS transfer as an example to describe the basic flow of the EOS resource payment (Only charge the first authorizer) signature.
##  准备数据
## Prepare the data

~~~
{
		"expiration": "2020-01-08T02:41:45",
		"ref_block_num": 17815,
		"ref_block_prefix": 408124069,
		"max_net_usage_words": 0,
		"max_cpu_usage_ms": 0,
		"delay_sec": 0,
		"actions": [{
			"account": "eosio.token",
			"authorization": [{
				"actor": "1stbill.tp", //代付资源账号，必须放在authorization数组首位  The resource payer's account must be placed first in the authorization array

				"permission": "active"
			}, {
				"actor": "xiaoyuantest",
				"permission": "active"
			}],
			"data": {
				"quantity": "0.0001 EOS",
				"to": "eosiomanager",
				"from": "xiaoyuantest",
				"memo": ""
			},
			"name": "transfer"
		}],
		"context_free_actions": [],
		"transaction_extensions": []
	}
~~~

##  将步骤一准备的数据使用操作账号签名，这里使用的是xiaoyuantest账号签名，得到以下数据
## Sign the data of step 1 with the operation account. Here we sign with xiaoyuantest to get the following data

~~~
{
		"compression": "none",
		"transaction": {
			"expiration": "2020-01-08T02:41:45",
			"ref_block_num": 17815,
			"ref_block_prefix": 408124069,
			"max_net_usage_words": 0,
			"max_cpu_usage_ms": 0,
			"delay_sec": 0,
			"context_free_actions": [],
			"actions": [{
				"account": "eosio.token",
				"name": "transfer",
				"authorization": [{
					"actor": "1stbill.tp",
					"permission": "active"
				}, {
					"actor": "xiaoyuantest",
					"permission": "active"
				}],
				"data": "90b1cad3684f8deb701533d348ea3055010000000000000004454f530000000000"
			}],
			"transaction_extensions": []
		},
		"signatures": ["SIG_K1_K57rT6Vqe5Hez7LNHPW2x78WgjoiVWxqNpoyJpAjQPjXxJe266jdmsx9sd7TU4dEscMAmS5F97jdMuiPQb66448qGRMkb1"]
	}
~~~

##  将步骤2得到的transaction对象取出，使用TP签名接口签名，得到结果如下
## Take the transaction object obtained in step 2 and sign it with the TP signature interface. The result is as follows

~~~
{
	"message": "success",
	"result": 0,
	"data":{
	    "signature":SIG_K0_K0XXXX
	}
}
~~~

##  将TP签名后得到的signature插入步骤2中signatures数组的首位。并将组装好的数据广播。最终广播的数据结构如下
## Insert the signature (obtained by the TP signature) into the first position of the signatures array obtained in step 2. And broadcast the assembled data. The data structure of the final broadcast is as follows

~~~
{
		"compression": "none",
		"transaction": {
			"expiration": "2020-01-08T02:41:45",
			"ref_block_num": 17815,
			"ref_block_prefix": 408124069,
			"max_net_usage_words": 0,
			"max_cpu_usage_ms": 0,
			"delay_sec": 0,
			"context_free_actions": [],
			"actions": [{
				"account": "eosio.token",
				"name": "transfer",
				"authorization": [{
					"actor": "1stbill.tp",
					"permission": "active"
				}, {
					"actor": "xiaoyuantest",
					"permission": "active"
				}],
				"data": "90b1cad3684f8deb701533d348ea3055010000000000000004454f530000000000"
			}],
			"transaction_extensions": []
		},
		//TP接口签名得到的数据必须放在首位，否则会导致操作失败
                //The data signed by the TP interface must be put first, or the operation will fail
		"signatures": ["SIG_K0_K0XXX","SIG_K1_K1XXX"]
	}
~~~

## TP签名接口说明
## TP signature interface description

~~~
请求：
Request:


POST: "https://preserver.mytokenpocket.vip/v1/sign" "Accept: application/json"
Header: Signer //代付签名账号，示例中是1stbill.tp  In the example, the payer's signer account is 1stbill.tp
Body: transaction对象，具体格式参照步骤二的数据  transaction object, refer to the data in step 2 for the specific format

返回：
Response:
{
    "message": "success",
	"result": 0,
	"data":{
	    "signature":SIG_K0_K0XXXX
	}
}
result:
0:成功 Success
101：可以代付资源不足，提示用户充值  Insufficient resource in the payer's account, please remind the user to top-up resources.
103：失败 Fail
108：拒绝签名 Refuse to sign
~~~
