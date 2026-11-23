# 网络：dig 查 DNS

```bash
dig example.com            # 查 A 记录
dig example.com MX         # 查邮件服务器
dig @8.8.8.8 example.com   # 指定 DNS 服务器查
dig +short example.com     # 只要结果，不要啰嗦的输出
```

- `dig` 比 `nslookup` 输出全，排障时优先用它。
- `@8.8.8.8` 可以指定用哪个 DNS，怀疑本地 DNS 有问题时换个试试。
- `+short` 只出答案，写脚本时直接拿来用。
