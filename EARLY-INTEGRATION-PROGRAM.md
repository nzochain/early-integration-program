# Early Integration Program

The Early Integration Program helps teams integrate, experiment with and validate NZOChain security services in real product contexts — before or alongside a standard commercial plan.

**Presentation (public):** https://nzochain.com/early-integration/  
**This repository:** technical guides, API notes and integration examples complementary to the site and [product documentation](https://docs.nzochain.com/).

---

## Objectives

- Enable wallets, dApps, protocols and infrastructure teams to call the public NZOChain REST API in realistic workflows.
- Validate use cases (wallet risk, contracts, transaction firewall, simulation, approvals, consumer forensic flows where relevant) against documented behaviour and plan gates.
- Collect structured feedback to improve documentation, Developer Portal ergonomics and product fit.
- Identify a path to a commercial B2B relationship when both sides agree — without promising automatic partnership or custom commercial terms.

The program is **technical validation and integration**, not a grant, accelerator or unlimited free tier.

---

## Who can join

Teams building on supported EVM networks who need advisory security signals in product flows, including:

- Wallets
- dApps and DeFi protocols
- Exchanges and on-ramps
- Web3 startups and security-focused projects
- Developer tooling and blockchain infrastructure teams

Consumer-facing products may also use B2C surfaces (app, forensic page) under published B2C plans; B2B API integration still requires a Developer Portal project and API key.

NZOChain may participate in **external ecosystem programs** that support early-stage Web3 builders. Those programs are independent of this Early Integration track and **do not** change API quotas, SLAs or commercial terms unless explicitly agreed in writing.

---

## Eligibility

Participation is evaluated case by case. Typical expectations:

- A clear product or integration scenario (not generic curiosity-only requests).
- Ability to test against `https://api.nzochain.com` with your own backend or staging environment.
- Respect for published [plan gates and quotas](./PRICING.md) (Free plan and above are self-serve; higher tiers or Enterprise require commercial alignment).
- Commitment to keep API keys and any shared logs confidential; no publication of secrets in public repos or tickets.
- Acceptance that RiskScore, simulation and forensic outputs are **advisory**, not custody, insurance or legal proof.

NZOChain reserves the right to decline or pause participation when misuse, abuse or misrepresentation of product capabilities is detected.

---

## Benefits (what is actually offered)

| Benefit | Detail |
|---|---|
| Public API access | Per your selected B2B plan (including Free where applicable) — see [PRICING.md](./PRICING.md) |
| Documentation | This repo, [docs.nzochain.com](https://docs.nzochain.com/), OpenAPI reference |
| Integration examples | cURL, JavaScript/TypeScript, Python, PHP, Go — [integrations/](./integrations/) |
| Technical accompaniment | Best-effort alignment calls and integration Q&A **subject to team availability** |
| Use-case collaboration | Joint review of how NZOChain endpoints map to your flows |
| Feedback loop | Product and documentation improvements driven by integrator input |

**Not included:** financial support or grants; quotas beyond the published Free plan unless you purchase a paid plan; SLA or uptime guarantees; free third-party security audits; automatic commercial partnership; dedicated unlimited API access; or private features not described in public docs.

---

## Application process

1. **Prepare a short brief:** product name, supported networks, target users, and which NZOChain capabilities you plan to call (wallet scan, contract risk, transaction analyze/simulate, threat check, webhooks, etc.).
2. **Create a Developer Portal project** (if you do not already have one): https://developers.nzochain.com/
3. **Email** contact@nzochain.com with subject `NZOChain Early Integration Program`, attaching or pasting the brief and your intended timeline.
4. **Start with published docs:** [QUICKSTART.md](./QUICKSTART.md) and the relevant [use cases](./use-cases/) while the team reviews your request.

You may begin integration on the **Free** plan without waiting for a reply, provided you stay within public quotas and scopes.

---

## Approval process

- **Self-serve path:** Free and paid catalog plans are available through the Developer Portal; no program approval is required to use the public API within plan limits.
- **Program track:** After your email, NZOChain may schedule an alignment call, suggest a suitable plan tier, or ask for clarification on scope and data handling.
- **Outcome:** Confirmation of how the team will support your integration (documentation pointers, optional office hours) — **not** a guarantee of Enterprise pricing, custom quotas or SLA.

Commercial terms for Enterprise remain under separate sales contact.

---

## Technical onboarding

Recommended order:

1. Read [PRODUCT-STATUS.md](./PRODUCT-STATUS.md) for honest capability boundaries.
2. Confirm [supported networks](./api/supported-networks.md) (`ethereum`, `bnb`, `polygon`, `arbitrum`).
3. Generate an API key; assign minimal [scopes](./api/authentication.md).
4. Run the first wallet risk call from [QUICKSTART.md](./QUICKSTART.md).
5. Implement your language client using [integrations/](./integrations/README.md).
6. Configure [webhooks](./api/webhooks.md) if you rely on `revocation.completed` or future documented events.
7. Monitor [rate limits and errors](./api/rate-limits-and-errors.md) in production-like tests.

There is **no official SDK**; integrate via REST from your backend.

---

## API integration

- **Base URL:** `https://api.nzochain.com`
- **Auth:** header `X-API-Key` on `/api/v1/...` product routes
- **Scopes:** `wallet.scan`, `contract.scan`, `transaction.analyze`, `threat.check` — see [api/authentication.md](./api/authentication.md)
- **Plan gating:** independent of scopes (e.g. Transaction Firewall from Starter; simulation quota on paid B2B plans)
- **Consumer forensic analyze:** `POST /api/forensic/analyze` — documented at [https://docs.nzochain.com/](https://docs.nzochain.com/) and [use-cases/forensic-analysis.md](./use-cases/forensic-analysis.md); distinct from B2B key-authenticated v1 routes

Source of truth for request/response shapes: https://docs.nzochain.com/api/v1

---

## Support during participation

- **Primary:** public documentation and this repository.
- **Email:** contact@nzochain.com (same subject line) for integration blockers, doc gaps or program questions.
- **Response time:** best effort; **no** production SLA for Early Integration participants unless covered by a paid Enterprise contract.

Escalation for security incidents affecting your keys: rotate keys in the Developer Portal and notify NZOChain if you suspect platform abuse.

---

## Participation phases

| Phase | Activities |
|---|---|
| Discovery | Brief, plan selection, read product status and pricing |
| Integration | Implement auth, core endpoints, error handling, quotas |
| Validation | Test realistic volumes, webhook signatures, user flows (including advisory decisions) |
| Feedback | Share integration friction, doc gaps and feature requests |
| Next step | Continue on catalog plan, upgrade tier, or explore Enterprise conversation if needed |

Phases overlap; there is no fixed calendar unless agreed in email.

---

## Responsibilities

**Your team**

- Protect API keys; server-side usage only for B2B keys.
- Stay within quotas and acceptable use; handle `401` / `403` / `429` explicitly.
- Treat outputs as advisory; communicate limits to end users.
- Do not misrepresent NZOChain as insurance, custody or guaranteed exploit prevention.

**NZOChain**

- Maintain publicly documented API behaviour and honest product status.
- Provide integration documentation and examples in this repo.
- Offer reasonable technical guidance when capacity allows.

---

## Contacts and next steps

| Step | Action |
|---|---|
| Program page | https://nzochain.com/early-integration/ |
| Email | contact@nzochain.com — subject `NZOChain Early Integration Program` |
| Developer Portal | https://developers.nzochain.com/ |
| First API call | [QUICKSTART.md](./QUICKSTART.md) |

After onboarding, explore [use cases](./use-cases/) that match your product and keep [SECURITY-AND-ROADMAP.md](./SECURITY-AND-ROADMAP.md) in view for roadmap versus live features.

---

## Related

- [QUICKSTART.md](./QUICKSTART.md)
- [PRODUCT-STATUS.md](./PRODUCT-STATUS.md)
- [PRICING.md](./PRICING.md)
- [integrations/README.md](./integrations/README.md)
- [SECURITY-AND-ROADMAP.md](./SECURITY-AND-ROADMAP.md)