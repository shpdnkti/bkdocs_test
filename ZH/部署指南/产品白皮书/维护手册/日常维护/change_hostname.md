# 修改主机名

部署蓝鲸之前，建议就确定好主机名，部署蓝鲸的服务器要求主机名不能冲突。

本文描述已经搭建完蓝鲸，需要修改主机名时，应该如何操作:

1. 修改本机的主机名，假设修改为 `bk-1`

    ```bash
    hostnamectl set-hostname bk-1
    hostname # 确认
    ```

2. 此刻命令行提示符如果显示了主机名还是老的，可以退出登录，重新登录一下生效。
3. 修改 consul 的 node_name 配置项，和主机名保持一致。（非必须，但是强烈建议保持一致）

    ```bash
    vim /etc/consul.d/consul.json
    # 编辑 node_name 配置项
    systemctl restart consul
    ```

4. 如果修改主机名的机器是consul server的leader，那么这时会触发consul 集群的重新选主，需要等待一段时间。

    ```bash
    consul monitor # 持续观察日志输出，按Ctrl-C中断
    consul members # 观察是否正常加入集群
    ```
