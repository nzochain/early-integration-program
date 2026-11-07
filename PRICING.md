# Pricing

**As of:** 2026-11-07 · Commercial B2B reference validated against product truth for docs release 1.1.0

This page separates **B2B (API / Developer Portal)** plans from **B2C (consumer app)** plans. Wallet and scan entitlements on the consumer app are distinct from B2B API call quotas.

Official B2C pricing UI: https://app.nzochain.com/pricing  
Developer Portal: https://developers.nzochain.com/  
Product docs: https://docs.nzochain.com/

---

## B2B pricing (API)

| Plan | Monthly price | API calls / month | Simulations / month |
|---|---:|---:|---:|
| Free | $0 | 1,000 | 0 |
| Starter | $49 | 25,000 | 100 |
| Growth | $149 | 100,000 | 2,000 |
| Business | $499 | 500,000 | 10,000 |
| Enterprise | Custom | Under contract | Under contract |

API usage is governed by the monthly quota and overage rules of each plan. Public catalog plans include defined call limits and ceilings — not unlimited API calls, unlimited security coverage, SLA 99.9% or guaranteed uptime. Features apply only within the contracted plan.

### Free — $0

- 1,000 API calls / month
- Wallet risk
- Contract risk
- No Transaction Firewall
- No transaction analysis / simulation
- No Threat Intelligence
- **Hard cap** — no paid overage
- Exhaustion returns HTTP `429` with `RATE_LIMIT` semantics for Free quota exhaustion

### Starter — $49 / month

- 25,000 API calls / month
- Transaction Firewall
- 100 simulations / month
- No Threat Intelligence
- Overage: **$0.004** per extra call, up to **3×** monthly quota
- After 3×: **hard ceiling** (HTTP `429` `HARD_CEILING`)

### Growth — $149 / month

- 100,000 API calls / month
- Transaction Firewall
- 2,000 simulations / month
- Threat Intelligence **standard**
- Overage: **$0.002** per extra call, up to **3×** monthly quota
- After 3×: **hard ceiling**

### Business — $499 / month

- 500,000 API calls / month
- Transaction Firewall
- 10,000 simulations / month
- Threat Intelligence **full**
- Overage: **$0.001** per extra call, up to **3×** monthly quota
- After 3×: **hard ceiling**

### Enterprise — Custom

- Quotas set by contract
- Transaction Firewall
- Simulation with Tenderly when configured
- Threat Intelligence multi-source in **pilot-grade** modality
- Custom commercial terms and overage
- Contact sales / `contact@nzochain.com`

---

## Quotas and behaviour (B2B)

| Concept | Meaning |
|---|---|
| Monthly quota | Included API calls (and simulation quotas where applicable) per calendar month |
| Reset | Beginning of the month in **UTC** |
| Rate limit | Short-window request throttling (distinct from monthly quota) |
| Overage | Paid usage beyond included quota, when the plan allows it, until hard ceiling |
| Hard cap | Free plan: no overage; blocked at included quota |
| Hard ceiling | Paid plans: after **3×** included quota, further calls rejected (`HARD_CEILING`) |
| API key expiration | Separate from quota exhaustion |

**Quota exhaustion does not mean the API key expired.**

Early consumption warning notifications are **not** promised as a universally available feature in this release.

Error reference: [api/rate-limits-and-errors.md](./api/rate-limits-and-errors.md)

---

## B2C pricing (consumer app)

Public individual plans (app surface). Prices below are the published **monthly** amounts.

| Plan | Monthly price | Wallets | Scans / month | Contract analyses / month |
|---|---:|---:|---:|---:|
| Free | $0 | 1 | 50 | 5 |
| Basic | $4.99 | 3 | 500 | 50 |
| Pro | $9.99 | 10 | 2,000 | 200 |
| Premium | $19.99 | 50 | 10,000 | 1,000 |

Shared B2C notes:

- On-demand scanning plus optional scheduled re-scan every **6 hours (opt-in, off by default)**.
- Networks: Ethereum, BNB Chain, Polygon, Arbitrum.
- Revocation requires the user to sign in their own wallet.
- Alert channels expand by plan (email → push → Telegram / extended history on higher tiers).

B2C entitlements are **not** B2B API call quotas. **Premium** (B2C) is not the same product surface as **Business** or **Enterprise** (B2B).

The live consumer checkout currently exposes monthly plans. An annual “pay 10, use 12” style benefit is not presented as an active commercial offer in this documentation until confirmed in the live pricing UI.

Official UI: https://app.nzochain.com/pricing  
Public docs: https://docs.nzochain.com/pricing/individual

---

## Related

- [PRODUCT-STATUS.md](./PRODUCT-STATUS.md)
- [QUICKSTART.md](./QUICKSTART.md)
- [api/rate-limits-and-errors.md](./api/rate-limits-and-errors.md)
