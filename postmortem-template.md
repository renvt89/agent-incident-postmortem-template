# Agent Incident Postmortem — <short title>

> Blameless format. Describe systems and guardrails, not people. Free template, not legal/compliance advice.

- **Incident ID:** 
- **Date (UTC):** 
- **Severity:** (SEV1 data/money loss · SEV2 customer-visible · SEV3 internal only)
- **Agent / tool involved:** 
- **Model + version / prompt version:** (e.g. provider/model@date, system-prompt commit)
- **Author:** 

## 1. Summary
Two sentences: what happened and the impact.

## 2. Timeline (UTC)
| Time | Event |
|---|---|
| hh:mm | First agent action |
| hh:mm | First signal something was wrong |
| hh:mm | Agent stopped / access revoked |
| hh:mm | Full recovery |

## 3. Trigger
The prompt, task, event or input that started it (quote it, redact secrets).

## 4. Blast radius
- Systems affected:
- Data affected:
- Users / customers affected:
- Money / budget affected:
- Explicitly NOT affected:

## 5. What the agent did vs what it should have done
| Step | Agent did | Should have done |
|---|---|---|
| 1 | | |
| 2 | | |

### Tool-call trace excerpt
Paste the 5-20 tool calls around the failure (redact secrets).
```
[hh:mm:ss] tool=<name> args=<redacted> -> result=<short>
```

### Detection
- How was it detected (alert, user report, cost spike, reviewer)?
- Time from first bad action to detection:
- What would have detected it sooner?

### 5 whys
1. Why did the agent take the harmful action?
2. Why was that action permitted?
3. Why did no check catch it before execution?
4. Why was the gap not known before?
5. Why did the process allow that gap? (root cause)

## 6. Guardrail that failed
- Which control should have stopped this (permission scope, dry-run, budget cap, approval checkpoint, allowlist, test)?
- Why it did not fire (missing / misconfigured / bypassed / never existed):

## 7. Fix
- Recovery actions taken:
- Code / config / permission changes (link commits or PRs):

## 8. Prevention rule
One rule specific enough for a script or reviewer to check.
- **Rule:** 
- **Where it lives:** (agent instructions, CI check, policy file)
- **Owner:** 
- **Review date:** 

## 9. Owner sign-off
- Name: 
- Date: 
- Follow-up review date: 
