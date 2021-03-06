
### 请求地址

/api/c/compapi/v2/job/fast_execute_sql/



### 请求方法

POST


### 功能描述

快速执行 SQL 脚本

### 请求参数


#### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用 ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -&gt; 点击应用 ID -&gt; 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |

#### 接口参数

| 字段          |  类型      | 必选   |  描述      |
|---------------|------------|--------|------------|
| bk_biz_id      |  long       | 是     | 业务 ID |
| script_id      |  long       | 否     | SQL 脚本 ID |
| script_content |  string    | 否     | 脚本内容 Base64，如果同时传了 script_id 和 script_content，则 script_id 优先 |
| script_timeout |  int       | 否     | 脚本超时时间，秒。默认 1000，取值范围 60-86400 |
| db_account_id  |  long       | 是     | SQL 执行的 db 帐号 ID，必填, 从帐号管理-DB 帐号处获得。 |
| custom_query_id  |  array    | 否     | *deprecated*，请使用 target_server.dynamic_group_id_list 替代。配置平台上的自定义分组 ID |
| ip_list          |  array    | 否     | *deprecated*，请使用 target_server.iplist 替代。静态 IP 列表 |
| target_server    |  dict     | 否     | 目标服务器 |
| bk_callback_url |  string   | 否     | 回调 URL，当任务执行完成后，JOB 会调用该 URL 告知任务执行结果。回调协议参考 callback_protocol 组件文档 |

#### target_server
| 字段      |  类型      | 必选   |  描述      |
|-----------|------------|--------|------------|
| ip_list               | array | 否     | 静态 IP 列表 |
| dynamic_group_id_list | array | 否     | 动态分组 ID 列表 |
| topo_node_list        | array | 否     | 动态 topo 节点列表 |

#### ip_list

| 字段      |  类型      | 必选   |  描述      |
|-----------|------------|--------|------------|
| bk_cloud_id |  long    | 是     | 云区域 ID |
| ip          |  string | 是     | IP 地址 |

#### topo_node_list
| 字段      |  类型      | 必选   |  描述      |
|-----------|------------|--------|------------|
| id               | long   | 是     | 动态 topo 节点 ID，对应 CMDB API 中的 bk_inst_id |
| node_type        | string | 是     | 动态 topo 节点类型，对应 CMDB API 中的 bk_obj_id,比如"module","set"|

### 请求参数示例

```python
{
    "bk_app_code": "esb_test",
    "bk_app_secret": "xxx",
    "bk_token": "xxx",
    "bk_biz_id": 1,
    "script_id": 1,
    "script_content": "c2hvdyBkYXRhYmFzZXM7",
    "script_timeout": 1000,
    "db_account_id": 32,
    "target_server": {
        "dynamic_group_id_list": ["blo8gojho0skft7pr5q0", "blo8gojho0sabc7priuy"],
        "ip_list": [{
                "bk_cloud_id": 0,
                "ip": "10.0.0.1"
            }, {
                "bk_cloud_id": 0,
                "ip": "10.0.0.2"
            }
        ],
        "topo_node_list": [{
                "id": 1000,
                "node_type": "module"
            }
        ]
    }
}
```

### 返回结果示例

```python
{
    "result": true,
    "code": 0,
    "message": "success",
    "data": {
        "job_instance_name": "API Quick SQL Execution1524454292038",
        "job_instance_id": 10000
    }
}
```