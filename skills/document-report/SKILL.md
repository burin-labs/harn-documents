---
name: document-report
short: Create verified document artifacts from agent findings.
description: Generate report-ready Markdown, Typst, PDF, DOCX, or presentation artifacts through harn-documents helpers and explicit renderer preflights.
when-to-use: Use when the user asks for a PDF report, DOCX, Google Docs-ready draft, PowerPoint/Slides outline, or durable file artifact from agent findings.
allowed-tools: ["*"]
---
# Document Report

Use `harn-documents` for the deterministic middle of a document workflow:

1. Normalize findings into `{title, subtitle, summary, sections, findings}`.
2. Render Markdown with `render_markdown_report(report)` and Typst source with
   `render_typst_report(report)`.
3. Write the rendered source to explicit workspace artifact paths after the user
   has approved the destination.
4. Preflight external renderers before invoking them:
   - `typst compile <report.typ> <report.pdf>` for PDF.
   - `pandoc <report.md> --from gfm --to docx -o <report.docx>` for DOCX.
5. Verify produced files with available deterministic tools such as `stat`,
   `sha256`, `pdftotext`, Poppler rendering, or package-specific checks.
6. Build file references with `file_artifact_spec(...)`. On Harn runtimes with
   first-class file artifacts, emit them with `artifact_emit("file", spec, options)`.

Do not embed PDF/DOCX bytes in transcripts. Keep binary payloads on disk or in an
artifact store, and pass `file://`, `artifact://`, `harn-artifact://`, or `urn:`
references with MIME type, size, and SHA-256 metadata when available.
