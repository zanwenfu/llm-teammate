# LLM Teammate

Use GitHub Copilot as a coding teammate that is **forced to go through code review** — every change it makes is pushed to a GitLab Merge Request that you must manually review and approve.

## How It Works

When you ask Copilot to make a code change, it will:
1. Create a new branch (`llm/<description>`) on GitLab
2. Push the changes directly to the remote branch
3. Open a Merge Request for you to review

Copilot will **never** edit files locally. You are required to review and approve every MR before it is merged.

## Setup

### Prerequisites
- [VS Code](https://code.visualstudio.com/) with [GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat) extension
- [Node.js](https://nodejs.org/) (for `npx`)
- A GitLab account on `coursework.cs.duke.edu`

### 1. Create a GitLab Personal Access Token
1. Go to [https://coursework.cs.duke.edu/-/user_settings/personal_access_tokens](https://coursework.cs.duke.edu/-/user_settings/personal_access_tokens)
2. Create a new token with the **`api`** scope
3. Copy and save the token — you'll need it each time VS Code starts the MCP server

### 2. Find Your GitLab Project ID
Your project ID is displayed on the main page of your GitLab project, directly below the project name.

### 3. Clone This Repo and Open in VS Code
```bash
git clone <your-project-url>
code <project-folder>
```

### 4. Start a Copilot Chat
When you open a Copilot chat, VS Code will prompt you for:
- **GitLab Personal Access Token** — paste the token from step 1
- **GitLab Project ID** — enter the ID from step 2

The GitLab MCP server will start automatically.

### 5. Protect Your Main Branch (Recommended)
To enforce that MRs require approval before merging:
1. Go to your GitLab project → **Settings** → **Repository** → **Protected branches**
2. Ensure `main` is protected and requires at least **1 approval** before merge

This prevents anyone (including the LLM) from merging without human review.

## File Overview

| File | Purpose |
|------|---------|
| `.github/copilot-instructions.md` | Rules Copilot follows every chat (no local edits, always use MRs) |
| `.vscode/mcp.json` | MCP server config connecting Copilot to the GitLab API |

## Troubleshooting

- **401 Unauthorized**: Your PAT may be expired or missing the `api` scope. Regenerate it.
- **MCP server not starting**: Ensure Node.js is installed and `npx` is available. Restart VS Code.
- **Copilot editing locally**: Remind it to follow the instructions, or start a new chat session. The rules in `.github/copilot-instructions.md` are loaded automatically each session.
