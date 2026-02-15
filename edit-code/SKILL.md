---
name: edit-code
description: Code modification workflow with mandatory backups, inline change notes, and user review/approval. Use when asked to modify files or code (e.g., "modify X file", "change code", "complete these edits", "修改xxx，实现xxx", "修改xxx（文件名），实现xxx（修改目标）") and the work must be backed up, annotated, and reviewed before finalizing.
---

# Edit Code

## Overview

Edit code safely with per-file backups, inline change notes, and explicit user review before finalizing.

## Workflow

1. Locate project instructions.
   - Look for `AGENTS.md` or `agents.md` at the project root and follow it.
   - If neither exists, invoke `$project-agents` to generate `AGENTS.md` at the project root before proceeding.
   - If additional context is needed, skim `README.md` and nearby docs for conventions.

2. Confirm file format supports comments.
   - If the file format does not allow comments (e.g., strict JSON), pause and ask the user how to record change notes before editing.

3. Create a backup before any edits.
   - For `path/to/file.ext`, create `path/to/file_bak.ext`.
   - If there is no extension, create `path/to/file_bak`.
   - If a backup already exists, ask whether to overwrite it.

4. Apply minimal edits only.
   - Keep changes concise.
   - Do not refactor or alter the existing structure.
   - Touch only lines required to achieve the requested change.

5. Annotate every change inline.
   - Add a short, language-appropriate comment at each modification site.
   - Use a consistent tag like `NOTE(change): ...`.
   - Examples:
     - Python: `# NOTE(change): adjust bounds check`
     - JS/TS/Java/C/C++: `// NOTE(change): ...`
     - HTML: `<!-- NOTE(change): ... -->`

6. Present changes for review.
   - Show the modified snippets (or a focused diff) with the inline notes.
   - Ask for explicit approval.

7. Handle approval outcome.
   - If approved: delete the `_bak` backup file(s) and remove inline `NOTE(change)` comments from the modified file(s).
   - If not approved: ask whether to redo from scratch or make small fixes.
     - Redo: delete the modified file, restore from the `_bak` backup, then start over.
     - Small fixes: keep the backup and continue editing with new notes.

## Multi-file edits

Repeat the backup/annotate/review steps per file. Do not delete any backups until all files are approved.

## New files

If a request requires creating a new file with no prior version to back up, confirm with the user before proceeding.
