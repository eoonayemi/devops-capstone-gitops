<!-- Contributing guidelines for the DevOps Capstone GitOps project -->
# Contributing Guide

## Development Workflow

1. Pick a card from the Trello Backlog
2. Move it to "In Progress"
3. Create a feature branch on your local machine
4. Write code and commit with the correct format
5. Push and open a Pull Request
6. Move the Trello card to "Review/QA"
7. Wait for CI checks to pass
8. Merge the PR
9. Move the card to "Done"

## Branching Rules

- `main` — production-ready code only. **No direct pushes.**
- `feature/TRELLO-###-description` — one branch per Trello card

Create a branch like this:

```bash
git checkout -b feature/TRELLO-003-add-tests
```

## Commit Format

Every commit MUST follow this format:

Examples:

- `[TRELLO-001] Set up repository structure`
- `[TRELLO-002] Configure GitHub Actions CI pipeline`
- `[TRELLO-003] Add palindrome test case`

Commits that do not reference a Trello ID will be flagged in code review.

## Pull Request Process

1. PR title must include Trello ID: `[TRELLO-###] Description`
2. CI checks (lint + tests) must be green
3. Describe what changed and why
4. Wait for review before merging
5. Delete the feature branch after merge

## CI/CD Explanation

The pipeline (`.github/workflows/ci.yml`) runs automatically on every push and PR.

**Pipeline stages:**

1. **Install** — `pip install -r requirements.txt`
2. **Lint** — `flake8 app.py test_app.py` (must produce zero output)
3. **Test** — `pytest test_app.py -v` (all 8 tests must pass)

If any stage fails, the pipeline goes red and the PR is blocked.

## Coding Standards

- Follow PEP 8 style guide (flake8 enforces this automatically)
- Two blank lines between top-level functions
- Maximum line length: 79 characters
- No unused imports
- Descriptive variable names

## Failure Handling

If CI fails:

1. Click on the red X next to the failing check on GitHub
2. Read the error output
3. Fix the issue locally
4. Commit the fix with `[TRELLO-###] Fix lint/test failure`
5. Push again — CI will re-run automatically
