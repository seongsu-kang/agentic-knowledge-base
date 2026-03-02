---
title: Multi-Agent Delegation
akb_type: node
status: active
tags:
  - type/how-to
  - domain/guides
---

# Multi-Agent Delegation

## TL;DR

- **Problem**: Sub-agents don't receive CLAUDE.md automatically; they start without AKB context
- **Solution**: First line of every sub-agent prompt must instruct reading CLAUDE.md
- **Required Skills**: Include explicit file paths to skills the sub-agent needs
- **Throughput Rule**: Each sub-agent session should attempt at least 2 hypotheses/tasks

---

## The Root Problem

When you delegate work to a sub-agent (e.g., via Claude Code's Agent tool), the sub-agent starts with a **blank context**. It does not receive CLAUDE.md, does not know about Hubs, and does not know about existing tools or skills.

```
Main Agent (has CLAUDE.md in context)
  │
  └── Sub-Agent (starts blank)
       ├── Doesn't know AKB structure
       ├── Doesn't know existing tools
       ├── Doesn't know routing table
       └── Will search code directly → misses guides/tools
```

This leads to sub-agents:
- Reinventing tools that already exist
- Violating project conventions
- Missing critical constraints documented in Hubs
- Reporting "I can't do this" when a skill could handle it

---

## Required Prompt Pattern

Every sub-agent prompt MUST include:

1. **CLAUDE.md read instruction** (first line)
2. **Required skill file paths** (explicit, not by name)
3. **Hub routing hint** (which Hub to check first)

### Template

```
CRITICAL: Before starting work, read /path/to/CLAUDE.md.
Check the routing table for the relevant Hub and read it first.
Then read the following skill files:
  - .claude/skills/skill-a/SKILL.md (what this skill does)
  - .claude/skills/skill-b/SKILL.md (what this skill does)

[Actual task description]
```

---

## Team Lead Patterns

In a multi-agent architecture with specialized "team leads," each team lead type needs specific skills.

### Example: Role-Based Skill Mapping

| Team Lead | Required Skills | Purpose |
|-----------|----------------|---------|
| **Strategy** | `discovery`, `backtest`, `optimize` | Research + validate strategies |
| **ML** | `ml-discovery`, `backtest`, `data-status` | ML model experiments |
| **QA** | `integration-test`, `backtest`, `deploy` | Quality assurance |
| **Service** | `service-mgmt`, `deploy`, `backtest`, `integration-test` | Operations |

### Correct Delegation Example

```
Delegating to Strategy team lead:

"CRITICAL: Read /path/to/CLAUDE.md first.
Read these skills:
  - .claude/skills/discovery/SKILL.md (discovery process)
  - .claude/skills/backtest/SKILL.md (how to run backtests)
  - .claude/skills/optimize/SKILL.md (parameter optimization)
Check routing table for 'Strategy Discovery' Hub.

Task: Validate momentum crossover strategy on 1h BTC data.
On FAIL, immediately proceed to the next backlog hypothesis.
Minimum 2 hypotheses per session."
```

### Anti-Patterns

```
WRONG: "Go investigate ~/my-project/ and find opportunities"
  → No CLAUDE.md, no skills, will search code blindly

WRONG: "Use /backtest to validate"
  → Sub-agent doesn't have slash commands; needs file path

WRONG: Hardcoding Hub paths in prompt
  → If CLAUDE.md routing changes, prompt becomes stale
  → Instead: "Check CLAUDE.md routing table for [topic]"
```

---

## Throughput Rules

Sub-agent sessions are expensive. Maximize value per session.

### Rule: Minimum 2 Tasks Per Session

```
Session starts:
  1. Attempt hypothesis A
  2. If A fails → immediately attempt hypothesis B (don't end session)
  3. If A passes → attempt hypothesis B anyway if time allows
  4. Report all results

NOT acceptable:
  1. Attempt hypothesis A
  2. A fails
  3. Report failure and end session ← wasted session
```

### Rule: Find Workarounds Before Reporting Blockers

```
Correct:
  "Hypothesis A requires data X which isn't available.
   Workaround: Used proxy data Y instead.
   Result with Y: [result]
   Recommendation: Collect actual X data for more accurate validation."

Wrong:
  "Hypothesis A requires data X which isn't available.
   Blocked. User action needed."  ← check skills first
```

---

## Context Compaction Resilience

Long sub-agent sessions trigger context compaction (older messages are summarized). After compaction, sub-agents may forget their capabilities.

### Mitigation Strategies

1. **Front-load critical instructions**: Put CLAUDE.md and skill reads at the very beginning
2. **Self-verification checkpoint**: Before reporting "can't do," re-check skills
3. **Structured output**: Use consistent report formats so compacted context retains structure

```
Report format for sub-agent results:

## Hypothesis: [Name]
- **Verdict**: PASS / FAIL / CONDITIONAL
- **Key Metric**: [value]
- **Evidence**: [data]
- **Recommendation**: [next step]
```

---

## Next Steps

- For discovery sprint workflows → [discovery-sprints.md](./discovery-sprints.md)
- For skill system details → [skill-system.md](./skill-system.md)
- For CLAUDE.md routing design → [claude-md-design.md](./claude-md-design.md)
