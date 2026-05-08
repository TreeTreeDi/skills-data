---
name: git-history-recover
description: Git 历史恢复与回退
---

# Git History Recover Skill

通过 reflog 恢复已删除的分支、误删的 commit，以及回退到指定版本。

## reflog 查找操作记录

```bash
# 查看所有操作历史（默认保留 90 天）
git reflog

# 查看特定分支的 reflog
git reflog show <branch-name>

# 格式化输出
git reflog --format="%h %s" -20
```

## 恢复已删除的分支

```bash
# 1. 查找分支被删除前的 commit hash
git reflog | grep "branch-name"

# 2. 恢复分支
git checkout -b <branch-name> <commit-hash>

# 示例
git reflog | grep "console/feat"
# 结果：abc1234 HEAD@{15}: checkout: moving from console/feat_7.0.x_1234 to master
git checkout -b console/feat_7.0.x_1234 abc1234
```

## 恢复误删的 commit

```bash
# 1. 查找丢失的 commit
git reflog | grep "commit"

# 2. 恢复指定 commit
git checkout <commit-hash>

# 或创建新分支指向该 commit
git checkout -b <new-branch-name> <commit-hash>
```

## 回退到指定版本

```bash
# 回退到指定 commit（保留工作区变更）
git reset --soft <commit-hash>

# 回退到指定 commit（保留工作区变更，取消 staged）
git reset --mixed <commit-hash>

# 回退到指定 commit（丢弃所有变更，危险操作）
git reset --hard <commit-hash>

# 回退远程分支（谨慎使用）
git push origin <branch-name> --force
```