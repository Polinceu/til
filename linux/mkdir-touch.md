# Linux：mkdir 和 touch

```bash
mkdir -p a/b/c    # 一次建多层目录
touch new.txt     # 建空文件，或刷新已有文件的时间
mkdir -p logs/{app,db}   # 花括号展开，一次建两个
```

- `mkdir` 不加 `-p` 时父目录不存在会报错。
- `touch` 已存在的文件会刷新时间戳，不改内容。
- 花括号展开是 shell 的功能：`logs/{app,db}` 变成 `logs/app logs/db`。
