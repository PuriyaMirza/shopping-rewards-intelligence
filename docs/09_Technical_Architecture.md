# Technical Architecture

## Goal

Implement the product with the least architecture necessary to validate behavior, while preserving a clean path to tool-backed and multi-agent execution.

## Phase 1 — Custom GPT or single assistant

Components:

- One system prompt
- Lightweight user profile
- Web retrieval for current public information
- Manual evaluation suite
- Structured internal reasoning templates

Do not build separate services yet.

## Phase 2 — Modular tool-backed application

Suggested components:

- Orchestrator/router
- Product research module
- Retailer intelligence module
- Rewards retrieval adapters
- Acquisition intelligence module
- Synthesis module
- Structured result schema
- Evaluation harness
- Request and result logging

Potential implementation choices include the OpenAI Agents SDK, a custom orchestration layer, or a workflow tool. The product documents should remain valid regardless of framework.

## Phase 3 — Data and automation

Only after validation:

- Retailer profile store
- Public rewards snapshots
- Historical rate data
- Source freshness metadata
- Alerting and scheduled checks
- User preference persistence
- Browser extension or web interface

## Data-source strategy

### Public comparison sources

Use public aggregators such as Cashback Monitor and Evreward for discovery and comparison, subject to their terms and technical accessibility.

### Authoritative sources

Use official retailer, portal, forwarding-service, and policy pages when a precise claim matters.

### Logged-in offers

Treat targeted or account-specific offers as user-verification items unless a future secure integration is explicitly implemented.

## Security and privacy

- Do not collect portal passwords.
- Do not store payment credentials.
- Minimize personal profile data.
- Separate public offer observations from targeted user offers.
- Keep source and retrieval metadata for dynamic claims.

## Performance strategy

- Route only needed capabilities.
- Retrieve only applicable retailer fields.
- Parallelize independent research after intent classification.
- Cache stable retailer data with freshness rules.
- Do not cache dynamic reward rates without timestamps and expiry.

## Observability

Track:

- Selected route
- Sources queried
- Retrieval failures
- Latency by module
- Reward coverage
- Confidence
- Evaluation scores
- User corrections

## Why not start fully multi-agent

Independent agents add latency, cost, coordination failures, and debugging complexity. Begin modularly inside one assistant and split only where benchmarks show a measurable benefit.
