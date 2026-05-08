---
name: git-commit-split
description: Git Commit 拆分分析与执行
---

# Git Commit Split Skill

分析 staged 文件，判断是否需要拆分 commit，生成拆分方案并执行。

## 拆分优先级（从高到低）

1. **dt-common 与业务代码混合** → 必须拆
2. **global 配置变更** → 必须拆
3. **大文件变更** → 建议拆（提供代码行数）
4. **重构代码和新功能混在一起** → 建议拆

## 拆分流程

对每一批 commit 执行：

```bash
# 1. 移除本批不需要的文件
git restore --staged <不属于本批的文件>

# 2. 确认当前 staged
git diff --staged --name-only

# 3. 执行 commit
git commit -m "<type>(<scope>): <message>"

# 4. 将下一批文件加入 staged
git add <下一批文件>

# 5. 重复直到完成
```

## 用户采纳后选项

- **直接拆分执行**：自动执行拆分流程（不执行 push）
- **仅生成 message**：只输出每批 commit message

## 输出

- 需拆分的数量及原因
- 每个 commit message 及对应文件列表
- dt-common 同步提示（如涉及）

> ⚠️ 无论何种情况，**绝对不能执行 git push**。