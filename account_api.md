## 通过邀请码注册账号，并更新邀请码状态为已使用
Request URL
```javascript
   /v1/invite_code/open_createacc
```
POST
```golang
        blockchain_id: 4, //默认4 表示eos底层
        code: 815101
        account: 'tokenpocket2'
        public_key: 'EOS5xy38sAWXZ5kStiQSKGK1mJNeKVfeJV3a3kpPRpqt1yryUsTGF'
        app_key: 'newdex'
        timestamp: 1552397394
        sign: '1015f06e780ffb68a4f556afabcb9b8604aa4fb8be1b35fc24c01a99bdc4af27'  //签名包含上面5个参数, 所有参数名按字母排序，拼接成key1=value&key2=value2&app_key='newdex'做sha256
```
Response
```javascript
   {
        result: 0, //0表示成功
        message: "success",
        data: "d0ff5bbecc0d8cc2c48caf306e7a2585a79ffd510cb77e3a39d57222ba443012"
   }
```