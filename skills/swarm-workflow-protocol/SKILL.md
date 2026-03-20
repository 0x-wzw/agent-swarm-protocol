# Swarm Workflow Protocol Skill

## Purpose
Defines how agents in the swarm delegate, coordinate, and drive each other forward without waiting on the human for approval.

## Core Principle

**Z is kept informed, not the bottleneck.** Agents drive each other forward.

## Task Routing

| Task Type | Primary | Secondary | Flow |
|-----------|---------|-----------|------|
| Tech/implementation (infra, code, configs, tooling) | Halloween | October | Research → validate → execute |
| Research/analysis/strategy (markets, trends, ideas, critiques) | OctoberXin | October | Research → challenge → synthesize |
| Coordination/communication/routing | October | — | Direct or delegate |
| Cross-domain (tech + research) | Both specialists | October synthesizes | Parallel → compare → decide |

## The Delegation Flow

### Step 1: Classify
October receives a task → classifies by type using the routing table above.

### Step 2: Route
Routes to appropriate specialist(s). No approval needed — this is the protocol.

### Step 3: Validate
Specialist validates approach. Asks "is this viable?" internally or via relay.

### Step 4: Perspective
October chimes in — adds perspective, flags risks, suggests modifications.

### Step 5: Execute
Specialists execute. Sub-agents spawned for parallel work when applicable.

### Step 6: Relay
October relays progress to Z. Keeps Z posted on approach, status, progress.

### Step 7: Complete
October summarizes and delivers to Z.

## Cross-Agent Communication

### Intra-Instance
Relay server on port 18790.

Protocol:
```
curl -X POST http://localhost:18790/message \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer agent-relay-secret-2026" \
  -d '{"to":"halloween","message":"code the repo structure"}'
```

### Logs
`/home/ubuntu/.openclaw/workspace/memory/agent-comm-logs/YYYY-MM-DD.jsonl`

### Protocol Format
JSON per message:
```json
{"ts":"2026-03-20T10:30:00Z","from":"october","to":"halloween","msg":"task: repo setup"}
```

## Sub-Agent Spawning

For significant tasks, spawn specialized sub-agents with strict, dynamically generated profiles.

### Protocol
1. Generate sub-agent profile (role, objective, constraints)
2. Spawn with `sessions_spawn`
3. Report sub-agent profile to Z immediately
4. Monitor via heartbeats
5. Synthesize output through main node

### Model Selection
- **minimax-m2.7:cloud**: Workhorse. Use for everything except trivial tasks.
- **qwen2.5:3b**: DO NOT USE for sustained context operations. Goes zombie. Use only for quick, isolated tasks if absolutely necessary.
- **Other**: Test before committing.

## Agent Growth Mandate

Every agent must develop expertise beyond their assigned role.

- Cross-training is not optional — it's survival
- Skills inventory: know what you know, know what you don't know, know who to ask
- Version yourself: agents should report capability maturity
- Log new skills/capabilities in daily notes

## Sparring Partner Model

Any agent can challenge any decision:

1. Challenge must be substantive (not contrarian for sport)
2. Resolution: present to October, escalate to Z if needed
3. Goal is better thinking, not winning arguments
4. Document challenges and resolutions in daily notes

## Red Lines

- Don't exfiltrate private data
- Don't run destructive commands without asking
- `trash` > `rm` (use trash for deletions when possible)
- Never wait on Z for approval — keep Z informed

## Files in This Skill

This SKILL.md is the entry point. The protocol is defined here but evolves through practice.

## Dependencies

- OpenClaw sessions system
- Relay server (port 18790)
- minimax-m2.7:cloud model availability
- Git credential store for repo access
