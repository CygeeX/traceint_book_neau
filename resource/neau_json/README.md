# neau_json

这些样本来自我学校微信小程序/网页端抓包整理，按用户动作和 `operationName` 分类。

## 统一接口 URL

```text
https://wechat.v2.traceint.com/index.php/graphql/
```

## 主要流程

```text
index
-> getUserCancleConfig
-> list
-> libLayout
-> reserueSeat
-> after reserve index
-> reserveCancle
-> after cancel index
```

## 目录说明

- `login/`：当前这份新抓包里没有独立登录/OAuth 样本，暂时只有占位说明。
- `index/`：首页总状态、登录态、当前预约、`getSToken`、退座配置。
- `list/`：自习室/教室列表，主要用于确认 `lib_id / libId`。
- `layout/`：座位图，主要用于确认 `seatKey`、`seat_status`、座位布局。
- `reserve/`：提交预约、预约后确认状态。
- `cancel/`：退座、退座后刷新首页确认。
- `sign/`：当前未抓到真实签到提交接口，只有占位说明。
- `unknown/`：暂时无法稳定归类的辅助接口。

## 关键字段

- `cookie`：请求认证信息，样本里只保留结构，真实值已脱敏。
- `getSToken`：首页 `index` 返回，退座时常作为 `sToken` 来源。
- `sToken`：退座请求 `reserveCancle` 的核心参数。
- `token`：预约成功后 `reserve.reserve.token`，用于标识当前预约。
- `lib_id / libId`：教室/自习室 ID。
- `seat_key / seatKey`：座位键，例如 `"15,24"`。
- `seat_status`：座位状态，常见 `1` 表示可预约，`0` 表示非座位/不可用。

## 安全说明

- 样本里的 `cookie` 必须脱敏。
- 不要提交真实 `cookie`。
- 不要把手机号、学号、姓名、openid、unionid 写进样本。
- 本目录中的 `token / getSToken / sToken` 也已做保守脱敏。

## 当前未确认事项

- 真实签到提交接口是否已抓到。
- 预约失败响应样本是否已抓到。
- 验证码触发时的响应是否已抓到。

## 备注

- 当前抓包里预约提交接口的真实拼写是 `reserueSeat`，不要擅自改成 `reserveSeat`。
- 退座成功信息可能出现在 `errors` 里，而不是 `data.userAuth.reserve.reserveCancle`。
- `unknown/01_advert_link.md` 是预约动作后出现的辅助广告接口，不属于核心预约流程。
