# 01_325_lib_layout_response

## 作用

获取三楼 325 自习室的座位布局信息。

该接口会返回：

```txt
1. 自习室基本信息
2. 座位总数
3. 已预约座位数
4. 已使用座位数
5. 座位图最大坐标
6. 每个座位或布局元素的坐标、编号、key、状态
```

---

## 请求信息

### 请求方法

```txt
POST
```

### 请求 URL

```txt
https://wechat.v2.traceint.com/index.php/graphql/
```

---

## 请求体

```json
{
  "operationName": "libLayout",
  "query": "query libLayout($libId: Int, $libType: Int) {\n userAuth {\n reserve {\n libs(libType: $libType, libId: $libId) {\n lib_id\n is_open\n lib_floor\n lib_name\n lib_type\n lib_layout {\n seats_total\n seats_booking\n seats_used\n max_x\n max_y\n seats {\n x\n y\n key\n type\n name\n seat_status\n status\n }\n }\n }\n }\n }\n}",
  "variables": {
    "libId": 126507
  }
}
```

---

## 关键请求头

```txt
:method: POST
:authority: wechat.v2.traceint.com
:path: /index.php/graphql/
:scheme: https
content-type: application/json
app-version: 2.2.9
accept: */*
origin: https://web.traceint.com
referer: https://web.traceint.com/
accept-language: zh-CN,zh;q=0.9
```


## 响应关键路径

```txt
data.userAuth.reserve.libs
```
含义：返回的自习室列表。

---

```txt
data.userAuth.reserve.libs[0]
```
含义：当前查询到的 325 自习室信息。

---

```txt
data.userAuth.reserve.libs[0].lib_layout
```
含义：325 自习室的座位布局信息。

---

```txt
data.userAuth.reserve.libs[0].lib_layout.seats
```
含义：325 自习室里的座位/布局元素数组。

---

## 关键字段

### 自习室字段

```txt
lib_id：自习室 ID
is_open：是否开放
lib_floor：所在楼层
lib_name：自习室名称
lib_type：自习室类型
```

本样本中：

```json
{
  "lib_id": 126507,
  "is_open": true,
  "lib_floor": "三楼",
  "lib_name": "325自习室",
  "lib_type": 0
}
```

---

### 座位布局字段

```txt
seats_total：总座位数
seats_booking：已预约座位数
seats_used：已使用座位数
max_x：座位图最大 x 坐标
max_y：座位图最大 y 坐标
seats：座位/布局元素数组
```

本样本中：

```json
{
  "seats_total": 400,
  "seats_booking": 4,
  "seats_used": 303,
  "max_x": 34,
  "max_y": 70
}
```

---

### seats 单项字段

每一项结构示例：

```json
{
  "x": 18,
  "y": 7,
  "key": "7,18",
  "type": 1,
  "name": "394",
  "seat_status": 1,
  "status": false
}
```

字段含义：

```txt
x：横坐标
y：纵坐标
key：座位 key
type：布局元素类型
name：座位号
seat_status：座位状态
status：状态布尔值
```

---

## 座位状态初步记录

根据样本观察：

```txt
type = 1 且 name 不为 null：真实座位
name = null：非具体座位，可能是桌子、过道、墙体或其他布局元素
seat_status = 1：可预约座位
seat_status = 0：非可预约元素
seat_status = 2：待确认状态，可能是预约/占用相关
seat_status = 3：待确认状态，可能是使用中/占用相关
seat_status = 4：待确认状态，可能是不可用/已预约相关
```


## 可预约座位样例

```json
{
  "x": 18,
  "y": 7,
  "key": "7,18",
  "type": 1,
  "name": "394",
  "seat_status": 1,
  "status": false
}
```

含义：

```txt
座位号：394
座位 key：7,18
所属自习室 lib_id：126507
当前状态：可预约
```

---

## 非座位元素样例

```json
{
  "x": 14,
  "y": 1,
  "key": "1,14",
  "type": 7,
  "name": null,
  "seat_status": 0,
  "status": false
}
```

含义：

```txt
该元素不是具体可预约座位。
```

---

## 样本响应

```json
# 01_325_lib_layout_response

## 作用

获取三楼 325 自习室的座位布局信息。

该接口会返回：

```txt
1. 自习室基本信息
2. 座位总数
3. 已预约座位数
4. 已使用座位数
5. 座位图最大坐标
6. 每个座位或布局元素的坐标、编号、key、状态
```

---

## 请求信息

### 请求方法

```txt
POST
```

### 请求 URL

```txt
https://wechat.v2.traceint.com/index.php/graphql/
```

---

## 请求体

```json
{
  "operationName": "libLayout",
  "query": "query libLayout($libId: Int, $libType: Int) {\n userAuth {\n reserve {\n libs(libType: $libType, libId: $libId) {\n lib_id\n is_open\n lib_floor\n lib_name\n lib_type\n lib_layout {\n seats_total\n seats_booking\n seats_used\n max_x\n max_y\n seats {\n x\n y\n key\n type\n name\n seat_status\n status\n }\n }\n }\n }\n }\n}",
  "variables": {
    "libId": 126507
  }
}
```

---

## 关键请求头

```txt
:method: POST
:authority: wechat.v2.traceint.com
:path: /index.php/graphql/
:scheme: https
content-type: application/json
app-version: 2.2.9
accept: */*
origin: https://web.traceint.com
referer: https://web.traceint.com/
accept-language: zh-CN,zh;q=0.9
```

### Cookie 关键字段

```txt
FROM_TYPE=weixiao
v=5.5
FROM_CODE=...
wechatSESS_ID=...
Authorization=...
SERVERID=...
```

注意：保存到项目文档时，完整 Cookie、Authorization、wechatSESS_ID 建议脱敏。

示例：

```txt
Cookie: FROM_TYPE=weixiao; v=5.5; FROM_CODE=...; wechatSESS_ID=***; Authorization=***; SERVERID=***
```

---

## 响应关键路径

```txt
data.userAuth.reserve.libs
```

含义：返回的自习室列表。

---

```txt
data.userAuth.reserve.libs[0]
```

含义：当前查询到的 325 自习室信息。

---

```txt
data.userAuth.reserve.libs[0].lib_layout
```

含义：325 自习室的座位布局信息。

---

```txt
data.userAuth.reserve.libs[0].lib_layout.seats
```

含义：325 自习室里的座位/布局元素数组。

---

## 关键字段

### 自习室字段

```txt
lib_id：自习室 ID
is_open：是否开放
lib_floor：所在楼层
lib_name：自习室名称
lib_type：自习室类型
```

本样本中：

```json
{
  "lib_id": 126507,
  "is_open": true,
  "lib_floor": "三楼",
  "lib_name": "325自习室",
  "lib_type": 0
}
```

---

### 座位布局字段

```txt
seats_total：总座位数
seats_booking：已预约座位数
seats_used：已使用座位数
max_x：座位图最大 x 坐标
max_y：座位图最大 y 坐标
seats：座位/布局元素数组
```

本样本中：

```json
{
  "seats_total": 400,
  "seats_booking": 4,
  "seats_used": 303,
  "max_x": 34,
  "max_y": 70
}
```

---

### seats 单项字段

每一项结构示例：

```json
{
  "x": 18,
  "y": 7,
  "key": "7,18",
  "type": 1,
  "name": "394",
  "seat_status": 1,
  "status": false
}
```

字段含义：

```txt
x：横坐标
y：纵坐标
key：座位 key
type：布局元素类型
name：座位号
seat_status：座位状态
status：状态布尔值
```

---

## 座位状态初步记录

根据样本观察：

```txt
type = 1 且 name 不为 null：真实座位
name = null：非具体座位，可能是桌子、过道、墙体或其他布局元素
seat_status = 1：可预约座位
seat_status = 0：非可预约元素
seat_status = 2：待确认状态，可能是预约/占用相关
seat_status = 3：待确认状态，可能是使用中/占用相关
seat_status = 4：待确认状态，可能是不可用/已预约相关
```

当前代码中可以暂时按下面条件筛选可预约座位：

```python
seat["type"] == 1 and seat["name"] is not None and seat["seat_status"] == 1
```

---

## 可预约座位样例

```json
{
  "x": 18,
  "y": 7,
  "key": "7,18",
  "type": 1,
  "name": "394",
  "seat_status": 1,
  "status": false
}
```

含义：

```txt
座位号：394
座位 key：7,18
所属自习室 lib_id：126507
当前状态：可预约
```

---

## 非座位元素样例

```json
{
  "x": 14,
  "y": 1,
  "key": "1,14",
  "type": 7,
  "name": null,
  "seat_status": 0,
  "status": false
}
```

含义：

```txt
该元素不是具体可预约座位。
```

---

## 样本响应

```json
{
  "data": {
    "userAuth": {
      "reserve": {
        "libs": [
          {
            "lib_id": 126507,
            "is_open": true,
            "lib_floor": "三楼",
            "lib_name": "325自习室",
            "lib_type": 0,
            "lib_layout": {
              "seats_total": 400,
              "seats_booking": 4,
              "seats_used": 303,
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
                  "x": 17,
                  "y": 1,
                  "key": "1,17",
                  "type": 8,
                  "name": null,
                  "seat_status": 0,
                  "status": false
                },
                {
                  "x": 18,
                  "y": 1,
                  "key": "1,18",
                  "type": 8,
                  "name": null,
                  "seat_status": 0,
                  "status": false
                },
                {
                  "x": 19,
                  "y": 1,
                  "key": "1,19",
                  "type": 8,
                  "name": null,
                  "seat_status": 0,
                  "status": false
                },
                {
                  "x": 20,
                  "y": 1,
                  "key": "1,20",
                  "type": 8,
                  "name": null,
                  "seat_status": 0,
                  "status": false
                },
                {
                  "x": 21,
                  "y": 1,
                  "key": "1,21",
                  "type": 8,
                  "name": null,
                  "seat_status": 0,
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

---

## 备注

完整响应中的 `seats` 数组很长，文档里可以只保留代表性样本。



