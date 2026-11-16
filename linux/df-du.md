# Linux：df 看磁盘剩多少，du 看谁占得多

```bash
df -h               # 各挂载点剩余空间（-h 人类可读）
df -h /             # 只看根分区
du -sh /var/*       # /var 下各目录占用
du -sh ./* | sort -rh | head  # 当前目录最大的 10 个
du -sh --exclude=node_modules .  # 排除掉 node_modules
```

- 磁盘满了先 `df -h` 看哪个分区满，再 `du` 往下钻。
- `du` 看的是"文件实际占用的块"，`ls -l` 看的是逻辑大小，两者会差一点。
- 删了文件空间没释放？进程还拿着句柄，`lsof | grep deleted` 找出来重启进程。
