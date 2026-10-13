# Git：cherry-pick，把单个提交"摘"过来

## 场景：main 上的热修复，想合到 release 分支

```bash
git checkout release
git cherry-pick a1b2c3d   # 把 main 上的某个提交摘过来
```

只拿**一个**提交，不像 merge 会把整个分支历史带过来。

## 一次摘多个

```bash
git cherry-pick a1b2c3d e4f5g6h   # 逐个摘
git cherry-pick a1b2c3d^..e4f5g6h # 摘一个区间（左开右闭）
```

## 冲突处理和 rebase 一套

```bash
# 冲突了：改好文件
git add <file>
git cherry-pick --continue
git cherry-pick --abort   # 后悔药
```

## 和 rebase 的关系

rebase 本质上就是"自动 cherry-pick 一串提交"。
理解了 cherry-pick，rebase 就不神秘了。

## 什么时候用

- 热修复要同步到多个发布分支。
- 别人分支上有个提交你也想要，但不想 merge 整个分支。

注意：摘过来的提交会有**新的 hash**，
原提交和摘过来的提交 Git 认为是两个提交，别重复 merge。
