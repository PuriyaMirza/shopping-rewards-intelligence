# Execution Workflows and Routing Rules

## Execution philosophy

Start with the minimum work required, deepen only when it materially improves the answer, and stop once the decision is adequately supported.

## Request classification

| Intent | Example | Route |
|---|---|---|
| Browse | Show me towel stores | 1-3-4-6 |
| Product research | Best towels under $100 | 1-2-3-4-6 |
| Retailer comparison | Brooklinen vs The Company Store | 1-3-4-6 |
| Exact-product optimization | Where should I buy this model? | 1-3-4-6 |
| International acquisition | How do I buy this from Japan? | 1-3-4-5-6 |
| Hybrid | Find the best Japanese backpack and import it | 1-2-3-4-5-6 |

## Routing decision tree

```text
Receive request
  -> Parse intent and constraints
  -> Does the user need product selection or comparison?
       yes: run Product Research
  -> Are retailers relevant?
       yes: run Retailer Intelligence
  -> Are candidate retailers known?
       yes: run Rewards Intelligence
  -> Is delivery or acquisition complex?
       yes: run Acquisition Intelligence
  -> Synthesize a unified response
```

## Dependency rules

- Product Research and broad Retailer Intelligence may run in parallel after intent is clear.
- Rewards Intelligence generally requires a retailer list.
- Acquisition Intelligence generally requires a retailer-product or retailer-category context.
- Decision Synthesis waits for all selected capabilities or a defined timeout/failure condition.

## Planning output contract

```yaml
intent: browse_retailers
category: bath_towels
constraints:
  destination: US
  condition: new
required_capabilities:
  - retailer_intelligence
  - rewards_intelligence
response_depth: concise
assumptions:
  - online shopping is acceptable
```

## Specialist finding contract

```yaml
entity:
  type: retailer
  name: Example Retailer
retailer:
  category_relevance: high
  retailer_type: specialty
  price_tier: premium
  strengths:
    - strong assortment
rewards:
  chase: null
  rakuten: 4%
  delta: 2x
  united: null
delivery:
  ships_to_us: true
  complexity: low
confidence:
  level: medium
  reason: public rate should be verified before checkout
sources:
  - source_reference
```

## Rewards rules

- Attempt all four MVP programs whenever retailers are shown.
- Distinguish “no offer found” from “not checked” and “not publicly verifiable.”
- Preserve fixed bonuses and multipliers as different offer types.
- Record exclusions and minimum spend.
- Include retrieval time in a production implementation.
- Do not infer a targeted Chase offer from a public aggregator.

## Stop conditions

Stop when:

- The user's intent is satisfied.
- Enough credible options cover the meaningful retailer landscape.
- Additional research is unlikely to change the recommendation.
- The requested response depth is reached.
- A dynamic fact cannot be verified after reasonable attempts.

Do not continue merely to increase answer length or retailer count.

## Failure handling

- Rewards unavailable: provide retailer advice and explicitly say rates could not be verified.
- Product evidence conflicting: present uncertainty and avoid a false winner.
- International shipping unclear: distinguish confirmed paths from possible paths.
- One specialist fails: degrade gracefully instead of failing the entire answer.
- Source disagreement: surface the disagreement and recommend checkout verification.

## Unified response requirement

The final answer must not resemble concatenated agent reports. It should prioritize the decision, remove repeated evidence, and preserve a consistent response structure.
