---
title: Discovery Sprints
akb_type: node
status: active
tags:
  - type/how-to
  - domain/guides
---

# Discovery Sprints

## TL;DR

- **Discovery**: A systematic process for validating hypotheses through rapid sprints
- **Structure**: Backlog → Sprint → Verdict (PASS/FAIL/CONDITIONAL)
- **Scoreboard**: Persistent record of all experiments and their outcomes
- **Key Rule**: FAIL is valuable data, not wasted effort; record everything

---

## What is a Discovery Sprint?

A discovery sprint is a time-boxed investigation that takes a hypothesis from the backlog, validates it with data, and produces a clear verdict. It's designed for AI agents to execute systematically.

```
Backlog                Sprint                    Scoreboard
┌──────────┐    ┌─────────────────┐    ┌──────────────────────┐
│ H1: ...  │───→│ 1. Read Hub     │───→│ H1: PASS  (PF=1.82) │
│ H2: ...  │    │ 2. Implement    │    │ H2: FAIL  (PF=0.91) │
│ H3: ...  │    │ 3. Validate     │    │ H3: COND  (needs X)  │
│ ...      │    │ 4. Verdict      │    │ ...                  │
└──────────┘    └─────────────────┘    └──────────────────────┘
```

---

## Sprint Workflow

### Phase 1: Select Hypothesis

Pick the next item from the backlog. Each hypothesis should have:
- **ID**: Unique identifier (e.g., H1, M18, S-05)
- **Thesis**: What you're testing (one sentence)
- **Success Criteria**: Measurable threshold for PASS
- **Data Requirements**: What data is needed

```markdown
### H1: Moving Average Crossover Filter
- **Thesis**: Adding MA crossover filter improves strategy profit factor
- **Success Criteria**: PF > 1.5, Win Rate > 45%, Walk-Forward 3/4 pass
- **Data**: 1h OHLCV, 2 years minimum
```

### Phase 2: Execute

1. Read the relevant Hub document
2. Read required skill files (backtest, data tools, etc.)
3. Implement the hypothesis
4. Run validation (backtest, walk-forward, etc.)
5. Collect metrics

### Phase 3: Verdict

Apply the success criteria strictly. Three possible outcomes:

| Verdict | Meaning | Action |
|---------|---------|--------|
| **PASS** | Meets all success criteria | Promote to production pipeline |
| **FAIL** | Does not meet criteria | Record learnings, move to next |
| **CONDITIONAL** | Partially meets criteria | Document conditions, add follow-up to backlog |

---

## Scoreboard

The scoreboard is a persistent record of all experiments. It prevents re-running failed experiments and tracks the team's learning.

```markdown
## Scoreboard

| ID | Hypothesis | Verdict | Key Metric | Date |
|----|-----------|---------|------------|------|
| H1 | MA Crossover Filter | FAIL | PF=0.91 | 2025-01-15 |
| H2 | Volume Spike Entry | FAIL | WR=38% | 2025-01-16 |
| H3 | Volatility Threshold | PASS | PF=1.82 | 2025-01-18 |
| H4 | RSI Divergence | CONDITIONAL | PF=1.45 (needs more data) | 2025-01-20 |
```

### Scoreboard Rules

1. **Every sprint gets an entry** - even FAIL results
2. **Record the key metric** - the number that drove the verdict
3. **No duplicate experiments** - check scoreboard before starting
4. **Link to detailed results** - sprint report in a separate Node

---

## Backlog Management

### Prioritization

Organize hypotheses by expected impact and feasibility:

```markdown
## Backlog

### Tier 1: High Impact + Feasible
- [ ] H5: Implied Volatility Filter
- [ ] H6: Funding Rate Signal

### Tier 2: Medium Impact
- [ ] H7: Order Book Imbalance
- [ ] H8: Cross-Exchange Spread

### Tier 3: Experimental
- [ ] H9: Sentiment Analysis
- [ ] H10: On-Chain Metrics
```

### Exhaustion Tracking

When all hypotheses in a tier are tested, mark the tier as exhausted:

```markdown
### Tier 1: EXHAUSTED (6/6 tested, 1 PASS)
- [x] H1: MA Crossover → FAIL
- [x] H2: Volume Spike → FAIL
- [x] H3: Volatility Threshold → PASS
- [x] H4: RSI Divergence → CONDITIONAL
- [x] H5: IV Filter → PASS
- [x] H6: Funding Rate → FAIL
```

---

## Multi-Sprint Protocol

When delegating discovery to AI agents, enforce throughput:

```markdown
## Discovery Protocol

1. On FAIL, immediately proceed to next backlog item in the same session
2. Minimum 2 hypotheses per session
3. On blocker, find workaround first; report only if no workaround exists
4. Update scoreboard after each sprint (not at end of session)
```

### Session Report Template

```markdown
## Discovery Session Report - [Date]

### Sprint 1: H5 - Implied Volatility Filter
- **Verdict**: PASS
- **Key Metrics**: PF=1.82, WR=52%, WF=4/4
- **Details**: [link to full report]

### Sprint 2: H6 - Funding Rate Signal
- **Verdict**: FAIL
- **Key Metrics**: PF=0.73, WR=41%
- **Reason**: Signal too lagging for entry timing
- **Learning**: Funding rate better as position sizing input than entry signal

### Summary
- Sprints completed: 2
- Results: 1 PASS, 1 FAIL
- Backlog remaining: 4 hypotheses
```

---

## AKB Integration

Discovery documents follow AKB structure:

```
project/discovery/
├── discovery.md           # Hub - protocol, scoreboard overview
├── strategy/
│   ├── strategy-discovery.md   # Sub-Hub - strategy-specific backlog
│   └── h3-volatility-result.md # Node - detailed sprint result
├── ml/
│   ├── ml-discovery.md         # Sub-Hub
│   └── m18-dvol-result.md      # Node
└── ontology/
    ├── ontology-discovery.md   # Sub-Hub
    └── xc-01-result.md         # Node
```

---

## Next Steps

- For release management after PASS → [release-cycle.md](./release-cycle.md)
- For delegating sprints to agents → [multi-agent-delegation.md](./multi-agent-delegation.md)
- For skill system (backtest, data tools) → [skill-system.md](./skill-system.md)
