# harn-documents

Deterministic report rendering and portable document artifact construction for
Harn agents.

The package owns document-domain behavior: a small report shape, Markdown and
Typst rendering, renderer argument construction, and portable file/manifest
specs. Harn owns artifact validation, session recording, and protocol
projection.

## Install

```bash
harn add github.com/burin-labs/harn-documents@v0.1.7
```

For local package development:

```bash
harn add ../harn-documents
```

Consumers import the stable module exported by `harn.toml`. The generated
[API reference](docs/api.md) describes every package-owned function.

```harn
import {
  artifact_manifest,
  file_artifact_spec,
  render_markdown_report,
  render_typst_report,
} from "harn-documents/lib"
```

## Reports

Render deterministic source, write it to an explicit artifact path, and invoke
the external renderer only after checking that it is available:

```harn
const report = {
  title: "Review findings",
  summary: "Two findings need attention.",
  findings: [{severity: "high", title: "Validate the input boundary"}],
}

const markdown = render_markdown_report(report)
const typst = render_typst_report(report)
const compile = typst_compile_command("out/report.typ", "out/report.pdf", {})
```

The package returns renderer argv instead of starting processes. The calling
harness retains ownership of command policy, execution, and verification.

## Artifacts

Keep document bytes on disk or in an artifact store. Publish references through
Harn directly; the runtime validates the specs and projects the resulting event
to supported agent protocols:

```harn
const pdf = file_artifact_spec("out/report.pdf", "application/pdf", {
  name: "report.pdf",
  size_bytes: 12345,
  sha256: "sha256:...",
})
const manifest = artifact_manifest([pdf], {title: "Review findings"})

const file_receipt = artifact_emit("file", pdf, {session_id: session_id})
const manifest_receipt = artifact_emit(
  "artifact_manifest",
  manifest,
  {session_id: session_id},
)
```

`artifact_manifest_schema_url()` returns the Harn-owned JSON Schema for the
portable manifest contract:
`https://harnlang.com/schemas/artifact-manifest.v1.schema.json`.

## Development

Use the version in `.harn-version`:

```bash
harn check --strict-types lib.harn main.harn tests/test_main.harn
harn fmt --check lib.harn main.harn tests/test_main.harn
harn lint --strict lib.harn main.harn tests/test_main.harn
harn test tests/ --parallel
harn package check
harn package docs --check
harn package pack --dry-run
```
