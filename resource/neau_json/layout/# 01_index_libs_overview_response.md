# 01_index_libs_overview_response

## 作用

首页状态接口，用于获取：

- 当前 cookie 是否有效
- 当前用户是否已有预约
- 学校所有自习室概览
- 每个自习室的开放状态、剩余座位数、开放时间
- 当前预约信息 reserve

## 请求体

```json
{
  "operationName": "index",
  "query": "query index($pos: String!, $param: [hash]) { ... }",
  "variables": {
    "pos": "App-首页"
  }
}
```

## 关键请求头

```txt
:method: POST
:authority: wechat.v2.traceint.com
:path: /index.php/graphql/
:scheme: https
content-length: 756
user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/132.0.0.0 Safari/537.36 NetType/WIFI MicroMessenger/7.0.20.1781(0x6700143B) WindowsWechat(0x63090a13) UnifiedPCWindowsWechat(0xf2541b18) XWEB/20079 Flue
content-type: application/json
app-version: 2.2.9
accept: */*
origin: https://web.traceint.com
sec-fetch-site: same-site
sec-fetch-mode: cors
sec-fetch-dest: empty
referer: https://web.traceint.com/
accept-encoding: gzip, deflate, br
accept-language: zh-CN,zh;q=0.9
cookie: FROM_TYPE=weixiao
cookie: v=5.5
cookie: FROM_CODE=WwsCBVIBBgs%3D
cookie: Hm_lvt_7ecd21a13263a714793f376c18038a87=1783410004,1783410405,1783412237,1783413967
cookie: HMACCOUNT=6BE039FDE396071E
cookie: wechatSESS_ID=fe6e9ff95a9da4daa04779bee0847fbb00392643f6c7015f
cookie: Authorization=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJ1c2VySWQiOjQ1NDA5NTc2LCJzY2hJZCI6MjAzODAsImV4cGlyZUF0IjoxNzgzNDg3NzcwLCJ0YWciOiJjb29raWUtOTFkOSJ9.SNBp7aPZ76npIszsiH6NETM0d01iEP5Zv-E_fKK-hvtn5lXX3PJtZMPRTA6ptM10hPmM1BCjxed7lb49-8sMiNveP7RzGpP5Bf8eyImfWMRYrOX_q9jh7i8Pq0SYHOW8KVNghzLnMQzu37JJhKReM9hYHELtnkacGEqanou5DH9SOocMq4F8D9t8wWWnXUBhm5PNNss_n4T5O_HA7SVLRhI5G6ar_oUWCnNSXKcIGGvZhe-BAY2-YmSxR6F5LzWLUYy9nS9ayCz_W1-r-nHNwUnMbvtsbyVuzUcl4CHzxYD4OQAvOI7gdsOV2Z0hobDZM0bJNd2P8sCGyQl9ocNubg
cookie: Hm_lpvt_7ecd21a13263a714793f376c18038a87=1783480575
cookie: SERVERID=d3936289adfff6c3874a2579058ac651|1783480595|1783480561
priority: u=1, i
```


## 响应关键路径

```txt
data.userAuth.reserve.libs
```

表示学校自习室列表。

```txt
data.userAuth.reserve.reserve
```

表示当前用户是否已有预约。

如果是：

```json
"reserve": null
```

说明当前没有预约座位。





## 关键字段

```txt
lib_id：自习室 ID，后续查座位图 / 预约座位会用
lib_floor：楼层
lib_name：自习室名称
is_open：是否开放
lib_rt.seats_total：总座位数
lib_rt.seats_used：已使用座位数
lib_rt.seats_booking：已预约座位数
lib_rt.seats_has：剩余座位数
open_time_str：开放时间
close_time_str：关闭时间
advance_booking：可提前多久预约
```

## 样本响应

```json
{
  "data": {
    "userAuth": {
      "reserve": {
        "libs": [
          {
            "lib_id": 126493,
            "lib_floor": "一楼",
            "is_open": false,
            "lib_name": "140自习室",
            "lib_type": 0,
            "lib_group_id": 0,
            "lib_comment": "",
            "lib_rt": {
              "seats_total": 196,
              "seats_used": 0,
              "seats_booking": 0,
              "seats_has": 196,
              "reserve_ttl": 60,
              "open_time": 0,
              "open_time_str": "待定",
              "close_time": "0",
              "close_time_str": " 8:00",
              "advance_booking": "0秒"
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
              "seats_used": 174,
              "seats_booking": 7,
              "seats_has": 219,
              "reserve_ttl": 1800,
              "open_time": 1783461600,
              "open_time_str": " 6:00",
              "close_time": "1783519200",
              "close_time_str": " 22:00",
              "advance_booking": "1小时"
            }
          },
          {
            "lib_id": 126507,
            "lib_floor": "三楼",
            "is_open": true,
            "lib_name": "325自习室",
            "lib_type": 0,
            "lib_group_id": 0,
            "lib_comment": "",
            "lib_rt": {
              "seats_total": 400,
              "seats_used": 300,
              "seats_booking": 5,
              "seats_has": 95,
              "reserve_ttl": 1800,
              "open_time": 1783461600,
              "open_time_str": " 6:00",
              "close_time": "1783519200",
              "close_time_str": " 22:00",
              "advance_booking": "1小时"
            }
          },
          {
            "lib_id": 126514,
            "lib_floor": "三楼",
            "is_open": false,
            "lib_name": "334自习室",
            "lib_type": 0,
            "lib_group_id": 0,
            "lib_comment": "",
            "lib_rt": {
              "seats_total": 260,
              "seats_used": 0,
              "seats_booking": 0,
              "seats_has": 260,
              "reserve_ttl": 60,
              "open_time": 0,
              "open_time_str": "待定",
              "close_time": "0",
              "close_time_str": " 8:00",
              "advance_booking": "0秒"
            }
          },
          {
            "lib_id": 126521,
            "lib_floor": "四楼",
            "is_open": false,
            "lib_name": "413自习室",
            "lib_type": 0,
            "lib_group_id": 0,
            "lib_comment": "",
            "lib_rt": {
              "seats_total": 400,
              "seats_used": 0,
              "seats_booking": 0,
              "seats_has": 400,
              "reserve_ttl": 60,
              "open_time": 0,
              "open_time_str": "待定",
              "close_time": "0",
              "close_time_str": " 8:00",
              "advance_booking": "0秒"
            }
          },
          {
            "lib_id": 126528,
            "lib_floor": "四楼",
            "is_open": false,
            "lib_name": "419自习室",
            "lib_type": 0,
            "lib_group_id": 0,
            "lib_comment": "",
            "lib_rt": {
              "seats_total": 96,
              "seats_used": 0,
              "seats_booking": 0,
              "seats_has": 96,
              "reserve_ttl": 60,
              "open_time": 0,
              "open_time_str": "待定",
              "close_time": "0",
              "close_time_str": " 8:00",
              "advance_booking": "0秒"
            }
          },
          {
            "lib_id": 126535,
            "lib_floor": "四楼",
            "is_open": false,
            "lib_name": "423自习室",
            "lib_type": 0,
            "lib_group_id": 0,
            "lib_comment": "",
            "lib_rt": {
              "seats_total": 260,
              "seats_used": 0,
              "seats_booking": 0,
              "seats_has": 260,
              "reserve_ttl": 60,
              "open_time": 0,
              "open_time_str": "待定",
              "close_time": "0",
              "close_time_str": " 8:00",
              "advance_booking": "0秒"
            }
          },
          {
            "lib_id": 126542,
            "lib_floor": "五楼",
            "is_open": false,
            "lib_name": "515自习室",
            "lib_type": 0,
            "lib_group_id": 0,
            "lib_comment": "",
            "lib_rt": {
              "seats_total": 400,
              "seats_used": 0,
              "seats_booking": 0,
              "seats_has": 400,
              "reserve_ttl": 60,
              "open_time": 0,
              "open_time_str": "待定",
              "close_time": "0",
              "close_time_str": " 8:00",
              "advance_booking": "0秒"
            }
          },
          {
            "lib_id": 126549,
            "lib_floor": "五楼",
            "is_open": false,
            "lib_name": "五楼走廊自习区",
            "lib_type": 0,
            "lib_group_id": 0,
            "lib_comment": "",
            "lib_rt": {
              "seats_total": 92,
              "seats_used": 0,
              "seats_booking": 0,
              "seats_has": 92,
              "reserve_ttl": 60,
              "open_time": 0,
              "open_time_str": "待定",
              "close_time": "0",
              "close_time_str": " 8:00",
              "advance_booking": "0秒"
            }
          },
          {
            "lib_id": 126556,
            "lib_floor": "五楼",
            "is_open": false,
            "lib_name": "521自习室",
            "lib_type": 0,
            "lib_group_id": 0,
            "lib_comment": "",
            "lib_rt": {
              "seats_total": 96,
              "seats_used": 0,
              "seats_booking": 0,
              "seats_has": 96,
              "reserve_ttl": 60,
              "open_time": 0,
              "open_time_str": "待定",
              "close_time": "0",
              "close_time_str": " 8:00",
              "advance_booking": "0秒"
            }
          },
          {
            "lib_id": 126563,
            "lib_floor": "五楼",
            "is_open": false,
            "lib_name": "524自习室",
            "lib_type": 0,
            "lib_group_id": 0,
            "lib_comment": "",
            "lib_rt": {
              "seats_total": 212,
              "seats_used": 0,
              "seats_booking": 0,
              "seats_has": 212,
              "reserve_ttl": 60,
              "open_time": 0,
              "open_time_str": "待定",
              "close_time": "0",
              "close_time_str": " 8:00",
              "advance_booking": "0秒"
            }
          },
          {
            "lib_id": 126765,
            "lib_floor": "三楼",
            "is_open": false,
            "lib_name": "棘园三楼教工餐厅自习室",
            "lib_type": 0,
            "lib_group_id": 1745,
            "lib_comment": "",
            "lib_rt": {
              "seats_total": 120,
              "seats_used": 0,
              "seats_booking": 0,
              "seats_has": 120,
              "reserve_ttl": 1800,
              "open_time": 1783499400,
              "open_time_str": " 16:30",
              "close_time": "1783515600",
              "close_time_str": " 21:00",
              "advance_booking": "1小时"
            }
          }
        ],
        "libGroups": [
          {
            "id": 1745,
            "group_name": "棘园三楼教工餐厅自习室"
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