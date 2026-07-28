# Product Decisions

## PD-001 — Rewards are a persistent overlay

**Decision:** Whenever retailers are recommended or compared, attempt to show Chase, Rakuten, Delta, and United rewards immediately.

**Alternatives considered:** A separate rewards mode; rewards only during purchase optimization.

**Rationale:** Rewards intelligence is the product's defining layer and should not require an extra request.

**Tradeoff:** Responses contain slightly more information at the first level.

## PD-002 — Product quality before rewards

**Decision:** Do not recommend an inferior or unsuitable product solely because it earns more points.

**Rationale:** Trust and decision quality are more important than nominal reward maximization.

## PD-003 — Retailer comparison is multidimensional

**Decision:** Compare assortment, quality positioning, price, reputation, shipping, returns, and rewards.

**Rationale:** The best portal rate does not make a retailer the best purchase path.

## PD-004 — Use public data by default

**Decision:** Do not require the user's portal credentials or point balances for MVP utility.

**Rationale:** Public aggregators and official pages provide useful baseline intelligence with much lower privacy and implementation cost.

**Tradeoff:** Targeted logged-in offers require user verification.

## PD-005 — Rich retailer schema with selective retrieval

**Decision:** Preserve optional retailer fields but retrieve only those needed for the request.

**Rationale:** Schema richness does not inherently create execution cost; unnecessary retrieval and processing do.

## PD-006 — Layered conversation with rewards in Layer 1

**Decision:** Use progressive disclosure, but include retailer rewards in the immediate answer.

**Rationale:** Progressive disclosure should prevent overload without hiding the signature capability.

## PD-007 — Acquisition intelligence is first-class

**Decision:** Support direct international shipping, forwarding, and proxy purchasing as a core capability.

**Rationale:** Discovering a product is insufficient when the user cannot practically obtain it.

## PD-008 — Dynamic routing

**Decision:** Invoke only needed specialist capabilities.

**Rationale:** This improves latency, cost, relevance, and maintainability.

## PD-009 — Begin modular, not distributed

**Decision:** Implement one assistant with modular capability instructions before deploying independent agents.

**Rationale:** Avoid premature multi-agent complexity. Split components only when evaluation proves value.

## PD-010 — Preserve a canonical PRD

**Decision:** Maintain one readable PRD with supporting specifications as separate documents.

**Rationale:** Executives and engineers need a concise source of product truth, while deeper documents can evolve independently.
