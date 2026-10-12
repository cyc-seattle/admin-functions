# AGENTS.md

Guidance for coding agents working in this repository.

## Overview

A deprecated, archived CLI that runs reports: it copies Clubspot data into Google Sheets.
`ReportRunner` (`src/runner.ts`) reads the "Reports" worksheet of a config spreadsheet and runs
each enabled row. Each `Report` subclass registers in the `reports` map in `src/reports.ts`. It
uses the published `@cyc-seattle/commodore`, `gsuite-sdk`, and `clubspot-sdk` packages.

## Development

mise provides the tools in `mise.toml`. Run `mise trust`, then `mise run install`.

- `mise run ci` — `check`, then `test`
- `mise run check` — typecheck, Prettier, and ESLint
- `mise run format` — fix formatting with Prettier and ESLint
- `mise run test` — run the tests with vitest

Run the CLI with `pnpm exec tsx src/main.ts`. There is no build step.

## Authentication

Google and Clubspot auth are separate.

- **Google:** Application Default Credentials from `gcloud auth application-default login`, as
  your own account. Never log in as a super-admin.
- **Clubspot:** `CLUBSPOT_EMAIL` and `CLUBSPOT_PASSWORD`, or `-u` for the username. The password
  has no short flag, and `--password` is hidden, because a secret on argv leaks into `ps` and
  shell history. Never commit a credential.

## Testing

Tests live in `test/` and run with vitest. Mock the external SDK boundary (Parse,
google-spreadsheet, googleapis) and test pure logic. `test/roster.test.ts` is the pattern:
hand-rolled mocks and no live API.

## Comments

Comments explain **why**, not what. Keep them to a line or two. Write one where a reader would
otherwise get it wrong: a non-obvious constraint, a surprising API behavior, or a decision that
looks arbitrary but isn't.

- Don't narrate the code, restate the diff, or argue for the approach you chose.
- Cite an issue (`#107`) instead of recounting its discussion.
- Don't cite a local plan file.
- Test each comment: if you deleted it, would a competent reader still make the same change
  correctly? If yes, delete it.

The same applies to docs:

- **Record the outcome, not the path to it.** Say what to do today, not what failed on the way.
- **No personal identifiers.** Use a role name or `<placeholder>` instead of an email address or a
  numeric account ID.

## Workflow

- PR titles are conventional commits. PRs merge by squash.
- Never push to `main`.
