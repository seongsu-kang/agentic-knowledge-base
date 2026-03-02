---
title: CLAUDE.md Design Patterns
akb_type: node
status: active
tags:
  - type/how-to
  - domain/guides
---

# CLAUDE.md Design Patterns

## TL;DR

- **Routing Table**: Map tasks to entry points so AI finds the right Hub/Node immediately
- **Working Rules**: Codify observed AI failure patterns as explicit rules
- **Anti-Patterns**: Document what NOT to do, based on real incidents
- **Size Budget**: CLAUDE.md is injected into every prompt; keep it lean

---

## The Role of CLAUDE.md

CLAUDE.md is the **Root** of AKB. It is auto-injected as system prompt in Claude Code (and can be manually included in other AI tools). Its job is **minimal routing** - pointing AI to the right place, not containing all knowledge.

```
CLAUDE.md (Root)
├── TL;DR (what this project is)
├── Routing Table (task → entry point)
├── Working Rules (how AI should behave)
├── Folder Structure (orientation)
└── Learning Paths (onboarding sequences)
```

---

## Pattern 1: Routing Table

The routing table is the most important section. It maps **tasks** to **entry points**.

```markdown
## Routing Table

| Task | Read First | Entry Point |
|------|------------|-------------|
| API integration | Hub | `projects/api/api.md` |
| Auth system | Hub | `projects/auth/auth.md` |
| Database schema | - | `projects/database/schema.md` |
| Deployment | - | `operations/deploy.md` |
| Bug investigation | Hub → issues/ | `issues/` |
```

**Design principles:**
- Frequently accessed files get direct paths
- Complex domains route through Hub first
- "Read First" column tells AI what to check before diving in

---

## Pattern 2: Hub-First Principle

Based on observed AI behavior, agents tend to skip Hubs and search Nodes directly via Grep/Glob. This causes them to miss existing tools, scripts, and guides.

```markdown
## AI Working Rules (CRITICAL)

### Hub-First Principle

> Do NOT implement or test before reading the relevant Hub document.

| Situation | Read First | What to Find |
|-----------|------------|--------------|
| Schema change | `database/database.md` | Migration tools, naming conventions |
| New endpoint | `api/api.md` | Existing patterns, auth middleware |
| Debugging | Hub → `issues/` | Known issues, existing debug scripts |
```

### Correct vs Anti-Patterns

```
Correct:
  Schema change → database.md (Hub) → find migration tool → use it

Anti-pattern:
  Schema change → write raw SQL → miss migration tool → inconsistency
```

---

## Pattern 3: Exploration Depth Rules

AI tends to read a few Hubs and judge "sufficient." For strategic or cross-cutting questions, enforce deeper exploration.

```markdown
### Exploration Depth by Question Type

| Question Type | Minimum | Additional |
|---------------|---------|------------|
| Implementation | Hub | Related Nodes |
| Debugging | Hub → issues/ | Existing tools |
| Strategy/Ideas | Hub | Design docs, test results, issue history |
| Cross-domain | Both Hubs | Both core docs |
```

---

## Pattern 4: Self-Verification Before Escalation

AI (especially after context compaction) may forget its own capabilities and escalate to the user unnecessarily.

```markdown
### Self-Verification Checklist

Before saying "I can't do this" or "User action required":

1. Check CLAUDE.md routing table for relevant skills/tools
2. Glob search `.claude/skills/` for matching skills
3. If a skill exists, read it and assess feasibility
4. Only after all checks fail: report with specific reason
   "Tried X, but [concrete reason] prevents completion"
```

**Real incident**: AI reported "server restart needed - user action required" when a deployment skill existed that could handle it remotely. After being pointed to the skill, AI resolved it in 2 minutes.

---

## Pattern 5: Size Budget

CLAUDE.md is injected into every prompt. Every line costs tokens across all interactions.

**What belongs in CLAUDE.md:**
- TL;DR (project identity)
- Routing table (task → entry point)
- Critical rules (things that cause incidents if missed)
- Folder structure (orientation)
- Learning paths (onboarding)

**What does NOT belong in CLAUDE.md:**
- Detailed how-to guides (put in Nodes)
- Full API documentation (put in Nodes)
- Historical records (put in archive/)
- Implementation details (put in code or Nodes)

---

## Pattern 6: Scope Separation

When your project has both documentation and source code, separate them clearly.

```markdown
## Scope

| What | Where | Why |
|------|-------|-----|
| Knowledge & docs | This AKB repo | Grep/Glob search without code noise |
| Source code | `~/my-project/` | Separate CI/CD, separate concerns |
| Design docs | AKB `project/design/` | Survives code refactors |
| Issue records | AKB `project/issues/` | Searchable history |
```

**Why separate**: AKB documents mixed with source code create Grep/Glob noise. AI searching for "authentication" finds code files instead of the design doc explaining *why* the auth system works this way.

---

## Next Steps

- For skill system patterns → [skill-system.md](./skill-system.md)
- For multi-agent delegation → [multi-agent-delegation.md](./multi-agent-delegation.md)
- For AKB fundamentals → [../methodology/agentic-knowledge-base.md](../methodology/agentic-knowledge-base.md)
