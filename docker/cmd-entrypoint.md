# Dockerfile：CMD 和 ENTRYPOINT

```dockerfile
FROM python:3.12-slim
ENTRYPOINT ["python", "app.py"]
CMD ["--help"]
```

- `ENTRYPOINT` 是固定的启动命令，`CMD` 是默认参数。
- `docker run img --port 8080` 会替换 `CMD`，`ENTRYPOINT` 不变。
- 两个都写 exec 格式（JSON 数组），shell 格式收不到 SIGTERM，容器停不干净。
