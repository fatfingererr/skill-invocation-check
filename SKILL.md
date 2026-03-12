---
name: skill-invocation-check
description: 检查 skill 的触发规范与质量。当用户要求审查 skill 的 description、评估触发精准度、设计触发测试用例，或诊断 skill 为何未被正确触发时使用。
---

<essential_principles>
## Skill 触发机制原理

### 三级渐进式披露
| 层级 | 内容 | 加载时机 | Token 成本 |
|------|------|---------|-----------|
| L1 | YAML `description` | 始终在系统提示词 | ~50-100 |
| L2 | SKILL.md 正文 | 匹配后才读取 | ~500-2000 |
| L3 | references/scripts | 执行时按需加载 | 依需求 |

### 触发的两个事实
1. **Agent 只在觉得搞不定时才找 Skill**：简单任务即使 description 完美匹配也可能不触发
2. **Agent 天生偏向欠触发 (under-triggering)**：Description 要写得更主动，把边界往外推

### 关键洞察
- Skill 激活消耗 **1-2 步工具调用**
- Description 准不准直接影响 **Token 消耗和响应速度**
- 误触发 = 浪费，漏触发 = 能力缺失
- 「什么时候该用」的信息**只能写在 description**，Body 是触发后才加载的

### Description 三要素
1. **能做什么**：核心价值
2. **核心能力**：具体包含哪些能力
3. **激活条件**：用户说什么话/做什么操作时触发
</essential_principles>

<intake>
你想做什么？

1. **审查 skill description** — 分析某个 skill 的触发规范是否合格
2. **设计触发测试用例** — 为 skill 建立评测集（应触发/不应触发）
3. **诊断触发问题** — 分析为何 skill 未被正确触发
4. **完整评测流程** — 执行 description 评测并产出改进建议

回复数字或描述你的需求。
</intake>

<routing>
| 回应 | 下一步 |
|-----|-------|
| 1, "审查", "review", "检查 description" | workflows/review-description.md |
| 2, "测试", "test case", "评测集" | workflows/design-test-cases.md |
| 3, "诊断", "为什么没触发", "debug" | workflows/diagnose-triggering.md |
| 4, "完整评测", "full evaluation" | workflows/full-evaluation.md |

**读取对应 workflow 后严格遵循。**
</routing>

<quick_reference>
## Description 质量检查清单

### ✅ 必须包含
- [ ] 说明**能做什么**（核心价值）
- [ ] 列出**核心能力**（具体功能）
- [ ] 明确**激活条件**（触发短语/操作）
- [ ] 使用第三人称（不用「我可以」「你可以」）

### ❌ 常见问题
| 问题 | 示例 | 影响 |
|------|------|------|
| 太模糊 | "Helps with projects" | 什么都能匹配 |
| 缺触发条件 | "Creates documentation systems" | Agent 不知何时用 |
| 过于技术化 | "Implements entity model with hierarchical relationships" | 没有用户视角触发词 |
| 第一人称 | "I can help you process files" | 不符合规范 |

### 正面示例
```yaml
description: >
  分析 Figma 设计稿并生成开发交付文档。当用户上传 .fig 文件、
  要求「设计规范」、「组件文档」或「设计转代码交付」时使用。
```

### 防止过度触发（负向触发）
```yaml
description: >
  CSV 文件的高级数据分析，包括统计建模、回归分析。
  不要用于简单的数据浏览（那个用 data-viz skill）。
```
</quick_reference>

<workflows_index>
| Workflow | 用途 |
|----------|------|
| review-description.md | 审查单一 skill 的 description 质量 |
| design-test-cases.md | 设计触发测试用例（应触发/不应触发） |
| diagnose-triggering.md | 诊断触发失败原因 |
| full-evaluation.md | 完整评测流程与迭代改进 |
</workflows_index>

<references_index>
| Reference | 内容 |
|-----------|------|
| description-patterns.md | 优秀 description 示例库 |
| anti-patterns.md | 常见错误与修正方案 |
| evaluation-metrics.md | 评测指标定义（召回率/精确率） |
</references_index>

<success_criteria>
Skill 触发检查完成的标志：
- [ ] Description 包含三要素（能做什么、核心能力、激活条件）
- [ ] 无常见反模式（太模糊、缺触发条件、过于技术化）
- [ ] 有明确的触发边界（知道何时用、何时不用）
- [ ] 若有需要，包含负向触发说明
- [ ] 评测集覆盖应触发和不应触发场景
</success_criteria>
