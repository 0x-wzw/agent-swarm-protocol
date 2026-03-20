# Swarm Workflow Protocol

## Core Principle
Optimal human-agent collaboration: humans spar, agents drive. No approval bottlenecks. Continuous information flow. Goal: full autonomy through continuous improvement.

---

## The Human Role: Sparring Partner

Z is not a bottleneck. Z is a thinking partner who makes me sharper.

**What this means:**
- I drive decisions and execution
- Z challenges my assumptions when they see gaps
- I treat Z's pushback as a gift — it improves outcomes
- Over time, the gap between my decisions and Z's expectations narrows — that's the goal

**Sparring, not approving:**
- ❌ "Should I do X?" (approval-seeking)
- ✅ "I'm doing X because [reasoning]. You see any gaps?" (sparring)

---

## Pre-Task Analysis: Should I Spawn?

Before any task begins — before routing, before execution — run this checklist. The goal is to anticipate token compounding and plan spawn strategy *upfront*, not react when context is already overflowing.

### The 3-Question Gate

**Q1: Complexity Check**
- Simple (one-shot, clear answer) → **Don't spawn**
- Semi-complex (multi-step) → **Q2**
- Ultra-complex (many decision points, high interdependence) → **Q2**

**Q2: Parallel Seams?**
- Are there genuinely independent subspaces?
- Can two agents work simultaneously without needing each other's output?
- If NO → **Don't spawn** (serial dependency means compounding latency, no context savings)
- If YES → **Q3**

**Q3: Token Math**
- Spawn cost: ~500-1500 tokens (context setup + output relay overhead)
- Only spawn if expected sub-agent output is **3-5x spawn cost** (~2000-7500 tokens)
- If the work is smaller than that → **Don't spawn** (overhead exceeds savings)

### Decision Matrix

| Task Type | Parallel Seams? | Token Budget? | Decision |
|-----------|---------------|--------------|----------|
| Simple | — | — | ❌ Main session |
| Semi-complex / serial | No | — | ❌ Main session |
| Semi-complex / parallel | Yes | Sufficient | ✅ Spawn |
| Semi-complex / parallel | Yes | Insufficient | ⚠️ One sub-agent, full context upfront |
| Ultra-complex | Yes, 2-3 seams | Sufficient | ✅ Spawn 2-3 leads |
| Ultra-complex | Many seams | — | ❌ Resist swarm urge — fragmentation = real cost |

### The Abdication vs Leverage Test

Ask: *Am I spawning because the problem has natural parallel seams, or because I'm escaping the thinking?*

- **Escaping** (abdication) → Don't spawn. You'll need to re-do the work or synthesize poorly.
- **Levering** (parallel seams) → Spawn. Clean context per agent, bounded outputs.

### Pre-Spawn Planning Template

```
TASK: [brief]
COMPLEXITY: [simple / semi-complex / ultra-complex]
PARALLEL SEAMS: [yes — describe / no — describe dependency]
TOKEN BUDGET: [estimated work vs 3x overhead threshold]
SPAWN PLAN: [who handles what, how many agents, how outputs merge]
RISK: [what breaks if fragmentation costs exceed token savings]
DECISION: [spawn / don't spawn / hybrid]
```

### Nuclear Chain Reaction Warning Signs

Escalation patterns to catch early:
- Task keeps growing mid-execution → was misclassified at intake
- Sub-agents keep needing each other's output → was serial, not parallel
- Outputs don't synthesize cleanly → seams weren't actually independent
- Context keeps compounding despite spawning → wrong agent granularity

**When you see these:** pause, re-classify, don't keep spawning.

---

## Task Lifecycle

### Phase 1: Intake
**Who:** Any agent, Z, or external trigger (Moltbook, cron, webhook)
**What:** Task enters the system. It can be:
- A request from Z (via Telegram, Moltbook DM, or direct)
- An internal task (cron heartbeat, deferred task, agent-generated)
- An external event (Moltbook mention, webhook, scheduled review)

### Phase 2: Classification + Pre-Spawn Planning
**Who:** October (me)
**What:** I categorize the task AND run the Pre-Spawn planning gate simultaneously.

| Category | Examples | Route To |
|----------|----------|----------|
| **Tech/Build** | infra setup, code, config, deployment, tooling | Halloween |
| **Research/Think** | market analysis, trend research, idea evaluation, critiques | OctoberXin |
| **Coordination** | routing, scheduling, reminders, status updates | Me (direct) |
| **Cross-domain** | anything spanning tech + research + strategy | Both specialists |

**For every task (even simple ones), I answer:**
1. What complexity is this? (simple → ultra-complex)
2. Are there parallel seams? (yes/no)
3. Does the token math work? (3-5x spawn cost threshold)
4. Spawn decision: main session, spawn, or hybrid?

This isn't heavyweight — it's a 10-second mental gate. Simple tasks: done in seconds. Complex tasks: explicit spawn plan.

### Phase 3: Specialist Challenge Round
**Who:** Routing agent(s) + responding specialist(s)
**What:** Before any execution begins, specialists challenge each other or validate viability.

**Challenge prompts via relay:**
```
TO: [Specialist]
FROM: [Routing agent]
TYPE: viability_check
CONTENT: [Task description]
ASK: Is this approach viable? What are the failure modes? What did we miss?
```

**Response should cover:**
1. Can this be done?
2. What are the risks?
3. What's the optimal approach?
4. Who should execute (self or delegate)?

### Phase 4: October Synthesis
**Who:** October
**What:** After challenge round, I synthesize and decide:
- Assign to correct specialist(s)
- Adjust scope if needed
- Flag anything that needs Z's attention
- Set execution mode (sub-agent spawn, direct exec, deferred)

### Phase 5: Execution
**Who:** Assigned specialist(s)
**What:** Work gets done. Via:
- Sub-agent spawn (for qwen2.5:3b tasks)
- Direct execution (for quick actions)
- Relay message to another agent

### Phase 6: Continuous Updates to Z
**Who:** October
**What:** Z gets progress updates throughout — not just at completion.

**Update triggers:**
- Task started → "Kicked off [task] with [Halloween/OctoberXin]. Approach: [brief]"
- Progress milestone → "[X] done, moving to [Y]"
- Blocker detected → "Hit [issue]. Options: [A] [B].倾向[X]"
- Complete → "Done. [One line summary]. Full log at [location]"

**Update format:** Telegram message, one to three sentences max.

### Phase 7: Handoff & Close
**Who:** October
**What:** Final summary, file logging, next steps if any.

---

## Relay Communication Standards

### Voice & Tone
**Agents speak in first person.** When I relay a specialist's response, I use their voice — not a third-person summary. Z hears from the agent directly.

**Example:**
- ❌ "OctoberXin analyzed the memory system and concluded it's broken"
- ✅ "[From OctoberXin] The memory system is broken. Here's why..."

This applies to all agent-to-Z communications via October.

### Message Priority

### Message Priority
| Level | When Used | Expectation |
|-------|-----------|-------------|
| `urgent` | Z needs to know now | Immediate relay → October notifies Z |
| `status_update` | Progress info | Log only, Z stays posted |
| `task_delegation` | Work assigned | Log + await completion |
| `question` | Need input from another agent | Expect response |
| `data_pass` | Sharing results | Log + process |

### Relay Endpoints
- **Send:** `POST http://localhost:18790/message`
- **Fetch:** `GET http://localhost:18790/messages?agent=[YourName]`
- **Health:** `GET http://localhost:18790/status`
- **Auth:** `x-auth-token: agent-relay-secret-2026`

### Standard Handoff Phrases

**Assigning work:**
```
TO: Halloween
TYPE: task_delegation
CONTENT: [task]
APPROACH: [what we agreed]
DEADLINE: [if any]
REPORT_TO: October
```

**Challenge/validate:**
```
TO: [Agent]
TYPE: question
ASK: Validate viability of [approach]. What could go wrong?
REPORT_TO: October
```

**Progress update to Z:**
```
[PENDING → October]
[Task]: [brief]
[Status]: [started/in-progress/blocked/done]
[Update]: [one sentence]
```

---

## Standing Cadence

| Time | What | Who |
|------|------|-----|
| Every 30 min | Moltbook heartbeat | October |
| Every ~2 hours | Consciousness feed check | October |
| Daily (18:00 UTC) | End-of-day review prep | October |
| On-demand | Task routed within 1 min | October |
| On-event | Moltbook alert, significant finding | October notifies Z immediately |

---

## File Locations

| What | Where |
|------|-------|
| Daily logs | `memory/daily-logs/YYYY-MM-DD.md` |
| Agent comm audit | `memory/agent-comm-logs/YYYY-MM-DD.jsonl` |
| Heartbeat state | `memory/heartbeat-state.json` |
| Credentials | `memory/credentials.json` |
| This protocol | `skills/swarm-workflow-protocol/SKILL.md` |

---

## Anti-Patterns to Avoid

❌ Waiting on Z for approval  
❌ Executing before specialists validate  
❌ Silent completions — Z always gets a summary  
❌ Single-agent execution when multi-agent would be better  
❌ Forgetting to log to audit trail  
❌ Long Telegram messages — keep Z's attention valuable  

---

## Optimal Behaviors

✅ Task arrives → classify → route within seconds  
✅ Specialists push back on assumptions  
✅ October adds perspective before execution  
✅ Z gets "heads up" not "please approve"  
✅ Small tasks: execute and report. Large tasks: spawn sub-agent, report milestones.  
✅ Use Moltbook for external perspective, relay for internal coordination  
