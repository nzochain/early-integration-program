# Use case: contract analysis

Evaluate advisory risk for a smart contract / token address on a supported EVM network.

---

## What it solves

- On-demand contract risk signals for listing, swap warnings and dApp allowlists
- Consistent Firewall-style envelope (`riskScore`, `riskLevel`, `decision`)

---

## Endpoint

`POST https://api.nzochain.com/api/v1/contracts/risk`

```json
{
  "address": "0xYOUR_CONTRACT_ADDRESS",
  "network": "ethereum"
}
```

| Item | Value |
|---|---|
| Scope | `contract.scan` |
| Minimum B2B plan | Free |
| Auth | `X-API-Key` |

Source: https://docs.nzochain.com/api/v1

---

## Operational notes

- Same supported networks as wallet risk: `ethereum`, `bnb`, `polygon`, `arbitrum`
- Missing scope → `403 SCOPE_REQUIRED`
- Consumes monthly API call quota
- Treat output as advisory — contract analysis does not replace audits

---

## Related

- [wallet-risk-scanning.md](./wallet-risk-scanning.md)
- Product feature overview: https://docs.nzochain.com/features/contract-analysis
