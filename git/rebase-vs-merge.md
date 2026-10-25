# Git：rebase 和 merge 到底选哪个

## merge：保留分叉历史

```bash
git checkout main
git merge feature
```

产生一个 merge commit，历史是真实的"分叉又汇合"。
适合**公共分支**（main/develop），因为不改写已发布的历史。

## rebase：把提交"搬"到最新

```bash
git checkout feature
git rebase main
```

把 feature 上的提交一个个 cherry-pick 到 main 最新处，
历史变成一条直线，干净。

## 我的习惯

- 个人功能分支同步主干：`rebase`，历史清爽，review 好看。
- 合进主干、发布版本：`merge --no-ff`，保留"这里合过一个功能"的记录。
- **已经 push 到公共仓库的提交，别 rebase**，
  会改写历史，队友的本地分支全乱。

## rebase 冲突了怎么办

```bash
git status            # 看冲突文件，手动改好
git add <file>
git rebase --continue # 继续搬下一个提交
git rebase --abort    # 搞砸了，直接放弃回原样
```

记住 `--abort` 这颗后悔药，rebase 就没那么可怕了。
