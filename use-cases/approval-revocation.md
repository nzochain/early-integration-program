# Use case: approval revocation

Review risky token approvals and revoke them **only** with the wallet owner’s authorization.

**NZOChain never revokes approvals without the holder’s signature.** A revoke takes effect only after on-chain confirmation.

---

## Flow (available product behaviour)

1. **Identify risky permissions** — review active approvals (unlimited vs capped; spender risk).
2. **Review the permission** — inspect spender, token, amount/cap and risk assessment.
3. **Prepare the revocation transaction** — product prepares the revoke tx for confirmation.
4. **User signs in their wallet** — MetaMask, WalletConnect or other supported EVM connectors.
5. **On-chain confirmation** — wait for blockchain confirmation.
6. **Persist result in history** — confirmed revokes leave the active list / appear in history; B2B webhooks may emit `revocation.completed`.

Public feature docs: https://docs.nzochain.com/features/permission-revoke

---

## Plan notes (B2C app)

Per public docs:

- Users can review approvals with basic risk flagging on lower tiers.
- Full approval revocation (single and bulk) through NZOChain is documented for **Pro** and **Premium**.
- Always confirm live app entitlements at https://app.nzochain.com/

Integrators building B2B products should not assume every B2C entitlement maps 1:1 to API scopes.

---

## B2B webhook

When a revocation is confirmed on-chain, projects subscribed to webhooks may receive:

**Event (live):** `revocation.completed`

Headers:

- `X-NZOChain-Signature: sha256=<hmac>`
- `X-NZOChain-Event: revocation.completed`

Details: [api/webhooks.md](../api/webhooks.md)

Roadmap (not live): `wallet.scan.completed`, `risk.alert`.

---

## Networks

Scan and revoke cover the four EVM networks: Ethereum, BNB Chain, Polygon, Arbitrum. Solana is not a supported scan network.

---

## Related

- [api/webhooks.md](../api/webhooks.md)
- [PRODUCT-STATUS.md](../PRODUCT-STATUS.md)
