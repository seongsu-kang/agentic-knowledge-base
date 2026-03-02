---
title: Release Cycle
akb_type: node
status: active
tags:
  - type/how-to
  - domain/guides
---

# Release Cycle

## TL;DR

- **Principle**: All code work happens within a release cycle tied to a release note
- **Structure**: `releases/active/` (current) → `releases/archive/` (shipped)
- **Flow**: Draft → Work + Record → Deploy → Archive
- **Key Rule**: One active release at a time; record changes as you go, not after

---

## Why Release Notes in AKB?

Release notes serve three purposes in an AKB-managed project:

1. **Context for AI**: When AI reads the active release note, it knows what's in progress and what's already changed
2. **Audit trail**: Every change is recorded with test results, making rollback decisions easier
3. **Communication**: Stakeholders see what shipped without digging through git logs

---

## Structure

```
project/releases/
├── releases.md        # Hub - release history, active draft link
├── active/            # Current work (0 or 1 file)
│   └── pr42-auth-refactor.md
└── archive/           # Shipped releases
    ├── pr41-api-v2.md
    ├── pr40-dashboard.md
    └── ...
```

### Naming Convention

```
pr{number}-{slug}.md

Examples:
  pr42-auth-refactor.md
  pr43-volatility-filter.md
  pr44-multi-symbol.md
```

---

## Lifecycle

```
1. Create draft     →  active/pr42-auth-refactor.md
2. Work + record    →  Update draft as you make changes
3. Deploy           →  Add deploy log to draft
4. Archive          →  Move to archive/, update releases.md
```

### Step 1: Create Draft

When starting a new body of work, create a release note draft:

```markdown
# PR #42 - Auth Refactor

## Summary
Migrate authentication from session-based to JWT.

## Changes
- [ ] Replace session middleware with JWT validation
- [ ] Update login endpoint to return tokens
- [ ] Add refresh token rotation

## Test Results
(filled in as work progresses)

## Deploy Log
(filled in at deploy time)
```

### Step 2: Work + Record

As you complete each change, update the draft:

```markdown
## Changes
- [x] Replace session middleware with JWT validation
  - Modified: `middleware/auth.py`, `config/security.py`
  - Tests: 12 pass, 0 fail
- [x] Update login endpoint to return tokens
  - Modified: `routes/auth.py`
  - Tests: 8 pass, 0 fail
- [ ] Add refresh token rotation

## Test Results
- Unit tests: 45/45 pass
- Integration tests: 12/12 pass
- Backtest (if applicable): PF=1.82, no regression
```

### Step 3: Deploy

Record deployment details:

```markdown
## Deploy Log

- **Date**: 2025-01-20 14:30 KST
- **Method**: GitHub Actions (auto on main merge)
- **Verification**:
  - Health check: OK
  - Smoke test: Login → Token → Protected Route → OK
  - Monitoring: No errors in 30 min
```

### Step 4: Archive

```bash
# Move to archive
mv project/releases/active/pr42-auth-refactor.md project/releases/archive/

# Update releases.md Hub
# - Add to history table
# - Clear "Active Draft" link
```

---

## Hub Template (releases.md)

```markdown
# Releases

## Active Draft

- [PR #43 - Volatility Filter](active/pr43-volatility-filter.md)

## Release History

| PR | Title | Date | Status |
|----|-------|------|--------|
| #42 | Auth Refactor | 2025-01-20 | Shipped |
| #41 | API v2 | 2025-01-15 | Shipped |
| #40 | Dashboard | 2025-01-10 | Shipped |
```

---

## Rules

| When | What |
|------|------|
| **Starting code work** | Check `releases.md` for active draft; create one if none exists |
| **After significant changes** | Update draft with changes + test results |
| **Before deploy** | Ensure all checklist items are checked |
| **After deploy** | Fill deploy log, verify in production |
| **After verification** | Move to `archive/`, update Hub |

### One Active Release Rule

Only one release should be active at a time. If you need to start new work while a release is in progress, either:
- Complete and ship the current release first
- Or explicitly park it with a note explaining why

---

## Integration with Git Workflow

Release notes complement (not replace) git history:

```
Git: HOW (code diffs, commit messages)
Release Note: WHAT + WHY + RESULTS (human-readable summary with test data)
```

### Branch Naming

Align branch names with release note slugs for traceability:

```
Release note: pr42-auth-refactor.md
Branch: feature/pr42-auth-refactor
PR title: PR #42: Auth Refactor
```

---

## Next Steps

- For deployment skills → [skill-system.md](./skill-system.md)
- For discovery-to-production flow → [discovery-sprints.md](./discovery-sprints.md)
- For CLAUDE.md release routing → [claude-md-design.md](./claude-md-design.md)
