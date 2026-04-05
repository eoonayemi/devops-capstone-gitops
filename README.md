# DevOps Capstone – GitOps Workflow

## Project Overview

This project demonstrates a GitOps-style development workflow for a lightweight
internal Flask API service. Git is the single source of truth. All work is tracked
through Trello, enforced through GitHub Actions CI, and documented for fast onboarding.

## Architecture

The application is a Python Flask API with three endpoints:

- `GET /health` — returns service health status
- `POST /sum` — accepts two numbers and returns their sum
- `POST /reverse-string` — accepts a string and returns it reversed

## Workflow Description

1. A task is created as a card in Trello (Backlog)
2. Developer creates a feature branch: `feature/TRELLO-###-description`
3. Code is written and committed with the format: `[TRELLO-###] Description`
4. A Pull Request is opened — CI pipeline runs automatically
5. CI must pass (lint + tests) before the PR can be merged
6. Card moves to Done after merge

## Commit Convention

Every commit must reference a Trello ID:

## Setup Instructions

```bash
# Clone the repository
git clone https://github.com/yourusername/devops-capstone-gitops.git
cd devops-capstone-gitops

# Install dependencies
pip install -r requirements.txt

# Run tests
pytest test_app.py -v

# Run linter
flake8 app.py test_app.py

# Run the app
python app.py
```

## Reflection Answers

### 1. What is GitOps and why is Git the "single source of truth"?

GitOps is a practice where Git is used as the authoritative record for
everything in a system — not just code, but also configuration, workflows,
and infrastructure definitions. Before GitOps, teams would make changes
directly on servers or through manual processes, making it impossible to
track what changed, when, and why. By making Git the single source of truth,
every change becomes visible, reviewable, and reversible. In this project,
the CI/CD pipeline is defined in ci.yml inside the repository itself. This
means the pipeline is versioned alongside the code — if something breaks,
you can see exactly which commit caused it and roll it back. The Trello IDs
in commit messages create a direct link between business requirements (the
task card) and technical implementation (the code change), which helps future
team members understand why code was written the way it was.

### 2. What problems does CI/CD solve in a development team?

Without CI/CD, developers push code manually, and broken code often makes
it into the main codebase because nobody caught the error in time. This is
called "integration hell." CI (Continuous Integration) solves this by
automatically running linting and tests every time code is pushed. In this
project, flake8 checks that the code follows Python style rules (no messy
formatting, no unused imports), and pytest verifies that all the API endpoints
still work correctly. If either check fails, the CI pipeline turns red and
the pull request is blocked — meaning bad code cannot be merged. This gives
the team confidence that the main branch is always in a working state, and
developers catch problems immediately rather than days later.

### 3. What is the purpose of linting and why does code style matter?

Linting is automated checking of code for style problems and potential errors
before the code even runs. flake8 checks Python code against PEP 8, which is
the official Python style guide. Code style matters because software is read
far more often than it is written. If one developer writes code in a messy
style, other team members spend extra mental energy reading it. Consistent
style means any developer can open any file and understand it quickly. In this
project, flake8 enforces rules like two blank lines between functions, no
trailing whitespace, and maximum line length. Making linting a required CI
step means style cannot be ignored — developers are forced to write clean code
before their changes can be merged.

### 4. How does the branching strategy support safe collaboration?

The branching strategy used here protects the main branch. Nobody is allowed
to push directly to main — every change must go through a feature branch and
a pull request. The branch naming convention (feature/TRELLO-###-description)
makes it immediately clear what each branch is for. This means multiple
developers can work simultaneously on different features without stepping on
each other. Pull requests add a review step where a teammate (or CI checks)
must approve the work before it merges. If a feature branch breaks something,
only that branch is affected — main stays clean. This mirrors professional
team practices used at real software companies.

### 5. What did you learn about developer onboarding and documentation?

Onboarding documentation is often neglected but it is one of the highest-value
investments a team can make. The goal of GETTING_STARTED.md is that a
completely new developer can clone the repo, run the tests, and understand the
workflow in under one hour. This forces you to think about every hidden
assumption your setup has. For example, you might forget to document that
Python must be installed, or that the email used for git config must match
GitHub. Writing good documentation also reveals gaps in your own understanding
— if you cannot explain a step simply, you may not fully understand it
yourself. In this project, the combination of README (what this is),
GETTING_STARTED (how to run it), and CONTRIBUTING (how to contribute to it)
creates three layers of documentation that serve different readers at different
stages.
