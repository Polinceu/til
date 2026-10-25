# 网络：DNS 查询，dig 比 nslookup 好用

## 查 A 记录

```bash
dig example.com +short
# 93.184.216.34
```

`+short` 只输出结果，写脚本时清爽。

## 看完整解析过程

```bash
dig example.com +trace
```

从根服务器一路问下来，能看出卡在哪一级。

## 查指定记录类型

```bash
dig example.com MX +short      # 邮件服务器
dig example.com TXT +short     # SPF/DKIM 验证信息
dig www.example.com CNAME +short
```

## 指定 DNS 服务器

```bash
dig @8.8.8.8 example.com +short
dig @114.114.114.114 example.com +short
```

怀疑本地 DNS 被污染/劫持时，换个公共 DNS 对比一下就知道。

## 常见记录类型

| 类型 | 用途 |
|------|------|
| A | 域名 → IPv4 |
| AAAA | 域名 → IPv6 |
| CNAME | 域名 → 另一个域名 |
| MX | 邮件服务器 |
| TXT | 文本，常用于域名验证 |

改完 DNS 不生效？先 `dig` 看 TTL，
缓存没过期的话，等，或者换网络试。
