---
id: 5bef6337-44fd-47b3-8b12-0a09b43da03f
type: insight
source: stratafy_chat
category: technology
impactLevel: medium
confidenceLevel: confirmed
status: processed
actionable: true
lastUpdated: 2026-02-16T13:50:55.827578+00:00
---

# ISR Caching Creates Schema Delivery Risk

## Summary
Vercel ISR can serve stale HTML after deploy, making schema invisible to crawlers. Key SEO pages need prerender:true or post-deploy CDN purge.

## Description
Vercel ISR (stale-while-revalidate) caused stale HTML to be served from edge nodes after deploy, making schema invisible to some validators. Key SEO pages should either use prerender: true or have a post-deploy CDN purge step in CI. This is a technical risk to monitor — schema that exists in code but isn't served to crawlers has zero value.

## Classification
- **Source**: stratafy chat
- **Category**: technology
- **Impact**: medium
- **Confidence**: confirmed
- **Status**: processed
- **Actionable**: Yes
- **Tags**: Vercel, ISR, caching, schema, SEO-risk, CI-CD, technical-debt


