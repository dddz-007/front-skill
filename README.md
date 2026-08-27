# front-skill

在已有前端代码仓库中安全地分析、实现、修改和验证需求。适用于新增功能、修改功能、修复缺陷、页面与组件开发、带 Figma 或截图的 UI 还原、有限范围重构、联调前 Mock，以及后续纠错。

核心原则：**先调查、再复用、后修改**——以仓库当前约定和用户已有修改为事实来源，每次只做最小且完整的变更，并用实际证据验证结果。

适配 Vue、React、Angular、Svelte、小程序等前端项目。

## 项目结构

```text
front-skill/
├── SKILL.md                          # Skill 主入口：规则、工作流选择与交付要求
├── agents/
│   └── openai.yaml                   # Agent 界面配置（显示名、默认提示词）
└── references/
    ├── feature-workflow.md           # 新功能 / 多文件 / 完整缺陷修复流程
    ├── surgical-change.md            # 单文件 / 单代码块 / 单点修改流程
    ├── ui-figma.md                   # Figma、设计稿、截图视觉还原流程
    └── validation.md                 # 验证、复查与编码异常恢复
```

## 工作流

| 场景 | 参考文档 |
|------|----------|
| 新功能、多文件修改、完整缺陷修复 | [references/feature-workflow.md](references/feature-workflow.md) |
| 单文件、单代码块、强调「只改这里」 | [references/surgical-change.md](references/surgical-change.md) |
| 包含 Figma、设计稿、截图、原型或视觉还原 | [references/ui-figma.md](references/ui-figma.md) |
| 最终复查、交付，或编辑失败 / 乱码 / 命令超时 | [references/validation.md](references/validation.md) |

## 核心规则摘要

1. **修改前先调查** — 阅读仓库说明、Git 状态、目标文件、入口链路、同类实现和项目配置。
2. **复用优先** — 当前功能已有实现 → 同业务模块 → 公共组件 / Hook / 工具 / 样式 → 框架原生能力 → 最后才新增代码。
3. **范围受控** — 将需求转成实施边界；只做最小且完整的修改，不批量格式化无关文件。
4. **保护用户改动** — 脏工作区中的无关变更视为用户资产，不覆盖、不清理、不回退。
5. **安全编辑** — 源码优先使用局部补丁；保持文件原有编码和换行，尤其保护 UTF-8 中文。
6. **验证后再交付** — 未经用户明确要求，禁止提交、推送、创建 PR、发布或部署。

完整规则见 [SKILL.md](SKILL.md)。

## 平台兼容性

本仓库遵循 Agent Skills 的通用目录格式：`SKILL.md` 是入口，`references/` 按需提供详细工作流。无需为不同平台维护多份 Skill 内容；只需将整个仓库放入对应平台的 Skill 目录。

| 平台 | 项目级目录 | 用户级目录 | 手动调用 |
|------|------------|------------|----------|
| Codex | `.agents/skills/front-skill/` | `~/.agents/skills/front-skill/` | `$front-skill` |
| Claude Code | `.claude/skills/front-skill/` | `~/.claude/skills/front-skill/` | `/front-skill` |
| OpenCode | `.opencode/skills/front-skill/` | `~/.config/opencode/skills/front-skill/` | 在提示词中点名 `front-skill`，由 Agent 调用 `skill` 工具加载 |
| Cursor | `.cursor/skills/front-skill/` | `~/.cursor/skills/front-skill/` | `/front-skill` |
| Qoder | `.qoder/skills/front-skill/` | `~/.qoder/skills/front-skill/` | `/front-skill` |

> OpenCode 也兼容 `.agents/skills/` 和 `.claude/skills/`；Cursor 也兼容 `.agents/skills/`、`.claude/skills/` 和 `.codex/skills/`。如果同一项目需要同时支持 Codex、OpenCode 和 Cursor，可只保留一份 `.agents/skills/front-skill/`。Claude Code 和 Qoder 仍应使用各自的原生目录，或通过目录链接指向同一份 Skill。

## 安装

### 安装到用户目录

将仓库克隆到所用平台的用户级目录。以下命令任选其一：

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

用户级安装会让 Skill 对本机的所有项目生效。目标父目录不存在时，请先创建父目录。

### 安装到项目目录

如果只希望在当前项目中使用，请将本仓库的完整内容复制到上表对应的项目级目录。目录中必须保留 `SKILL.md`、`references/`；`agents/openai.yaml` 是 Codex 的可选界面元数据，其他平台会忽略它。

以 Codex、OpenCode、Cursor 共用目录为例：

```text
your-project/
└── .agents/
    └── skills/
        └── front-skill/
            ├── SKILL.md
            ├── agents/
            │   └── openai.yaml
            └── references/
                ├── feature-workflow.md
                ├── surgical-change.md
                ├── ui-figma.md
                └── validation.md
```

安装后如未出现在 Skill 列表中，请重启对应客户端，并确认目录名为 `front-skill`、入口文件名严格为大写 `SKILL.md`。

平台约定可参考官方文档：[Codex](https://learn.chatgpt.com/docs/build-skills)、[Claude Code](https://code.claude.com/docs/en/skills)、[OpenCode](https://opencode.ai/docs/skills/)、[Cursor](https://cursor.com/docs/skills)、[Qoder](https://docs.qoder.com/extensions/skills)。

## 各平台如何使用

### Codex

在 Codex CLI 或 IDE 扩展中输入 `$` 选择 Skill，或直接在提示词中调用：

```text
$front-skill 完成下面的前端需求：
[需求内容、Figma 链接或截图]
```

Codex 也会在任务与 `description` 匹配时自动加载该 Skill。

### Claude Code

```text
/front-skill 完成下面的前端需求：
[需求内容、Figma 链接或截图]
```

Claude Code 也可以根据 Skill 描述自动调用。

### OpenCode

OpenCode 将可用 Skill 暴露给 Agent，由 Agent 通过内置 `skill` 工具加载。直接描述需求并点名 Skill 即可：

```text
使用 front-skill 完成下面的前端需求：
[需求内容、Figma 链接或截图]
```

也可以只描述前端任务，让 OpenCode 根据 `description` 自动选择。普通 Agent Skill 不等同于 OpenCode 的自定义斜杠命令，因此不把 `/front-skill` 作为通用调用方式。

### Cursor

在 Agent 聊天中输入 `/` 并选择 `front-skill`，或直接输入：

```text
/front-skill 完成下面的前端需求：
[需求内容、Figma 链接或截图]
```

Cursor 也会在上下文匹配时自动应用该 Skill。

### Qoder

在 IDE 聊天、Quest 或 CLI 中调用：

```text
/front-skill 完成下面的前端需求：
[需求内容、Figma 链接或截图]
```

Qoder 也支持根据请求和 Skill 描述自动触发。

## 使用示例

### 普通前端需求

```text
调用当前平台中的 front-skill 完成下面的需求：

[需求内容]
[UI/Figma 链接或截图]
```

### 只调查，不修改

```text
调用当前平台中的 front-skill 分析下面的需求。
本轮只调查入口、已有实现和设计，输出实施合同，不修改代码。

[需求内容]
[UI/Figma 链接]
```

### 按实施合同执行

```text
调用当前平台中的 front-skill 执行下面的实施合同。
严格遵守实施范围，分批实现，每批先检查实际 Diff 和验证结果。
禁止提交、push、发布和部署。

[实施合同]
```

### 单点修改

```text
调用当前平台中的 front-skill 做一个单点修改。
仅修改以下文件和指定区域，禁止修改其他行为：

文件：
[文件路径]

指定区域：
[函数、模板、样式或行附近的代码]

目标参考：
[参考文件或代码]
```

### 审查当前 Diff

```text
调用当前平台中的 front-skill 审查当前工作区的实际 Diff。
本轮只审查，不修改。检查复用、范围、公共 API、编码、编译、测试和视觉结果。
```

## License

MIT
