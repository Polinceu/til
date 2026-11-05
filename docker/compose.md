# Docker：Compose 的 service 依赖怎么写

```yaml
services:
  web:
    build: .
    depends_on:
      db:
        condition: service_healthy
  db:
    image: postgres:16
    healthcheck:
      test: ["CMD", "pg_isready"]
      interval: 5s
```

- `depends_on` 默认只等容器启动，不等服务就绪；要等就绪得配 `condition: service_healthy`。
- `docker compose up -d` 后台跑，`down` 会删容器但默认保留 volume，加 `-v` 才清数据。
- 本地开发用 `docker compose watch` 可以改代码自动同步，不用反复 rebuild。
