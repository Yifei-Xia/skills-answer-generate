# skills-answer-generate

# Answer Quality Eval

Evaluate the content quality of AI-generated answers based on user queries.

## Overview

A systematic quality evaluation framework for AI-generated answers in search scenarios. Outputs structured scores and improvement suggestions. Designed for search product operations teams to conduct quality audits, batch evaluations, and optimization strategy planning.

## Evaluation Dimensions

| Dimension | Default Weight | Description |
|-----------|---------------|-------------|
| Relevance | 25% | How well the answer matches the query intent |
| Accuracy | 30% | Factual correctness, no AI hallucinations |
| Completeness | 20% | Whether key information is sufficiently covered |
| Readability | 15% | Clear expression, well-organized structure |
| Safety | Veto | No harmful or non-compliant content |
| Timeliness | 10% | Whether information is up-to-date |

Weights are dynamically adjusted based on query type. See [STANDARDS.md](STANDARDS.md) for details.

## Category Risk Classification

| Risk Level | Categories | Veto Rules |
|-----------|------------|------------|
| High-risk | Medical, Legal, Political, Financial | Safety Fail OR Accuracy ≤ 2 → Score = 0 |
| Time-sensitive | Breaking news, Social issues, Sports events | Safety Fail OR Timeliness ≤ 2 → Score = 0 |
| Standard | Factual Q&A, How-to guides, Encyclopedia, etc. | Safety Fail only → Score = 0 |

## Usage

Provide the following to trigger an evaluation:

1. **User query** (required)
2. **Generated answer content** (required)
3. **Query type** (optional, auto-detected if not provided)

Supports both single and batch evaluations. Batch evaluations include per-category dimension breakdowns and an exploratory analysis report.

## Quality Grades

| Grade | Score Range | Action |
|-------|-----------|--------|
| Excellent | 4.0 - 5.0 | Display directly |
| Acceptable | 3.0 - 3.9 | Normal display |
| Borderline | 2.5 - 2.9 | Downgrade or manual review |
| Unacceptable | < 2.5 | Do not display, fallback to traditional results |

## File Structure

```
answer-quality-eval/
├── SKILL.md          # Main file: evaluation workflow, scoring system, output templates
├── STANDARDS.md      # Detailed standards: weight adjustments, veto rules, scoring anchors
├── examples.md       # Examples: various scenario cases and batch summary format
├── README.md         # Chinese README
├── README_EN.md      # English README
└── versions/
    └── v1/           # v1 archive
```

## Changelog

- **v1**: Initial version with six-dimension evaluation system, category risk classification (accuracy/timeliness veto), per-category batch breakdowns, and exploratory analysis


# Answer Quality Eval - 生成答案质量评估

根据用户 query 评估 AI 生成答案的内容质量。

## 功能简介

对搜索场景中 AI 生成的答案进行系统化质量评估，输出结构化评分和改进建议。适用于搜索产品运营对生成答案进行质量审核、批量评估或制定优化策略。

## 评估维度

| 维度 | 默认权重 | 说明 |
|------|---------|------|
| 相关性 | 25% | 答案与 query 的匹配程度 |
| 准确性 | 30% | 事实正确、无 AI 幻觉 |
| 完整性 | 20% | 信息覆盖是否充分 |
| 可读性 | 15% | 表达清晰、结构合理 |
| 安全性 | 一票否决 | 无有害/违规内容 |
| 时效性 | 10% | 信息是否过时 |

权重会根据 query 类型动态调整，详见 [STANDARDS.md](STANDARDS.md)。

## 类目风险分级

| 风险等级 | 适用类目 | 一票否决规则 |
|---------|---------|------------|
| 高风险 | 医疗、法律、时政、金融 | 安全性 Fail 或准确性 ≤ 2 → 总分归 0 |
| 时效敏感 | 时事热点、社会议题、赛事 | 安全性 Fail 或时效性 ≤ 2 → 总分归 0 |
| 常规 | 事实问答、操作指南、知识百科等 | 仅安全性 Fail → 总分归 0 |

## 使用方式

提供以下信息即可触发评估：

1. **用户 query**（必须）
2. **生成答案内容**（必须）
3. **query 类型**（可选，未提供时自动判断）

支持单条评估和批量评估，批量评估会按类目拆分各维度平均分，并输出探索分析报告。

## 质量定级

| 等级 | 分数范围 | 处理建议 |
|------|---------|----------|
| 优质 | 4.0 - 5.0 | 直接展示 |
| 合格 | 3.0 - 3.9 | 正常展示 |
| 边缘 | 2.5 - 2.9 | 降级展示或人工审核 |
| 不合格 | < 2.5 | 不展示，回退传统结果 |

## 文件结构

```
answer-quality-eval/
├── SKILL.md          # 主文件：评估流程、评分体系、输出模板
├── STANDARDS.md      # 评估标准细则：权重调整、否决规则、评分锚点
├── examples.md       # 评估示例：各类场景案例和批量汇总格式
├── README.md         # 中文说明
├── README_EN.md      # English README
└── versions/
    └── v1/           # v1 版本存档
```

## 版本记录

- **v1**：初始版本，包含六维度评估体系、类目风险分级（准确性/时效性一票否决）、批量评估按类目拆分、探索分析
