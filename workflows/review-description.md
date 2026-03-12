# Workflow: 审查 Skill Description

<required_reading>
先读取这些参考文件：
1. references/description-patterns.md
2. references/anti-patterns.md
</required_reading>

<process>
## Step 1: 获取 Skill 信息

请用户提供 skill 路径或名称，然后读取其 SKILL.md 的 YAML frontmatter。

```bash
head -20 ~/.openclaw/workspace/skills/{skill-name}/SKILL.md
```

## Step 2: 解析 Description

从 frontmatter 提取 `description` 字段，分析是否包含三要素：

| 要素         | 检查点                 | 状态 |
|--------------|------------------------|------|
| **能做什么** | 有明确说明核心价值吗？ | ⬜    |
| **核心能力** | 列出具体功能了吗？     | ⬜    |
| **激活条件** | 有触发短语/操作吗？    | ⬜    |

## Step 3: 检查常见问题

逐项检查反模式：

| 检查项                            | 结果 |
|-----------------------------------|------|
| 是否太模糊（如 "Helps with X"）？ | ⬜    |
| 是否缺少触发条件？                | ⬜    |
| 是否过于技术化（没有用户视角）？  | ⬜    |
| 是否使用第一/第二人称？           | ⬜    |
| 是否有 skill 间边界不清的问题？   | ⬜    |

## Step 4: 评估触发边界

分析：
- 这个 skill 的**核心场景**是什么？
- 有哪些**边缘场景**可能被误触发？
- 有哪些**相似 skill** 可能竞争触发？
- 是否需要**负向触发**说明？

## Step 5: 产出审查报告

格式：
```markdown
## Skill Description 审查报告

### 基本信息
- **Skill**: {name}
- **当前 Description**: ...

### 三要素检查
| 要素     | 状态 | 说明 |
|----------|------|------|
| 能做什么 | ✅/❌  | ...  |
| 核心能力 | ✅/❌  | ...  |
| 激活条件 | ✅/❌  | ...  |

### 反模式检查
- ✅/❌ 问题1...
- ✅/❌ 问题2...

### 触发边界分析
- 核心场景: ...
- 边缘场景: ...
- 潜在冲突 skill: ...

### 改进建议
1. ...
2. ...

### 建议的新 Description
```yaml
description: >
  ...
```
```

## Step 6: 询问是否套用

如果用户同意，帮忙更新 SKILL.md 的 description。
</process>

<success_criteria>
- [ ] 已读取并解析 skill 的 description
- [ ] 完成三要素和反模式检查
- [ ] 分析了触发边界
- [ ] 提供具体改进建议和新 description 范本
- [ ] 用户确认后套用修改（可选）
</success_criteria>
