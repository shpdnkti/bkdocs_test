
### 请求地址

/api/c/compapi/v2/sops/operate_task/



### 请求方法

POST


### 功能描述

操作任务，如开始、暂停、继续、终止等

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
|   bk_biz_id   |   string     |   是   |  模板所属业务 ID |
|   task_id     |   string     |   是   |  任务 ID         |
|   action      |   string     |   是   |  操作类型       |

#### action

| 值        | 描述     |
|-----------|----------|
| start     | 开始任务，等效于调用 start_task 接口 |
| pause     | 暂停任务，任务处于执行状态时调用  |
| resume    | 继续任务，任务处于暂停状态时调用  |
| revoke    | 终止任务  |

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
    "action": "start",
    "bk_biz_id": "2",
    "task_id": "10"
}
```

### 返回结果示例

<<<<<<< HEAD
```plain
=======
```bash
>>>>>>> e1a8ba8043275274bebe47274a313b1fd4d2b0fe
{
    "result": true,
    "data": {}
}
```

### 返回结果参数说明

| 字段      | 类型      | 描述      |
|-----------|----------|-----------|
|  result      |    bool    |      true/false 操作是否成功     |
|  data        |    dict  |      result=true 时返回数据      |
|  message     |    string  |      result=false 时错误信息     |