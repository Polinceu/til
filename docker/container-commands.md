# Docker：容器管理的常用命令

```bash
docker ps              # 正在跑的容器
docker ps -a           # 包括已退出的
docker start/stop/restart myapp   # 启动/停止/重启
docker rm myapp        # 删容器（先 stop）
docker rm -f myapp     # 强制删（运行中也删）
docker exec -it myapp sh   # 进容器
docker logs -f --tail 50 myapp  # 看日志
```

- `docker ps` 不加 `-a` 看不到已退出的容器，找"跑起来又挂了"的容器要加 `-a`。
- `docker rm` 删的是容器，镜像还在；删镜像用 `docker rmi`。
- 容器名重复会报错，先 `docker ps -a` 确认名字没被占。
