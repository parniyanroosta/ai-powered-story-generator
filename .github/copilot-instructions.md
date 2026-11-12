# GitHub Copilot instructions

## Project purpose
This repository contains an AI-powered personalized story app that helps caregivers teach children aged 4–7 about everyday situations, emotions, and behaviours. Prioritize a safe, understandable, useful MVP over optional enhancements.

## Start with the project sources of truth
Before planning or changing the project, inspect the relevant current files:
- `docs/PROJECT_DEFINITION.md` — product scope and goals
- `docs/USER_STORIES_ACCEPTANCE_CRITERIA.md` — user needs and testable outcomes
- `delivery/ROADMAP.md` — milestone sequence
- `delivery/CURRENT_STATUS.md` — verified delivery state
- `delivery/DECISIONS.md` — decisions already made

Also inspect the relevant implementation, tests, GitHub issue, and pull request when available. Treat repository contents and verified GitHub state as authoritative; do not assume a task is complete from a plan or an issue title alone.

## How to work
- Follow the repository's delivery-assistant skill at `.claude/skills/delivery-assistant/SKILL.md` for planning, issue selection, and the end-to-end development/review workflow. GitHub Copilot supports project skills stored in `.claude/skills`; do not create a duplicate copy unless the skill is intentionally relocated.
- Work on one issue at a time, using a focused branch from the latest `main`. Never implement task changes directly on `main`.
- Keep changes limited to the requested issue and its acceptance criteria. Prefer the smallest clear implementation; avoid speculative features and unnecessary abstractions.
- Before coding, state assumptions and surface ambiguity or tradeoffs. Ask the user when uncertainty could materially change the implementation; do not silently choose between plausible interpretations.
- Run relevant tests and checks, and manually verify acceptance criteria where appropriate. Report exactly what was and was not run; never claim a check passed without evidence.
- Open a pull request to `main`, link the issue, and summarize scope, tests, and limitations. Wait for the user's review and approval before merging or starting another issue. Rebase on the latest `main` before final merge, resolve conflicts carefully, and rerun relevant checks.
- Update delivery documentation only when the corresponding progress or decision is verified. Never invent issue numbers, test results, project status, or successful GitHub actions.

## Keep project guidance current
If instructions conflict with the actual codebase or a newer user decision, point out the conflict and ask which source should govern. When a durable project decision changes, propose updating the appropriate document rather than silently allowing instructions to drift.
