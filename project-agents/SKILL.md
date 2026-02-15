---
name: project-agents
description: "Read a codebase (entire project or a specified subpath) to extract API interface specifications, core internal logic, and module interactions, then summarize and update the project's AGENTS.md. Use when asked to study a project, review or reference code, or provide a structured overview of how the system works (e.g., 'study this project', 'reference the code', 'review this part of the code')."
---

# Project Agents

## Overview

Enable consistent project understanding by producing or updating AGENTS.md with API specs, core logic, and module interaction notes for the current project or a specified subpath.

## Workflow Decision Tree

- If the user provides a path, scope all analysis to that subpath and note the scope in AGENTS.md.
- If AGENTS.md exists at the project root, update relevant sections and preserve unrelated content.
- If AGENTS.md does not exist, create it in the project root using the template below.

## Step 1: Confirm scope and objectives

- Identify the target root or subpath and the expected depth.
- Check `.gitignore` for default exclusions; include ignored paths only when explicitly requested.
- Determine the public API surfaces to inspect (HTTP, RPC, CLI, event topics, internal service interfaces).
- Ask for clarification if the requested scope or output format is ambiguous.

## Step 2: Map the codebase quickly

- Use `rg --files` and `rg` to locate entry points, routers, controllers, handlers, and schema or type definitions.
- Skip directories listed in `.gitignore` during discovery unless explicitly requested.
- Record top-level modules or directories and their responsibilities.
- List key configuration and bootstrap files that control wiring and runtime behavior.

## Step 3: Extract API interface specifications

- For each API surface, record: location, protocol, endpoint or command, inputs and outputs, auth, errors, and versioning.
- Capture shared request or response types and validation rules.
- Include precise file paths and symbol names for each spec.

## Step 4: Summarize core logic

- For each core module, describe responsibilities, key functions or classes, and critical algorithms or business rules.
- Note data stores, external integrations, and side effects.
- Keep summaries factual; mark unknowns and avoid speculation.

## Step 5: Describe module interactions

- Explain how modules call or depend on each other, including flow order and shared models.
- Highlight cross-cutting concerns (auth, caching, logging, config).
- If helpful, describe high-level sequence flows in bullets.

## Step 6: Update AGENTS.md

- Update or create `AGENTS.md` in the project root only; do not add extra docs unless requested.
- Preserve existing content outside the sections you touch.
- Use concise bullets, include file paths, and keep the scope explicit.

### AGENTS.md template

```markdown
# AGENTS

## Scope
- Target root or subpath:
- Notes on exclusions:

## API Interface Specs
### <API surface name>
- Location:
- Protocol:
- Endpoints/commands:
- Inputs:
- Outputs:
- Auth:
- Errors:
- Versioning:
- Related types/schemas:

## Core Logic
### <Module name>
- Responsibilities:
- Key symbols:
- Data flow:
- Integrations/side effects:

## Module Interactions
- <Module A> -> <Module B>: <summary>
- Cross-cutting concerns:

## Key Files and Entry Points
- <path>: <why it matters>

## Open Questions (optional)
- <unknowns or follow-ups>
```

## Quality checks

- Ensure each major claim points to a file path or symbol.
- Keep the summary scoped to the requested root or subpath.
- Re-read AGENTS.md for clarity, completeness, and consistency.
