# Shopping Rewards Intelligence

Shopping Rewards Intelligence is an AI shopping advisor that combines product research, retailer intelligence, rewards optimization, and acquisition support.

Its defining behavior is simple: **whenever retailers are discussed, relevant rewards information should be overlaid immediately whenever it can be verified.**

Version 1.0 of this repository captures the canonical product requirements, decision principles, information architecture, conversation design, evaluation framework, modular agent architecture, routing workflows, implementation plan, and a handoff document for future ChatGPT sessions or collaborators.

## Problem

A strong purchase decision often requires separate research across product reviews, retailer websites, shopping portals, coupons, delivery policies, and international forwarding services. The cognitive overhead is high, and rewards are often treated as an afterthought.

Shopping Rewards Intelligence unifies those layers while preserving a clear hierarchy: product suitability and retailer credibility come before rewards.

## Core capabilities

- Discover mainstream and specialty retailers.
- Recommend and compare products when requested.
- Compare retailers, not only reward rates.
- Overlay Chase Shop & Earn, Rakuten, Delta Shopping, and United Shopping opportunities.
- Optimize the purchase path for an exact product.
- Help users acquire products that do not ship directly to the United States.
- State uncertainty and verification requirements rather than fabricating dynamic data.

## MVP user profile

- Primary card: Chase Sapphire Preferred
- Preferred currency: Chase Ultimate Rewards
- Typical Chase earning pace: approximately 5,000 points per month
- Portals in scope: Chase Shop & Earn, Rakuten, Delta Shopping, United Shopping
- Decision priority: product quality first
- Paid retail memberships: none assumed
- Additional opportunities: new-customer offers, newsletter discounts, subscriptions, statement offers, gift-card strategies, in-store pickup, and refurbished/open-box inventory

No account credentials, transaction history, or point balances are required. Public aggregators and public retailer data are the default sources. Logged-in or targeted offers are treated as user-verification items.

## Repository map

- `docs/01_Project_Vision.md` — vision, users, jobs, and principles
- `docs/02_PRD.md` — canonical PRD
- `docs/03_Information_Architecture.md` — domain model and retailer schema
- `docs/04_Conversation_Design.md` — response behavior and progressive disclosure
- `docs/05_Evaluation_Framework.md` — benchmarks and acceptance criteria
- `docs/06_GPT_Specification.md` — implementation-agnostic assistant specification
- `docs/07_Agent_Architecture.md` — specialist capabilities and dynamic routing
- `docs/08_Execution_Workflows.md` — routing rules, dependencies, and stop conditions
- `docs/09_Technical_Architecture.md` — phased technical plan
- `docs/10_Roadmap.md` — validation and implementation sequence
- `DECISION_PRINCIPLES.md` — product constitution
- `PRODUCT_DECISIONS.md` — decision log
- `PROJECT_HANDOFF.md` — complete context for a new ChatGPT window or teammate
- `research/Competitors.md` — initial competitive landscape
- `prompts/system_prompt.md` — first operational prompt draft
- `prompts/agent_prompts.md` — modular capability prompts
- `tests/acceptance_tests.md` — runnable evaluation scenarios
- `examples/` — target response patterns

## Product maturity

1. Product design and evaluation framework.
2. Custom GPT MVP and manual validation.
3. Tool-backed modular application with routing and structured outputs.
4. Production product, potentially including a web app, browser extension, historical reward tracking, and alerts.

## Status

**Version:** 1.0 design repository  
**Implementation status:** ready to begin a Custom GPT MVP  
**Next milestone:** implement the prompt, run the acceptance suite, and record observed failures before adding complexity.
