# Docker：.dockerignore 和 .gitignore 一样重要

## 问题：构建上下文太大

```bash
docker build -t myapp .
# Sending build context to Docker daemon  1.2GB  ← 离谱
```

`docker build` 会先把整个目录打包发给 daemon，
`node_modules`、`.git`、日志全在里面，又慢又浪费缓存。

## 写法（和 .gitignore 几乎一样）

```
node_modules
.git
*.log
dist
.env
.DS_Store
```

## 效果

```bash
# 加之前
Sending build context to Docker daemon  1.2GB
# 加之后
Sending build context to Docker daemon  12.8MB
```

## 几个注意点

- `COPY . .` 受 `.dockerignore` 影响，`COPY --from` 不受。
- `.dockerignore` 本身、Dockerfile 不会被忽略（除非你写了）。
- 敏感文件（`.env`、密钥）一定要忽略，
  不然 `docker history` 都能翻出来。

习惯：新建项目先写 `.gitignore`，顺手复制一份改成 `.dockerignore`。
