# Integrations

Educational examples for **your backend** calling the NZOChain **REST API**. There is **no official SDK** in this release.

This section documents **how clients integrate with NZOChain** — keys, scopes, endpoints and webhooks — not internal platform suppliers.

## Connect your application

1. Create a project at https://developers.nzochain.com/
2. Generate an API key and store it as a secret (`NZOCHAIN_API_KEY` in examples).
3. Restrict [scopes](../api/authentication.md) to the minimum required for your routes.
4. Call `https://api.nzochain.com` from **server-side** code only (never expose keys in browser bundles).
5. Optionally register [webhooks](../api/webhooks.md) for supported events (e.g. `revocation.completed`).

Base URL: `https://api.nzochain.com`  
Auth header: `X-API-Key: YOUR_NZOCHAIN_API_KEY`  
Primary starter endpoint: `POST /api/v1/wallets/risk`

| Guide | Language |
|---|---|
| [curl.md](./curl.md) | cURL |
| [javascript-typescript.md](./javascript-typescript.md) | JavaScript & TypeScript |
| [python.md](./python.md) | Python |
| [php.md](./php.md) | PHP |
| [go.md](./go.md) | Go |

## Rules shared by all examples

- Use environment variables for secrets.
- Never commit real API keys.
- Handle HTTP `401`, `403` and `429` explicitly.
- Each successful call consumes B2B quota per [PRICING.md](../PRICING.md).
- Examples are not an official package or SDK.

## Confirmed v1 endpoints

| Method | Path | Min plan |
|---|---|---|
| `POST` | `/api/v1/wallets/risk` | Free |
| `POST` | `/api/v1/contracts/risk` | Free |
| `POST` | `/api/v1/transactions/analyze` | Starter |
| `POST` | `/api/v1/transactions/simulate` | Starter (+ simulation quota) |
| `POST` | `/api/v1/threats/check` | Growth |

Source of truth: https://docs.nzochain.com/api/v1
