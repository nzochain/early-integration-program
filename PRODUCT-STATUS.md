# Product Status

**As of:** 2026-11-07 · **Docs release:** 1.0.0

This page describes the publicly confirmed product state for NZOChain. Unverified claims are marked as pending and must not be treated as live features.

---

## Product identity

NZOChain is a Web3 security infrastructure that exposes risk analysis and assessment services through:

- a **REST API** for developers and organizations (B2B), and
- a **consumer application** for individual users (B2C).

It helps teams evaluate wallet, contract and transaction risk signals before or during product workflows.

---

## RiskScore

The current RiskScore is based on:

- heuristics,
- evaluation rules,
- security signals from multiple sources.

### Do not describe the current product as

- “AI-powered RiskScore”
- “proprietary AI model”
- “autonomous AI security engine”

AI-assisted scoring may be a future evolution. It is **not** a confirmed current product capability for public marketing.

---

## Scanning model

### On-demand scanning

Analysis requested by a user or application (typical API / app flow).

### Scheduled re-scan

Optional monitoring when available and enabled by the user/project, with a **six-hour** interval.

Important facts:

- Re-scan is **opt-in** and **not** enabled by default.
- Production scheduler execution for all tenants has **not** been universally confirmed in this documentation set — treat it as a product capability that must be enabled and verified per environment, not as a guaranteed always-on service for every account.
- Do **not** use marketing language such as:
  - real-time monitoring
  - continuous monitoring
  - mempool monitoring

---

## Supported networks (scan engine)

Confirmed for the identified scan engine:

| Network | API `network` value |
|---|---|
| Ethereum | `ethereum` |
| BNB Chain | `bnb` |
| Polygon | `polygon` |
| Arbitrum | `arbitrum` |

**Not** currently supported by the identified scan engine:

- Solana
- Base

See [api/supported-networks.md](./api/supported-networks.md).

---

## Feature availability by surface

| Area | Status |
|---|---|
| Wallet risk (API) | Available — Free plan and above |
| Contract risk (API) | Available — Free plan and above |
| Transaction analysis (Transaction Firewall) | Available — Starter and above |
| Transaction simulation | Available by plan quota; may depend on external simulation configuration (e.g. Tenderly) when configured |
| Threat intelligence | Growth (standard) / Business+ (full) — Enterprise pilot-grade multi-source by contract |
| Approval risk review | Available in product flows |
| User-authorized approval revocation | Available — user must sign in their wallet; NZOChain does not revoke without authorization |
| B2B webhooks | Live event confirmed: `revocation.completed` |
| Official SDK | **Not published** — integrate via REST API |
| Open-source proprietary backend | **Not published** |

Plan gates and quotas: [PRICING.md](./PRICING.md).

---

## Integration path

1. Create a project in the [Developer Portal](https://developers.nzochain.com/).
2. Generate an API key.
3. Call `https://api.nzochain.com` with header `X-API-Key`.
4. Follow published OpenAPI / Mintlify docs: https://docs.nzochain.com/

There is **no** official package such as `@nzochain/sdk`. Community examples in this repository are educational only.

---

## Honest limitations

- Risk signals are advisory; they do not guarantee safety of a wallet, contract or transaction.
- Simulation success is not guaranteed for every contract or network.
- Quota exhaustion is not the same as API key expiration.
- Early Integration participation does not imply SLA, free enterprise quotas or commercial partnership.

---

## Related documents

- [PRICING.md](./PRICING.md)
- [QUICKSTART.md](./QUICKSTART.md)
- [SECURITY-AND-ROADMAP.md](./SECURITY-AND-ROADMAP.md)
- [EARLY-INTEGRATION-PROGRAM.md](./EARLY-INTEGRATION-PROGRAM.md)
