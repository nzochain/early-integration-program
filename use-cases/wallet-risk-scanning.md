# Use case: wallet risk scanning

Assess the advisory risk of an EVM wallet address before onboarding, transfers or privileged actions.

---

## What it solves

- On-demand RiskScore for a wallet on a supported network
- Human-readable reasons and an advisory `decision` (`ALLOW` | `REVIEW` | `BLOCK`)
- Integration into wallets, dApps, compliance triage queues and internal tooling

RiskScore is based on heuristics, evaluation rules and multi-source security signals. It is **advisory**, not a guarantee of safety. It is **not** marketed here as an AI model.

---

## How to query

`POST https://api.nzochain.com/api/v1/wallets/risk`

Headers:

- `Content-Type: application/json`
- `X-API-Key: YOUR_NZOCHAIN_API_KEY`

Body:

```json
{
  "wallet": "0xYOUR_WALLET_ADDRESS",
  "network": "ethereum"
}
```

Optional DTO fields documented publicly: `forceRefresh`, `includeBlocked`, `requesterWallet`.

Scope: `wallet.scan` · Minimum plan: **Free**

---

## Interpreting RiskScore

Envelope fields from the API v1 contract:

| Field | Meaning |
|---|---|
| `riskScore` | Numeric advisory score (0–100 scale in product docs) |
| `riskLevel` | `SAFE` \| `CAUTION` \| `HIGH` \| `CRITICAL` |
| `decision` | `ALLOW` \| `REVIEW` \| `BLOCK` |
| `reasons` | Human-readable phrases when present |

Typical mapping: CRITICAL/HIGH → BLOCK · CAUTION → REVIEW · SAFE → ALLOW.

Product logic should decide how to act on `REVIEW` / `BLOCK` (block UX, require secondary confirmation, queue for manual review, etc.).

---

## Supported networks

`ethereum` · `bnb` · `polygon` · `arbitrum`

See [api/supported-networks.md](../api/supported-networks.md).

---

## Limitations

- On-demand by default; scheduled re-scan is opt-in (6h) when available/enabled — not real-time or mempool monitoring
- Solana and Base are not supported by the identified scan engine
- Consumes monthly B2B API quota
- Results are advisory only

Examples: [integrations/](../integrations/)
