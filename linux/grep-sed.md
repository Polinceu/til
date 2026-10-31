# Linux：grep 和 sed 的常用组合

```bash
# 递归查内容，排除 .git
grep -rn "TODO" --exclude-dir=.git .

# 只看文件名
grep -rl "password" /etc 2>/dev/null

# sed 原地替换（先备份）
sed -i.bak 's/old/new/g' file.txt
```

- `grep -r` 递归，`-n` 显示行号，`-i` 忽略大小写。
- sed 的 `s/old/new/g` 里 `g` 是全局，不加只换每行第一个。
- 正则里 `/` 要转义时可以换分隔符：`sed 's|/old/path|/new/path|'`。
