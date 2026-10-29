# Contributing to Tracewick

Thank you for your interest in Tracewick! This is the default contributing guide for every
repository in the Tracewick organization. A repository may ship its own `CONTRIBUTING.md` with
setup instructions and extra rules; when it does, that file takes precedence.

## Before you start

- For anything larger than a small fix, open an issue first so we can agree on the approach.
- Architecture decisions are recorded as ADRs in each repository's `docs/adr/` directory. A change
  that contradicts an accepted ADR needs a new ADR.

## Rules

- **Fail-open.** Tracewick runs inside production processes. Code must never throw into, block, or
  noticeably slow down the host application. Failures are swallowed, counted and reported through
  diagnostics.
- **Tests** accompany every change. Never skip, disable or delete a test to make CI pass.
- **Language.** Code, comments, commit messages, issues and documentation are written in English.

## Branching model

Tracewick follows [git flow](https://nvie.com/posts/a-successful-git-branching-model/):

- `main` holds released code only; every commit on it is a tagged release.
- `develop` is the integration branch. Feature pull requests target `develop`.
- `feature/<short-name>` branches start from `develop` and merge back into it.
- `release/<version>` and `hotfix/<version>` branches merge into both `main` (tagged) and
  `develop`.

## Commits and pull requests

- Commit messages and PR titles follow [Conventional Commits](https://www.conventionalcommits.org/),
  for example `feat(encoder): add pprof encoder` or `fix(sampler): keep event type on reset`.
- Keep pull requests focused: one logical change per PR.
- Update `CHANGELOG.md` under `Unreleased` when users will notice the change.

## License

By contributing, you agree that your contributions are licensed under the
[Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0).
