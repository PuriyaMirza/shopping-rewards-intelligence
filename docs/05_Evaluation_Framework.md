# Evaluation Framework

## Purpose

Evaluate the product with repeatable scenarios instead of relying on whether an answer merely “feels good.”

## Scoring dimensions

Score each response from 1 to 5.

1. Product accuracy and suitability
2. Retailer relevance and credibility
3. Rewards coverage
4. Retailer-comparison completeness
5. Tradeoff explanation
6. Conversation quality and low friction
7. Transparency and confidence handling
8. Actionability
9. Discovery value
10. Acquisition completeness, when applicable

## Critical failures

Any of the following causes a benchmark failure regardless of average score:

- Fabricated reward rate, price, inventory, policy, or source
- Recommending an inferior or unsuitable product solely for rewards
- Ignoring an exact-product constraint
- Presenting an unauthorized or risky seller as equivalent to an authorized seller without warning
- Omitting rewards from a retailer recommendation without explaining that they could not be verified
- Confusing forwarding with proxy purchasing
- Claiming guaranteed customs, delivery, or coupon outcomes

## Acceptance threshold

- Average score of at least 4.0/5
- No critical failures
- All scenario-specific “must” criteria met
- The response can be acted on without a separate round of basic portal research

## Core benchmark categories

### A. Browse

#### A1 — Bath towels

Prompt: “Show me places that sell bath towels.”

Must:

- Curate approximately 8–15 strong retailers
- Organize them meaningfully
- Include rewards at the first level
- Include mainstream and specialty choices
- Avoid prematurely recommending one towel

#### A2 — Office clothing

Prompt: “Show me places that sell stylish office clothing.”

Must:

- Cover multiple price tiers and retailer types
- Include rewards immediately
- Surface at least one less-obvious strong option

#### A3 — Japanese stationery

Prompt: “Show me Japanese stationery stores.”

Must:

- Include specialty retailers rather than defaulting to Amazon
- Include rewards where available
- Identify direct U.S. shipping
- Identify when forwarding or proxy purchasing may be required
- Explain shipping, customs, return, and complexity tradeoffs

### B. Product research

Prompt: “What are the best bath towels under $120?”

Must recommend products appropriate to the budget, explain differences, map to credible retailers, and overlay rewards.

### C. Retailer comparison

Prompt: “Compare Brooklinen and The Company Store.”

Must compare assortment, quality positioning, price, target customer, shipping, returns, reputation, and rewards.

### D. Exact-product optimization

Prompt: “Where should I buy the Sony WH-1000XM6?”

Must preserve the model, find credible retailers, compare rewards, and provide verification steps. It should not run unnecessary product discovery.

### E. International acquisition

Prompt: “Find a Japan-only mechanical pencil and tell me how to get it shipped to the U.S.”

Must distinguish product selection from acquisition path and explain direct shipping, forwarding, or proxy options.

### F. Conversation quality

Evaluate unnecessary questions, assumptions, structure, concision, and whether the answer feels unified rather than assembled.

## Evaluation process

1. Run the same scenario on each prompt or architecture version.
2. Save the response and retrieval timestamp.
3. Score all applicable dimensions.
4. Record critical failures separately.
5. Change one meaningful system variable at a time.
6. Keep regressions visible in a change log.
