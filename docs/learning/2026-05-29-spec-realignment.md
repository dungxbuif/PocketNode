# Product Spec Realignment After Brainstorming

Date: 2026-05-29

## Task Summary

Updated the PocketNode source spec so it matches the approved brainstorming
direction: browser-only PWA MVP, Go backend, browser-native local-first
features, consent-first AI, and academic learning records.

## Skills Practiced

- Product spec realignment.
- Scope control after brainstorming.
- PWA-first architecture documentation.
- Browser capability risk documentation.
- Academic documentation hygiene.

## What Was Learned

A source spec can become misleading after brainstorming if it still describes an
older architecture. The spec must clearly separate approved MVP commitments from
post-MVP ideas so future implementation agents do not build the wrong platform
or assume native capabilities in a browser-only product.

## Implementation Details

The old draft was replaced with an aligned product specification. The new spec
defines the MVP as a Next.js/PWA web app with a Go backend, local browser
SQLite, CRDT/HLC sync proof, browser-compatible peer pairing, Google Drive E2EE,
consent-first server AI, and browser-local AI benchmarks.

## Tradeoffs And Limits

The web-only MVP is ambitious because browser support varies for OPFS, WebGPU,
WebRTC, local persistence, and local AI. The spec avoids promising native mDNS
and instead uses browser-compatible peer pairing.

## Validation Evidence

- Reviewed the approved brainstorming design.
- Rewrote `docs/product/SPEC.md` to remove conflicts with the old local Go
  daemon and mobile/desktop-first direction.
- Ran placeholder scan and `git diff --check`.

## Reusable Guidance

When a brainstorming decision changes scope, update the source spec or clearly
mark it superseded before planning implementation. Future work should not infer
MVP scope from older diagrams or platform lists.
