# NZOChain — Early Integration Program

Explore, integrate and build with NZOChain, a Web3 security infrastructure designed to help developers and organizations assess wallet, contract and transaction risks through REST APIs.

This public repository is the first official documentation and example set for teams that want to evaluate and integrate NZOChain into wallets, dApps, protocols, exchanges and other Web3 products.

> **Scope:** documentation, integration examples and public resources only.  
> This is **not** a release of NZOChain proprietary source code, backend systems or private infrastructure.  
> No open-source license is granted in this phase. Public visibility does not mean reuse rights over NZOChain intellectual property.

**Version:** 1.0.0 · **Date:** 2026-11-07 · **Branch target:** `main`

---

## What this program is

The Early Integration Program brings NZOChain closer to teams that want to test available security capabilities and validate real product use cases before a deeper commercial relationship.

You can:

- Learn the current product status with honest limitations.
- Call the public REST API with language-specific examples.
- Review pricing, quotas and rate-limit behaviour.
- Explore wallet, contract, transaction and approval-related workflows.
- Contact the team to collaborate on integration feedback.

---

## Confirmed capabilities

Available according to plan and configuration (see [PRICING.md](./PRICING.md) and [PRODUCT-STATUS.md](./PRODUCT-STATUS.md)):

| Capability | Notes |
|---|---|
| Wallet risk scanning | On-demand analysis via REST API |
| Contract risk analysis | On-demand analysis via REST API |
| Transaction analysis | Transaction Firewall — Starter and above |
| Transaction simulation | Plan quota + external simulation configuration when applicable |
| Threat intelligence | Growth and above (standard / full by plan) |
| Approval risk review & user-authorized revocation | User must authorize revocation in their wallet |
| REST API integration | Official integration path — **no official SDK published** |

Conditional features are **not** universal. Always check plan entitlements.

---

## Official links

Confirm these public surfaces before integrating:

| Resource | URL |
|---|---|
| Website | https://nzochain.com/ |
| Developer Portal | https://developers.nzochain.com/ |
| Documentation | https://docs.nzochain.com/ |
| API | https://api.nzochain.com/ |
| B2C App | https://app.nzochain.com/ |
| Early Integration page | https://nzochain.com/early-integration/ |
| This repository | https://github.com/nzochain/early-integration-program |

Portuguese overview: [README.pt-BR.md](./README.pt-BR.md)

---

## Navigation

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

## Security notice for contributors and readers

Never publish real API keys, tokens, passwords, `.env` values, private RPCs, customer logs or personal data in issues, PRs or forks.

Use placeholders only, for example:

```bash
NZOCHAIN_API_KEY=YOUR_NZOCHAIN_API_KEY
```

---

## Contact

**Email:** contact@nzochain.com  
**Suggested subject:** `NZOChain Early Integration Program`
