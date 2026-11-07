# Security and Roadmap

NZOChain is committed to continuous security improvement for its public products and API surfaces.

This document separates **current** capabilities from **intentions** and **funding-dependent** goals.

---

## Independent security audit (intent)

**English (required wording):**

> NZOChain is targeting an independent security audit during the first half of 2027, subject to funding, recurring revenue and liquidity conditions that make the investment sustainable. No audit has been contracted or scheduled at this stage.

**Português (mesmo grau de compromisso):**

> A NZOChain pretende uma auditoria de segurança externa independente durante o primeiro semestre de 2027, sujeita a financiamento, receita recorrente e condições de liquidez que tornem o investimento sustentável. Nenhuma auditoria foi contratada ou agendada nesta fase.

Conditions that may enable the audit investment include, for example:

- Sufficient recurring revenue
- A liquidity event
- Financing or resource availability that justifies the spend

### Do not describe this as

- A completed audit
- A contracted audit
- A certification
- A security guarantee

---

## Roadmap status bands

### Available today

- Wallet risk scanning (API + app flows)
- Contract risk analysis
- Transaction analysis (Transaction Firewall) on eligible B2B plans
- Transaction simulation on eligible plans (live path may depend on Tenderly configuration; otherwise static / degraded analysis)
- Threat intelligence on Growth+ plans (standard / full by tier; Enterprise pilot-grade multi-source by contract)
- Approval risk review and **user-authorized** revocation
- B2B webhook event: `revocation.completed`
- REST API integration (no official SDK)

### Evolving

- Documentation coverage and integration examples (this repository)
- Developer Portal UX for keys, quotas and webhooks
- Risk signal quality and triage rules (heuristic / multi-source)

### Planned / roadmap (not live)

- Webhook events `wallet.scan.completed` and `risk.alert` (roadmap — not live)
- Broader webhook catalog beyond `revocation.completed`
- Future AI-assisted scoring explorations (not a current confirmed product claim)

### Dependent on validation or funding

- Independent external security audit (H1 2027 target — conditional)
- Enterprise commercial packaging beyond the public catalog
- Any SLA / uptime commitments (not advertised in the public catalog)

Precise feature ship dates that are not approved must not be announced here.

---

## Security practices for integrators

- Keep API keys server-side only.
- Use environment variables and rotate keys if exposed.
- Verify webhook HMAC signatures (`X-NZOChain-Signature`).
- Treat RiskScore and `decision` as **advisory**, not custody or insurance.
- Never revoke approvals without the wallet owner’s signature.

---

## Related

- [PRODUCT-STATUS.md](./PRODUCT-STATUS.md)
- [api/webhooks.md](./api/webhooks.md)
- [EARLY-INTEGRATION-PROGRAM.md](./EARLY-INTEGRATION-PROGRAM.md)
