---
title: Skill System
akb_type: node
status: active
tags:
  - type/how-to
  - domain/guides
---

# Skill System

## TL;DR

- **Skill**: An operational playbook stored in `.claude/skills/{name}/SKILL.md`
- **Purpose**: Encode repeatable procedures so AI executes them consistently
- **Sync Principle**: When the system changes, update the skill; stale skills cause incidents
- **Not just docs**: Skills are executable knowledge - AI reads them and follows the steps

---

## What is a Skill?

A skill is a markdown file that teaches AI **how to perform a specific operation**. Unlike regular documentation that explains concepts, skills are **step-by-step playbooks** that AI follows to complete tasks.

```
.claude/skills/
├── deploy/
│   └── SKILL.md          # How to deploy to production
├── backtest/
│   └── SKILL.md          # How to run backtests
├── service-management/
│   └── SKILL.md          # How to start/stop/restart services
└── data-pipeline/
    └── SKILL.md          # How to check data status
```

---

## Skill vs Regular Documentation

| Aspect | Skill | Regular Doc |
|--------|-------|-------------|
| **Purpose** | "How to do X right now" | "What X is and why" |
| **Format** | Commands, endpoints, parameters | Explanations, diagrams |
| **Consumer** | AI executing a task | Human understanding context |
| **Staleness risk** | High (commands change) | Lower (concepts stable) |
| **Location** | `.claude/skills/` | AKB nodes |

---

## Anatomy of a Skill

A well-designed skill has these sections:

```markdown
# Service Management

## TL;DR
- Start/stop/restart the application stack
- Monitor health and logs
- Manage strategy runners

## Prerequisites
- SSH access to server (or local Docker)
- Database connection string

## Commands

### Start Services
docker compose up -d api web trader

### Check Health
curl http://localhost:8000/health

### View Logs
docker compose logs -f --tail=100 api

## Parameters

| Service | Port | Health Endpoint |
|---------|------|-----------------|
| API | 8000 | /health |
| Web | 5173 | / |
| Trader | - | (no HTTP) |

## Troubleshooting
- If API won't start → check DB connection
- If Trader crashes → check exchange API keys
```

---

## Skill Sync Principle (Critical)

> When the system changes, the skill MUST be updated in the same commit.

### Why This Matters

Skills are operational playbooks. If a parameter changes in code but the skill still documents the old value, AI will use the wrong parameter. This has caused real production incidents.

### What Triggers a Skill Update

| Change Type | Skill Update |
|-------------|--------------|
| API endpoint changed | Update command examples |
| New parameter added | Add to parameter table |
| Service added/removed | Update service list |
| Deploy process changed | Update deploy steps |
| Default values changed | Update parameter defaults |

### Correct Pattern

```
Code change: Authentication endpoint moved from /auth to /api/auth

1. Update source code
2. Update skill: deploy/SKILL.md (new endpoint)
3. Update skill: service-management/SKILL.md (health check URL)
4. Commit all together
```

### Anti-Pattern

```
Code change: Strategy parameter SL changed from 1% to 5%

1. Update source code ← committed
2. Skill still says SL=1% ← forgotten
3. Next day: AI reads skill, reports SL=1% in daily journal ← wrong
```

---

## Skill Invocation Patterns

Skills can be invoked via slash commands in Claude Code:

```
User: /deploy
AI: [Reads .claude/skills/deploy/SKILL.md]
    [Follows the checklist step by step]
    [Reports results]
```

### Naming Convention

| Skill Name | Invocation | Purpose |
|------------|------------|---------|
| `deploy` | `/deploy` | Production deployment |
| `backtest` | `/backtest` | Run strategy backtests |
| `service-management` | `/service-management` | Start/stop services |

---

## Multi-Skill Coordination

Complex operations may require multiple skills. Document the sequence in each skill's "Prerequisites" or "Related Skills" section.

```markdown
## Related Skills

- Before deploying → run `/backtest` to verify strategy performance
- After deploying → run `/service-management status` to verify health
- If tests fail → see `/integration-test` skill for debugging
```

---

## Next Steps

- For delegating skills to sub-agents → [multi-agent-delegation.md](./multi-agent-delegation.md)
- For CLAUDE.md routing to skills → [claude-md-design.md](./claude-md-design.md)
