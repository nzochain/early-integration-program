# API authentication

B2B product routes under `/api/v1/...` require:

```http
X-API-Key: YOUR_NZOCHAIN_API_KEY
```

This is **not** cookie session auth and **not** `Authorization: Bearer` on product v1 routes.

Developer Portal project/key/webhook management uses a **separate developer session JWT** contract. Do not mix portal session auth with product API key auth.

---

## Obtain a key

1. Open https://developers.nzochain.com/
2. Create a project
3. Generate an API key (portal format commonly shown as `pk_live_...` in docs) and store it as a secret

New keys typically receive default v1 product scopes (including `wallet.scan`). You can restrict scopes in the portal.

The B2C app (https://app.nzochain.com/) does **not** use this API key — it uses wallet connection.

---

## Scopes (v1)

| Scope | Endpoint |
|---|---|
| `wallet.scan` | `POST /api/v1/wallets/risk` |
| `contract.scan` | `POST /api/v1/contracts/risk` |
| `transaction.analyze` | `POST /api/v1/transactions/analyze` and `/simulate` |
| `threat.check` | `POST /api/v1/threats/check` |

Missing scope → HTTP `403` with `SCOPE_REQUIRED` and `required`.

Plan gating is independent: you may have the scope and still receive `PLAN_UPGRADE_REQUIRED`.

---

## Example

```bash
curl -X POST "https://api.nzochain.com/api/v1/wallets/risk?lang=en" \
  -H "Content-Type: application/json" \
  -H "X-API-Key: YOUR_NZOCHAIN_API_KEY" \
  -d '{"wallet":"0xYOUR_WALLET_ADDRESS","network":"ethereum"}'
```

---

## Auth errors vs quota

| HTTP | Meaning |
|---|---|
| `401` | Missing, invalid or revoked API key |
| `403` `SCOPE_REQUIRED` | Key lacks required scope |
| `403` `PLAN_UPGRADE_REQUIRED` | Feature above plan |
| `429` | Monthly quota / hard ceiling / short-window rate limit |

**Quota exhaustion ≠ API key expiration.** A `429` does not mean the key expired.

---

## Best practices

- Server-side only
- Environment variables
- Rotate keys if leaked
- Separate keys per environment
- No official SDK — use REST clients

Source: https://docs.nzochain.com/api/authentication
