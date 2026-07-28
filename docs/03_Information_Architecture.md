# Information Architecture

## Purpose

Define what the product knows and how entities relate without forcing every request to load every field.

## Domain model

```text
Shopping category
  -> Brand or product
  -> Retailer
  -> Rewards offers
  -> Promotions
  -> Delivery/acquisition path
  -> User context
```

The product should support both category-first and exact-product-first journeys.

## Shopping categories

Initial broad domains include home, electronics, clothing, travel goods, outdoor, beauty, pets, automotive, office, food, and specialty imports. The taxonomy should remain flexible rather than attempting exhaustive classification in the MVP.

## Retailer schema

A rich schema does not require every field to be loaded. Fields are tiered by retrieval frequency.

### Tier 1 — Core

- Name
- Retailer type
- Relevant categories
- Price tier
- Short positioning summary
- Rewards-source availability

### Tier 2 — Frequently useful

- Shipping policy
- Return policy
- Authorized brands or seller status
- Membership requirements
- Physical store or pickup availability
- Typical promotion patterns
- General reputation

### Tier 3 — Conditional or expert

- Gift-card exclusions
- Coupon stacking rules
- Portal exclusions
- Historical reward behavior
- Warranty caveats
- Marketplace seller risk
- International shipping detail
- Import and customs considerations

Execution efficiency comes from selective retrieval, not permanently deleting useful optional fields.

## Rewards model

Each offer should be represented independently rather than flattened prematurely.

Recommended fields:

- Retailer
- Portal or issuer
- Offer type: multiplier, percentage cashback, fixed bonus, statement credit, or other
- Offer value
- Minimum spend, if any
- Expiration, if known
- Eligibility and exclusions
- Public versus targeted
- Retrieval timestamp
- Confidence
- Verification requirement
- Source reference

Different currencies remain separate unless an explicit, configurable valuation model is applied.

## Product model

- Product name and model
- Category
- Brand
- Intended use
- Key specifications
- Price range
- Strengths and weaknesses
- Suitable user profiles
- Credible or authorized retailers
- Availability confidence

## Acquisition model

- Ships directly to destination
- Countries supported
- Forwarding available
- Proxy purchase required
- Shipping carriers, when relevant
- Estimated complexity
- Cost categories
- Customs or duties risk
- Warranty and return implications
- Regional compatibility

## User context

Store only information that materially improves recommendations:

- Primary card and preferred reward currency
- Portals available to the user
- Country and delivery defaults
- Product-quality priority
- Retailer and brand preferences
- Paid memberships
- Relevant fit or compatibility preferences

Do not require account credentials, balances, or transaction history.
