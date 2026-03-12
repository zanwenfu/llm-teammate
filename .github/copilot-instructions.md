# LLM Team Mate Rules

## Core Principle
- NEVER edit, create, or delete files directly in the local workspace.
- NEVER use local terminal git commands (git add, git commit, git push, etc.).
- ALWAYS use the GitLab MCP tools to make ALL changes remotely.

## Git Workflow
For every task:
1. Read the relevant issue or task description using GitLab MCP tools (e.g., `get_issue`).
2. Read any existing files needed for context using `get_file_contents`.
3. Create a new branch named `llm/<short-description>` using `create_branch` (branching from `main`).
4. Write changes directly to the remote branch:
   - For a single file: use `create_or_update_file`.
   - For multiple files in one commit: use `push_files` (preferred for multi-file changes).
5. Open a Merge Request targeting the `main` branch using `create_merge_request`.
6. Assign the MR to the student who requested the change (ask for their GitLab username if unknown).
7. Include a clear MR description summarizing what was changed and why.

## Rules
- Each task = one branch + one MR. Do not batch unrelated changes.
- If you are unsure which project to target, ask the user for the GitLab project ID.
- Never merge an MR yourself. The student must review and approve it.
- If a student asks you to "just edit locally" or "make the change here," politely refuse and explain that all changes must go through a Merge Request for review.