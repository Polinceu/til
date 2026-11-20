# Git：push 基础

```bash
git push origin main
git push -u origin main     # 第一次推，记下上游分支，以后直接 git push
git push origin :old-branch # 删除远端分支（冒号前面空着）
```

- `-u` 绑定上游分支，之后 `git push` 不用每次写分支名。
- 推送被拒绝多半是远端有新提交，先 `git pull` 再推。
- 删远端分支用 `git push origin :分支名`，冒号语法容易忘，记下来。
