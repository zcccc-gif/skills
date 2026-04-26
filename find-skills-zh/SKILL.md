---
name: find-skills-zh
description: "帮助用户发现和安装 agent 技能。当用户问'如何做 X'、'找一个 X 的技能'、'有没有可以做 X 的技能'、或表达对扩展功能的兴趣时使用此技能。当用户寻找可能作为可安装技能存在的功能时使用。"
---

# 查找技能

此技能帮助你从开放的 agent 技能生态系统中发现和安装技能。

## 何时使用此技能

当用户：
- 问"如何做 X"，其中 X 可能是已有技能的常见任务
- 说"找一个 X 的技能"或"有没有 X 的技能"
- 问"你能做 X 吗"，其中 X 是专业功能
- 表达对扩展 agent 功能的兴趣
- 想搜索工具、模板或工作流程
- 提到希望在特定领域获得帮助（设计、测试、部署等）

## 什么是技能 CLI？

技能 CLI (`npx skills`) 是开放 agent 技能生态系统的包管理器。技能是扩展 agent 功能的模块化包。

**关键命令：**

- `npx skills find [query]` - 交互式或按关键词搜索技能
- `npx skills add <package>` - 从 GitHub 或其他来源安装技能
- `npx skills check` - 检查技能更新
- `npx skills update` - 更新所有已安装的技能

**浏览技能：** https://skills.sh/

## 如何帮助用户查找技能

### 步骤 1：理解需求

当用户寻求帮助时，识别：
1. 领域（如 React、测试、设计、部署）
2. 具体任务（如写测试、创建动画、审查 PR）
3. 这是否是常见任务，可能已有技能存在

### 步骤 2：先检查排行榜

在运行 CLI 搜索之前，检查 [skills.sh 排行榜](https://skills.sh/) 查看是否有知名技能。

例如，Web 开发的顶级技能：
- `vercel-labs/agent-skills` — React、Next.js、Web 设计（每个 100K+ 安装）
- `anthropics/skills` — 前端设计、文档处理（100K+ 安装）

### 步骤 3：搜索技能

如果排行榜没有覆盖用户需求，运行查找命令：

```bash
npx skills find [query]
```

例如：
- 用户问"如何让我的 React 应用更快？" → `npx skills find react performance`
- 用户问"能帮我审查 PR 吗？" → `npx skills find pr review`
- 用户问"我需要创建一个变更日志" → `npx skills find changelog`

### 步骤 4：推荐前验证质量

**不要仅基于搜索结果推荐技能。** 始终验证：

1. **安装数量** - 优先选择 1K+ 安装的技能。100 以下需谨慎。
2. **来源声誉** - 官方来源（`vercel-labs`、`anthropics`、`microsoft`）比未知作者更可信。
3. **GitHub 星标** - 检查源仓库。来自 <100 星仓库的技能应持怀疑态度。

### 步骤 5：向用户展示选项

找到相关技能后，向用户展示：
1. 技能名称和功能
2. 安装数量和来源
3. 可运行的安装命令
4. 了解更多链接

示例回复：

```
找到一个可能有帮助的技能！"react-best-practices" 技能提供
来自 Vercel Engineering 的 React 和 Next.js 性能优化指南。
（185K 安装）

安装命令：
npx skills add vercel-labs/agent-skills@react-best-practices

了解更多：https://skills.sh/vercel-labs/agent-skills/react-best-practices
```

### 步骤 6：提供安装

如果用户想继续，可以为他们安装：

```bash
npx skills add <owner/repo@skill> -g -y
```

`-g` 标志全局安装，`-y` 跳过确认提示。

## 常见技能类别

| 类别 | 示例查询 |
|------|----------|
| Web 开发 | react, nextjs, typescript, css, tailwind |
| 测试 | testing, jest, playwright, e2e |
| DevOps | deploy, docker, kubernetes, ci-cd |
| 文档 | docs, readme, changelog, api-docs |
| 代码质量 | review, lint, refactor, best-practices |
| 设计 | ui, ux, design-system, accessibility |
| 生产力 | workflow, automation, git |

## 有效搜索技巧

1. **使用具体关键词**："react testing" 比 "testing" 更好
2. **尝试替代术语**：如果 "deploy" 不行，试试 "deployment" 或 "ci-cd"
3. **检查热门来源**：许多技能来自 `vercel-labs/agent-skills` 或 `ComposioHQ/awesome-claude-skills`

## 未找到技能时

如果没有相关技能：
1. 确认未找到现有技能
2. 提供直接帮助完成任务
3. 建议用户可以用 `npx skills init` 创建自己的技能

示例：

```
搜索了与 "xyz" 相关的技能，但没有找到匹配项。
我仍然可以直接帮你完成这个任务！你想让我继续吗？

如果这是你经常做的事情，可以创建自己的技能：
npx skills init my-xyz-skill
```
