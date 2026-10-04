# AGENTS.md

<!-- BEGIN HARN SHARED AGENT CONTRACT: managed by harn-bump-fleet -->

## Ecosystem working agreement

- Build ambitious outcomes behind small typed interfaces; give behavior one owner
  and generate or parity-test projections instead of duplicating policy.
- Work autonomously within approved scope. Pause for destructive or production effects,
  exceptional spend, material ambiguity, or new authority.
- Treat stop, wait, stand down, pivot, and steer as control events.
- Use the smallest owning product-path check. Add a falsifier for contested, load-bearing,
  or potentially vacuous claims; record controls, recovery, and blind spots.
- Evidence follows source/artifact identity. Reuse proof when relevant code, build inputs,
  and dependencies are unchanged. Repeat affected checks for relevant changes, failures,
  deployment, or packaging differences. Do not rebuild or recapture solely for main.
- Ship means owning-main integration with terminal merge and applicable release/deploy
  checks. Confirm landed content and result; an open PR is incomplete.
- Use `ship` with a deployed Smart Ship caller; otherwise use `gh pr merge --squash --auto`.
  Never use `--admin`; incidents use `bypass-ci`, `bypass-merge-queue`, or `force-merge`.

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

