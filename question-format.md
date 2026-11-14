# Question format

Templates and examples for step 6 (ask) and step 8 (plan) of `SKILL.md`. The goal is to sound like a careful colleague: short, plain, and specific.

## A single question

```
<Plain-language question>? <Intention and reason: "I plan to X because Y.">
<Basis: file name, or "this is a guess">. <What changes depending on the answer.>

(a) <Option> (Recommended)
(b) <Option>, <short trade-off>
(c) <Option>, <short trade-off>
```

Example:

> Where should I store login sessions? Your project already uses PostgreSQL (see `db/config.py`), so I plan to use it. This decides whether I add a new dependency.
>
> (a) PostgreSQL (Recommended)
> (b) Redis, faster but a new service to run
> (c) In memory, lost on restart

## A batched round

Use when the decisions are independent: answering one does not change the options of another. At most 4 per round. Open with the goal sentence (first round only) and a progress line.

> You want password reset by email, so users can recover accounts without support. Round 1 of about 2: scope and behavior.
>
> 1. **Link lifetime.** I'm guessing 1 hour, since nothing in the code covers it. (a) 1 hour (Recommended) (b) 24 hours (c) 15 minutes
> 2. **Wrong email address.** Should the page say "no such account", or always say "if that account exists, we sent an email"? I plan the second, because it does not reveal which emails are registered. (a) Same message for all (Recommended) (b) Say "no such account"
> 3. **Existing sessions.** After a reset, should other logged-in sessions be signed out? I plan yes. (a) Yes (Recommended) (b) No

If question 1 changes what you ask in round 2, say so: "Depending on this, I may ask one more thing about expiry."

## Dependent questions

Ask the first alone and wait:

> Before the details: should this live in the existing `api/` service, or in a new service? This decides most of the other choices.

## Defaults list (in the plan, not asked)

For low-cost items that follow evidence in the code:

> Defaults I'll use: 2-space indentation and `camelCase` names (as in `src/`), tests in `tests/` with pytest (as in the existing tests), error messages in the same style as `errors.py`.

## The plan

```
Goal: Add password reset by email so users can recover accounts without support.
Done when: A user can request a reset, get an email, set a new password; old link stops working.
Not touching: Login flow, the user table schema.
Decisions: Link lifetime 1 hour (confirmed). Same message for unknown emails (confirmed). Sign out other sessions (delegated).
Defaults I'll use: Existing email helper in `mail.py`; tests in `tests/`.
Plan: 1. Add token model. 2. Add two endpoints. 3. Add email template. 4. Add tests.
Verification: Run `pytest tests/auth`; request a reset by hand against the dev server.
What could break: Existing session handling if sign-out is done in the wrong place.

Proceed with this plan?
```

## Bad and good wording

| Bad | Good |
|---|---|
| "Which persistence layer should be used?" | "Where should I store login sessions?" |
| "Confirm error-handling strategy?" | "If the API times out, should I retry or show an error right away?" |
| "Should I follow existing conventions?" (for each of 12 items) | One defaults list in the plan |
| "Is it OK to proceed?" (after a long silent plan) | "Proceed with this plan?" after the short plan above |

## Showing the ledger on request

When the user types "show assumptions":

| Decision | Default | Basis | Cost if wrong | Status |
|---|---|---|---|---|
| Link lifetime | 1 hour | guess | low | confirmed |
| Sign out other sessions | yes | convention | medium | delegated |
| Email helper | `mail.py` | evidence | low | default |

## Unattended run note

At the top of the end-of-task report:

> Nobody was available to answer, so these are unconfirmed: link lifetime (used 1 hour), sign-out of other sessions (used yes). Blocked: dropping the old `reset_tokens` table (high cost). Question to unblock: "Is it safe to drop the old table, and is there a backup?"
