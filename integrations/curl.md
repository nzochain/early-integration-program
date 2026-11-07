# cURL integration

Call NZOChain API v1 from a terminal with cURL.

## Requirements

- cURL installed
- Environment variable `NZOCHAIN_API_KEY`
- Network access to `https://api.nzochain.com`

## Environment

```bash
export NZOCHAIN_API_KEY="YOUR_NZOCHAIN_API_KEY"
```

Windows PowerShell:

```powershell
$env:NZOCHAIN_API_KEY = "YOUR_NZOCHAIN_API_KEY"
```

## Wallet risk request

```bash
curl -sS -w "\nHTTP_STATUS:%{http_code}\n" \
  -X POST "https://api.nzochain.com/api/v1/wallets/risk?lang=en" \
  -H "Content-Type: application/json" \
  -H "X-API-Key: ${NZOCHAIN_API_KEY}" \
  -d '{
    "wallet": "0xYOUR_WALLET_ADDRESS",
    "network": "ethereum"
  }'
```

Valid `network` values: `ethereum` | `bnb` | `polygon` | `arbitrum`.

## Contract risk

```bash
curl -sS -X POST "https://api.nzochain.com/api/v1/contracts/risk?lang=en" \
  -H "Content-Type: application/json" \
  -H "X-API-Key: ${NZOCHAIN_API_KEY}" \
  -d '{
    "address": "0xYOUR_CONTRACT_ADDRESS",
    "network": "ethereum"
  }'
```

## Expected success envelope

Per published API v1 contract:

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

Do not treat illustrative enum unions as a live numeric sample for a specific address.

## Error handling

| HTTP | Typical meaning |
|---|---|
| `400` | Invalid body |
| `401` | Missing / invalid / revoked API key |
| `403` | `SCOPE_REQUIRED` or `PLAN_UPGRADE_REQUIRED` |
| `429` | `RATE_LIMIT` (Free hard cap) or `HARD_CEILING` (paid after 3×) |

## Quota note

Each successful product call counts toward the monthly B2B API call quota. Simulation has a separate monthly quota on paid plans.

## How to run

1. Export `NZOCHAIN_API_KEY`.
2. Replace placeholder addresses.
3. Execute the `curl` command.
4. Inspect JSON body and HTTP status.

These examples were validated statically against the published request/response contract. No live API calls were executed while authoring this guide.
