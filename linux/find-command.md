# Linux：find 的几个高频用法

## 按名字找

```bash
find . -name "*.log"          # 当前目录递归找
find /var -name "*.tmp" -type f  # 只找文件
find . -iname "readme*"       # 忽略大小写
```

## 按时间找

```bash
find . -mtime -7              # 7 天内改过的
find . -mtime +30 -name "*.log"  # 30 天前 的日志（可删？）
find . -mmin -60              # 60 分钟内改过的
```

`-7` 是以内，`+30` 是以外，这个正负号老记反。

## 找到直接处理：-exec

```bash
find . -name "*.log" -mtime +30 -exec rm {} \;
find . -type f -name "*.bak" -exec ls -lh {} \;
```

`{}` 是占位符，`\;` 是 -exec 的结束符（分号要转义）。

## 先预览再删

```bash
find . -name "*.tmp" -print   # 先看会删掉啥
find . -name "*.tmp" -delete  # 确认后再删（比 -exec rm 快）
```

血泪教训：`-exec rm` 之前一定先 `-print` 看一眼，
find 的递归能力配上 rm，删错了找不回来。
