# Rate limits and errors

NZOChain API errors typically return JSON with `success: false` and a `code` in `SCREAMING_SNAKE` when applicable.

Official reference: https://docs.nzochain.com/api/errors

---

## Authentication

| HTTP | When |
|---|---|
| `401` | `X-API-Key` missing, invalid or revoked |

---

## Plan and feature gates (v1)

| HTTP | `code` | When |
|---|---|---|
| `403` | `SCOPE_REQUIRED` | Key lacks required scope (`required` may be present) |
| `403` | `PLAN_UPGRADE_REQUIRED` | Feature above plan (`feature`, `upgradeUrl` may be present) |
| `403` | `SIMULATION_QUOTA` | Monthly simulate quota exhausted (`used`, `quota`) |

Example:

```json
{
  "success": false,
  "statusCode": 403,
  "code": "PLAN_UPGRADE_REQUIRED",
  "message": "This API v1 feature requires a higher B2B plan.",
  "upgradeUrl": "/pricing"
}
```

---

## Monthly API call volume

| Plan | Behaviour |
|---|---|
| Free | Hard cap → `429 RATE_LIMIT` (`limit`, `used`, `resetAt`). No paid overage. |
| Starter | Overage $0.004/call up to **3×**, then `429 HARD_CEILING` |
| Growth | Overage $0.002/call up to **3×**, then `429 HARD_CEILING` |
| Business | Overage $0.001/call up to **3×**, then `429 HARD_CEILING` |
| Enterprise | Quotas/overage under contract |

`resetAt` points to the **start of the next month UTC**.

**Quota ≠ key expiration.**

Short-window infrastructure rate limits may also return `429` and are distinct from monthly quotas.

---

## Other statuses

| HTTP | Typical use |
|---|---|
| `400` | Invalid body (address, network, calldata) |
| `500` | Internal failure (generic client message in production) |

---

## Related

- [PRICING.md](../PRICING.md)
- [api/authentication.md](./authentication.md)
