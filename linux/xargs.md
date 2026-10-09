# Linux：xargs，把输出变成参数

## 基本用法

```bash
find . -name "*.log" | xargs rm        # 删掉找到的文件
cat urls.txt | xargs -n1 curl -s -o /dev/null -w "%{http_code}\n"
```

`xargs` 把管道来的每一行变成后面命令的参数。

## 文件名带空格的坑

```bash
# 错误示范：文件名 "my file.log" 会被拆成两个参数
find . -name "*.log" | xargs rm

# 正确：用 \0 分隔
find . -name "*.log" -print0 | xargs -0 rm
```

`-print0` + `xargs -0` 用空字符分隔，空格、换行都不怕。

## 控制并发：-P

```bash
cat hosts.txt | xargs -P 10 -I {} ssh {} "uptime"
```

`-P 10` 同时跑 10 个，批量巡检机器时很快。
`-I {}` 指定占位符，参数放中间位置时用。

## 限制每批数量：-n

```bash
echo a b c d | xargs -n2 echo  # 两两一组
# a b
# c d
```

一次参数太多会超系统限制（ARG_MAX），
`xargs` 默认会自动分批，这也是它比 `$(...)` 稳的原因。
