# 变更域名

安装部署后，BK_DOMAIN 默认使用的是 bktencent.com，如果需要修改成其他的域名。例如换成 bktencent.org，可以按以下步骤进行：

- 备份中控机的 install 目录

  ```bash
  tar -czf /data/src/backup/install_ce_$(date +%Y%m%d).tgz -C /data install
  ```

- 运行变更域名脚本 **（请使用实际的域名进行替换）**

  ```bash
  cd /data/install
  ./bin/change_bk_domain.sh bktencent.org
  ```

- 上述脚本运行成功后:
    - 如果域名是配置的本地 hosts 文件，请修改本机的 hosts 文件。
    - 如果是通过 DNS 解析的，请修改相应的 DNS 解析。

- 请重新部署所有官方 SaaS 
  ```
  ./bkcli install saas-o
  ``` 