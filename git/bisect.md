# Git：bisect 二分定位 bug 引入点

```bash
git bisect start
git bisect bad HEAD
git bisect good v1.0
# 每次 checkout 后测一下，告诉它好还是坏
git bisect good   # 或 git bisect bad
git bisect reset
```

- 只要知道一个好的版本和一个坏的版本，bisect 会自动二分，log 级复杂度找到元凶。
- 测试命令固定时可以用 `git bisect run ./test.sh` 全自动跑完。
- 结束后一定 `git bisect reset`，不然 HEAD 还停在 bisect 状态。
