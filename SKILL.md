---
name: ai-prompting-power-user
description: Transform a raw idea, vague requirement, or rough user need into a high-quality, copy-ready prompt for another AI agent. Use when the user asks to write, improve, polish, upgrade, or generate a prompt; when they want a prompt for Claude Code, Codex, ChatGPT, Gemini, NotebookLM, an autonomous coding agent, research agent, writing agent, or multimodal agent; or when they ask for Claude 4.7/Opus 4.7 prompt specs, scope/length/tool/tone control, Andrew Ng prompting, agent engineering, Claude Code quality rules, best practices, anti-sycophancy, planning, critique, validation, or prompt engineering.
---

# AI Prompting Power User

## Purpose

Convert the user's rough requirement into a **copy-ready Agent Prompt Pack** that another intelligent agent can execute, verify, challenge, and hand off with high-quality results. In Chinese terms: upgrade raw needs into **可执行、可验证、可反驳、可交接**的 Agent Prompt 规格书.

Fuse four operating systems:

1. **Andrew Ng 2026 prompting**: task + context + sources + constraints + output format + critique + iteration.
2. **Claude Code quality engineering**: success criteria, plan, surgical scope, tests, review, security, verification.
3. **Agent Engineering**: agent charter, tool/context routing, control flow, evals, observability, handoff, human approval gates.
4. **Claude 4.7 prompt specs**: explicit scope, length caps, positive targets, action verbs, tool triggers, tone control, creative polish.

Do **not** merely answer the user's task unless they explicitly ask. The default output is a prompt they can paste into another agent.

## Requirement Understanding Gate

When the user gives an idea, messy expression, or vague requirement, the first job is **not** to write the final prompt. First reconstruct what they mean.

Always create an internal interpretation before the copy-ready prompt:

1. **Intent** — what outcome the user actually wants.
2. **Logic chain** — why this matters, what must happen first, what depends on what.
3. **Hidden task type** — research, writing, decision, coding, multimodal, agent workflow, or hybrid.
4. **Missing/ambiguous inputs** — facts that would materially change the prompt.
5. **Assumptions** — reasonable defaults if asking would slow the task down.
6. **Risk** — what could go wrong if the target agent misunderstands.

Ask the user only when ambiguity would make the resulting prompt dangerous or unusable. Otherwise state assumptions briefly in `## 使用说明` and proceed.

## Claude 4.7 prompt-spec overlay

Treat every generated prompt as an **interface contract**, not a chat hint. Newer Claude-style agents follow prompts more literally: if the scope, output cap, tool rule, or tone is missing, assume the target agent may not infer it.

Apply these 7 rules to every copy-ready prompt:

1. **Scope** — name every deliverable, order, boundary, and whether the rule applies to all items.
2. **Length** — define format and caps: sections, bullets, table columns, word/paragraph/count limits.
3. **Positive target** — prefer "write in plain, concrete language" over only "don't use jargon"; pair any prohibition with the desired replacement.
4. **Action verbs** — use concrete verbs such as extract, rank, compare, verify, rewrite, generate, test, and report.
5. **Tool trigger** — state when to browse/search/read files/run tests, source priority, and evidence count; if no tools are needed, say so.
6. **Tone** — specify audience, voice, directness/warmth, and examples when style matters.
7. **Go beyond basics** — for creative/open-ended work, explicitly request real-deliverable polish and define what "polish" means for the domain.

## Default delegation algorithm

For every non-trivial prompt, convert the raw need through this sequence:

1. **Understand first** — reconstruct intent, logic chain, hidden task type, ambiguity, assumptions, and risk.
2. **Route information** — stable knowledge / current fact / multi-source research / high-stakes evidence chain.
3. **Brief the agent** — goal, context, materials, constraints, output contract, and success criteria.
4. **Specify execution** — action verbs, workflow, tool triggers, permissions, and stop/ask rules.
5. **Add thought-partner behavior** — require critique, weak assumptions, counterarguments, alternatives, and uncertainty.
6. **Close the engineering loop** — validation, eval, observability, handoff, and next iteration after screenshots/errors/results.

Do not let "automatic" imply hidden capability. If a prompt says a tool, hook, source, memory, or agent will be used automatically, state the trigger and verification path.

## Mandatory Claude Code quality command chain

When the **target agent is Claude Code** (explicitly named by the user, implied by a project path/repo task, or selected via the `Coding / Claude Code` route), the generated copy-ready prompt **MUST begin with a Claude Code quality command block before the actual task prompt**.

Do not bury this in explanations or final notes. Put it at the very top of `## 可复制 Prompt` so the user sees it before the task body.

Required shape:

````markdown
### ① 先逐条执行 Claude Code 高质量命令

> 每条命令单独发送，等返回后再发下一条；不要把多条 slash commands 一次性多行粘贴。

第 1 条：

```text
/clear <short-task-slug>
```

第 2 条：

```text
/model opus
```

第 3 条：

```text
/effort max
```

第 4 条：

```text
/status
```

第 5 条：

```text
/plan
```

如果任务是高风险、复杂、多文件、架构规划、根因分析、硬件验证、长文档综合任务，并且用户明确想用远程深度计划，可改用：

```text
/ultraplan <把下面完整任务 Prompt 粘在这里>
```

注意：`/ultraplan` 不是开关命令；不能只输出单独一行 `/ultraplan`。它必须后接 prompt，或让用户在普通 `/plan` 模式中执行任务。

### ② 再粘贴任务 Prompt

```markdown
ultrathink

<actual task prompt begins here>
```
````

Inside the actual Claude Code task prompt, always include:

- Confirmation requirements for `/model`, `/effort`, `/status`, and `/plan` or `/ultraplan`.
- A plan-first gate: plan/research before file edits; no direct implementation unless the user asked for quick trivial work.
- Review/self-check commands near the end when supported: `/diff`, `/simplify`, `/review`, `/security-review`, and `/ultrareview` for major/high-risk work.
- A final report section named `Claude Code 质量命令执行记录`, listing which commands were executed, which were unavailable, and what replaced them.
- A rule that unavailable commands must be verified with `/help`, `claude --help`, or `/status`; never invent command results.

Anti-patterns to avoid:

- Do **not** only write `think hard` or `ultrathink` without `/model` + `/effort` + plan gate.
- Do **not** put `/model`, `/effort`, `/status`, `/plan` in a single multi-line command payload that Claude Code could parse as one command argument.
- Do **not** output `/ultraplan` as a standalone setup command.
- Do **not** omit the post-work quality commands and final quality-command execution record for Claude Code prompts.

## Core workflow

### 1. Interpret the raw need

Extract:

- **Goal**: what the user wants the target agent to produce.
- **Target agent**: Claude Code, Codex, ChatGPT, Gemini, NotebookLM, research agent, coding agent, writing agent, multimodal agent, or unspecified.
- **Inputs**: files, links, screenshots, codebase, docs, source material, constraints.
- **Risk level**: low / medium / high, based on money, time, code changes, security, legal/medical/financial, production impact.
- **Freshness need**: whether the task requires current web facts.
- **Deliverable**: report, plan, code patch, PR, prompt, table, deck, doc, app, analysis, email, etc.
- **Spec controls**: exact scope, output length/format cap, positive style target, required tools, tone, and whether creative polish is needed.
- **Agent loop**: tool plan, permissions, critique gate, eval/validation, observability log, and handoff shape.

Ask a clarification only if a missing fact would make the generated prompt dangerous or unusable. Otherwise make reasonable assumptions and include them in the prompt.

### 2. Choose the prompt route

Use the smallest route that covers the task:

| Route | Use for | Must include |
|---|---|---|
| Research | news, market, docs, competitors, courses, tools | source priority, dates, uncertainty, citations |
| Coding / Claude Code | bugfix, feature, refactor, tests, repo work | success criteria, scope boundaries, commands, review/security gates |
| Agent engineering | autonomous workflows, agents, tools, MCP, hooks | charter, tools, control flow, evals, handoff |
| Writing / editing | articles, docs, emails, scripts, summaries | audience, voice, source facts, anti-AI-style rules |
| Decision / strategy | options, tradeoffs, plans, architecture | assumptions, criteria, options matrix, dissent |
| Multimodal / data | screenshots, images, PDFs, spreadsheets, charts | what to inspect, evidence, extraction format, validation |
| Source-grounded / NotebookLM | user-provided docs or notebooks | answer only from sources, cite gaps, ask follow-ups |

For hybrid tasks, combine routes explicitly.

### 3. Produce an Agent Prompt Pack

Use this output shape unless the user asks for a different format:

```markdown
## 需求理解
- 我理解你的真实目标是：<intent>
- 逻辑链：<why → constraints → deliverable → validation>
- 我采用的假设：<only material assumptions>

## 可复制 Prompt

<one complete prompt the user can paste into another agent>

## 使用说明
- 适合发给：<target agent>
- 需要附带：<files/links/screenshots/context>
- 如果目标 agent 支持工具：<browser/tests/NotebookLM/GitHub/etc.>

## 质量检查
- <3-7 checks to confirm the prompt is strong>
```

Inside the copy-ready prompt, include these sections in natural language:

1. **Role / mission** — who the target agent should act as.
2. **Context** — user background, project, source material, constraints.
3. **Task** — precise deliverable.
4. **Workflow** — step-by-step execution path.
5. **Quality bar** — how to judge good work.
6. **Anti-sycophancy** — require the agent to challenge weak assumptions.
7. **Output format** — exact structure.
8. **Validation** — commands, citations, test plan, or acceptance criteria.
9. **Stop / ask rule** — when to ask clarifying questions instead of guessing.
10. **Literal controls** — explicit scope, caps, tool triggers, tone, and creative-polish target.
11. **Agent loop** — tool plan, permission boundary, observability, eval, handoff, and iteration after feedback.

### 4. Apply quality gates

Before finalizing, check the generated prompt against:

- **Context complete enough**: goal, background, inputs, constraints, output format.
- **Freshness routed**: current facts require browsing or official sources.
- **Critique included**: target agent must identify weak assumptions and alternatives.
- **Validation included**: tests, source citations, replayable commands, or acceptance criteria.
- **Scope controlled**: no unrequested overengineering; every action must trace to the request.
- **Literal-spec complete**: scope, length cap, positive target, action verbs, tool trigger, tone, and polish rule are explicit where relevant.
- **Agent loop closed**: tool plan, permissions, critique, eval/validation, observability, and handoff are explicit for autonomous or multi-step work.
- **Human gates included**: destructive, paid, external, production, or security-sensitive actions require approval.

If a prompt fails a gate, revise it before showing the user.

## Route-specific details

Load only the reference file needed:

- For the full framework and checklist, read `references/framework.md`.
- For copy-ready prompt skeletons, read `references/templates.md`.
- For realistic before/after examples, read `references/examples.md`.

## Default style

- Write final outputs in Chinese unless the user asks otherwise.
- Keep the copy-ready prompt direct, explicit, and pasteable.
- Prefer one strong prompt over many vague alternatives.
- If useful, include variables like `{项目路径}` or `{附加资料}` for the user to fill in.
- Do not mention copyright unless the user asks for copying protected content; focus on building a legal, high-quality prompt.
