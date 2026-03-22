---
id: 9e5915e3-eb4f-49e4-8867-3cbeb0a2d78d
type: initiative
status: draft
priority: low
strategy: Product Architecture
completionPercentage: 0
---

# [FUTURE] Dependency & Sequencing Intelligence

## Description
Dependency mapping between strategies and initiatives. Critical path analysis, cascade impact, and bottleneck detection.

## Parent Strategy
[Product Architecture](../strategy/product/product-architecture.md)

## Status & Progress
- **Status**: draft
- **Priority**: low
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-07-01
- **Target Date**: 2026-09-30

## Content
## Overview

Model explicit dependencies between strategies and initiatives, turning the strategy tree from a hierarchy into a network that answers "what breaks if this slips?" Adds graph-based analysis on top of the existing strategy structure.

## Scope

- **Dependency Mapping**: Initiative A must complete before B can start (blocks/blocked_by edges)
- **Shared Resource Constraints**: Multiple initiatives competing for the same capacity
- **Cascade Impact Analysis**: If X slips by 2 weeks, calculate downstream effects automatically
- **Critical Path Identification**: Which sequence of initiatives determines overall timeline?
- **Bottleneck Detection**: Where are dependencies creating queues?
- Graph model layered on existing strategy tree with dependency edges

## Expected Outcomes

- Reveal the constraint network underneath the organisational hierarchy
- Enable solo founders to instantly see cascade effects when timelines slip
- Provide scaling teams with tools to prevent parallel initiatives from blocking each other
- Support advisory firms with dependency mapping as part of strategy health assessments
- Deliver investor-grade reporting on execution interdependencies
