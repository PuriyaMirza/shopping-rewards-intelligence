# Agent Architecture

## Architectural principle

Use dynamic routing. Only the capabilities required for the current request should run. The user experiences one coherent assistant.

## Agent 1 — Intent and Planning

Always runs conceptually.

Responsibilities:

- Interpret intent
- Extract constraints
- Infer low-risk defaults
- Select capabilities
- Decide whether clarification is necessary
- Define response depth

It should not perform deep product or rewards research.

## Agent 2 — Product Research

Use when the user asks what to buy, compares products, or needs alternatives.

Skip when the user has already chosen an exact product and only wants the best purchase path.

Outputs:

- Product shortlist
- Fit rationale
- Key tradeoffs
- Evidence confidence

## Agent 3 — Retailer Intelligence

Use whenever retailers are relevant.

Responsibilities:

- Build the retailer landscape
- Compare assortment, positioning, price, credibility, policies, and delivery
- Identify authorized or credible sellers
- Surface high-value niche retailers

## Agent 4 — Rewards Intelligence

Normally use whenever retailers appear.

Responsibilities:

- Retrieve Chase, Rakuten, Delta, and United offers
- Identify fixed bonuses and material public promotions
- Record exclusions, confidence, and verification requirements

It must not guess rates or collapse currencies without a valuation model.

## Agent 5 — Acquisition Intelligence

Use when delivery is difficult or international.

Responsibilities:

- Determine direct U.S. shipping
- Distinguish package forwarding and proxy buying
- Assess cost categories, customs, return, warranty, and compatibility risks

## Agent 6 — Decision Synthesis

Always runs last conceptually.

Responsibilities:

- Reconcile product, retailer, price, rewards, and delivery findings
- Apply the decision hierarchy
- Remove duplication
- Present rewards at the first useful level
- Produce one unified answer

## Typical routes

- Browse retailers: 1 -> 3 -> 4 -> 6
- Product research: 1 -> 2 -> 3 -> 4 -> 6
- Exact product: 1 -> 3 -> 4 -> 6
- International retailer search: 1 -> 3 -> 4 -> 5 -> 6
- Full international product research: 1 -> 2 -> 3 -> 4 -> 5 -> 6

## MVP implementation note

These agents do not initially need to be separately deployed. Begin with a single assistant containing modular capability instructions and explicit routing rules. Split into independently executed agents only when evaluation proves that parallelism, isolation, or independent ownership improves outcomes.
