# Docker：容器互访用服务名，不用 IP

```bash
docker network create mynet
docker run -d --name db --network mynet postgres:16
docker run -d --name web --network mynet myapp
# web 里直接用 db:5432 就能连到数据库
```

- 同一个自定义网络里的容器，自带 DNS 解析，服务名就是主机名。
- 默认 bridge 网络没有这个 DNS 功能，所以生产和联调都建议自建网络。
- 需要从宿主机访问时才映射端口 `-p`，容器之间互访不需要映射。
