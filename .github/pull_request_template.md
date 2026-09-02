## What changed

<!--
Title this pull request `[Area] Sentence case`, for example:
  [Rendering] Escape pipe characters in Markdown table cells
  [Artifacts] Accept a checksum on a manifest entry
  [CI] Advance the package workflow pin

Then describe the change in three to five sentences. Example:

  A report whose finding title contained a pipe character produced a broken
  Markdown table, because `render_markdown_report` interpolated cell text
  without escaping it. This escapes pipes and backslashes on the way into a
  table cell, leaving every other rendering path untouched. A new case in
  `tests/test_main.harn` fails on the old renderer and passes on the new one,
  and the full suite plus `harn package docs --check` is green. The export
  surface did not change, so this is a patch bump.
-->

## How you verified it

<!--
Name the command you ran and what it showed.

If you changed the export surface, confirm you regenerated `docs/api.md` with
`harn package docs` and added a `## Unreleased` line to `CHANGELOG.md`.

If you touched a renderer, confirm the output is still deterministic: the same
report in gives byte-identical output every run.
-->

## Consumer impact

<!--
Consumers pin a released version. Say whether this is a patch, a minor, or a
breaking change, and why. If it is breaking, say what a pinned consumer has to
do about it.
-->
