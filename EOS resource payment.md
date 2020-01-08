该文档以EOS转账为例描述了EOS资源代付签名基本流程
##  准备数据
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
				"actor": "1stbill.tp", //代付资源账号，必须放在authorization数组首位
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
		"signatures": ["SIG_K0_K0XXX","SIG_K1_K1XXX"]
	}
~~~

## TP签名接口说明
~~~
请求：

POST: "https://preserver.mytokenpocket.vip/v1/sign" "Accept: application/json"
Header: Signer //代付签名账号，示例中是1stbill.tp
Body: transaction对象，具体格式参照步骤二的数据

返回：
{
    "message": "success",
	"result": 0,
	"data":{
	    "signatures":SIG_K0_K0XXXX
	}
}
result:
0:成功
101：可以代付资源不足，提示用户充值
103：失败
108：拒绝签名
~~~
