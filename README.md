# 检测控制器 #
* [1. 病症对应检测项和指标项接口](#gdi)
* [2. 通过检测项ID获取检测项和指标信息(为下次继续检测预留接口)](#gd)


**病症对应检测项和指标项接口**<p id='gdi'></p>
----
* **URL**

  `<auth_host>mapi/detect/v1/base/getDetectionAndIndicators`

* **Method:**
  
  `GET`
  
*  **URL Params**

   Name   | Required | Data Type | Description 
:---------|:-------- |:--------- |:-------- 
user_id|true|int|用户ID
disease_id|true|int|病症ID

* **Success Response:**

   Name   |   Datatype   | Description 
:---------|:---------|:-------- 
id|int|检测项ID
project_name|string|检测项名称
instrument_name|string|检测仪器
close_enable|int|是否允许关闭不检测或跳过检测标志
announcements|string|检测项注意事项
cast_time|int|检测预计花费时间
indicators|object|指标列表
indicators[*].id|int|指标ID
indicators[*].indicator_name|string|指标名称
indicators[*].announcements|string|指标检测注意事项
indicators[*].group_name|string|分组标志名称
indicators[*].fields|object|指标包含哪些具体检测指标
indicators[*].fields[0].indicator_id|int|指标ID,对应indicators[*].id
indicators[*].fields[0].field_real_name|string|字段名(保留)
indicators[*].fields[0].description|string|描述
indicators[*].fields[0].field_index|string|字段值索引，提交值时用来确定是指标的哪一个个值，一个指标可能会包含多个检测指标值
indicators[*].fields[0].unit_name|string|单位
indicators[*].fields[0].min_value|double|最小值
indicators[*].fields[0].max_value|double|最大值

* **空类型说明:**

   Datatype   |   Value   | Description 
:---------|:---------|:-------- 
int|-1|整型值为空时，返回-1
float|-1|float型值为空时，返回-1
string|null|string型值为空时，返回null
array|null|array型值为空时，返回null
object|null|object型值为空时，返回null

* **Error Response:**

   Status   |   Result 
:---------|:---------
1001|正常
1003|没有权限进行访问
1007|没有数据
10004|用户不存在
10005|顾客会员ID格式不正确
12002|病症ID格式不正确


* **Sample :**

  ```javascript
{
    "status": 1001,  
    "result": [
        {
            "id": 1,
            "project_name": "体质指数",
            "instrument_name": "身高体重秤",
            "cast_time": 3,
            "announcements": null,
            "indicators": [
                {
                    "id": 8,
                    "indicator_name": "体质指数",
                    "announcements": null,
                    "group_name": "base",
                    "fields": [
                        {
                            "indicator_id": 8,
                            "field_real_name": "height",
                            "description": "身高",
                            "field_index": "value1",
                            "unit_name": "CM",
                            "min_value": -1,
                            "max_value": -1
                        },
                        {
                            "indicator_id": 8,
                            "field_real_name": "weight",
                            "description": "体重",
                            "field_index": "value2",
                            "unit_name": "kg",
                            "min_value": -1,
                            "max_value": -1
                        },
                        {
                            "indicator_id": 8,
                            "field_real_name": "bmi",
                            "description": "体质指数",
                            "field_index": "value3",
                            "unit_name": "kg/m2",
                            "min_value": -1,
                            "max_value": -1
                        }
                    ]
                }
            ],
            "close_enable": 1
        },
        {
            "id": 2,
            "project_name": "血糖",
            "instrument_name": "干式血生化分析仪",
            "cast_time": 9,
            "announcements": null,
            "indicators": [
                {
                    "id": 1,
                    "indicator_name": "空腹血糖",
                    "announcements": null,
                    "group_name": "blood",
                    "fields": [
                        {
                            "indicator_id": 1,
                            "field_real_name": "fbg",
                            "description": "空腹血糖",
                            "field_index": "value1",
                            "unit_name": "mmol/L",
                            "min_value": 1,
                            "max_value": 100
                        }
                    ]
                },
                {
                    "id": 2,
                    "indicator_name": "餐后2小时血糖",
                    "announcements": null,
                    "group_name": "blood",
                    "fields": [
                        {
                            "indicator_id": 2,
                            "field_real_name": "two_hpbg",
                            "description": "餐后2小时血糖",
                            "field_index": "value1",
                            "unit_name": "mmol/L",
                            "min_value": 1,
                            "max_value": 100
                        }
                    ]
                }
            ],
            "close_enable": 0
        },
        {
            "id": 3,
            "project_name": "血压",
            "instrument_name": "血压计",
            "cast_time": 4,
            "announcements": null,
            "indicators": [
                {
                    "id": 6,
                    "indicator_name": "血压",
                    "announcements": null,
                    "group_name": "base",
                    "fields": [
                        {
                            "indicator_id": 6,
                            "field_real_name": "sbp",
                            "description": "收缩压",
                            "field_index": "value1",
                            "unit_name": "mmHg",
                            "min_value": 10,
                            "max_value": 300
                        },
                        {
                            "indicator_id": 6,
                            "field_real_name": "dbp",
                            "description": "舒张压",
                            "field_index": "value2",
                            "unit_name": "mmHg",
                            "min_value": 10,
                            "max_value": 300
                        }
                    ]
                }
            ],
            "close_enable": 1
        },
        {
            "id": 4,
            "project_name": "糖尿病血生化（空腹）",
            "instrument_name": "干式血生化分析仪",
            "cast_time": 9,
            "announcements": null,
            "indicators": [
                {
                    "id": 11,
                    "indicator_name": "高密度脂蛋白胆固醇",
                    "announcements": null,
                    "group_name": "blood",
                    "fields": [
                        {
                            "indicator_id": 11,
                            "field_real_name": "hdl_c",
                            "description": "高密度脂蛋白胆固醇",
                            "field_index": "value1",
                            "unit_name": "mmol/L",
                            "min_value": 0.1,
                            "max_value": 50
                        }
                    ]
                },
                {
                    "id": 13,
                    "indicator_name": "低密度脂蛋白胆固醇",
                    "announcements": null,
                    "group_name": "blood",
                    "fields": [
                        {
                            "indicator_id": 13,
                            "field_real_name": "ldl_c",
                            "description": "低密度脂蛋白胆固醇",
                            "field_index": "value1",
                            "unit_name": "mmol/L",
                            "min_value": 1,
                            "max_value": 100
                        }
                    ]
                },
                {
                    "id": 19,
                    "indicator_name": "尿蛋白",
                    "announcements": null,
                    "group_name": "urine",
                    "fields": [
                        {
                            "indicator_id": 19,
                            "field_real_name": "up",
                            "description": "尿蛋白",
                            "field_index": "value1",
                            "unit_name": null,
                            "min_value": -1,
                            "max_value": -1
                        }
                    ]
                }
            ],
            "close_enable": 1
        },
        {
            "id": 5,
            "project_name": "糖化血红蛋白",
            "instrument_name": "糖化血红蛋白",
            "cast_time": 5,
            "announcements": null,
            "indicators": [
                {
                    "id": 5,
                    "indicator_name": "糖化血红蛋白",
                    "announcements": null,
                    "group_name": "blood",
                    "fields": [
                        {
                            "indicator_id": 5,
                            "field_real_name": "hba1c",
                            "description": "糖化血红蛋白",
                            "field_index": "value1",
                            "unit_name": "%",
                            "min_value": 1,
                            "max_value": 100
                        }
                    ]
                }
            ],
            "close_enable": 0
        }
    ]
}
  ```

**通过检测项ID获取检测项和指标信息**<p id='gd'></p>
----

* **URL**

  `<auth_host>mapi/detect/v1/base/getContinueDetections`

* **Method:**
  
  `GET`
  
*  **URL Params**

   Name   | Required | Data Type | Description 
:---------|:-------- |:--------- |:-------- 
detections|true|string|检测病症ID,多个可以实用','分割
user_id|true|int|顾客ID

* **Success Response:**

   Name   |   Datatype   | Description 
:---------|:---------|:-------- 
id|int|检测项ID
project_name|string|检测项名称
instrument_name|string|检测仪器
close_enable|int|是否允许关闭不检测或跳过检测标志
announcements|string|检测项注意事项
cast_time|int|检测预计花费时间
indicators|object|指标列表
indicators[*].id|int|指标ID
indicators[*].indicator_name|string|指标名称
indicators[*].announcements|string|指标检测注意事项
indicators[*].group_name|string|分组标志名称
indicators[*].fields|object|指标包含哪些具体检测指标
indicators[*].fields[0].indicator_id|int|指标ID,对应indicators[*].id
indicators[*].fields[0].field_real_name|string|字段名(保留)
indicators[*].fields[0].description|string|描述
indicators[*].fields[0].field_index|string|字段值索引，提交值时用来确定是指标的哪一个个值，一个指标可能会包含多个检测指标值
indicators[*].fields[0].unit_name|string|单位
indicators[*].fields[0].min_value|double|最小值
indicators[*].fields[0].max_value|double|最大值

* **空类型说明:**

   Datatype   |   Value   | Description 
:---------|:---------|:-------- 
int|-1|整型值为空时，返回-1
float|-1|float型值为空时，返回-1
string|null|string型值为空时，返回null
array|null|array型值为空时，返回null
object|null|object型值为空时，返回null

* **Error Response:**

   Status   |   Result 
:---------|:---------
1001|正常
1003|没有权限进行访问
1007|没有数据
10004|用户不存在
10005|顾客会员ID格式不正确
12003|检测列表不能为空

* **Sample :**

  ```javascript
{
    "status": 0,
    "result": [
        {
            "id": 1,
            "project_name": "体质指数",
            "instrument_name": "身高体重秤",
            "cast_time": 3,
            "announcements": null,
            "indicators": [
                {
                    "id": 8,
                    "indicator_name": "体质指数",
                    "announcements": null,
                    "group_name": "base",
                    "fields": [
                        {
                            "indicator_id": 8,
                            "field_real_name": "height",
                            "description": "身高",
                            "field_index": "value1",
                            "unit_name": "CM",
                            "min_value": -1,
                            "max_value": -1
                        },
                        {
                            "indicator_id": 8,
                            "field_real_name": "weight",
                            "description": "体重",
                            "field_index": "value2",
                            "unit_name": "kg",
                            "min_value": -1,
                            "max_value": -1
                        },
                        {
                            "indicator_id": 8,
                            "field_real_name": "bmi",
                            "description": "体质指数",
                            "field_index": "value3",
                            "unit_name": "kg/m2",
                            "min_value": -1,
                            "max_value": -1
                        }
                    ]
                }
            ],
            "close_enable": 1
        },
        {
            "id": 2,
            "project_name": "血糖",
            "instrument_name": "干式血生化分析仪",
            "cast_time": 9,
            "announcements": null,
            "indicators": [
                {
                    "id": 1,
                    "indicator_name": "空腹血糖",
                    "announcements": null,
                    "group_name": "blood",
                    "fields": [
                        {
                            "indicator_id": 1,
                            "field_real_name": "fbg",
                            "description": "空腹血糖",
                            "field_index": "value1",
                            "unit_name": "mmol/L",
                            "min_value": 1,
                            "max_value": 100
                        }
                    ]
                },
                {
                    "id": 2,
                    "indicator_name": "餐后2小时血糖",
                    "announcements": null,
                    "group_name": "blood",
                    "fields": [
                        {
                            "indicator_id": 2,
                            "field_real_name": "two_hpbg",
                            "description": "餐后2小时血糖",
                            "field_index": "value1",
                            "unit_name": "mmol/L",
                            "min_value": 1,
                            "max_value": 100
                        }
                    ]
                }
            ],
            "close_enable": 1
        },
        {
            "id": 3,
            "project_name": "血压",
            "instrument_name": "血压计",
            "cast_time": 4,
            "announcements": null,
            "indicators": [
                {
                    "id": 6,
                    "indicator_name": "血压",
                    "announcements": null,
                    "group_name": "base",
                    "fields": [
                        {
                            "indicator_id": 6,
                            "field_real_name": "sbp",
                            "description": "收缩压",
                            "field_index": "value1",
                            "unit_name": "mmHg",
                            "min_value": 10,
                            "max_value": 300
                        },
                        {
                            "indicator_id": 6,
                            "field_real_name": "dbp",
                            "description": "舒张压",
                            "field_index": "value2",
                            "unit_name": "mmHg",
                            "min_value": 10,
                            "max_value": 300
                        }
                    ]
                }
            ],
            "close_enable": 1
        }
    ]
}
  ```