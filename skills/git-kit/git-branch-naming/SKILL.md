---
name: git-branch-naming
description: Git 分支命名校验与建议
---

# Git Branch Naming Skill

校验分支命名是否符合规范，生成合规的分支名建议。

## 分支格式

`<appName>/<branchType>_<version>_<description>`

| 字段 | 可选值 |
|------|--------|
| **appName** | `dataAssets`, `console`, `batch`, `stream`, `tag`, `easyIndex`, `dataApi`, `global`, `dt-common`, `uic` |
| **branchType** | `global`, `release`, `test`, `feat`, `fix`, `hotfix`, `conflict` |
| **version** | 如 `7.0.x`、`6.4.x` |
| **description** | 小写+下划线，通常为需求/Bug ID |

> **注意**：`publicService` 和 `portal` 在 v6.4.x 及以上已整合到 `console`。

## 示例

```
console/feat_7.0.x_addGitSkill
dataAssets/fix_6.3.x_1234
tag/conflict_7.0.x_12345
dt-common/feat_14.x.y_1231
```

## 输出格式

- ✅ 合规 / ❌ 不合规 + 修正建议
- 不合规时自动生成推荐分支名

## dt-common 版本对应

| 产品版本 | dt-common 分支版本 |
|---------|------------------|
| v7.0.x  | dev_15.x.y       |
| v6.4.x  | dev_14.x.y       |
| v6.3.x  | dev_13.x.y       |
| v6.2.x  | dev_12.x.y       |
| v6.0.x  | dev_11.x.y       |

精确版本以 `packages/dt-common/package.json` 中 version 字段为准。