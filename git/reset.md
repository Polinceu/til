# Git：reset 的三种模式，别再只会 --hard

```bash
git reset --soft HEAD~1   # 只动 HEAD：提交没了，改动还在暂存区
git reset --mixed HEAD~1  # 默认：提交没了，改动回工作区（未暂存）
git reset --hard HEAD~1   # 全清：提交没了，改动也丢了
```

- 想"撤回提交、改改再提"：用 `--soft` 或默认的 `--mixed`。
- `--hard` 会丢工作区改动，用之前确认 `git status` 是干净的。
- 已经 push 的提交别 reset，队友的历史会乱；用 `git revert` 生成一个"反向提交"。
