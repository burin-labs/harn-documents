# AGENTS.md

<!-- BEGIN HARN SHARED AGENT CONTRACT: managed by harn-bump-fleet -->

## Ecosystem working agreement

- Pursue the ambitious product outcome; make the seams boring with small typed
  interfaces, explicit invariants, and deterministic projections.
- Give each behavior one semantic owner. Generate or parity-test other surfaces
  instead of maintaining competing implementations.
- Work autonomously inside approved scope. Pause for destructive, production,
  high-spend, ambiguous, or authority-expanding actions—not routine reversible work.
- Treat stop, wait, stand down, and pivot as control events for long-lived work.
- Match evidence to the claim. Use the smallest owning product-path check;
  add a falsifier for contested, load-bearing, or potentially vacuous claims.
  Record relevant controls, recovery, and blind spots without repeating proof.
- Evidence follows source and artifact identity, not the branch name. Reuse
  verified branch or merge-candidate evidence after landing when relevant code,
  build inputs, and dependencies are unchanged. Repeat affected checks only
  for a relevant change, observed failure, deployment, or packaging difference.
- "Ship" means integrated on owning main with terminal integration checks and
  applicable release or deployment checks complete. Confirm the landed change
  and merge result; do not rebuild or recapture screenshots solely for main.
- Ship a ready PR by adding the `ship` label when the repo has a Smart Ship
  caller (`.github/workflows/smart-ship.yml`); otherwise land through the merge
  queue with `gh pr merge --squash --auto`. Never `gh pr merge --admin`.
  Incidents use the org override labels `bypass-ci`, `bypass-merge-queue`, or
  `force-merge`.

<!-- END HARN SHARED AGENT CONTRACT -->

<!-- Repository-specific guidance below. The fleet manages only the block above. -->

## This package

harn-documents is a published Harn package, so its exports are a contract that
pinned consumers depend on. Read [`CONTRIBUTING.md`](CONTRIBUTING.md) before
changing anything under `[exports]` in `harn.toml`.

Two rules are easy to break and expensive to catch late:

- The package renders documents and returns renderer argument lists. It never
  starts a process. Command execution belongs to the calling harness.
- Renderers are deterministic. The same report must produce byte-identical
  output on every run.

Regenerate `docs/api.md` with `harn package docs` rather than editing it, and
add a `## Unreleased` line to `CHANGELOG.md` for any consumer-visible change.

## Pull request titles

Title every pull request `[Area] Sentence case`, for example
`[Rendering] Escape pipe characters in Markdown table cells`. Common areas here
are `Rendering`, `Artifacts`, `Skills`, `Docs`, and `CI`.

