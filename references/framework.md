# AI Prompting Power User Framework

## 1. Power-user mental model

A high-quality prompt is a work delegation, not a magic sentence. It gives the target agent:

- clear mission;
- sufficient context;
- input material;
- constraints and boundaries;
- evaluation criteria;
- required reasoning/critique behavior;
- output format;
- validation method.

For Claude 4.7-style models, treat the prompt as an interface contract. Do not rely on the model to infer missing scope, length, tool use, or tone.

## 2. Default work-delegation workflow

Before writing the final prompt, map the task into seven decisions:

| Decision | Required output in the prompt |
|---|---|
| Requirement understanding | intent, logic chain, hidden task type, material ambiguities, assumptions, risk |
| Information route | stable knowledge / current web facts / deep research / high-stakes evidence chain |
| Briefing | goal, context, materials, constraints, audience, success criteria |
| Spec contract | scope, length, positive target, action verbs, tool triggers, tone |
| Thought partner | critique, weak assumptions, counterarguments, alternatives, uncertainty |
| Agent engineering | charter, context plan, tool plan, control flow, permissions, eval, observability, handoff |
| Validation | citations, tests, commands, screenshots, review gates, or human acceptance checklist |

If a row is irrelevant, omit it deliberately. Do not leave it implicit for important tasks.

## 3. Requirement Understanding Gate

When the raw input is an idea or rough expression, first translate it into a requirement map:

```text
Intent: what the user wants to accomplish.
Logic chain: why → what must be true → what the target agent must do → how success is checked.
Hidden task type: research / writing / decision / coding / multimodal / agent workflow / hybrid.
Material ambiguity: missing facts that change the prompt.
Assumptions: defaults safe enough to proceed.
Risk: likely failure if the target agent misreads the request.
```

Only ask a question if the ambiguity makes the prompt dangerous or unusable. Otherwise include assumptions in the prompt pack and continue.

## 4. Claude 4.7 prompt-spec rules

Apply this overlay before choosing any larger framework:

1. **Scope**: name every output, order, boundary, and whether rules apply to all items.
2. **Length**: define the format and cap: bullets, table columns, sections, word/paragraph/count limits.
3. **Positive target**: describe the desired behavior; pair any "do not" with the replacement behavior.
4. **Action verbs**: use concrete verbs: extract, rank, compare, verify, rewrite, generate, test, report.
5. **Tool trigger**: state when to browse/search/read files/run tests, source priority, and evidence count.
6. **Tone**: specify audience, voice, warmth/directness, and examples when style matters.
7. **Go beyond basics**: for creative/open-ended tasks, request real-deliverable polish and define what polish means.

## 5. Andrew Ng course principles distilled

### Finding Information

First classify information freshness:

- Stable knowledge: model knowledge is acceptable.
- Current fact: require browsing and dates.
- Deep comparison: require multi-source research.
- High-stakes fact: require primary sources and explicit uncertainty.

Prompt clause:

```text
先判断这个任务是否依赖最新信息。若依赖，请优先查官方/一手来源，标注发布日期和访问日期；不要把模型记忆当作事实。
```

### AI as a Thought Partner

Require the agent to be more than a compliant generator:

```text
不要默认同意我。请指出我的薄弱假设、可能失败点、反例、替代方案，以及你会如何改进这个请求。
```

### Multimedia and Code

Modern prompting includes files, screenshots, tables, PDFs, repos, and execution traces. Require:

- what to inspect;
- what evidence to extract;
- how to validate;
- how to iterate after screenshots/errors/results.

## 6. Claude Code quality fusion

For coding or repo prompts, include:

- Success criteria: command or observable result.
- Surgical scope: only change what the request needs.
- Simplicity: no speculative abstraction.
- Plan: for multi-file or risky work.
- TDD/characterization: when fixing bugs or implementing behavior.
- Review: code review, security, and regression checks.
- Verification: exact commands to run.

Useful clause:

```text
每一行改动都必须能追溯到当前请求；不要顺手重构、改格式或加未来扩展点。完成标准是验证命令通过，而不是“看起来完成”。
```

## 7. Agent Engineering fusion

For autonomous/agentic prompts, include:

- Agent charter: role, mission, non-goals, inputs, outputs.
- Context plan: files, docs, memory, source material, state, and what must not be assumed.
- Tool plan: browser, filesystem, GitHub, NotebookLM, tests, database, MCP, and exact triggers.
- Control flow: plan → execute → observe → critique → verify → handoff.
- Permissions: ask before destructive/external/paid/production/security-sensitive actions.
- Observability: log assumptions, commands, files touched, sources used.
- Eval: acceptance criteria, failure modes, regression checks, and human acceptance points.
- Handoff: concise final report with artifacts and next steps.

Useful clause:

```text
请先给出任务分解和验收标准；执行中记录关键假设、工具调用、修改文件、验证结果；遇到破坏性/外部可见/付费/生产操作先暂停请求确认。
```

## 8. Prompt quality checklist

A prompt is strong if it answers:

1. Did we correctly understand the user's intent and logic?
2. What exactly should the agent deliver?
3. What context/material must it use?
4. What should it not do?
5. Does it need latest sources?
6. How should it challenge the user/request?
7. What output structure is required?
8. How can the result be verified?
9. When must it stop and ask?
10. Are scope, length, positive target, action verbs, tool rules, tone, and polish explicit where relevant?
11. For agentic work, are charter, context, tools, control flow, permissions, eval, observability, and handoff explicit?
