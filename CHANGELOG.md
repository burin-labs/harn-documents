# Changelog

## 0.1.5

- Moved the public `lib` export to `lib.harn` so installed consumers can import
  helpers with the documented `harn-documents/lib` module path.

## 0.1.4

- Added deterministic Managed Agents `/v1/artifacts` request helpers for
  registering file specs and artifact manifests, listing artifacts, and reading
  metadata/content paths.

## 0.1.3

- Added bundle-level artifact manifest session-update helpers and
  `artifact_emit` argument construction for Harn's first-class
  `artifact_manifest` runtime kind.

## 0.1.2

- Added exported artifact manifest schema URL, version, and MIME helpers for
  the Harn-owned `harn.artifacts.v1` contract.

## 0.1.1

- Added file artifact manifest helpers and canonical Harn ACP artifact update
  NDJSON rendering for headless and managed-agent flows.

## 0.1.0

- Added deterministic Markdown and Typst report rendering helpers.
- Added file artifact reference helpers for Harn `artifact_emit("file", ...)`.
- Added document-report skill instructions for PDF/DOCX artifact workflows.
