# Git：合并冲突，别慌，三步走完

冲突不是事故，是 Git 在问你"同一行两个人改了，听谁的"，按流程处理就行。

## 标准流程

```bash
git pull          # 或者 git merge / git rebase，出现 CONFLICT
git status        # 看哪些文件冲突（both modified）
# 打开文件，找到 <<<<<<< ======= >>>>>>> 标记，手动选一边或合并
git add <冲突文件>
git commit        # merge 场景：提交这次合并
# rebase 场景：git rebase --continue
```

## 冲突标记长这样

```
<<<<<<< HEAD
print("a")
=======
print("b")
>>>>>>> feature
```

`=======` 上面是当前分支的内容，下面是对方分支的，删掉标记、留想要的。

## 退路

- `git merge --abort`：合并还没完成时，整个撤回。
- `git rebase --abort`：rebase 中途撤回，回到 rebase 之前。
- 冲突文件只想全要对方的：`git checkout --theirs <文件>` 再 `git add`；
  全要自己的：`--ours`。用之前确认一次，别拿错方向。
