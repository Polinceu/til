# Linux：tmux，SSH 一断任务不死

跑长时间任务最怕 SSH 断了进程跟着死，tmux 让任务活在服务器上的会话里，
断线重连就能回来。

## 最小流程

```bash
tmux new -s work     # 新建一个叫 work 的会话
# 跑你的长任务……
# 按 Ctrl-b 再按 d：detach，会话留在后台
tmux attach -t work  # 断线回来，接回会话
tmux ls              # 看有哪些会话
tmux kill-session -t work
```

## 会话里分屏

- `Ctrl-b` 是前缀键，先按它再按后面的键：
- `%` 左右分屏，`"` 上下分屏，方向键在分屏间切换。
- `c` 新窗口，`n`/`p` 切换窗口，`d`  detach。

## 注意

- tmux 会话在服务器重启后就没了，真正要"开机自启"的任务还是写 systemd。
- 滚动查看历史输出：`Ctrl-b` 再按 `[`，用方向键翻，`q` 退出。
