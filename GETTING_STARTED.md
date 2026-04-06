<!-- Onboarding guide – target: new developer set up in under 1 hour -->
# Getting Started Guide

Welcome! This guide will get you up and running in under 1 hour.

## Prerequisites

Before you begin, make sure you have:

- Python 3.8 or higher installed
- Git installed
- A GitHub account
- A terminal / command prompt

## Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/devops-capstone-gitops.git
cd devops-capstone-gitops
```

## Step 2: Install Dependencies

```bash
pip install -r requirements.txt
```

This installs Flask (the web framework), pytest (for testing), and flake8 (linter).

## Step 3: Run the Tests

```bash
pytest test_app.py -v
```

You should see 8 tests all passing (green). If any fail, check that your
Python version is 3.8+.

## Step 4: Run the Linter

```bash
flake8 app.py test_app.py
```

No output = no problems. Any output means there is a style issue to fix.

## Step 5: Understanding the Branch Workflow

Never work directly on main. Always create a feature branch:

```bash
# First, make sure main is up to date
git checkout main
git pull origin main

# Create your branch (replace ### with your Trello card ID)
git checkout -b feature/TRELLO-###-your-description
```

## Step 6: Making Commits

Every commit must reference a Trello ID:

```bash
git add .
git commit -m "[TRELLO-###] Short description of what you did"
git push origin feature/TRELLO-###-your-description
```

## Step 7: Opening a Pull Request

1. Go to the repository on GitHub
2. Click "Compare & pull request" (it appears after you push)
3. Title format: `[TRELLO-###] Your description`
4. Wait for the CI pipeline to pass (green checkmark)
5. Merge the PR

## Troubleshooting

**"pip is not recognized"** — Python is not in your PATH. Reinstall Python and
check "Add to PATH" during installation.

**"git is not recognized"** — Git is not installed. Download from git-scm.com.

**Tests fail with "ModuleNotFoundError: flask"** — Run `pip install -r requirements.txt` again.

**flake8 shows errors** — Read the error message carefully. It tells you the file,
line number, and what the problem is. Common fixes: add blank lines between functions,
remove trailing spaces, shorten long lines.

**CI fails on GitHub but tests pass locally** — Check that your local Python version
matches. Also check that you didn't accidentally leave a syntax error in a file.
