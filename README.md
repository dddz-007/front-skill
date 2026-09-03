# front-skill

[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-compatible-16a34a)](https://agentskills.io/) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> 如果你让 AI 参与过前端开发，这个 Skill 值得先装：让 Agent 先想清楚、按约定实现、只改该改的，并用证据交付。

**一个覆盖前端开发全流程的跨平台 Agent Skill**，适用于 Codex、Claude Code、OpenCode、Cursor 和 Qoder。

它提供四种可复用模式：**需求分析与实施合同**、**按合同结合 UI 实现**、**单点修改**、**代码审查**。

如果你遇到过“AI 没看已有代码就重复造轮子”“改一个按钮却动了半个项目”“覆盖未提交修改”或“没有验证就说完成”，`front-skill` 就是为这类前端协作准备的。

[在线文档](https://dddz-007.github.io/front-skill/) · [30 秒开始](#30-秒开始) · [完整规则](SKILL.md) · [参与改进](CONTRIBUTING.md)

> English: `front-skill` is a cross-platform Agent Skill for the complete frontend development lifecycle—from requirement analysis and implementation contracts to UI implementation, surgical changes, and code review.

## 30 秒开始

选择你使用的平台，将仓库克隆到对应的 Skill 目录。安装后重启客户端（如平台需要），然后显式调用 `front-skill`。

| 平台 | 安装目录 | 调用方式 |
|------|----------|----------|
| Codex | `~/.agents/skills/front-skill/` | `$front-skill` |
| Claude Code | `~/.claude/skills/front-skill/` | `/front-skill` |
| OpenCode | `~/.config/opencode/skills/front-skill/` | 在提示词中点名 `front-skill` |
| Cursor | `~/.cursor/skills/front-skill/` | `/front-skill` |
| Qoder | `~/.qoder/skills/front-skill/` | `/front-skill` |

```bash
# 以 Codex 为例；其他平台只需替换目标目录
git clone https://github.com/dddz-007/front-skill.git ~/.agents/skills/front-skill
```

Windows PowerShell：

```powershell
New-Item -ItemType Directory -Force "$HOME\.agents\skills" | Out-Null
git clone https://github.com/dddz-007/front-skill.git "$HOME\.agents\skills\front-skill"
```

> Claude Code 和 Qoder 不读取 `.agents/skills`，请使用对应目录。所有平台都要求目录名为 `front-skill`，入口文件名为大写 `SKILL.md`。

## 你是否需要 front-skill？

适合安装，如果你：

- 让 AI 参与已有 Vue、React、Angular、Svelte 或小程序项目；
- 希望先分析需求和仓库，再得到清晰的实施合同；
- 需要根据 Figma、设计稿、截图或原型完成真实页面；
- 只想修改一个文件、代码块或行为，不希望范围扩大；
- 需要在提交前审查当前 Diff，并获得可核对的验证结果；
- 经常处理包含未提交代码的工作区，不希望 AI 覆盖已有修改。

它不以从零生成一次性静态页面、纯视觉创意或后端主导任务为主要目标。

## 四种工作模式

### 1. 需求分析：输出实施合同

先调查入口、数据流、组件、样式、路由、项目约定和工作区状态，再明确需求理解、验收标准、复用能力、文件边界、UI 对应关系、实施步骤和验证方案。

### 2. 按合同实现：结合 UI 完成需求

按实施合同分批修改，优先复用已有能力，结合 Figma、设计稿、截图或原型完成页面与组件，并持续检查实际 Diff 和验证结果。

### 3. 单点修改：只改该改的地方

锁定指定文件、函数、模板、样式或行为，避免无关重构、公共 API 扩散和隐式行为变化。

### 4. 代码审查：聚焦当前 Diff

审查需求覆盖、复用、修改范围、公共 API、中文编码、编译、测试、交互和视觉结果，适合提交前复查、他人改动检查和 AI 自检。

## 它改变了什么

| 常见的 AI 前端协作方式 | front-skill 的工作方式 |
|------------------------|------------------------|
| 看见需求就开始写 | 先调查仓库、设计依据与 Git 状态 |
| 直接输出代码，没有共同边界 | 先输出目标、约束、复用点、文件范围和验证方式 |
| 新写一个相似组件 | 按业务模块、公共组件、框架能力的顺序优先复用 |
| 顺手重构相邻代码 | 按明确范围做最小且完整的改动 |
| 忽略未提交代码 | 把无关变更视为用户资产并加以保护 |
| 改完即声称完成 | 聚焦实际 Diff，定向验证并如实说明未验证项 |

## 工作流

```text
调查仓库 → 建立实施边界 → 输出实施合同 → 复用现有能力 → 小步修改 → 聚焦 Diff → 定向验证 → 证据化交付
```

详细规则：

- [完整功能实施](references/feature-workflow.md)：新功能、多文件修改、完整缺陷修复；
- [单点修改](references/surgical-change.md)：单文件、单代码块、强调“只改这里”；
- [UI / Figma 还原](references/ui-figma.md)：Figma、设计稿、截图、原型或视觉还原；
- [验证与异常恢复](references/validation.md)：最终复查、交付、编辑失败、乱码或超时。

完整约束见 [SKILL.md](SKILL.md)。

## 使用示例

### 完整前端需求

```text
调用 front-skill 完成下面的前端需求。
先调查仓库和当前工作区，输出实施合同；确认后按合同结合 Figma / 截图实现，并完成定向验证。

[需求内容]
[Figma 链接、截图或其他 UI 参考]
```

### 只分析，不修改

```text
调用 front-skill 分析下面的前端需求。
本轮只调查入口、已有实现、可复用能力和设计约束，输出实施合同，不修改代码。

[需求内容或 Figma 链接]
```

### 单点修改

```text
调用 front-skill 做一个单点修改。
仅修改以下文件和指定区域，禁止修改其他行为；先检查未提交修改，完成后查看实际 Diff 并验证。

文件：[文件路径]
指定区域：[函数、模板、样式或行附近的代码]
目标参考：[参考文件、代码或设计]
```

### 代码审查

```text
调用 front-skill 审查当前工作区的实际 Diff。
本轮只审查，不修改。检查需求覆盖、复用、修改范围、公共 API、编码、编译、测试和视觉结果。
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

欢迎提交真实失败案例、平台兼容问题和工作流建议。请尽量提供原始需求、平台与版本、项目技术栈、Agent 实际与预期行为、相关 Diff / 日志 / 截图，以及是否可以稳定复现。详情见 [CONTRIBUTING.md](CONTRIBUTING.md)。

如果它帮你减少了一次误改或返工，欢迎点个 Star，并分享你的真实案例。

## License

[MIT](LICENSE)
