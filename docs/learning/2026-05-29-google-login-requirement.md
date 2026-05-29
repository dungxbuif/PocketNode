# Google Login Requirement

Date: 2026-05-29

## Task Summary

Added Google login as an MVP account requirement for PocketNode's web app and
Go backend.

## Skills Practiced

- OAuth/OIDC product requirement design.
- Authentication scope separation.
- High-risk auth documentation.
- Privacy-aware account flow documentation.

## What Was Learned

Google login and Google Drive backup both use Google identity infrastructure,
but they are different authorization concerns. Login should request only the
minimal identity scope needed to authenticate the user. Google Drive backup
authorization must stay separate so login does not imply Drive access.

## Implementation Details

The product spec now requires the Go backend to validate Google OAuth/OIDC
identity, create or link the PocketNode account, and issue the app's own
session. The design checkpoint now marks Google login as an MVP backend and
privacy/security requirement.

## Tradeoffs And Limits

This change adds an auth hard gate. Future implementation needs careful session
security, CSRF protection, token leakage prevention, logout/session expiry
behavior, and tests around account linking.

## Validation Evidence

- Updated `docs/product/SPEC.md`.
- Updated the brainstorming design checkpoint.
- Ran placeholder scan and `git diff --check`.

## Reusable Guidance

Keep Google login scopes minimal. Do not reuse login consent for Google Drive
backup. Treat account linking and session handling as high-risk stories.
