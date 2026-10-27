# Docker：多阶段构建，镜像瘦身最有效的一招

## 痛点：构建工具污染了运行镜像

```dockerfile
# 反面教材：golang 镜像 800MB+，跑个二进制而已
FROM golang:1.22
COPY . /app
RUN go build -o /app/server .
CMD ["/app/server"]
```

## 多阶段：构建和运行分开

```dockerfile
# 阶段一：构建
FROM golang:1.22 AS builder
WORKDIR /app
COPY . .
RUN CGO_ENABLED=0 go build -o server .

# 阶段二：运行，只要二进制
FROM alpine:3.19
WORKDIR /app
COPY --from=builder /app/server .
CMD ["./server"]
```

最终镜像只有十几 MB，构建时的 Go 工具链全扔了。

## Node 项目同理

```dockerfile
FROM node:20 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM node:20-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY package*.json ./
RUN npm ci --omit=dev
CMD ["node", "dist/index.js"]
```

## 要点

- `COPY --from=builder` 只拿产物，不拿源码和依赖。
- 构建阶段和运行阶段可以用完全不同的基础镜像。
- 镜像小了，推送拉取都快，攻击面也小，一举三得。
