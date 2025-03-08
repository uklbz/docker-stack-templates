# PostgreSQL Docker 配置

这个目录包含用于部署 PostgreSQL 数据库服务的 Docker Compose 配置。

## 配置说明

- 使用 PostgreSQL 16.3 Bullseye 镜像
- 数据库名称、用户名和密码可在 .env 文件中配置
- 数据持久化存储在指定的卷目录中
- 容器自动重启
- 使用独立的网络 `postgresql_network`
- 健康检查确保 PostgreSQL 服务正常运行

## 使用前准备

1. 确保 `.env` 文件中的配置符合您的需求，特别是数据库名称、用户名和密码
2. 根据需要调整数据卷路径

## 使用方法

### 启动 PostgreSQL 服务

```bash
docker-compose up -d
```

### 停止 PostgreSQL 服务

```bash
docker-compose down
```

### 查看日志

```bash
docker-compose logs -f
```

### 连接到 PostgreSQL

```bash
docker exec -it postgresql psql -U $DB_USER -d $DB_NAME
```

## 环境变量

`.env` 文件中包含以下环境变量：

- `DB_NAME` - 数据库名称（默认 pgdb）
- `DB_USER` - 数据库用户名（默认 uk）
- `DB_PASSWORD` - 数据库密码（默认 uk）
- `TZ` - 时区设置（默认 Asia/Shanghai）
- `VOLUME_DIR` - 数据卷目录路径
- `COMPOSE_PROJECT_NAME` - Docker Compose 项目名称

## 数据持久化

PostgreSQL 数据存储在指定的卷目录中，即使容器被删除，数据也会保留。

## 安全注意事项

- 请确保修改 `.env` 文件中的 `DB_PASSWORD` 为强密码
- 生产环境中应考虑使用 Docker Secrets 或其他安全的方式管理密码
- 考虑限制 PostgreSQL 的网络访问，只允许必要的连接

## 备份与恢复

### 创建备份

```bash
docker exec -t postgresql pg_dumpall -c -U $DB_USER > dump_$(date +%Y-%m-%d_%H_%M_%S).sql
```

### 恢复备份

```bash
cat your_dump.sql | docker exec -i postgresql psql -U $DB_USER -d $DB_NAME
``` 