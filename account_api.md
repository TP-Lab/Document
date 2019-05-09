## 通过邀请码注册账号，并更新邀请码状态为已使用
Request URL
```javascript
   /v1/invite_code/open_createacc
```
POST
```golang
        blockchain_id: 4, //4表示eos底层， 6表示bos底层， 7表示iost底层
        account: "tokenpocket2",
        public_key: "EOS5xy38sAWXZ5kStiQSKGK1mJNeKVfeJV3a3kpPRpqt1yryUsTGF",
        app_key: "newdex",
        timestamp: 1552397394,
        sign: "1015f06e780ffb68a4f556afabcb9b8604aa4fb8be1b35fc24c01a99bdc4af27"  //签名包含上面5个参数, 所有参数名按字母排序，拼接成app_key={app_secret}&key1=value&key2=value2做sha256, 注意这里的app_key是app_sercet
```
Response
```javascript
   {
        result: 0, //0表示成功
        message: "success",
        data: "d0ff5bbecc0d8cc2c48caf306e7a2585a79ffd510cb77e3a39d57222ba443012"
   }
```

## 通过网页邮件获取邀请码
Request URL
```javascript
   /v1/invite_code/open_codebyemail
```
POST
```golang
        blockchain_id: 4, //4表示eos底层， 6表示bos底层， 7表示iost底层
        email: "heipackermail@gmail.com",
        app_key: "newdex"
```
Response
```javascript
   {
        result: 0, //0表示成功
        message: "success",
        data: {
            "code": "120302"
        }
   }
```


## dapp注册帐号接口（支持手机号等中心化方式，也支持非中心化方式）
Request URL
```javascript
   /v1/invite_code/createacc
```
POST
```golang
        app_id: 'newdex' //创建帐号的名额从这个对应的扣除
        code: 815101 //如果为空只会从app_id对应的里扣除帐号激活码
        account_type: 0 // 帐号类型， 0表示去中心化的帐号类型， 1表示伙伴类型帐号（即通过手机号邮箱等方式注册的）
        blockchain_id: 4, //默认4 表示eos底层
        account: 'tokenpocket2'
        owner: 'EOS5xy38sAWXZ5kStiQSKGK1mJNeKVfeJV3a3kpPRpqt1yryUsTGF' //默认为空， 服务端生成
        active: 'EOS5xy38sAWXZ5kStiQSKGK1mJNeKVfeJV3a3kpPRpqt1yryUsTGF' //默认跟owner一样
        center_way: 0 // 创建方式， 0表示手机号方式，1表示邮箱方式， 只有account_type=1这个参数才有效
        center_num: '18700647311' //只有account_type=1这个参数才有效， 如果center_way=0则是手机号码， 如果center_way=1则是邮箱
        timestamp: 1552397394 //单位秒
        sign: '1015f06e780ffb68a4f556afabcb9b8604aa4fb8be1b35fc24c01a99bdc4af27'  //签名包含上面参数, 所有参数名按字母排序l， app_key放最前面，拼接成app_key=*****&app_id='newdex'&key1=value&key2=value2做sha256
```
Response
```javascript
   {
        result: 0, //0表示成功， 其他表示失败
        message: "success",
        data: "d0ff5bbecc0d8cc2c48caf306e7a2585a79ffd510cb77e3a39d57222ba443012"
   }
```