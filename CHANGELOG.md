# Changelog

All notable releases and milestones for ScoutScore.

---

## March 2026

### Paid Fidelity Verification (V1 + V2)

ScoutScore now dogfoods x402 - sending real USDC to services and validating responses end-to-end.

- V1 (X-PAYMENT header) and V2 (PAYMENT-SIGNATURE header) protocol support
- 198 domains paid-probed with real USDC on Base mainnet
- 60 services verified (36%), 109 broken (64%)
- $0.78 total USDC spent across all probes
- New flags: `PAID_VERIFIED`, `PAID_HOLLOW`, `PAID_SETTLED_FAILED`, `PAID_REJECTED`, `PAID_IGNORED`
- Paid verification results integrated into scoring (fidelity floor/cap + availability adjustments)

### Multi-Facilitator Discovery

Expanded from 1 discovery source to 5 dedicated scanners + auto-discovery.

- CDP Bazaar (505 domains)
- PayAI Facilitator (1,099 domains)
- AnySpend (5 domains)
- OpenFacilitator (20 domains)
- Dexter (19 domains)
- Facilitator Radar: auto-discovers new x402 facilitators from x402.org/ecosystem, 24+ facilitators tracked
- Total: 1,630 x402 domains + 457 ERC-8004 domains = 2,079 unique domains

### ERC-8004 Base Mainnet

- Registered as Agent #26282 on Base mainnet
- Production ERC-8004 pipeline: crawler, batch writer, automated cron
- 448 on-chain domains indexed, 1,362 agents tracked

### On-Chain Payment Intelligence

- Integrated Dune Analytics data into scoring pipeline
- $19.6M USDC tracked across 198 wallets
- 5.1M+ transactions, 218K unique payers
- New flags: `HAS_ONCHAIN_REVENUE`, `HIGH_PAYMENT_VOLUME`, `DIVERSE_PAYER_BASE`

### Scoring Recalibration

- Paid verification integrated into fidelity + availability pillars
- `PAID_VERIFIED` services receive a fidelity floor of 80
- `PAID_SETTLED_FAILED` services capped at fidelity 30, availability downgraded to 30
- 57 services dropped from HIGH tier due to paid verification failures
- Average trust score: 34.7/100 (down from 35.6 due to paid verification impact)

### Dashboard Redesign

- Domain watchlist with monitoring UI
- Status strip, ecosystem pulse, expandable domain cards
- Team management and activity logs

### SIWE-Authenticated Fidelity

- SIWE (Sign-In with Ethereum) authenticated fidelity probing
- Auto-detection of SIWE-required endpoints
- New flag: `SIWE_AUTHENTICATED`

### x402 Mainnet Payment Integration

- Live paid API access on Base mainnet via xpay facilitator
- x402 V2 protocol support for payment-gated endpoints

### @scoutscore/mcp-server@0.1.2

- Added `scan_skill` tool for GitHub repository trust scanning
- 5 MCP tools: `check_trust`, `check_fidelity`, `get_ecosystem_stats`, `search_services`, `scan_skill`

---

## February 2026

### @scoutscore/sdk@0.1.0

Initial beta release of the TypeScript SDK, published to npm as [@scoutscore/sdk](https://www.npmjs.com/package/@scoutscore/sdk).

- `ScoutScore` client class with full TypeScript support
- `scoreBazaarService()` for single-service scoring
- `scoreBazaarBatch()` for batch scoring (up to 20 services)
- `getFidelity()` for fidelity verification
- `getLeaderboard()` for browsing the service directory
- `getBazaarStats()` for marketplace statistics
- `getHealth()` for API health checks
- Custom error classes with automatic retry and exponential backoff
- Complete TypeScript type definitions and JSDoc documentation

### @scoutscore/mcp-server@0.1.0

Initial release of the MCP server, published to npm as [@scoutscore/mcp-server](https://www.npmjs.com/package/@scoutscore/mcp-server).

- Exposes ScoutScore capabilities as MCP tools for any compatible AI agent
- Score services, batch score, check fidelity, and browse leaderboard via MCP

### ElizaOS Plugin

ScoutScore plugin submitted as [PR #6513](https://github.com/elizaos/eliza/pull/6513) to elizaos/eliza.

- Adds trust scoring actions directly to Eliza agents
- Integrates with ScoutScore API for real-time service evaluation

### A2A Agent Card

ScoutScore agent card published following the Google A2A protocol specification.

- Machine-readable agent capabilities declaration
- Enables discovery and interoperability with other A2A-compatible agents

### x402 Payment Gate (Sepolia)

Pay-per-query scoring endpoint deployed on Sepolia testnet via x402 protocol.

- Agents can pay per score lookup using x402-compatible wallets
- Testnet deployment for integration testing ahead of mainnet

### Scoring Improvements

- **Fidelity bonus** - Services that pass fidelity probing with high confidence receive a score boost; services that fail receive a penalty
- **Price mismatch penalty** - Advertised price not matching actual x402 payment amount is now penalized
- **Description quality scoring** - Generic, template, and low-effort descriptions are detected and penalized; technical, detailed documentation is rewarded
- **Deduplication** - Duplicate and near-duplicate content detection across service listings
