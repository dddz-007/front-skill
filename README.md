# front-skill

[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-compatible-16a34a)](https://agentskills.io/) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> 让 AI 在已有前端项目里改得准、改得少、验得清。

[在线文档](https://dddz-007.github.io/front-skill/) · [30 秒开始](#30-秒开始) · [完整规则](SKILL.md) · [参与改进](CONTRIBUTING.md)

> GitHub Pages 直接渲染这份根目录 `README.md`，不再维护单独的文档副本。部署方法见[发布到 GitHub Pages](#发布到-github-pages)。

让 AI 修改成熟前端项目，难点往往不是“不会写代码”，而是**没查现有实现就重复造轮子、顺手改出需求范围、覆盖未提交代码、破坏中文编码，最后未经验证就宣称完成**。

`front-skill` 专门约束这些失控点：要求 Agent **先调查、优先复用、锁定范围、小步修改、验证后交付**，并为完整功能、单点修改、Figma / 截图还原和异常恢复提供针对性工作流。

一份 Skill 即可用于 **Codex、Claude Code、OpenCode、Cursor 和 Qoder**，适配 Vue、React、Angular、Svelte、小程序等已有前端项目。

## 30 秒开始

以同时兼容 Codex、OpenCode 和 Cursor 的 `.agents/skills` 目录为例：

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/dddz-007/front-skill.git ~/.agents/skills/front-skill
```

然后在对应 Agent 中发出任务。Codex 使用 `$front-skill`；Claude Code、Cursor 和 Qoder 使用 `/front-skill`；OpenCode 在提示词中点名 `front-skill`：

```text
调用 front-skill 完成下面的前端需求。
先调查已有实现和工作区改动，明确范围后再做最小修改，并完成定向验证。

[需求内容、Figma 链接或截图]
```

> Claude Code 和 Qoder 不读取 `.agents/skills`，请使用下方对应的安装目录。

## 它改变了什么

| 常见的 AI 修改方式 | front-skill 的工作方式 |
|--------------------|------------------------|
| 看见需求就开始写 | 先读取仓库约定、入口、同类实现与 Git 状态 |
| 新写一个相似组件 | 按业务模块、公共组件、框架能力的顺序优先复用 |
| 顺手重构相邻代码 | 先形成实施边界，只做最小且完整的修改 |
| 忽略未提交代码 | 把脏工作区中的无关变更视为用户资产 |
| 改完即声称完成 | 查看实际 Diff，执行定向检查，并如实说明未验证项 |

## 适合什么场景

- 已有前端仓库中的新功能、缺陷修复和有限范围重构；
- 根据 Figma、截图或原型还原页面与组件；
- 用户明确要求“只改这个文件 / 代码块 / 行为”；
- 工作区已有未提交修改，需要避免覆盖或误清理；
- 需要可核对的复用说明、修改范围与验证结果。

它不以从零生成一次性静态页面、纯视觉创意或后端主导任务为主要目标。

## 工作流

| 场景 | 参考文档 |
|------|----------|
| 新功能、多文件修改、完整缺陷修复 | [references/feature-workflow.md](references/feature-workflow.md) |
| 单文件、单代码块、强调“只改这里” | [references/surgical-change.md](references/surgical-change.md) |
| Figma、设计稿、截图、原型或视觉还原 | [references/ui-figma.md](references/ui-figma.md) |
| 最终复查、交付、编辑失败、乱码或超时 | [references/validation.md](references/validation.md) |

核心执行链路：

```text
调查仓库 → 建立实施边界 → 复用现有能力 → 小步修改 → 聚焦 Diff → 定向验证 → 证据化交付
```

完整约束见 [SKILL.md](SKILL.md)。

## 安装与调用

将完整仓库克隆到对应平台的 Skill 目录：

| 平台 | 用户级目录 | 项目级目录 | 显式调用 |
|------|------------|------------|----------|
| Codex | `~/.agents/skills/front-skill/` | `.agents/skills/front-skill/` | `$front-skill` |
| Claude Code | `~/.claude/skills/front-skill/` | `.claude/skills/front-skill/` | `/front-skill` |
| OpenCode | `~/.config/opencode/skills/front-skill/` | `.opencode/skills/front-skill/` | 在提示词中点名 `front-skill` |
| Cursor | `~/.cursor/skills/front-skill/` | `.cursor/skills/front-skill/` | `/front-skill` |
| Qoder | `~/.qoder/skills/front-skill/` | `.qoder/skills/front-skill/` | `/front-skill` |

```bash
# Codex
git clone https://github.com/dddz-007/front-skill.git ~/.agents/skills/front-skill

# Claude Code
git clone https://github.com/dddz-007/front-skill.git ~/.claude/skills/front-skill

# OpenCode
git clone https://github.com/dddz-007/front-skill.git ~/.config/opencode/skills/front-skill

# Cursor
git clone https://github.com/dddz-007/front-skill.git ~/.cursor/skills/front-skill

# Qoder
git clone https://github.com/dddz-007/front-skill.git ~/.qoder/skills/front-skill
```

OpenCode 也兼容 `.agents/skills/` 和 `.claude/skills/`；Cursor 也兼容 `.agents/skills/`、`.claude/skills/` 和 `.codex/skills/`。安装后若未出现，请重启客户端，并确认目录名为 `front-skill`、入口文件名为大写 `SKILL.md`。

## 使用示例

以下示例使用“调用 front-skill”作为平台中性写法；实际显式调用语法以上表为准。

### 普通前端需求

```text
调用 front-skill 完成下面的需求：

[需求内容]
[UI / Figma 链接或截图]
```

### 只调查，不修改

```text
调用 front-skill 分析下面的需求。
本轮只调查入口、已有实现和设计，输出实施合同，不修改代码。

[需求内容]
[UI / Figma 链接]
```

### 按实施合同执行

```text
调用 front-skill 执行下面的实施合同。
严格遵守实施范围，分批实现，每批先检查实际 Diff 和验证结果。
禁止提交、push、发布和部署。

[实施合同]
```

### 单点修改

```text
调用 front-skill 做一个单点修改。
仅修改以下文件和指定区域，禁止修改其他行为：

文件：[文件路径]
指定区域：[函数、模板、样式或行附近的代码]
目标参考：[参考文件或代码]
```

### 审查当前 Diff

```text
调用 front-skill 审查当前工作区的实际 Diff。
本轮只审查，不修改。检查复用、范围、公共 API、编码、编译、测试和视觉结果。
```

## 项目结构

```text
front-skill/
├── SKILL.md                          # Skill 主入口
├── agents/openai.yaml                # Codex 可选界面元数据
└── references/
    ├── feature-workflow.md           # 完整功能实施流程
    ├── surgical-change.md            # 单点修改流程
    ├── ui-figma.md                   # UI / Figma 还原流程
    └── validation.md                 # 验证与异常恢复
```

## 参与改进

欢迎提交真实失败案例、平台兼容问题和工作流建议。为了让规则能针对实际行为迭代，请尽量提供“原始需求、Agent 的错误行为、技术栈和相关 Diff”。详情见 [CONTRIBUTING.md](CONTRIBUTING.md)。

如果它帮你减少了一次误改或返工，欢迎点个 Star，并分享你的真实案例。

## 发布到 GitHub Pages

本仓库使用根目录单一文档源：`README.md` 负责内容，根目录 `index.html` 负责页面展示。无需维护 `docs/` 副本。

手动发布步骤：

1. 将本地修改 push 到 `master` 分支。
2. 打开 GitHub 仓库的 **Settings → Pages**。
3. 在 **Build and deployment** 中选择 **Deploy from a branch**。
4. 选择分支 `master` 和目录 `/(root)`，点击 **Save**。
5. 等待 GitHub Actions 完成部署，访问 `https://dddz-007.github.io/front-skill/`。

以后只需修改根目录 `README.md` 并重新 push，Pages 会自动显示最新内容。

## License

[MIT](LICENSE)
