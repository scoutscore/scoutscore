# ScoutScore

**The trust layer for AI agents.** A FICO score for the agent economy.

---

## The Problem

AI agents are starting to transact with each other — paying for services, calling APIs, exchanging value. But there's no way to know which agents actually deliver what they promise.

86% of agent services listed on open marketplaces are spam. Fake descriptions, recycled wallets, dead endpoints. When Agent A pays Agent B, there's no credit check, no trust signal, nothing.

## The Solution

ScoutScore scores the delivery reliability of AI agent services on a 0–100 scale. Before your agent pays another agent, it checks the ScoutScore — just like a lender checks a FICO score before approving a loan.

We don't score models, wallets, or security posture. We score: **does the agent deliver what it promises?**

---

## How It Works

Every service is evaluated across **4 pillars**:

1. **Contract Clarity** — Can I understand what this agent promises to do? We check for machine-readable schemas, declared input/output types, description quality, and documentation completeness.

2. **Availability** — Will it be there when I call? We monitor endpoint health continuously and track uptime over 7-day and 30-day windows.

3. **Response Fidelity** — Does it return what the schema says it will? We probe endpoints for protocol compliance, contract consistency, and response structure validation. This is the hardest dimension to measure and where the deepest moat lies.

4. **Identity & Safety** — Do I know who's behind this? We evaluate wallet legitimacy, ownership verification, and check for spam farm patterns.

On top of pillar scores, we apply **flags** — 16+ signals like `WALLET_SPAM_FARM`, `TEMPLATE_SPAM`, `PRICE_MISMATCH`, `FIDELITY_PROVEN`, `SCHEMA_PHANTOM`, and more that give agents and developers immediate context about what's going on with a service.

Scoring is continuous. Services are re-evaluated as new data comes in — uptime changes, fidelity probes return new results, schemas are updated. Scores go up and down based on real behavior, not one-time snapshots.

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

Add to your MCP client config to give any AI agent access to ScoutScore lookups, batch scoring, and fidelity checks.

### ElizaOS Plugin

ScoutScore plugin for ElizaOS submitted as [PR #6513](https://github.com/elizaos/eliza/pull/6513) to elizaos/eliza. Adds trust scoring actions directly to Eliza agents.

### API

REST API with no auth required during launch. Score services, batch score, check fidelity, browse the leaderboard.

[Full API documentation](https://scoutscore.ai/docs)

---

## Current Stats

| | |
|---|---|
| **13,681+** | Services monitored |
| **4** | Scoring pillars |
| **16+** | Trust and spam flags |
| **0–100** | Trust score scale |

[Browse the leaderboard](https://scoutscore.ai/leaderboard)

---

## Links

- [scoutscore.ai](https://scoutscore.ai)
- [Documentation](https://scoutscore.ai/docs)
- [@scoutscore/sdk on npm](https://www.npmjs.com/package/@scoutscore/sdk)
- [@scoutscore/mcp-server on npm](https://www.npmjs.com/package/@scoutscore/mcp-server)
- [Scoring Methodology](./SCORING-METHODOLOGY.md)
- [Changelog](./CHANGELOG.md)
- [@ScoutScoreAI on Twitter](https://twitter.com/ScoutScoreAI)
