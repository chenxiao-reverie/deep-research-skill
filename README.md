<div align="center">

# 🔍 Deep Research

**一次搜索远远不够 —— 让 Agent 学会「系统地调研」**

[![License: MIT](https://img.shields.io/badge/License-MIT-5D9A5B?style=flat-square)](https://opensource.org/licenses/MIT)
[![Skill](https://img.shields.io/badge/Skill-Agent%20Skills-6C5CE7?style=flat-square)](https://code.claude.com/docs/en/skills)
[![Platform](https://img.shields.io/badge/platform-40%2B%20agents-FF6B6B?style=flat-square)](#安装)
[![Deps](https://img.shields.io/badge/dependencies-none-2ECC71?style=flat-square)](#安装)
[![i18n](https://img.shields.io/badge/i18n-bilingual-F39C12?style=flat-square)](#双语检索策略)

一个开源的 **Agent Skill**，用四阶段方法论 + 双语检索策略，把「随便搜两下就回答」变成「系统调研后再回答」。

[English](#english) · [安装](#安装) · [工作原理](#工作原理) · [方法论](#四阶段方法论)

</div>

---

## 为什么需要它

大模型联网调研最常见的失败模式，不是「搜不到」，而是**搜得不够就急着答**：

| 典型症状 | 后果 |
|---------|------|
| 搜 1–2 次就收工 | 结论片面，只覆盖了一个切面 |
| 只看搜索摘要，不读全文 | 丢失关键限定条件与上下文 |
| 全程只查一种语言 | 漏掉一手信源，或漏掉本地语境 |
| 问「今天的新闻」却只搜年份 | 时效性信息完全错位 |
| 调研还没做完就开始写 | 内容空洞、经不起追问 |

这个 Skill 不提供任何工具，而是**约束 Agent 的行为**：什么时候必须继续检索、什么时候才算调研完成。

---

## 核心特性

| | 特性 | 说明 |
|---|------|------|
| 🎯 | **四阶段方法论** | 广泛探索 → 深入挖掘 → 多样性与交叉验证 → 综合自检 |
| 🌐 | **双语检索策略** | 英文为主（一手信源）、中文为辅（本地语境），附配比判定表 |
| ⏱️ | **时间意识** | 构造查询前先核对当前日期，「今天 / 本周 / 今年」对应不同精度写法 |
| ✅ | **自检清单** | 6 项检查全部通过，才允许进入内容生成 |
| 🔤 | **术语转换规范** | 先取官方英文术语再检索，避免硬译导致整条检索线失效 |
| 📊 | **六类信息覆盖** | 事实数据 / 实例案例 / 专家观点 / 趋势预测 / 横向对比 / 挑战批评 |

---

## 安装

`SKILL.md` 是 **[Agent Skills 开放标准](https://code.claude.com/docs/en/skills)**，因此同一个文件夹可跨工具使用，无需任何改造。

### 通用方式（推荐）

多数工具都识别通用路径 `.agents/skills/`，装这里覆盖面最广：

```bash
git clone https://github.com/chenxiao-reverie/deep-research-skill.git \
  .agents/skills/deep-research
```

### 按平台安装

| 平台 | 用户级（全局可用） | 项目级（随仓库共享） |
|------|------------------|-------------------|
| **Claude Code** | `~/.claude/skills/` | `.claude/skills/` |
| **Codex CLI** | `~/.agents/skills/` | `.agents/skills/` |
| **Cursor** | `~/.cursor/skills/` | `.cursor/skills/` |
| **GitHub Copilot** | `~/.copilot/skills/` | `.github/skills/` |
| **Gemini CLI** | `~/.gemini/skills/` | `.gemini/skills/` |
| **Windsurf** | — | `.windsurf/skills/` |
| **Kiro** | — | `.kiro/skills/` |
| **OpenCode / Cline / Roo / Goose / Trae** | — | `.opencode/` · `.cline/` · `.roo/` · `.goose/` · `.trae/` |

### 作为 git submodule

团队共享同一套调研标准时：

```bash
git submodule add https://github.com/chenxiao-reverie/deep-research-skill.git \
  .agents/skills/deep-research
```

> **无依赖、无需 API Key。** 本 Skill 复用宿主环境自带的搜索与网页抓取能力，是纯方法论约束。

---

## 工作原理

```
用户提问
   │
   ▼
┌──────────────────────────────────────┐
│ ① 广泛探索                           │  摸清格局，提炼关键维度       │
├──────────────────────────────────────┤
│ ② 深入挖掘                           │  逐维度定向检索，抓取全文     │
├──────────────────────────────────────┤
│ ③ 多样性与交叉验证                    │  六类信息全覆盖，中英并行     │
├──────────────────────────────────────┤
│ ④ 综合自检                           │  6 项检查是否全部通过？      │
└──────────────────────────────────────┘
   │ 否 → 回到检索，绝不开始生成
   ▼ 是
      进入内容创作阶段
```

### 综合自检清单

调研完成的判定标准，**任何一项为「否」就继续检索**：

- [ ] 至少从 3–5 个不同角度做了检索？
- [ ] 已抓取并通读最重要的信息源全文？
- [ ] 掌握了具体的数据、实例和专家观点？
- [ ] 既了解积极面，也了解挑战与局限？
- [ ] 信息是最新的，且来自权威来源？
- [ ] 同时覆盖了英文与中文来源？

---

## 四阶段方法论

### ① 广泛探索

先用宽泛查询摸清整体格局，再从中提炼出需要深挖的子话题与不同立场。

### ② 深入挖掘

针对每个关键维度定向检索：**多种措辞**、**抓取全文**、**顺藤摸瓜**追溯来源中提及的重要资料。

### ③ 多样性与交叉验证

| 信息类型 | 目的 | 查询示例 |
|---------|------|---------|
| 事实与数据 | 提供硬证据 | `"[topic] statistics"` |
| 实例与案例 | 真实落地情况 | `"[topic] case study"` |
| 专家观点 | 权威视角 | `"[topic] expert analysis"` |
| 趋势与预测 | 未来走向 | `"[topic] trends 2026"` |
| 横向对比 | 提供替代方案 | `"[A] vs [B]"` |
| 挑战与批评 | 保持观点平衡 | `"[topic] limitations"` |

### ④ 综合自检

逐项确认后，才允许进入内容创作。

---

## 双语检索策略

**核心原则：查询串用英文，输出用中文。**

英文查询在索引覆盖、一手信源、学术与技术资料上的召回显著更好；但这不意味着放弃中文 —— 两者覆盖的是**不同的信息生态**，应当并行。

| 议题特征 | 检索策略 |
|---------|---------|
| 技术、学术、前沿研究 | **英文为主**（70–80%） |
| 全球市场、跨国企业、宏观趋势 | **英文为主** |
| 中国政策、A股、国内市场数据 | **中文为主**（60–70%） |
| 国内产品、本地落地、区域案例 | **中文为主** |
| 中外对比类话题 | **双语均衡** |

### 术语转换

用英文检索前，先确认术语的英文对照，避免译错导致整条检索线失效：

1. 先用中文搜一次，从权威来源提取**官方英文术语**
2. 再用该术语展开英文检索
3. 若是外来概念（RAG、agentic workflow、OKR），**直接用原词**，不要回译

### 时间意识

**构造查询前先查看当前日期**，按意图选择精度：

| 用户意图 | 所需精度 | 查询示例 |
|---------|---------|---------|
| 「今天 / 刚发布」 | 月 + 日 | `"tech news February 28 2026"` |
| 「本周」 | 周区间 | `"releases week of Feb 24 2026"` |
| 「最近 / 最新」 | 月 | `"breakthroughs February 2026"` |
| 「今年 / 趋势」 | 年 | `"industry trends 2026"` |

> 需精确到日时，绝不能退化成只写年份 —— 搜 `"tech news 2026"` 搜不到今天的新闻。

---

## 何时触发

**调研类问题**

- 「X 是什么」「解释一下 X」「调研一下 X」
- 需要多来源、当前、全面信息的问题
- 单次网页搜索不足以妥善作答的问题

**内容创作前预研**

- 演示文稿（PPT / 幻灯片）
- 前端页面或 UI 原型
- 文章、报告或文档
- 视频或多媒体内容

**英文触发词**：`what is X` · `explain X` · `compare X and Y` · `research X` · `latest on X` · `deep dive into X` · `investigate X`

---

## 常见错误

Skill 明确列出的反面模式：

- ❌ 搜 1–2 次就收工
- ❌ 只看搜索摘要，不读来源全文
- ❌ 面对多面议题只搜一个切面
- ❌ 忽略相反立场与争议挑战
- ❌ 明明有最新数据，却还在用过时信息
- ❌ 调研尚未完成，就开始生成内容
- ❌ 全程只查中文，漏掉英文世界的一手信源
- ❌ 全程只查英文，漏掉国内市场数据与本地语境
- ❌ 把中文术语硬译成英文去搜，导致检索方向跑偏

---

## 贡献

欢迎提交 issue 与 PR：

- **改进方法论** —— 补充新的检索策略、议题类型的语言配比
- **补充触发词** —— 让 description 覆盖更多真实使用场景
- **平台适配** —— 补充新工具的安装说明

> ⚠️ 提交 PR 前请确保 `SKILL.md` 的 YAML frontmatter 可被正常解析（描述中不要出现未加引号的「冒号 + 空格」）。

## License

[MIT](LICENSE) © chenxiao-reverie

---

<div align="center">

## English

**One search is never enough.**

</div>

`deep-research` is an open-source **Agent Skill** that teaches AI coding agents how to research systematically — and when research is actually done.

It enforces a four-phase pipeline (**Broad Exploration → Deep Dive → Diversity & Cross-Validation → Synthesis Check**) and gates content generation behind a 6-item self-check list. Queries are written primarily in **English** (broader index coverage, better primary sources) with parallel **Chinese** queries for local context. Temporal-awareness rules keep results fresh — "today" vs. "this week" vs. "this year" each require a different query granularity.

**Install:** `SKILL.md` is an [open standard](https://code.claude.com/docs/en/skills) supported by 40+ agents. Clone into the universal path:

```bash
git clone https://github.com/chenxiao-reverie/deep-research-skill.git \
  .agents/skills/deep-research
```

Or a platform-specific directory such as `~/.claude/skills/` (Claude Code), `~/.cursor/skills/` (Cursor), or `.github/skills/` (GitHub Copilot). See [安装](#安装) for the full table.

**No dependencies. No API keys.** It reuses the host agent's existing search and fetch tools — it's a behavioral constraint, not a tool.

MIT License © chenxiao-reverie