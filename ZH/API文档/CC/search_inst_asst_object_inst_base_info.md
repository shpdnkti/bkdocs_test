
### 请求地址

/api/c/compapi/v2/cc/search_inst_asst_object_inst_base_info/



### 请求方法

POST


### 功能描述

查询实例关联模型实例基本信息

### 请求参数


#### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用 ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -&gt; 点击应用 ID -&gt; 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |


#### 接口参数

| 字段      |  类型      | 必选   |  描述      |
|-----------|------------|--------|------------|
| fields         |  array   | 否     | 指定查询的字段，参数为业务的任意属性，如果不填写字段信息，系统会返回业务的所有字段 |
| condition      |  dict    | 否     | 查询条件|
| page           |  dict    | 否     | 分页条件 |

#### condition

| 字段      |  类型      | 必选   |  描述      |
|-----------|------------|--------|------------|
| bk_obj_id |  string    | 是     | 实例模型 ID |
| bk_inst_id|  int    |  是    |实例 ID |
|association_obj_id|string|  是  | 关联对象的模型 ID， 返回 association_obj_id 模型与 bk_inst_id 实例有关联的实例基本数据（bk_inst_id,bk_inst_name）|
|is_target_object| bool |  否 |bk_obj_id 是否为目标模型， 默认 false， 关联关系中的源模型，否则是目标模型|

#### page

| 字段      |  类型      | 必选   |  描述      |
|-----------|------------|--------|------------|
| start    |  int    | 否      | 记录开始位置,默认值 0|
| limit    |  int    | 否     | 每页限制条数,默认值 20,最大 200 |


### 请求参数示例

```python
{
    "bk_app_code": "esb_test",
    "bk_app_secret": "xxx",
    "bk_token": "xxx",
    "bk_supplier_account": "123456789",
    "condition": {
        "bk_obj_id":"bk_switch", 
		"bk_inst_id":12, 
		"association_obj_id":"host", 
		"is_target_object":true, 
    },
    "page": {
        "start": 0,
        "limit": 10,
    }
}
```

### 返回结果示例

```python

{
    "result": true,
    "code": 0,
    "message": "success",
    "permission": null,
    "data": {
        "count": 4,
        "info": [
            {
                "bk_inst_id": 1,
                "bk_inst_name": "127.0.0.3"
            }
        ],
        "page": {
            "start": 0,
            "limit": 1
        }
    }
}
```

### 返回结果参数说明

#### data

| 名称  | 类型  | 说明 |
|---|---|---|---|
| count| int| 记录条数 |
| info| object array |  关联对象的模型 ID， 实例关联模型的实例基本数据（bk_inst_id,bk_inst_name） |
| page| object|分页信息|

#### data.info 字段说明
| 名称  | 类型  | 说明 |
|---|---|---|---|
| bk_inst_id | int | 实例 ID |
| bk_inst_name | string  | 实例名 | 

##### data.info.bk_inst_id,data.info.bk_inst_name 字段说明

不同模型 bk_inst_id, bk_inst_name 对应的值

| 模型   | bk_inst_id   | bk_inst_name |
|---|---|---|---|
|业务 | bk_biz_id | bk_biz_name|
|集群 | bk_set_id | bk_set_name|
|模块 | bk_module_id | bk_module_name|
|进程 | bk_process_id | bk_process_name|
|主机 | bk_host_id | bk_host_inner_ip|
|通用模型 | bk_inst_id | bk_inst_name|


#### data.page 字段说明

| 名称  | 类型  | 说明 |
|---|---|---|---|
|start|int|服务端本次获取数据偏移位置|
|limit|int|服务端返回数据条数限制|