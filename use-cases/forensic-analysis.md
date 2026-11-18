# Use case: forensic analysis (consumer)

Help end users triage a suspected wallet drain with a **heuristic, advisory** timeline — without claiming legal proof or fund recovery.

This flow is primarily a **B2C / public app** capability. B2B integrators may reference it when guiding users after an incident or when building companion education in their own product.

---

## What it solves

- Consolidated view of recent on-chain activity when tokens or NFTs left a wallet without clear user intent.
- A **90-day** advisory window (`windowDays=90`) covering outbound transfers, approval-related patterns and residual permissions.
- Verdict triage (`approval-drain`, `key-compromised`, `no-outflow`, `inconclusive`, and related UI refinements) to suggest **next steps**, not criminal attribution.

Outputs are **product heuristics**. They are **not** definitive forensic proof, court-ready evidence or attacker identification.

---

## Public surfaces

| Surface | URL |
|---|---|
| App page («Foste hackeado?» / “Were you hacked?”) | https://app.nzochain.com/forensic |
| Product documentation | https://docs.nzochain.com/ (forensic analysis feature page) |
| Analyze endpoint | `POST https://api.nzochain.com/api/forensic/analyze` |

Initial analyze requests on the public path do **not** require B2B API key authentication. Viewing full residual approval detail and **user-authorized revocation** in the forensic UX typically requires **login** and **wallet connect**.

Supported networks for this product flow: **Ethereum, BNB Chain, Polygon, Arbitrum** (same EVM set as the public scan engine).

---

## Typical user journey

1. User opens the forensic page and submits the affected `0x…` address.
2. Optionally provides short context (character limit per public docs) and a subset of networks.
3. Platform returns verdict, timeline elements, drainer hints and permission summaries within the 90-day window.
4. User follows advisory guidance: pause signing, revoke dangerous approvals (self-signed, non-custodial), consider a new wallet if key compromise is suspected, use [transaction simulation](./transaction-simulation.md) before signing again.

Rate limiting may return HTTP `429` on heavy use; retry later per public API guidance.

---

## How integrators should position it

- Point users to the **public app** and **docs** — do not embed internal architecture or undocumented endpoints.
- Pair forensic triage with your own support playbooks; NZOChain does **not** recover stolen assets.
- For programmatic B2B risk calls, use v1 routes (`/api/v1/wallets/risk`, etc.) with `X-API-Key` — see [api/authentication.md](../api/authentication.md).

---

## Limitations

- Heuristic verdicts can be `inconclusive` when data is partial or a network fails in the request.
- No guarantee of completeness across all historical activity beyond the documented window.
- Not a substitute for law enforcement, exchange support or professional incident response retainers.
- Distinct quotas and rate limits from B2B v1 API monthly call quotas.

---

## Related

- [approval-revocation.md](./approval-revocation.md)
- [transaction-simulation.md](./transaction-simulation.md)
- [wallet-risk-scanning.md](./wallet-risk-scanning.md)
- [PRODUCT-STATUS.md](../PRODUCT-STATUS.md)