---
title: AKB Templates Guide
akb_type: hub
status: active
tags:
  - "type/hub"
  - "domain/templates"
---

# AKB Templates

> This Hub is a TOC for humans.

## TL;DR

- **Purpose**: Templates for writing AKB-style documents
- **Types**: Hub Template, Node Template, Task Template
- **Key Features**: Minimal frontmatter, contextual links, keyword optimization

---

## Template List

| Template | Purpose | When to Use |
|----------|---------|-------------|
| [hub-template.md](./hub-template.md) | Folder entry point (Human TOC) | Creating new folder |
| [node-template.md](./node-template.md) | Regular document | Writing new document |
| [task-template.md](./task-template.md) | Task tracking (TODO) | Adding tasks |

---

## How to Use

### Step 1: Copy Template

```bash
# Hub (folder entry point)
cp .templates/hub-template.md [folder]/[folder].md

# Node (regular document)
cp .templates/node-template.md [folder]/[name].md
```

### Step 2: Write Frontmatter (Minimal)

**Required fields only**:

```yaml
---
title: "Document Title"
akb_type: hub|node
status: active|draft|deprecated
tags:
  - "type/..."
  - "domain/..."
---
```

| Field | Description | Example |
|-------|-------------|---------|
| `title` | Document title | "HD Wallet Implementation" |
| `akb_type` | AKB layer | `hub` or `node` |
| `status` | Document status | `active`, `draft`, `deprecated` |
| `tags` | Classification | `["type/how-to", "domain/wallet"]` |

### Step 3: Write TL;DR (Keyword Optimization)

```markdown
## TL;DR

- **HD Wallet**: BIP-44 path implementation
- **Keystore**: Private key encryption and storage
- **Transaction Signing**: Sign and broadcast logic
```

**Rules:**
- 3-5 bullet points
- **Bold keywords** (Grep search targets)
- One line each

### Step 4: Add Contextual Links

```markdown
## Next Steps

- For transaction signing → [transaction-signing.md](./transaction-signing.md)
- For multisig wallets → [multisig-wallet.md](./multisig-wallet.md)
```

**Rules:**
- Place in **body text**, not Frontmatter
- Include **context** with links
- Use relative paths (`./`, `../`)

---

## Best Practices

### DO

- Frontmatter: only 4 fields (title, akb_type, status, tags)
- TL;DR: **bold keywords**
- Body: **contextual links**
- Filenames: **include keywords** (grep-friendly)
- Keep under 200 lines

### DON'T

- ~~Use triggers, related in Frontmatter~~ (AI doesn't read them)
- ~~Obsidian `[[]]` format~~ → Use markdown links
- ~~List links without context~~
- ~~Vague filenames~~ (e.g., `strategy.md`)

---

## Next Steps

- To understand AKB principles → [agentic-knowledge-base.md](../methodology/agentic-knowledge-base.md)
- For project knowledge → [projects.md](../projects/projects.md)
