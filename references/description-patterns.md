# Description 优秀示例库

<overview>
收集经过验证的高品质 description 示例，作为撰写和审查的参考。
</overview>

<pattern name="figma-design">
## Figma 设计交付

```yaml
description: >
  分析 Figma 设计稿并生成开发交付文档。当用户上传 .fig 文件、
  要求"设计规范"、"组件文档"或"设计转代码交付"时使用。
```

**为什么好：**
- 明确核心价值（分析设计稿 → 生成交付文档）
- 列出具体触发条件（.fig 文件、特定短语）
- 有多个触发入口
</pattern>

<pattern name="linear-workflow">
## Linear 项目管理

```yaml
description: >
  管理 Linear 项目工作流，包括迭代规划、任务创建和状态跟踪。
  当用户提到"迭代"、"Linear 任务"、"项目规划"或要求
  "创建工单"时使用。
```

**为什么好：**
- 说明具体能力（迭代规划、任务创建、状态跟踪）
- 列出用户可能的表述方式
- 覆盖正式和口语表述
</pattern>

<pattern name="css-migration">
## CSS 迁移工具

```yaml
description: >
  处理 CSS 预处理器迁移，包括 LESS/SASS 转 PostCSS、移除预处理器依赖、
  处理复杂 mixin 嵌套。当用户提到"CSS 迁移""移除 less-loader"
  "换成 PostCSS""LESS 转换"或上传 .less/.scss 文件要求转换时使用。
```

**为什么好：**
- 详细列出核心能力
- 包含技术术语和通用表述
- 支持文件类型触发
</pattern>

<pattern name="data-analysis-with-boundary">
## 数据分析（带边界说明）

```yaml
description: >
  CSV/Excel 文件的高级数据分析，包括统计建模、回归分析、聚类分析。
  当用户要求"深度分析""建立模型""找出规律"时使用。
  不要用于简单的数据浏览或基础图表生成（使用 data-viz skill）。
```

**为什么好：**
- 明确说明"进阶"定位
- 包含负向触发，避免和 data-viz 竞争
- 清楚划分边界
</pattern>

<pattern name="code-review">
## Code Review

```yaml
description: >
  执行代码审查，检查安全漏洞、性能问题、可维护性和团队规范遵循。
  当用户要求"code review""审查 PR""检查这段代码"或上传
  diff/patch 文件时支持。支持针对特定维度的审查请求。
```

**为什么好：**
- 列出审查维度
- 包含英文和中文触发词
- 支持多种输入形式
</pattern>

<pattern name="sprint-planning">
## Sprint Planning

```yaml
description: >
  协助迭代规划，包括计算团队速率、任务拆解、工时估算、风险评估。
  当用户说"规划下一个 sprint""迭代计划""这週要做什么"
  或要求"拆解任务""估算工时"时使用。
  不要用于任务状态跟踪（使用 linear-workflow skill）。
```

**为什么好：**
- 详细列出规划相关能力
- 包含正式和口语触发
- 明确和相关 skill 的边界
</pattern>

<guidelines>
## 撰写指南

### 结构模板
```yaml
description: >
  {核心价值/能做什么}，包括 {能力1}、{能力2}、{能力3}。
  当用户{触发条件1}、{触发条件2}或{触发条件3}时使用。
  [可选] 不要用于{排除场景}（使用 {其他skill}）。
```

### 触发词选择
1. **动词优先**："分析""创建""检查""迁移""规划"
2. **领域术语**："PR""sprint""PostCSS""regression"
3. **用户表述**："帮我看一下""搞个""弄一下"
4. **文件类型**：".fig"".less"".csv"

### 长度指南
- 理想长度：80-150 字
- 最短：50 字（可能遗漏触发条件）
- 最长：200 字（太长会降低匹配效率）
</guidelines>
