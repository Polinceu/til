# Linux：环境变量的设置与生效

```bash
export FOO=bar      # 当前 shell 生效
echo $FOO           # bar
env | grep FOO      # 看所有环境变量

# 永久生效：写进 ~/.bashrc（交互 shell）或 ~/.profile（登录 shell）
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc    # 立即生效，不用重开终端

# 只给一条命令用
FOO=bar python3 app.py
```

- `export` 的变量子进程能继承，不 export 的只有当前 shell 能看到。
- PATH 里自己的目录放前面，优先用自己的版本。
- 密钥别写进 `.bashrc`，用专门的 `.env` 文件 + `source`，且别进版本库。
