# JavaScript / TypeScript integration

Call NZOChain API v1 with `fetch`. These snippets are educational examples — **not** an official SDK.

## Requirements

- Node.js 18+ (built-in `fetch`) or a modern browser runtime for prototyping
- For production dApps: call the API from **your backend** only (never expose API keys in public client JS)
- Environment variable `NZOCHAIN_API_KEY`

## Environment

```bash
export NZOCHAIN_API_KEY="YOUR_NZOCHAIN_API_KEY"
```

## JavaScript (Node)

```javascript
async function walletRisk(wallet, network = 'ethereum') {
  const apiKey = process.env.NZOCHAIN_API_KEY;
  if (!apiKey) {
    throw new Error('Missing NZOCHAIN_API_KEY');
  }

  const res = await fetch(
    'https://api.nzochain.com/api/v1/wallets/risk?lang=en',
    {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'X-API-Key': apiKey,
      },
      body: JSON.stringify({ wallet, network }),
    },
  );

  const body = await res.json().catch(() => ({}));

  if (res.status === 401) {
    throw new Error('Unauthorized: check API key');
  }
  if (res.status === 403) {
    throw new Error(
      `Forbidden: ${body.code || 'SCOPE_OR_PLAN'} ${body.required || body.feature || ''}`,
    );
  }
  if (res.status === 429) {
    throw new Error(
      `Quota/rate limited: ${body.code || 'RATE_LIMIT_OR_HARD_CEILING'} resetAt=${body.resetAt || 'n/a'}`,
    );
  }
  if (!res.ok || body.success === false) {
    throw new Error(`Request failed HTTP ${res.status}`);
  }

  return body.data;
}

walletRisk('0xYOUR_WALLET_ADDRESS', 'ethereum')
  .then((data) => {
    console.log(data.riskScore, data.riskLevel, data.decision);
  })
  .catch((err) => {
    console.error(err.message);
    process.exitCode = 1;
  });
```

## TypeScript

```typescript
type Network = 'ethereum' | 'bnb' | 'polygon' | 'arbitrum';
type RiskLevel = 'SAFE' | 'CAUTION' | 'HIGH' | 'CRITICAL';
type Decision = 'ALLOW' | 'REVIEW' | 'BLOCK';

interface FirewallData {
  riskScore: number;
  riskLevel: RiskLevel;
  decision: Decision;
  reasons?: string[];
  meta?: Record<string, unknown>;
}

interface ApiSuccess {
  success: true;
  data: FirewallData;
}

async function walletRisk(
  wallet: string,
  network: Network = 'ethereum',
): Promise<FirewallData> {
  const apiKey = process.env.NZOCHAIN_API_KEY;
  if (!apiKey) {
    throw new Error('Missing NZOCHAIN_API_KEY');
  }

  const res = await fetch(
    'https://api.nzochain.com/api/v1/wallets/risk?lang=en',
    {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'X-API-Key': apiKey,
      },
      body: JSON.stringify({ wallet, network }),
    },
  );

  const body = (await res.json().catch(() => ({}))) as Partial<ApiSuccess> & {
    success?: boolean;
    code?: string;
    required?: string;
    feature?: string;
    resetAt?: string;
  };

  if (!res.ok || body.success === false) {
    throw new Error(
      `HTTP ${res.status} code=${body.code || 'UNKNOWN'}`,
    );
  }

  return (body as ApiSuccess).data;
}
```

## Expected response shape

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

## How to run

```bash
export NZOCHAIN_API_KEY="YOUR_NZOCHAIN_API_KEY"
node wallet-risk.js
```

## Quota note

Each call consumes monthly B2B API quota. `429` does not mean the key expired.

Static validation only — no live API calls were made while authoring this guide.
