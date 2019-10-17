## 概述
本文档是 TokenPocket 快讯 相关的 API

### 快讯列表

Request URL
```javascript
    /v1/news/list
```
GET
```javascript
    start: 0 //可选 默认0
    count: 10 //可选 默认10 
    lang: 'zh-Hans' // 可选  zh-Hans 为中文  en 为英文  默认 'zh-Hans' 
    app_key: '' // 请联系 bd@tokenpocket.pro
```

Response
```javascript
   {
        result: 0,
        message: "success",
        data: [
            {
                hid: 1,
                title: "区块链世界",
                content: "司法局哦玩儿附近沃尔",
                source: "币世界",
                "tag_bg_color": "",
                "tag_color":    "",
                "top_icon":     "",
                "bottom_icon":  "",
                "app_id":       1,
                img_url: "https://tp-statics.cdn.bcebos.com/news/1571278859982",
                create_time: "2019-10-17T10:26:11Z",
                update_time: "2019-10-17T10:26:11Z"
            },
            {
                hid: 2,
                title: "区块链世界",
                content: "司法局哦玩儿附近沃尔",
                source: "币世界",
                "tag_bg_color": "",
                "tag_color":    "",
                "top_icon":     "",
                "bottom_icon":  "",
                "app_id":       1,
                img_url: "https://tp-statics.cdn.bcebos.com/news/1571278859982",
                create_time: "2019-10-17T10:26:11Z",
                update_time: "2019-10-17T10:26:11Z"
            }
        ]
   }
```


## 根据id获取快讯详情
Request URL
```javascript
    /v1/news
```
GET
```javascript
    id: 2 // hid
    app_key: '' // 请联系 bd@tokenpocket.pro
```
Response
```javascript
   {
        result: 0,
        message: "success",
        data: {
            hid: 2,
            title: "区块链世界",
            content: "司法局哦玩儿附近沃尔",
            source: "币世界",
            "tag_bg_color": "",
            "tag_color":    "",
            "top_icon":     "",
            "bottom_icon":  "",
            "app_id":       1,
            img_url: "https://tp-statics.cdn.bcebos.com/news/1571278859982",
            create_time: "2019-10-17T10:26:11Z",
            update_time: "2019-10-17T10:26:11Z"
        }
   }
```