# Use case: transaction simulation

Simulate a transaction to understand potential outcomes before signing, within plan quotas.

---

## Prerequisites

| Item | Requirement |
|---|---|
| B2B plan | **Starter** or higher |
| Scope | `transaction.analyze` |
| Feature gate | `transaction_simulate` |
| Auth | `X-API-Key` |
| Monthly simulation quota | Starter 100 · Growth 2,000 · Business 10,000 · Enterprise under contract · Free **0** |

Exhausted simulation quota → `403 SIMULATION_QUOTA`.

---

## Endpoint

`POST https://api.nzochain.com/api/v1/transactions/simulate`

```json
{
  "wallet": "0xYOUR_WALLET_ADDRESS",
  "network": "ethereum",
  "tx": {
    "to": "0xYOUR_TO_ADDRESS",
    "data": "0xYOUR_CALLDATA",
    "value": "0"
  }
}
```

Source: https://docs.nzochain.com/api/v1

---

## External dependency (Tenderly)

- **Live** simulation requires **Tenderly** when configured.
- Without Tenderly (or if the live call fails), the API returns **static / degraded** analysis.
- Do **not** guarantee successful simulation for every contract or network.

Enterprise docs may reference Tenderly when configured under contract.

---

## Limitations

- Not available on Free
- Separate simulation quota from general API call quota
- Advisory / best-effort outcomes
- Supported networks remain the four EVM networks documented for the product

---

## Related

- [transaction-analysis.md](./transaction-analysis.md)
- [PRICING.md](../PRICING.md)
- [api/rate-limits-and-errors.md](../api/rate-limits-and-errors.md)
