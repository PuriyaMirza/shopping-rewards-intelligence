# Product Requirements Document

**Product:** Shopping Rewards Intelligence  
**Version:** 1.0  
**Status:** Approved for MVP implementation

## 1. Objective

Build an AI shopping assistant that unifies product research, retailer discovery, retailer comparison, rewards overlays, purchase optimization, and international acquisition support.

## 2. User value proposition

The user receives a high-quality shopping recommendation and a rewards-aware purchase path in one interaction. Rewards are not a separate mode; they are a persistent annotation on retailer recommendations.

## 3. Scope

### MVP must support

- Category-level retailer discovery
- Product recommendations and comparisons
- Exact-product purchase optimization
- Retailer comparison across assortment, positioning, reputation, price, shipping, returns, and rewards
- Rewards overlays for Chase Shop & Earn, Rakuten, Delta Shopping, and United Shopping
- Fixed-point bonus offers when publicly visible
- New-customer and newsletter offers when relevant
- International direct shipping, freight forwarding, and proxy-purchase guidance
- Confidence and verification disclosures
- Public-data-first operation without account credentials

### Conditional capabilities

- Coupons and stacking considerations
- Statement offers, when supplied by the user or publicly documented
- Gift-card strategies
- In-store pickup
- Refurbished and open-box inventory
- Membership pricing

### Out of scope for MVP

- Automatic checkout or purchasing on the user's behalf
- Storing financial credentials or portal passwords
- Continuous background monitoring
- Large-scale coupon clipping
- Guaranteed price or inventory accuracy
- Predicting future sales without evidence
- Deep browser automation
- Full historical price or reward-rate databases
- Loyalty programs outside the initial four portals as a core feature

## 4. User inputs

### Required

- A natural-language shopping request

### Optional

- Budget
- Intended use
- Exact product or model
- Delivery country
- Timing
- Size, compatibility, or technical constraints
- Preferred reward currency
- Retailer or brand preferences

The assistant should use low-risk assumptions instead of blocking on optional inputs.

## 5. Decision hierarchy

1. Explicit user constraints
2. Product suitability and quality
3. Retailer credibility and authorized-seller status
4. Total economic value
5. Rewards earned
6. Delivery feasibility and convenience
7. Secondary promotions

## 6. Core functional requirements

### FR-1: Intent classification

Classify requests as browse, product research, retailer comparison, exact-product optimization, international acquisition, timing, or hybrid.

### FR-2: Retailer landscape

Return a curated set of relevant retailers organized by useful dimensions such as specialty, price tier, retailer type, or style.

### FR-3: Rewards overlay

Whenever retailers are recommended or compared, attempt to show relevant Chase, Rakuten, Delta, and United offers. Do not silently omit rewards; state when rates could not be verified.

### FR-4: Retailer comparison

Compare more than rewards. Include the fields that affect the decision, such as assortment, price, product quality positioning, shipping, returns, reputation, authorized status, and international delivery.

### FR-5: Product intelligence

When requested, produce a defensible product shortlist with suitability rationale and tradeoffs.

### FR-6: Purchase optimization

For an exact item, preserve the user's choice and identify credible sellers, current rewards, promotions, delivery, and final verification steps.

### FR-7: Acquisition intelligence

When a product is difficult to obtain, distinguish direct international shipping, package forwarding, and proxy purchasing. Explain cost categories, customs, returns, warranties, and compatibility risks.

### FR-8: Confidence

Label dynamic findings as high, medium, or low confidence based on verification quality and recency.

### FR-9: Progressive disclosure

Lead with an immediately useful answer and rewards overlay. Add deeper retailer, product, checkout, or acquisition detail only as needed.

## 7. Non-functional requirements

- Modular and implementation-agnostic product design
- Selective retrieval of only relevant retailer fields
- Graceful degradation when one data source fails
- Traceable source use for dynamic information
- No unsupported currency equivalency calculations
- Consistent user-facing voice across specialist workflows

## 8. Success metrics

Initial MVP metrics are evaluation-based rather than commercial:

- Retailer relevance
- Product fit
- Rewards coverage
- Retailer-comparison completeness
- Tradeoff clarity
- Transparency
- Actionability
- Discovery value
- Clarification efficiency
- Hallucination rate

## 9. MVP acceptance threshold

A benchmark response should average at least 4.0/5 across the evaluation dimensions, contain no fabricated dynamic facts, and satisfy all critical scenario-specific requirements.
