---
id: d70ffe09-496e-4b30-8ba1-adcfd820823b
type: initiative
status: in_progress
priority: high
strategy: Product Architecture
completionPercentage: 60
---

# Platform Quality & Developer Experience

## Description
Production hardening and developer experience infrastructure — linting, performance optimization, testing enforcement, service architecture, and code quality tooling. The work that makes the MVP demo-ready and the codebase maintainable at velocity. Covers: oxlint custom rules, formatter, Core Web Vitals optimization, test coverage enforcement, service modularity standards.

## Parent Strategy
[Product Architecture](../strategy/product/product-architecture.md)

## Status & Progress
- **Status**: in progress
- **Priority**: high
- **Completion**: 60%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-03-15
- **Target Date**: Not set

## Content
# Platform Quality & Developer Experience

## Status: In Progress — 60% (March 22, 2026)

Major infrastructure quality push completed this week. Linting, formatting, performance, testing, and service architecture all overhauled in a single sprint.

## Recent Progress (Mar 15–22)

### Linting Infrastructure (39 commits)

**ESLint → oxlint Migration** — Replaced ESLint with oxlint as primary linter. All 16 custom ESLint rules ported to oxlint JS plugins. oxlint runs ~50x faster, enabling pre-push enforcement without developer friction.

**Custom Rules (16 total across 3 tiers):**

| Tier | Rules | Purpose |
|---|---|---|
| **Critical** | require-await-supabase, no-fetch-generic, require-effect-provide | Prevent runtime bugs |
| **Quality** | no-service-role-in-api, any-in-service-interface, use-generated-validation | Enforce architecture |
| **Style** | require-uuid-validation, require-workspace-validation, no-hard-delete | Defense-in-depth |

**oxfmt** — Replaced Prettier with oxfmt for code formatting. Faster, consistent with oxlint ecosystem.

**Zero-Violation Baseline** — Resolved all existing violations across the entire codebase to establish a clean baseline. This involved 500+ individual fixes across all layers.

**Stratafy Linting Skill** — Created `/stratafy-linting` skill documenting custom rule development, plugin management, and configuration patterns.

### Performance Optimization (11 commits)

**Core Web Vitals** — Targeted improvements for demo-readiness:
- 38 `ref()` → `shallowRef()` migrations (reduced reactivity overhead)
- Lazy landing components with `@nuxt/fonts` (font optimization)
- Deferred auth initialization on public pages (faster TTFB)
- Lightweight `LandingHeader` on public pages
- `modulePreload` re-enabled, dead CSS removed
- MDC components lazy-loaded (reduced TBT)
- Blur transition deferred until after first navigation
- Static pages prerendered

**Result:** Public pages load significantly faster. Landing page optimized for demo/prospect first impressions.

### Service Architecture (10 commits)

**Monolith Splits:**
- MCP server: 24,893 lines → 26 domain modules
- Integration: workspace-snapshot-service split into focused modules
- AI + Alignment: 3 oversized services split
- Organogram: service impl split into focused files
- Foundation: monolithic service split + validation deduplication
- Strategy: tactics service split
- Markdown export: split into focused modules

**Max Lines Threshold:** Reduced to 1,300 lines per file via lint rule.

### Testing (5 commits)

- 42 test gaps closed across 15 layers
- Pre-push hook enforcing test coverage (blocks push if layer has 0 tests)
- Unit tests added for: agent, AI, alignment, chat, cortex, document, finance, integration, MCP, radar, rhythm, strategy

### Database Hardening (3 commits)

- Timestamp type consistency across all tables
- Missing indexes and foreign keys added
- Audit field standardization
- chat_messages session index for query performance

### Error Handling (3 commits)

- Standardized error handlers across agent, chat, integration APIs
- Effect anti-pattern fixes (FiberFailure violations resolved)

### SEO & Public Site (6 commits)

- `llms.txt` and `llms-full.txt` for LLM discoverability
- `nuxt-gtag` → `@nuxt/scripts` for Google Analytics
- Duplicate h1 fix on blog posts
- 60-char title limit enforcement
- Prerendered static pages

### Key Commits

| Commit | What |
|---|---|
| `2fbafea7` | Replace ESLint with oxlint --type-aware |
| `9d408b5c` | Migrate 16 custom rules to oxlint JS plugins |
| `41785e5d` | Replace Prettier with oxfmt |
| `ab37892e` | Split MCP monolith into 26 modules |
| `290ca96a` | Test coverage enforcement + 42 gaps closed |
| `096488bd` | DB schema consistency pass |
| `6bfb1fea` | 38 ref() → shallowRef() |
| `60212583` | Reduce TBT: lazy MDC, remove dead async, eliminate reflows |
| `b089df64` | llms.txt for LLM discoverability |
| `d492aa89` | Standardize API error handling across 7 layers |

---

## Scope

### In Scope (Ongoing)
- Custom lint rule development and enforcement
- Performance optimization (Core Web Vitals targets: LCP < 2.5s, CLS < 0.1, INP < 200ms)
- Test coverage expansion and enforcement
- Service architecture standards (max file size, module boundaries)
- Public site optimization (SEO, performance, accessibility)
- Database schema quality (indexes, FKs, type consistency)
- Error handling standardization

### Out of Scope
- Feature development (covered by other initiatives)
- CI/CD pipeline (covered by US Compliance initiative when activated)
- Security hardening beyond lint rules (covered by US Compliance)

## What's Done
- [x] ESLint → oxlint migration complete
- [x] 16 custom rules ported to oxlint JS plugins
- [x] oxfmt replacing Prettier
- [x] Zero-violation baseline achieved
- [x] 7 monolithic services split into focused modules
- [x] 42 test gaps closed, pre-push enforcement live
- [x] DB schema consistency pass
- [x] Core Web Vitals optimizations (shallowRef, lazy components, fonts)
- [x] Public page performance (deferred auth, lightweight header)
- [x] llms.txt for LLM discoverability
- [x] Error handling standardized across 3 layers

## What Remains
- [ ] Integration test coverage (beyond unit tests)
- [ ] Performance benchmarking under production load
- [ ] Remaining service splits as files exceed 1,300 lines
- [ ] Additional lint rules as patterns emerge
- [ ] Mobile responsiveness edge cases
- [ ] Lighthouse CI for automated performance regression detection

## Relationship to Other Initiatives
- **MVP Development**: Platform quality is what makes the MVP demo-ready and production-grade
- **MCP Server Optimisation**: Modularization (done here) is prerequisite for permission-scoped tools
- **US Compliance & Certification**: Some overlap on security lint rules and testing — compliance will add CI/CD and formal change management
