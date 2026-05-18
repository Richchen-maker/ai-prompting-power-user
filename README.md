# AI Prompting Power User

Turn rough requirements into copy-ready, high-quality prompts for AI agents.

This OpenClaw/Codex skill helps transform vague ideas into executable prompt specifications with clear context, workflow, critique behavior, output format, validation rules, and handoff requirements.

## What It Does

- Reconstructs the user's real intent before writing the prompt.
- Routes tasks by type: research, coding, writing, decision, multimodal, source-grounded, or agent engineering.
- Adds explicit scope, length, tone, tool triggers, validation, and stop/ask rules.
- Produces an Agent Prompt Pack that can be pasted into another AI agent.
- Includes stronger Claude Code task prompts with planning, review, and verification gates.

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

## Privacy

This repository contains only generic skill instructions, examples, and templates. It does not include private keys, personal paths, credentials, proprietary datasets, or user-specific configuration.

## License

MIT License. See [LICENSE](LICENSE).
