# Docker：docker exec 进容器调试

## 进容器看一眼

```bash
docker exec -it myapp sh        # alpine 镜像一般只有 sh
docker exec -it myapp bash      # debian/ubuntu 镜像用 bash
```

`-i` 保持输入，`-t` 分配终端，合起来就是交互式 shell。

## 不进容器，直接执行

```bash
docker exec myapp ls /app
docker exec myapp env | sort
docker exec -u root myapp whoami   # 换用户执行
```

查问题时比 exec 进去再敲命令快。

## 对比：run vs exec

| 命令 | 作用 |
|------|------|
| `docker run` | **新建**一个容器并执行 |
| `docker exec` | 在**已运行**的容器里执行 |

调试线上容器用 exec，别 run 个新的——新容器没有线上的状态。

## 顺手记两个

```bash
docker logs -f --tail 100 myapp   # 看日志
docker cp myapp:/app/config.yaml ./  # 把文件拷出来看
docker inspect myapp | grep -i ip     # 看容器 IP 等元信息
```

exec + logs + inspect，容器问题基本都能定位。
