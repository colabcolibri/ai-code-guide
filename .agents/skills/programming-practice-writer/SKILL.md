---
name: programming-practice-writer
description: Create new project-agnostic programming practice documents from user-provided content. Use when Codex receives notes, examples, code-review learnings, incident findings, implementation patterns, or architecture guidance and must turn them into a structured reusable reference following a consistent taxonomy.
---

# Programming Practice Writer

## Purpose

Use this skill to create new programming practice documents from content provided by the user.

The skill defines the writing taxonomy for source documents. It must not depend on an existing knowledge-base folder, existing references, or project-specific documents. Treat the target location as part of the user's current request or infer it from the repository structure.

## Workflow

1. Identify the durable programming practice inside the user's content.
2. Remove incidental project context: company names, private paths, repository names, internal apps, migration IDs, tickets, PR numbers, and proprietary helper names.
3. Preserve the technical lesson: decision criteria, implementation pattern, validation method, anti-patterns, edge cases, and trade-offs.
4. Classify the content by domain, practice type, risk, maturity, and likely specialist agents.
5. Choose the folder by domain: `database/`, `frontend/`, `backend/`, `testing/`, `security/`, `architecture/`, `devops/`, `data/`, `ai/`, or `general/`.
6. Create one focused document per practice. Split unrelated practices into separate files.
7. Add YAML frontmatter for discovery, filtering, and future relationship mapping.
8. Use neutral examples and generic names.
9. Add diagrams when they clarify architecture, data flow, lifecycle, schema relationships, or decision paths.
10. Update an index only when the user asks for it or when the target folder already has an index pattern.

## Taxonomy

Add YAML frontmatter to every new source document unless the user explicitly asks for plain Markdown. Keep metadata stable and useful for future search, relationship mapping, and agent retrieval.

```yaml
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
intended_agents:
  - code-review
  - backend
  - database
```

Use `related: []` when no relationship exists yet. Use `intended_agents` only for likely consumers, not as a promise that those agents exist.

## Controlled Vocabulary

Use these lists as defaults, not hard limits. Prefer existing values when they fit; create a new value only when it is clearer than forcing a bad match.

### domain

- `database`: SQL, data modeling, migrations, indexing, transactions, query performance, data integrity.
- `backend`: APIs, services, background jobs, domain logic, server-side integration patterns.
- `frontend`: UI architecture, state management, rendering, accessibility, forms, client-side performance.
- `testing`: unit, integration, contract, E2E, fixtures, test data, regression strategy.
- `security`: authentication, authorization, secrets, input handling, isolation, secure defaults.
- `architecture`: system design, boundaries, modularity, coupling, scalability, resilience.
- `devops`: CI/CD, deployment, observability, runtime operations, environments, infrastructure.
- `data`: analytics, pipelines, modeling, quality checks, lineage, warehousing.
- `ai`: LLM usage, retrieval, evaluation, prompting, agent workflows, AI safety in code.
- `general`: cross-cutting engineering practices that do not belong to one technical domain.

### category

Common categories by domain:

- `database`: `search`, `indexing`, `query-performance`, `transactions`, `migrations`, `schema-design`, `constraints`, `rls`, `backup-restore`, `observability`.
- `backend`: `api-design`, `validation`, `error-handling`, `auth`, `background-jobs`, `caching`, `integration`, `concurrency`, `idempotency`.
- `frontend`: `component-design`, `state-management`, `forms`, `accessibility`, `performance`, `routing`, `data-fetching`, `design-system`.
- `testing`: `unit-testing`, `integration-testing`, `e2e-testing`, `contract-testing`, `test-data`, `mocking`, `coverage-strategy`.
- `security`: `authentication`, `authorization`, `secrets`, `input-sanitization`, `dependency-security`, `tenant-isolation`, `auditability`.
- `architecture`: `modularity`, `boundaries`, `event-driven`, `scalability`, `resilience`, `trade-off-analysis`, `decision-records`.
- `devops`: `ci`, `cd`, `deployments`, `observability`, `logging`, `metrics`, `alerts`, `environment-config`.
- `data`: `etl`, `elt`, `data-quality`, `analytics-modeling`, `governance`, `lineage`, `warehouse-design`.
- `ai`: `retrieval`, `evaluation`, `prompting`, `agent-reference`, `tool-use`, `structured-output`, `guardrails`.
- `general`: `code-review`, `documentation`, `naming`, `refactoring`, `debugging`, `maintainability`.

### status

- `draft`: useful but not yet reviewed or proven across more than one context.
- `stable`: reviewed and safe to use as a default reference.
- `proven`: repeatedly used or validated in real projects.

### tags

Tags should be lowercase kebab-case. Prefer concrete technologies, practices, and failure modes:

- technologies: `postgresql`, `react`, `typescript`, `nodejs`, `python`, `stripe`, `redis`.
- practices: `full-text-search`, `indexing`, `rate-limiting`, `idempotency`, `pagination`, `accessibility`.
- qualities: `performance`, `security`, `reliability`, `maintainability`, `observability`, `developer-experience`.
- failure modes: `n-plus-one`, `race-condition`, `slow-query`, `stale-cache`, `injection-risk`, `flaky-test`.

Avoid vague tags like `best-practices`, `important`, `misc`, or `advanced`.

### applies_to

Use human-readable strings for technologies, contexts, or situations:

- `"PostgreSQL"`
- `"user-facing search"`
- `"multi-tenant applications"`
- `"React forms"`
- `"public API endpoints"`
- `"background job processing"`

### related

Use relative paths to source documents when a relationship is known. Keep `related: []` when none is known yet. Do not invent relationships just to fill the field.

### intended_use

Use one or more:

- `human-reference`: primarily useful for engineers reading the guide.
- `agent-reference`: useful as retrieved context for coding agents.
- `code-review-reference`: useful during implementation review.
- `implementation-reference`: useful while building a feature.
- `troubleshooting-reference`: useful when diagnosing a bug, incident, or performance issue.

### intended_agents

Use likely consumer labels only, not promises that the repo contains these agents:

- `code-review`
- `backend`
- `frontend`
- `database`
- `security`
- `testing`
- `architecture`
- `devops`
- `data`
- `ai`

## Document Shape

Use this structure for new references unless the user provides a stronger local convention:

1. Title
2. Purpose
3. Decision Summary
4. When To Use
5. Recommended Practice
6. Implementation Pattern
7. Validation
8. Anti-Patterns
9. Checklist
10. References

## Writing Rules

- Always write source documents in English, regardless of the source material language.
- Use a title specific to the problem or practice, not a generic title like "Boas práticas".
- Use a readable kebab-case filename derived from the title.
- Prefer "prefira", "evite", "use quando" and "trade-off" over absolute claims.
- Make examples executable or close to executable.
- Use visual explanations when helpful: Mermaid `flowchart`, `sequenceDiagram`, `stateDiagram`, `classDiagram`, `erDiagram`, C4-style diagrams in Mermaid, decision tables, timelines, and compact ASCII diagrams are acceptable.
- Prefer Mermaid `erDiagram` for database entity relationships and Mermaid `flowchart` or `sequenceDiagram` for request/query flows.
- Use neutral entities such as `users`, `products`, `contacts`, `documents`, `orders`, or `customers`.
- Replace internal authorization helpers with generic descriptions such as "application authorization function".
- Do not cite private repositories, internal paths, migrations, tickets, incidents, or PRs in the main body.
- If local context is useful, put it in an optional appendix named "Local Notes".
- Keep checklist items actionable and objectively verifiable.

## Quality Bar

A generated practice document is incomplete unless it answers:

- What problem does this practice prevent?
- What should be the default recommendation?
- When is the recommendation not appropriate?
- How should someone implement it?
- How should someone validate it?
- What common mistakes should an agent avoid?
