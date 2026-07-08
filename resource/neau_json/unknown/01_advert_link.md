# advertLink

## 作用

预约动作后出现的辅助广告链接查询，不属于核心选座/退座流程。

## URL

```text
POST https://wechat.v2.traceint.com/index.php/graphql/
```

## operationName

`advertLink`

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
  "operationName": "advertLink",
  "query": "query advertLink($type: String!) {\n userAuth {\n user {\n advertLink(type: $type)\n }\n }\n}",
  "variables": {
    "type": "reserve"
  }
}
```

## Response Body

```json
{
  "data": {
    "userAuth": {
      "user": {
        "advertLink": ""
      }
    }
  }
}
```

## 关键字段

- `variables.type`
- `data.userAuth.user.advertLink`

## 对旧项目可能的映射

- 暂未发现旧项目运行时代码中直接依赖该接口

## 备注

- 查询接口，不会改变状态。
- 当前先放入 `unknown/`，后续如果确认属于固定页面行为，再决定是否移动。
