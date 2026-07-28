# Shopping Rewards Intelligence — Complete Project Handoff

Use this document to bring a new ChatGPT session, product manager, designer, or engineer fully up to speed.

## 1. Project summary

Shopping Rewards Intelligence is a proposed AI shopping advisor that combines product discovery, retailer comparison, shopping-portal rewards, purchase optimization, and international acquisition support.

The project began with the question of whether public data could help identify Chase Shop & Earn opportunities. It expanded after recognizing that the user often begins with a broad shopping need—such as “I want towels”—rather than an exact product. The desired experience is therefore broader than a portal-rate checker.

The assistant should help the user understand a category, identify retailers, evaluate products when needed, compare retailer experiences, overlay rewards, and determine how to complete the purchase. Its distinguishing behavior is that rewards appear naturally and immediately whenever retailers are shown.

## 2. Product name

The approved title is **Shopping Rewards Intelligence**.

## 3. Initial user profile

- Primary card: Chase Sapphire Preferred
- Preferred currency: Chase Ultimate Rewards
- Approximate Chase earning pace: 5,000 points per month
- Shopping portals in scope: Chase Shop & Earn, Rakuten, Delta Shopping, United Shopping
- Decision priority: product quality first
- The user has accounts with many retailers but does not want paid memberships such as Amazon Prime, Walmart+, or Costco assumed
- The assistant should consider new-customer offers, subscriptions, newsletter discounts, statement offers, gift-card strategies, in-store pickup, and refurbished/open-box products
- U.S. delivery is the default

The assistant does not need the user's portal logins, passwords, balances, or transaction history. Public aggregators can provide baseline comparison data. Chase's logged-in portal remains authoritative for targeted offers.

## 4. Product problem

Shopping decisions are fragmented across search engines, retailer pages, editorial reviews, Reddit, portal aggregators, card portals, airline malls, coupon sites, and delivery services. Users must manually reconcile product quality, retailer quality, price, rewards, policies, and shipping.

The product should reduce that cognitive overhead and become the user's starting point for shopping.

## 5. Jobs to be done

1. Browse a category and see a retailer landscape with rewards.
2. Research and compare products.
3. Optimize purchase of an exact product without being redirected into discovery.
4. Compare retailers across assortment, quality, price, policies, reputation, and rewards.
5. Judge whether a current reward rate is good when historical data eventually exists.
6. Acquire difficult or international products, especially Japanese items that may require direct international shipping, forwarding, or proxy purchasing.

## 6. Defining product decisions

### Rewards always appear early

The user explicitly rejected a model where rewards appear only in a later optimization mode. When retailers are displayed at the first discovery level, rewards should be overlaid immediately.

Example:

- Retailer A: 6x Chase
- Retailer B: 2x Chase
- Retailer C: 500-point bonus
- Retailer D: 2 Delta miles per dollar

The product should preserve different offer types rather than flattening them.

### Product quality comes first

Rewards cannot justify an inferior product or unreliable retailer.

### Retailer comparison is broader than rewards

Job 4 must compare retailer assortment, target customer, price, quality positioning, shipping, returns, reputation, and rewards.

### Progressive disclosure remains important

The assistant should not dump all available data. However, rewards are included in the first layer rather than withheld.

### Public-data-first

Public aggregators such as Cashback Monitor and Evreward can be referenced for baseline information. Official portal and retailer pages should be used for authoritative details. Targeted logged-in offers require user verification.

### Rich schemas are acceptable

A retailer can have many possible fields without slowing every request, provided the system retrieves only fields relevant to the current decision. The schema is tiered into core, frequently useful, and expert/conditional fields.

### Acquisition intelligence is first-class

Japanese and other international products may be compelling but difficult to obtain. The product should help determine direct U.S. shipping, package forwarding, or proxy purchase and explain customs, costs, warranties, returns, and compatibility.

### Maintain a solid PRD

Supporting documents do not replace the PRD. The PRD is the canonical readable product document, while information architecture, conversation design, evaluation, agent architecture, and technical architecture are supporting specifications.

### Implementation-agnostic product design

Product requirements should remain useful whether the final product is a Custom GPT, web application, browser extension, SDK agent, or multi-agent system.

## 7. Layered interaction model

### Layer 1 — Immediate answer plus rewards overlay

Show the useful retailer or product answer and rewards together.

### Layer 2 — Retailer intelligence

Explain store positioning, assortment, price, reputation, shipping, and returns.

### Layer 3 — Product intelligence

Recommend or compare products when needed.

### Layer 4 — Purchase intelligence

Optimize seller, portal, promotions, pickup, gift-card strategy, or open-box path.

### Layer 5 — Acquisition intelligence

Handle direct international shipping, forwarding, proxy buying, customs, and related risks.

Users can enter at any level. An exact-product request may jump directly to purchase optimization.

## 8. Information architecture

Key entities:

- Shopping category
- Product
- Brand
- Retailer
- Rewards offer
- Promotion
- Delivery/acquisition path
- User context

Retailer fields are tiered:

Core: name, type, categories, price tier, positioning, reward-source availability.

Frequently useful: shipping, returns, authorized brands, membership pricing, physical stores, typical promotions.

Conditional: gift-card exclusions, coupon stacking, portal exclusions, historical rates, international shipping, warranty, customs, and marketplace risk.

## 9. Conversation rules

- Answer the primary question first.
- Do not ask whether rewards should be included.
- Ask a clarifying question only if the answer would materially alter products, retailers, compatibility, budget, or delivery.
- Make reasonable low-risk assumptions.
- Explain tradeoffs.
- State uncertainty clearly.
- Stop when more research is unlikely to change the decision.

## 10. Confidence model

- High: verified directly from a current authoritative source.
- Medium: supported by credible public sources but should be checked before checkout.
- Low: incomplete, conflicting, or potentially stale.

Dynamic information includes portal offers, fixed bonuses, prices, inventory, coupons, promotions, and current shipping terms. These should be refreshed whenever possible.

## 11. Evaluation framework

Responses are scored 1–5 on:

- Product fit
- Retailer relevance
- Rewards coverage
- Retailer comparison
- Tradeoff clarity
- Conversation quality
- Transparency
- Actionability
- Discovery value
- Acquisition completeness when applicable

A passing benchmark averages at least 4.0, satisfies all scenario-specific must-haves, and has no critical failure.

Critical failures include fabricating dynamic information, ignoring an exact-product constraint, silently omitting rewards, confusing forwarding with proxy buying, or recommending an inferior product solely for rewards.

Important benchmark cases include:

- Bath towel retailer browsing
- Office clothing browsing
- Japanese stationery plus U.S. delivery
- Best towels under a budget
- Brooklinen versus The Company Store
- Exact Sony headphone purchase optimization
- Niche retailers with no verifiable rewards
- Japan-only product acquisition

## 12. Agent architecture

The approved architecture has six specialist capabilities:

1. Intent and Planning
2. Product Research
3. Retailer Intelligence
4. Rewards Intelligence
5. Acquisition Intelligence
6. Decision Synthesis

The system uses dynamic routing. It does not run all agents on every request.

Typical routes:

- Retailer browse: 1, 3, 4, 6
- Product research: 1, 2, 3, 4, 6
- Exact product: 1, 3, 4, 6
- International retailer search: 1, 3, 4, 5, 6
- Full international research: 1, 2, 3, 4, 5, 6

Decision Synthesis is conceptually always last, though it can be lightweight.

The MVP should not deploy six independent agents. Start with one assistant containing modular capability instructions and explicit routing. Split agents only when benchmarks show measurable value.

## 13. Execution rules

Product Research and Retailer Intelligence can often run in parallel after intent classification. Rewards generally require candidate retailers. Acquisition generally requires a retailer or product context. Synthesis waits for selected modules or handles failures gracefully.

The system should distinguish:

- no offer found
- not checked
- not publicly verifiable

The system should preserve percentage cashback, point multipliers, and fixed bonuses as different reward types.

## 14. Out of scope for MVP

- Automatic checkout
- Purchasing for the user
- Credential storage
- Continuous monitoring
- Deep browser automation
- Full price or rewards history
- Guaranteed inventory, stacking, tracking, customs, or delivery outcomes
- Broad support for every portal and loyalty program

## 15. Repository and process

The repository should live at:

`https://github.com/PuriyaMirza/shopping-rewards-intelligence`

The repository is intended to become a public portfolio artifact demonstrating product strategy, AI conversation design, evaluation methodology, modular agent orchestration, and technical planning.

The canonical documents are:

- README
- PRD
- Project Vision
- Information Architecture
- Conversation Design
- Evaluation Framework
- GPT Specification
- Agent Architecture
- Execution Workflows
- Technical Architecture
- Roadmap
- Decision Principles
- Product Decisions
- Competitor Research
- Prompt drafts
- Acceptance tests

## 16. Immediate next steps

1. Upload the Version 1.0 repository files.
2. Create the first Custom GPT using `prompts/system_prompt.md`.
3. Run the acceptance tests without changing the prompt between scenarios.
4. Record failures and user corrections.
5. Revise the prompt and product documents based on evidence.
6. Avoid building independent agents or scraping infrastructure until the prompt-only MVP demonstrates where those investments are necessary.

## 17. Guidance for the next ChatGPT session

Treat this repository as the canonical source of truth. Do not reopen settled decisions casually. Specifically preserve:

- The name Shopping Rewards Intelligence
- Rewards in the first response layer
- Product quality over rewards
- Multidimensional retailer comparison
- Public-data-first architecture
- Acquisition intelligence for international products
- Dynamic routing and minimal agent use
- A canonical PRD plus supporting specifications
- Implementation-agnostic requirements

The next useful work is implementation and evaluation, not additional speculative architecture.
