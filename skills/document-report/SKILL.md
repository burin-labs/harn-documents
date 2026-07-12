---
name: document-report
short: Create verified document artifacts from agent findings.
description: Generate report-ready Markdown, Typst, PDF, DOCX, or presentation artifacts through harn-documents helpers and explicit renderer preflights.
when-to-use: Use when the user asks for a PDF report, DOCX, Google Docs-ready draft, PowerPoint/Slides outline, or durable file artifact from agent findings.
allowed-tools: ["*"]
---
# Document report

Use `harn-documents` for the deterministic middle of a document workflow:

1. Normalize findings into `{title, subtitle, summary, sections, findings}`.
2. Render Markdown with `render_markdown_report(report)` and Typst source with
   `render_typst_report(report)`.
3. Write the rendered source to explicit workspace artifact paths after the user
   has approved the destination.
4. Preflight external renderers before invoking them. Use
   `typst_compile_command(...)` for PDF and `pandoc_docx_command(...)` for
   DOCX instead of rebuilding renderer arguments.
5. Verify produced files with available deterministic tools such as `stat`,
   `sha256`, `pdftotext`, Poppler rendering, or package-specific checks.
6. Build file references with `file_artifact_spec(...)`, then collect them with
   `artifact_manifest(...)`.
7. On Harn runtimes with first-class file artifacts, emit each file with
   `artifact_emit("file", spec, options)`. For headless or managed-agent logs,
   use `artifact_session_updates_ndjson(...)` to produce canonical Harn ACP
   `session/update` artifact extension frames.
8. For Managed Agents API hosts (`harn serve api`, Harn Cloud), use
   `managed_agent_artifact_register_request(...)` for each produced file and
   `managed_agent_artifact_manifest_register_body(...)` for the manifest file
   instead of hand-building `/v1/artifacts` JSON.

Do not embed PDF/DOCX bytes in transcripts. Keep binary payloads on disk or in an
artifact store, and pass `file://`, `artifact://`, `harn-artifact://`, or `urn:`
references with MIME type, size, and SHA-256 metadata when available.
