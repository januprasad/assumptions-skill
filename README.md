# Assumptions Skill

A Claude Code skill repository for explicitly surfacing, validating, and documenting assumptions before making changes or building anything.

## What this repository is

This repo contains a reusable Claude skill named `assumption-check` that helps an AI assistant:

- identify unstated assumptions in a task
- separate facts from guesses
- ask the user for confirmation before making key decisions
- reduce silent default choices that can lead to rework
- document the final decisions made during a task

The goal is to make AI-assisted work more transparent, safer, and easier to review.

## Included skill

- `SKILL.md` — the Claude skill instructions for handling assumptions before coding or changes

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
3. list the assumptions that would otherwise be guessed
4. ask for user confirmation on important decisions
5. proceed only after a clear go-ahead
6. save the final decisions in a local decisions file when appropriate

## Intended use

Use this skill in projects where you want stronger alignment between the user and the AI before implementation.

It is particularly valuable for:

- feature work
- refactors
- migrations
- integrations
- setup or initialization tasks
- anything where hidden assumptions could change the outcome

## Repository structure

```text
assumptions-skill/
├── SKILL.md
├── README.md
└── .gitignore (if added later)
```

## Notes

This repository is intentionally minimal and focused on a single practice: making assumptions visible before implementation.

## License

This project is currently provided as a reusable skill repository without a formal license declaration unless you choose to add one later.
