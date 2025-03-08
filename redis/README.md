# Redis Docker 配置

这个目录包含用于部署 Redis 服务的 Docker Compose 配置。

## 配置说明

- 使用 Redis 7.0 Bullseye 镜像
- 端口映射：根据 .env 文件中的 REDIS_PORT 设置（默认 6379）
- 持久化数据存储在 volumes 目录中
- 使用自定义的 redis.conf 配置文件
- 容器自动重启
- 使用独立的网络 `redis_network`
- 健康检查确保 Redis 服务正常运行

## 使用前准备

1. 确保 `.env` 文件中的配置符合您的需求，特别是 `REDIS_PASSWORD`
2. 如需自定义 Redis 配置，请修改 `config/redis.conf` 文件

## 使用方法

### 启动 Redis 服务

```bash
docker-compose up -d
```

### 停止 Redis 服务

```bash
docker-compose down
```

### 查看日志

```bash
docker-compose logs -f
```

### 连接到 Redis CLI

```bash
docker exec -it redis redis-cli -a $REDIS_PASSWORD
```

## 环境变量

`.env` 文件中包含以下环境变量：

- `REDIS_PORT` - Redis 服务端口（默认 6379）
- `REDIS_PASSWORD` - Redis 访问密码
- `TZ` - 时区设置（默认 Asia/Shanghai）
- `VOLUME_DIR` - 数据卷目录路径
- `COMPOSE_PROJECT_NAME` - Docker Compose 项目名称

## 数据持久化

Redis 数据存储在 volumes 目录中，即使容器被删除，数据也会保留。

## 安全注意事项

- 请确保修改 `.env` 文件中的 `REDIS_PASSWORD` 为强密码
- 生产环境中应考虑使用 Docker Secrets 或其他安全的方式管理密码
- 根据需要调整 redis.conf 中的安全设置 