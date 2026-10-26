# 网络：curl 常用参数备忘

## 只看响应头

```bash
curl -I https://example.com
```

看状态码、缓存头、重定向，`-I` 发的是 HEAD 请求。

## 跟随重定向

```bash
curl -L https://short.url/abc
```

短链接、http→https 跳转，不加 `-L` 只能拿到 301。

## 保存文件

```bash
curl -o out.zip https://example.com/a.zip   # 指定文件名
curl -O https://example.com/a.zip            # 用远程文件名
curl -C - -o big.iso https://example.com/big.iso  # 断点续传
```

## 调试接口

```bash
curl -s -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d '{"name":"a","age":20}'
```

`-s` 静默（去掉进度条），`-w` 自定义输出：

```bash
curl -s -o /dev/null -w "%{http_code} %{time_total}s\n" https://example.com
```

一行看出状态码和耗时，写健康检查脚本很好用。

## 忽略证书（仅调试）

```bash
curl -k https://self-signed.local
```

`-k` 跳过证书校验，自签证书联调时用，
生产脚本里别加。
