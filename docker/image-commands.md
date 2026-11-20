# Docker：镜像的常用操作

```bash
docker images                    # 本地镜像列表
docker images -a                 # 包括中间层
docker pull nginx:1.25           # 拉指定版本
docker rmi nginx:1.25            # 删镜像
docker tag myapp:latest myapp:v1 # 打标签
docker image prune               # 删没用的悬空镜像
docker image prune -a            # 删所有没被容器用的镜像
```

- 悬空镜像（`<none>`）是构建时被新层取代的旧层，定期 prune 清理。
- `docker rmi` 删不掉被容器用的镜像，先删容器或加 `-f`。
- 镜像名格式：`仓库/名:标签`，不写标签默认 `latest`。
