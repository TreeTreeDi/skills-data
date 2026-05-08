---
name: git-commit-message
description: Git Commit Message 生成与校验
---

# Git Commit Message Skill

校验和生成符合规范的 commit message。

## 格式

`<type>(<scope>): #<id>, <commit message>`

| 字段 | 说明 |
|------|------|
| **type** | `feat`, `fix`, `hotfix`, `docs`, `style`, `refactor`, `test`, `build`, `ci`, `chore` |
| **scope** | 必须匹配 appName（或为 global / dt-common） |
| **#id** | 从分支名末段数字提取；hotfix 必须带 id；feat/fix 可省略 |
| **commit message** | 英文，≤80 字符 |

## 示例

```
feat(dataAssets): #1234, add user authentication feature
fix(console): #5678, resolve memory leak in data processor
chore(global): update dependencies and refactor build config
feat(dt-common): #1231, add shared date picker component
```

## 规则

- 当前分支为 main / release → 禁止直接 commit
- 检测并提示 dt-common 同步需求
- **绝对不能执行 git push**

## type 推断

- 新功能 → feat
- Bug 修复 → fix
- 紧急线上问题 → hotfix
- 配置/依赖 → chore / build
- 重构 → refactor

## scope 推断

- `apps/<appName>/*` → scope = appName
- `packages/dt-common/*` → scope = dt-common
- 根目录配置 → scope = global