# Deep Research Skill

> 系统化的多角度、双语联网调研方法论 —— 一次搜索永远不够。

**English below ⬇️**

---

## 这是什么

`deep-research` 是一个面向 AI 编码助手（如 Claude Code、CodeBuddy 等）的 **Skill**，为「联网调研」提供一套可执行的系统化方法论。

普通的网页搜索往往是「一次浅搜 + 直接作答」，而本 Skill 约束 AI 完成**四个阶段的完整调研流程**：广泛探索 → 深入挖掘 → 多样性与交叉验证 → 综合自检，确保在进入内容创作之前，已经从多个角度、多个层次、多个来源收集了足够的信息。

## 核心特性

- 🔍 **四阶段调研方法论** — 从摸清版图到定向深挖，逐层推进，拒绝一搜即答
- 🌐 **双语检索策略** — 英文查询串为主（覆盖一手信源）、中文查询串补充（覆盖本地语境），并给出不同议题类型的语言配比判定表
- ⏱️ **时间意识** — 构造查询前必须核对当前日期，「今天 / 本周 / 最新 / 今年」对应不同精度的查询写法，避免漏掉时效信息
- ✅ **综合自检清单** — 6 项检查全部通过才允许进入内容生成阶段
- 🧭 **术语转换规范** — 先从权威中文来源提取官方英文术语再展开英文检索，避免硬译导致检索方向跑偏
- 📊 **六类信息覆盖** — 事实数据、实例案例、专家观点、趋势预测、横向对比、挑战批评，一个都不能少

## 适用场景

**调研类问题**

- 「X 是什么」「解释一下 X」「调研一下 X」「查一查 X」
- 需要来自多个来源的、当前的、全面信息的问题
- 单次网页搜索不足以妥善作答的问题

**内容创作前预研**

- 制作演示文稿（PPT / 幻灯片）
- 设计前端页面或 UI 原型
- 撰写文章、报告或文档
- 制作视频或多媒体内容

## 安装

### 方式一：手动安装

将本仓库克隆或复制到你的 Skill 目录：

```bash
# 用户级（全局可用）
git clone https://github.com/<your-username>/deep-research-skill.git \
  ~/.workbuddy/skills/deep-research

# 或项目级（仅当前项目）
git clone https://github.com/<your-username>/deep-research-skill.git \
  <your-project>/.workbuddy/skills/deep-research
```

目录结构：

```
deep-research/
├── SKILL.md    # Skill 本体：完整方法论与触发规则
└── README.md   # 本文件
```

> 只要你的 Agent 框架支持以 `SKILL.md` 为核心的 Skill 加载机制（frontmatter 含 `name` 与 `description`），即可直接使用，无需额外配置。

### 方式二：作为子模块

```bash
git submodule add https://github.com/<your-username>/deep-research-skill.git \
  .workbuddy/skills/deep-research
```

## 工作原理

加载后，Skill 会接管 AI 的联网调研行为，按以下流程执行：

```
用户提问
   │
   ▼
┌─────────────────────────────────┐
│ ① 广泛探索                       │  宽泛搜索摸清格局，提炼关键维度
├─────────────────────────────────┤
│ ② 深入挖掘                       │  逐维度定向检索，抓取全文，顺藤摸瓜
├─────────────────────────────────┤
│ ③ 多样性与交叉验证                │  六类信息全覆盖，中英文来源并行
├─────────────────────────────────┤
│ ④ 综合自检                       │  6 项检查全部通过？
└─────────────────────────────────┘
   │ 否 → 回到检索
   ▼ 是
进入内容创作阶段
```

### 双语检索判定表（节选）

| 议题特征 | 检索策略 |
|---------|---------|
| 技术、学术、前沿研究 | 英文为主（70–80%） |
| 全球市场、跨国企业、宏观趋势 | 英文为主 |
| 中国政策、A股、国内市场数据 | 中文为主（60–70%） |
| 国内产品、本地落地、区域案例 | 中文为主 |
| 中外对比类话题 | 双语均衡 |

### 综合自检清单

- [ ] 至少从 3–5 个不同角度做了检索？
- [ ] 已抓取并通读最重要的信息源全文？
- [ ] 掌握了具体的数据、实例和专家观点？
- [ ] 既了解积极面，也了解挑战／局限？
- [ ] 信息是最新的，且来自权威来源？
- [ ] 同时覆盖了英文与中文来源？

**任何一项为「否」→ 继续调研，不开始生成内容。**

## 使用示例

安装后无需任何手动调用，Skill 会在以下场景自动触发：

```
用户：帮我调研一下 AI 在医疗领域的应用现状
       → 触发四阶段调研：英文为主 + 中文补充，覆盖诊断/治疗/监管/伦理等维度

用户：写一篇关于 RAG 技术趋势的文章
       → 创作前预研：先完成完整调研，再动笔

用户：latest on enterprise AI adoption？
       → English triggers 同样生效："what is X", "research X", "deep dive into X"…
```

## 兼容性

- 任何支持 `SKILL.md` 规范（frontmatter: `name` + `description`）的 Agent / Skill 框架
- 无外部依赖、无需 API Key —— 纯方法论 Skill，复用宿主环境自带的搜索与网页抓取能力

## License

MIT

---

## English Introduction

`deep-research` is an agent **Skill** that replaces shallow one-shot web searches with a systematic, multi-perspective, **bilingual (English + Chinese) research methodology**.

It enforces a four-phase pipeline — **Broad Exploration → Deep Dive → Diversity & Cross-Validation → Synthesis Check** — and gates content generation behind a 6-item self-check list. Queries are primarily written in English (broader index coverage, better primary sources) with parallel Chinese queries for local context, and temporal-awareness rules keep results fresh ("today" vs "this week" vs "this year").

**Use cases:** research questions ("what is X", "compare X and Y", "latest on X") and pre-research before any content creation (slides, articles, reports, UI prototypes).

**Install:** clone into your skills directory (e.g. `~/.workbuddy/skills/deep-research` or `<project>/.workbuddy/skills/deep-research`). Works with any framework that loads skills from a `SKILL.md` frontmatter file. No dependencies, no API keys.

License: MIT
