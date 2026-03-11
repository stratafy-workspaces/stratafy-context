---
id: b5c26579-28a8-4cd2-a471-c7bf2a509c3b
type: initiative
status: draft
priority: low
strategy: Product Architecture
completionPercentage: 0
---

# Document Signing & Finalization

## Description
Native document signing infrastructure enabling markdown documents to be finalized, cryptographically hashed, and legally signed within Stratafy. Eliminates need for PDF conversion or external e-signature tools for standard commercial contracts.

## Parent Strategy
[Product Architecture](../strategy/product/product-architecture.md)

## Status & Progress
- **Status**: draft
- **Priority**: low
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: Not set
- **Target Date**: Not set

## Content
## Overview

Enable markdown documents in Stratafy to be locked, signed, and used as legally binding contracts — without converting to PDF or leaving the platform. The markdown itself becomes the legal artifact, with cryptographic hashing and audit trails providing integrity verification.

## Legal Basis

Under the ESIGN Act (2000) and UETA (1999), electronic signatures are format-agnostic. A markdown document rendered in Stratafy satisfies legal requirements as long as four criteria are met:
1. **Intent to sign** — clear, deliberate sign action with confirmation
2. **Consent to do business electronically** — demonstrated by platform usage + explicit checkbox
3. **Association of signature with record** — audit trail linking signer identity, timestamp, content hash
4. **Record retention** — both parties can access and export the signed document

## Technical Scope

### Database
- `finalized_at`, `finalized_by`, `content_hash` fields on documents table
- `document_signatures` table: document_id, user_id, signature_type, content_hash, ip_address, user_agent, signed_at, metadata
- RLS policy blocking content updates on finalized documents

### MCP Tools
- `finalize_document` — compute SHA-256 hash, lock content, record finalization
- `sign_document` — verify integrity, record signature with full audit trail
- `verify_document` — re-hash content and confirm against stored hash

### Frontend
- Lock icon + signed banner on finalized documents
- Edit toggle disabled for finalized docs
- Verify button (re-hash and confirm integrity)
- Sign button for counterparties

### Counterparty Access (Phase 2)
- Tokenized share link for external parties
- Auth-free rendered markdown view with "Review and Sign" flow
- Email notification on signature completion
- Signed copy accessible to both parties

### Optional Enhancements (Phase 3)
- PDF export of signed document with audit trail appended
- Multi-party sequential signing
- Signing reminders and expiration
- Blockchain hash anchoring for independent verification

## Strategic Value

- Advisory firms can draft, sign, and file engagement letters entirely within Stratafy
- Documents remain agent-queryable after signing (unlike PDF)
- Complete lifecycle: creation → review → signing → filing → strategic linking
- Differentiator: no other strategic OS has native signing

## Estimate
- Core infrastructure (DB, hash, RLS, MCP tools): 0.5 days
- Frontend (lock, banner, verify, sign UI): 0.5 days
- Counterparty share-and-sign flow: 2-3 days
- Total: ~1 week
