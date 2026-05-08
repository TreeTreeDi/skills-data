---
name: git-conflict-resolve
description: Git 冲突检测与解决
---

# Git Conflict Resolve Skill

检测、解决和验证 Git 合并冲突。

## 检测冲突

```bash
# 合并前检查是否有冲突
git fetch origin <target-branch>
git merge origin/<target-branch> --no-commit --no-ff

# 或在 MR 中查看
git fetch origin
git log --oneline --left-right HEAD...origin/<branch>
```

## 解决低版本合并高版本冲突流程

```bash
# 1. 基于 release 分支拉取 conflict 分支
git checkout tag/release_7.0.x
git pull
git checkout -b tag/conflict_7.0.x_{id}

# 2. 拉取目标分支并合并
git fetch origin tag/release_6.4.x
git merge origin/tag/release_6.4.x

# 3. 编辑冲突文件，解决冲突标记
# <<<<<<< HEAD
# 你的修改
# =======
# 目标分支的修改
# >>>>>>>

# 4. 标记冲突已解决
git add <resolved-files>

# 5. 完成合并提交
git commit -m "conflict(scope): resolve conflicts with release/7.0.x"

# 6. 推送到远程
git push origin tag/conflict_7.0.x_{id}
```

## 验证冲突已解决

```bash
# 检查冲突文件列表（应为空）
git diff --check

# 验证合并结果
git log --oneline -3
git show --stat HEAD
git status
```

## 放弃合并

```bash
git merge --abort
git reset --hard ORIG_HEAD
```