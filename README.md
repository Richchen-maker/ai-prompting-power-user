# AI Prompting Power User

Turn rough requirements into copy-ready, high-quality prompts for AI agents.

This OpenClaw/Codex skill transforms vague ideas into executable prompt specifications with clear context, workflow, critique behavior, output format, validation rules, and handoff requirements.

Most prompt libraries give you static templates. This skill acts more like a prompt architect: it reconstructs the real task, chooses the right prompt pattern, adds operational constraints, and produces a copy-ready Agent Prompt Pack that another AI agent can execute with less ambiguity.

## Core Value

- **Intent reconstruction before writing**: turns messy requests into explicit goals, assumptions, risks, and success criteria before generating the prompt.
- **Agent-ready workflow design**: adds role, scope, context plan, tool triggers, control flow, validation, handoff, and stop/ask rules.
- **Anti-sycophancy by default**: prompts the target agent to challenge weak assumptions, expose missing data, and avoid blindly agreeing.
- **Engineering-grade execution prompts**: supports coding tasks with plan, minimal patch scope, tests, security review, and verification reporting.
- **Source-grounded research prompts**: forces citations, freshness checks, uncertainty labels, and separation between evidence and inference.
- **Reusable prompt system**: includes a framework, templates, examples, and optional agent metadata so teams can adapt it instead of starting from scratch.

## Who It Is For

- Founders and operators who need to turn rough business or product ideas into executable AI-agent tasks.
- Engineers who want better prompts for Claude Code, Codex, Cursor, ChatGPT, or other coding agents.
- Researchers and analysts who need grounded reports with citations, uncertainty, and clear evidence boundaries.
- Prompt builders who want a structured way to move beyond one-line prompt tricks.

## What It Does

- Reconstructs the user's real intent before writing the prompt.
- Routes tasks by type: research, coding, writing, decision, multimodal, source-grounded, or agent engineering.
- Adds explicit scope, length, tone, tool triggers, validation, and stop/ask rules.
- Produces an Agent Prompt Pack that can be pasted into another AI agent.
- Includes stronger Claude Code task prompts with planning, review, and verification gates.
- Provides practical examples for coding, research, decision review, source-grounded synthesis, and agent workflow design.

## Output Structure

The skill usually produces:

- **Requirement Understanding**: intent, logic chain, task type, assumptions, and misunderstanding risks.
- **Agent Prompt Pack**: role, objective, inputs, constraints, workflow, output format, quality bar, and validation rules.
- **Execution Notes**: when to use tools, when to ask the user, what to verify, and how to report the result.
- **Critique Layer**: weak assumptions, missing information, and failure modes the target agent should actively check.

## Install

Copy this repository into your OpenClaw skills directory:

```bash
mkdir -p ~/.openclaw/skills
git clone https://github.com/Richchen-maker/ai-prompting-power-user.git ~/.openclaw/skills/ai-prompting-power-user
openclaw skills check
```

If your environment uses Codex skills, place the same directory under your configured skills path and restart the agent session.

## Files

- `SKILL.md` — main skill instructions.
- `references/framework.md` — underlying prompting framework.
- `references/templates.md` — reusable prompt templates.
- `references/examples.md` — example transformations.
- `agents/openai.yaml` — optional agent metadata.

## Usage

Ask your agent to use `ai-prompting-power-user` when you need to improve or generate a prompt, for example:

```text
帮我把这个需求升级成一个可复制给 Claude Code 的高质量 prompt：
我想修复登录偶发失败的问题。
```

The default output is not the answer to the task itself, but a polished prompt another agent can execute.

## Five Beginner Walkthroughs

### 1. Turn a vague coding request into a Claude Code task

Goal: get a coding agent to fix a bug without broad, risky changes.

Steps:

1. Start with the raw need: `帮我修一下登录偶发失败的问题。`
2. Ask: `Use ai-prompting-power-user to turn this into a Claude Code prompt.`
3. Add known context if available: stack, error logs, files, reproduction steps.
4. The skill will produce a prompt with success criteria, investigation workflow, minimal patch scope, tests, and final reporting requirements.
5. Paste the generated prompt into Claude Code/Codex and require it to report changed files plus verification commands.

Good final prompt behavior: the coding agent reads the login flow, reproduces or isolates the bug, makes a small fix, runs tests, and reports root cause.

### 2. Convert “research this tool” into a source-grounded evaluation

Goal: avoid shallow summaries and force evidence-backed adoption advice.

Steps:

1. Start with: `帮我看看 {工具名} 值不值得用。`
2. Specify your scenario: team size, budget, data sensitivity, existing stack.
3. Ask the skill to generate a research-agent prompt.
4. Check that the output requires official docs, pricing, GitHub or changelog, security/privacy pages, and recent user feedback.
5. Run the generated prompt in an agent with web access.

Good final prompt behavior: the research agent returns adopt / defer / reject, with sources, dates, risks, cost, alternatives, and a short trial plan.

### 3. Make an advisor challenge your plan instead of agreeing

Goal: get sharper decision feedback.

Steps:

1. Paste your plan after: `你觉得这个方案怎么样？`
2. Ask the skill to turn it into an anti-sycophancy review prompt.
3. Keep the generated sections for strengths, fragile assumptions, failure modes, alternatives, MVP, and missing data.
4. Paste the prompt and your plan into the target agent.
5. Use the output to cut the plan down to a testable next step.

Good final prompt behavior: the advisor gives direct critique, identifies hidden assumptions, and recommends a smaller validation path.

### 4. Summarize documents without hallucinated facts

Goal: force the agent to stay inside provided sources.

Steps:

1. Collect the documents or NotebookLM sources you want summarized.
2. Start with: `根据这些资料帮我写总结，但不要用外部知识补。`
3. Ask the skill to generate a source-grounded prompt.
4. Confirm the prompt requires citations for each core claim and flags missing evidence.
5. Run it against your document set.

Good final prompt behavior: the agent separates source-backed conclusions from gaps and says “insufficient evidence” when the documents do not support a claim.

### 5. Design an MVP research agent workflow

Goal: turn a broad automation idea into a buildable agent workflow.

Steps:

1. Start with: `我想做一个自动研究机器人。`
2. Add the first use case: daily news, market tracking, competitor monitoring, academic search, or internal knowledge base.
3. Ask the skill to generate an Agent Engineering prompt.
4. Use the generated sections: charter, context plan, tool plan, control flow, evals, observability, guardrails, and MVP milestones.
5. Hand the prompt to a coding or architecture agent to produce the first implementation plan.

Good final prompt behavior: the agent does not design an oversized platform; it gives a small workflow with permissions, evaluation criteria, logs, and a two-day MVP.

## Repository Layout

```text
.
├── SKILL.md
├── references/
│   ├── framework.md
│   ├── templates.md
│   └── examples.md
├── agents/
│   └── openai.yaml
├── README.md
├── LICENSE
└── CHANGELOG.md
```

## Privacy

This repository contains only generic skill instructions, examples, and templates. It does not include private keys, personal paths, credentials, proprietary datasets, or user-specific configuration.

## License

MIT License. See [LICENSE](LICENSE).
