---
name: git-scenarios
description: Git 常用场景命令指南
---

# Git Scenarios Skill

常用 Git 场景的命令参考。

## 1. 获取远程 tag

```bash
# 拉取所有远程 tag
git fetch origin --tags

# 拉取指定 tag
git fetch origin tag <tag-name>

# 查看本地 tag 列表
git tag -l

# 基于 tag 创建分支
git checkout -b <new-branch> <tag-name>
```

## 2. 查看指定文件的变更记录

```bash
# 查看文件的所有变更历史
git log --oneline <file-path>

# 查看文件在特定 commit 的内容
git show <commit-hash>:<file-path>

# 查看文件在两个版本之间的差异
git diff <commit-a>..<commit-b> -- <file-path>

# 查看某行代码的最近修改
git blame <file-path> | grep "<code-line>"

# 精确定位到行号
git log -p <file-path> | grep -A 5 -B 5 "<code>"
```

## 3. 撤销已 push 的 commit

```bash
# 创建新 commit 撤销指定 commit 的变更
git revert <commit-hash>

# 撤销最近的一个 commit
git revert HEAD

# 撤销指定范围的 commits
git revert <older-commit-hash>..HEAD

# 推送到远程
git push origin <branch-name>
```

## 4. 查看两个分支的差异

```bash
# 查看分支间差异（仅文件列表）
git diff --name-status <branch-a>..<branch-b>

# 查看分支间差异（详细）
git diff <branch-a>..<branch-b>

# 查看当前分支比目标分支多了哪些 commits
git log --oneline <target-branch>..HEAD

# 查看两个分支的共同祖先之后各自的变化
git log --oneline --left-right HEAD...origin/<branch>
```

## 5. 暂存工作区

```bash
# 暂存当前工作区
git stash

# 暂存时添加描述
git stash push -m "work in progress: xxx"

# 查看暂存列表
git stash list

# 恢复最近的暂存（保留暂存记录）
git stash apply

# 恢复最近的暂存（删除暂存记录）
git stash pop

# 恢复指定的暂存
git stash apply stash@{0}

# 删除暂存
git stash drop stash@{0}
```

## 6. 查看 commit 属于哪些 tag

```bash
# 查找包含指定 commit 的所有 tag
git tag --contains <commit-hash>

# 查看某 commit 属于哪个 tag
git describe --all --tags <commit-hash>

# 查看 commit 的完整路径：属于哪些分支
git branch -a --contains <commit-hash>

# 查看两个 tag 之间的所有 commit
git log <tag-a>..<tag-b> --oneline

# 查看某 tag 之后的所有 tags
git log --oneline --after "<tag-date>" --decorate --tags
```

> 如果 commit hash 未知，可先用 `git log --oneline -n` 找到目标 commit。