# 退座 reserveCancle

## 作用

提交退座请求。

## URL

```text
POST https://wechat.v2.traceint.com/index.php/graphql/
```

## operationName

`reserveCancle`

## Request Headers

- `content-type: application/json`
- `app-version: 2.2.9`
- `origin: https://web.traceint.com`
- `referer: https://web.traceint.com/`
- `user-agent: Mozilla/5.0 ... WindowsWechat ...`
- `cookie: v=5.5; <REDACTED_COOKIE_PARTS>`

## Request Body

```json
{
  "operationName": "reserveCancle",
  "query": "mutation reserveCancle($sToken: String!) {\n userAuth {\n reserve {\n reserveCancle(sToken: $sToken) {\n timerange\n img\n hours\n mins\n per\n }\n }\n }\n}",
  "variables": {
    "sToken": "<REDACTED_STOKEN>"
  }
}
```

## Response Body

```json
{
  "errors": [
    {
      "msg": "退座成功",
      "code": 1
    }
  ],
  "data": {
    "userAuth": {
      "reserve": {
        "reserveCancle": null
      }
    }
  }
}
```

## 关键字段

- `variables.sToken`
- `errors[].msg`
- `errors[].code`
- `data.userAuth.reserve.reserveCancle`

## 对旧项目可能的映射

- 旧项目 `get_SToken`
- 旧项目 `pass_reserveCancle`
- 旧抓包 `resource/old_json/cancel/cancel.txt`

## 备注

- 这是 mutation，会改变预约状态。
- 退座成功信息可能出现在 `errors` 里，而不是 `data.userAuth.reserve.reserveCancle`。
- 这和旧项目代码里“只判断有没有 `error` 键”的做法不完全一致。
