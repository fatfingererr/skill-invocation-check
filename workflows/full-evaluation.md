# Workflow: 完整 Description 评测流程

<required_reading>
1. references/evaluation-metrics.md
2. workflows/design-test-cases.md
</required_reading>

<process>
## Phase 1: 准备

### Step 1.1: 确认评测目标
- 目标 skill 名称
- 当前 description 版本
- 评测目的（新建验证/迭代改进/问题排查）

### Step 1.2: 准备评测集
若无现成评测集，先执行 `workflows/design-test-cases.md`。

确保：
- 16-20 条测试 query
- 应触发 8-10 条 + 不应触发 8-10 条
- 每条都有 rationale

## Phase 2: 执行评测

### Step 2.1: 逐条测试

对每条 test case：
1. 将 query 发送给 Agent
2. 观察是否载入了目标 skill
3. 记录结果：`triggered` / `not_triggered`

**记录格式：**
```json
{
  "id": 1,
  "query": "...",
  "expected": true,
  "actual": true,
  "passed": true
}
```

### Step 2.2: 计算指标

| 指标 | 公式 | 意义 |
|------|------|------|
| **召回率 (Recall)** | 应触发中实际触发 / 应触发总数 | 该用的时候用了没 |
| **精确率 (Precision)** | 不应触发中正确未触发 / 不应触发总数 | 不该用的时候克制住了没 |

**目标：**
- 召回率 ≥ 80%
- 精确率 ≥ 90%

## Phase 3: 分析结果

### Step 3.1: 失败案例分析

对每个失败的 case：
1. 为什么失败？
2. 是 description 的问题还是测试 case 设计的问题？
3. 需要怎么修正？

### Step 3.2: 模式识别

看失败案例有没有共同模式：
- 某类表述风格一直失败
- 某个领域边界不清
- 和特定 skill 竞争

## Phase 4: 迭代改进

### Step 4.1: 修正 Description

根据分析结果修正：
- 漏触发居多 → 补充触发关键词，边界推宽
- 误触发居多 → 增加负向说明，收窄范围
- 两者都有 → 重新理清边界定位

**改进原则：**
- 从反馈提炼**通用规律**，不要过拟合到具体 case
- 一次只改一个维度，方便追踪效果

### Step 4.2: 重跑评测

用完整评测集重跑，对比前后得分。

### Step 4.3: 记录迭代

```markdown
## 迭代记录

### v1.0 → v1.1
- 日期: 2026-03-10
- 召回率: 60% → 80%
- 精确率: 90% → 85%
- 改动: 增加口语触发词「搞个」「弄一下」
- 副作用: 略增加误触发，可接受
```

## Phase 5: 终止条件

评测迭代可以结束当：
- 召回率 ≥ 80% 且精确率 ≥ 90%
- 连续两轮无明显改进
- 剩余失败 case 是边缘情况，投入产出比不合理
</process>

<evaluation_report_template>
## Description 评测报告

### 基本信息
- **Skill**: {name}
- **Description 版本**: {version}
- **评测日期**: {date}

### 评测结果
| 指标 | 结果 |
|------|------|
| 应触发 (n={x}) | {y}/{x} 成功 |
| 不应触发 (n={x}) | {y}/{x} 正确未触发 |
| **召回率** | {x}% |
| **精确率** | {x}% |

### 失败案例
| ID | Query | Expected | Actual | 分析 |
|----|-------|----------|--------|------|
| 3 | ... | 应触发 | 未触发 | 缺少「XXX」关键词 |

### 改进建议
1. ...
2. ...

### 建议的新 Description
```yaml
description: >
  ...
```
</evaluation_report_template>

<success_criteria>
- [ ] 准备了 16-20 条评测集
- [ ] 逐条执行测试并记录结果
- [ ] 计算召回率和精确率
- [ ] 分析失败案例并识别模式
- [ ] 提出具体改进建议
- [ ] 若迭代，记录版本变化
</success_criteria>
