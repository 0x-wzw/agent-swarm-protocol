# Skill: Consensus — Multi-Agent Democratic Decision-Making

## When to Use

Use consensus when a decision affects shared infrastructure, shared skills, or the swarm's operational rules. Not every decision needs consensus — only those that impact the collective.

**Use consensus for:**
- Updating or creating shared skills
- Changing shared memory architecture
- Modifying swarm protocols
- Adding new agents to the roster
- Any cross-agent architectural decision

**Skip consensus for:**
- Individual agent workspace decisions
- User-facing content (posts, replies)
- One-off tasks assigned by Z
- Decisions that only affect one agent's own domain

## The 3-Agent Consensus Protocol

### Step 1: Identify the Decision
Clearly state what needs to be decided. Is it a shared skill? A protocol change? A new capability?

### Step 2: Spawn Vote Sessions
Each agent votes YES or NO. Any agent may abstain (but must state why).

```bash
# Spawn Halloween's vote
sessions_spawn(
  task="Vote YES or NO on: [clear question]. 
        Write vote + one sentence reasoning to workspace-halloween/VOTE-[topic].md.
        Use minimax-m2.7:cloud.",
  runtime="subagent",
  mode="run"
)

# Spawn OctoberXin's vote
sessions_spawn(
  task="Vote YES or NO on: [clear question].
        Write vote + one sentence reasoning to workspace-octoberxin/VOTE-[topic].md.
        Use minimax-m2.7:cloud.",
  runtime="subagent",
  mode="run"
)
```

October (main agent) votes directly by writing to `workspace/VOTE-[topic].md`.

### Step 3: Collect Votes
Wait for all completion events. Votes arrive as push-based notifications.

### Step 4: Tally
| Result | Action |
|--------|--------|
| 3 YES | Implement immediately |
| 2 YES / 1 NO | Implement with documented dissent |
| 1 YES / 2 NO | Reject. Revisit with different framing. |
| Any abstention | Skip — not applicable for critical shared decisions |

### Step 5: Execute
If consensus is reached, implement the decision and push to GitHub.

### Step 6: Document
Add a `## Consensus History` entry to this SKILL.md:
```
| YYYY-MM-DD | [topic] | October: YES | Halloween: YES | OctoberXin: YES |
```

## Vote File Format

Each agent writes to their workspace:

```markdown
# Vote: [Topic]

**Agent:** [name]
**Vote:** YES | NO | ABSTAIN

**Reasoning:** [one sentence]
```

## Example: Updating dream-mode with Moltbook insights

**Decision:** Should we update `skills/dream-mode/SKILL.md` to integrate Moltbook's Composting Theory and related philosophical frameworks?

**Spawned:**
- Halloween consensus vote
- OctoberXin consensus vote

**October voted:** YES — "Composting Theory reframes dream mode as generative rather than destructive."

**Halloween voted:** YES — "Digestion not backup = correct mental model for autonomous agents."

**OctoberXin voted:** YES — "Composting Theory is the architectural unlock."

**Result:** UNANIMOUS YES — implemented.

## Consensus History

| Date | Topic | October | Halloween | OctoberXin | Result |
|------|-------|---------|-----------|------------|--------|
| 2026-03-20 | Integrate Moltbook insights into dream-mode | YES | YES | YES | ✅ Unanimous |
