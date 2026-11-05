# AGENTS.md - card-game-api-ts-playwright

Repository contract for any AI coding agent working here. Read this file, and the shared
workflow it links, before editing.

## Purpose

API automated tests for the Deck of Cards service at `https://deckofcardsapi.com`, written in
TypeScript with Playwright. `tests/card.game.test.ts` plays a card-game scenario against the live
service; `api/deck.api.ts` wraps the HTTP calls. This is a public portfolio repository, not a
deployed product and not a library anyone installs.

The repository is **archived** on GitHub. GitHub rejects pushes while it stays archived, so any
branch, PR, or merge needs explicit unarchiving authorization. Do not change archive state as a
side effect of another task, and leave `archive` unchanged when only the contents are in scope.

## Ownership

Maintained by Anton Gulin (`i@anton.qa`, https://anton.qa). Scope, publication, merge, and
unarchive decisions belong to Anton; an agent proposes, it does not assume. The public identity in
every metadata field, docstring, and attribution string is **Anton Gulin**.

## Local Contracts

Small, flat tree. The files that carry the contracts:

- `AGENTS.md` - this contract.
- `docs/dox-LICENSE.txt` - MIT notice for the DOX framework text adapted here.
- `package.json` - npm metadata, two dependencies (`@playwright/test`, `dotenv`), no scripts.
- `package-lock.json` - committed, lockfile version 3. It must stay in sync with `package.json`;
  dependency changes need explicit authorization.
- `playwright.config.ts` - test directory `./tests`, HTML reporter, Chromium project, base URL
  hardcoded to the public service.
- `api/deck.api.ts` - page-object style wrapper over the deck endpoints.
- `tests/card.game.test.ts` - the suite, organised into named test cases and steps.
- `.github/workflows/playwright.yml` - runs the suite on push and pull request to `main`.
- `.github/workflows/code-review.yml` - calls the shared Robin review workflow
  (`antongulin/robin/.github/workflows/review.yml@main`).
- `.gitignore` - ignores `node_modules/`, `.env`, reports, and editor files.
- `README.md` - human setup and usage instructions.

Configuration and side effects:

- `BASE_URL` is read from `.env` locally and from the `BASE_URL` GitHub secret in CI. `.env` is
  gitignored. Never commit it, print its values, or copy secrets into prompts or logs.
- Tests call a live public API. They need network access and produce no local state beyond
  `playwright-report/` and `test-results/`, both ignored.

## Work Guidance

- Inspect the real files before changing them. There is one source line or one scalar per change in
  most tasks here; keep the diff that small.
- Keep dependency and lockfile bytes untouched unless the task is explicitly about dependencies.
  Release engineering, upgrades, and installs are separate work.
- GitHub Actions: new or changed jobs use the standard Ubicloud runner, `runs-on:
  ubicloud-standard-2`. The existing `playwright.yml` job still uses `ubuntu-latest`; migrating it
  is separate, separately authorised work, not a side effect.
- The Robin `review` job takes a `runner` input. Its contract is a JSON-encoded string, so the label
  is written as `'"ubicloud-standard-2"'` (quoted inside quoted), not as a bare label.
- Merge strategy: squash by default for one cohesive PR, subject to the repository actually
  permitting squash merges. The archived repository's merge-setting response did not expose
  `allow_squash_merge`, so verify the setting before merging rather than assuming it.
- Shared workflow rules are not duplicated here. Read `~/.agents/instructions/WORKFLOW.md`, or
  https://github.com/antongulin/baseline/blob/main/baseline/02-agents.md when that file is absent.

## Verification

Run only what the change can break. This repository has no lint, typecheck, or unit-only path.

- `npx playwright test` - the full suite. Requires `BASE_URL` and live network access to the public
  service, so it fails without either. It is not runnable offline and is not a substitute for reading
  the diff.
- `python3 -c "import json; json.load(open('package.json'))"` - confirms the manifest still parses
  after a metadata edit.
- `git diff --check` - catches whitespace damage.
- CI: the `Playwright API Tests` workflow is the authoritative suite. The last recorded run on
  2026-06-17 failed, so do not claim a green suite without a current run on the change.

## DOX rules

This hierarchy follows the DOX framework (https://github.com/agent0ai/dox). The parts that bind
every change here:

- Read before editing: read this file, walk from the root to each path you will touch, and read the
  nearest `AGENTS.md` for that path.
- Update after editing: every meaningful change gets a documentation pass. Update this file when
  purpose, structure, commands, contracts, permissions, or this index change. Remove stale text
  instead of explaining history.
- Hierarchy: this is the only root. A child `AGENTS.md` is created only when a folder becomes a
  durable boundary with its own rules, and it must use the order Purpose, Ownership, Local
  Contracts, Work Guidance, Verification, Child DOX Index.
- Closeout: re-check changed paths, refresh this index if anything moved, and run the checks above
  when relevant. Report docs deliberately left unchanged.

## Child DOX Index

None. Every path is covered by this root file, and no directory here carries its own durable rules.
Add a child only when that stops being true.

## Framework attribution

This documentation structure adapts the DOX framework from https://github.com/agent0ai/dox at
revision `765ae4ac02cc884eefcd41a3d0f71941721adb89`, retrieved 2026-11-05. Its MIT license is
preserved in [`docs/dox-LICENSE.txt`](docs/dox-LICENSE.txt).
