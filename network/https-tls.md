# 网络：HTTPS 握手在干什么

1. 客户端发 ClientHello：支持的 TLS 版本、加密套件、随机数。
2. 服务端回 ServerHello + 证书 + 自己的随机数。
3. 客户端验证证书链，生成预主密钥，用服务端公钥加密发过去。
4. 双方算出会话密钥，之后全部用对称加密通信。

- TLS 1.3 把往返压到 1-RTT，1.2 需要 2-RTT。
- 证书验证失败时浏览器拦截的不是加密本身，而是“你连的到底是不是这个域名”。
- 抓包排障用 `openssl s_client -connect host:443 -servername host`。
