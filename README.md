# Assumptions Skill

A Claude Code skill repository for explicitly surfacing, validating, and documenting assumptions before making changes or building anything.

## What this repository is

This repo contains a reusable Claude skill named `assumption-check` that helps an AI assistant:

- identify unstated assumptions in a task
- separate facts from guesses
- ask the user for confirmation before making key decisions
- reduce silent default choices that can lead to rework
- show a short plan for approval before any code is written
- document the final decisions made during a task

The goal is to make AI-assisted work more transparent, safer, and easier to review.

## Included files

- `SKILL.md` — the Claude skill instructions for handling assumptions before coding or changes
- `references/categories.md` — a checklist of assumption categories used to build the ledger
- `references/question-format.md` — question, plan, and ledger templates with good and bad examples

## Why it matters

Many coding tasks include decisions that are not explicitly stated by the user, such as:

- technology choices
- naming conventions
- behavior on failures
- trade-offs between speed and correctness
- scope boundaries
- integration patterns

Without explicit assumption checking, AI systems can make silent choices that look reasonable but may be wrong. This skill forces a short, deliberate confirmation step before building.

## What the skill does

The skill helps the assistant:

1. stop before editing files
2. inspect the relevant code and context
3. restate the goal, what "done" means, and what must not change
4. list the assumptions that would otherwise be guessed, each with its basis and cost if wrong
5. ask only what matters, using a fixed ask-or-proceed rule, with independent questions batched together
6. show a short plan and proceed only after a clear go-ahead
7. save the final decisions, with their status and scope, in `.claude/decisions.md`
8. stop and ask again if something unplanned comes up mid-implementation
9. verify the result and report which decisions were applied and what deviated

## Controls for the user

- **Autonomy setting:** `strict` (ask almost everything), `balanced` (default), or `fast` (ask only about high-cost items).
- **Show assumptions:** type "show assumptions" at any point to see the current ledger.
- **Decision status:** each saved decision is marked `confirmed`, `delegated`, or `default`, and as `task-only` or `project-wide`. Saved decisions are checked against the current code before they are reused.
- **Unattended runs:** when nobody can answer, the skill uses recommended defaults, marks them unconfirmed, and makes no irreversible changes.

## Intended use

Use this skill in projects where you want stronger alignment between the user and the AI before implementation.

It is particularly valuable for:

- feature work
- refactors
- migrations
- integrations
- setup or initialization tasks
- anything where hidden assumptions could change the outcome

It is skipped for pure questions, explanations, code reading, and tiny edits (one file, no behavior change).

## Repository structure

```text
assumptions-skill/
├── SKILL.md
├── README.md
└── references/
    ├── categories.md
    └── question-format.md
```

## Notes

This repository is intentionally minimal and focused on a single practice: making assumptions visible before implementation.

## License

This project is currently provided as a reusable skill repository without a formal license declaration unless you choose to add one later.
