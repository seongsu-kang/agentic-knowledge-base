# Agentic Knowledge Base (AKB)

**AI Agent-Friendly File-Based Knowledge Protocol**

> "Don't inject everything into AI at once. Instead, give it **well-structured documents** that are easy to find."

---

## What is AKB?

AKB is a **file-based knowledge system** designed for AI agents to autonomously **search**, **learn**, and **retrieve** context without requiring infrastructure like Vector DBs.

```
AKB = Lightweight Knowledge Graph on Markdown

Ontology/KG              AKB
───────────              ───
Entity (Node)      →     .md file
rdf:type           →     tags: [type/]
rdfs:comment       →     TL;DR section
Edge/Relationship  →     Contextual links in body
```

### Why AKB?

| Comparison | AKB | RAG | System Prompt |
|-----------|-----|-----|---------------|
| Infrastructure | None | Vector DB | None |
| Token Efficiency | Load only what's needed | Chunk-based | Load everything |
| AI Navigation | Grep + Contextual links | Similarity search | None |
| Maintenance | Edit files | Re-indexing | Edit prompts |

---

## Quick Start

### 1. Clone this template

```bash
git clone https://github.com/seongsu-kang/agentic-knowledge-base.git my-knowledge-base
cd my-knowledge-base
```

### 2. Connect with AI tools

- **Claude Code**: CLAUDE.md is auto-injected as system prompt
- **Cursor / Windsurf**: Add CLAUDE.md to project rules
- **Other AI tools**: Include CLAUDE.md in context

### 3. Start building with AI

See the workflow examples below.

---

## Workflow Examples

### Example 1: Knowledge-Driven Development

AKB enables a natural flow: **Ideate → Document → Plan → Build**

```
You: "I want to build a blockchain wallet. Help me ideate."

AI: [Explores ideas, writes to ideas/blockchain-wallet-ideation.md]
    - Core features analysis
    - Security considerations
    - UX patterns research
    - Tech stack recommendations

You: "Turn this ideation into knowledge docs."

AI: [Creates structured docs in projects/blockchain-wallet/]
    - architecture.md (system design)
    - security-model.md (threat model, key management)
    - user-flows.md (UX specifications)
    - tech-decisions.md (why these choices)

You: "Review the knowledge and create tasks."

AI: [Reads knowledge, creates tasks/active/wallet-implementation.md]
    - Phase 1: Core wallet logic
    - Phase 2: Key management
    - Phase 3: Transaction signing
    - Phase 4: UI implementation

You: "Let's start Phase 1."

AI: [Reads relevant knowledge, implements with full context]
```

**Key benefit**: AI always has the context it needs. No repeated explanations.

---

### Example 2: Batch Knowledge Review

Keep your knowledge base clean and consistent with AI agents.

```
You: "Run 100 agents to review all knowledge docs.
      Check if they follow AKB principles and fix them."

AI: [Spawns parallel agents, each reviewing documents]

    Agent 1: learnings/docker-basics.md
    - Missing TL;DR → Added
    - No contextual links → Added "Next Steps" section
    - Good keyword density

    Agent 2: projects/api-server/architecture.md
    - TL;DR present
    - File too long (350 lines) → Split into 2 docs
    - Links in frontmatter → Moved to body

    ... (98 more agents)

    Summary:
    - 23 docs updated, 5 docs split, 12 docs merged
    - All now follow AKB methodology
```

**Key benefit**: Maintain consistency at scale without manual review.

---

### Example 3: Context-Aware Debugging

```
You: "The wallet transaction signing is failing."

AI: [Searches knowledge base]
    Found: projects/blockchain-wallet/security-model.md
    Found: projects/blockchain-wallet/tech-decisions.md
    Found: tasks/archive/wallet-phase2-key-management.md

    [Reads relevant context, understands the design decisions]

    "Based on your security model that uses HD wallets with BIP-44,
     and your decision to use ethers.js v6, the issue is likely..."
```

**Key benefit**: AI understands *why* things were built this way.

---

## Folder Structure

```
your-knowledge-base/
├── CLAUDE.md                # [Root] AI routing (auto-injected)
│
├── methodology/             # AKB methodology (read this!)
│   └── agentic-knowledge-base.md
│
├── guides/                  # Real-world patterns & guides
│   └── guides.md            # [Hub]
│
├── ideas/                   # Ideation & brainstorming
│   └── ideas.md             # [Hub]
│
├── learnings/               # Technical learning notes
│   └── learnings.md         # [Hub]
│
├── projects/                # Project-specific knowledge
│   └── projects.md          # [Hub]
│
├── tasks/                   # Task tracking
│   ├── tasks.md             # [Hub]
│   ├── active/
│   ├── blocked/
│   └── archive/
│
└── .templates/              # Document templates
    └── templates.md         # [Hub]
```

---

## Writing Documents

For document structure, frontmatter schema, and writing principles, see:

**[AKB Methodology](methodology/agentic-knowledge-base.md)**

Key principles:
- **TL;DR with keywords** - AI finds docs via search
- **Contextual links in body** - AI follows links with context
- **One topic per document** - Keep under 200 lines
- **Keyword-rich filenames** - `wallet-security-model.md` not `security.md`

Templates are in `.templates/` - but usually just ask AI to create docs following AKB principles.

---

## Real-World Patterns

AKB has been used in production projects managing trading systems, ontology design, and multi-agent workflows. The `guides/` directory contains anonymized patterns extracted from real-world usage:

| Guide | What You'll Learn |
|-------|-------------------|
| [CLAUDE.md Design](guides/claude-md-design.md) | Root design: routing tables, working rules, anti-patterns |
| [Skill System](guides/skill-system.md) | Skills as operational playbooks, structure, sync principles |
| [Multi-Agent Delegation](guides/multi-agent-delegation.md) | Passing Root context to sub-agents, required skill paths |
| [Discovery Sprints](guides/discovery-sprints.md) | Hypothesis → Validation → Verdict sprint workflows |
| [Release Cycle](guides/release-cycle.md) | PR-based release note management |

---

## Design Philosophy

AKB was designed based on **observed AI agent behavior**:

- AI skips Hubs, searches Nodes directly via Grep/Glob
- AI doesn't parse Frontmatter metadata (triggers, related, etc.)
- AI follows links that have context in body text

**Design principle:**
> "Don't try to change AI behavior. Optimize documents so AI can find them easily."

---

## License

MIT License - see [LICENSE](LICENSE)

---

## Author

**Seongsu Kang (Ethan)**
- GitHub: [@seongsu-kang](https://github.com/seongsu-kang)
- LinkedIn: [Seongsu Kang](https://www.linkedin.com/in/seongsu-kang-8ab564151)

---

## Contributing

Contributions welcome! Feel free to submit a Pull Request.
