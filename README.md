# NZOChain Early Integration Program

**Public documentation and REST API integration examples for NZOChain Web3 security infrastructure.**

NZOChain helps developers, wallets, dApps, protocols and exchanges assess **wallet risk**, **smart-contract risk** and **transaction risk** on supported EVM networks through a documented REST API.

> **Primary journey:** [NZOChain website](https://nzochain.com/) → [Early Integration Program page](https://nzochain.com/early-integration/) → this repository for technical guides.  
> GitHub is the complementary home for public docs and examples — not a replacement for the program landing page.

**Version:** 1.1.0 · **Updated:** 2026-11-07 · **Branch:** `main`

---

## What you will find here

| Area | Contents |
|---|---|
| Product status | Honest current capabilities and limitations |
| Pricing | B2B API plans and B2C consumer plans |
| Quickstart | First authenticated API call |
| Integrations | cURL, JavaScript/TypeScript, Python, PHP, Go |
| Use cases | Wallet scan, contracts, transactions, simulation, approvals |
| API reference notes | Auth, networks, rate limits, webhooks |
| Program info | How to join Early Integration; QuickNode Startup status |

> **Scope:** documentation, integration examples and public resources only.  
> This is **not** a release of NZOChain proprietary source code, backend systems or private infrastructure.  
> No open-source license is granted in this phase. Public visibility does not grant reuse rights over NZOChain intellectual property.

---

## Confirmed capabilities (by plan)

| Capability | Notes |
|---|---|
| Wallet risk scanning | On-demand REST analysis |
| Contract risk analysis | On-demand REST analysis |
| Transaction analysis | Transaction Firewall — Starter and above |
| Transaction simulation | Plan quota; may use Tenderly when configured |
| Threat intelligence | Growth and above (tiered) |
| Approval risk review & user-authorized revocation | User must sign in their wallet |
| REST API | Official path — **no official SDK published** |

Conditional features are not universal. See [PRICING.md](./PRICING.md) and [PRODUCT-STATUS.md](./PRODUCT-STATUS.md).

**Supported scan networks:** Ethereum · BNB Chain · Polygon · Arbitrum  
**Not** documented as supported: Solana, Base.

---

## Official public surfaces

| Resource | URL |
|---|---|
| Website | https://nzochain.com/ |
| Early Integration Program (presentation) | https://nzochain.com/early-integration/ |
| Developer Portal | https://developers.nzochain.com/ |
| Product documentation | https://docs.nzochain.com/ |
| API base | https://api.nzochain.com/ |
| Consumer app | https://app.nzochain.com/ |
| This repository | https://github.com/nzochain/early-integration-program |

Portuguese overview: [README.pt-BR.md](./README.pt-BR.md)

---

## Start in five minutes

1. Create a project in the [Developer Portal](https://developers.nzochain.com/).
2. Generate an API key (`X-API-Key`) — never commit real keys.
3. Call wallet risk:

```bash
curl -sS -X POST "https://api.nzochain.com/api/v1/wallets/risk?lang=en" \
  -H "Content-Type: application/json" \
  -H "X-API-Key: YOUR_NZOCHAIN_API_KEY" \
  -d '{"wallet":"0xYOUR_WALLET_ADDRESS","network":"ethereum"}'
```

Full guide: [QUICKSTART.md](./QUICKSTART.md)

---

## Documentation map

| Topic | Document |
|---|---|
| Product status | [PRODUCT-STATUS.md](./PRODUCT-STATUS.md) |
| Pricing (B2B + B2C) | [PRICING.md](./PRICING.md) |
| Quickstart | [QUICKSTART.md](./QUICKSTART.md) |
| Integrations | [integrations/README.md](./integrations/README.md) |
| Use cases | [use-cases/](./use-cases/) |
| Supported networks | [api/supported-networks.md](./api/supported-networks.md) |
| API authentication | [api/authentication.md](./api/authentication.md) |
| Rate limits & errors | [api/rate-limits-and-errors.md](./api/rate-limits-and-errors.md) |
| Webhooks | [api/webhooks.md](./api/webhooks.md) |
| Early Integration Program | [EARLY-INTEGRATION-PROGRAM.md](./EARLY-INTEGRATION-PROGRAM.md) |
| QuickNode Startup Program | [QUICKNODE-STARTUP-PROGRAM.md](./QUICKNODE-STARTUP-PROGRAM.md) |
| Security & roadmap | [SECURITY-AND-ROADMAP.md](./SECURITY-AND-ROADMAP.md) |
| Contributing | [CONTRIBUTING.md](./CONTRIBUTING.md) |

### Integrations by language

- [cURL](./integrations/curl.md)
- [JavaScript / TypeScript](./integrations/javascript-typescript.md)
- [Python](./integrations/python.md)
- [PHP](./integrations/php.md)
- [Go](./integrations/go.md)

### Use cases

- [Wallet risk scanning](./use-cases/wallet-risk-scanning.md)
- [Contract analysis](./use-cases/contract-analysis.md)
- [Transaction analysis](./use-cases/transaction-analysis.md)
- [Transaction simulation](./use-cases/transaction-simulation.md)
- [Approval revocation](./use-cases/approval-revocation.md)

---

## Topics (for discovery)

Useful search terms that describe this repository honestly:

- Web3 security API documentation
- Wallet risk scoring (EVM)
- Smart contract risk analysis
- Transaction firewall / simulation notes
- Approval revocation (user-authorized)
- Early Integration Program for NZOChain

This repository is structured so documentation and examples can be found by developers, search engines and AI tools that index public GitHub content. **No ranking or indexing outcome is promised.**

---

## Security notice

Never publish real API keys, tokens, passwords, `.env` values, private RPCs, customer logs or personal data.

```bash
NZOCHAIN_API_KEY=YOUR_NZOCHAIN_API_KEY
```

---

## Contact

**Email:** contact@nzochain.com  
**Suggested subject:** `NZOChain Early Integration Program`  
**Program page:** https://nzochain.com/early-integration/
