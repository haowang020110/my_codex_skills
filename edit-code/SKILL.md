---
name: edit-code
description: Python code modification workflow with mandatory backups, inline change notes, and user review/approval. Use when asked to modify `.py` files or Python code. If the request targets any non-Python file, pause and ask the user to confirm a Python file target.
---

# Edit Code

## Overview

Edit Python code safely with per-file backups, inline change notes, and explicit user review before finalizing.

## Workflow

1. Locate project instructions.
   - Look for `AGENTS.md` or `agents.md` at the project root and follow it.
   - If neither exists, invoke `$project-agents` to generate `AGENTS.md` at the project root before proceeding.
   - If additional context is needed, skim `README.md` and nearby docs for conventions.

2. Enforce Python-only scope.
   - Edit only files ending in `.py`.
   - If any requested target is not a `.py` file, pause and ask the user to provide or confirm a Python file path before editing.

3. Confirm file format supports comments.
   - Python files support `#` comments; if the target format is not comment-friendly, pause and ask how to record change notes.

4. Create a backup before any edits.
   - For `path/to/file.ext`, create `path/to/file_bak.ext`.
   - If there is no extension, create `path/to/file_bak`.
   - If a backup already exists, ask whether to overwrite it.

5. Apply minimal edits only.
   - Keep changes concise.
   - Do not refactor or alter the existing structure.
   - Touch only lines required to achieve the requested change.

6. Annotate every change inline.
   - Add a short comment at each modification site in Python using a consistent tag like `# NOTE(change): ...`.
   - Example: `# NOTE(change): adjust bounds check`

7. Present changes for review.
   - Show the modified snippets (or a focused diff) with the inline notes.
   - Ask for explicit approval.

8. Handle approval outcome.
   - If approved: delete the `_bak` backup file(s) and remove inline `NOTE(change)` comments from the modified file(s).
   - If not approved: ask whether to redo from scratch or make small fixes.
     - Redo: delete the modified file, restore from the `_bak` backup, then start over.
     - Small fixes: keep the backup and continue editing with new notes.

## Multi-file edits

Repeat the backup/annotate/review steps per Python file. Do not delete any backups until all files are approved.

## New files

If a request requires creating a new file with no prior version to back up, confirm with the user before proceeding. New files must be Python files (`.py`) for this skill.
