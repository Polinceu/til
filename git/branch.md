# Git：分支的常用操作

```bash
git branch                # 看本地分支（* 是当前）
git branch -a             # 连远程分支一起看
git switch feature        # 切分支（新命令，比 checkout 清楚）
git switch -c feature     # 新建并切换
git branch -d feature     # 合并过的分支才能删
git branch -D feature     # 强制删，没合并也删
git branch -m old new     # 重命名
git push origin --delete feature  # 删远程分支
```

- `git switch` 是专门切分支的，`checkout` 还能切文件，容易混。
- 删远程分支不会删本地的，`git fetch -p` 清理本地残留的远程引用。
- 分支名用 `feature/xxx`、`fix/xxx` 这种前缀，协作时一眼看懂用途。
