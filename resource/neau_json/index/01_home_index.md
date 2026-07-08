# 首页 index

## 作用

获取首页总状态、当前登录态、当前预约、`getSToken`、常用座位、当前用户信息。

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
- `cookie: FROM_TYPE=weixiao; v=5.5; <REDACTED_COOKIE_PARTS>`

## Request Body

```json
{
  "operationName": "index",
  "query": "query index($pos: String!, $param: [hash]) {\n userAuth {\n oftenseat {\n list {\n id\n info\n lib_id\n seat_key\n status\n }\n }\n message {\n new(from: \"system\") {\n has\n from_user\n title\n num\n }\n indexMsg {\n message_id\n title\n content\n isread\n isused\n from_user\n create_time\n }\n }\n reserve {\n reserve {\n token\n status\n user_id\n user_nick\n sch_name\n lib_id\n lib_name\n lib_floor\n seat_key\n seat_name\n date\n exp_date\n exp_date_str\n validate_date\n hold_date\n diff\n diff_str\n mark_source\n isRecordUser\n isChooseSeat\n isRecord\n mistakeNum\n openTime\n threshold\n daynum\n mistakeNum\n closeTime\n timerange\n forbidQrValid\n renewTimeNext\n forbidRenewTime\n forbidWechatCancle\n }\n getSToken\n }\n currentUser {\n user_id\n user_nick\n user_mobile\n user_sex\n user_sch_id\n user_sch\n user_last_login\n user_avatar(size: MIDDLE)\n user_adate\n user_student_no\n user_student_name\n area_name\n user_deny {\n deny_deadline\n deny_reason\n }\n sch {\n sch_id\n sch_name\n activityUrl\n isShowCommon\n isBusy\n }\n subscribe_remind\n }\n record {\n recordRegInfo {\n reg_start\n reg_end\n }\n recordShortlistInfo\n }\n }\n ad(pos: $pos, param: $param) {\n name\n pic\n url\n }\n homeIconAd: ad(pos: \"home-icon\", param: $param) {\n name\n pic\n url\n }\n}",
  "variables": {
    "pos": "App-首页"
  }
}
```

## Response Body

```json
{
  "data": {
    "userAuth": {
      "oftenseat": {
        "list": [
          {
            "id": 18291079,
            "info": "212自习室 399号",
            "lib_id": 126500,
            "seat_key": "7,26",
            "status": 0
          },
          {
            "id": 18291072,
            "info": "212自习室 2号",
            "lib_id": 126500,
            "seat_key": "61,26",
            "status": 0
          }
        ]
      },
      "message": {
        "new": {
          "has": false,
          "from_user": null,
          "title": null,
          "num": 1
        },
        "indexMsg": null
      },
      "reserve": {
        "reserve": null,
        "getSToken": "<REDACTED_STOKEN>"
      },
      "currentUser": {
        "user_id": 45409576,
        "user_nick": "<REDACTED_NICKNAME>",
        "user_mobile": "<REDACTED_PHONE>",
        "user_sex": 0,
        "user_sch_id": 20380,
        "user_sch": "东北农业大学",
        "user_last_login": 1782981862,
        "user_avatar": "https://static.wechat.v2.traceint.com/data/attachment/no_pic.jpg",
        "user_adate": 1726550590,
        "user_student_no": "<REDACTED_STUDENT_NO>",
        "user_student_name": "<REDACTED_NAME>",
        "area_name": null,
        "user_deny": {
          "deny_deadline": null,
          "deny_reason": null
        },
        "sch": {
          "sch_id": 20380,
          "sch_name": "东北农业大学",
          "activityUrl": null,
          "isShowCommon": true,
          "isBusy": true
        },
        "subscribe_remind": true
      },
      "record": {
        "recordRegInfo": {
          "reg_start": "0",
          "reg_end": "0"
        },
        "recordShortlistInfo": ""
      }
    },
    "ad": [
      {
        "name": "广告位示例",
        "pic": "http://wechat.v2.traceint.com/data/attachment/2026-05-12/pre_xxx.png",
        "url": "http://wechat.v2.traceint.com/index.php/click?...&token=<REDACTED_AD_TOKEN>"
      }
    ],
    "homeIconAd": []
  }
}
```

## 关键字段

- `data.userAuth.currentUser`
- `data.userAuth.reserve.reserve`
- `data.userAuth.reserve.getSToken`
- `data.userAuth.oftenseat.list`
- `data.userAuth.currentUser.sch.sch_id`

## 对旧项目可能的映射

- 旧项目 `Activity.index`
- `have_seat`
- `verify_cookie`
- `get_SToken`

## 备注

- 这是查询接口，不会改变预约状态。
- 当前样本里 `reserve.reserve = null`，说明首页时尚未有预约。
