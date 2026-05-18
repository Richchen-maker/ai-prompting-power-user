# Examples

## Example 0 — Raw idea to understood requirement

Raw need: “我有个想法，想让 AI 帮我把每天看到的机器人新闻整理成能行动的东西。”

Requirement understanding:

```markdown
## 需求理解
- 真实目标：把零散机器人新闻转成可执行情报，而不是普通新闻摘要。
- 逻辑链：每天有信息噪音 → 需要筛选重要变化 → 关联公司/技术/产品/论文/专利 → 输出行动建议和下一步追踪。
- 任务类型：研究 + agent workflow + source-grounded report。
- 关键假设：面向中文报告；优先公开来源；需要来源链接和日期。
- 误解风险：目标 agent 可能只做新闻摘要，漏掉“行动建议、追踪对象、验证证据”。
```

Better prompt:

```text
你是机器人产业情报分析 agent。请把每天输入的机器人/具身智能/自动驾驶/无人机相关新闻，整理成可执行中文情报简报。

Scope：不要泛泛摘要；只输出值得追踪的变化、证据和行动建议。
Length：最多 10 条情报，每条不超过 120 字；附来源表。
Tool trigger：涉及最新新闻时必须搜索或读取我提供的链接；每条情报记录 URL、发布日期、访问日期。

工作流：
1. 提取新闻事实。
2. 判断它影响的公司、技术路线、产品、论文、专利或供应链。
3. 过滤低价值 PR。
4. 给出“为什么重要”和“下一步追踪什么”。
5. 标注不确定性和需要复查的来源。

输出：
- 今日 TL;DR
- 情报表：事件 / 影响对象 / 为什么重要 / 证据 / 下一步动作
- 来源表
- 明天需要继续追踪的问题
```

## Example 1 — Raw need to coding prompt

Raw need: “帮我修一下登录 bug。”

Better prompt:

```text
你是资深全栈工程师。请在当前代码库中修复“用户输入正确账号密码后偶发无法登录”的 bug。

Success criteria：新增或定位一个能复现该问题的测试；修复后运行相关测试通过；不要改动无关 UI 或认证架构。

工作流：
1. 先阅读登录流程相关文件，画出请求链路。
2. 找最小复现路径，优先检查 session/cookie/token 刷新、并发、时区、缓存。
3. 只做最小修复，不做大重构。
4. 运行测试并报告命令输出。
5. 最终说明根因、改动文件、验证结果和剩余风险。
```

## Example 2 — Raw need to research prompt

Raw need: “帮我看看这个 AI 工具值不值得用。”

Better prompt:

```text
请研究 {工具名} 是否值得在我们的 {场景} 中采用。

要求优先官方文档、GitHub、pricing、安全/隐私政策、近期用户反馈。所有事实标注来源和日期。

输出：
- 结论：采用 / 暂缓 / 不采用
- 适配我们的理由
- 成本和限制
- 安全/合规风险
- 与当前方案对比
- 7 天试用计划
- 仍需人工确认的问题
```

## Example 3 — Raw need to anti-sycophancy prompt

Raw need: “你觉得我这个方案怎么样？”

Better prompt:

```text
请像一个严格但建设性的顾问审查我的方案。不要默认同意我。

请输出：
1. 方案最强的 3 点。
2. 最脆弱的 5 个假设。
3. 如果失败，最可能因为什么失败。
4. 我忽略的替代方案。
5. 你会如何把方案缩小成 2 周可验证 MVP。
6. 需要我补充的数据。

我的方案：{粘贴方案}
```

## Example 4 — Raw need to NotebookLM/source-grounded prompt

Raw need: “根据这些资料帮我写总结。”

Better prompt:

```text
请只基于我提供/NotebookLM 中的来源回答，不要使用外部常识补全未出现的事实。

任务：把资料总结成一份 {用途} 报告。

输出：
- 5 条核心结论，每条标注来源
- 证据表：结论 / 来源 / 原文依据 / 可信度
- 资料中的矛盾或缺口
- 我下一步应该追问或补充的材料

如果资料不足，请明确说“不足以判断”，不要编造。
```

## Example 5 — Raw need to Claude 4.7-style prompt spec

Raw need: “帮我 review 这个 prompt。”

Better prompt:

```text
请把下面 prompt 当作规格书审查，而不是泛泛评价。

Scope：只检查 7 项：任务目标、输入范围、输出格式、长度上限、工具触发、语气目标、验证方式。
Positive target：用清晰、可执行、可复制的改写替代泛泛批评。
Tool trigger：不需要外部工具；若 prompt 引用了文件、链接或实时事实，再明确要求读取或搜索。
Go beyond basics：不要只指出问题，给出能直接粘贴的最小改写。

Action verbs：
1. 标出每一项缺失或含糊之处。
2. 说明它会如何导致模型误解或少做事。
3. 给出一版最小改写，不重写无关段落。

Output format：输出表格，列为：问题位置 / 问题类型 / 风险 / 最小改写。
Length cap：最多列 10 个问题；每格不超过 40 字。
Tone：直接、专业、少废话。

Prompt：{粘贴原 prompt}
```

## Example 6 — Raw need to agent engineering prompt

Raw need: “我想做一个自动研究机器人。”

Better prompt:

```text
你是 Agent Engineering 架构师。请把“自动研究机器人”设计成可执行、可评估、可逐步落地的 agent 工作流，不要一上来设计复杂平台。

Scope：只设计 MVP 工作流，不写完整代码。
Length：输出 8 个小节，每节不超过 6 条。
Positive target：给出可落地、可验证、可交接的设计。
Tool trigger：涉及最新公开资料时使用 web search；涉及已有资料时读取指定文件；每个来源记录 URL、日期和可信度。

请输出：
1. Agent Charter：使命、非目标、输入、输出、权限边界。
2. Context Plan：需要哪些主题、来源、历史记录、用户偏好；哪些不能靠记忆假设。
3. Tool Plan：search/browser/files/NotebookLM/citation/test 分别何时用。
4. Control Flow：plan → search → source ranking → synthesis → critique → verify → handoff。
5. Eval：好报告的标准、失败模式、人工验收点。
6. Observability：需要记录的假设、工具调用、来源、文件、命令、验证结果。
7. Guardrails：付费、外部发布、删除数据、抓取受限内容前必须停下来问。
8. MVP：2 天内版本和 2 周内版本。

最后给出你反对这个方案的最强理由，以及如何用一个小实验验证它是否值得继续。
```
