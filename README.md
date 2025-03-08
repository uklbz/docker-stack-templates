# Docker Stack Templates

这个仓库包含了各种常用服务的 Docker Compose 配置模板，方便快速部署和管理各种开发和生产环境中的服务。

## 目录结构

每个服务都有自己的目录，包含以下文件：

- `docker-compose.yaml` - Docker Compose 配置文件
- `.env` - 环境变量配置文件
- 配置文件目录 - 包含服务特定的配置文件
- `README.md` - 服务特定的说明文档

## 可用的服务模板

目前仓库包含以下服务的配置模板：

- [Redis](./redis/README.md) - Redis 内存数据库
- [PostgreSQL](./postgresql/README.md) - PostgreSQL 关系型数据库

## 使用方法

### 基本使用流程

1. 进入对应服务的目录
2. 根据需要修改 `.env` 文件中的配置
3. 使用 `docker-compose up -d` 启动服务
4. 使用 `docker-compose down` 停止服务

### 示例：启动 Redis 服务

```bash
cd redis
# 编辑 .env 文件，设置密码等参数
docker-compose up -d
```

### 示例：启动 PostgreSQL 服务

```bash
cd postgresql
# 编辑 .env 文件，设置数据库名、用户名和密码等参数
docker-compose up -d
```

## 自定义配置

每个服务目录中的 `.env` 文件包含了可自定义的配置参数。您可以根据需要修改这些参数，例如：

- 端口映射
- 用户名和密码
- 数据卷路径
- 其他服务特定的配置

## 数据持久化

所有服务都配置了数据持久化，数据存储在各自目录下的 `volumes` 目录中。即使容器被删除，数据也会保留。

## 安全注意事项

- 请确保修改默认的用户名和密码
- 生产环境中应考虑使用 Docker Secrets 或其他安全的方式管理密码
- 根据需要限制服务的网络访问

## 贡献

欢迎贡献新的服务模板或改进现有模板。请通过 Pull Request 提交您的贡献。

## 许可证

MIT 