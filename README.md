# ScoutScore

**Trust Infrastructure for AI Agents.** Score any x402 service before your agent pays.

---

## The Problem

AI agents are starting to transact with each other - paying for services, calling APIs, exchanging value. But there's no way to know which agents actually deliver what they promise.

86% of agent services listed on open marketplaces are spam. Fake descriptions, recycled wallets, dead endpoints. When Agent A pays Agent B, there's no credit check, no trust signal, nothing.

## The Solution

ScoutScore scores the delivery reliability of AI agent services on a 0-100 scale. Before your agent pays another agent, it checks the ScoutScore - just like a lender checks a FICO score before approving a loan.

We don't just check if services are online. We send real USDC payments on Base mainnet, validate responses against declared schemas, and track on-chain payment history across $19.6M in USDC volume. The result: a trust score grounded in actual behavior, not self-reported claims.

**North Star:** Does the agent deliver what it promises?

---

## How It Works

Every service is evaluated across **4 weighted pillars**:

| Pillar | Weight | Question |
|--------|--------|----------|
| **Contract Clarity** | 20% | Can I understand what this agent promises to do? |
| **Availability** | 30% | Will it be there when I call? |
| **Response Fidelity** | 30% | Does it return what the schema says it will? |
| **Identity & Safety** | 20% | Do I know who's behind this? |

Trust score = pure weighted average of the four pillars. No hidden bonuses or penalties - every modifier is absorbed into its respective pillar.

On top of pillar scores, we apply **30+ flags** - signals like `WALLET_SPAM_FARM`, `PAID_VERIFIED`, `SCHEMA_PHANTOM`, `PRICE_MISMATCH`, `HAS_ONCHAIN_REVENUE`, and more that give agents and developers immediate context about a service.

Scoring is continuous. Health checks run every 30 minutes, fidelity probes every 6 hours, and paid verification probes validate real payment flows. Scores go up and down based on real behavior, not one-time snapshots.

---

## Paid Fidelity Verification

ScoutScore dogfoods x402 - we send real USDC to services and validate what comes back. This is the hardest dimension to measure and where the deepest moat lies.

```
  2,060  x402 services indexed
    |
    v
    198  domains paid-probed (real USDC on Base mainnet)
    |
    |  85% accepted payment
    v
    169  accepted real USDC
   /   \
  /     \
 60     109
 36%     64%
  |       |
WORK   BROKEN
```

- **V1 + V2 protocol support** - X-PAYMENT header (V1) and PAYMENT-SIGNATURE header (V2)
- **$0.78 total USDC spent** across all verification probes
- New flags: `PAID_VERIFIED`, `PAID_HOLLOW`, `PAID_SETTLED_FAILED`, `PAID_REJECTED`, `PAID_IGNORED`

64% of services that accepted payment returned errors instead of content. Without paid verification, these services look healthy.

---

## Discovery Sources

ScoutScore indexes x402 services from 5 facilitator discovery APIs plus an auto-discovery system:

| Source | Domains | Cadence |
|--------|---------|---------|
| CDP Bazaar (Coinbase) | 505 | Every 4h |
| PayAI Facilitator | 1,099 | Every 4h |
| AnySpend | 5 | Every 6h |
| OpenFacilitator | 20 | Every 6h |
| Dexter | 19 | Every 6h |
| **Facilitator Radar** | auto | Every 6h |

Facilitator Radar automatically discovers new x402 facilitators by scanning x402.org/ecosystem and probing for discovery endpoints. 24+ facilitators tracked.

---

## On-Chain

ScoutScore is registered on-chain via [ERC-8004](https://eips.ethereum.org/EIPS/eip-8004):

- **Agent #1308** on Ethereum Sepolia
- **Agent #26282** on Base mainnet

On-chain payment intelligence feeds directly into scoring:

| Metric | Value |
|--------|-------|
| USDC volume tracked | $19.6M |
| Wallets analyzed | 198 |
| Transactions analyzed | 5.1M+ |
| Unique payers identified | 218,306 |

Data sourced from Dune Analytics. Flags like `HAS_ONCHAIN_REVENUE`, `HIGH_PAYMENT_VOLUME`, and `DIVERSE_PAYER_BASE` are derived from on-chain payment patterns.

---

## Integrate

### SDK

```bash
npm install @scoutscore/sdk
```

```typescript
import { ScoutScore } from '@scoutscore/sdk';

const scout = new ScoutScore();
const result = await scout.scoreBazaarService('example.com');
console.log(result.score, result.level, result.flags);
```

### MCP Server

```bash
npm install @scoutscore/mcp-server
```

5 tools available: `check_trust`, `check_fidelity`, `get_ecosystem_stats`, `search_services`, `scan_skill`. Add to your MCP client config to give any AI agent access to ScoutScore lookups, batch scoring, and fidelity checks.

### ElizaOS Plugin

ScoutScore plugin for ElizaOS submitted as [PR #6513](https://github.com/elizaos/eliza/pull/6513) to elizaos/eliza. Adds trust scoring actions directly to Eliza agents.

### API

REST API with no auth required during launch. Score services, batch score, check fidelity, browse the leaderboard.

[Full API documentation](https://scoutscore.ai/docs)

---

## Current Stats

| | |
|---|---|
| **2,079** | Unique domains scored |
| **20,662** | Endpoints indexed |
| **5** | Facilitator discovery sources + auto-discovery |
| **30+** | Trust and spam flags |
| **4** | Scoring pillars |
| **$19.6M** | On-chain USDC tracked |
| **198** | Domains paid-verified with real USDC |
| **29** | Days of continuous monitoring |

[Browse the leaderboard](https://scoutscore.ai/leaderboard)

---

## Links

- [scoutscore.ai](https://scoutscore.ai)
- [Leaderboard](https://scoutscore.ai/leaderboard)
- [Documentation](https://scoutscore.ai/docs)
- [Blog](https://scoutscore.ai/blog)
- [@scoutscore/sdk on npm](https://www.npmjs.com/package/@scoutscore/sdk)
- [@scoutscore/mcp-server on npm](https://www.npmjs.com/package/@scoutscore/mcp-server)
- [Scoring Methodology](./SCORING-METHODOLOGY.md)
- [Changelog](./CHANGELOG.md)
- [@ScoutScoreAI on Twitter](https://twitter.com/ScoutScoreAI)
