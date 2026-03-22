---
id: 070e46d0-770a-4001-bedc-761a4211e6c8
type: initiative
status: draft
priority: high
strategy: Product Architecture
completionPercentage: 5
---

# US Compliance & Certification Readiness

## Description
Achieve SOC 2 Type I certification for US enterprise market entry. Current readiness assessed at ~45% — authentication, RBAC, RLS, and validation are solid. Critical gaps: no MFA, no audit logging, no rate limiting, CI doesn't run tests, no change management controls, no dependency scanning. Phased plan: Phase 1 (security foundations, ~42hrs), Phase 2 (hardening, ~40hrs), Phase 3 (documentation, ~30hrs), Phase 4 (audit engagement). Estimated 3-4 months to Type I, $30-65K + engineering time.

## Parent Strategy
[Product Architecture](../strategy/product/product-architecture.md)

## Status & Progress
- **Status**: draft
- **Priority**: high
- **Completion**: 5%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: Not set
- **Target Date**: Not set

## Content
# US Compliance & Certification Readiness

## Why This Matters
US enterprise and mid-market buyers require compliance certifications before signing. SOC 2 is table stakes for B2B SaaS; ISO 27001 strengthens global credibility. Without these, Stratafy is locked out of serious enterprise deals and certain investor expectations.

## Current State (Assessed 2026-03-15)

**Overall SOC 2 Type I Readiness: ~45%**

### What's Already Solid
- **Authentication**: Supabase JWT + middleware enforcement on all non-public routes
- **RBAC**: Role hierarchy (owner/admin/editor), workspace-scoped permissions
- **Data Isolation**: RLS policies on most tables, workspace_id scoping throughout
- **Input Validation**: Zod schemas + Effect-based validation across API endpoints
- **SQL Injection Prevention**: Supabase client with parameterized queries — no raw SQL
- **Secrets Management**: `.env` excluded from git, `.env.example` documented
- **Encryption in Transit**: HTTPS enforced, secure cookies with PKCE
- **Soft Deletes**: 294 `deleted_at` instances across migrations
- **Database Migrations**: 80+ versioned migrations in `supabase/migrations/`
- **Test Infrastructure**: Vitest with 4 workspaces, 80% coverage thresholds, 84 test files, 2,182 tests
- **Infrastructure as Code**: Vercel config, cron jobs, migration-based DB management

---

## Phase 1: Security Foundations — Engineering Work (Weeks 1-2)

### 1.1 CI/CD Pipeline ✅ IN PROGRESS
- **Gap**: CI targeted dead `v3` branch and never ran; no test execution in pipeline
- **Action**: Retarget CI to `main`, add unit tests to pipeline
- **Status**: ✅ CI now targets `main` with lint + typecheck + unit tests (commit 6c92e2d3)
- **Remaining**: Fix 7 pre-existing lint errors surfaced by CI (3x `no-restricted-globals` in InsightSync, 3x `no-console` in entity-embedding-service, 1x `no-dupe-keys` in eslint config). CI is red until these are resolved.
- **Note**: Vercel deploys independently on push to `main` — CI is a safety net, not a gate. PR-based gating to be added when team grows.
- **Effort**: ~4 hours (2 hours done, ~2 hours remaining for lint fixes)

### 1.2 Multi-Factor Authentication (CRITICAL)
- **Gap**: No MFA/2FA implementation anywhere in codebase
- **Action**: Enable Supabase MFA (TOTP) — they support it natively
- **Scope**: Admin accounts mandatory, all users recommended
- **Effort**: ~8 hours

### 1.3 Rate Limiting (CRITICAL)
- **Gap**: No rate limiting middleware on any endpoint, no DDoS protection
- **Action**: Add rate limiting middleware (per-user + per-IP), return 429 with Retry-After headers
- **Effort**: ~8 hours

### 1.4 Audit Event Logging (CRITICAL)
- **Gap**: No logging of login attempts, permission violations, admin actions, or data access. `server/middleware/error-logger.ts` exists but is disabled
- **Action**: Enable error-logger middleware; implement structured audit event logging for auth events, CRUD operations, and admin actions
- **Effort**: ~16 hours

### 1.5 Change Management Controls (CRITICAL)
- **Gap**: No CODEOWNERS, no required PR reviewers, no branch protection, no PR template
- **Action**: Create CODEOWNERS file, enable branch protection rules, add PR template
- **Note**: Solo developer currently — full PR workflow deferred until team grows. CODEOWNERS and branch protection can be added now for audit trail.
- **Effort**: ~4 hours

### 1.6 Dependency Vulnerability Scanning (CRITICAL)
- **Gap**: No Dependabot or Renovate config, no automated security advisory alerts
- **Action**: Add `.github/dependabot.yml` for npm + GitHub Actions
- **Effort**: ~2 hours

**Phase 1 Total: ~42 hours**

---

## Phase 2: High-Priority Gaps (Weeks 3-4)

### 2.1 Missing Audit Columns
- **Gap**: Finance tables (`fin_accounts`, `fin_strategy_mappings`), org tables (`org_proposals`, `org_positions`), `workspace_snapshots`, and `context_suggestions` missing `created_by`/`updated_by` fields
- **Action**: Database migration to add audit columns; `workspace_snapshots.created_by` FK references `auth.users(id)` instead of canonical `ws_users(id)`
- **Effort**: ~8 hours

### 2.2 Error Monitoring Integration
- **Gap**: No Sentry, Datadog, or similar error tracking service
- **Action**: Integrate Sentry for error tracking and alerting
- **Effort**: ~8 hours

### 2.3 Security Headers
- **Gap**: No Content-Security-Policy headers, no explicit CSRF token implementation
- **Action**: Add CSP headers in nuxt.config or middleware; add CSRF middleware for mutations
- **Effort**: ~8 hours

### 2.4 Password Policy Documentation
- **Gap**: Password management delegated to Supabase but no documented policy (min length, complexity, expiration, history)
- **Action**: Configure and document password requirements in Supabase; add account lockout after failed attempts
- **Effort**: ~4 hours

### 2.5 Session Management Hardening
- **Gap**: No inactivity timeout enforcement, no concurrent session limits, no session binding
- **Action**: Configure JWT expiry policy; document session timeout; add session management
- **Effort**: ~8 hours

### 2.6 Health & Readiness Endpoints
- **Gap**: Only integration layer has health endpoint — no root `/health` or `/ready`
- **Action**: Create root health endpoint checking DB, cache, external services
- **Effort**: ~4 hours

**Phase 2 Total: ~40 hours**

---

## Phase 3: Documentation & Process (Weeks 5-8)

### 3.1 Access Control Matrix
- Document what each role can do across all resources
- Map permission boundaries (workspace vs system scope)

### 3.2 Incident Response Plan
- Define severity levels, escalation paths, communication templates
- Assign incident response roles

### 3.3 Backup & Recovery Documentation
- Document RTO/RPO targets
- Create recovery runbook
- Schedule monthly backup restoration tests
- Verify Supabase backup geo-redundancy

### 3.4 Rollback Procedures
- Document deployment rollback process
- Document database migration rollback process
- Define rollback RTO targets

### 3.5 Environment Promotion Process
- Document dev → staging → prod promotion workflow
- Add startup configuration validation script

### 3.6 Vendor Risk Management
- Document all third-party services (Supabase, Vercel, Anthropic, Voyage AI, etc.)
- Assess each vendor's SOC 2 status
- Define vendor review cadence

### 3.7 Data Retention & Deletion Policy
- Document retention periods for each data type
- Document deletion procedures for user data requests
- Verify soft delete coverage across all entities

**Phase 3 Total: ~30 hours (primarily documentation)**

---

## Phase 4: SOC 2 Type I Audit

### 4.1 Engage Auditor
- Select AICPA-accredited auditor
- Budget: $15,000-$30,000 for Type I

### 4.2 Readiness Assessment
- Map controls to Trust Service Criteria (Security, Availability, Confidentiality)
- Complete readiness assessment with auditor

### 4.3 Compliance Tooling (Optional)
- Evaluate Vanta, Drata, or Secureframe for continuous evidence collection
- Budget: $10,000-$25,000/year

### 4.4 Achieve Type I Report
- Point-in-time assessment of control design

---

## Phase 5: SOC 2 Type II (Post-Type I)
- 6-12 month observation period
- Continuous evidence collection
- Achieve Type II report (controls operating effectively over time)

## Phase 6: ISO 27001 (Parallel Track)
- Leverage SOC 2 control overlap (~60-70%)
- Establish ISMS (Information Security Management System)
- Certification audit

## Phase 7: Sector-Specific (As Needed)
- CCPA/CPRA privacy compliance for California user data
- HIPAA BAA readiness if healthcare customers emerge
- FedRAMP evaluation if government pipeline develops

---

## Budget Estimate

| Item | Estimate |
|------|----------|
| Engineering effort (Phases 1-3) | ~112 hours |
| SOC 2 Type I audit fees | $15,000-$30,000 |
| Compliance tooling (annual) | $10,000-$25,000 |
| Error monitoring (Sentry) | $2,400/year |
| Fractional CISO (optional) | $3,000-$5,000/month |
| **Total Phase 1-4** | **$30,000-$65,000 + engineering time** |

## Key Considerations
- Assign a compliance lead or fractional CISO
- Timeline: ~8 weeks engineering + 4-6 weeks audit = **3-4 months to SOC 2 Type I**
- Many Phase 1 items (rate limiting, MFA, CI/CD) are good engineering practice regardless of SOC 2

## Progress Log
- **2026-03-15**: Initial codebase assessment completed (45% readiness)
- **2026-03-15**: CI pipeline fixed — retargeted to `main`, unit tests added (commit 6c92e2d3). 7 pre-existing lint errors surfaced, CI currently red.
