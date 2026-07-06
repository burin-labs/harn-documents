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
import {
  artifact_manifest,
  artifact_manifest_emit_args,
  artifact_manifest_schema_url,
  artifact_manifest_session_update,
  artifact_session_updates_ndjson,
  file_artifact_spec,
  managed_agent_artifact_manifest_register_body,
  managed_agent_artifact_register_request,
  render_markdown_report,
  render_typst_report,
} from "harn-documents/lib"
```

The package returns deterministic Markdown and Typst source. Workflows can write
those strings to files, invoke `typst compile` or `pandoc`, then build a
portable file reference with `file_artifact_spec(path, mime, {})`. On Harn
runtimes with first-class file artifacts, publish that reference with
`artifact_emit("file", spec, options)`.

`artifact_manifest_schema_url()` returns the Harn-owned JSON Schema for the
manifest contract:
`https://harnlang.com/schemas/artifact-manifest.v1.schema.json`.

For headless and managed-agent flows, collect produced files into a manifest and
emit canonical Harn ACP artifact updates:

```harn
let report = file_artifact_spec("out/report.pdf", "application/pdf", {
  size_bytes: 12345,
  sha256: "sha256:...",
})
let manifest = artifact_manifest([report], {title: "Code findings"})
let updates = artifact_session_updates_ndjson(manifest.artifacts, {})
let manifest_update = artifact_manifest_session_update(manifest, {})
let emit = artifact_manifest_emit_args(manifest, {})
// artifact_emit(emit.kind, emit.spec, emit.options)
```

For Managed Agents API hosts such as `harn serve api` or Harn Cloud, convert the
same file references into deterministic `/v1/artifacts` request descriptors:

```harn
let request = managed_agent_artifact_register_request(report, {
  visibility: "internal",
  session_id: "ses_123",
  task_id: "task_456",
})
let manifest_body = managed_agent_artifact_manifest_register_body(
  manifest,
  "artifact://session/artifact-manifest.json",
  {session_id: "ses_123"},
)
```

## Layering

- Harn core: safe file artifact references and managed-agent artifact APIs.
- `harn-documents`: reusable report/document helpers, file artifact manifests,
  ACP update helpers, Managed Agents artifact request helpers, and skills.
- Burin: coding-agent-specific prompts, report buttons, previews, and product UI.
