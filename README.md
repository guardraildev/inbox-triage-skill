# Inbox Triage Skill for Claude Code

One Skill that reads your unread mail, groups duplicates, sorts them into reply / later / noise, and marks noise as read — only after you approve.

## Requirements

- Claude Code
- A Gmail MCP connector. Tool names in `settings.json` follow the `mcp__gmail__*` pattern; rename them to match your connector.

## What's here

- `.claude/skills/inbox-triage/SKILL.md`: the Skill (trigger, guardrails, never-noise list, 5 steps)
- `.claude/settings.json`: allow read + label tools, deny send / reply / forward / trash

## Install

```bash
mkdir -p .claude/skills
cp -r .claude/skills/inbox-triage <your-repo>/.claude/skills/
cp .claude/settings.json <your-repo>/.claude/settings.json   # or merge the deny list into yours
```

## Run

```
/inbox-triage
```

## Run every morning (macOS / Linux cron)

```
0 8 * * 1-5 cd ~/inbox && claude -p "/inbox-triage" > ~/inbox/today.md
```

Edit the **never-noise list** in `SKILL.md` before the first run.
