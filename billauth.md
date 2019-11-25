## 概述
本文档是 TokenPocket 代付签名授权 相关的 API， （需要提前联系TP 获取 appid 和 配置action白名单， 联系方式：bd@tokenpocket.pro）

### 签名

## 请求中心化做签名
Request URL
```javascript
    /v1/sign
```
POST
```golang
    { transaction: TxObject} //TxObject 要签名的 transaction 的对象 (其中data 是序列化后的)
    //header添加 `Appid`: `xxxx` // 请联系我们 bd@tokenpocket.pro 获取
    //header添加 `Sign`: `xxxxx` // sha256(appkey=xxxx&appid=xxxxx&timestamp=now)
    //header添加 `Chainid`: 表示当前使用的chainId
    //header添加 `Timestamp`: 签名的时间
```
Response
```javascript
   {
        result: 0,
        message: "success",
        data: {
            "signature": "签名内容"
        }
   }
```
