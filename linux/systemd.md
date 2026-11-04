# Linux：systemd 服务的最小配置

```ini
[Unit]
Description=My App
After=network.target

[Service]
ExecStart=/usr/local/bin/myapp
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

- `systemctl enable` 是开机自启，`start` 只是现在启动，两回事。
- `Restart=on-failure` 比 `always` 稳：配置错误导致秒退时不会无限重启刷日志。
- 看日志用 `journalctl -u myapp -f`，不要再去翻 `/var/log` 里找。
