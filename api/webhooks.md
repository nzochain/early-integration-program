# Webhooks

Outbound HMAC webhooks for B2B projects.

## Live vs roadmap

| Event | Status |
|---|---|
| `revocation.completed` | **Live** (currently supported) |
| `wallet.scan.completed` | **Roadmap — not live** |
| `risk.alert` | **Roadmap — not live** |

Do not treat B2C email / push / Telegram alerts as B2B webhooks.

Source: https://docs.nzochain.com/api/webhooks

---

## Managing subscriptions

Recommended: Developer Portal UI — https://developers.nzochain.com/webhooks

Portal/session management is a **separate** auth contract from product `X-API-Key` calls.

Example management route (portal session — not product API key):

```http
POST https://api.nzochain.com/api/developer/projects/:projectId/webhooks
Body: { "url": "https://your-app.com/hooks", "events": ["revocation.completed"] }
```

---

## Event: `revocation.completed`

Fired when an approval revocation is confirmed on-chain.

### Headers

- `X-NZOChain-Signature: sha256=<hmac>`
- `X-NZOChain-Event: revocation.completed`

### Body (schema from public docs)

```json
{
  "event": "revocation.completed",
  "timestamp": "2026-09-15T18:00:00.000Z",
  "data": {
    "wallet": "0xYOUR_WALLET_ADDRESS",
    "network": "ethereum",
    "spender": "0xYOUR_SPENDER_ADDRESS",
    "dappName": null,
    "symbol": "USDT",
    "txHash": "0xYOUR_TX_HASH",
    "revokedAt": "2026-09-15T18:00:00.000Z"
  }
}
```

---

## Verifying authenticity

1. Read the **raw JSON body**.
2. Compute HMAC-SHA256 with your webhook secret (`whsec_*` format in docs).
3. Compare to `X-NZOChain-Signature` (prefix `sha256=`).

---

## Delivery behaviour

- HTTPS only (SSRF protections apply)
- Retries: 1s → 5s → 30s
- Expect HTTP 2xx; non-2xx marks the webhook as failing after retries

---

## Related

- [use-cases/approval-revocation.md](../use-cases/approval-revocation.md)
- [api/authentication.md](./authentication.md)
