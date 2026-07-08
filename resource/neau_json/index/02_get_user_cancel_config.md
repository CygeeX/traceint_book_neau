# 退座配置 getUserCancleConfig

## 作用

查询当前学校是否启用/要求某类退座校验配置。

## URL

```text
POST https://wechat.v2.traceint.com/index.php/graphql/
```

## operationName

`getUserCancleConfig`

## Request Headers

- `content-type: application/json`
- `app-version: 2.2.9`
- `origin: https://web.traceint.com`
- `referer: https://web.traceint.com/`
- `user-agent: Mozilla/5.0 ... WindowsWechat ...`
- `cookie: FROM_TYPE=weixiao; v=5.5; <REDACTED_COOKIE_PARTS>`

## Request Body

```json
{
  "operationName": "getUserCancleConfig",
  "query": "query getUserCancleConfig {\n userAuth {\n user {\n holdValidate: getSchConfig(fields: \"hold_validate\", extra: true)\n }\n }\n}",
  "variables": {}
}
```

## Response Body

```json
{
  "data": {
    "userAuth": {
      "user": {
        "holdValidate": "true"
      }
    }
  }
}
```

## 关键字段

- `data.userAuth.user.holdValidate`

## 对旧项目可能的映射

- `resource/old_json/login/13.txt`
- 退座前的学校配置查询

## 备注

- 查询接口，不会改变状态。
- 这个接口在旧项目运行时代码里没有直接封装，但旧抓包里出现过。
