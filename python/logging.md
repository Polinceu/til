# Python：logging 基础

```python
import logging

logging.basicConfig(level=logging.INFO, format="%(levelname)s %(message)s")
logging.debug("看不见，级别不够")
logging.info("服务启动了")
logging.warning("磁盘快满了")
```

- 级别从低到高：DEBUG < INFO < WARNING < ERROR < CRITICAL。
- 默认级别是 WARNING，所以 INFO/DEBUG 默认不打印，得 `basicConfig(level=...)`。
- 别用 `print` 打日志，`logging` 能分级、能写文件、能关掉。
