# Git：stash，写到一半被叫去改 bug 时的救星

## 场景：手头代码没写完，线上 bug 来了

```bash
git stash          # 把工作区改动暂存，回到干净状态
git checkout main
# ... 修 bug，提交 ...
git checkout feature
git stash pop      # 把暂存的改动弹回来
```

## 常用变体

```bash
git stash -u              # 连 untracked 的新文件一起存
git stash push -m "wip: 登录页一半"  # 起个名字，好认
git stash list            # 看暂存了几份
git stash apply stash@{1} # 应用指定的一份（不删除）
git stash drop stash@{0}  # 删掉一份
```

`pop` = apply + drop，一步到位。

## 注意事项

- stash 是按"当前分支"存的，但 pop 不检查分支，
  切错分支 pop 也能成功，自己小心。
- 长期不 pop 的 stash 会变成垃圾，定期 `list` 清理。
- 如果改动已经值得一个 commit，直接 commit 别 stash，
  `git commit -m "wip"` 以后还能 amend。

小结：stash 是"临时停车场"，不是"长期仓库"。
