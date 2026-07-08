# 212 自习室 libLayout

## 作用

进入 `212自习室` 后获取座位图，用于确认 `seatKey`、`seat_status`、座位编号和布局。

## URL

```text
POST https://wechat.v2.traceint.com/index.php/graphql/
```

## operationName

`libLayout`

## Request Headers

- `content-type: application/json`
- `app-version: 2.2.9`
- `origin: https://web.traceint.com`
- `referer: https://web.traceint.com/`
- `user-agent: Mozilla/5.0 ... WindowsWechat ...`
- `cookie: FROM_TYPE=weixiao; v=5.5; FROM_CODE=<REDACTED>; <REDACTED_COOKIE_PARTS>`

## Request Body

```json
{
  "operationName": "libLayout",
  "query": "query libLayout($libId: Int, $libType: Int) {\n userAuth {\n reserve {\n libs(libType: $libType, libId: $libId) {\n lib_id\n is_open\n lib_floor\n lib_name\n lib_type\n lib_layout {\n seats_total\n seats_booking\n seats_used\n max_x\n max_y\n seats {\n x\n y\n key\n type\n name\n seat_status\n status\n }\n }\n }\n }\n }\n}",
  "variables": {
    "libId": 126500
  }
}
```

## Response Body

> 原始样本里的 `seats` 列表非常长，这里保留关键结构和代表性座位；原始来源为 `图书馆接口（2）.md` 中 `libLayout` 区块。

```json
{
  "data": {
    "userAuth": {
      "reserve": {
        "libs": [
          {
            "lib_id": 126500,
            "is_open": true,
            "lib_floor": "二楼",
            "lib_name": "212自习室",
            "lib_type": 0,
            "lib_layout": {
              "seats_total": 400,
              "seats_booking": 0,
              "seats_used": 0,
              "max_x": 34,
              "max_y": 70,
              "seats": [
                {
                  "x": 14,
                  "y": 1,
                  "key": "1,14",
                  "type": 7,
                  "name": null,
                  "seat_status": 0,
                  "status": false
                },
                {
                  "x": 26,
                  "y": 7,
                  "key": "7,26",
                  "type": 1,
                  "name": "399",
                  "seat_status": 1,
                  "status": false
                },
                {
                  "x": 24,
                  "y": 15,
                  "key": "15,24",
                  "type": 1,
                  "name": "341",
                  "seat_status": 1,
                  "status": false
                },
                {
                  "x": 16,
                  "y": 66,
                  "key": "66,16",
                  "type": 7,
                  "name": null,
                  "seat_status": 0,
                  "status": false
                }
              ]
            }
          }
        ]
      }
    }
  }
}
```

## 关键字段

- `data.userAuth.reserve.libs[0].lib_id`
- `lib_layout.seats_total`
- `lib_layout.max_x`
- `lib_layout.max_y`
- `seats[].key`
- `seats[].name`
- `seats[].seat_status`
- `seats[].type`

## 对旧项目可能的映射

- 旧项目 `Activity.libLayout`
- `get_libLayout`
- `reserve_floor`
- `pass_reserve`
- `seatKey` 的来源

## 备注

- 查询接口，不会改变状态。
- 当前样本中 `seatKey = "15,24"` 对应的座位号可从后续预约确认接口看出是 `341`。
