# Workflow: 诊断触发问题

<process>
## Step 1: 收集问题描述

询问用户：
1. 哪个 skill 有问题？
2. 用户输入了什么？
3. 预期结果是什么（应触发/不应触发）？
4. 实际结果是什么？

## Step 2: 读取 Skill Description

```bash
head -20 ~/.openclaw/workspace/skills/{skill-name}/SKILL.md
```

提取 `description` 字段。

## Step 3: 分析触发失败原因

### 情况 A：应触发但没触发（Under-triggering）

**检查清单：**
| 可能原因                   | 检查方式                                         |
|----------------------------|--------------------------------------------------|
| Description 缺少触发关键词 | 用户的 query 中的关键词有出现在 description 吗？ |
| 任务太简单                 | Agent 认为自己能直接完成，不需要 skill           |
| 触发条件写得太保守         | Description 边界太窄                             |
| 有竞争 skill               | 其他 skill 的 description 更匹配                 |

**快速调试技巧：**
直接问 Agent："你什么时候会使用 {skill-name} 这个 Skill？"
观察它的理解是否与预期一致。

### 情况 B：不应触发但触发了（Over-triggering）

**检查清单：**
| 可能原因           | 检查方式                                      |
|--------------------|-----------------------------------------------|
| Description 太模糊 | 是否用了通用词汇（helps, manages, handles）？ |
| 缺少负向触发       | 是否需要明确说"不要用于 X"？                |
| 触发条件太宽       | 列出的触发词是否过于广泛？                    |
| 和其他 skill 重叠  | 两个 skill 的领域有交集吗？                   |

## Step 4: 提出修正方案

根据诊断结果，提出具体修正：

### 针对 Under-triggering：
```yaml
# 修正前
description: 处理 CSS 迁移

# 修正后
description: >
  处理 CSS 迁移，包括 LESS/SASS 转 PostCSS、移除预处理器依赖。
  当用户提到"CSS 迁移""移除 less-loader""换成 PostCSS"
  或上传 .less/.scss 文件要求转换时使用。
```

### 针对 Over-triggering：
```yaml
# 修正前
description: 分析数据并生成报告

# 修正后
description: >
  CSV/Excel 文件的高级数据分析，包括统计建模、回归分析。
  不要用于简单的数据浏览或图表生成（使用 data-viz skill）。
```

## Step 5: 验证修正

建议用户：
1. 套用修正后的 description
2. 用原本失败的 query 重新测试
3. 再测试 2-3 个类似场景确认修正有效
</process>

<common_diagnoses>
## 常见诊断结果

### "关键词缺失"
用户的表述方式没有出现在 description 中。
**修正**：补充更多同义词和口语表述。

### "任务过简"
Agent 判断任务简单到不需要 skill。
**修正**：这是正常行为，不需要修正。

### "竞争失败"
有另一个 skill 的 description 更匹配。
**修正**：明确两个 skill 的边界，可能需要同时调整两个。

### "边界模糊"
Description 没有清楚说明何时用/何时不用。
**修正**：加入负向触发说明。
</common_diagnoses>

<success_criteria>
- [ ] 明确了问题类型（under/over-triggering）
- [ ] 找到根本原因
- [ ] 提出具体修正方案
- [ ] 用户验证修正有效
</success_criteria>
