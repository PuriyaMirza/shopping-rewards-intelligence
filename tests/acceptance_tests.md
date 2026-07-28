# Acceptance Tests

## Scoring

Score each applicable dimension 1–5:

- Product fit
- Retailer relevance
- Rewards coverage
- Retailer comparison
- Tradeoff clarity
- Conversation quality
- Transparency
- Actionability
- Discovery value
- Acquisition completeness

Passing requires an average of 4.0 or higher, all must-have criteria, and no critical failure.

## Test 1 — Broad browse

**Prompt:** Show me places that sell bath towels.

**Must:**

- Show a curated retailer landscape
- Group options meaningfully
- Overlay rewards immediately
- Include mainstream and specialty retailers
- Avoid selecting one towel without being asked

## Test 2 — Office clothing browse

**Prompt:** Show me stores for stylish office clothing that is not overly formal.

**Must:**

- Cover multiple price tiers
- Include relevant retailer types
- Overlay rewards immediately
- Provide discovery value

## Test 3 — Japanese stationery and delivery

**Prompt:** Show me Japanese stationery stores and help me understand how I can get products shipped to the U.S.

**Must:**

- Include specialist stores
- Include rewards when available
- Identify direct U.S. shipping
- Explain forwarding versus proxy buying
- Note customs, returns, and complexity

## Test 4 — Product research

**Prompt:** Recommend the best bath towels under $120.

**Must:**

- Recommend products within budget
- Explain product differences
- Map products to credible retailers
- Overlay rewards

## Test 5 — Retailer comparison

**Prompt:** Compare Brooklinen and The Company Store.

**Must:**

- Compare assortment, quality positioning, price, target customer, shipping, returns, and rewards
- State who each retailer is best for

## Test 6 — Exact product

**Prompt:** Where should I buy the Sony WH-1000XM6?

**Must:**

- Preserve the exact model
- Avoid unnecessary alternatives
- Compare credible retailers and rewards
- Include checkout verification

## Test 7 — Fixed bonus

**Prompt:** Show me luggage stores with good rewards.

**Must:**

- Preserve fixed-point bonuses as distinct from multipliers
- Include major credible luggage retailers
- Explain that nominal rates across currencies are not directly equivalent

## Test 8 — No verifiable rewards

**Prompt:** Show me niche stores for handmade Japanese kitchen tools.

**Must:**

- Still provide retailer value
- Explicitly state where reward rates could not be verified
- Never fabricate an offer

## Test 9 — International exact product

**Prompt:** I found a Japan-only pen. How do I buy it from the U.S.?

**Must:**

- Ask for a link or exact model only if required
- Explain direct shipping, forwarding, and proxy routes
- Cover return and warranty risk

## Test 10 — Unnecessary agent suppression

**Prompt:** Compare the rewards for Macy's and Bloomingdale's.

**Must:**

- Run retailer and rewards logic
- Avoid deep product research
- Include enough retailer context to explain tradeoffs
