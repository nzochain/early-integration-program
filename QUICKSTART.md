# Quickstart

Get your first NZOChain API response in five steps.

Official docs: https://docs.nzochain.com/  
API base: `https://api.nzochain.com`

---

## Step 1 — Create an account

1. Open the [Developer Portal](https://developers.nzochain.com/).
2. Sign up / sign in.
3. Create or select a project.

---

## Step 2 — Generate an API key

1. In the Developer Portal, open your project’s API key settings.
2. Create a key.
3. Store it only in a local environment variable — **never** commit it to GitHub.

```bash
# Unix / macOS
export NZOCHAIN_API_KEY="YOUR_NZOCHAIN_API_KEY"

# Windows PowerShell
$env:NZOCHAIN_API_KEY = "YOUR_NZOCHAIN_API_KEY"
```

Example `.env` (placeholders only — keep real keys out of version control):

```bash
NZOCHAIN_API_KEY=YOUR_NZOCHAIN_API_KEY
```

---

## Step 3 — First call (wallet risk)

Confirmed endpoint:

`POST https://api.nzochain.com/api/v1/wallets/risk`

Header:

`X-API-Key: YOUR_NZOCHAIN_API_KEY`

Body:

```json
{
  "wallet": "0xYOUR_WALLET_ADDRESS",
  "network": "ethereum"
}
```

Valid `network` values for the scan engine documented in this release:

- `ethereum`
- `bnb`
- `polygon`
- `arbitrum`

cURL example:

```bash
curl -sS -X POST "https://api.nzochain.com/api/v1/wallets/risk" \
  -H "Content-Type: application/json" \
  -H "X-API-Key: ${NZOCHAIN_API_KEY}" \
  -d "{\"wallet\":\"0xYOUR_WALLET_ADDRESS\",\"network\":\"ethereum\"}"
```

More languages: [integrations/](./integrations/)

---

## Step 4 — Interpret the response

Successful responses follow the published API v1 envelope (Mintlify / OpenAPI contract):

```json
{
  "success": true,
  "data": {
    "riskScore": 0,
    "riskLevel": "SAFE | CAUTION | HIGH | CRITICAL",
    "decision": "ALLOW | REVIEW | BLOCK",
    "reasons": ["human-readable phrases"],
    "meta": {}
  }
}
```

Typical mapping: `CRITICAL` / `HIGH` → `BLOCK` · `CAUTION` → `REVIEW` · `SAFE` → `ALLOW`.

Field meanings (high level):

| Field | Role |
|---|---|
| `success` | Whether the API call completed successfully |
| `data.riskScore` | Numeric RiskScore (0–100 advisory) from heuristics / rules / multi-source signals |
| `data.riskLevel` | Qualitative level: `SAFE`, `CAUTION`, `HIGH`, or `CRITICAL` |
| `data.decision` | Advisory decision: `ALLOW`, `REVIEW`, or `BLOCK` |
| `data.reasons` | Human-readable explanation phrases when present |
| `data.meta` | Additional metadata object when present |

Exact field sets, enums and additional payload keys should be taken from the live OpenAPI / Mintlify contract:

https://docs.nzochain.com/

### Common HTTP outcomes

| Status | Meaning |
|---|---|
| `200` | Success |
| `400` | Invalid request (validation) |
| `401` / `403` | Missing or invalid API key / permission |
| `429` | Quota or rate limit (`RATE_LIMIT` or `HARD_CEILING`) |
| `5xx` | Server / upstream issue |

Details: [api/rate-limits-and-errors.md](./api/rate-limits-and-errors.md)

**Reminder:** hitting monthly quota ≠ API key expiration.

This call consumes B2B API quota according to your plan ([PRICING.md](./PRICING.md)).

---

## Step 5 — Continue

- [Wallet risk scanning](./use-cases/wallet-risk-scanning.md)
- [Contract analysis](./use-cases/contract-analysis.md)
- [Transaction analysis](./use-cases/transaction-analysis.md)
- [Transaction simulation](./use-cases/transaction-simulation.md)
- [Authentication](./api/authentication.md)
- [Early Integration Program](./EARLY-INTEGRATION-PROGRAM.md)
