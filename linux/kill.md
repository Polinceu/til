# Linux：kill 停进程

```bash
ps aux | grep nginx     # 先找到进程号
kill 1234               # 发 TERM 信号，进程可以自己收尾
kill -9 1234            # SIGKILL，强制杀，进程来不及收尾
pkill -f "python app.py"  # 按名字杀
```

- 先 `kill`（TERM），进程能正常清理；不行再 `kill -9`。
- `kill -9` 不给进程收尾机会，可能丢数据、留脏文件。
- `pkill -f` 按命令行匹配，写错模式可能误杀，用前先 `pgrep -f` 确认。
