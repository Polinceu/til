# Linux：history 查历史命令

```bash
history              # 列出历史命令
history | grep ssh   # 找以前敲过的 ssh
!123                 # 重新执行第 123 条
!!                   # 重新执行上一条
```

- `history` 默认显示最近 1000 条，太多就管道给 `grep` 筛。
- `!数字` 执行对应编号的命令，`!!` 是上一条，敲错了别乱用。
- 带密码的命令别直接敲，`export HISTCONTROL=ignorespace` 后，行首加空格的命令不进历史。
