# SILO - LazyCat App

[SILO](https://github.com/pgsty/silo)（S3 兼容对象存储，MinIO 社区分支，PGSTY 维护）的懒猫微服（LazyCat）打包。

## 模式

- **镜像模式（mirror）**：`docker.io/pgsty/silo` 镜像经 `docker.1ms.run` 加速器拉取，`require_digest_match: true` 校验镜像内容与上游一致。
- **自动跟随上游**：每日检查上游 `RELEASE.YYYY-MM-DD...` 日期 tag（`channel: date` 映射为 SemVer），发现新版本自动更新版本号与镜像、构建 LPK、发布商店。
- **喵喵商店发布**：仅私有商店（MiaoMiao private store），不发布官方商店。

## 设置向导参数

| 参数 | 说明 |
| --- | --- |
| 管理员用户名 | 默认 `admin` |
| 管理员密码 | 默认随机 20 位 |

## 说明

- **双端口**：S3 API `9000`（应用内）+ Web 控制台 `9001`（子域名入口）
- 数据卷 `/lzcapp/var/silo:/data`
- 健康检查用 bash `/dev/tcp` 探测（镜像基于 UBI micro，无 curl/wget）
- 镜像内置 `mcli` 客户端，可 `lzc-cli project exec` 进容器管理
- 官方商店已有他人发的另一个 silo 包（`cloud.lazycat.app.silo`），本包 `community.` 前缀独立发布

## 所需 Secrets

| Secret | 说明 |
| --- | --- |
| `APPSTORE_URL` / `APPSTORE_TOKEN` | 喵喵商店 API 地址与发布令牌 |
| `APP_ID` | 可选 |
| `PRIVATE_STORE_GROUP_CODES` | 可选，私有分组码 |

## 许可

AGPL-3.0（上游，继承 MinIO）
