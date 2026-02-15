---
name: git-skills
description: "Git workflow automation and guidance: stop tracking files or folders and update .gitignore, review the working tree and propose grouped commits with messages for approval, and push or pull with remotes. Use when the user asks to ignore files, remove items from the Git index/cache, organize or write commits, or sync with a remote repository."
---

# Git Skills

## Overview
Handle common Git tasks with safety checks and clear approval gates. Always propose a plan before staging, committing, or running network operations.

## Core workflow
1. Confirm repo root, current branch, and clean or dirty state (`git status -sb`).
2. If the request involves commits, scan diffs and classify changes by intent and scope.
3. Present a complete plan and wait for approval before staging, committing, or pushing or pulling.
4. Execute approved commands and report results.

## Task: Stop tracking files or ignore patterns
- Add precise rules to `.gitignore` for files, folders, or extensions.
- If files are already tracked, remove them from the index with `git rm --cached` (use `-r` for directories) and keep local files intact.
- Stage `.gitignore` and the index removals only after approval.
- Propose a commit message (e.g., `chore(git): stop tracking <pattern>`).

## Task: Group changes into commits
- Read every changed file and infer intent (feat, fix, refactor, docs, test, build, ci, chore) and scope (module or package).
- Keep unrelated changes in separate groups; avoid mixing formatting-only changes with logic.
- Check repo conventions: look for `.gitmessage`, `CONTRIBUTING.md`, commitlint config, or recent `git log -5`.
- If no convention is clear, use Conventional Commits: `type(scope): summary` (<=72 chars).
- Provide all groups and commit messages in one response before running `git add` or `git commit`.

## Task: Push or pull
- Confirm remote and branch if not explicit (`git remote -v`, `git branch --show-current`).
- For pull, prefer `git pull --ff-only` unless the user asks for merge or rebase.
- For push, confirm upstream; avoid force push unless explicitly approved.
- Ask for approval before any network operation.

## Approval plan format
Use this format for commit grouping:
Plan:
1) Group: <name>
   Files: <file1>, <file2>, ...
   Commit message: <message>
2) Group: ...
Ask: "Approve this plan? If yes, I will run the staging and commit commands in this order."
