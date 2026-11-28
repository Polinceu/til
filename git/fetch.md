# Git：fetch 和 pull 的区别

```bash
git fetch origin              # 只下载，不合并
git status                    # 看本地落后多少
git merge origin/main         # 手动合并
git pull origin main          # fetch + merge 一步到位
```

- `fetch` 只把远端更新拿下来，不动你的工作区，随时能看。
- `pull` 是 `fetch` + `merge`，拿下来直接合，冲突当场就要解决。
- 不确定远端改了什么时先 `fetch` 看一眼，再决定合不合。
