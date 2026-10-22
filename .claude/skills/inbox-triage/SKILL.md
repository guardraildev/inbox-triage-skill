---
name: inbox-triage
description: Run when the user asks to triage, clean, check, or sort their inbox or unread mail. Reads unread mail, groups duplicates, proposes reply / later / noise, and marks noise as read only after the user approves.
---

## Guardrails

- Never send, reply to, or forward mail from this skill.
- Never archive or delete. The only write action is "mark as read" on messages the user approved.
- Never-noise list (always goes to "reply" or "later", regardless of content):
  - subject or body contains: invoice, contract, payment, security alert, password
  - calendar invitations
  - mail from a sender the user replied to in the last 30 days

## Steps

1. Fetch unread mail from the last 24 hours.
2. Group messages by normalized subject (strip "Re:", "Fwd:", ticket numbers). Same subject from different senders is one group.
3. For each group, pick one bucket:
   - **Reply** — asks the user a question, assigns them a task, or is from a person waiting on them
   - **Later** — informational but relevant; newsletters the user opens; threads they are cc'd on
   - **Noise** — automated notifications, marketing, duplicates of something already in Reply/Later
   Apply the never-noise list before deciding.
4. Show a table: group, count, bucket, one-line reason, link to the newest message. Then stop and ask: "Mark the Noise groups as read?"
5. Only if the user says yes: mark every message in the Noise groups as read. Report the count.
