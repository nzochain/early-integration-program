# Use case: transaction analysis

Analyze a proposed transaction (Transaction Firewall) before the user signs.

---

## Prerequisites

| Item | Requirement |
|---|---|
| B2B plan | **Starter** or higher |
| Scope | `transaction.analyze` |
| Auth | `X-API-Key` |

Free plan does **not** include Transaction Firewall. Attempting analyze on Free → `403 PLAN_UPGRADE_REQUIRED`.

---

## Endpoint

`POST https://api.nzochain.com/api/v1/transactions/analyze`

```json
{
  "chainId": 1,
  "wallet": "0xYOUR_WALLET_ADDRESS",
  "to": "0xYOUR_TO_ADDRESS",
  "calldata": "0xYOUR_CALLDATA",
  "value": "0"
}
```

Response follows the published Firewall envelope (`riskScore`, `riskLevel`, `decision`, `reasons`, `meta`).

Source: https://docs.nzochain.com/api/v1

---

## Integration tips

- Run analysis server-side before presenting a signing prompt
- Map `chainId` carefully to supported networks
- Handle `403` plan/scope errors and `429` quota errors distinctly
- Advisory only — does not stop a user who bypasses your UI

---

## Related

- [transaction-simulation.md](./transaction-simulation.md)
- [PRICING.md](../PRICING.md)
