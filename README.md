# harn-documents

Deterministic document report helpers and file artifact references for Harn
agents.

`harn-documents` is deliberately a Harn package, not a Burin package. Harn owns
the reusable artifact vocabulary, report intermediate representation, package
metadata, and skill instructions. Burin can layer coding-agent report UX on top
without pushing PDF, DOCX, or renderer dependencies into Harn core.

## Quickstart

```bash
harn add ../harn-documents
harn test tests/
harn package check
harn package docs
harn package pack
```

Consumers import stable modules through the `[exports]` entries in `harn.toml`.

```harn
import { file_artifact_spec, render_markdown_report, render_typst_report } from "harn-documents/lib"
```

The package returns deterministic Markdown and Typst source. Workflows can write
those strings to files, invoke `typst compile` or `pandoc`, then build a
portable file reference with `file_artifact_spec(path, mime, {})`. On Harn
runtimes with first-class file artifacts, publish that reference with
`artifact_emit("file", spec, options)`.

## Layering

- Harn core: safe file artifact references and managed-agent artifact APIs.
- `harn-documents`: reusable report/document helpers and skills.
- Burin: coding-agent-specific prompts, report buttons, previews, and product UI.
