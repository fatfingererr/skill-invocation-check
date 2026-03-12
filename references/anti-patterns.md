# Description 常见错误与修正

<overview>
收集常见的 description 反模式及其修正方案。
</overview>

<anti_pattern name="too-vague">
## 反模式：太模糊

**问题：**
```yaml
description: Helps with projects.
```

**为什么有问题：**
- 「projects」太通用，几乎什么都能匹配
- 缺少具体能力说明
- 缺少触发条件

**修正：**
```yaml
description: >
  管理 GitHub 项目，包括 issue 分类、PR 审查流程、release 规划。
  当用户提到「GitHub issue」「PR 流程」「发版计划」时使用。
```
</anti_pattern>

<anti_pattern name="missing-trigger">
## 反模式：缺少触发条件

**问题：**
```yaml
description: Creates sophisticated multi-page documentation systems with advanced formatting.
```

**为什么有问题：**
- 说明了能力，但没说什么时候该用
- Agent 无法判断何时加载

**修正：**
```yaml
description: >
  创建多页面文档系统，支持进阶格式化、交叉引用、目录生成。
  当用户要求「建立文档网站」「生成技术手册」「整理成文档」
  或提到「Docusaurus」「GitBook」时使用。
```
</anti_pattern>

<anti_pattern name="too-technical">
## 反模式：过于技术化

**问题：**
```yaml
description: Implements the Project entity model with hierarchical parent-child relationships using recursive CTE queries.
```

**为什么有问题：**
- 全是实现细节，没有用户视角
- 用户不会说「recursive CTE queries」
- 缺少自然语言触发词

**修正：**
```yaml
description: >
  处理项目阶层结构，支持父子关系、树状展示、递归查询。
  当用户要求「整理项目结构」「建立阶层」「显示项目树」时使用。
```
</anti_pattern>

<anti_pattern name="wrong-pov">
## 反模式：错误的人称

**问题：**
```yaml
description: I can help you analyze CSV files and create beautiful charts.
```

**为什么有问题：**
- 使用第一人称「I」
- 使用第二人称「you」
- 不符合 skill description 规范

**修正：**
```yaml
description: >
  分析 CSV 文件并生成可视化图表。当用户上传 .csv 文件
  或要求「分析数据」「生成图表」时使用。
```
</anti_pattern>

<anti_pattern name="no-boundary">
## 反模式：边界不清

**问题：**
```yaml
description: 数据分析和可视化工具。
```

**为什么有问题：**
- 「数据分析」范围太广
- 可能和其他数据相关 skill 竞争
- 没有说明何时用、何时不用

**修正：**
```yaml
description: >
  高级数据分析，包括统计建模、回归分析、聚类。
  当用户要求「深度分析」「建立模型」时使用。
  不要用于简单的数据浏览（使用 data-viz skill）。
```
</anti_pattern>

<anti_pattern name="trigger-in-body">
## 反模式：触发条件写在 Body

**问题：**
```yaml
---
description: 处理 PDF 文件。
---

# PDF Processor

## When to use
使用这个 skill 当用户要求转换 PDF、提取文字、合并文件时。
```

**为什么有问题：**
- 「When to use」写在 Body 里
- Body 是触发**后**才加载的
- Agent 在判断是否触发时看不到这些信息

**修正：**
```yaml
---
description: >
  处理 PDF 文件，包括格式转换、文字提取、文件合并。
  当用户上传 .pdf 文件或要求「转换 PDF」「提取文字」「合并文件」时使用。
---

# PDF Processor

## Instructions
...
```
</anti_pattern>

<anti_pattern name="keyword-stuffing">
## 反模式：关键词堆砌

**问题：**
```yaml
description: >
  数据分析数据可视化数据处理数据清洗数据转换数据建模
  数据预测数据报告数据dashboard数据API数据整合。
```

**为什么有问题：**
- 没有自然语言结构
- 重复堆砌降低可读性
- Agent 可能无法正确理解

**修正：**
```yaml
description: >
  全流程数据处理，从清洗、分析到可视化。支持预测建模、
  报告生成、Dashboard 创建。当用户提到「处理数据」「分析数据」
  「生成报告」「建立 Dashboard」时使用。
```
</anti_pattern>

<fix_checklist>
## 修正检查清单

修正 description 时确认：
- [ ] 核心价值清楚（能做什么）
- [ ] 能力具体（不是泛泛的「helps with」）
- [ ] 有触发条件（什么时候用）
- [ ] 触发词包含用户视角表述
- [ ] 使用第三人称
- [ ] 若有相邻 skill，有边界说明
- [ ] 长度适中（80-150 字）
</fix_checklist>
