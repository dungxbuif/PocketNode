# PocketNode Spec Decomposition Design

Date: 2026-05-29

## Source

- Source spec: `docs/product/SPEC.md`
- Intake type: New spec
- Harness lane: High-risk
- Desired output: exhaustive product decomposition, not implementation yet

## Approved Direction

PocketNode should be decomposed into living Harness artifacts instead of using
`docs/product/SPEC.md` as the long-term operating plan. The source spec remains
input material. Future work should rely on smaller product docs, epics, story
candidates, decision records, and validation matrix rows.

This is an academic learning project. Every completed task must leave a
learning record that explains the concrete skills practiced, what was learned,
and how the lesson applies to future PocketNode work.

The MVP direction is a browser-only web product:

- Next.js/PWA web client as the only MVP client surface.
- Go backend API for account/server workflows, consent-aware AI processing,
  telemetry, and optional cloud processing.
- No mobile app in MVP.
- No desktop app in MVP.
- No local Go daemon in MVP.
- Browser-native local-first capabilities are MVP product requirements, not
  only future research.

## Stack Certainty

Firm MVP commitments:

- Browser-only web MVP.
- Go backend API.
- Google login for user accounts.
- Server-side AI may be used only after explicit user consent.
- Local ledger behavior must continue to work without AI consent.
- Browser-native local SQLite, sync, encrypted backup, and local AI capability
  proof are part of MVP acceptance.

Capability-gated browser commitments:

- Local SQLite should use browser-compatible SQLite, preferably SQLite WASM with
  OPFS where supported.
- CRDT/local sync should use a browser-side operation log or change-set model
  with HLC-style ordering and deterministic merge behavior.
- LAN discovery cannot be promised as automatic mDNS in every browser. MVP
  should define this as manual peer pairing or browser-supported local pairing,
  using QR/code/link exchange, WebRTC, relay-assisted setup, or available local
  network APIs.
- Google Drive E2EE backup must encrypt client-side before upload. The Go
  backend must not receive plaintext backup data for this flow.
- Local AI benchmarks should run in the browser using WASM/WebGPU-capable
  models where available, with explicit fallback behavior when device capability
  is insufficient.

Longer-term surfaces:

- Flutter mobile comes after the web MVP.
- Rust/Tauri desktop comes after mobile or when native local capabilities become
  a priority.
- Stronger local/offline AI can follow the web MVP and benchmark findings.

## Product Docs To Create

Create English living product docs under `docs/product/`:

| File | Purpose | Source coverage |
| --- | --- | --- |
| `overview.md` | Product vision, actors, MVP boundaries, roadmap sequence, and non-goals. | Core philosophy, system context, user roles |
| `ledger.md` | Wallets, categories, transactions, transfers, budgets, quick entry, audit trail. | FR-1, FR-5.4, NFR performance |
| `receipt-ai.md` | Consent-first receipt processing, extraction JSON, review flow, tax extraction, bulk processing, local benchmark expectations. | FR-2, FR-5.3, FR-5.5 |
| `assistant.md` | Ledger Assistant, quick prompts, voice/text transaction drafting, text-to-SQL constraints, chart/table outputs. | FR-3 |
| `sync-backup.md` | Browser-local SQLite, operation log, CRDT/HLC merge, peer pairing, Google Drive E2EE backup and restore. | FR-4, NFR-3 |
| `imports-reconciliation.md` | Vietnamese bank imports, Money Lover parser, dynamic mapper, categorization, reconciliation scoring. | FR-2.3, FR-5.1, FR-5.2 |
| `privacy-security.md` | Google login, consent gates, zero-knowledge boundaries where applicable, retention, deletion, app lock, secret handling. | NFR-1, AI fallback notes |
| `platforms.md` | MVP web/PWA surface, post-MVP mobile and desktop surfaces, browser constraints. | Container diagram, platform notes |
| `telemetry-commercial.md` | Anonymous telemetry, crash reporting, Pro/lifetime account model, metadata allowlist. | NFR-4, section 6 |
| `poc-roadmap.md` | MVP capability gates and post-MVP research gates. | Technology PoC plan |

Create academic learning records under `docs/learning/`:

| File | Purpose |
| --- | --- |
| `README.md` | Explains the learning-log workflow and required fields. |
| `skill-index.md` | Index of learned skills by topic, task, proof, and related source files. |
| `YYYY-MM-DD-<task-slug>.md` | Per-task learning note written after the task is completed. |

## Candidate Epics

Use these epics as the exhaustive backlog frame:

| Epic | Scope | MVP status |
| --- | --- | --- |
| E01 Ledger Core | Wallets, categories, transactions, transfers, budgets, quick entry, local CRUD performance, audit trail. | MVP |
| E02 Receipt AI | Consent gate, receipt upload/capture, server-side or local extraction, JSON draft, review UI, tax extraction, bulk queue. | MVP |
| E03 Imports and Reconciliation | Money Lover CSV parser, Vietnamese bank mapper, categorization, duplicate detection, reconciliation scoring. | MVP |
| E04 Ledger Assistant | Consent gate, quick prompts, chat contracts, structured chart/table payloads, transaction drafting. | MVP limited |
| E05 Browser Local-First Storage and Sync | SQLite WASM/OPFS, operation log, CRDT/HLC merge, offline edits, manual/browser peer pairing. | MVP |
| E06 Google Drive E2EE Backup | Client-side encryption, Drive upload/download, restore, ciphertext verification. | MVP |
| E07 Privacy and Security | Consent enforcement, data minimization, retention/deletion, app lock, secrets, server boundaries. | MVP |
| E08 Web Platform | Next.js/PWA app shell, offline capability checks, browser support messaging, responsive web UX. | MVP |
| E09 Central Go Backend | Google login, APIs, consent-aware AI endpoints, telemetry/licensing, upload handling, retention controls. | MVP |
| E10 Local AI Benchmarks | Browser-local AI benchmark harness, model/device capability checks, fallback policy. | MVP acceptance gate |
| E11 Mobile Client | Flutter app reusing contracts, mobile capture, quick entry widgets. | Post-MVP |
| E12 Desktop Client | Rust/Tauri client reusing contracts, stronger native local capabilities. | Post-MVP |

Each story candidate should include:

- Source FR/NFR references.
- Labels: `mvp`, `post-mvp`, `poc-gated`, `privacy-sensitive`, `browser-capability`.
- Risk flags from `docs/FEATURE_INTAKE.md`.
- Validation expectation.
- Any browser capability assumptions or fallback behavior.

## MVP Data Flow

1. The web client stores and reads ledger data locally first through
   browser-compatible SQLite.
2. Local changes are written to an operation log or change-set stream.
3. Offline edits must be mergeable with CRDT/HLC conflict handling.
4. Peer sync uses browser-compatible pairing rather than assuming native mDNS.
5. Google Drive backup encrypts locally with WebCrypto before upload.
6. Server AI is consent-first. Receipt images/text, imported statement snippets,
   chat prompts, and ledger context cannot be sent to the Go backend AI flow
   until the user opts in.
7. Google login authenticates users through standard OAuth/OIDC and is separate
   from Google Drive authorization for encrypted backup.
8. AI outputs are drafts or suggestions until the user confirms them.
9. Telemetry uses a strict allowlist and excludes raw financial amounts, OCR
   text, receipt images, imported rows, chat prompts, and generated SQL.

## Error Handling

The product contract should define visible states and fallbacks for:

- AI consent denied.
- AI provider or Go backend unavailable.
- Browser does not support OPFS, WebCrypto, WebGPU, WebRTC, or another required
  capability.
- Local SQLite open/read/write failure.
- Offline merge conflict or duplicate operation uncertainty.
- Peer pairing failure.
- Google Drive OAuth failure, quota failure, upload/download failure, or
  decrypt failure.
- Receipt/import parse failure.
- Low-confidence extraction.
- Unsupported CSV or Excel format.
- Duplicate detection uncertainty.
- Upload limits.
- Auth/session failure.
- Google login callback, token validation, account linking, logout, or session
  expiry failure.
- Retention/deletion request.

Ledger basics must remain usable without AI consent. Where a browser capability
is missing, the UI should either fall back to a supported mode or clearly mark
the feature unavailable on that device/browser.

## Validation Shape

The MVP validation matrix should distinguish product proof, privacy proof, and
browser capability proof.

Expected unit proof:

- Money parsing.
- Wallet/category/transaction/transfer rules.
- Budget thresholds.
- Money Lover CSV parsing, including quoted decimal-comma examples from the
  provided sample.
- Bank import column mapping.
- Reconciliation scoring.
- Operation log and CRDT merge behavior.
- Consent gate enforcement.
- Google login claim/session mapping.
- Telemetry allowlist filtering.
- Encryption/decryption helpers.

Expected integration proof:

- Browser SQLite persistence with selected storage backend.
- Offline edit and reload recovery.
- Peer pairing/sync flow under the selected browser-compatible mechanism.
- Google Drive OAuth and encrypted backup with plaintext exclusion.
- Go backend API contracts.
- Google OAuth/OIDC login and session handling.
- AI provider mocks and consent-aware request handling.
- Upload limits and retention/deletion flows.

Expected E2E proof:

- Add/edit/delete transaction.
- Transfer excluded from reports.
- Budget warning behavior.
- Import the Money Lover sample file.
- Receipt-to-draft with consent.
- Denied-consent fallback.
- Assistant quick prompt with consent.
- Telemetry exclusion of sensitive data.
- Offline edits merged between two browser contexts or devices.
- Google Drive encrypted backup and restore.
- Google login, logout, and session expiry.

Expected benchmark/proof reports:

- Browser local SQLite read/write latency.
- CRDT/HLC merge correctness.
- LAN/manual peer pairing latency and reliability.
- Google Drive E2EE ciphertext verification.
- Browser-local AI model capability, memory, latency, and fallback matrix.

Expected academic learning proof after each completed task:

- A task learning note exists under `docs/learning/`.
- The note names the practical skills used, for example PWA, responsive web app
  for mobile browsers, SQLite WASM/OPFS, CRDT, WebCrypto, Google Drive API,
  Go backend API design, consent-first AI, or benchmark design.
- The note explains what was learned, what was difficult, what tradeoffs were
  made, what commands or tests proved the work, and what future task should
  reuse the lesson.
- `docs/learning/skill-index.md` links the skill to the task note and affected
  project files.

## Decisions To Record

Create decision records for:

1. Web-only browser MVP with Next.js/PWA.
2. Central Go backend with explicit consent for server-side AI.
3. Google login is part of MVP account access.
4. Google login authorization is separate from Google Drive backup
   authorization.
5. No local Go daemon in MVP.
6. Browser-native local-first features are MVP requirements.
7. LAN discovery is defined as browser-compatible peer pairing, not guaranteed
   automatic mDNS.
8. Client-side encrypted Google Drive backup must keep plaintext away from the
   Go backend.
9. Mobile, desktop, and stronger native local AI are post-MVP phases.
10. PocketNode tasks must produce academic learning notes after completion.

## Academic Learning Log Workflow

Because PocketNode is an academic project, the done definition for every future
task should include a learning note. The note should be written after
implementation and validation, when the actual lesson is known.

Each learning note should include:

- Task summary.
- Skills practiced.
- New concepts learned.
- Implementation details that made the skill concrete.
- Mistakes, limitations, or tradeoffs.
- Validation evidence.
- Reusable guidance for future PocketNode tasks.

Examples of skills to track include:

- WASM and browser-native PWA architecture.
- Responsive web app behavior for mobile browsers.
- SQLite in the browser, including WASM, OPFS, and fallback storage.
- CRDT and HLC merge behavior.
- Browser peer pairing and LAN-adjacent sync constraints.
- WebCrypto and Google Drive E2EE backup.
- Go backend API design.
- Consent-first AI request handling.
- Local AI benchmarking in WebGPU/WASM environments.
- Privacy-preserving telemetry.

## Open Risks

- Browser support for SQLite WASM/OPFS varies by platform and browser.
- Browser-only peer discovery cannot match native mDNS reliability.
- Browser-local AI may not meet latency or memory thresholds on many devices.
- A central AI backend weakens the original zero-knowledge claim unless consent,
  minimization, retention, and deletion rules are enforced and tested.
- Exhaustive mapping will create many candidate stories; only selected slices
  should become detailed story packets during implementation planning.

## Harness Delta

The next planning step should create the product docs, epic/story candidate
index, learning-log structure, validation matrix rows, and decision records
from this design. It should not implement application code yet unless the user
explicitly selects a first implementation slice after reviewing the written
spec.
