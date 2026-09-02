# Repository settings proposal

This file **proposes** changes to GitHub repository settings. It does not apply
them. Repository and organization settings are the founder's to change, so
treat every item below as a recommendation waiting on a decision.

Written during the org-wide repository hygiene sweep on 2026-09-01.

## What this repository is

harn-documents is a published Harn package, not a scaffold. It ships tagged
releases through v0.1.7, a generated API reference, a maintained changelog, a
test suite, and a packaged skill. Consumers install it by version with
`harn add github.com/burin-labs/harn-documents@v0.1.7`, which makes its exports
a contract rather than an implementation detail.

That is why this repository got fuller contributor documentation than the
vendored grammar wrappers in the same sweep, and why the recommendations below
keep it open rather than locking it down.

One thing to be clear about: there is no evidence of external users today. The
repository has no stars, no forks, no external pull requests, and no issues, and
every commit is from a single maintainer or from automation. The case for
treating it as real rests on it being a versioned library with a public install
path and a published API contract, not on observed adoption.

## Proposed changes

| Setting | Today | Proposed | Why |
| --- | --- | --- | --- |
| Issues | Enabled | **Keep enabled** | Anyone who installs a released version needs a way to report that it does not work. |
| Discussions | Disabled | Enable only if a question actually arrives | Speculative. An empty discussions tab reads as a dead project, which is worse than not having one. |
| Wiki | Check and disable if enabled | Disabled | `README.md`, `CONTRIBUTING.md`, and the generated `docs/api.md` are the documentation. A wiki would let the same facts drift apart. |
| Projects | Check and disable if enabled | Disabled | No planning happens here. |
| Pull requests from non-members | Allowed | **Keep allowed** | This is a library with a public install path, and there is no vendored supply-chain surface to protect. An outside fix is welcome and reviewable. |
| Branch protection on `main` | Verify | Require the CI status check and a pull request | The package workflow already gates `harn package check` and `harn package docs --check`. Requiring it keeps a broken install off a release tag. |
| Merge strategy | Verify | Squash only, delete branch on merge | Keeps history one commit per change, matching the rest of the org. |
| Description | Empty | **Set one** | The repository has no GitHub description. Reuse the manifest's: "Deterministic document report helpers and file artifact references for Harn agents." |

## Deliberately not proposed

- **Archiving or making it private.** Consumers resolve released versions from
  this public repository. Either change breaks installs.
- **Restricting outside pull requests.** Appropriate for the vendored grammar
  wrappers, wrong here. A published library that refuses patches is telling
  people not to depend on it.
