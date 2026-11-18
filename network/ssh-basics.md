# 网络：SSH 的基础用法

```bash
ssh user@host                  # 登录
ssh -p 2222 user@host          # 指定端口
ssh -i ~/.ssh/key.pem user@host  # 指定密钥
ssh user@host "uptime"         # 直接在远端跑命令
ssh -L 8080:localhost:80 user@host  # 本地端口转发
```

- 第一次连会问 `Are you sure you want to continue`，确认指纹后写入 `~/.ssh/known_hosts`。
- `~/.ssh/config` 可以给常用主机起别名，省得每次敲地址和端口。
- 私钥权限必须是 600，不然 ssh 拒绝用。
