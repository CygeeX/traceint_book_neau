# 提交预约 reserueSeat

## 作用

选中座位后提交预约。

## URL

```text
POST https://wechat.v2.traceint.com/index.php/graphql/
```


## 请求头

- `content-type: application/json`
- `app-version: 2.2.9`
- `origin: https://web.traceint.com`
- `referer: https://web.traceint.com/`
- `user-agent: Mozilla/5.0 ... WindowsWechat ...`
- `cookie: <REDACTED_COOKIE_PARTS>`

## 请求体

```json
{
  "operationName": "reserueSeat",
  "query": "mutation reserueSeat($libId: Int!, $seatKey: String!, $captchaCode: String, $captcha: String!) {\n userAuth {\n reserve {\n reserueSeat(\n libId: $libId\n seatKey: $seatKey\n captchaCode: $captchaCode\n captcha: $captcha\n )\n }\n }\n}",
  "variables": {
    "seatKey": "15,24",
    "libId": 126500,
    "captchaCode": "",
    "captcha": ""
  }
}
```

## Response Body

```json
{
  "data": {
    "userAuth": {
      "reserve": {
        "reserueSeat": true
      }
    }
  }
}
```

## 关键字段

```txt
operationName
  固定为 reserueSeat。

query
  GraphQL mutation 语句，mutation 名和返回字段都叫 reserueSeat。

variables.libId
  房间/阅览室/楼层对应的 lib_id。
  例如：126507 表示 325自习室。

variables.seatKey
  座位 key。
  东北农业大学这里的 seatKey 不是单纯的座位号，而是类似 "15,18" 这样的坐标形式。
  例如："15,18" 最终对应座位名 338。

variables.captchaCode
  验证码 code。
  当前样本中为空字符串。

variables.captcha
  验证码字段。
  GraphQL 中定义为 String!，表示必传。
  即使当前不需要验证码，也要传空字符串。

data.userAuth.reserve.reserueSeat
  true 表示预约成功。
  false 或 errors 表示预约失败。
```

## 对旧项目可能的映射

- 旧项目 `reserveSeat`
- `pass_reserve`
- `seatKey` 提交动作

## 备注

- 这是 mutation，会改变预约状态。
- 真实接口拼写是 `reserueSeat`，不要改成 `reserveSeat`。
