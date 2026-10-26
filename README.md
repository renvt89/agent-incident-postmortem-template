# Agent Incident Postmortem Template (free)

A one-page, **blameless** postmortem template for incidents caused or worsened by an AI agent: a coding agent that deleted files, a support bot that promised a refund, an autonomous workflow that looped and burned budget.

It is a **free template only**. It is not legal, compliance or insurance advice, and it is not an audit. Adapt it to your own process.

## How to use it

1. Copy [`postmortem-template.md`](postmortem-template.md) into your incident folder within 48 hours of the incident.
2. Fill the sections in order and keep the language blameless. Describe systems and guardrails, not people.
3. Finish with **one prevention rule** that is specific enough for a script or a reviewer to check.
4. Get owner sign-off, then link the rule into your agent's instructions or CI.

## Sections

| # | Section | What goes in it |
|---|---|---|
| 1 | Summary | Two sentences: what happened and the impact. |
| 2 | Timeline | UTC timestamps from the first agent action to full recovery. |
| 3 | Trigger | The prompt, task, event or input that started it. |
| 4 | Blast radius | Systems, data, users and money affected, and what was *not* affected. |
| 5 | Agent did vs should have done | Side-by-side: actual actions and expected actions. |
| 6 | Guardrail that failed | Which control should have stopped it, and why it did not. |
| 7 | Fix | What was done to recover, and what changed in code or config. |
| 8 | Prevention rule | One checkable rule, with an owner and a review date. |
| 9 | Owner sign-off | Name, date, and the follow-up review date. |

## Why blameless

Agent incidents almost always involve a missing or bypassed guardrail: permissions that were too broad, no dry-run, no budget cap, no human checkpoint on an irreversible action. Blaming the model, or the person who ran it, hides the control that has to change.

## License

MIT. Use it, fork it, adapt it.

---

Need the longer version with worked examples, a severity rubric and a guardrail checklist? The paid pack is the Agent Incident Postmortem Pack: https://renvt89.gumroad.com/l/mmuky?ref=gh-pm
