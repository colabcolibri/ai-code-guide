# AI Code Guide

Practical, project-agnostic programming references for humans and AI coding agents.

## Purpose

This repository stores durable programming practices: recommended decisions, trade-offs, implementation patterns, validation steps, and anti-patterns.

The goal is not to ship agents, prompts, automations, or specialist tooling directly. The goal is to maintain a practical knowledge base that can be referenced by humans, coding agents, custom instructions, agent memory, or future specialist tools.

The only agent-facing asset in this repository is a helper skill for writing new source documents consistently. It exists to keep the knowledge base well structured; it is not the product of the repository.

## Index

| Document | Domain | Main Use |
| -------- | ------ | -------- |
| [Horizontal Scaling and Load Balancing Best Practices](architecture/horizontal-scaling-and-load-balancing-best-practices.md) | Architecture | Vertical vs horizontal scaling, load balancers, L4/L7 trade-offs, algorithms, and operational validation |
| [Server-Sent Events Best Practices](backend/server-sent-events-best-practices.md) | Backend | SSE, EventSource, real-time updates, Redis Pub/Sub fanout, connection management, and WebSocket trade-offs |
| [Database Sharding Best Practices](database/database-sharding-best-practices.md) | Database | Horizontal database scaling, shard keys, routing, rebalancing, distributed queries, and sharding trade-offs |
| [PostgreSQL Text Search Best Practices](database/postgresql-text-search-best-practices.md) | Database | Full Text Search, `pg_trgm`, GIN indexes, ranking, performance, and search safety |

## Principles

- Separate durable technical knowledge from local project context.
- Explain when a practice applies and when it does not.
- Include concrete examples and objective validation steps.
- Document anti-patterns because they help agents avoid common regressions.
- Write for both humans and agents: predictable structure, clear language, and low coupling.
- Track source inspiration separately from official references so readers can understand where a guide started without making the guide dependent on that source.

## File Conventions

- Use kebab-case names that are readable to humans, for example `postgresql-text-search-best-practices.md`.
- Group content by domain: `database/`, `frontend/`, `backend/`, `testing/`, `security/`, `architecture/`, `devops/`, `data/`, `ai/`.
- One file should cover one coherent practice. Split the document when it starts mixing independent decisions.
- Update this index whenever adding, moving, or renaming a reference.

## Source Metadata

Each source document should start with YAML frontmatter so the knowledge base can later be searched, related, or imported into agent tooling without rewriting every file.

Use this shape:

```yaml
---
title: "Human-readable title"
domain: database | backend | frontend | testing | security | architecture | devops | data | ai | general
category: "Specific category inside the domain"
status: draft | stable | proven
last_reviewed: YYYY-MM-DD
tags:
  - tag-one
  - tag-two
applies_to:
  - "Technology, language, framework, or context"
related:
  - "relative/path-to-related-source.md"
intended_use:
  - human-reference
  - agent-reference
---
```

Keep metadata useful, not exhaustive. Prefer stable tags and relationships over trying to model everything upfront.

## Source Attribution

When a guide is inspired by an article, video, talk, thread, code review, incident, or documentation page, include a short source note in the guide.

Use this shape:

```markdown
## Source Inspiration

This guide was inspired by:

- [Title or short description](https://example.com): one-sentence note about the specific idea, example, or framing adapted from the source.

## References

- Official documentation and stable technical references.
```

Keep source inspiration separate from references:

- `Source Inspiration` explains where the guide originated.
- `References` lists authoritative or supporting technical material.
