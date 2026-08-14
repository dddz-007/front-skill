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

## 安装

将本仓库克隆或复制到 Cursor Skills 目录，例如：

```text
~/.cursor/skills/front-skill/
```

或在 Cursor 设置中通过 Skill 路径引用本仓库。

## 如何使用

### 普通前端需求

```text
使用 $front-skill 完成下面的需求：

[需求内容]
[UI/Figma 链接或截图]
```

### 只调查，不修改

```text
使用 $front-skill 分析下面的需求。
本轮只调查入口、已有实现和设计，输出实施合同，不修改代码。

[需求内容]
[UI/Figma 链接]
```

### 按实施合同执行

```text
使用 $front-skill 执行下面的实施合同。
严格遵守实施范围，分批实现，每批先检查实际 Diff 和验证结果。
禁止提交、push、发布和部署。

[实施合同]
```

### 单点修改

```text
使用 $front-skill 做一个单点修改。
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
使用 $front-skill 审查当前工作区的实际 Diff。
本轮只审查，不修改。检查复用、范围、公共 API、编码、编译、测试和视觉结果。
```

## License

MIT
