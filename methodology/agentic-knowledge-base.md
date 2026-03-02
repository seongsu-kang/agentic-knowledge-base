---
title: Agentic Knowledge Base (AKB)
akb_type: node
status: active
tags:
  - type/how-to
  - domain/akb
---

# Agentic Knowledge Base (AKB)

**Autonomous Navigation Knowledge Protocol for AI Agents**

> This document is the **Canonical Reference** for AKB.

---

## TL;DR

- **Definition**: A file-based knowledge system where AI **searches** via Grep/Glob and **navigates** via contextual links
- **Essence**: File-based Lightweight Ontology (Tags = Types, Body Links = Edges)
- **Philosophy**: Optimize documents so AI can find them easily
- **Structure**: Root (CLAUDE.md) → Hub (Human TOC) → Node (Actual Information)
- **Core Rules**: 4 writing principles (TL;DR, Contextual Links, Keyword Optimization, Atomicity)

---

## Definition

> "Code is logic that machines execute. AKB is context that agents think with."

AKB is a **file-based connected knowledge system** designed for AI agents to autonomously **search**, **learn**, and **retrieve** context without requiring infrastructure like Vector DBs.

### Core Philosophy

> "Don't try to inject everything into AI at once.
> Instead, give it **well-structured documents** that are easy to find."

---

## Essence: File-Based Ontology

> "Infuse the essence of Ontology into Markdown"

```
┌─────────────────────────────────────────────────────┐
│           AKB = Lightweight Knowledge Graph          │
├─────────────────────────────────────────────────────┤
│                                                     │
│   Ontology/KG                AKB                    │
│   ───────────                ───                    │
│   Entity (Node)       →      .md file               │
│   rdf:type            →      tags: [type/]          │
│   domain              →      tags: [domain/]        │
│   rdfs:comment        →      TL;DR section          │
│   Edge/Relationship   →      Contextual links       │
│                                                     │
└─────────────────────────────────────────────────────┘
```

---

## Architecture

AKB has a 3-tier hierarchy: **[Root] → [Hub] → [Node]**

```
project/
├── CLAUDE.md                      # [Root] Minimal routing (direct paths to key files)
│
└── projects/
    │
    ├── blockchain-wallet/         # [Hub] Human TOC
    │   ├── blockchain-wallet.md   #   └─ Hub entry point
    │   └── key-management.md      # [Node] Specific knowledge
    │
    ├── security/
    │   ├── security.md            # [Hub]
    │   ├── encryption/
    │   │   ├── encryption.md      # [Sub-Hub]
    │   │   ├── hd-wallet.md       # [Node] ← AI finds directly via search
    │   │   └── seed-phrase.md     # [Node]
```

### Roles by Layer

| Layer | Role | Description |
|-------|------|-------------|
| **Root** (CLAUDE.md) | Minimal routing | Auto-injected as system prompt, provides key file paths |
| **Hub** ({folder}.md) | Human TOC | For understanding folder contents; AI reads selectively |
| **Node** (*.md) | Actual information | What AI searches directly via Grep/Glob |

---

## Schema Specification

### Frontmatter

```yaml
---
title: "Document Title"
akb_type: hub|node
status: active|draft|deprecated
tags:
  - "type/..."      # Document type
  - "domain/..."    # Domain classification
---
```

| Field | Type | Purpose |
|-------|------|---------|
| `title` | string | Document identification |
| `akb_type` | enum | Distinguish hub/node |
| `status` | enum | Document lifecycle |
| `tags` | array | Domain classification (helps Grep search) |

### Tags (Classification)

| Namespace | Purpose | Examples |
|-----------|---------|----------|
| `type/` | Document type | `type/how-to`, `type/reference`, `type/api-guide` |
| `domain/` | Domain classification | `domain/wallet`, `domain/security` |

---

## Writing Principles (4 Rules)

### Rule 1: TL;DR Required + Keyword Optimization

Include **core keywords naturally** so AI can find them via Grep.

```markdown
## TL;DR

- **HD Wallet**: BIP-44 path implementation
- **Private Key**: Encryption and **Keystore** management
- **Transaction Signing**: Logic implementation
```

**Guidelines:**
- 3-5 bullet points
- **Bold core keywords** (Grep search targets)
- One line each

### Rule 2: Contextual Links (Placed in Body)

Place links **within the flow of body text**.

**Example 1: Natural inline placement**
```markdown
The core of this wallet is the **[HD Wallet structure](./hd-wallet-structure.md)**.

For key storage, see [Keystore Encryption](./keystore-encryption.md).
```

**Example 2: Next Steps section**
```markdown
## Next Steps

- If you need transaction signing → [transaction-signing.md](./transaction-signing.md)
- If building a multisig wallet → [multisig-wallet.md](./multisig-wallet.md)
```

**Why this works:**
- Context gives AI a "reason to follow" the link
- Links are discovered naturally within reading flow

**Less effective pattern:**
```markdown
## Related Documentation  ← Context-free list
- [hd-wallet-structure.md](./hd-wallet-structure.md)
- [keystore-encryption.md](./keystore-encryption.md)
```
→ Without context, AI struggles to judge "why should I follow this?"

### Rule 3: Keyword-Optimized Filenames

Include **core keywords in filenames** for Grep/Glob discoverability.

```
❌ Vague
wallet.md
security.md

✅ Specific
hd-wallet-bip44.md
keystore-encryption.md
transaction-signing-flow.md
```

### Rule 4: Atomicity

- One document = one topic
- Under 200 lines recommended (AI token efficiency)
- When too long, split and connect via Hub

---

## Body Structure Template

```markdown
# Title

## TL;DR

- **Keyword1**: Description
- **Keyword2**: Description
- **Keyword3**: Description

---

## Body

### Section 1

Content...
See `path/file.md` for details. (explicit path)

### Section 2

Content...

---

## Next Steps

- If [Scenario A] → [fileA.md](./fileA.md)
- If [Scenario B] → [fileB.md](./fileB.md)
- If [Scenario C] → [fileC.md](../folder/fileC.md)
```

---

## Hub Role

```
Hub = Human TOC (Table of Contents)
      + Keyword collection that helps Grep searches
```

**Hub serves three purposes:**
1. Humans use it to understand folder contents
2. Rich in search keywords, so Grep can catch it
3. AI reads it selectively when it needs structural overview

---

## CLAUDE.md Routing Strategy

CLAUDE.md is included in the system prompt, so it has **size constraints**.

### Routing Principles

```markdown
# CLAUDE.md

## Routing Table

| Task | Entry Point |
|------|-------------|
| Wallet overview | `projects/blockchain-wallet/blockchain-wallet.md` (Hub) |
| HD Wallet impl | `projects/blockchain-wallet/hd-wallet-bip44.md` |
| Transaction signing | `projects/blockchain-wallet/transaction-signing.md` |
```

**Principle:**
- Frequently used key files → direct paths
- Everything else → Hub reference

---

## Comparison with Other Approaches

| Comparison | AKB | RAG | System Prompt |
|------------|-----|-----|---------------|
| Infrastructure | None | Vector DB | None |
| Token Efficiency | Load only what's needed | Chunk-based | Load everything |
| AI Navigation | Grep + Contextual Links | Similarity search | None |
| Maintenance | Edit files | Re-indexing | Edit prompts |

---

## Summary

> **AKB** is a file-based knowledge system designed for AI to autonomously navigate knowledge.

**Key takeaways:**
- Minimal frontmatter (4 fields only)
- Connect via contextual links in body
- Hubs are human TOC
- Optimize filenames and TL;DR for keyword search

> "Don't try to change AI behavior. Optimize documents so AI can find them easily."

---

## Next Steps

- If you need templates → [../.templates/templates.md](../.templates/templates.md)
- If you want real-world patterns → [../guides/guides.md](../guides/guides.md)

---

## Design Background

AKB was designed by analyzing actual AI agent behavior patterns.

**Observed AI behavior:**
- Skips Hubs, searches Nodes directly via Grep/Glob
- Doesn't parse Frontmatter metadata (triggers, related, etc.)
- Follows links that have context in body text

**Design principle:**
> "Don't try to change AI behavior. Optimize documents so AI can find them easily."

This principle led to minimizing Frontmatter, strengthening contextual links in body text, and including search keywords in filenames and TL;DR sections.

### AKB Does Not Dictate How AI Navigates

**The responsibility lies with the document designer, not the AI.**

| Misunderstanding | Correct Understanding |
|------------------|----------------------|
| "AI must consciously navigate using AKB" | AKB does not prescribe how AI navigates |
| "AI should meta-recognize Hub intersections" | AI simply finds the information it needs |
| "Is AI following AKB principles?" | If the answer is good, AKB worked |

**Key insight:**
> If AI naturally found the information it needed and produced a good answer, that's proof AKB is working.
> AI doesn't need to meta-consciously think "Am I following AKB right now?"
> That's the document designer's responsibility, not AI's.
