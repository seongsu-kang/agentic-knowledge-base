# Your Knowledge Base

AI Agent-friendly Knowledge Base using AKB (Agentic Knowledge Base) methodology.

> **AKB Principle**: `methodology/agentic-knowledge-base.md`

---

## TL;DR

- **Purpose**: Personal/team knowledge management optimized for AI agents
- **Structure**: AKB style (Root → Hub → Node)
- **Philosophy**: AI finds knowledge through search (Grep/Glob) + contextual links

---

## AKB Core Concept

> **AKB** = File-based knowledge system where AI finds via **Search (Grep/Glob)** and navigates via **Contextual Links**

| Layer | Role | AI Usage |
|-------|------|----------|
| **Root** (CLAUDE.md) | Minimal routing | Auto-injected as system prompt |
| **Hub** ({folder}.md) | Human TOC + guides | **Check before starting work** |
| **Node** (*.md) | Actual information | Direct search via Grep/Glob |

> 📖 Detail: `methodology/agentic-knowledge-base.md`

---

## AI Working Rules (CRITICAL)

### Hub-First Principle

> ⛔ **Read Hub document BEFORE implementing/testing**

Based on AKB observations, AI tends to skip Hubs and search directly.
But **Hubs contain existing tools/scripts/guides** - missing them causes redundant work.

### Required Check Situations

| Situation | Read First | What to Find |
|-----------|------------|--------------|
| Debugging/Testing | Hub → guides/ | Existing debug tools |
| API Calls | Hub → related Node | Documented methods |
| New Feature | Hub | Similar existing features |

### Correct Patterns

```
✅ Wallet Debugging
   → wallet.md (Hub) → guides/debugging.md
   → Use existing debug scripts

✅ Transaction Testing
   → transaction.md (Hub) → test utilities

✅ API Integration
   → api.md (Hub) → existing client libraries
```

### Anti-Patterns

```
❌ Skip Hub → curl API directly
❌ Skip Hub → Write scripts from scratch
❌ Skip Hub → Start with assumptions
```

### Exploration Depth Principle

> ⛔ **For strategy/idea questions, Hub alone is NOT enough. Explore detail docs.**

AI tends to read a few Hubs and judge "sufficient".
But **strategic questions need specific context** - shallow exploration leads to superficial answers.

#### Exploration Depth by Question Type

| Question Type | Minimum | Additional |
|---------------|---------|------------|
| Implementation | Hub | Related Nodes |
| Debugging/Testing | Hub → guides/ | Existing tools |
| **Strategy/Ideas** | Hub | **Design philosophy, core problems, phase docs** |
| **Connecting A and B** | **Both Hubs** | **Both core docs (design, business, phases)** |

#### When Deep Exploration is Needed

```
✅ "How to connect Wallet and Payment systems?"
   → wallet.md + payment.md (both Hubs)
   → architecture.md (system design)
   → security-model.md (design philosophy)
   → business-requirements.md (business context)

✅ "Ideas for improving transaction speed?"
   → transaction.md (Hub)
   → performance-analysis.md (problem details, current approach)

✅ "Apply this architecture to another domain?"
   → architecture.md (Hub)
   → design-philosophy.md (domain-independent principles)
```

#### Risks of Shallow Exploration

```
❌ Read only 4 Hubs → "sufficient" judgment → superficial ideas
❌ List only technical features → No connection to actual problems
❌ Deep dive one side only → Forced fitting (bad integration)
```

> **Domain ≠ Core Problem**
> Knowing "it's a wallet service" but not "what's the core problem" → Technology pushing happens.
> AKB Hubs specify core problems, enabling "problem-centered" connections.

---

## Routing Table

| Task | ⚠️ Read First | Entry Point |
|------|---------------|-------------|
| AKB Methodology | - | `methodology/agentic-knowledge-base.md` |
| Create New Document | `.templates/templates.md` | Choose appropriate template |
| **Learning Notes** | - | `learnings/learnings.md` |
| **Task Tracking** | - | `tasks/tasks.md` |
| **Ideas/Brainstorm** | - | `ideas/ideas.md` |
| **Project Knowledge** | - | `projects/projects.md` |
| **Active Tasks** | `tasks/tasks.md` | `tasks/active/` |
| **Blocked Issues** | `tasks/tasks.md` | `tasks/blocked/` |
| **Real-World Patterns** | - | `guides/guides.md` |
| CLAUDE.md Design | `guides/guides.md` | `guides/claude-md-design.md` |
| Skill System | `guides/guides.md` | `guides/skill-system.md` |
| Multi-Agent Delegation | `guides/guides.md` | `guides/multi-agent-delegation.md` |
| Discovery Sprints | `guides/guides.md` | `guides/discovery-sprints.md` |
| Release Cycle | `guides/guides.md` | `guides/release-cycle.md` |

---

## Hub Entry Points

| Hub | Description | Path |
|-----|-------------|------|
| **methodology/** | AKB methodology | `methodology/methodology.md` |
| **learnings/** | Technical learning notes | `learnings/learnings.md` |
| **tasks/** | Task tracking & TODOs | `tasks/tasks.md` |
| **ideas/** | Ideas & exploration | `ideas/ideas.md` |
| **projects/** | Project-specific knowledge | `projects/projects.md` |
| **guides/** | Real-world patterns & guides | `guides/guides.md` |
| **.templates/** | Document templates | `.templates/templates.md` |

---

## Folder Structure

```
your-knowledge-base/
│
├── CLAUDE.md                    # [Root] AI entry point
├── README.md                    # GitHub intro
│
├── .templates/                  # Document templates
│   ├── templates.md             # Template guide [Hub]
│   ├── hub-template.md
│   └── node-template.md
│
├── methodology/                 # [Hub] AKB methodology
│   ├── methodology.md           # Hub entry
│   └── agentic-knowledge-base.md
│
├── guides/                      # [Hub] Real-world patterns
│   ├── guides.md                # Hub entry
│   ├── claude-md-design.md      # Root design patterns
│   ├── skill-system.md          # Operational playbooks
│   ├── multi-agent-delegation.md
│   ├── discovery-sprints.md
│   └── release-cycle.md
│
├── ideas/                       # [Hub] Ideas/Ideation
│   └── ideas.md                 # Hub entry + routing
│
├── tasks/                       # [Hub] Task tracking
│   ├── tasks.md                 # Hub entry
│   ├── active/                  # In progress
│   ├── blocked/                 # Waiting
│   └── archive/                 # Done
│
├── learnings/                   # [Hub] Technical learning
│   └── learnings.md             # Hub entry
│
└── projects/                    # [Hub] Project knowledge
    ├── projects.md              # Hub entry
    │
    └── my-project/              # Example project
        ├── my-project.md        # Project Hub
        ├── architecture.md      # [Node]
        └── guides/              # Sub-folder
            └── guides.md        # [Sub-Hub]
```

---

## Learning Paths

### Path 1: Understanding AKB

1. `methodology/agentic-knowledge-base.md` - AKB principles
2. `.templates/templates.md` - How to use templates
3. This CLAUDE.md - AI working rules

### Path 2: Starting Your Knowledge Base

1. Choose a folder (`learnings/`, `projects/`, `ideas/`)
2. Copy template from `.templates/`
3. Write with TL;DR + contextual links
4. Update the Hub file

### Path 3: Real-World Patterns

1. `guides/claude-md-design.md` - How to design CLAUDE.md
2. `guides/skill-system.md` - Operational playbooks
3. `guides/multi-agent-delegation.md` - Sub-agent patterns
4. `guides/discovery-sprints.md` - Hypothesis validation
5. `guides/release-cycle.md` - PR-based releases

### Path 4: Adding a New Project

1. Create `projects/{project-name}/` folder
2. Create `{project-name}.md` Hub file
3. Add nodes as needed
4. Update `projects/projects.md`

---

## Workflows

### New Document

> ⚠️ **Read first**: `.templates/templates.md`

```
1. Choose appropriate Hub folder (or create)
2. Copy template (Hub: hub-template.md, Node: node-template.md)
3. Write Frontmatter (akb_type, status, tags)
4. Write TL;DR section with keywords
5. Add contextual links in body
6. Update Hub {folder}.md
```

### New Project

```
1. Create projects/{project-name}/ folder
2. Create {project-name}.md Hub file
3. Update projects/projects.md
4. Add routing in this CLAUDE.md if frequently used
```

### Task Management

```
1. Create task in tasks/active/
2. Use task-template.md
3. Update tasks/tasks.md
4. Move to tasks/archive/ when done
```

---

## Writing Rules (4 Principles)

1. **TL;DR Required**: Include searchable keywords (bold)
2. **Contextual Links**: Place links in body text with context
3. **Keyword-Optimized Filenames**: `wallet-security.md` not `security.md`
4. **Atomicity**: One topic per document, under 200 lines

> 📖 Detail: `methodology/agentic-knowledge-base.md`

---

*Last updated: 2026-03*
