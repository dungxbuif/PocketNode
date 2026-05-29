# PocketNode Product Specification

Version: 0.1.0
Updated: 2026-05-29
Status: Draft aligned after brainstorming

## 1. Purpose

PocketNode is a personal finance hub for people who want strong control over
their financial data while still using AI to speed up receipt capture, import
cleanup, reconciliation, and financial analysis.

This repository is also an academic learning project. Product work must produce
working software and learning records that explain the practical skills learned
during each task.

## 2. Current Product Direction

The MVP is a browser-only web product.

MVP commitments:

- Next.js/PWA web client.
- Go backend API.
- Google login for user accounts.
- Browser-local ledger storage using browser-compatible SQLite.
- Offline-capable local changes and CRDT/HLC merge behavior.
- Browser-compatible peer pairing or LAN-adjacent sync.
- Google Drive end-to-end encrypted backup using client-side encryption.
- Consent-first server-side AI through the Go backend.
- Browser-local AI benchmarks as MVP acceptance evidence.
- No mobile app in MVP.
- No desktop app in MVP.
- No local Go daemon in MVP.

Post-MVP direction:

- Flutter mobile client.
- Rust/Tauri desktop client.
- Stronger native local/offline AI.
- More reliable native LAN discovery if browser constraints block the desired
  sync experience.

## 3. Product Principles

### Local-first by default

The ledger should work locally in the browser before depending on cloud services.
Network failures must not block basic ledger usage.

### Consent-first AI

Receipt images, OCR text, imported statement snippets, chat prompts, ledger
context, or other sensitive financial data must not be sent to server-side AI
until the user explicitly opts in.

### User-reviewed automation

AI and import systems create drafts, matches, suggestions, or visualizations.
They do not silently create final financial records without user confirmation.

### Privacy-aware cloud services

The Go backend may support accounts, APIs, telemetry, licensing, and
consent-aware AI processing. It must minimize retained sensitive data and must
not receive plaintext Google Drive backup data.

### Academic learning record

Every completed task must create or update a learning note under
`docs/learning/` and update `docs/learning/skill-index.md`.

## 4. Actors

- Personal user: manages wallets, transactions, receipts, imports, budgets, and
  assistant questions.
- Household member: may later participate in shared or synchronized finance
  workflows.
- Reviewer/accountant: may later review exports, audit trails, or tax-related
  receipt data.
- PocketNode operator: maintains the Go backend, telemetry allowlists, AI
  provider integrations, and commercial account flows.

## 5. MVP Architecture

```text
-----------------------+         +---------------------------+
| Next.js / PWA Web App | <-----> | Go Backend API            |
|                       |         |                           |
| - Browser SQLite      |         | - Account/API workflows   |
| - Google login UI     |         | - Google OAuth validation |
| - Operation log       |         | - Consent-aware AI        |
| - CRDT/HLC merge      |         | - Telemetry allowlist     |
| - WebCrypto E2EE      |         | - Licensing/commercial    |
| - PWA/offline shell   |         | - Upload/retention rules  |
+----------+------------+         +---------------------------+
           |
           | Client-side encrypted backup only
           v
+-----------------------+
| Google Drive App Data |
| ciphertext only       |
+-----------------------+
```

Browser capability constraints must be explicit in the product. A browser-only
MVP cannot promise native mDNS on every platform. Sync discovery must be defined
as browser-compatible peer pairing through QR code, pairing code, link exchange,
WebRTC, relay-assisted setup, or available browser local-network APIs.

## 6. Functional Requirements

### FR-1 Ledger Core

FR-1.1 Wallets
Users can create and manage multiple wallets.

FR-1.2 Transactions
Users can add, edit, delete, and view income and expense transactions. Categories
support parent-child hierarchy, for example `Food` -> `Groceries` or `Coffee`.

FR-1.3 Transfers
Users can transfer money between their own wallets. The system creates linked
source/destination entries and excludes the transfer pair from income/expense
reports by default.

FR-1.4 Budgets
Users can set weekly or monthly limits by wallet or category. The system warns
at 80% usage and at 100% exceeded.

FR-1.5 Quick Entry
The web MVP should support fast transaction entry optimized for mobile browsers.
Native mobile widgets are post-MVP.

FR-1.6 Audit Trail
Manual add, edit, delete, import, and AI-confirm actions should produce an audit
record with timestamp and changed fields.

### FR-2 Receipt AI

FR-2.1 Receipt Upload/Capture
The web MVP supports receipt image/PDF upload and, where browser APIs allow,
camera capture.

FR-2.2 Consent Gate
The user must explicitly consent before receipt data is sent to server-side AI.

FR-2.3 Receipt Extraction
The AI pipeline returns structured JSON including merchant, transaction date,
total amount, tax amount, currency, and suggested category.

FR-2.4 Review UI
The UI shows the original receipt and extracted draft side by side. The user
must confirm or edit before a transaction is written.

FR-2.5 Tax Extraction
The product should support tax fields relevant to Vietnam VAT and later
GST/HST/PST or other regional tax rules.

FR-2.6 Bulk Processing
The product should support bulk receipt/image/PDF upload. MVP limits may be
smaller than the long-term target of 20 files at once, but the architecture
should support queued processing.

FR-2.7 Local AI Benchmark
The MVP must include browser-local AI benchmark evidence using WASM/WebGPU-capable
models where available. This proof does not replace consent-first server AI.

### FR-3 Imports And Reconciliation

FR-3.1 Vietnamese Bank Imports
Users can import CSV or Excel statements from common Vietnamese banks.

FR-3.2 Dynamic Column Mapping
The import flow detects or lets the user map date, debit amount, credit amount,
description, currency, and account/wallet fields.

FR-3.3 Money Lover Import
The product must support the provided Money Lover CSV shape:
`Nhóm,Số tiền,Đơn vị tiền tệ`.

The parser must correctly handle values such as:

- `Ăn uống,1723000,VND`
- `Tiền chuyển đi,"59245245,00",VND`

FR-3.4 Categorization
The product suggests categories from Vietnamese keywords and aliases, including
unsigned text such as `chuyen khoan`, `tiki`, `shopee`, `grab`, `be`, and
`an sang`.

FR-3.5 Reconciliation
The product matches ledger transactions to bank statement rows using amount,
date tolerance, and description similarity. Duplicate uncertainty must be shown
to the user instead of silently deleting records.

### FR-4 Ledger Assistant

FR-4.1 Consent Gate
The assistant cannot send chat prompts or ledger context to server-side AI until
the user opts in.

FR-4.2 Quick Prompts
The assistant provides starter prompts for monthly spending, top expenses,
category analysis, and largest receipt.

FR-4.3 Transaction Drafting
The assistant can draft a transaction from natural language. The user must
confirm before writing to the ledger.

FR-4.4 Query And Visualization
The assistant returns structured chart/table payloads for the web UI, including
donut, bar, line/area, and grid/table views.

FR-4.5 Text-to-SQL Safety
If Text-to-SQL is used, generated SQL must be constrained to safe read-only
queries unless a separate confirmed write flow exists.

FR-4.6 Voice Input
Voice-to-transaction is post-MVP unless browser support and product priority make
it part of a selected web story.

### FR-5 Browser Local-First Storage And Sync

FR-5.1 Browser SQLite
The web app stores ledger data in browser-compatible SQLite, preferably SQLite
WASM backed by OPFS where supported.

FR-5.2 Fallback Handling
If the browser lacks the selected storage capability, the app must show clear
compatibility messaging or use a documented fallback.

FR-5.3 Operation Log
Local changes are recorded as operations or change sets suitable for merge and
sync.

FR-5.4 CRDT/HLC Merge
Offline changes from two browser contexts or devices must merge deterministically
without losing transactions.

FR-5.5 Peer Pairing
The web MVP supports browser-compatible peer pairing. It must not claim universal
automatic mDNS discovery.

FR-5.6 Sync Proof
MVP acceptance requires proof that two browser profiles/devices can edit offline
and merge changes.

### FR-6 Google Drive E2EE Backup

FR-6.1 Client-Side Encryption
The web app encrypts backup data locally with WebCrypto before upload.

FR-6.2 User-Owned Secret
The encryption key or seed phrase is controlled by the user and is not sent to
the Go backend.

FR-6.3 Google Drive App Data
Encrypted backups are stored in the user's Google Drive App Data area where
possible.

FR-6.4 Restore
Users can download, decrypt locally, and restore a backup.

FR-6.5 Ciphertext Verification
Validation must prove that Google Drive and the Go backend never receive
plaintext backup content for this flow.

### FR-7 Go Backend

FR-7.1 API Contracts
The Go backend provides APIs required by the web MVP.

FR-7.2 Google Login
The web MVP supports login with Google. The Go backend validates Google OAuth
identity tokens or authorization-code exchange results, creates or links the
PocketNode account, and issues the application's own session. Login scope must
be minimal and must be separate from Google Drive backup authorization.

FR-7.3 Consent-Aware AI
Server AI endpoints must reject sensitive AI requests unless consent is present.

FR-7.4 Upload Handling
The backend enforces upload limits, content-type checks, retention rules, and
deletion workflows.

FR-7.5 Telemetry
Telemetry is allowlisted and must exclude raw financial amounts, OCR text,
receipt images, imported rows, chat prompts, generated SQL, and plaintext backup
data.

FR-7.6 Commercial Accounts
The backend may store account, subscription tier, public key, and last activity
metadata for Pro/lifetime workflows.

## 7. Non-Functional Requirements

NFR-1 Privacy And Consent
Sensitive AI flows are opt-in. Cloud processing must be disclosed before use.

NFR-2 Local Responsiveness
Basic ledger actions should feel instant and should not depend on the network.
Target local interaction latency is under 100ms for normal CRUD flows.

NFR-3 Browser Capability Transparency
The product must detect and explain missing browser capabilities for SQLite,
OPFS, WebCrypto, WebGPU, WebRTC, camera capture, and related APIs.

NFR-4 Data Integrity
Sync and merge logic must avoid silent data loss. Conflicts or duplicate
uncertainty must be reviewable.

NFR-5 Security
The product should support app/session lock behavior appropriate for a web PWA.
Secrets must not be logged or sent to telemetry.

NFR-5.1 Authentication Security
Google login must use standard OAuth/OIDC validation, protect sessions against
CSRF and token leakage, and avoid storing Google access tokens unless a later
story explicitly needs them. Google Drive backup authorization must be requested
separately from login.

NFR-6 Observability
Anonymous operational telemetry and crash reporting may be used only through a
strict metadata allowlist.

NFR-7 Learning Evidence
Each completed task must include a learning note and skill-index update.

## 8. Validation And Acceptance

MVP validation must include:

- Unit tests for money parsing, ledger rules, transfer exclusion, budgets,
  import parsing, reconciliation scoring, consent gates, telemetry filtering,
  Google login claim/session mapping, encryption helpers, and CRDT/HLC merge
  logic.
- Integration tests for browser SQLite persistence, offline reload recovery,
  Go API contracts, Google OAuth/OIDC callback or token verification, AI
  provider mocks, upload limits, retention/deletion flows, Google Drive
  encrypted backup, and peer pairing/sync.
- E2E tests for transaction CRUD, Money Lover sample import, receipt-to-draft
  with consent, denied-consent fallback, Google login, logout/session expiry,
  assistant quick prompt, telemetry exclusion, offline merge, and encrypted
  backup/restore.
- Benchmark reports for browser SQLite read/write latency, CRDT/HLC correctness,
  peer pairing reliability, E2EE ciphertext verification, and browser-local AI
  latency/memory/capability.
- Learning notes under `docs/learning/` for completed tasks.

## 9. Roadmap

### MVP

- Browser-only Next.js/PWA client.
- Go backend API.
- Google login.
- Ledger core.
- Browser SQLite local storage.
- Operation log and CRDT/HLC sync proof.
- Browser-compatible peer pairing.
- Google Drive E2EE backup.
- Consent-first receipt AI and assistant.
- Money Lover import and Vietnamese bank import foundation.
- Telemetry allowlist.
- Browser-local AI benchmark proof.
- Academic learning-log workflow.

### Post-MVP

- Flutter mobile app.
- Rust/Tauri desktop app.
- Native mobile widgets.
- Native desktop local capabilities.
- Stronger local/offline AI.
- More reliable native LAN discovery.
- Expanded tax jurisdictions.
- Expanded bank import coverage.

## 10. Open Risks

- Browser support for SQLite WASM and OPFS varies.
- Browser-only peer pairing may not match native LAN discovery expectations.
- Browser-local AI may not meet performance targets on many user devices.
- Server-side AI weakens the original zero-knowledge ambition unless consent,
  minimization, retention, deletion, and audit rules are enforced.
- Google Drive OAuth and browser storage behavior may vary across browsers and
  privacy modes.
- Google login and Google Drive backup use different Google authorization
  scopes and must not be coupled accidentally.

## 11. Source Notes

This document replaces the earlier theoretical draft that centered on Flutter,
Tauri, a local Go daemon, and post-hoc cloud telemetry. Those ideas remain
available as post-MVP or research directions, but they are not the MVP shape
approved during brainstorming on 2026-05-29.
