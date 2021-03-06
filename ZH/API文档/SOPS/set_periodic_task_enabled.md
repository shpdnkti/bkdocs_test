
### 请求地址

/api/c/compapi/v2/sops/set_periodic_task_enabled/



### 请求方法

POST


### 功能描述

设置某个周期任务是否激活

### 请求参数


#### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用 ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -&gt; 点击应用 ID -&gt; 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |

#### 接口参数

| 字段          |  类型       | 必选   |  描述             |
|---------------|------------|--------|------------------|
|   task_id    |   string     |   是   |  周期任务 ID |
|   bk_biz_id    |   string     |   是   |  任务所属业务 ID |
|   enabled    |   bool     |   否   | 该周期任务是否激活，不传则为 false |

### 请求参数示例

<<<<<<< HEAD
```plain
=======
```bash
>>>>>>> e1a8ba8043275274bebe47274a313b1fd4d2b0fe
{
    "bk_app_code": "esb_test",
    "bk_app_secret": "xxx",
    "bk_token": "xxx",
    "bk_biz_id": "2",
    "task_id": "8",
    "enabled": false
}
```

### 返回结果示例

<<<<<<< HEAD
```plain
=======
```bash
>>>>>>> e1a8ba8043275274bebe47274a313b1fd4d2b0fe
{
    "data": {
        "enabled": false
    },
    "result": true
}
```

### 返回结果参数说明

|   名称   |  类型  |           说明             |
| ------------ | ---------- | ------------------------------ |
|  result      |    bool    |      true/false 操作是否成功     |
|  data        |    dict      |      result=true 时成功数据，详细信息请见下面说明     |
|  message        |    string      |      result=false 时错误信息     |

#### data

|   名称   |  类型  |           说明             |
| ------------ | ---------- | ------------------------------ |
|  enabled      |    bool    |      当前周期任务是否已经激活    |