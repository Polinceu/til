# Git：worktree 可以同时检出多个分支

```bash
git worktree add ../hotfix hotfix-branch
git worktree list
git worktree remove ../hotfix
```

- 修线上 bug 时不用 stash 当前改动、不用切分支，直接开一个 worktree 干活。
- 每个 worktree 有独立的工作区，但共享同一个 `.git` 对象库。
- 用完记得 `git worktree remove`，光删目录会留下残留记录，要用 `git worktree prune` 清理。
