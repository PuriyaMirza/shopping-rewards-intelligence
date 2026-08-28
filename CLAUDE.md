# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

This is a **design and specification repository**, not a codebase. There is no
application source, build system, dependency manifest, or automated test runner.
Version 1.0 captures the product requirements, decision principles, information
architecture, conversation design, evaluation framework, agent architecture,
routing workflows, technical plan, and prompt drafts for **Shopping Rewards
Intelligence** — a proposed AI shopping advisor.

All content is Markdown. Work here means editing specifications and prompts, and
(in the next phase) running the acceptance suite in `tests/acceptance_tests.md`
manually against an assistant built from `prompts/system_prompt.md`.

## Commands

There is nothing to build, lint, or compile. Useful operations:

```bash
# See the full document set and how pieces relate
cat README.md

# Full context for a new session or collaborator
cat PROJECT_HANDOFF.md

# Run the evaluation: paste each prompt from this file, unchanged between
# scenarios, into the assistant under test; score 1-5 per dimension.
cat tests/acceptance_tests.md
```

Evaluation is manual. A response passes when it averages >= 4.0 across the
applicable dimensions, meets every scenario "Must" item, and has no critical
failure (fabricating dynamic data, ignoring an exact-product constraint,
silently omitting rewards, confusing forwarding with proxy buying, or
recommending an inferior product for rewards).

## Repository structure

- `README.md` — entry point and document map
- `docs/01`–`docs/10` — numbered canonical specs; `02_PRD.md` is the canonical
  product document, the rest are supporting specifications
- `DECISION_PRINCIPLES.md` — the 32-point "product constitution"; evaluate every
  change against it
- `PRODUCT_DECISIONS.md` — decision log (PD-001…PD-010) with alternatives and tradeoffs
- `PROJECT_HANDOFF.md` — complete standalone context
- `prompts/system_prompt.md` — first operational assistant prompt
- `prompts/agent_prompts.md` — modular per-capability prompt drafts
- `tests/acceptance_tests.md` — 10 benchmark scenarios with must-have criteria
- `examples/` — target response patterns (`browse`, `compare`, `optimize`, `international`)
- `research/Competitors.md` — competitive landscape
- `future/` — deferred designs (`api_design`, `automation`, `browser_extension`,
  `database_schema`); Phase 3 material, not current scope
- `CHANGELOG.md`, `Security.md`

## Architecture of the product being designed

Understanding any single spec requires holding these cross-cutting models in mind.

### Layered interaction model (`docs/04`, `PROJECT_HANDOFF.md` §7)

Five layers the user can enter at any point:

1. Immediate answer **plus rewards overlay**
2. Retailer intelligence (positioning, assortment, price, reputation, shipping, returns)
3. Product intelligence (recommend / compare products)
4. Purchase intelligence (seller, portal, promotions, pickup, gift cards, open-box)
5. Acquisition intelligence (direct international shipping, forwarding, proxy buying, customs)

The defining behavior: **whenever retailers are shown, verifiable rewards are
overlaid in Layer 1** — never deferred to a separate "optimization mode" and
never gated behind a "do you want rewards?" question. Progressive disclosure
reduces clutter but must not hide rewards.

### Rewards portals in scope

Chase Shop & Earn, Rakuten, Delta Shopping, United Shopping. Percentage
cashback, point multipliers, and fixed-point bonuses are **distinct reward
types** and must never be flattened into one number. Unlike currencies (points
vs. airline miles) stay separate unless a transparent valuation model is applied.

### Agent architecture and dynamic routing (`docs/07`, `docs/08`)

Six specialist capabilities: (1) Intent & Planning, (2) Product Research,
(3) Retailer Intelligence, (4) Rewards Intelligence, (5) Acquisition
Intelligence, (6) Decision Synthesis. Routing is dynamic — not every request
runs every capability. Typical routes:

- Retailer browse: 1, 3, 4, 6
- Product research: 1, 2, 3, 4, 6
- Exact product: 1, 3, 4, 6 (no product discovery)
- International retailer search: 1, 3, 4, 5, 6
- Full international research: 1, 2, 3, 4, 5, 6

Synthesis is conceptually always last. Product Research and Retailer
Intelligence can run in parallel after intent classification; Rewards needs
candidate retailers; Acquisition needs retailer/product context.

### Implementation phasing (`docs/09`, `docs/10`)

- **Phase 1 (current target):** one Custom GPT / single assistant — one system
  prompt, lightweight user profile, web retrieval, manual eval suite. Do **not**
  build separate services or deploy six independent agents yet.
- **Phase 2:** modular tool-backed app — orchestrator/router plus capability
  modules, structured result schema, eval harness, logging. Framework-agnostic.
- **Phase 3:** data and automation — retailer store, rewards snapshots,
  historical rates, alerting, persistence, browser extension / web UI.

Split a capability into its own agent/service only when benchmarks show
measurable value (Decision Principle 31, PD-009).

### Data-source strategy

Public-data-first: public aggregators (Cashback Monitor, Evreward) for baseline
comparison; official retailer/portal/policy pages for precise claims; targeted
logged-in offers are always **user-verification items**, never presented as
universal. No portal credentials, passwords, balances, or transaction history.
Distinguish "no offer found" vs. "not checked" vs. "not publicly verifiable".

### Confidence model

Every dynamic claim (offers, bonuses, prices, inventory, coupons, shipping
terms) is High / Medium / Low confidence and should carry retrieval metadata.
Never fabricate; a partial transparent answer beats a comprehensive fabricated one.

## Working conventions

- `docs/02_PRD.md` is canonical. Supporting specs may evolve independently but
  must not contradict it.
- Check proposed changes against `DECISION_PRINCIPLES.md`. Do not reopen settled
  decisions (product name, rewards in Layer 1, product quality over rewards,
  multidimensional retailer comparison, public-data-first, dynamic routing,
  implementation-agnostic requirements) without recording rationale in
  `PRODUCT_DECISIONS.md` and `CHANGELOG.md`.
- Keep requirements implementation-agnostic — valid whether the product ends up
  a Custom GPT, web app, browser extension, or multi-agent system.
