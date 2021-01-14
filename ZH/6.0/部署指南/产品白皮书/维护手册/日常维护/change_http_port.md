# 修改蓝鲸入口的HTTP访问端口

蓝鲸默认部署的是http协议+80端口的访问，比如 http://paas.bktencent.com 。有些用户因为网络原因，需要修改80端口为特殊的端口，比如8080。

本文档描述这种变更需求步骤。

1. 修改和端口变更相关的变量

    ```bash
    source /data/install/utils.fc

    # 从default/global.env 中复制相关变量到 userdef.env 中然后重定义端口
    cat <<EOF >> $CTRL_DIR/bin/03-userdef/global.env 
    # 访问PaaS平台的域名
    BK_PAAS_PUBLIC_URL="http://paas.bktencent.com:8080"
    BK_PAAS_PUBLIC_ADDR="paas.bktencent.com:8080"
    # 访问CMDB的域名
    BK_CMDB_PUBLIC_ADDR="cmdb.bktencent.com:8080"
    BK_CMDB_PUBLIC_URL="http://cmdb.bktencent.com:8080"
    # 访问Job平台的域名
    BK_JOB_PUBLIC_ADDR="job.bktencent.com:8080"
    BK_JOB_PUBLIC_URL="http://job.bktencent.com:8080"
    BK_JOB_API_PUBLIC_ADDR="jobapi.bktencent.com:8080"
    BK_JOB_API_PUBLIC_URL="http://jobapi.bktencent.com:8080"
    EOF

    ./bkcli install bkenv
    ./bkcli sync common

    # 刷新 consul 中存储的值
    consul kv put bkcfg/ports/paas_http 8080
    ```

2. 渲染PaaS和CMDB配置并重启

    ```bash
    ./bkcli render paas
    ./bkcli restart paas

    ./bkcli render cmdb
    ./bkcli restart cmdb
    ```

3. 渲染job的配置，并重启

    ```bash
    # 刷新前端index.html调用的api地址
    ./pcmd.sh -m nginx '$CTRL_DIR/bin/release_job_frontend.sh -p $BK_HOME -s $BK_PKG_SRC_PATH -B $BK_PKG_SRC_PATH/backup -i $BK_JOB_API_PUBLIC_URL'

    # 刷新job后台的web.url配置，并重启进程
    ./bkcli render job
    ./bkcli restart job
    ```

4. 重新部署SaaS，从PaaS中获取新的PUBLIC_URL

    ```bash
    ./bkcli install saas-o 
    ```