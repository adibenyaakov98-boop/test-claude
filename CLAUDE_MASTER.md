# CLAUDE.md - Master Template

This file provides guidance to Claude Code when working on this project.

## GitHub Integration

**Automatic GitHub Connection & Push**

Claude automatically:
1. Initializes git locally and commits after each file change
2. Pushes to a public GitHub repository under `adibenyaakov98-boop`
3. Handles version control—no manual commits needed

**SETUP REQUIRED - First Time Only:**
Before Claude can push to GitHub, you must:

1. **Create GitHub Repository** (using GitHub CLI):
   ```bash
   gh auth login  # if not already authenticated
   gh repo create <repo-name> --public --source=. --remote=origin --push
   ```
   Or create manually on github.com and run:
   ```bash
   git remote add origin https://github.com/adibenyaakov98-boop/<repo-name>.git
   git branch -M main
   git push -u origin main
   ```

2. **GitHub CLI Setup** (one-time):
   - Install: https://cli.github.com
   - Authenticate: `gh auth login`
   - Grant these permissions: `repo`, `workflow`, `read:org`

3. **Git Configuration** (one-time):
   ```bash
   git config --global user.name "Claude Code"
   git config --global user.email "noreply@anthropic.com"
   ```

Once set up, all changes are automatically committed and pushed to preserve complete development history.

## Claude Code Settings

**Defaults for this project:**
- Model: `haiku` (or specify your preferred model)
- Thinking: Enabled for complex tasks
- Priority: Quality & testing, then documentation

## Quick Start

### Prerequisites
- [e.g., Node.js 18+, Python 3.10+, Git, etc.]

### Setup
```bash
# [Brief setup command if needed]
```

## Core Commands

**Testing** (most important)
```bash
# [Test command]
```

**Development**
```bash
# Build/Run: [command]
# Lint: [command]
# Format: [command]
```

## Project Structure

```
[project-root]/
├── [directory]     - [Brief purpose]
├── [directory]     - [Brief purpose]
└── [directory]     - [Brief purpose]
```

## Code Standards

### Testing
- **Requirement**: Every feature must have tests before deployment
- **Coverage**: Aim for [X]% coverage on core logic
- **Run tests**: `[test command]` before committing

### Documentation
- Add docstrings/comments for complex logic
- Update README for user-facing changes
- Keep code self-documenting (clear variable names, small functions)

### Code Style
- [Any specific conventions or patterns to follow]

## What Claude Should Focus On

1. **Quality first**: Write clean, tested code over quick solutions
2. **Test early**: Write tests alongside code, not after
3. **Document as you go**: Clear commits, meaningful variable names
4. **Ask when uncertain**: Clarify requirements before building
