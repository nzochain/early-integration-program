# Integrations

Educational examples for calling the NZOChain **REST API**. There is **no official SDK** in this release.

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
