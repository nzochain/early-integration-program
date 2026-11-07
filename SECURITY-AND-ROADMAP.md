# Security and Roadmap

NZOChain is committed to continuous security improvement for its public products and API surfaces.

This document separates **current** capabilities from **intentions** and **funding-dependent** goals.

---

## Independent security audit (intent)

> NZOChain intends to commission an independent security audit during the first half of 2027. Delivery of this goal depends on funding availability, recurring revenue growth or a liquidity event that makes the investment sustainable. The audit has not been contracted or scheduled.

**Português:**

> A NZOChain pretende realizar uma auditoria de segurança independente durante o primeiro semestre de 2027. A concretização deste objetivo dependerá da disponibilidade de financiamento, do crescimento da receita recorrente ou de um evento de liquidez que torne o investimento sustentável. A auditoria ainda não foi contratada nem agendada.

Conditions that may enable the audit investment include, for example:

- Sufficient recurring revenue
- A liquidity event
- Financing or resource availability that justifies the spend

This statement describes intent only. It is not a completed audit, a contracted engagement, a certification or a security guarantee.

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
- Any SLA / uptime commitments (not part of the public catalog)

Ship dates are published only when they are approved for public communication.

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
