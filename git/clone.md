# Git：clone 常用选项

```bash
git clone https://github.com/user/repo.git
git clone --depth 1 https://github.com/user/repo.git   # 只拿最新一次提交，省时间
git clone -b dev https://github.com/user/repo.git     # 直接切到 dev 分支
```

- `--depth 1` 浅克隆，历史不要了，下载快，适合只看代码。
- `-b` 指定分支，省掉 clone 完再 checkout 的步骤。
- 浅克隆不能 `git log` 看完整历史，需要时再 `git fetch --unshallow`。
