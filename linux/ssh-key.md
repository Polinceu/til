# Linux：SSH 密钥，免密登录就三步

每次输密码登录服务器又慢又容易被爆破，密钥登录是标准做法。

## 三步

```bash
ssh-keygen -t ed25519 -C "my-laptop"   # 一路回车，生成 ~/.ssh/id_ed25519
ssh-copy-id user@服务器IP              # 把公钥写进服务器的 authorized_keys
ssh user@服务器IP                      # 直接进，不用输密码
```

## 常用配置（~/.ssh/config）

```
Host myserver
    HostName 1.2.3.4
    User root
    IdentityFile ~/.ssh/id_ed25519
```

写好之后 `ssh myserver` 就行，不用每次敲 IP。

## 安全习惯

- 私钥 `id_ed25519` 绝不发给别人、不进 git；公钥 `.pub` 才可以公开。
- `~/.ssh` 目录权限 700，`authorized_keys` 600，太松了 sshd 会拒绝。
- 服务器上可以关掉密码登录（`PasswordAuthentication no`），只留密钥。
