---
title: "Tasks"
akb_type: hub
status: active
tags:
  - "type/hub"
  - "domain/tasks"
---

# Tasks

> This Hub is a TOC for humans. Track your work items here.

## TL;DR

- **Purpose**: Task tracking and TODO management
- **Structure**: active/ (in progress), blocked/ (waiting), archive/ (done)
- **Keywords**: tasks, todo, work items, progress tracking

---

## Task Folders

| Folder | Description | Status |
|--------|-------------|--------|
| `active/` | Currently working on | In Progress |
| `blocked/` | Waiting on something | Blocked |
| `archive/` | Completed tasks | Done |

---

## Active Tasks

| Task | Priority | Started |
|------|----------|---------|
| (none) | - | - |

---

## How to Add Tasks

1. Copy template: `cp ../.templates/task-template.md ./active/task-name.md`
2. Fill in the checklist
3. Update this Hub
4. Move to `archive/` when done

---

## Task Template Fields

```yaml
---
title: Task Title
akb_type: node
status: planned|in_progress|blocked|done
tags:
  - "type/task"
  - "priority/high|medium|low"
depends_on: []
---
```

---

## Next Steps

- For task template → [task-template.md](../.templates/task-template.md)
- For project context → [projects.md](../projects/projects.md)
- For learning notes → [learnings.md](../learnings/learnings.md)
