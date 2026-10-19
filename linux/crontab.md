# Linux：crontab 五段格式

## 格式

```
* * * * * command
分 时 日 月 周
```

```bash
0 2 * * * /opt/backup.sh          # 每天 2:00
*/10 * * * * /opt/healthcheck.sh  # 每 10 分钟
0 9 * * 1                        # 每周一 9:00
0 0 1 * *                        # 每月 1 号 0:00
```

## 编辑和查看

```bash
crontab -e    # 编辑当前用户的
crontab -l    # 查看
crontab -r    # 删除（慎用，没确认的）
```

## 三个坑

1. **环境变量**：cron 的 PATH 很小，脚本里用绝对路径，
   或在 crontab 头部写 `PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin`。

2. **输出**：命令的输出会发邮件（一般没配），建议重定向：
   `0 2 * * * /opt/backup.sh >>/var/log/backup.log 2>&1`

3. **`%` 要转义**：crontab 里 `%` 表示换行，
   `date +%Y%m%d` 得写成 `date +\%Y\%m\%d`。

## 系统级 vs 用户级

- `crontab -e`：当前用户，简单任务用这个。
- `/etc/cron.d/`：系统级，多一个"以哪个用户跑"字段，
  适合多用户机器。
