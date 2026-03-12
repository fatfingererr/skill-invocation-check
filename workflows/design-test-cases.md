# Workflow: 设计触发测试用例

<required_reading>
先读取：
1. references/evaluation-metrics.md
2. templates/test-case-template.json
</required_reading>

<process>
## Step 1: 理解 Skill 定位

读取目标 skill 的 SKILL.md，回答：
- 这个 skill 的**核心任务**是什么？
- **典型用户**会怎么描述需求？
- 有哪些**相邻领域**容易混淆？

## Step 2: 设计应触发案例（8-10 条）

**覆盖维度：**
- 正式表述（"请帮我做 X"）
- 口语表述（"X 一下""搞个 X"）
- 隐含意图（没直接提 skill 名但显然需要）
- 带上下文（有文件路径、前因后果）
- 错字/缩写（真人会打错）

**示例：**
```json
{
  "query": "我们项目要把 LESS 换成 PostCSS，有 200 多个文件，怎么迁移风险最低？",
  "should_trigger": true,
  "rationale": "明确的 CSS 迁移需求，符合 skill 核心场景"
}
```

## Step 3: 设计不应触发案例（8-10 条）

**重点选择：**
- 共享关键词但实际需要别的工具
- 触及 skill 领域但处于不该触发的上下文
- 相邻 skill 的核心场景

**常见错误：选太容易的反例**
- ❌ "写一个斐波那契函数"（作为 CSS 迁移 skill 的反例毫无价值）
- ✅ "项目已经用 PostCSS 了，想加 px-to-viewport 插件"（同领域但不该触发）

## Step 4: 标注理由

每个 test case 必须附上 `rationale`：
- 为什么应该/不应该触发
- 测试的是 description 的哪个面向

## Step 5: 组装评测集

输出格式：
```json
{
  "skill_name": "less-to-postcss",
  "description_version": "v1.0",
  "created_at": "2026-03-10",
  "test_cases": [
    {
      "id": 1,
      "query": "...",
      "should_trigger": true,
      "rationale": "...",
      "category": "formal|informal|implicit|contextual|typo"
    }
  ]
}
```

## Step 6: 存储评测集

建议路径：
```
~/.openclaw/workspace/skills/{skill-name}/eval/
├── trigger-test-cases.json
└── trigger-results/
    └── {date}-run.json
```
</process>

<design_principles>
## 测试用例设计原则

### 真实性
测试 query 越像真人说的话，评测结果越有参考价值：
- 带文件路径
- 带个人上下文
- 带前因后果
- 甚至带拼写错误

### 边界测试
最有意义的反例是：
- 共享关键词但需要不同工具
- 在 skill 领域边缘但不该触发

### 平衡性
- 应触发：8-10 条
- 不应触发：8-10 条
- 覆盖不同表述风格
</design_principles>

<success_criteria>
- [ ] 理解了 skill 的核心定位和边界
- [ ] 设计了 8-10 条应触发案例（覆盖多种表述）
- [ ] 设计了 8-10 条不应触发案例（选近似场景）
- [ ] 每个 case 都有明确 rationale
- [ ] 评测集已存档
</success_criteria>
