# 预约后 index

## 作用

预约成功后刷新状态，确认当前预约是否存在，并返回预约 token、状态、座位号、签到页/二维码/ websocket 等信息。

## URL

```text
POST https://wechat.v2.traceint.com/index.php/graphql/
```

## operationName

`index`

## Request Headers

- `content-type: application/json`
- `app-version: 2.2.9`
- `origin: https://web.traceint.com`
- `referer: https://web.traceint.com/`
- `user-agent: Mozilla/5.0 ... WindowsWechat ...`
- `cookie: <REDACTED_COOKIE_PARTS>`

## Request Body

```json
{
  "operationName": "index",
  "query": "query index($url: String!, $pos: String!, $param: [hash]) {\n userAuth {\n reserve {\n reserve {\n token\n status\n user_id\n user_nick\n sch_id\n sch_name\n lib_id\n lib_name\n lib_floor\n seat_name\n }\n qrUrl\n weixiao {\n isOpen\n url\n pic\n }\n }\n webSocket {\n url\n qrType\n protocol\n }\n config: user {\n notSign: getSchConfig(fields: \"reserve.notSign\")\n blueSignOpen: getSchConfig(fields: \"adm.blueSignOpen\")\n doorSignOpen: getSchConfig(fields: \"adm.doorSignOpen\")\n doorSignURL: getSchConfig(fields: \"adm.doorSignURL\")\n forbidQrValid: getSchConfig(fields: \"forbidQrValid\", extra: true)\n }\n }\n wechatJSSDK(url: $url) {\n appId\n timestamp\n nonceStr\n signature\n }\n ad(pos: $pos, param: $param) {\n name\n pic\n url\n }\n}",
  "variables": {
    "url": "https://web.traceint.com/web/index.html",
    "pos": "新版-签到页面-中间"
  }
}
```

## Response Body

```json
{
  "data": {
    "userAuth": {
      "reserve": {
        "reserve": {
          "token": "<REDACTED_RESERVE_TOKEN>",
          "status": 2,
          "user_id": 45409576,
          "user_nick": "<REDACTED_NICKNAME>",
          "sch_id": 20380,
          "sch_name": "东北农业大学",
          "lib_id": 126500,
          "lib_name": "212自习室",
          "lib_floor": "二楼",
          "seat_name": "341"
        },
        "qrUrl": "https://mp.weixin.qq.com/s/xxxxx",
        "weixiao": {
          "isOpen": true,
          "url": "https://msg.weixiao.qq.com/t/<REDACTED>",
          "pic": "https://wechat.v2.traceint.com/data/attachment/2023-01-31/pre_xxx.jpg"
        }
      },
      "webSocket": {
        "url": "wss://wechat.v2.traceint.com/ws",
        "qrType": "qr/flush",
        "protocol": "{\"AUTH_ERROR\":1000,\"JS\":1001,\"ID\":1002,\"MSG\":1003,\"ALERT\":1004,\"JSON\":1005,\"CLOSE_TOKEN\":\"TKC\",\"TOKEN\":\"TK\",\"TO\":1006}"
      },
      "config": {
        "notSign": "false",
        "blueSignOpen": "false",
        "doorSignOpen": "false",
        "doorSignURL": "\"https:\\/\\/mp.weixin.qq.com\\/s\\/xxxxx\"",
        "forbidQrValid": "\"\""
      }
    },
    "wechatJSSDK": {
      "appId": "wx2996d437cd442527",
      "timestamp": 1782986422,
      "nonceStr": "<REDACTED_NONCE>",
      "signature": "<REDACTED_SIGNATURE>"
    },
    "ad": []
  }
}
```

## 关键字段

- `data.userAuth.reserve.reserve`
- `token`
- `status`
- `lib_id`
- `seat_name`
- `qrUrl`
- `webSocket.url`
- `wechatJSSDK`

## 对旧项目可能的映射

- 预约后再次确认当前预约状态
- 旧项目 `index` 的“预约后确认”变体
- `have_seat`
- `token / seat_name / status` 的确认来源

## 备注

- 这是查询接口，不会改变状态。
- 这个接口既能确认预约成功，也明显带有签到页状态信息。
- 当前样本未发现独立的真实签到 mutation。
