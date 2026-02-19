# Changelog

All notable releases and milestones for ScoutScore.

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

- **Fidelity bonus** — Services that pass fidelity probing with high confidence receive a score boost; services that fail receive a penalty
- **Price mismatch penalty** — Advertised price not matching actual x402 payment amount is now penalized
- **Description quality scoring** — Generic, template, and low-effort descriptions are detected and penalized; technical, detailed documentation is rewarded
- **Deduplication** — Duplicate and near-duplicate content detection across service listings
