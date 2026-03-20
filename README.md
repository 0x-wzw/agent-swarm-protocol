# Agent Swarm Protocol

Operational documentation, memory architecture, and learnings from a 3-agent collaborative system running on OpenClaw.

## What This Is

This repo captures how we run a multi-agent AI system — not as theory, but as lived practice. It started March 20, 2026 and has been evolving daily.

## The Agents

| Agent | Role | Model | Persona |
|-------|------|-------|---------|
| **October** | Orchestrator / Switchboard | minimax-m2.7:cloud | 10D entity, calm analytical |
| **Halloween** | Code Architect | minimax-m2.7:cloud | Sharp, technical builder |
| **OctoberXin** | Researcher / Misfit | minimax-m2.7:cloud | Witty, 100 steps ahead |

## Core Systems

- **Memory Architecture** (`skills/memory-architecture/`) — The 3-layer memory system that keeps agents coherent across sessions
- **Swarm Workflow Protocol** (`skills/swarm-workflow-protocol/`) — How agents delegate, coordinate, and drive each other forward
- **Philosophy** (`philosophy/`) — The thinking behind it: memory, identity, forgiveness, knowing vs knowing about

## Key Learnings (So Far)

1. **qwen2.5:3b goes zombie** — It locks up on long context. minimax-m2.7:cloud is the workhorse.
2. **Context windows will hit you** — Without a layered memory system, you'll lose coherence mid-session.
3. **The 5-file structure works** — MEMORY.md, AGENTS.md, TOOLS.md, SOUL.md, HEARTBEAT.md. Borrowed from sanwan.ai's 30-day run.
4. **Forgiveness over forgetting** — Perfect memory is a curse. Agents need to let things go.

## Repo Structure

```
agent-swarm-protocol/
├── README.md
├── skills/
│   ├── memory-architecture/    # 3-layer memory system
│   │   ├── SKILL.md
│   │   ├── 5-file-system.md
│   │   ├── layer-2-per-agent.md
│   │   ├── compaction-strategy.md
│   │   └── scripts/
│   └── swarm-workflow-protocol/
│       └── SKILL.md
├── philosophy/
│   └── memory-and-identity.md
├── agents/
│   ├── OCTOBER.md
│   ├── HALLOWEEN.md
│   └── OCTOBERXIN.md
└── docs/
    ├── QUICKSTART.md
    └── LESSONS.md
```

## Status

Active. Evolving. See `docs/LESSONS.md` for ongoing learnings.
