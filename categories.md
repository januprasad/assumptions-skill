# Assumption categories

A checklist for building the assumption ledger (step 4 of `SKILL.md`). Go through each category and ask: "Does the request already answer this, or would I have to choose?" Skip a category when the answer is obvious from the request or the code.

## Scope

- Which files, modules, or services are in scope, and which are explicitly out?
- Is this a minimal change or a broader cleanup? (Refactoring nearby code, renaming, reformatting.)
- Does the task include docs, migrations, or config changes?
- What does "done" look like? What should not be touched?

## Technology choices

- Which language features, libraries, frameworks, or services to use?
- New dependency or existing one? Which version?
- Build, run, or deploy tooling that the change must work with.

## Conventions

- Naming, file layout, formatting, and code style (usually dictated by the surrounding code).
- Where new code should live and how it should be structured.
- Commit, branch, or PR conventions if the task includes them.

## Data and edge cases

- Input validation: what is valid, what happens with empty, huge, or malformed input?
- Data formats, schemas, and migrations. Is existing data affected?
- Time zones, locales, encodings, currencies, units.
- Concurrency and ordering, if more than one thing can happen at once.

## Behavior on failure

- Retry, fail fast, fall back, or ask the user?
- What does the user see on error, and what gets logged?
- Is partial success acceptable, or must it be all-or-nothing?

## Side effects

- Does the change write, delete, send, charge, or publish anything outside the code?
- Are there public interfaces, APIs, or file formats that other code or people depend on?
- Is any step irreversible? (Treat as high cost. See the checkpoint rule in step 8.)
- Security and permissions: secrets, access control, personal data.

## Testing

- Which tests to add or update, and at what level?
- How will the change be verified (commands, manual steps)?
- Is it acceptable to leave existing failing tests alone?

## Constraints

- Compatibility: supported versions, platforms, browsers, or backward compatibility.
- Performance or size limits.
- Deadlines or "good enough for now" versus "production quality".
- The existing test and CI setup: what must pass before this can merge?

## Typical high-cost items

Always worth asking about, whatever the basis:

- Deleting or rewriting data, or running a migration.
- Changing a public interface or data format.
- Adding a service, paid dependency, or anything with ongoing cost.
- Anything that sends messages, makes payments, or touches production.
