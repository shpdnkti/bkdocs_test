## 私有构建机问题排查
### 私有构建机安装失败

1. 请检查部署时有无提供对应平台的 jre.zip 。
2. 请检查 jre.zip 内是否有 `bcprov-jdk16-1.46.jar` 。
3. 请检查 Linux / MacOS 系统中是否有 `unzip` 命令。（ Windows 版本包含在 agent 里了）
4. 如果已经完成了上述步骤，请清空安装目录后重新安装。避免旧的错误安装包缓存造成干扰。
