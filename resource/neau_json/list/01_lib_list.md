# 自习室列表 list

## 作用

进入选座页后，查询全部可用教室/自习室，用于确认 `lib_id / libId`。

## URL

```text
POST https://wechat.v2.traceint.com/index.php/graphql/
```

## operationName

`list`

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
  "operationName": "list",
  "query": "query list {\n userAuth {\n reserve {\n libs(libType: -1) {\n lib_id\n lib_floor\n is_open\n lib_name\n lib_type\n lib_group_id\n lib_comment\n lib_rt {\n seats_total\n seats_used\n seats_booking\n seats_has\n reserve_ttl\n open_time\n open_time_str\n close_time\n close_time_str\n advance_booking\n }\n }\n libGroups {\n id\n group_name\n }\n reserve {\n isRecordUser\n }\n }\n record {\n libs {\n lib_id\n lib_floor\n is_open\n lib_name\n lib_type\n lib_group_id\n lib_comment\n lib_color_name\n lib_rt {\n seats_total\n seats_used\n seats_booking\n seats_has\n reserve_ttl\n open_time\n open_time_str\n close_time\n close_time_str\n advance_booking\n }\n }\n }\n rule {\n signRule\n }\n protocol {\n content\n }\n }\n}"
}
```

## Response Body

```json
{
  "data": {
    "userAuth": {
      "reserve": {
        "libs": [
          {
            "lib_id": 126493,
            "lib_floor": "一楼",
            "is_open": true,
            "lib_name": "140自习室",
            "lib_type": 0,
            "lib_group_id": 0,
            "lib_comment": "",
            "lib_rt": {
              "seats_total": 196,
              "seats_used": 0,
              "seats_booking": 0,
              "seats_has": 196,
              "reserve_ttl": 1800,
              "open_time": 1782943200,
              "open_time_str": " 6:00",
              "close_time": "1783000800",
              "close_time_str": " 22:00",
              "advance_booking": "1小时"
            }
          },
          {
            "lib_id": 126500,
            "lib_floor": "二楼",
            "is_open": true,
            "lib_name": "212自习室",
            "lib_type": 0,
            "lib_group_id": 0,
            "lib_comment": "",
            "lib_rt": {
              "seats_total": 400,
              "seats_used": 0,
              "seats_booking": 0,
              "seats_has": 400,
              "reserve_ttl": 1800,
              "open_time": 1782943200,
              "open_time_str": " 6:00",
              "close_time": "1783000800",
              "close_time_str": " 22:00",
              "advance_booking": "1小时"
            }
          },
          {
            "lib_id": 126507,
            "lib_floor": "三楼",
            "is_open": true,
            "lib_name": "325自习室",
            "lib_type": 0
          },
          {
            "lib_id": 126514,
            "lib_floor": "三楼",
            "is_open": true,
            "lib_name": "334自习室",
            "lib_type": 0
          },
          {
            "lib_id": 126521,
            "lib_floor": "四楼",
            "is_open": true,
            "lib_name": "413自习室",
            "lib_type": 0
          },
          {
            "lib_id": 126528,
            "lib_floor": "四楼",
            "is_open": true,
            "lib_name": "419自习室",
            "lib_type": 0
          },
          {
            "lib_id": 126535,
            "lib_floor": "四楼",
            "is_open": true,
            "lib_name": "423自习室",
            "lib_type": 0
          },
          {
            "lib_id": 126542,
            "lib_floor": "五楼",
            "is_open": true,
            "lib_name": "515自习室",
            "lib_type": 0
          },
          {
            "lib_id": 126549,
            "lib_floor": "五楼",
            "is_open": true,
            "lib_name": "五楼走廊自习区",
            "lib_type": 0
          },
          {
            "lib_id": 126556,
            "lib_floor": "五楼",
            "is_open": true,
            "lib_name": "521自习室",
            "lib_type": 0
          },
          {
            "lib_id": 126563,
            "lib_floor": "五楼",
            "is_open": true,
            "lib_name": "524自习室",
            "lib_type": 0
          },
          {
            "lib_id": 126765,
            "lib_floor": "三楼",
            "is_open": false,
            "lib_name": "棉园三楼教工餐厅自习室",
            "lib_type": 0,
            "lib_group_id": 1745
          }
        ],
        "libGroups": [
          {
            "id": 1745,
            "group_name": "棉园三楼教工餐厅自习室"
          }
        ],
        "reserve": null
      },
      "record": {
        "libs": []
      },
      "rule": {
        "signRule": null
      },
      "protocol": {
        "content": ""
      }
    }
  }
}
```

## 关键字段

- `data.userAuth.reserve.libs[].lib_id`
- `lib_name`
- `lib_floor`
- `is_open`
- `lib_rt`

## 对旧项目可能的映射

- 旧抓包 `resource/old_json/book/all.txt`
- `get_lib_id` 的动态来源
- 新学校应优先用这里替代旧项目硬编码楼层映射

## 备注

- 查询接口，不会改变状态。
- 新学校可以直接从这里提取 `lib_id`，不应继续沿用旧项目 `floor -> lib_id` 硬编码。
