# Linux：journalctl 查 systemd 服务日志

用 systemd 的机器上，别再到处找 log 文件了。

## 看某个服务的日志

```bash
journalctl -u nginx -f              # 实时跟（像 tail -f）
journalctl -u nginx --since "1 hour ago"
journalctl -u nginx --since today -p err  # 今天的错误级
```

## 时间范围

```bash
journalctl --since "2026-10-01" --until "2026-10-02"
journalctl --since "30 min ago"
journalctl -b                       # 本次开机以来的
journalctl -b -1                    # 上次开机的（查崩溃前日志神器）
```

## 配合 grep 和 JSON

```bash
journalctl -u myapp -o json | jq '.MESSAGE'
journalctl -u myapp --no-pager | grep -i "error"
```

`-o json` + jq 适合写脚本解析。

## 磁盘被日志塞满？

```bash
journalctl --disk-usage             # 看占了多少
journalctl --vacuum-size=500M       # 只保留 500M
journalctl --vacuum-time=7d         # 只保留 7 天
```

`/etc/systemd/journald.conf` 里可以设 `SystemMaxUse`，
一劳永逸。线上机器建议都设一下。
