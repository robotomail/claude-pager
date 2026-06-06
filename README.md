# claude-pager

A Claude Code skill that turns an agent into an on-call teammate. It runs a health check on a schedule, classifies each result against a runbook, and emails you only when something genuinely needs you. Reply to that email and the agent verifies your reply and acts on it.

Email runs on [Robotomail](https://robotomail.com): the agent gets its own mailbox, a send API, and a signed inbound webhook for replies, so you skip the DNS, SPF, DKIM, and deliverability setup.

## Install

Drop `SKILL.md` into your Claude Code skills directory:

```bash
mkdir -p ~/.claude/skills/claude-pager
curl -sL https://raw.githubusercontent.com/robotomail/claude-pager/main/SKILL.md \
  -o ~/.claude/skills/claude-pager/SKILL.md
```

Then ask Claude Code to "monitor my infrastructure" or "watch production and email me."

## What it does

- **A loop** — one reproducible check on a schedule, printing one status line. Quiet by default.
- **A runbook** — severity tiers, a triage tree, and a noise list, so it stays silent until something matters (and so a real customer's 404 reads as a product signal, not noise).
- **A channel** — email out via Robotomail, plus an optional verified two-way reply path: HMAC signature check, replay rejection, and thread matching before the agent acts.

The whole point is judgment, not thresholds: most runs do nothing, a small number reach you, and nothing destructive happens without a human "yes."

## Write-up

The full story and step-by-step: [I gave Claude Code a pager](https://x.com/johnjoubert/status/2063219913494253728).
