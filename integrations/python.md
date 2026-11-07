# Python integration

Call NZOChain API v1 with `requests` (or `httpx`). Educational example only — not an official SDK.

## Requirements

- Python 3.10+
- `requests` (`pip install requests`)
- Environment variable `NZOCHAIN_API_KEY`

## Environment

```bash
export NZOCHAIN_API_KEY="YOUR_NZOCHAIN_API_KEY"
```

## Complete example

```python
import os
import sys
import requests

API_BASE = "https://api.nzochain.com"
ENDPOINT = f"{API_BASE}/api/v1/wallets/risk"


def wallet_risk(wallet: str, network: str = "ethereum") -> dict:
    api_key = os.environ.get("NZOCHAIN_API_KEY")
    if not api_key:
        raise RuntimeError("Missing NZOCHAIN_API_KEY")

    response = requests.post(
        ENDPOINT,
        params={"lang": "en"},
        headers={
            "Content-Type": "application/json",
            "X-API-Key": api_key,
        },
        json={"wallet": wallet, "network": network},
        timeout=60,
    )

    try:
        body = response.json()
    except ValueError:
        body = {}

    if response.status_code == 401:
        raise RuntimeError("Unauthorized: check API key")
    if response.status_code == 403:
        raise RuntimeError(
            f"Forbidden: {body.get('code')} {body.get('required') or body.get('feature')}"
        )
    if response.status_code == 429:
        raise RuntimeError(
            f"Quota/rate limited: {body.get('code')} resetAt={body.get('resetAt')}"
        )
    if response.status_code >= 400 or body.get("success") is False:
        raise RuntimeError(f"Request failed HTTP {response.status_code}: {body}")

    return body.get("data") or {}


if __name__ == "__main__":
    try:
        data = wallet_risk("0xYOUR_WALLET_ADDRESS", "ethereum")
        print(data.get("riskScore"), data.get("riskLevel"), data.get("decision"))
    except Exception as exc:
        print(exc, file=sys.stderr)
        sys.exit(1)
```

## Expected response fields

From the published v1 envelope: `riskScore`, `riskLevel` (`SAFE` | `CAUTION` | `HIGH` | `CRITICAL`), `decision` (`ALLOW` | `REVIEW` | `BLOCK`), optional `reasons` and `meta`.

## How to run

```bash
pip install requests
export NZOCHAIN_API_KEY="YOUR_NZOCHAIN_API_KEY"
python wallet_risk.py
```

## Quota note

Successful calls consume monthly B2B API quota. Treat RiskScore as advisory.

Static validation only — no live API calls were made while authoring this guide.
