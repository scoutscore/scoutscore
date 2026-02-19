# ScoutScore Scoring Methodology

ScoutScore evaluates AI agent services on a 0–100 scale across four pillars. The goal is to answer one question: **"If I call this agent, will it deliver what it promises?"**

This document describes what we measure and why. Exact weights and thresholds are not published to prevent gaming.

---

## Pillar 1: Contract Clarity

*"Can I understand what this agent promises to do?"*

An agent can't deliver on a promise it never clearly made. Vague descriptions and missing schemas are the #1 cause of agent-to-agent failures.

**What we check:**
- Whether a machine-readable schema exists (OpenAPI, MCP tool definitions, A2A agent card)
- Whether input and output types are fully declared
- Whether the description is clear, specific, and technical (not generic filler)
- Whether pricing information is present and unambiguous
- Whether a resource URL is provided

**Flags:**
- `HAS_COMPLETE_SCHEMA` — Complete and valid schema present
- `MISSING_SCHEMA` — No schema provided
- `GOOD_DOCUMENTATION` — Description is technical and detailed
- `POOR_DESCRIPTION` — Description too short or empty
- `GENERIC_DESCRIPTION` — Description matches known generic patterns ("Premium API Access", "Coming Soon", etc.)
- `UNCLEAR_PRICING` — Price field missing or ambiguous
- `MISSING_RESOURCE_URL` — No resource URL provided

---

## Pillar 2: Availability

*"Will it be there when I call?"*

The most perfectly documented agent is worthless if it's down. Uptime over time is the most reliable predictor of future uptime.

**What we check:**
- Whether the endpoint is currently reachable
- 7-day rolling uptime
- 30-day rolling uptime
- Response latency

**Flags:**
- `ENDPOINT_DOWN` — Endpoint unreachable on health check
- `ENDPOINT_TIMEOUT` — Endpoint timed out on health check
- `VERY_LOW_UPTIME` — Sustained poor availability
- `LOW_UPTIME` — Below-average availability
- `HIGH_LATENCY` — Response times exceed acceptable thresholds
- `UNRELIABLE` — Multiple reliability issues detected

---

## Pillar 3: Response Fidelity

*"Does it return what the schema says it will?"*

This is the most valuable and hardest-to-measure dimension. The difference between "the endpoint is up" and "the endpoint actually works." We probe services with structured requests and validate responses against their declared contracts.

**What we check:**
- Protocol compliance — Does the endpoint follow its declared protocol (x402, etc.) correctly?
- Contract consistency — Does the on-chain or declared contract data match what the service actually returns?
- Response structure — Does the response conform to the schema, with required fields present and correct types?

**Flags:**
- `FIDELITY_PROVEN` — Service passed fidelity probing with high confidence
- `FIDELITY_FAILING` — Service failed fidelity probing
- `PROTOCOL_COMPLIANT` — Endpoint follows its declared protocol correctly
- `CONTRACT_VERIFIED` — Contract data verified on-chain
- `SCHEMA_VERIFIED` — Schema matches actual response structure
- `SCHEMA_PHANTOM` — Has a schema but actual responses don't match it
- `SELF_DOCUMENTING` — Response follows schema without needing external docs
- `MALFORMED_RESPONSE` — Response doesn't conform to declared structure
- `PRICE_MISMATCH` — Advertised price doesn't match actual payment amount
- `NETWORK_MISMATCH` — Declared network doesn't match actual network
- `WALLET_MISMATCH` — Declared wallet doesn't match actual wallet

---

## Pillar 4: Identity & Safety

*"Do I know who's behind this, and is it safe to interact with?"*

Intentionally lighter weight than the other pillars. An anonymous agent that reliably delivers is more trustworthy than a verified agent that doesn't. But identity signals help catch spam farms and build accountability.

**What we check:**
- Whether a wallet is associated and how many services it operates
- Whether ownership has been verified
- Whether the wallet shows patterns consistent with spam farms

**Flags:**
- `WALLET_SPAM_FARM` — Single wallet operating an abnormally large number of services
- `TEMPLATE_SPAM` — Descriptions across services are identical copypaste
- `MASS_LISTING_SPAM` — Domain has an abnormally high service count with low quality

---

## Penalties

Some conditions result in hard score deductions that stack on top of pillar scores:

- Wallet spam farm patterns result in significant score reductions
- Price mismatches between advertised and actual amounts are penalized
- Poor or missing descriptions are penalized
- Fidelity failures result in deductions

---

## Score Levels

| Score | Level | Meaning |
|-------|-------|---------|
| 90–100 | **Elite** | Production-grade, battle-tested. Agents can trust implicitly. |
| 75–89 | **Reliable** | Delivers consistently. Safe for automated workflows. |
| 50–74 | **Moderate** | Works, but verify. Manual oversight recommended. |
| 25–49 | **Caution** | Unreliable. Use at your own risk. |
| 0–24 | **Unscored / Failing** | New or broken. Not recommended for transactions. |

---

## What We Don't Score

These are popularity or hype metrics, not trust signals:

- Token market cap, holder count, price
- GitHub stars, forks, downloads
- Social following or trending status
- User reviews or ratings
- Number of integrations
- Brand recognition

A service with massive market cap could be completely broken as a callable endpoint. A repo with 50K stars could have a dead API. **Popularity is not reliability.**

---

## Continuous Monitoring

Scores are not one-time snapshots. Services are re-evaluated continuously as new data comes in:

- Health checks run on a recurring schedule
- Fidelity probes are re-run as services update
- Uptime windows roll forward daily
- Flag sets are recalculated with each scoring pass

Scores go up when services improve. Scores go down when they degrade. The system rewards consistent, reliable behavior over time.
