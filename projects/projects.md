---
title: "Projects"
akb_type: hub
status: active
tags:
  - "type/hub"
  - "domain/projects"
---

# Projects

> This Hub is a TOC for humans. Organize project-specific knowledge here.

## TL;DR

- **Purpose**: Project-specific technical knowledge
- **Structure**: One folder per project with its own Hub
- **Keywords**: projects, documentation, technical knowledge

---

## Project List

| Project | Description | Status |
|---------|-------------|--------|
| (empty) | Add your projects here | - |

---

## Suggested Project Structure

```
projects/
├── projects.md              # This Hub
│
├── project-a/               # Project A
│   ├── project-a.md         # Project Hub
│   ├── architecture.md      # System design
│   ├── api/                 # API documentation
│   │   └── api.md
│   └── guides/              # How-to guides
│       └── guides.md
│
└── project-b/               # Project B
    └── project-b.md
```

---

## How to Add a Project

1. Create folder: `mkdir project-name`
2. Create Hub: `cp ../.templates/hub-template.md ./project-name/project-name.md`
3. Add documentation as needed
4. Update this Hub

---

## Project Hub Template

Each project should have:

1. **TL;DR**: What is this project? Key technologies?
2. **Architecture**: System overview
3. **Quick Start**: How to get started
4. **Documents List**: What's in this folder
5. **Next Steps**: Where to go from here

---

## Next Steps

- For Hub template → [hub-template.md](../.templates/hub-template.md)
- For task tracking → [tasks.md](../tasks/tasks.md)
- For learning notes → [learnings.md](../learnings/learnings.md)
