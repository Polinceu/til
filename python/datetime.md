# Python：datetime 常用操作速记

```python
from datetime import datetime, timedelta

now = datetime.now()
print(now.strftime("%Y-%m-%d %H:%M:%S"))  # 2026-11-15 10:30:00

# 字符串转时间
d = datetime.strptime("2026-11-15", "%Y-%m-%d")

# 加减时间
print(now + timedelta(days=7))      # 一周后
print(now - timedelta(hours=2))     # 两小时前

# 时间戳互转
print(int(now.timestamp()))         # 秒级时间戳
print(datetime.fromtimestamp(1794000000))
```

- `strftime` 是时间→字符串，`strptime` 是字符串→时间，别记反。
- `%Y` 四位年，`%m` 月，`%d` 日，`%H` 时，`%M` 分，`%S` 秒。
- 涉及时区再用 `timezone`，本地脚本一般不用折腾。
