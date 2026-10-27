# Worked example: the claimed $78k runaway-agent bill

This is a worked example of the template in this repo. It is filled in from **public, self-reported claims** in one Hacker News thread. The root cause is **not verified**. Every fact below is attributed, and nothing is asserted about what happened inside the agents.

Source: https://news.ycombinator.com/item?id=49861047

## 1. Summary

The HN poster, who says he is CTO of the affected company, reports unexplained agent charges taken across 20 days in July and August. He says no user prompt asked for 823 agents or for work needing 2130 billion tokens. Status: **unresolved, root cause unknown** (reported to the Italian Police and the GDPR authority, per the poster).

## 2. Impact (as claimed)

| Field | Value | Source |
|---|---|---|
| Duration | ~20 days (July-August) | poster |
| Agents created | 823 | poster |
| Tokens | 2130 billion | poster |
| Card limit | 50K/month, then a second card was used | poster |
| Verified by a third party | No | - |

## 3. Timeline

Only what the poster states. A real postmortem would add timestamps from provider logs and billing exports.

- July-August: charges accumulate over ~20 days.
- The poster says the tool's UX gave no feedback on what the agents were doing and showed no consumption metrics.
- After the card limit was reached, the poster says, another card was used.
- Later: reported to police and the data-protection authority.

## 4. Detection

**How was it detected?** By the charges, after the fact.
**How should it have been detected?** On day 1, by a usage alert or a hard spend cap.

## 5. Blast radius

What the agent setup could reach, as described: billing, and more than one company payment card. A commenter (verdverm) asked why agents had credentialed access that could affect which card was charged. That question is the core finding of this example.

## 6. Contributing factors (hypotheses, not findings)

- No provider-side hard spend cap, or a cap above the card limit.
- No concurrency cap on agent creation.
- No human acknowledgement above a usage threshold (commenter blooalien: pause and email a human at a sane default).
- Billing credentials reachable from the agent's environment.
- No visibility into running agents or token use.

## 7. Action items

| # | Action | Type | Owner | Due |
|---|---|---|---|---|
| 1 | Only use vendors that support hard billing limits (commenter verdverm: otherwise 'instant disqualification') | prevent | platform | before next deploy |
| 2 | Set a daily token budget and alert at 50% / stop at 100% | detect + mitigate | platform | this week |
| 3 | Cap concurrent agents per task | prevent | platform | this week |
| 4 | Remove payment and billing credentials from every agent environment | prevent | security | today |
| 5 | Require a human ack to exceed any threshold | mitigate | on-call | this week |

Minimal local budget check (generic example):

```python
import json, sys
BUDGET = 5_000_000  # tokens per day
used = sum(json.loads(l)["tokens"] for l in open("usage-today.jsonl"))
if used >= BUDGET:
    sys.exit(f"STOP: {used} tokens >= daily budget {BUDGET}")
print(f"ok: {used}/{BUDGET}")
```

## 8. What went well / what to learn

The poster escalated to authorities and published details, which lets others check their own setups. The lesson for any team: decide your spend cap, concurrency cap and credential boundary **before** an agent runs unattended.

---

Format model: Anthropic's public postmortem style, https://www.anthropic.com/research/april-23-postmortem

Want the extended pack (severity rubric, cost-incident and data-leak variants, customer-comms templates)? https://renevibe76.gumroad.com/l/mmuky?ref=postmortem-example